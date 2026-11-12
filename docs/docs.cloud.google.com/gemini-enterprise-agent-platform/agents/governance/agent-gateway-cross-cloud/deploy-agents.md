---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/agents/governance/agent-gateway-cross-cloud/deploy-agents
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/agents/governance/agent-gateway-cross-cloud/deploy-agents
title: Deploy and register cross-cloud agents
description: Deploy agent workloads and Model Context Protocol (MCP) tools into a governed namespace and register them with Agent Registry.
data_source: docs.cloud.google.com
---

> **Preview**
>
> This feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](https://docs.cloud.google.com/terms/service-terms#1) . Pre-GA features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

> **Request access:** Agent Gateway for cross-cloud is available in Limited Preview. To use this feature, complete the [access request form](https://docs.google.com/forms/d/e/1FAIpQLSeUpnNRtYQjLRblii-KoUbJJ7DjEV6fvQAfO21IAXgVSqFjpw/viewform) .

This guide explains how to deploy your agent workloads and Model Context Protocol (MCP) tools into a governed namespace and register them with [Agent Registry](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/agent-registry) in Gemini Enterprise Agent Platform. Before deploying agents, make sure that you [set up Agent Gateway for cross-cloud](https://docs.cloud.google.com/gemini-enterprise-agent-platform/agents/governance/agent-gateway-cross-cloud/setup) on your cluster.

## Label workloads for auto-registration

The `agent-governance-cross-cloud-controller` controller automatically registers agents and MCP servers in Agent Registry. To register a workload, add the `apphub.cloud.google.com/functional-type` label to the `metadata.labels` field of its `Deployment` manifest:

- For agents, set the label to `AGENT` .
- For MCP servers, set the label to `MCP_SERVER` .

For example:

```
metadata:
  labels:
    apphub.cloud.google.com/functional-type: "AGENT"
```

> **Caution:** Agent Registry requires each agent and MCP server URL—such as the URL in an Agent Card—to be unique across all clusters that are registered to the same Google Cloud project. In-cluster URLs such as `SERVICE `` . `` NAMESPACE `` .svc.cluster.local` aren't unique across clusters, so if two clusters in the same project run a service with the same name and namespace, registration of the second service fails with an `Interface URL ... is already in use by another service` error. The same error occurs if registry entries from a deleted cluster weren't removed. Use unique service names or namespaces across clusters, and delete a cluster's Agent Registry entries when you decommission it.

### Specify the Agent Card location

When the controller registers an agent, it fetches the agent's Agent Card to populate the agent's registry entry. To specify where the controller fetches the Agent Card, add the `a2a-protocol.org/agent-card` annotation to the deployment. If the annotation is missing, the controller uses the following defaults:

- Protocol: `HTTP`
- Port: `8080`
- Endpoint: `/.well-known/agent-card.json`

For example:

```
metadata:
  labels:
    apphub.cloud.google.com/functional-type: "AGENT"
  annotations:
    a2a-protocol.org/agent-card: |
      card:
        endpoint: /.well-known/agent-card.json
        protocol: HTTP
        port: 8080
```

> **Note:** If your agent workload requires authentication for requests to its Agent Card, Agent Card retrieval fails. The agent is still registered in Agent Registry, but its registry entry doesn't include the details from the Agent Card.

### Describe MCP server capabilities

For MCP servers, the controller extracts the server's capabilities from the `modelcontextprotocol.info/urls` and `modelcontextprotocol.info/capabilities` annotations on the deployment.

For example:

```
metadata:
  labels:
    apphub.cloud.google.com/functional-type: "MCP_SERVER"
  annotations:
    modelcontextprotocol.info/urls: |
      - http://my-mcp-server.default.svc.cluster.local:8080/mcp
    modelcontextprotocol.info/capabilities: |
      card:
        endpoint: "/mcp"
        protocol: "HTTP"
        port: 8080
```

In the `modelcontextprotocol.info/urls` annotation, list the endpoint URLs where the controller can reach your MCP server.

If you specify only the `modelcontextprotocol.info/urls` annotation, the controller uses the following default values for the MCP server capabilities:

- Protocol: `HTTP`
- Port: `8080`
- Endpoint: `/mcp`

> **Note:** If the `modelcontextprotocol.info/urls` annotation is missing, or if your MCP server requires authentication for requests, MCP server capabilities retrieval fails. The MCP server is still registered in Agent Registry, but its registry entry doesn't include the details from the MCP server capabilities.

### Find the registered service resource

When the controller registers a workload, it adds the `agentregistry.cloud.google.com/service-uri` annotation to the workload's deployment. This annotation contains the URI of the service resource that's registered in Agent Registry. To get the URI, run the following commands:

```
SERVICE_URI=$(kubectl get deployment DEPLOYMENT_NAME \
    --namespace=NAMESPACE \
    -o jsonpath='{.metadata.annotations.agentregistry\.cloud\.google\.com/service-uri}')
echo $SERVICE_URI
```

Replace the following:

- `DEPLOYMENT_NAME` : the name of your agent or MCP server deployment.
- `NAMESPACE` : the namespace of the deployment.

If the command returns no output, the controller hasn't registered the workload yet.

## Attach projected KSA OIDC tokens

Your agent workloads must authenticate with Agent Gateway for cross-cloud by using a projected Kubernetes service account (KSA) OpenID Connect (OIDC) token, which is exchanged using Workload Identity Federation. The token's audience must be your workload identity pool provider.

To attach the token, do the following:

1.  Mount a projected KSA token in your agent containers:

    ```
    spec:
      template:
        spec:
          containers:
          - name: AGENT_CONTAINER_NAME
            volumeMounts:
            - name: ksa-token-vol
              mountPath: /var/run/secrets/tokens
              readOnly: true
          volumes:
          - name: ksa-token-vol
            projected:
              sources:
              - serviceAccountToken:
                  path: ksa-token
                  expirationSeconds: 3600
                  audience: "//iam.googleapis.com/projects/PROJECT_NUMBER/locations/global/workloadIdentityPools/POOL_ID/providers/PROVIDER_ID"
    ```

    Replace the following:

    - `AGENT_CONTAINER_NAME` : the name of your agent container.
    - `PROJECT_NUMBER` : your Google Cloud project number.
    - `POOL_ID` : the ID of the workload identity pool that you [created during setup](https://docs.cloud.google.com/gemini-enterprise-agent-platform/agents/governance/agent-gateway-cross-cloud/setup#create-pool-provider) .
    - `PROVIDER_ID` : the ID of the workload identity pool provider that you [created during setup](https://docs.cloud.google.com/gemini-enterprise-agent-platform/agents/governance/agent-gateway-cross-cloud/setup#create-pool-provider) .

2.  Include the token in every request that your workload sends to the Agent Gateway for cross-cloud proxy, for both HTTP and HTTPS traffic on ports `80` , `443` , and `8443` . Read the token from `/var/run/secrets/tokens/ksa-token` and pass it in the `Proxy-Authorization` header as a bearer token:

    ```
    Proxy-Authorization: Bearer KSA_TOKEN
    ```

    Replace `KSA_TOKEN` with the contents of `/var/run/secrets/tokens/ksa-token` . The kubelet refreshes the token before it expires, so read the token from the file for each request instead of caching it.

## Route agent traffic through Agent Gateway for cross-cloud

The Agent Gateway for cross-cloud proxy governs outbound agent traffic, such as large language model (LLM), Model Context Protocol (MCP), and Agent-to-Agent (A2A) requests. The gateway supports the following modes:

- **Forward proxy** : You configure your agent workload to send traffic to the gateway over HTTP or HTTPS `CONNECT` , and the gateway forwards the traffic to the destination. For HTTPS requests, the gateway performs [TLS inspection](https://docs.cloud.google.com/gemini-enterprise-agent-platform/agents/governance/agent-gateway-cross-cloud/setup#configure-tls-inspection) so that it can inspect and govern the request.
- **Transparent proxy** : Outbound traffic is redirected to the gateway without an HTTP `CONNECT` tunnel—for example, by using `iptables` redirect rules or the `curl --connect-to` option.

The gateway accepts forward proxy (HTTP `CONNECT` ) traffic only on port `8443` , and transparent proxy traffic only on port `443` for HTTPS and port `80` for HTTP. Other ports don't work, even if you change the spec of the gateway's Kubernetes resources, such as its `Service` or `Deployment` .

This section describes how to configure forward proxy mode.

> **Note:** Traffic interception isn't part of Agent Gateway for cross-cloud. To use transparent proxy mode, configure your existing service mesh or network stack to redirect outbound agent traffic to the gateway.

To route traffic through the gateway, configure the HTTP client in your agent workload to use the Agent Gateway for cross-cloud Kubernetes service as its forward proxy. Many HTTP client libraries read the standard proxy environment variables. For example, you can set these variables in your deployment manifest:

```
spec:
  template:
    spec:
      containers:
      - name: AGENT_CONTAINER_NAME
        env:
        - name: HTTPS_PROXY
          value: "https://GATEWAY_NAME.GATEWAY_NAMESPACE.svc:8443"
        - name: HTTP_PROXY
          value: "http://GATEWAY_NAME.GATEWAY_NAMESPACE.svc:8443"
        - name: NO_PROXY
          value: "NO_PROXY_HOSTS"
```

Replace the following:

- `AGENT_CONTAINER_NAME` : the name of your agent container.
- `GATEWAY_NAME` : the name of the `GCPAgentGateway` resource that you [created during setup](https://docs.cloud.google.com/gemini-enterprise-agent-platform/agents/governance/agent-gateway-cross-cloud/setup#create-gateway) . The Kubernetes Service for the gateway has the same name as the `GCPAgentGateway` resource.
- `GATEWAY_NAMESPACE` : the namespace of the `GCPAgentGateway` resource.
- `NO_PROXY_HOSTS` : a comma-separated list of hosts that should bypass the gateway, such as the Kubernetes API server and in-cluster services—for example, `.cluster.local,.svc,10.0.0.0/8` .

The Agent Gateway for cross-cloud service accepts proxy traffic on port `8443` . Use the `http://` scheme for `HTTP_PROXY` and the `https://` scheme for `HTTPS_PROXY` . If your HTTP client library doesn't read these environment variables, configure the proxy address directly in the client.

In forward proxy mode, the `Proxy-Authorization` header authenticates your workload to the gateway. The gateway removes the `Proxy-Authorization` header before it forwards the request, so the destination never receives your KSA token. To authenticate to the destination, pass the destination's credentials in the standard `Authorization` header, which the gateway forwards unchanged:

```
Authorization: Bearer DESTINATION_TOKEN
```

Replace `DESTINATION_TOKEN` with a token that the destination accepts.

### Trust the TLS inspection root CA

Because the gateway inspects TLS traffic, your agent workloads must trust the root CA certificate that Agent Gateway for cross-cloud uses to issue certificates. When the `agent-governance-cross-cloud-controller` controller starts, it creates this CA and publishes the public root CA certificate in a `ConfigMap` named `air-root-ca` in the `geap-system` namespace.

To configure your agent workloads to trust the root CA, do the following:

1.  Copy the public root CA certificate into a `ConfigMap` in each namespace where your agents run:

    ```
    CA_DATA="$(kubectl get configmap air-root-ca --namespace=geap-system \
        -o jsonpath='{.data.ca\.crt}')"
    kubectl create configmap air-root-ca \
        --namespace=AGENT_NAMESPACE \
        --from-literal=ca.crt="${CA_DATA}" \
        --dry-run=client -o yaml | kubectl apply -f -
    ```

    Replace `AGENT_NAMESPACE` with the namespace of your agent workload.

    > **Caution:** Only copy the public certificate. Never copy the CA `Secret` , which contains the private key, into agent namespaces.

2.  Mount the `ConfigMap` in your agent containers:

    ```
    spec:
      template:
        spec:
          containers:
          - name: AGENT_CONTAINER_NAME
            volumeMounts:
            - name: agent-gateway-ca
              mountPath: /etc/agent-gateway-ca
              readOnly: true
          volumes:
          - name: agent-gateway-ca
            configMap:
              name: air-root-ca
    ```

3.  Configure your workload to trust `/etc/agent-gateway-ca/ca.crt` . How you do this depends on your language runtime and HTTP client library. Many runtimes and libraries read the following environment variables:

    ```
    spec:
      template:
        spec:
          containers:
          - name: AGENT_CONTAINER_NAME
            env:
            - name: SSL_CERT_FILE
              value: "/etc/agent-gateway-ca/ca.crt"
            - name: REQUESTS_CA_BUNDLE
              value: "/etc/agent-gateway-ca/ca.crt"
            - name: CURL_CA_BUNDLE
              value: "/etc/agent-gateway-ca/ca.crt"
            - name: NODE_EXTRA_CA_CERTS
              value: "/etc/agent-gateway-ca/ca.crt"
    ```

    > **Warning:** The `SSL_CERT_FILE` , `REQUESTS_CA_BUNDLE` , and `CURL_CA_BUNDLE` variables replace the default trust store instead of adding to it. Only `NODE_EXTRA_CA_CERTS` adds the certificate to the default trust store. Hosts in `NO_PROXY_HOSTS` bypass the gateway and present their own certificates, so if your workload connects to these hosts, point these variables to a bundle that contains both the root CA and your default CA certificates.

### Trust private CAs for destinations

When the gateway forwards a request to a destination over TLS, it verifies the destination's certificate. By default, the gateway trusts only public CAs. If a destination uses a certificate that's issued by a private or self-signed CA, add that CA to the gateway's trust bundle by modifying the gateway's `Deployment` . The `Deployment` has the same name as the `GCPAgentGateway` resource.

> **Note:** The `agent-governance-cross-cloud-controller` controller doesn't revert changes that you make to the gateway's `Deployment` . Applying the change restarts the gateway.

To add a private CA to the gateway's trust bundle, do the following:

1.  Create a `ConfigMap` that contains the CA certificate in the gateway's namespace:

    ```
    kubectl create configmap DESTINATION_CA_CONFIGMAP \
        --namespace=GATEWAY_NAMESPACE \
        --from-file=ca.crt=CA_CERT_FILE
    ```

    Replace the following:

    - `DESTINATION_CA_CONFIGMAP` : a name for the `ConfigMap` .
    - `GATEWAY_NAMESPACE` : the namespace of the `GCPAgentGateway` resource.
    - `CA_CERT_FILE` : the path to the PEM-encoded CA certificate.

    If the destination uses a certificate that's issued by your Kubernetes cluster's CA, skip this step and use the `kube-root-ca.crt` `ConfigMap` that Kubernetes creates in each namespace.

2.  Get the image of the gateway container:

    ```
    kubectl get deployment GATEWAY_NAME \
        --namespace=GATEWAY_NAMESPACE \
        -o jsonpath='{.spec.template.spec.containers[?(@.name=="agent-gateway")].image}'
    ```

    Replace `GATEWAY_NAME` with the name of the `GCPAgentGateway` resource.

3.  Edit the gateway's `Deployment` to add an init container that combines the default CA bundle with your CA, and mount the combined bundle in the gateway container. The init container uses the gateway image so that the combined bundle contains only the gateway's default CAs and your CA:

    ```
    spec:
      template:
        spec:
          initContainers:
          - name: init-ca-bundle
            image: GATEWAY_IMAGE
            command: ["/bin/sh", "-c"]
            args:
            - cat /etc/ssl/certs/ca-certificates.crt /etc/custom-ca/ca.crt > /var/run/envoy-certs/ca-certificates.crt
            volumeMounts:
            - name: custom-private-ca-vol
              mountPath: /etc/custom-ca
              readOnly: true
            - name: envoy-ca-bundle-vol
              mountPath: /var/run/envoy-certs
          containers:
          - name: agent-gateway
            volumeMounts:
            - name: envoy-ca-bundle-vol
              mountPath: /etc/ssl/certs/ca-certificates.crt
              subPath: ca-certificates.crt
              readOnly: true
          volumes:
          - name: custom-private-ca-vol
            configMap:
              name: DESTINATION_CA_CONFIGMAP
          - name: envoy-ca-bundle-vol
            emptyDir: {}
    ```

    Replace the following:

    - `GATEWAY_IMAGE` : the image from the previous step.
    - `DESTINATION_CA_CONFIGMAP` : the `ConfigMap` from the first step, or `kube-root-ca.crt` .

## What's next

- [Enforce cross-cloud governance policies](https://docs.cloud.google.com/gemini-enterprise-agent-platform/agents/governance/agent-gateway-cross-cloud/enforce-policies)
- [Configure cross-cloud agent observability](https://docs.cloud.google.com/gemini-enterprise-agent-platform/agents/governance/agent-gateway-cross-cloud/observability)
- [Learn more about Agent Registry](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/agent-registry)
