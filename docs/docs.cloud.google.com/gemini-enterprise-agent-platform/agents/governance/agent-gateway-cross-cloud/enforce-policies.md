---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/agents/governance/agent-gateway-cross-cloud/enforce-policies
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/agents/governance/agent-gateway-cross-cloud/enforce-policies
title: Enforce cross-cloud governance policies
description: Enforce safety and access governance policies for cross-cloud agents using Gemini Enterprise Agent Platform.
data_source: docs.cloud.google.com
---

> **Preview**
>
> This feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](https://docs.cloud.google.com/terms/service-terms#1) . Pre-GA features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

> **Request access:** Agent Gateway for cross-cloud is available in Limited Preview. To use this feature, complete the [access request form](https://docs.google.com/forms/d/e/1FAIpQLSeUpnNRtYQjLRblii-KoUbJJ7DjEV6fvQAfO21IAXgVSqFjpw/viewform) .

This guide explains how to enforce governance policies for cross-cloud agents using Gemini Enterprise Agent Platform after you [deploy and register your cross-cloud agents](https://docs.cloud.google.com/gemini-enterprise-agent-platform/agents/governance/agent-gateway-cross-cloud/deploy-agents) .

## Enforce centralized cloud policies

You can enforce centralized safety and access policies by binding cloud-managed [Model Armor](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/configure-model-armor) templates and Identity-Aware Proxy (IAP) policies to your local [Agent Gateway](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/gateways/agent-gateway-overview) for cross-cloud proxies. You define the policies in Google Cloud, and then create a `GCPExtensionBinding` custom resource in your cluster that tells the proxy which services evaluate its traffic.

You can bind the following services:

- **Model Armor** : Screens prompts and responses for prompt injection, jailbreak attempts, and harmful content. For details, see [Configure Model Armor](https://docs.cloud.google.com/gemini-enterprise-agent-platform/agents/governance/agent-gateway-cross-cloud/enforce-policies#configure-model-armor) .
- **IAP** : Authorizes agent access to tools, such as Model Context Protocol (MCP) servers, by evaluating IAM allow policies. For details, see [Configure IAP](https://docs.cloud.google.com/gemini-enterprise-agent-platform/agents/governance/agent-gateway-cross-cloud/enforce-policies#configure-iap) .

### Identify the agent principal

IAP policies identify agents by their [Agent Identity](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/agent-identity-overview) . The proxy obtains this identity for each request, and IAP evaluates your policies against it. Model Armor bindings don't use the agent principal. The principal identifier for an agent workload has the following format:

```
principal://agents.global.org-ORGANIZATION_ID.system.id.goog/resources/agentplatformhybrid/projects/PROJECT_NUMBER/locations/LOCATION/clusters/CLUSTER_NAME/namespaces/AGENT_NAMESPACE/serviceaccounts/KSA_NAME
```

If your project isn't associated with an organization and you omitted the `gcp.orgId` value when you [installed the control plane Helm chart](https://docs.cloud.google.com/gemini-enterprise-agent-platform/agents/governance/agent-gateway-cross-cloud/setup#install-control-plane) , the principal identifier uses your project number instead of your organization ID:

```
principal://agents.global.proj-PROJECT_NUMBER.system.id.goog/resources/agentplatformhybrid/projects/PROJECT_NUMBER/locations/LOCATION/clusters/CLUSTER_NAME/namespaces/AGENT_NAMESPACE/serviceaccounts/KSA_NAME
```

To apply a policy to multiple agents, use one of the following principal sets:

- All cross-cloud agents in your organization: `principalSet://agents.global.org- `` ORGANIZATION_ID `` .system.id.goog/attribute.platform/agentplatformhybrid`
- All cross-cloud agents in a project: `principalSet://agents.global.org- `` ORGANIZATION_ID `` .system.id.goog/attribute.platformContainer/agentplatformhybrid/projects/ `` PROJECT_NUMBER`

If you omitted `gcp.orgId` because your project isn't associated with an organization, the organization-wide principal set does not apply. Instead, use the following principal set to apply a policy to all cross-cloud agents in your project:

- All cross-cloud agents in a project (no organization): `principalSet://agents.global.proj- `` PROJECT_NUMBER `` .system.id.goog/attribute.platformContainer/agentplatformhybrid/projects/ `` PROJECT_NUMBER`

Replace the following:

- `ORGANIZATION_ID` : the ID of your Google Cloud organization. Use this value only if you set `gcp.orgId` when you installed the control plane Helm chart.
- `PROJECT_NUMBER` : your Google Cloud project number.
- `LOCATION` : the region where you [registered the cluster](https://docs.cloud.google.com/gemini-enterprise-agent-platform/agents/governance/agent-gateway-cross-cloud/setup#register-cluster) .
- `CLUSTER_NAME` : the name of the [registered cluster](https://docs.cloud.google.com/gemini-enterprise-agent-platform/agents/governance/agent-gateway-cross-cloud/setup#register-cluster) .
- `AGENT_NAMESPACE` : the namespace of your agent workload.
- `KSA_NAME` : the name of the Kubernetes service account that your agent workload uses.

### Configure Model Armor

To screen agent traffic to large language models (LLMs) with Model Armor, do the following:

1.  Create a Model Armor template that defines your filter settings. For example, the following command creates a template that enables prompt injection and jailbreak detection and basic content filtering:

    ```
    gcloud model-armor templates create TEMPLATE_ID \
        --project=PROJECT_ID \
        --location=LOCATION \
        --pi-and-jailbreak-filter-settings-enforcement=enabled \
        --pi-and-jailbreak-filter-settings-confidence-level=HIGH \
        --basic-config-filter-enforcement=enabled
    ```

    Replace the following:

    - `TEMPLATE_ID` : a name for the template.
    - `PROJECT_ID` : your Google Cloud project ID.
    - `LOCATION` : the region for the template—for example, `us-central1` . The template must be in the same region where you [registered the cluster](https://docs.cloud.google.com/gemini-enterprise-agent-platform/agents/governance/agent-gateway-cross-cloud/setup#register-cluster) . Model Armor templates in other regions aren't supported.

    For all available filter settings, see [Create and manage templates](https://docs.cloud.google.com/model-armor/manage-templates) .

2.  Save the following manifest as `model-armor-binding.yaml` :

    ```
    apiVersion: networkservices.googleapis.com/v1alpha1
    kind: GCPExtensionBinding
    metadata:
      name: BINDING_NAME
      namespace: GATEWAY_NAMESPACE
    spec:
      targetRefs:
      - group: networkservices.googleapis.com
        kind: GCPAgentGateway
        name: GATEWAY_NAME
      producerExtension: "modelarmor.LOCATION.rep.googleapis.com"
      producerMetadata:
        model_armor_settings: '[{"request_template_id":"projects/PROJECT_ID/locations/LOCATION/templates/TEMPLATE_ID","response_template_id":"projects/PROJECT_ID/locations/LOCATION/templates/TEMPLATE_ID"}]'
      failOpen: false
    ```

    Replace the following:

    - `BINDING_NAME` : a name for the binding.
    - `GATEWAY_NAMESPACE` : the namespace of your `GCPAgentGateway` resource.
    - `GATEWAY_NAME` : the name of the `GCPAgentGateway` resource that you [created during setup](https://docs.cloud.google.com/gemini-enterprise-agent-platform/agents/governance/agent-gateway-cross-cloud/setup#create-gateway) .
    - `LOCATION` : the region of your Model Armor template, which is the same region where you [registered the cluster](https://docs.cloud.google.com/gemini-enterprise-agent-platform/agents/governance/agent-gateway-cross-cloud/setup#register-cluster) .
    - `PROJECT_ID` : your Google Cloud project ID.
    - `TEMPLATE_ID` : the ID of your Model Armor template.

    The binding contains the following fields:

    - `targetRefs` : the `GCPAgentGateway` resource that enforces the policy.

    - `producerExtension` : the Google-managed Model Armor service extension.

    - `producerMetadata.model_armor_settings` : a JSON array, passed as a string, of objects that specify the Model Armor templates that the proxy uses to screen requests ( `request_template_id` ) and responses ( `response_template_id` ).

    - `failOpen` : the behavior when Model Armor can't screen the request. If `false` , the request is blocked. If `true` , the request is forwarded without screening. We recommend `false` .

      > **Caution:** During Limited Preview, `failOpen: true` doesn't apply if the proxy can't reach Google Cloud—for example, during a network partition or a regional outage. In that case, the proxy always blocks the request and returns an error, such as HTTP `403` or `500` . Similarly, if the binding references a Model Armor template that doesn't exist, the proxy returns an HTTP `404` error even when `failOpen` is `true` .

    Because the provided sample binding doesn't specify `matchConditions` , Model Armor screens all outbound traffic that passes through the gateway. To scope Model Armor to specific endpoints—for example, when the same gateway also routes MCP or Agent2Agent (A2A) traffic—add `matchConditions` to the binding's `spec` field:

    ```
    spec:
      matchConditions:
      - to:
          destination:
            hosts:
            - exact: "DESTINATION_HOST"
            paths:
            - prefix: "PATH_PREFIX"
    ```

    Replace the following:

    - `DESTINATION_HOST` : the hostname of the LLM endpoint to screen.
    - `PATH_PREFIX` : the request path prefix to screen.

    Model Armor screens a request if it matches at least one condition. Within a `destination` , a request must match an entry in each field that you set. Each host or path entry takes exactly one of `exact` , `prefix` , `suffix` , or `contains` . You can specify up to five conditions.

3.  Apply the manifest:

    ```
    kubectl apply -f model-armor-binding.yaml
    ```

4.  Wait for the binding to be reconciled:

    ```
    kubectl wait --for=condition=Reconciled=True \
        gcpextensionbinding/BINDING_NAME \
        -n GATEWAY_NAMESPACE \
        --timeout=300s
    ```

### Configure IAP

IAP acts as a centralized policy decision point that authorizes agent requests to tools based on IAM access policies. Before you begin, make sure that the destination MCP server is registered in [Agent Registry](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/agent-registry) .

To authorize agent access to an MCP server with IAP, do the following:

1.  Save the following access policy rules as `iap-rules.json` . The rule allows your agent to call specific tools on an MCP server. It uses a Common Expression Language (CEL) condition to restrict which tools the agent can call:

    ```json
    [
      {
        "description": "Allow agent to call specific MCP tools",
        "effect": "ALLOW",
        "principals": [
          "AGENT_PRINCIPAL"
        ],
        "operation": {
          "permissions": [
            "iap.googleapis.com/resources.egressViaIAP"
          ]
        },
        "conditions": {
          "iap.googleapis.com": {
            "title": "Allow only specific MCP tools",
            "expression": "destination.agent_registry.mcp_server.name == 'MCP_SERVER_ID' && destination.agent_registry.mcp_server.tool.name in ['TOOL_NAME_1', 'TOOL_NAME_2']"
          }
        }
      }
    ]
    ```

    Replace the following:

    - `AGENT_PRINCIPAL` : the [principal identifier](https://docs.cloud.google.com/gemini-enterprise-agent-platform/agents/governance/agent-gateway-cross-cloud/enforce-policies#identify-agent-principal) of your agent workload.
    - `MCP_SERVER_ID` : the ID of the MCP server in Agent Registry.
    - `TOOL_NAME_1` , `TOOL_NAME_2` : the names of the MCP tools that the agent can call.

    The condition uses the following attributes:

    - `destination.agent_registry.mcp_server.name` : the ID of the target MCP server in Agent Registry.
    - `destination.agent_registry.mcp_server.tool.name` : the name of the target tool.

    For more information about access policy rules and conditions, see [Create IAM access policies](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/policies/configure-iam-policies-uap) .

2.  Create the access policy and bind it to your project:

    ```
    gcloud beta iam access-policies create POLICY_ID \
        --project=PROJECT_ID \
        --location=global \
        --display-name="POLICY_DISPLAY_NAME" \
        --details-rules=iap-rules.json

    gcloud beta iam policy-bindings create POLICY_BINDING_ID \
        --project=PROJECT_ID \
        --location=global \
        --policy-kind=access \
        --policy=projects/PROJECT_ID/locations/global/accessPolicies/POLICY_ID \
        --target-resource=//cloudresourcemanager.googleapis.com/projects/PROJECT_ID
    ```

    Replace the following:

    - `POLICY_ID` : a name for the access policy.
    - `PROJECT_ID` : your Google Cloud project ID.
    - `POLICY_DISPLAY_NAME` : a display name for the access policy.
    - `POLICY_BINDING_ID` : a name for the policy binding.

3.  Save the following manifest as `iap-binding.yaml` :

    ```
    apiVersion: networkservices.googleapis.com/v1alpha1
    kind: GCPExtensionBinding
    metadata:
      name: BINDING_NAME
      namespace: GATEWAY_NAMESPACE
    spec:
      targetRefs:
      - group: networkservices.googleapis.com
        kind: GCPAgentGateway
        name: GATEWAY_NAME
      producerExtension: "iap.googleapis.com"
      failOpen: false
    ```

    Replace the following:

    - `BINDING_NAME` : a name for the binding.
    - `GATEWAY_NAMESPACE` : the namespace of your `GCPAgentGateway` resource.
    - `GATEWAY_NAME` : the name of your `GCPAgentGateway` resource.

    The `failOpen: false` setting blocks requests when IAP can't evaluate them. The proxy always blocks requests if it can't reach Google Cloud, regardless of the `failOpen` setting. Because the binding doesn't specify `matchConditions` , IAP evaluates all outbound traffic that passes through the gateway. To scope IAP to specific endpoints—for example, when the same gateway also routes LLM or A2A traffic—add `matchConditions` to the binding's `spec` field:

    ```
    spec:
      matchConditions:
      - to:
          destination:
            hosts:
            - exact: "DESTINATION_HOST"
            paths:
            - prefix: "/mcp"
    ```

    Replace `DESTINATION_HOST` with the hostname of the MCP server.

    To test your access policies before you enforce them, set `iamEnforcementMode` to `DRY_RUN` in the binding's `producerMetadata` field. In `DRY_RUN` mode, IAP logs its authorization decisions but doesn't block requests. If you omit `iamEnforcementMode` , the mode defaults to `ENFORCE` , which blocks requests that your access policies don't allow:

    ```
    spec:
      producerMetadata:
        iamEnforcementMode: "DRY_RUN"
    ```

    After you verify the logged decisions, remove `iamEnforcementMode` or set it to `ENFORCE` , and then reapply the manifest to enforce your policies.

4.  Apply the manifest:

    ```
    kubectl apply -f iap-binding.yaml
    ```

5.  Wait for the binding to be reconciled:

    ```
    kubectl wait --for=condition=Reconciled=True \
        gcpextensionbinding/BINDING_NAME \
        -n GATEWAY_NAMESPACE \
        --timeout=300s
    ```

## What's next

- [Configure cross-cloud agent observability](https://docs.cloud.google.com/gemini-enterprise-agent-platform/agents/governance/agent-gateway-cross-cloud/observability)
- [Learn about policies](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/policies/overview-uap)
- [Configure Model Armor on a gateway](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/configure-model-armor)
