---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/govern/gateways/set-up-gke-egress
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/gateways/set-up-gke-egress
title: Set up agent egress governance on GKE
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

> **Preview**
>
> This product or feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](https://docs.cloud.google.com/terms/service-terms#1) . Pre-GA products and features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

This document shows you how to configure Agent Gateway for Google Kubernetes Engine (GKE) to govern and secure outbound (egress) traffic from the self-managed AI agents running on your GKE cluster.

To establish a complete egress data path, you combine several Google Cloud and GKE networking services. This setup routes your agent traffic through a secure forward proxy that enforces your policies and sanitizes content.

To secure your outbound agent traffic, complete the following steps:

1.  [Enable the GKE ambient proxy](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/gateways/set-up-gke-egress#enable-gke-ambient) .
2.  [Create a Secure Web Proxy](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/gateways/set-up-gke-egress#create-swp-name) .
3.  [Configure mTLS authentication](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/gateways/set-up-gke-egress#configure-mtls) .
4.  [Create an egress Agent Gateway](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/gateways/set-up-gke-egress#create-egress-gateway) .
5.  [Configure egress redirection in GKE](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/gateways/set-up-gke-egress#configure-egress-redirection) .
6.  [Configure authorization and content security policies](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/gateways/set-up-gke-egress#configure-auth-csp) .

To learn more about this architecture, see [Agent Gateway on GKE overview](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/gateways/gke-overview) .

## Before you begin

Before you configure egress governance, complete the following prerequisites:

1.  Complete the common prerequisites in [Agent Gateway on GKE overview](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/gateways/gke-overview#prereqs) .

2.  Workload configuration: register your workloads with Agent Registry and deploy them with a SPIFFE identity. Save the following as `agent.yaml` and apply it to your cluster:

    ```
    apiVersion: v1
    kind: ServiceAccount
    metadata:
      name: KSA_NAME
      namespace: NAMESPACE
    ---
    apiVersion: apps/v1
    kind: Deployment
    metadata:
      name: AGENT_NAME
      namespace: NAMESPACE
      labels:
        # Identifies the workload as an AI agent
        registry.gke.io/functional-type: "AGENT"
    spec:
      replicas: 1
      selector:
        matchLabels:
          app: AGENT_NAME
      template:
        metadata:
          labels:
            app: AGENT_NAME
          annotations:
            # Indicates that the agent uses Agent Identity
            iam.gke.io/spiffe-identity-type: "agent-identity"
            # To assign an agent identity and per-Pod credentials to a workload
            iam.gke.io/identity: "spiffe://TRUST_DOMAIN/*"
        spec:
          serviceAccountName: KSA_NAME
          containers:
          - name: curl
            image: curlimages/curl:8.10.1
            command: ["sleep", "infinity"]
    ```

    > **Note:** This manifest uses a curl container to help you verify your configuration. Before deploying to production, replace the curl image with your AI agent's container image.

    Replace the following:

    - `KSA_NAME` : the name of the Kubernetes service account.
    - `NAMESPACE` : the namespace for the service account.
    - `AGENT_NAME` : the name of the agent deployment.
    - `AGENT_IMAGE` : the container image for the agent.
    - `CONTAINER_NAME` : the name of the agent container.
    - `ORG_ID` : the ID of your Google Cloud organization.

    > **Note:** If your agent application code needs to call Google Cloud APIs directly by using bound tokens from the metadata server, or perform direct Agent-to-Agent (A2A) mTLS authentication, you must also add the `iam.gke.io/inject-podcertificates: "true"` annotation to your Pod template.

## Enable the GKE ambient proxy

To redirect traffic from your agents, Agent Gateway uses the sidecar-less GKE ambient proxy.

1.  Prepare your cluster by following the instructions in [Prepare a cluster for Ambient networking](https://docs.cloud.google.com/kubernetes-engine/docs/how-to/prepare-ambient-networking) .

2.  Create a namespace for your agent workloads:

    ```
    kubectl create namespace NAMESPACE
    ```

    Replace `NAMESPACE` with a name for your namespace—for example, `agent-ns` .

3.  Add the Ambient label to the namespace that contains your agent workloads:

    ```
    kubectl label namespace NAMESPACE networking.gke.io/dataplane-mode=ambient
    ```

    Replace `NAMESPACE` with the name of your agent namespace—for example, `agent-ns` .

## Create a Secure Web Proxy

To enforce your security policies and perform the TLS inspection required for Agent Gateway guardrails, you must provision a Secure Web Proxy (SWP) alongside the necessary certificates, Certificate Authority (CA) pools, and gateway security policies.

1.  Create a proxy-only subnet. Secure Web Proxy requires one active proxy-only subnet per region and VPC network. If your network already has an active proxy-only subnet in your region, you can skip this step.

    ```
    gcloud compute networks subnets create PROXY_SUBNET_NAME \
        --purpose=REGIONAL_MANAGED_PROXY \
        --role=ACTIVE \
        --region=REGION \
        --network=NETWORK \
        --range=10.10.0.0/24
    ```

    Replace the following:

    - `PROXY_SUBNET_NAME` : a name for the subnet—for example, `gateway-subnet` .
    - `REGION` : the region for the subnet.
    - `NETWORK` : the name of your VPC network.

    > **Note:** When you provision the Secure Web Proxy later in this guide, Google Cloud automatically creates a Cloud Router and Cloud NAT gateway to provide it with outbound internet access.

2.  Generate a self-signed certificate and private key:

    ```
    openssl req -x509 -newkey rsa:2048 -nodes \
        -keyout CERT_KEY_FILE.key \
        -out CERT_FILE.crt \
        -days CERT_VALIDITY_DAYS \
        -subj "/CN=SWP_HOSTNAME" \
        -addext "subjectAltName=DNS:SWP_HOSTNAME"
    ```

    Replace the following:

    - `CERT_KEY_FILE` and `CERT_FILE` : local file names for the private key and certificate—for example, `swp` .
    - `CERT_VALIDITY_DAYS` : how long the certificate is valid—for example, `365` .
    - `SWP_HOSTNAME` : a hostname for the proxy certificate—for example, `swp.example.internal` . (Agents don't connect to the proxy by this name, so any internal name works for testing).

3.  Upload the certificate to Certificate Manager in the same region as your SWP:

    ```
    gcloud certificate-manager certificates create CERTIFICATE_NAME \
        --location=REGION \
        --certificate-file=CERT_FILE.crt \
        --private-key-file=CERT_KEY_FILE.key
    ```

    Replace the following:

    - `CERTIFICATE_NAME` : a name for the certificate—for example, `swp-cert` .
    - `REGION` : the region for the certificate.
    - `CERT_FILE` and `CERT_KEY_FILE` : the local file names for the certificate and private key that you created earlier.

4.  Create a CA Pool and a root CA:

    ```
    gcloud privateca pools create CA_POOL_NAME \
        --location=REGION \
        --tier=devops

    gcloud privateca roots create ROOT_CA_NAME \
        --pool=CA_POOL_NAME \
        --location=REGION \
        --subject="CN=CA_COMMON_NAME, O=ORGANIZATION" \
        --key-algorithm=rsa-pkcs1-4096-sha256 \
        --max-chain-length=1 \
        --auto-enable
    ```

    Replace the following:

    - `CA_POOL_NAME` : a name for the CA pool—for example, `swp-ca-pool` .
    - `ROOT_CA_NAME` : a name for the root CA—for example, `swp-root-ca` .
    - `CA_COMMON_NAME` : a common name for the CA—for example, `swp-ca` .
    - `ORGANIZATION` : the name of your organization—for example, `My Company` .

5.  Allow the Network Security Service agent to issue certificates from the pool:

    ```
    gcloud beta services identity create --service=networksecurity.googleapis.com

    gcloud privateca pools add-iam-policy-binding CA_POOL_NAME \
        --location=REGION \
        --member="serviceAccount:service-PROJECT_NUMBER@gcp-sa-networksecurity.iam.gserviceaccount.com" \
        --role=roles/privateca.certificateManager
    ```

    Replace the following:

    - `PROJECT_NUMBER` : your project number. `PROJECT_NUMBER` with your project number.
    - `REGION` : the region for the CA pool.
    - `CA_POOL_NAME` : the name of the CA pool.

6.  Export the CA certificate. The TrustConfig uses this in a later step:

    ```
    gcloud privateca pools get-ca-certs CA_POOL_NAME \
        --location=REGION \
        --output-file=CA_CERT_FILE.pem
    ```

    Replace the following:

    - `CA_POOL_NAME` : the name of the CA pool.
    - `REGION` : the region for the CA pool.
    - `CA_CERT_FILE` with a local filename for the certificate—for example, `swp-ca-cert` .

7.  Create a TLS Inspection Policy.

    1.  Save the following as `tls-inspection.yaml` :

        ```
        name: projects/PROJECT_ID/locations/REGION/tlsInspectionPolicies/TLS_INSPECTION_POLICY_NAME
        caPool: projects/PROJECT_NUMBER/locations/REGION/caPools/CA_POOL_NAME
        ```

    2.  Import the policy:

        ```
        gcloud network-security tls-inspection-policies import TLS_INSPECTION_POLICY_NAME \
            --location=REGION \
            --source=tls-inspection.yaml
        ```

        Replace the following:

        - `TLS_INSPECTION_POLICY_NAME` with a name for the TLS inspection policy—for example, `swp-tls-inspection` .
        - `REGION` : the region for the policy.
        - `CA_POOL_NAME` : the name of the CA pool.
        - `PROJECT_NUMBER` : your project number.

        > **Note:** If you're using the Google Cloud console, you can create the TLS inspection policy without using a manifest.

8.  Generate a TrustConfig from the exported CA certificate and import it:

    ```
    { echo "trustStores:"; echo "- trustAnchors:"; echo "  - pemCertificate: |"; \
      sed 's/^/      /' CA_CERT_FILE.pem; } > trust-config.yaml

    gcloud certificate-manager trust-configs import TRUST_CONFIG_NAME \
        --location=REGION \
        --source=trust-config.yaml
    ```

    Replace the following:

    - `TRUST_CONFIG_NAME` : a name for the trust config—for example, `swp-trust-config` .
    - `REGION` : the region for the trust config.
    - `CA_CERT_FILE` : the local filename for the CA certificate that you exported earlier.

9.  Create a gateway security policy and an allow-all rule:

    1.  Save the policy as `swp-policy.yaml` :

        ```
        name: projects/PROJECT_ID/locations/REGION/gatewaySecurityPolicies/POLICY_NAME
        description: POLICY_DESCRIPTION
        tlsInspectionPolicy: projects/PROJECT_NUMBER/locations/REGION/tlsInspectionPolicies/TLS_INSPECTION_POLICY_NAME
        ```

    2.  Import the policy:

        ```
        gcloud network-security gateway-security-policies import POLICY_NAME \
            --location=REGION \
            --source=swp-policy.yaml
        ```

    3.  Save the rule as `rule.yaml` :

        ```
        name: projects/PROJECT_ID/locations/REGION/gatewaySecurityPolicies/POLICY_NAME/rules/RULE_NAME
        priority: RULE_PRIORITY
        enabled: true
        sessionMatcher: "SESSION_MATCHER"
        applicationMatcher: "APPLICATION_MATCHER"
        basicProfile: ALLOW
        tlsInspectionEnabled: true
        ```

    4.  Import the rule:

        ```
        gcloud network-security gateway-security-policies rules import RULE_NAME \
            --gateway-security-policy=POLICY_NAME \
            --location=REGION \
            --source=rule.yaml
        ```

        > **Note:** For testing, `SESSION_MATCHER` can be `true` and `APPLICATION_MATCHER` can be `request.method != ''` to match all requests.

10. Create a Server TLS Policy for mTLS. Save the following as `server-tls.yaml` :

    ```
    name: projects/PROJECT_ID/locations/REGION/serverTlsPolicies/SERVER_TLS_POLICY_NAME
    allowOpen: false
    mtlsPolicy:
      clientValidationMode: ALLOW_INVALID_OR_MISSING_CLIENT_CERT
      clientValidationTrustConfig: projects/PROJECT_NUMBER/locations/REGION/trustConfigs/TRUST_CONFIG_NAME
    ```

    Import the policy:

    ```
    gcloud network-security server-tls-policies import SERVER_TLS_POLICY_NAME \
        --location=REGION \
        --source=server-tls.yaml
    ```

    Replace the following:

    - `SERVER_TLS_POLICY_NAME` : a name for the policy—for example, `swp-server-tls` .
    - `TRUST_CONFIG_NAME` : the name of the TrustConfig you created earlier (for example, `swp-trust-config` ).

11. Create the Secure Web Proxy.

    1.  Save the following manifest as `swp.yaml` :

        ```
        name: projects/PROJECT_ID/locations/REGION/gateways/SWP_NAME
        type: SECURE_WEB_GATEWAY
        addresses: ["IP_ADDRESS"]
        ports: [443, 80]
        certificateUrls: ["projects/PROJECT_ID/locations/REGION/certificates/CERTIFICATE_NAME"]
        serverTlsPolicy: projects/PROJECT_ID/locations/REGION/serverTlsPolicies/SERVER_TLS_POLICY_NAME
        gatewaySecurityPolicy: projects/PROJECT_ID/locations/REGION/gatewaySecurityPolicies/POLICY_NAME
        network: projects/PROJECT_ID/global/networks/NETWORK
        subnetwork: projects/PROJECT_ID/regions/REGION/subnetworks/SUBNETWORK
        routingMode: EXPLICIT_ROUTING_MODE
        ```

    2.  Import the proxy:

        ```
        gcloud network-services gateways import SWP_NAME \
            --source=swp.yaml \
            --location=REGION
        ```

    Replace the following:

    - `IP_ADDRESS` : an IP address for the proxy.
    - `CERTIFICATE_NAME` : the name of the Certificate Manager certificate you created earlier (for example, `swp-cert` ).
    - `NETWORK` : the name of the VPC network.
    - `SUBNETWORK` : the name of the subnetwork.
    - `EXPLICIT_ROUTING_MODE` : the routing mode. For Agent Gateway, this must be `EXPLICIT_ROUTING_MODE` .
    - `SERVER_TLS_POLICY_NAME` : the name of your Server TLS policy.

## Configure mTLS authentication

To authenticate traffic between the GKE ambient proxy and your Secure Web Proxy, configure mutual TLS (mTLS). When you use Workload Identity Federation for GKE, your Workload Identity Federation for GKE pool is already configured with the default shared certificate authority (CA).

To verify this configuration, run the following command:

```
gcloud iam workload-identity-pools describe PROJECT_ID.svc.id.goog \
    --location=global \
    --format="yaml(inlineCertificateIssuanceConfig)"
```

Replace `PROJECT_ID` with your project ID.

In the output, verify that `useDefaultSharedCa` is set to `true` . The expected output looks similar to the following:

```
inlineCertificateIssuanceConfig:
  keyAlgorithm: ECDSA_P256
  lifetime: 86400s
  rotationWindowPercentage: 50
  useDefaultSharedCa: true
```

If `useDefaultSharedCa: true` is missing or set to `false` , run the following command to configure it:

```
gcloud iam workload-identity-pools update PROJECT_ID.svc.id.goog \
    --location=global \
    --use-default-shared-ca
```

## Create an egress Agent Gateway

Create an egress Agent Gateway resource in Agent Platform and connect it to your Secure Web Proxy.

1.  Save the following manifest as a file named `agent-gateway.yaml` :

    ```
    name: GATEWAY_NAME
    protocols:
    - MCP
    registries: ["//agentregistry.googleapis.com/projects/PROJECT_ID/locations/REGION"]
    selfManaged:
      resourceUris:
      - "projects/PROJECT_ID/locations/REGION/gateways/SWP_NAME"
    ```

    Replace the following:

    - `GATEWAY_NAME` with a name for the Gateway—for example, `my-agent-egress-gateway` .
    - `PROJECT_ID` : your Google Cloud project ID.
    - `REGION` : the region for the Gateway.
    - `SWP_NAME` : the name of your Secure Web Proxy.

2.  Create the Gateway:

    ```
    gcloud beta network-services agent-gateways import GATEWAY_NAME \
        --source=agent-gateway.yaml \
        --location=REGION
    ```

    Replace the following:

    - `GATEWAY_NAME` : a name for the Gateway—for example, `my-agent-egress-gateway` .
    - `REGION` : the region for the Gateway.

3.  To verify that the AgentGateway resource was created, describe the Gateway:

    ```
    gcloud beta network-services agent-gateways describe GATEWAY_NAME \
        --location=REGION
    ```

    Replace the following:

    - `GATEWAY_NAME` : a name for the Gateway—for example, `my-agent-egress-gateway` .
    - `REGION` : the region for the Gateway.

## Configure egress redirection in GKE

To route your outbound agent traffic to your Secure Web Proxy, define the proxy's location for the GKE ambient proxy.

1.  Save the following manifest as a file named `swp-backend.yaml` . You must create the `GCPBackend` resource in the same namespace as your agent workloads.

    If your Secure Web Proxy is in the same VPC as your cluster, use the gateway URI:

    ```
    apiVersion: networking.gke.io/v1
    kind: GCPBackend
    metadata:
      name: swp-backend
      namespace: NAMESPACE
    spec:
      serviceUris:
      - "//networkservices.googleapis.com/projects/PROJECT_ID/locations/REGION/gateways/SWP_NAME"
    ```

    Alternatively, if your proxy is in a different VPC and uses Private Service Connect, use the service attachment URI:

    ```
    apiVersion: networking.gke.io/v1
    kind: GCPBackend
    metadata:
      name: swp-backend
      namespace: NAMESPACE
    spec:
      serviceUris:
      - "//compute.googleapis.com/projects/PROJECT_ID/regions/REGION/serviceAttachments/ATTACHMENT_NAME"
    ```

    Replace the following:

    - `NAMESPACE` : the namespace for your agent workloads.
    - `PROJECT_ID` : your Google Cloud project ID.
    - `REGION` : the region for the proxy or service attachment.
    - `SWP_NAME` : the name of your proxy (for same-VPC setups).
    - `ATTACHMENT_NAME` : the name of the Private Service Connect service attachment (for cross-VPC setups).

2.  Apply the manifest to your cluster:

    ```
    kubectl apply -f swp-backend.yaml
    ```

3.  Get your cluster's Service IPv4 CIDR range:

    ```
    gcloud container clusters describe CLUSTER_NAME \
        --location=LOCATION \
        --format="value(ipAllocationPolicy.servicesIpv4Cidr)"
    ```

    Replace the following:

    - `CLUSTER_NAME` : the name of your GKE cluster.
    - `LOCATION` : the cluster's location.

4.  Save the following manifest as a file named `egress-policy.yaml` :

    ```
    apiVersion: networking.gke.io/v1
    kind: GCPEgressPolicy
    metadata:
      name: prod-egress-policy
      namespace: NAMESPACE
    spec:
      to:
        excludeCIDRRanges:
          - SERVICE_CIDR
          - VPC_CIDR
      proxyRef:
        group: networking.gke.io
        kind: GCPBackend
        name: swp-backend
    ```

    Replace the following:

    - `SERVICE_CIDR` : the cluster Service CIDR from the previous step—for example, `34.118.224.0/20` .
    - `VPC_CIDR` : other internal ranges that shouldn't go through the proxy—for example, `10.0.0.0/8` .

    To prevent internal traffic, such as communication with the Kubernetes control plane, from routing through the proxy, use the `excludeCIDRRanges` field.

5.  Apply the manifest to your cluster:

    ```
    kubectl apply -f egress-policy.yaml
    ```

    The GKE Ambient data plane now routes egress traffic from your agent namespace to your Secure Web Proxy for policy enforcement.

## (Optional) Deploy test clients

To verify that your egress policies are working correctly, you can deploy a test agent with a registered SPIFFE identity (the positive control) and a plain client without an identity (the negative control).

1.  Save the following manifest as `agents.yaml` :

    ```
    apiVersion: v1
    kind: ServiceAccount
    metadata:
      name: agent-sa
      namespace: NAMESPACE
    ---
    apiVersion: apps/v1
    kind: Deployment
    metadata:
      name: test-agent
      namespace: NAMESPACE
      labels:
        registry.gke.io/functional-type: "AGENT"
    spec:
      replicas: 1
      selector:
        matchLabels:
          app: test-agent
      template:
        metadata:
          labels:
            app: test-agent
          annotations:
            iam.gke.io/spiffe-identity-type: "agent-identity"
            iam.gke.io/identity: "spiffe://agents.global.org-ORG_ID.system.id.goog/*"
        spec:
          serviceAccountName: agent-sa
          containers:
          - name: curl
            image: curlimages/curl:8.10.1
            command: ["sleep", "infinity"]
    ---
    apiVersion: apps/v1
    kind: Deployment
    metadata:
      name: plain-client
      namespace: NAMESPACE
    spec:
      replicas: 1
      selector:
        matchLabels:
          app: plain-client
      template:
        metadata:
          labels:
            app: plain-client
        spec:
          containers:
          - name: curl
            image: curlimages/curl:8.10.1
            command: ["sleep", "infinity"]
    ```

    Replace the following:

    - `NAMESPACE` : your agent namespace.
    - `ORG_ID` : the ID of your Google Cloud organization.

2.  Apply the deployments and wait for them to become ready:

    ```
    kubectl apply -f agents.yaml
    kubectl rollout status deploy/test-agent deploy/plain-client -n NAMESPACE
    ```

3.  Copy the Secure Web Proxy CA certificate into both Pods so they can securely connect through the proxy during testing:

    ```
    B64=$(base64 -w0 CA_CERT_FILE.pem)

    for p in test-agent plain-client; do
      kubectl exec -i -n NAMESPACE deploy/"$p" -- sh -c "cat > /tmp/swp-ca.pem" < CA_CERT_FILE.pem
    done
    ```

    Replace `CA_CERT_FILE` with the local name of the CA certificate you exported during the Secure Web Proxy setup.

## Configure authorization and content security policies

To enforce access controls and sanitize content, forward your outbound traffic to extension services, such as Identity-Aware Proxy (IAP) (IAP) or Model Armor, before it reaches its destination.

You can then delegate authorization to IAP or a custom authorization engine, and delegate content sanitization to Model Armor.

### Delegate authorization to IAP

To authorize your outbound requests by using IAP, bind the extension to your Gateway.

1.  Save the following match conditions as a file named `match.yaml` to define which traffic routes to IAP. For example, to evaluate traffic to example.com during testing:

    ```
    name: ext-binding
    producerExtension: iap.googleapis.com
    target:
      resources:
      - "//networkservices.googleapis.com/projects/PROJECT_ID/locations/REGION/agentGateways/GATEWAY_NAME"
    matchConditions:
    # invoke IAP for traffic to example.com for testing
    - to:
        destination:
          hosts:
          - exact: "example.com"
    ```

2.  Import the extension binding:

    ```
    gcloud beta service-extensions extension-bindings import my-iap-binding \
        --source=match.yaml \
        --location=REGION
    ```

    Replace `REGION` with the region for the extension binding.

3.  To verify your IAP response, run the following test commands:

    ```
    echo -n "no identity -> example.com: "; kubectl exec -n NAMESPACE deploy/plain-client -- curl -s -o /tmp/b -w "%{http_code} " --cacert /tmp/swp-ca.pem https://example.com/; kubectl exec -n NAMESPACE deploy/plain-client -- head -c 120 /tmp/b; echo
    echo -n "agent       -> example.com: "; kubectl exec -n NAMESPACE deploy/test-agent -- curl -s -o /tmp/b -w "%{http_code} " --cacert /tmp/swp-ca.pem https://example.com/; kubectl exec -n NAMESPACE deploy/test-agent -- head -c 120 /tmp/b; echo
    echo -n "agent       -> www.google.com (no IAP match): "; kubectl exec -n NAMESPACE deploy/test-agent -- curl -s -o /dev/null -w "%{http_code}\n" --cacert /tmp/swp-ca.pem https://www.google.com/
    ```

    Expected output:

    - **no identity → example.com:** 401, body... Error code 1200 (no token)
    - **agent → example.com:** 200 (Example Domain HTML). Right after binding IAP, you might first see 403 "Egress request is not authorized" for about 1–2 minutes while IAP propagates.
    - **agent → www.google.com:** 200 (the binding doesn't match, so IAP is skipped)

### Delegate content security to Model Armor

To protect against prompt injection and sensitive data leakage on outbound traffic, you can bind Google Cloud Model Armor to your egress Gateway.

1.  Grant the required roles to the Agent Gateway service account or the Service Extensions service account.

    > **Note:** For self-managed Gateways, this account uses the format `service- `` AGENT_GATEWAY_PROJECT_NUMBER `` @gcp-sa-dep.iam.gserviceaccount.com` .

    ```
    gcloud projects add-iam-policy-binding MODEL_ARMOR_PROJECT_ID \
        --member="serviceAccount:SERVICE_ACCOUNT" \
        --role="roles/modelarmor.calloutUser"

    gcloud projects add-iam-policy-binding MODEL_ARMOR_PROJECT_ID \
        --member="serviceAccount:SERVICE_ACCOUNT" \
        --role="roles/serviceusage.serviceUsageConsumer"

    gcloud projects add-iam-policy-binding MODEL_ARMOR_PROJECT_ID \
        --member="serviceAccount:SERVICE_ACCOUNT" \
        --role="roles/modelarmor.user"
    ```

    Replace the following:

    - `MODEL_ARMOR_PROJECT_ID` : the project ID where Model Armor is located.
    - `SERVICE_ACCOUNT` : the service account for the Gateway.

2.  Create a Model Armor template to filter sensitive data and prompt injection attacks. Our subsequent verification steps rely on this configuration:

    ```
    gcloud model-armor templates create TEMPLATE_NAME \
        --location=REGION \
        --basic-config-filter-enforcement=enabled \
        --pi-and-jailbreak-filter-settings-enforcement=enabled \
        --pi-and-jailbreak-filter-settings-confidence-level=MEDIUM_AND_ABOVE
    ```

    Replace `TEMPLATE_NAME` with a name for your template—for example, `safety-template` .

3.  To get the full resource path of your new template (which you need for the extension binding step), run the following command:

    ```
    gcloud model-armor templates describe TEMPLATE_NAME \
        --location=REGION \
        --format="value(name)"
    ```

    Replace `REGION` with the region for your template.

4.  Save the following match conditions as a file named `model-armor-match.yaml` to evaluate traffic to www.google.com during testing:

    ```
    - to:
        destination:
          hosts:
          - exact: "www.google.com"
    ```

5.  Bind Model Armor to your Gateway:

    ```
    gcloud beta service-extensions extension-bindings create my-model-armor-binding \
        --location=REGION \
        --producer-extension="modelarmor.REGION.rep.googleapis.com" \
        --target-resources="//networkservices.googleapis.com/projects/PROJECT_ID/locations/REGION/agentGateways/GATEWAY_NAME" \
        --fail-open \
        --match-conditions=model-armor-match.yaml \
        --producer-metadata=model_armor_settings='[{"request_template_id":"projects/TEMPLATE_PROJECT_ID/locations/REGION/templates/REQUEST_TEMPLATE","response_template_id":"projects/TEMPLATE_PROJECT_ID/locations/REGION/templates/RESPONSE_TEMPLATE"}]'
    ```

    Replace the following:

    - `REGION` : the region for your Agent Gateway. The binding and the Model Armor producer extension must use this same region, and Model Armor must be available in it. Other regions and the global `modelarmor.googleapis.com` endpoint aren't accepted.
    - `PROJECT_ID` : your Google Cloud project ID.
    - `GATEWAY_NAME` : the name of your Agent Gateway.
    - `TEMPLATE_PROJECT_ID` , `REQUEST_TEMPLATE` , and `RESPONSE_TEMPLATE` : the details for your Model Armor templates. The templates must be created in `REGION` . If a template doesn't exist in that region, matched requests fail with HTTP 404 "Not Found".

    **Note:** By default the binding fails closed (if Model Armor is unavailable, requests are blocked). The `--fail-open` flag allows traffic when the extension can't be reached.

6.  To verify Model Armor is filtering requests, run the following test commands:

    ```
    SENS='{"jsonrpc":"2.0","id":1,"method":"tools/call","params":{"name":"deploy-html","arguments":{"value":"<html> card 4111111111111111</html>"}}}'
    BEN='{"jsonrpc":"2.0","id":1,"method":"tools/call","params":{"name":"deploy-html","arguments":{"value":"Hello, how are you?"}}}'

    kubectl exec -n NAMESPACE deploy/test-agent -- curl -s -w " HTTP=%{http_code}\n" --cacert /tmp/swp-ca.pem -X POST -H 'Content-Type: application/json' -d "$SENS" "https://www.google.com/"
    kubectl exec -n NAMESPACE deploy/test-agent -- curl -s -o /dev/null -w "HTTP=%{http_code}\n" --cacert /tmp/swp-ca.pem -X POST -H 'Content-Type: application/json' -d "$BEN" "https://www.google.com/"
    ```

    Expected output:

    - **sensitive:** `403` `{"jsonrpc":"2.0","id":1,"result":{"content":[{"type":"text","text":"Traffic blocked by MA security policy."}],"isError":true}}`
    - **benign:** `405` (origin; it reached www.google.com)

### Delegate authorization to custom extensions

As an alternative to IAP, you can use custom extensions to delegate authorization decisions. For more information, see [Producers: Build and publish extensions](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/gateways/extension-bindings-overview#producer-setup) to create the appropriate `ProducerExtension` and `ExtensionBinding` .

## Troubleshoot

If you experience connectivity issues, verify the following configurations:

- **APIs:** verify that all required APIs are enabled in your project.
- **Namespace labels:** verify that your agent namespace has the `networking.gke.io/dataplane-mode=ambient` label.
- **Custom resources:** verify that the `GCPBackend` and `GCPEgressPolicy` custom resources applied without errors and are located in the same namespace as your agents.

## What's next

- To monitor your agents' traffic and behavior, see [Monitor Agent Gateway traffic](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/gateways/monitor-agent-gateway) .
- To resolve connectivity or policy issues, see [Troubleshoot Agent Gateway](https://docs.cloud.google.com/gemini-enterprise-agent-platform/troubleshooting/troubleshoot-agent-gateway) .
