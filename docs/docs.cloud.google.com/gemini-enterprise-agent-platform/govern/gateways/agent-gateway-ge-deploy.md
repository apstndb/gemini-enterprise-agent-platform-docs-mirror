---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/govern/gateways/agent-gateway-ge-deploy
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/gateways/agent-gateway-ge-deploy
title: Route Gemini Enterprise traffic through Agent Gateway
description: Deploy an agent on Gemini Enterprise and route traffic through Agent Gateway.
data_source: docs.cloud.google.com
---

> **Private Preview — Agent Gateway**
> 
> This feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](https://cloud.google.com/terms/service-terms#1) . This feature provides capabilities to govern and secure AI Agents, so the "Agentic AI Services" Service Specific Terms apply. Pre-GA features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

> **Feature access:** Your project must be on the allowlist before you can use Agent Gateway with Gemini Enterprise. Contact your Google Cloud account team for more information.

This page describes how to route Gemini Enterprise traffic through Agent Gateway. Agent Gateway is a central networking and security component of the Gemini Enterprise Agent Platform ecosystem. It provides secure and governed connectivity for all agentic interactions, whether they occur between users and agents, agents and tools, or among agents themselves.

## Before you begin

  - Make sure you are familiar with [Gemini Enterprise concepts](https://docs.cloud.google.com/gemini/enterprise/docs/concepts)
  - Learn about [Agent Gateway](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/gateways/agent-gateway-overview) . Note that Agent Gateway only supports Gemini Enterprise in Agent-to-Anywhere (egress) mode. Ingress traffic isn't supported.
  - [Create a dedicated test project](https://docs.cloud.google.com/resource-manager/docs/creating-managing-projects) to try this workflow. Avoid using projects that are also intended for other critical workloads.
  - Deploy a Gemini Enterprise app (also referred to as engine). The procedure on this page assumes that you already have an app deployed. For details, see [Create an app](https://docs.cloud.google.com/gemini/enterprise/docs/create-app) .

## Permissions required

Grant the Discovery Engine Service Agent (that is, the Google-managed service account for your project's Gemini Enterprise instance) the following permissions so that the Discovery Engine Service Agent can discover resources and route traffic.

  - **For Agent Registry:**
    
      - `agentregistry.agents.list`
      - `agentregistry.agents.search`
      - `agentregistry.agents.get`
      - `agentregistry.mcpServers.list`
      - `agentregistry.mcpServers.search`
      - `agentregistry.mcpServers.get`

  - **For Agent Gateway:**
    
      - `networkservices.agentGateways.list`
      - `networkservices.agentGateways.get`
      - `networkservices.agentGateways.use`

Use the following steps to grant permissions to the Discovery Engine Service Agent.

1.  Create a [custom role](https://docs.cloud.google.com/iam/docs/creating-custom-roles) with these permissions.
    
        gcloud alpha iam roles create AGENT_GATEWAY_ROLE_NAME \
        --project=PROJECT_ID \
        --title="Custom Agent Gateway and Agent Registry access role" \
        --description="Custom role for Agent Gateway and Agent Registry access" \
        --permissions="agentregistry.agents.list,agentregistry.agents.search,agentregistry.agents.get,agentregistry.mcpServers.list,agentregistry.mcpServers.search,agentregistry.mcpServers.get,networkservices.agentGateways.list,networkservices.agentGateways.get,networkservices.agentGateways.use"
    
    Replace the following:
    
      - `  AGENT_GATEWAY_ROLE_NAME  ` : The name for the custom role.
      - `  PROJECT_ID  ` : The project ID of the project where you deployed the agent.

2.  Assign the role to the Gemini Enterprise service account.
    
        gcloud alpha projects add-iam-policy-binding PROJECT_ID \
          --member="serviceAccount:service-PROJECT_NUMBER@gcp-sa-discoveryengine.iam.gserviceaccount.com" \
          --role="projects/PROJECT_ID/roles/AGENT_GATEWAY_ROLE_NAME"
    
    Replace the following:
    
      - `  PROJECT_ID  ` : Your project ID.
      - `  PROJECT_NUMBER  ` : Your project number.
      - `  AGENT_GATEWAY_ROLE_NAME  ` : The name of the custom role you created.

## Route Gemini Enterprise traffic through Agent Gateway

To route Gemini Enterprise traffic through Agent Gateway, perform the following steps:

1.  Register your agent with your Gemini Enterprise project's global instance of Agent Registry. Only traffic to and from registered agents, tools, and MCP servers is permitted through a gateway. For more information, see [Register an agent](https://docs.cloud.google.com/agent-registry/quickstart-register-agent) .

2.  Create an Agent Gateway resource and attach any authorization policies as needed. See [Set up Agent Gateway](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/gateways/set-up-agent-gateway) .
    
    **Location mapping:** To ensure proper routing, your Agent Gateway must be deployed in a specific region corresponding to your Gemini Enterprise multi-region setup. You must strictly adhere to the following mapping:
    
    | Gemini Enterprise location | Required Agent Gateway region |
    | -------------------------- | ----------------------------- |
    | `global`                   | `us-central1`                 |
    | `us`                       | `us-central1`                 |
    | `eu`                       | `europe-west1`                |
    

    Verify your gateway configuration. Use the Network Services API to retrieve your Agent Gateway configuration and inspect the settings.
    
        curl -X GET \
        -H "Authorization: Bearer $(gcloud auth application-default print-access-token)" \
        "https://networkservices.googleapis.com/v1alpha1/projects/PROJECT_ID/locations/AGENT_GATEWAY_REGION/agentGateways/AGENT_GATEWAY_NAME"
    
    Here is an example output for a properly configured gateway:
    
        {
          "name": "projects/my-ge-project/locations/us-central1/agentGateways/my-egress-gateway",
          "description": "A full configuration for Agent Gateway for Gemini Enterprise egress",
          "googleManaged": {
            "governedAccessPath": "AGENT_TO_ANYWHERE"
          },
          "protocols": [
            "MCP"
          ],
          "registries": [
            "//agentregistry.googleapis.com/projects/my-ge-project/locations/global"
          ]
        }

3.  Bind the gateway to your Gemini Enterprise engine by using the `UpdateEngine` API. Note that completing this step immediately routes all existing data connector traffic through the specified Agent Gateway.
    
        curl -X PATCH \
        -H "Authorization: Bearer $(gcloud auth print-access-token)" \
        -H "Content-Type: application/json" \
        -H "X-Goog-User-Project: PROJECT_ID" \
        -d '{
          "agentGatewaySetting": {
            "defaultEgressAgentGateway": {
              "name": "projects/PROJECT_ID/locations/AGENT_GATEWAY_REGION/agentGateways/AGENT_GATEWAY_NAME"
            }
          }
        }' \
        "https://discoveryengine.googleapis.com/v1/projects/PROJECT_NUMBER/locations/GE_LOCATION/collections/default_collection/engines/ENGINE_ID?updateMask=agentGatewaySetting.defaultEgressAgentGateway.name"
    
    Replace the following:
    
      - `  PROJECT_ID  ` : The project ID.
      - `  AGENT_GATEWAY_REGION  ` : The region of the Agent Gateway.
      - `  AGENT_GATEWAY_NAME  ` : The name of the Agent Gateway.
      - `  PROJECT_NUMBER  ` : The project number.
      - `  GE_LOCATION  ` : The location of the Gemini Enterprise engine (for example, `us` or `global` ).
      - `  ENGINE_ID  ` : The ID of the Gemini Enterprise engine.

4.  Verify the engine configuration. Use the following command to retrieve your engine configuration and inspect the settings:
    
        curl -s -X GET \
        -H "Authorization: Bearer $(gcloud auth application-default print-access-token)" \
        -H "X-Goog-User-Project: PROJECT_ID" \
        -H "Content-Type: application/json" \
        "https://discoveryengine.googleapis.com/v1/projects/PROJECT_NUMBER/locations/GE_LOCATION/collections/default_collection/engines/ENGINE_ID" \
        | jq '{name: .name, displayName: .displayName, agentGatewaySetting: .agentGatewaySetting}'
    
    Here is an example output for a properly configured engine:
    
        {
        "name": "projects/PROJECT_NUMBER/locations/GE_LOCATION/collections/default_collection/engines/ENGINE_ID",
        "displayName": "ENGINE_ID",
        "agentGatewaySetting": {
          "defaultEgressAgentGateway": {
            "name": "projects/PROJECT_ID/locations/AGENT_GATEWAY_REGION/agentGateways/AGENT_GATEWAY_NAME"
          }
        }
        }

5.  While egress governance is now enabled for your Gemini Enterprise instance (and immediately active for data connectors), your engine does not automatically know which external endpoints on the Agent Registry to interact with. Therefore, you must complete the following steps:
    
      - **Import Agent Registry resources** : Explicitly import the chosen Agent Registry agent or MCP server into your Gemini Enterprise Engine. The imported resource must be referenced using its exact Registry-based resource name from your project's global registry.
      - **Authorize data connectors** : If you are using data connectors rather than custom agents/MCP servers, navigate to the Gemini Enterprise web application UI, locate your connector, and click **Authorize** .

6.  To verify that egress is functioning correctly, perform the following steps:
    
    1.  Open the Gemini Enterprise web application.
    2.  Submit a query designed to trigger an external tool or data connector (for example, "Give me a list of recent issues from my GitHub connector").
    3.  Monitor the execution to ensure the response is successfully retrieved. Behind the scenes, the Gemini Enterprise agent packages the request, routes it through your Agent Gateway (which enforces any configured authorization policies), and retrieves the response from the destination.

## Restrict Gemini Enterprise binding to approved Agent Gateways

You can create custom organization policy constraints to restrict whether a Gemini Enterprise engine can bind to any or all Agent Gateways.

### Create custom organization policy constraints

This example creates a custom constraint that blocks all bindings between Gemini Enterprise engines and Agent Gateways.

### Agent-to-Anywhere

1.  To define a custom constraint for Agent-to-Anywhere mode (egress), create a file named `constraint-agent-gateway-egress.yaml` .
    
    The following example shows you how to enforce strict network isolation by disallowing any bindings. The `condition` field specifies that the operation is denied if an Agent Gateway resource is specified (field is present and not empty).
    
        name: organizations/ORGANIZATION_ID/customConstraints/custom.disallowGeminiEnterpriseAgentGatewayBinding
        resource_types:
        – discoveryengine.googleapis.com/Engine
        condition: >-
        has(resource.agentGatewaySetting.defaultEgressAgentGateway.name) &&
        resource.agentGatewaySetting.defaultEgressAgentGateway.name != ''
        actionType: DENY
        displayName: "Disallow all Agent Gateway Bindings for Discovery Engines"
        description: "To enforce strict network isolation, Discovery Engines are not permitted to bind to any Agent Gateway."
    
    Replace the following:
    
      - ORGANIZATION\_ID : your organization ID.
      - PROJECT\_ID : your project ID.
      - REGION : the region where the gateway was created.
      - AGENT\_GATEWAY\_NAME : your gateway name.

2.  Apply the custom constraint.
    
        gcloud alpha org-policies set-custom-constraint EGRESS_CONSTRAINT_PATH
    
    Replace EGRESS\_CONSTRAINT\_PATH with the full path to the custom constraint file created in the previous step.

3.  Create the organization policy to enforce the constraint. To define the organization policy, create a policy YAML file named `policy-agent-gateway-egress.yaml` . In this example we enforce this constraint at the project level but you might also set this at the organization or folder level.
    
        name: projects/PROJECT_ID/policies/custom.disallowGeminiEnterpriseAgentGatewayBinding
        spec:
        rules:
        – enforce: true
    
    Replace `  PROJECT_ID  ` with your project ID.

4.  Enforce the organization policy.
    
        gcloud alpha org-policies set-policy EGRESS_POLICY_PATH
    
    Replace EGRESS\_POLICY\_PATH with the full path to the organization policy YAML file created in the previous step. The policy requires up to 15 minutes to take effect.

For more information about how to use custom organization policy constraints, see [Create custom constraints](https://docs.cloud.google.com/organization-policy/create-custom-constraints) .

## What's next

Codelab

### [Codelab: Govern agentic workloads with Agent Platform](https://codelabs.developers.google.com/cloudnet-agent-gateway)

Learn how to govern agentic workloads with Agent Gateway on Gemini Enterprise Agent Platform.

Guide

### [Delegate authorization for Agent Gateway](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/gateways/delegate-authorization)

Learn how to delegate authorization for Agent Gateway to IAP, Model Armor, or your own custom authorization service.

Guide

### [Monitor Agent Gateway](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/gateways/monitor-agent-gateway)

Learn how to monitor Agent Gateway.
