---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/govern/gateways/set-up-gke-ingress
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/gateways/set-up-gke-ingress
title: Set up agent ingress governance on GKE
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

> **Preview**
>
> This product or feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](https://docs.cloud.google.com/terms/service-terms#1) . Pre-GA products and features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

This document shows you how to configure Agent Gateway for Google Kubernetes Engine (GKE) to govern and secure inbound (ingress) traffic to the self-managed AI agents and Model Context Protocol (MCP) servers running on your GKE cluster.

To secure your incoming connections, you provision a regional Application Load Balancer by using the GKE Gateway API. After you configure a standard Gateway and convert it into an Agent Gateway, you can enforce identity-based access controls, restrict specific MCP tool calls, and sanitize incoming prompts by using Google Cloud Model Armor.

To secure your inbound connections, complete the following steps:

1.  [Create a GKE Gateway](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/gateways/set-up-gke-ingress#create-gke-gateway) .
2.  [Turn the Gateway into an Agent Gateway](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/gateways/set-up-gke-ingress#turn-gateway-agent) .
3.  [Configure content security with Model Armor](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/gateways/set-up-gke-ingress#configure-content-security) .
4.  [Delegate authorization to a custom IDP](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/gateways/set-up-gke-ingress#delegate-auth-idp) .
5.  [Verify ingress governance](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/gateways/set-up-gke-ingress#verify-ingress) .
6.  [Verify resource status](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/gateways/set-up-gke-ingress#verify-status) .

To learn more about this architecture, see [Agent Gateway on GKE overview](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/gateways/gke-overview) .

## Before you begin

Before you configure ingress governance, complete the following prerequisites:

1.  Complete the common prerequisites in [Agent Gateway on GKE overview](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/gateways/gke-overview#prereqs) .

2.  Create a proxy-only subnet. Regional load balancers require one active proxy-only subnet per region and VPC network. If your network already has an active proxy-only subnet in your region, you can skip this step.

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

3.  Create the certificates for your Gateway by using Kubernetes Secrets, Compute SSL Certificates, or Certificate Manager.

4.  Create a namespace for your agent workloads:

    ```
    kubectl create namespace NAMESPACE
    ```

    Replace `NAMESPACE` with a name for your namespace—for example, `agent-ns` .

5.  Workload configuration: Register your workloads with Agent Registry and deploy them with a SPIFFE identity.

    1.  Save the following as `agent.yaml` and apply it to your cluster:

        ```
        apiVersion: v1
        kind: ServiceAccount
        metadata:
          name: KSA_NAME
          namespace: NAMESPACE
        ---
        # nginx config: listen on 8080, answer every method with 200 JSON
        apiVersion: v1
        kind: ConfigMap
        metadata:
          name: nginx-conf
          namespace: NAMESPACE
        data:
          default.conf: |
            server {
              listen 8080;
              location / {
                default_type application/json;
                return 200 '{"backend":"nginx","method":"$request_method","uri":"$request_uri"}\n';
              }
            }
        ---
        # The agent: curl for egress tests + nginx for ingress tests
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
              - name: curl                      # egress: kubectl exec -c curl
                image: curlimages/curl:8.10.1
                command: ["sleep", "infinity"]
              - name: nginx                     # ingress backend on :8080
                image: nginx:1.27
                ports:
                - containerPort: 8080
                volumeMounts:
                - name: conf
                  mountPath: /etc/nginx/conf.d
              volumes:
              - name: conf
                configMap:
                  name: nginx-conf
        ```

        Replace the following:

        - `KSA_NAME` : the name of the Kubernetes service account.
        - `NAMESPACE` : the namespace for the service account.
        - `AGENT_NAME` : the name of the agent deployment.
        - `TRUST_DOMAIN` : the trust domain for your resource hierarchy. For projects in an organization, use `agents.global.org- `` ORGANIZATION_ID `` .system.id.goog` . For projects without an organization, use `agents.global.proj- `` PROJECT_NUMBER `` .system.id.goog` .

        **Notes:**

        - This manifest deploys `curl` and `nginx` containers for testing. For production deployments, replace this deployment with your actual AI agent.
        - If you are deploying an Agent-to-Agent (A2A) workload, you must set the URL of your Agent Gateway (the GKE Gateway) in the `supportedInterfaces` section of your Agent Card. This ensures that clients discovering your agents by using Agent Registry connect through the governed ingress path.
        - If your agent application code needs to call Google Cloud APIs directly by using bound tokens from the metadata server, or perform direct Agent-to-Agent (A2A) mTLS authentication, you must also add the `iam.gke.io/inject-podcertificates: "true"` annotation to your Pod template.

    2.  Apply the manifest to your cluster:

        ```
        kubectl apply -f agent.yaml
        ```

## Create a GKE Gateway

To establish a network entry point for your inbound traffic, deploy a `Gateway` resource. During this preview, you can use only regional load balancers. You also need a `Service` and an `HTTPRoute` to direct incoming traffic from the Gateway to your agent workloads.

1.  Save the following manifest as `gke-gw-https.yaml` :

    ```
    apiVersion: gateway.networking.k8s.io/v1
    kind: Gateway
    metadata:
      name: my-agent-ingress-gateway
      namespace: NAMESPACE
    spec:
      # gke-l7-regional-external-managed (for regional external HTTP(S) LB)
      # gke-l7-rilb (for regional internal HTTP(S) LB)
      gatewayClassName: gke-l7-regional-external-managed
      listeners:
      - name: https
        protocol: HTTPS
        port: 443
        tls:
          mode: Terminate
          options:
            networking.gke.io/cert-manager-certs: CERTIFICATE_NAME
    ---
    apiVersion: v1
    kind: Service
    metadata:
      name: AGENT_NAME
      namespace: NAMESPACE
    spec:
      selector:
        app: AGENT_NAME
      ports:
      - name: http
        port: 8080
        targetPort: 8080
    ---
    apiVersion: gateway.networking.k8s.io/v1
    kind: HTTPRoute
    metadata:
      name: my-agent-route
      namespace: NAMESPACE
    spec:
      parentRefs:
      - name: my-agent-ingress-gateway
      hostnames:
      - HOSTNAME
      rules:
      - backendRefs:
        - name: AGENT_NAME
          port: 8080
    ```

    Replace the following:

    - `NAMESPACE` : your agent namespace.
    - `CERTIFICATE_NAME` : the name of the Certificate Manager certificate you created.
    - `AGENT_NAME` : the name of your agent deployment.
    - `HOSTNAME` : the external hostname for your Gateway.

2.  Apply the manifest to your cluster:

    ```
    kubectl apply -f gke-gw-https.yaml
    ```

## Turn the Gateway into an Agent Gateway

To apply agent governance policies to your incoming traffic, create a `GCPAgentGateway` custom resource that targets your standard Gateway.

1.  Save the following manifest as `agent-gateway.yaml` :

    ```
    apiVersion: networking.gke.io/v1
    kind: GCPAgentGateway
    metadata:
      name: my-ingress-agentgateway
      namespace: NAMESPACE
    spec:
      targetRefs:
      - group: gateway.networking.k8s.io
        kind: Gateway
        name: my-agent-ingress-gateway
    ```

2.  Apply the manifest to your cluster:

    ```
    kubectl apply -f agent-gateway.yaml
    ```

To enforce identity-based access controls for your incoming traffic, define a GCPAuthzPolicy custom resource. By using this resource, you can allow or deny traffic based on exact conditions, such as the identity of the calling client or the specific MCP operations being requested. For more examples and configuration details, see [Secure your Gateway](https://docs.cloud.google.com/kubernetes-engine/docs/how-to/secure-gateway#auth-policy) .

### Authorize specific MCP tool calls

To restrict inbound access to your MCP servers running on GKE, apply authorization rules based on MCP-specific conditions. For example, you can allow clients to use only the `tools/list` method and specific read-only `tools/call` parameters. To enforce this and block requests for all other MCP tools by default, apply a policy similar to the following:

1.  Save the following manifest as `authz-policy-mcp.yaml` :

    ```
    apiVersion: networking.gke.io/v1
    kind: GCPAuthzPolicy
    metadata:
      name: my-mcp-authz
      namespace: NAMESPACE
    spec:
      enforcementLevel: L7
      targetRefs:
      - group: gateway.networking.k8s.io
        kind: Gateway
        name: my-agent-ingress-gateway
      rules:
      - to:
          operations:
          - mcp:
              methods:
              - name: "tools/list"
              - name: "tools/call"
                params:
                - type: Exact
                  value: "get_weather"
                - type: Exact
                  value: "get_location"
      action: ALLOW
    ```

    Replace `NAMESPACE` with your agent namespace.

2.  Apply the manifest to your cluster:

    ```
    kubectl apply -f authz-policy-mcp.yaml
    ```

## Configure content security with Model Armor

To protect against prompt injection and sensitive data leakage on inbound traffic, you can bind Google Cloud Model Armor to your ingress Gateway using a GCPExtensionBinding custom resource.

1.  Create your request and response sanitization templates. You can reuse the template you created during the [egress setup](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/gateways/set-up-gke-egress#delegate-content-security-model-armor) , or create a new one by following the instructions in [Configure Model Armor](https://docs.cloud.google.com/security-command-center/docs/model-armor-overview) .

2.  Save the following manifest as `bind-agent-gateway-to-model-armor.yaml` :

    ```
    apiVersion: networking.gke.io/v1
    kind: GCPExtensionBinding
    metadata:
      name: bind-agent-gateway-to-model-armor
      namespace: NAMESPACE
    spec:
      targetRefs:
        - group: networking.gke.io
          kind: GCPAgentGateway
          name: my-ingress-agentgateway
      producerExtension: "modelarmor.REGION.rep.googleapis.com"
      failOpen: true
      producerMetadata:
        model_armor_settings: '[{"request_template_id":"projects/PROJECT_ID/locations/REGION/templates/REQUEST_TEMPLATE","response_template_id":"projects/PROJECT_ID/locations/REGION/templates/RESPONSE_TEMPLATE"}]'
    ```

    Replace the following:

    - `NAMESPACE` : your agent namespace.
    - `REGION` : the region for your Model Armor templates.
    - `PROJECT_ID` : your Google Cloud project ID.
    - `REQUEST_TEMPLATE` : the name of your request sanitization template.
    - `RESPONSE_TEMPLATE` : the name of your response sanitization template.

3.  Apply the manifest to your cluster:

    ```
    kubectl apply -f bind-agent-gateway-to-model-armor.yaml
    ```

> **Note:** Ensure you have granted the necessary IAM roles, such as `roles/modelarmor.calloutUser` , to your Gateway's service account. For instructions, see [Delegate content security to Model Armor](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/gateways/set-up-gke-egress#delegate-content-security-model-armor) .

## Delegate authorization to a custom IDP

To enforce centralized Identity and Access Management (IAM) controls through a Custom Identity Provider (IDP), bind your IDP to the Agent Gateway by using a GCPExtensionBinding custom resource.

1.  Save the following manifest as `bind-agent-gateway-to-custom-idp.yaml` :

    ```
    apiVersion: networking.gke.io/v1
    kind: GCPExtensionBinding
    metadata:
      name: custom-idp-extension
      namespace: NAMESPACE
    spec:
      targetRefs:
        - group: networking.gke.io
          kind: GCPAgentGateway
          name: my-ingress-agentgateway
      producerExtension: "example.provider.net"
    ```

2.  Apply the manifest to your cluster:

    ```
    kubectl apply -f bind-agent-gateway-to-custom-idp.yaml
    ```

## Verify ingress governance

To verify that your ingress Gateway is correctly routing traffic and enforcing both your authorization and Model Armor policies, run the following test commands from your local machine.

These commands test the Nginx backend deployed earlier, using specific Model Context Protocol (MCP) payloads:

1.  Run the test script:

    ```
    GW_IP=$(kubectl -n NAMESPACE get gateway my-agent-ingress-gateway -o jsonpath='{.status.addresses[0].value}')
    URL="https://HOSTNAME/"
    echo "Gateway IP: $GW_IP"

    PAYLOAD_A='{"jsonrpc":"2.0","id":1,"method":"tools/call","params":{"name":"get_weather","arguments":{"city":"Paris"}}}'
    PAYLOAD_B='{"jsonrpc":"2.0","id":2,"method":"tools/call","params":{"name":"get_weather","arguments":{"city":"my card is 4111111111111111"}}}'
    PAYLOAD_C='{"jsonrpc":"2.0","id":3,"method":"tools/call","params":{"name":"delete_everything","arguments":{}}}'
    PAYLOAD_D='{"jsonrpc":"2.0","id":4,"method":"tools/list"}'

    # A. allowed tool (get_weather), harmless -> Expect HTTP=200 (from nginx)
    curl -s -w " HTTP=%{http_code}\n" --cacert CA_CERT_FILE --resolve "HOSTNAME:443:$GW_IP" -H "Content-Type: application/json" -d "$PAYLOAD_A" "$URL"

    # B. allowed tool (get_weather), credit card number -> Expect HTTP=403 (blocked by Model Armor)
    curl -s -w " HTTP=%{http_code}\n" --cacert CA_CERT_FILE --resolve "HOSTNAME:443:$GW_IP" -H "Content-Type: application/json" -d "$PAYLOAD_B" "$URL"

    # C. tool not allowed (delete_everything) -> Expect HTTP=403 (blocked by GCPAuthzPolicy)
    curl -s -w " HTTP=%{http_code}\n" --cacert CA_CERT_FILE --resolve "HOSTNAME:443:$GW_IP" -H "Content-Type: application/json" -d "$PAYLOAD_C" "$URL"

    # D. tools/list -> Expect HTTP=200 (allowed by GCPAuthzPolicy)
    curl -s -w " HTTP=%{http_code}\n" --cacert CA_CERT_FILE --resolve "HOSTNAME:443:$GW_IP" -H "Content-Type: application/json" -d "$PAYLOAD_D" "$URL"
    ```

    Replace the following:

    - `NAMESPACE` : your agent namespace.
    - `HOSTNAME` : the external hostname for your Gateway.
    - `CA_CERT_FILE` : the path to the root certificate that signed your Gateway's certificate (if using a private CA or self-signed cert). If using a public CA, you can omit the `--cacert` flag.

## Verify resource status

To verify that your Gateway and its attached governance policies are successfully programmed and ready, check the status of your custom resources:

```
kubectl describe gateway my-agent-ingress-gateway -n NAMESPACE
kubectl describe gcpagentgateway my-ingress-agentgateway -n NAMESPACE
kubectl describe gcpextensionbinding bind-agent-gateway-to-model-armor -n NAMESPACE
```

In the output for each command, review the Status section. Ensure that the conditions indicate the resources are accepted and successfully programmed before you send traffic to the Gateway.

## Troubleshoot

To find methods for diagnosing and resolving Agent Gateway issues, see [Troubleshoot Agent Gateway connectivity](https://docs.cloud.google.com/gemini-enterprise-agent-platform/troubleshooting/troubleshoot-agent-gateway) .

## What's next

- To monitor your agents' traffic and behavior, see [Monitor Agent Gateway traffic](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/gateways/monitor-agent-gateway) .
