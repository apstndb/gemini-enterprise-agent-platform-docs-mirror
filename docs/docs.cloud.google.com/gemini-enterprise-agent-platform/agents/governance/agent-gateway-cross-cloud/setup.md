---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/agents/governance/agent-gateway-cross-cloud/setup
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/agents/governance/agent-gateway-cross-cloud/setup
title: Set up Agent Gateway for cross-cloud
description: Learn how to set up and deploy Agent Gateway for cross-cloud on standard Kubernetes clusters.
data_source: docs.cloud.google.com
---

> **Preview**
>
> This feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](https://docs.cloud.google.com/terms/service-terms#1) . Pre-GA features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

> **Request access:** Agent Gateway for cross-cloud is available in Limited Preview. To use this feature, complete the [access request form](https://docs.google.com/forms/d/e/1FAIpQLSeUpnNRtYQjLRblii-KoUbJJ7DjEV6fvQAfO21IAXgVSqFjpw/viewform) .

This guide explains how to deploy Agent Gateway for cross-cloud on standard Kubernetes clusters to extend Gemini Enterprise Agent Platform governance to your environment. For an overview of the three-plane architecture, see the [Agent Gateway for cross-cloud overview](https://docs.cloud.google.com/gemini-enterprise-agent-platform/agents/governance/agent-gateway-cross-cloud/overview) .

## Before you begin

Before you begin, ensure that you have the following:

- A Cloud Native Computing Foundation (CNCF)-conformant Kubernetes cluster.
- An existing service mesh or network stack configured in your cluster.
- Outbound network connectivity from your cluster to Google Cloud APIs over HTTPS (TCP port `443` ).
- The Google Cloud CLI version 591.0.0 or later installed. To update to the latest version, run `gcloud components update` .
- The Identity and Access Management (IAM) roles on your Google Cloud project that you need to enable APIs, create a workload identity pool and provider, and grant IAM roles.

## Enable APIs and register the cluster

Enable the required Google Cloud APIs, and then register your external cluster.

### Enable the required APIs

To enable the APIs that Agent Gateway for cross-cloud requires, run the following command:

```
gcloud services enable \
    agentregistry.googleapis.com \
    apphubendpoint.googleapis.com \
    cloudresourcemanager.googleapis.com \
    cloudtrace.googleapis.com \
    iam.googleapis.com \
    iamcredentials.googleapis.com \
    iap.googleapis.com \
    logging.googleapis.com \
    modelarmor.googleapis.com \
    monitoring.googleapis.com \
    networkservices.googleapis.com \
    serviceextensions.googleapis.com \
    sts.googleapis.com \
    telemetry.googleapis.com \
    trafficdirector.googleapis.com \
    --project=PROJECT_ID
```

Replace `PROJECT_ID` with the ID of your Google Cloud project.

### Extract the Kubernetes API server public key

To register your cluster, you need the public key that your cluster uses to sign service account tokens. To extract the public key, do the following:

1.  Set your current `kubectl` context to the cluster that you want to register.

2.  Retrieve the JSON Web Key Set (JWKS) of your cluster, and then convert the first RSA key to a public key file named `pubkey.pem` :

    ```
    kubectl get --raw /openid/v1/jwks > cluster-jwks.json

    N_HEX=$(jq -r '[.keys[] | select((.kty // "" | ascii_upcase) == "RSA" and (.n // "") != "" and (.e // "") != "")][0].n | gsub("-";"+") | gsub("_";"/") | . + ("==="[:(4 - length % 4) % 4])' cluster-jwks.json | base64 -d | od -An -tx1 | tr -d ' \n')
    E_HEX=$(jq -r '[.keys[] | select((.kty // "" | ascii_upcase) == "RSA" and (.n // "") != "" and (.e // "") != "")][0].e | gsub("-";"+") | gsub("_";"/") | . + ("==="[:(4 - length % 4) % 4])' cluster-jwks.json | base64 -d | od -An -tx1 | tr -d ' \n')

    openssl asn1parse -genconf <(printf "asn1=SEQUENCE:rsa_key\n[rsa_key]\nmodulus=INTEGER:0x%s\nexponent=INTEGER:0x%s\n" "$N_HEX" "$E_HEX") -noout -out /dev/stdout \
      | openssl rsa -RSAPublicKey_in -inform DER -pubout -out pubkey.pem
    ```

    These commands require a Bash shell and the `jq` and `openssl` utilities.

### Register the cluster

To register your cluster, do the following:

1.  Retrieve the OpenID Connect (OIDC) issuer URL of your cluster:

    ```
    kubectl get --raw /.well-known/openid-configuration | jq -r '.issuer'
    ```

    The output is the value of the `--service-account-issuer` flag of your cluster's Kubernetes API server. This value might differ from the external URL of your Kubernetes API server. Copy the output exactly. Don't add or remove a trailing slash.

2.  Register the cluster:

    ```
    gcloud alpha network-services registered-clusters create CLUSTER_NAME \
        --project=PROJECT_ID \
        --location=LOCATION \
        --oidc-issuer-url=OIDC_ISSUER_URL \
        --api-server-public-key="$(cat pubkey.pem)"
    ```

    Replace the following:

    - `CLUSTER_NAME` : a name for the registered cluster.
    - `PROJECT_ID` : the ID of your Google Cloud project.
    - `LOCATION` : the Google Cloud region for the registered cluster—for example, `us-central1` .
    - `OIDC_ISSUER_URL` : the exact issuer URL that you retrieved in the previous step. The URL must start with `https://` .

### Prevent accidental resource deletion

Deleting your Google Cloud project or unregistering a registered cluster while cross-cloud workloads are active disconnects in-cluster controllers and disrupts policy enforcement. To protect your Google Cloud resources from accidental deletion, apply the following safeguards:

- **Protect the Google Cloud project with liens** : Apply a [project lien](https://docs.cloud.google.com/resource-manager/docs/project-liens) to the Google Cloud project that hosts your registered cluster, [Agent Registry](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/agent-registry) , and federated identity pools to block accidental project deletion until all cross-cloud clusters are decommissioned.
- **Restrict destructive IAM permissions** : Limit permissions that can delete registered clusters or gateway resources (such as `networkservices.registeredClusters.delete` and `networkservices.agentGateways.delete` ) to dedicated platform administrator roles.
- **Retain Kubernetes resource finalizers** : Don't remove finalizers on in-cluster custom resources managed by the `agent-governance-cross-cloud-controller` controller. Finalizers ensure that corresponding Google Cloud control plane registrations are cleanly deprovisioned before local cluster resources are removed.
- **Delete custom resources before you remove the controller** : Before you uninstall the `agent-governance-cross-cloud` Helm chart or delete your Kubernetes cluster, delete all `GCPExtensionBinding` and `GCPAgentGateway` custom resources, and wait for the deletion to complete. If you remove the controller first, the corresponding Agent Gateway resource remains orphaned in Network Services. The orphaned gateway blocks deletion of the agent connectivity template and the registered cluster.

## Configure Workload Identity Federation

The in-cluster components of Agent Gateway for cross-cloud—the `agent-governance-cross-cloud-controller` controller, the telemetry collector, and the proxy—use Workload Identity Federation to authenticate to Google Cloud APIs. Each component exchanges its Kubernetes service account (KSA) token for a federated access token. You grant IAM roles directly to these federated identities, so you don't need to create Google Cloud service accounts or store service account keys in your cluster.

The Agent Identity Runtime (AIR) sidecar that runs with each proxy uses the workload identity pool to provide SPIFFE identities to your agent workloads. These identities are the [Agent Identities](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/agent-identity-overview) of your agents. Model Armor and IAP policies identify agents by their Agent Identity, not by the federated identities of the in-cluster components. For the principal format, see [Identify the agent principal](https://docs.cloud.google.com/gemini-enterprise-agent-platform/agents/governance/agent-gateway-cross-cloud/enforce-policies#identify-agent-principal) .

> **Important:** Don't grant Google Cloud project IAM roles to agent workload namespaces or agent Kubernetes service accounts on the workload identity pool. Only the dedicated control plane namespace ( `geap-system` ) and dedicated gateway namespace receive Google Cloud IAM role bindings. Don't run any other workloads in these namespaces. Agent workloads exchange their Kubernetes service account tokens only for scoped Agent Identities governed by IAP and Model Armor policies.

### Create a workload identity pool and provider

To create a workload identity pool and an OIDC provider for your cluster, do the following:

1.  If your cluster's OIDC issuer URL isn't publicly reachable, save the JSON Web Key Set (JWKS) of your cluster to a file:

    ```
    kubectl get --raw /openid/v1/jwks > cluster-jwks.json
    ```

    When you provide the JWKS to the provider, Google Cloud can verify KSA tokens without connecting to your cluster's OIDC issuer.

2.  Create a workload identity pool:

    ```
    gcloud iam workload-identity-pools create POOL_ID \
        --project=PROJECT_ID \
        --location=global \
        --display-name="POOL_DISPLAY_NAME"
    ```

3.  Create an OIDC provider in the pool:

    ```
    gcloud iam workload-identity-pools providers create-oidc PROVIDER_ID \
        --project=PROJECT_ID \
        --location=global \
        --workload-identity-pool=POOL_ID \
        --issuer-uri=OIDC_ISSUER_URL \
        --jwk-json-path=cluster-jwks.json \
        --attribute-mapping="google.subject=assertion.sub,attribute.namespace=assertion['kubernetes.io']['namespace'],attribute.service_account=assertion['kubernetes.io']['serviceaccount']['name']"
    ```

    > **Note:** If your cluster's OIDC issuer URL isn't publicly reachable, you must specify the `--jwk-json-path` flag. If the issuer is publicly reachable, you can omit the flag, and Google Cloud retrieves the JWKS from the issuer.

    Don't specify the `--allowed-audiences` flag. The cross-cloud components request tokens for the default audience, which is the full resource name of the provider: `//iam.googleapis.com/projects/ `` PROJECT_NUMBER `` /locations/global/workloadIdentityPools/ `` POOL_ID `` /providers/ `` PROVIDER_ID` .

Replace the following:

- `POOL_ID` : an ID for the workload identity pool.
- `PROJECT_ID` : your Google Cloud project ID.
- `POOL_DISPLAY_NAME` : a display name for the pool.
- `PROVIDER_ID` : an ID for the OIDC provider.
- `OIDC_ISSUER_URL` : the exact OIDC issuer URL that you retrieved when you [registered the cluster](https://docs.cloud.google.com/gemini-enterprise-agent-platform/agents/governance/agent-gateway-cross-cloud/setup#register-cluster) . This value must match the value that you passed to `--oidc-issuer-url` , including whether it ends with a trailing slash.

## Deploy the control plane

Use the provided Helm chart to deploy the in-cluster controller, `agent-governance-cross-cloud-controller` and telemetry collector in the `geap-system` namespace.

### Ensure connectivity for the controller

Ensure that your cluster firewall, proxy, egress rules, and network policies allow the following connectivity:

- **Google Cloud APIs** : The `agent-governance-cross-cloud-controller` controller pods and the telemetry collector must have outbound HTTPS and gRPC connectivity on TCP port `443` to `*.googleapis.com` .
- **Kubernetes API server** : The controller pods must be able to reach the Kubernetes API server to watch Kubernetes services, workloads, and custom resources.
- **Agent workloads in all namespaces** : The controller pods must be able to call agent and MCP server pods in any namespace in the cluster. The controller fetches the Agent Card from each agent workload to register the agent in Agent Registry.

### Grant IAM roles to the controller and telemetry collector

Grant IAM roles to the federated identities of the `agent-governance-cross-cloud-controller` controller and the telemetry collector, which run in the `geap-system` namespace:

- Satellite Operator ( `roles/networkservices.satelliteOperator` )
- Cloud Telemetry Writer ( `roles/telemetry.writer` )

> **Caution:** Every Kubernetes service account in the `geap-system` namespace receives these IAM roles. You must reserve `geap-system` exclusively for the control plane and telemetry components of Agent Gateway for cross-cloud:
>
> - Don't deploy agent workloads, MCP servers, or other application pods in `geap-system` .
> - Restrict Kubernetes RBAC permissions to create or modify pods, deployments, service accounts, and secrets in `geap-system` to trusted cluster administrators.
> - Set `automountServiceAccountToken: false` on the `default` service account in `geap-system` .

To grant the roles, run the following command:

```
for ROLE in \
    roles/networkservices.satelliteOperator \
    roles/telemetry.writer; do
  gcloud projects add-iam-policy-binding PROJECT_ID \
      --role="${ROLE}" \
      --member="principalSet://iam.googleapis.com/projects/PROJECT_NUMBER/locations/global/workloadIdentityPools/POOL_ID/attribute.namespace/geap-system"
done
```

Replace the following:

- `PROJECT_ID` : your Google Cloud project ID.
- `PROJECT_NUMBER` : your Google Cloud project number.
- `POOL_ID` : the ID of the [workload identity pool](https://docs.cloud.google.com/gemini-enterprise-agent-platform/agents/governance/agent-gateway-cross-cloud/setup#create-pool-provider) .

### Install the control plane Helm chart

To install the control plane, do the following:

1.  Install the `agent-governance-cross-cloud` Helm chart in the `geap-system` namespace:

    > **Important:** You must install the control plane in the `geap-system` namespace. The control plane doesn't support other namespaces, and the IAM role bindings that you granted in the previous section apply only to `geap-system` . Don't change the value of the `--namespace` flag.

    ```
    helm upgrade --install agent-governance-cross-cloud \
        oci://gcr.io/gke-release/agent-governance-cross-cloud \
        --version 0.1.0-preview \
        --namespace geap-system \
        --create-namespace \
        --set gcp.projectId=PROJECT_ID \
        --set-string gcp.projectNumber=PROJECT_NUMBER \
        --set-string gcp.orgId=ORGANIZATION_ID \
        --set gcp.location=LOCATION \
        --set gcp.registeredCluster=CLUSTER_NAME \
        --set gcp.workloadIdentityPool=POOL_ID \
        --set gcp.identityProvider=PROVIDER_ID
    ```

    Replace the following:

    - `PROJECT_ID` : your Google Cloud project ID.
    - `PROJECT_NUMBER` : your Google Cloud project number.
    - `ORGANIZATION_ID` : the ID of your Google Cloud organization. If your project isn't associated with an organization, omit the `--set-string gcp.orgId` flag.
    - `LOCATION` : the region where you [registered the cluster](https://docs.cloud.google.com/gemini-enterprise-agent-platform/agents/governance/agent-gateway-cross-cloud/setup#register-cluster) —for example, `us-central1` .
    - `CLUSTER_NAME` : the name of the registered cluster.
    - `POOL_ID` : the ID of the [workload identity pool](https://docs.cloud.google.com/gemini-enterprise-agent-platform/agents/governance/agent-gateway-cross-cloud/setup#create-pool-provider) .
    - `PROVIDER_ID` : the ID of the [workload identity pool provider](https://docs.cloud.google.com/gemini-enterprise-agent-platform/agents/governance/agent-gateway-cross-cloud/setup#create-pool-provider) .

    If your cluster's nodes have taints—for example, arm64 nodes on most cloud providers, including Google Cloud, AWS, and Azure—set pod tolerations in the `k8s.tolerations` Helm value. The tolerations apply to the controller, the OpenTelemetry (OTel) collector, and the gateway deployments that the controller creates. For example, save the following as `tolerations-values.yaml` , and then add `--values tolerations-values.yaml` to the preceding command:

    ```
    k8s:
      tolerations:
      - key: "kubernetes.io/arch"
        operator: "Equal"
        value: "arm64"
        effect: "NoSchedule"
    ```

    > **Caution:** Set tolerations before you create a `GCPAgentGateway` resource. Running `helm upgrade` updates the controller and OTel collector deployments, but the controller doesn't update existing gateway deployments. If you add tolerations after you create a gateway, see [Add tolerations to existing gateways](https://docs.cloud.google.com/gemini-enterprise-agent-platform/agents/governance/agent-gateway-cross-cloud/setup#add-tolerations) .

2.  Wait for the controller deployment to become ready:

    ```
    kubectl rollout status deployment/agent-governance-cross-cloud-controller \
        --namespace geap-system --timeout=180s
    ```

## Deploy the data plane

Deploy the Agent Gateway for cross-cloud proxy (Envoy proxy) by creating a `GCPAgentGateway` custom resource. The proxy inspects traffic and enforces policies for the agent workloads that it governs. Each proxy runs with an Agent Identity Runtime (AIR) sidecar that brokers workload identities, Secret Discovery Service (SDS) certificates, and local token exchange for the proxy.

You must deploy Agent Gateway for cross-cloud in a dedicated namespace (for example, `agent-gateway-system` ) that contains no agent workloads, MCP servers, or other application pods. A single gateway in this dedicated namespace can govern outbound traffic from agent workloads across your cluster.

### Grant IAM roles to the gateway

Grant IAM roles to the federated identities of the Agent Gateway for cross-cloud proxy. The binding applies to all KSAs in the gateway namespace, so grant these roles for each gateway namespace:

- Traffic Director Client ( `roles/trafficdirector.client` )
- App Hub Endpoint Viewer ( `roles/apphubendpoint.viewer` )
- Agent Registry Viewer ( `roles/agentregistry.viewer` )
- Service Extensions Editor ( `roles/serviceextensions.editor` ), which lets the proxy call Service Extensions policy callouts

> **Caution:** Every Kubernetes service account in `GATEWAY_NAMESPACE` receives these IAM roles, and pods in that namespace can mount the gateway's TLS inspection CA `Secret` . Enforce the following controls on `GATEWAY_NAMESPACE` :
>
> - Don't deploy agent workloads, MCP servers, or any other non-gateway pods in `GATEWAY_NAMESPACE` .
> - Restrict Kubernetes RBAC permissions to create or modify pods, workload controllers, service accounts, and secrets in `GATEWAY_NAMESPACE` to trusted cluster administrators and the `agent-governance-cross-cloud-controller` service account.
> - Set `automountServiceAccountToken: false` on the `default` service account in `GATEWAY_NAMESPACE` .

To grant the roles, run the following command:

```
for ROLE in \
    roles/trafficdirector.client \
    roles/apphubendpoint.viewer \
    roles/agentregistry.viewer \
    roles/serviceextensions.editor; do
  gcloud projects add-iam-policy-binding PROJECT_ID \
      --role="${ROLE}" \
      --member="principalSet://iam.googleapis.com/projects/PROJECT_NUMBER/locations/global/workloadIdentityPools/POOL_ID/attribute.namespace/GATEWAY_NAMESPACE"
done
```

Replace the following:

- `PROJECT_ID` : your Google Cloud project ID.
- `PROJECT_NUMBER` : your Google Cloud project number.
- `POOL_ID` : the ID of the [workload identity pool](https://docs.cloud.google.com/gemini-enterprise-agent-platform/agents/governance/agent-gateway-cross-cloud/setup#create-pool-provider) .
- `GATEWAY_NAMESPACE` : a dedicated namespace for the gateway. This namespace must not contain agent workloads.

> **Note:** If you want to scope the binding to a single gateway service account instead of the dedicated gateway namespace, set `--member` to `principal://iam.googleapis.com/projects/ `` PROJECT_NUMBER `` /locations/global/workloadIdentityPools/ `` POOL_ID `` /subject/system:serviceaccount: `` GATEWAY_NAMESPACE `` : `` GATEWAY_NAME` , where `GATEWAY_NAME` is the name that you plan to give the gateway when you [create the gateway](https://docs.cloud.google.com/gemini-enterprise-agent-platform/agents/governance/agent-gateway-cross-cloud/setup#create-gateway) .

### Create an agent connectivity template

Each gateway references an agent connectivity template, which is a Google Cloud resource that references your [registered cluster](https://docs.cloud.google.com/gemini-enterprise-agent-platform/agents/governance/agent-gateway-cross-cloud/setup#register-cluster) . You don't need to create a separate template for each gateway: you can map multiple gateways to a single template. You can also create multiple templates for the same cluster.

If you already have an agent connectivity template for your cluster that you want to use, skip to [Create the gateway](https://docs.cloud.google.com/gemini-enterprise-agent-platform/agents/governance/agent-gateway-cross-cloud/setup#create-gateway) .

To create an agent connectivity template, do the following:

1.  Save the following template definition as `act.yaml` :

    ```
    description: "Agent connectivity template for CLUSTER_NAME"
    agentCompute: K8S
    registeredCluster: "projects/PROJECT_ID/locations/LOCATION/registeredClusters/CLUSTER_NAME"
    ```

2.  Import the template:

    ```
    gcloud alpha network-services agent-connectivity-templates import ACT_NAME \
        --project=PROJECT_ID \
        --location=LOCATION \
        --source=act.yaml
    ```

Replace the following:

- `CLUSTER_NAME` : the name of the [registered cluster](https://docs.cloud.google.com/gemini-enterprise-agent-platform/agents/governance/agent-gateway-cross-cloud/setup#register-cluster) .
- `PROJECT_ID` : your Google Cloud project ID.
- `LOCATION` : the region where you [registered the cluster](https://docs.cloud.google.com/gemini-enterprise-agent-platform/agents/governance/agent-gateway-cross-cloud/setup#register-cluster) .
- `ACT_NAME` : a name for the agent connectivity template.

### Create the gateway

To create the gateway, do the following:

1.  If the gateway namespace doesn't already exist, create it:

    ```
    kubectl create namespace GATEWAY_NAMESPACE
    ```

    Replace `GATEWAY_NAMESPACE` with the dedicated namespace for the gateway that you used when you [granted roles to the gateway](https://docs.cloud.google.com/gemini-enterprise-agent-platform/agents/governance/agent-gateway-cross-cloud/setup#grant-gateway-roles) .

2.  Save the following manifest as `agent-gateway.yaml` :

    ```
    apiVersion: networkservices.googleapis.com/v1alpha1
    kind: GCPAgentGateway
    metadata:
      name: GATEWAY_NAME
      namespace: GATEWAY_NAMESPACE
    spec:
      agentConnectivityTemplateUri: "projects/PROJECT_ID/locations/LOCATION/agentConnectivityTemplates/ACT_NAME"
    ```

    Replace the following:

    - `GATEWAY_NAME` : a name for the gateway.
    - `GATEWAY_NAMESPACE` : the dedicated namespace for the gateway that you used when you [granted roles to the gateway](https://docs.cloud.google.com/gemini-enterprise-agent-platform/agents/governance/agent-gateway-cross-cloud/setup#grant-gateway-roles) .
    - `PROJECT_ID` : your Google Cloud project ID.
    - `LOCATION` : the region of the agent connectivity template. This region must match the region where you [registered the cluster](https://docs.cloud.google.com/gemini-enterprise-agent-platform/agents/governance/agent-gateway-cross-cloud/setup#register-cluster) .
    - `ACT_NAME` : the name of the [agent connectivity template](https://docs.cloud.google.com/gemini-enterprise-agent-platform/agents/governance/agent-gateway-cross-cloud/setup#create-act) .

3.  Apply the manifest:

    ```
    kubectl apply -f agent-gateway.yaml
    ```

4.  Wait for the gateway to be deployed and ready:

    ```
    kubectl wait --for=condition=Reconciled=True \
        gcpagentgateway/GATEWAY_NAME \
        -n GATEWAY_NAMESPACE \
        --timeout=300s
    ```

    When the gateway is ready, the command returns `gcpagentgateway.networkservices.googleapis.com/ `` GATEWAY_NAME `` condition met` .

    > **Note:** The `Reconciled` condition can become `True` up to two minutes before the gateway starts accepting connections on port `8443` . During this time, requests to the gateway fail with a connection error. Wait before you send traffic, or retry failed requests.

5.  Configure your service mesh to forward outbound agent traffic, such as large language model (LLM), Model Context Protocol (MCP), and Agent-to-Agent (A2A) requests, through the gateway.

### Add tolerations to existing gateways

If you add the `k8s.tolerations` Helm value after you create a `GCPAgentGateway` resource, do the following so that the controller re-creates the gateway deployment with the new tolerations:

1.  Run the `helm upgrade --install` command from [Install the control plane Helm chart](https://docs.cloud.google.com/gemini-enterprise-agent-platform/agents/governance/agent-gateway-cross-cloud/setup#install-control-plane) with `--values tolerations-values.yaml` .

2.  Delete the existing gateway deployment:

    ```
    kubectl delete deployment GATEWAY_NAME \
        --namespace GATEWAY_NAMESPACE
    ```

    Repeat this step for each gateway in your cluster.

3.  Restart the controller so that it re-creates the gateway deployment:

    ```
    kubectl rollout restart deployment/agent-governance-cross-cloud-controller \
        --namespace geap-system
    ```

This procedure doesn't affect the Google Cloud `AgentGateway` resource or any attached `GCPExtensionBinding` resources. Outbound traffic through the gateway is interrupted until the controller re-creates the gateway deployment.

### Allow outbound connectivity to Google APIs

Ensure that the Agent Gateway for cross-cloud proxy pods have outbound HTTPS and gRPC connectivity to `*.googleapis.com` on TCP port `443` .

## Configure TLS inspection

Configure Transport Layer Security (TLS) inspection to ensure that Agent Gateway for cross-cloud can inspect and govern outbound traffic.

### Secure the TLS inspection CA secret

Agent Gateway for cross-cloud uses a root certificate authority (CA) to issue the certificates that it presents when it inspects outbound TLS traffic. The controller creates this CA when it starts. The CA, including its private key, is stored in Kubernetes `Secret` resources in two namespaces: the controller namespace ( `geap-system` ) and the gateway namespace, where the Agent Gateway for cross-cloud proxy and AIR sidecar are deployed. Anyone who can read these `Secret` resources can impersonate external endpoints to your agent workloads. To protect the CA, apply the following safeguards:

- **Restrict RBAC access to the `Secret`** : Limit the `get` , `list` , and `watch` permissions on `Secret` resources in the `geap-system` and gateway namespaces to the Agent Gateway for cross-cloud service accounts and dedicated platform administrators. The `list` and `watch` permissions also expose `Secret` contents.
- **Isolate the controller and gateway namespaces** : Users who can create pods in a namespace can mount any `Secret` in that namespace. Run only Agent Gateway for cross-cloud components in the `geap-system` namespace and the gateway namespace. Don't deploy agent workloads or other pods in these namespaces. Limit permissions to create or modify pods, deployments, and other workload resources in these namespaces to trusted administrators.
- **Encrypt `Secret` data at rest** : Enable [encryption at rest](https://kubernetes.io/docs/tasks/administer-cluster/encrypt-data/) for `Secret` resources in your cluster's etcd datastore. Where possible, use a [KMS provider](https://kubernetes.io/docs/tasks/administer-cluster/kms-provider/) to manage the encryption keys.
- **Audit access to the `Secret`** : Enable [Kubernetes audit logging](https://kubernetes.io/docs/tasks/debug/debug-cluster/audit/) and monitor read access to the CA `Secret` .

## What's next

- [Deploy and register cross-cloud agents](https://docs.cloud.google.com/gemini-enterprise-agent-platform/agents/governance/agent-gateway-cross-cloud/deploy-agents)
- [Enforce cross-cloud governance policies](https://docs.cloud.google.com/gemini-enterprise-agent-platform/agents/governance/agent-gateway-cross-cloud/enforce-policies)
- [Configure cross-cloud agent observability](https://docs.cloud.google.com/gemini-enterprise-agent-platform/agents/governance/agent-gateway-cross-cloud/observability)
