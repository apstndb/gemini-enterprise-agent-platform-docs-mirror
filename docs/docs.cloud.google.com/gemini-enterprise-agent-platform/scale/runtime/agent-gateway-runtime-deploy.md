---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/scale/runtime/agent-gateway-runtime-deploy
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/scale/runtime/agent-gateway-runtime-deploy
title: Route Agent Runtime traffic through Agent Gateway
description: Deploy an agent on Agent Platform Runtime and route traffic through Agent Gateway.
data_source: docs.cloud.google.com
---

> **Private Preview — Agent Gateway**
> 
> This feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](https://cloud.google.com/terms/service-terms#1) . This feature provides capabilities to govern and secure AI Agents, so the "Agentic AI Services" Service Specific Terms apply. Pre-GA features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .
> 
> To request access to use Agent Gateway with Agent Runtime, see the [access request page](https://forms.gle/ZLNYKUDW7j2B4a8K7) .

This page describes how to route Agent Runtime traffic through Agent Gateway. Agent Gateway is a central networking and security component of the Gemini Enterprise Agent Platform ecosystem. It provides secure and governed connectivity for all agentic interactions, whether they occur between users and agents, agents and tools, or among agents themselves.

## Before you begin

  - Make sure you are familiar with [deploying agents on Agent Runtime](https://docs.cloud.google.com/gemini-enterprise-agent-platform/scale/runtime/deploy-an-agent) .

  - Learn about [Agent Gateway](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/gateways/agent-gateway-overview) . You can use Agent Gateway in Agent-to-Anywhere (egress) mode to secure and govern all outbound communications with outbound traffic to tools, models, APIs, and other agents. You use the gateway in Client-to-Agent (ingress) mode to control which clients can access your agents. The gateway lets you choose which IAP policies and Model Armor templates must be applied to these interactions.

  - [Create a dedicated test project](https://docs.cloud.google.com/resource-manager/docs/creating-managing-projects) to try this workflow. Avoid using projects that are also intended for other critical workloads.

### Limitations

  - While a single project and region can host multiple Agent-to-Anywhere (egress) and Client-to-Agent (ingress) Agent Gateway instances, all Agent Runtime agents deployed within that same project and region must bind to the same specific egress and ingress Agent Gateway instances.
    
    For example, if a project and region contains `egress-gateway-X` and `egress-gateway-Y` , all agents in that project and region must be configured to use the same gateway for egress. That is, either all agents use `egress-gateway-X` or all agents use `egress-gateway-Y` . You can't configure `agent-A` to use `egress-gateway-X` and `agent-B` to use `egress-gateway-Y` .
    
    This same binding rule applies to ingress gateways within a project and region as well.

  - The [Security Command Center Agent Engine Threat Detection service](https://docs.cloud.google.com/security-command-center/docs/agent-platform-threat-detection-overview) isn't available when Agent Gateway is enabled for an agent.

  - You can't unbind a Runtime agent from an Agent Gateway resource. For this reason, ensure that you use a dedicated test project.

## Route Agent Runtime traffic through Agent Gateway

To route Agent Runtime traffic through Agent Gateway, perform the following steps:

1.  Create an Agent Gateway resource and attach any authorization policies as needed. You can create a gateway either in Agent-to-Anywhere (egress) mode or Client-to-Agent (ingress) mode. Note that the agent and the gateway must be created in the same project and region. For instructions, see [Set up Agent Gateway](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/gateways/set-up-agent-gateway) .
    
    Ensure that the gateway is configured to meet your deployment's needs. For example, if your agent requires LLM access, configure the gateway to allow this access to prevent potential Agent Runtime deployment failures.

2.  Specify the gateway resource while deploying your agent. For example, to deploy the agent on Agent Runtime, use `client.agent_engines.create` to pass in the `local_agent` object along with any [optional configurations](https://docs.cloud.google.com/gemini-enterprise-agent-platform/scale/runtime/deploy-an-agent#configure-agent) .
    
    You must also make sure the Runtime instance is assigned an [agent identity](https://docs.cloud.google.com/gemini-enterprise-agent-platform/scale/runtime/agent-identity) by using the `identity_type` parameter as shown in this example.
    
        remote_agent = client.agent_engines.create(
          agent=local_agent,
          config={
              "agent_gateway_config": {
                "agent_to_anywhere_config": {"agent_gateway": AGENT_GATEWAY_TO_ANYWHERE_NAME},
                # "client_to_agent_config": {"agent_gateway": AGENT_GATEWAY_CLIENT_TO_AGENT_NAME}
              },
              "identity_type": types.IdentityType.AGENT_IDENTITY,
              # Other optional configuration ...
              # "requirements": requirements,
              # "gcs_dir_name": gcs_dir_name,
              # https://docs.cloud.google.com/gemini-enterprise-agent-platform/scale/runtime/agent-identity#opt-out-caa
              "env_vars": {
                "GOOGLE_API_PREVENT_AGENT_TOKEN_SHARING_FOR_GCP_SERVICES": False,
              }
          },
        )
    
    Replace `  AGENT_GATEWAY_TO_ANYWHERE_NAME  ` with the full path of the Agent Gateway you created in Agent-to-Anywhere (egress) mode. For example, ` projects/ PROJECT /locations/ REGION /agentGateways/ AGENT_GATEWAY_ID  ` .
    
    If you created a gateway in Client-to-Agent (ingress) mode, use the `client_to_agent_config` field instead and replace `  AGENT_GATEWAY_CLIENT_TO_AGENT_NAME  ` with the full path of the Agent Gateway you created for ingress.

3.  Register your agent with the Agent Registry instance in the same project and region as the agent and the gateway. For more information, see [Register an agent](https://docs.cloud.google.com/agent-registry/quickstart-register-agent) .

## Restrict Agent Runtime to approved Agent Gateways

You can create custom organization policy constraints to define the set of eligible Agent Gateway resources that can be used while deploying agents.

> **Note:** VPC Service Controls are not supported with Agent Gateway. However, if VPC Service Controls are enforced on the project, then these organization policies are required to ensure that agents only use sanctioned egress paths, preventing data exfiltration through unauthorized gateways.

### Create custom organization policy constraints

This example creates custom constraints that only allow traffic to and from a pre-approved list of gateways.

### Agent-to-Anywhere

1.  To define a custom constraint for Agent-to-Anywhere mode (egress), create a file named `constraint-agent-gateway-egress.yaml` .
    
    In the following example, the `condition` field specifies that the operation is allowed only if an Agent Gateway resource is specified (field is present and not empty) and if the specified gateway is in the pre-approved list.
    
        name: organizations/ORGANIZATION_ID/customConstraints/custom.allowlistedEgressAgentGatewaysForAgentEngine
        resource_types:
        - aiplatform.googleapis.com/ReasoningEngine
        condition: >-
        has(resource.spec.deploymentSpec.agentGatewayConfig.agentToAnywhereConfig.agentGateway) &&
        resource.spec.deploymentSpec.agentGatewayConfig.agentToAnywhereConfig.agentGateway != '' &&
        (resource.spec.deploymentSpec.agentGatewayConfig.agentToAnywhereConfig.agentGateway in [
          'projects/AGENT_PROJECT_ID_1/locations/REGION_1/agentGateways/AGENT_GATEWAY_ID_1',
          'projects/AGENT_PROJECT_ID_2/locations/REGION_2/agentGateways/AGENT_GATEWAY_ID_2',
        ])
        method_types:
        - CREATE
        - UPDATE
        action_type: ALLOW
        display_name: Restrict Reasoning Engine Egress to Approved Agent Gateways
        description: Reasoning Engines can only be bound to a pre-approved list of
        Agent Gateway instances. Binding to any other gateway is denied.
    
    Replace the following:
    
      - ORGANIZATION\_ID : your organization ID.
      - AGENT\_PROJECT\_ID : your project ID.
      - REGION : the region where the gateway was created.
      - AGENT\_GATEWAY\_ID : your gateway ID.

2.  Apply the custom constraint.
    
        gcloud alpha org-policies set-custom-constraint EGRESS_CONSTRAINT_PATH
    
    Replace EGRESS\_CONSTRAINT\_PATH with the full path to the custom constraint file created in the previous step.

3.  Create the organization policy to enforce the constraint. To define the organization policy, create a policy YAML file named `policy-agent-gateway-egress.yaml` . In this example we enforce this constraint at the project level but you might also set this at the organization or folder level.
    
        name: projects/AGENT_PROJECT_ID/policies/custom.allowlistedEgressAgentGatewaysForAgentEngine
        spec:
          rules:
          - enforce: true
    
    Replace `  AGENT_PROJECT_ID  ` with your project ID.

4.  Enforce the organization policy.
    
        gcloud alpha org-policies set-policy EGRESS_POLICY_PATH
    
    Replace EGRESS\_POLICY\_PATH with the full path to the organization policy YAML file created in the previous step. The policy requires up to 15 minutes to take effect.

### Client-to-Agent

1.  To define a custom constraint for Client-to-Agent mode (ingress), create a file named `constraint-agent-gateway-ingress.yaml` .
    
    In the following example, the `condition` field specifies that the operation is allowed only if an Agent Gateway resource is specified (field is present and not empty) and if the specified gateway is in the pre-approved list.
    
        name: organizations/ORGANIZATION_ID/customConstraints/custom.allowlistedIngressAgentGatewaysForAgentEngine
        resource_types:
        - aiplatform.googleapis.com/ReasoningEngine
        condition: >-
        has(resource.spec.deploymentSpec.agentGatewayConfig.clientToAgentConfig.agentGateway) &&
        resource.spec.deploymentSpec.agentGatewayConfig.clientToAgentConfig.agentGateway != '' &&
        (resource.spec.deploymentSpec.agentGatewayConfig.clientToAgentConfig.agentGateway in [
          'projects/AGENT_PROJECT_ID_1/locations/REGION_1/agentGateways/AGENT_GATEWAY_ID_1',
          'projects/AGENT_PROJECT_ID_2/locations/REGION_2/agentGateways/AGENT_GATEWAY_ID_2',
        ])
        method_types:
        - CREATE
        - UPDATE
        action_type: ALLOW
        display_name: Restrict Reasoning Engine Ingress to Approved Agent Gateways
        description: Reasoning Engines can only be bound to a pre-approved list of
        Agent Gateway instances. Binding to any other gateway is denied.
    
    Replace the following:
    
      - ORGANIZATION\_ID : your organization ID.
      - AGENT\_PROJECT\_ID : your project ID.
      - REGION : the region where the gateway was created.
      - AGENT\_GATEWAY\_ID : your gateway ID.

2.  Apply the custom constraint.
    
        gcloud alpha org-policies set-custom-constraint INGRESS_CONSTRAINT_PATH
    
    Replace INGRESS\_CONSTRAINT\_PATH with the full path to the custom constraint file created in the previous step.

3.  Create the organization policy to enforce the constraint. To define the organization policy, create a policy YAML file named `policy-agent-gateway-ingress.yaml` . In this example we enforce this constraint at the project level but you might also set this at the organization or folder level.
    
        name: projects/AGENT_PROJECT_ID/policies/custom.allowlistedIngressAgentGatewaysForAgentEngine
        spec:
          rules:
          - enforce: true
    
    Replace `  AGENT_PROJECT_ID  ` with your project ID.

4.  Enforce the organization policy.
    
        gcloud alpha org-policies set-policy INGRESS_POLICY_PATH
    
    Replace INGRESS\_POLICY\_PATH with the full path to the organization policy YAML file created in the previous step. The policy requires up to 15 minutes to take effect.

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
