---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/govern/gateways/set-up-agent-gateway
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/gateways/set-up-agent-gateway
title: Set up Agent Gateway
description: Secure and govern AI agent connectivity with Agent Gateway. Centralize access policies, mTLS, and Model Context Protocol (MCP) security for agent-to-agent and agent-to-tool interactions across diverse runtimes.
data_source: docs.cloud.google.com
---

To centralize access control and secure connectivity across your agentic workflows, you can set up an Agent Gateway resource to manage ingress or egress traffic.

Before you set up a gateway, review the conceptual basics and core components in the [Agent Gateway overview](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/gateways/agent-gateway-overview) .

## Required permissions

The following permissions are required to create and manage Agent Gateways. You can get these permissions either with [custom roles](https://docs.cloud.google.com/iam/docs/creating-custom-roles) or by using other [predefined roles](https://docs.cloud.google.com/iam/docs/roles-overview#predefined) .

#### Required permissions

  - `compute.networkAttachments.list`
  - `compute.regions.list`
  - `modelarmor.templates.list`
  - `networksecurity.authzPolicies.create`
  - `networksecurity.authzPolicies.delete`
  - `networksecurity.authzPolicies.get`
  - `networksecurity.authzPolicies.list`
  - `networksecurity.operations.get`
  - `networkservices.agentGateways.create`
  - `networkservices.agentGateways.delete`
  - `networkservices.agentGateways.get`
  - `networkservices.agentGateways.list`
  - `networkservices.agentGateways.update`
  - `networkservices.agentGateways.use`
  - `networkservices.authzExtensions.create`
  - `networkservices.authzExtensions.delete`
  - `networkservices.authzExtensions.get`
  - `networkservices.authzExtensions.list`
  - `networkservices.authzExtensions.update`
  - `networkservices.authzExtensions.use`
  - `networkservices.operations.get`

> **Note:** Because Workforce Identity Federation is in Preview, it has limited support for Agent Platform and Agent Gateway. If you encounter loading, creation, or import errors in Google Cloud console or gcloud CLI, access the service using a standard Google Account managed through Cloud Identity or Google Workspace.

## Required APIs

Enable the following APIs in the Google Cloud project that you are using for this guide. These APIs let you access the full suite of capabilities offered by Gemini Enterprise Agent Platform. Review the rationale for each API to determine which services are required for your specific architecture and governance needs.

#### Required APIs

  - **Core APIs for Agent Gateway operations:**
      - **Compute Engine API ( `compute.googleapis.com` ):** Provides core networking infrastructure, subnets, routing, and Private Service Connect (PSC) network attachments.
      - **Network Security API ( `networksecurity.googleapis.com` ):** Creates and enforces authorization policies ( `authzPolicies` ) for gateway traffic.
      - **Network Services API ( `networkservices.googleapis.com` ):** Manages core Agent Gateway resources and authorization extensions ( `authzExtensions` ).
      - **Identity and Access Management API ( `iam.googleapis.com` ):** Manages agent identities, service accounts, and IAM access policies.
      - **Identity-Aware Proxy API ( `iap.googleapis.com` ):** Authenticates and verifies agent, endpoint, and server traffic.
      - **Agent Registry API ( `agentregistry.googleapis.com` ):** Registers and manages agents, MCP servers, and tool endpoints governed by the gateway.
      - **Model Armor API ( `modelarmor.googleapis.com` ):** Configures Model Armor guardrails to inspect and filter prompt injection, toxic content, and sensitive data.
      - **Cloud DNS API ( `dns.googleapis.com` ):** Handles private DNS routing and domain resolution for private VPC egress.
  - **Observability APIs:**
      - **Cloud Logging API ( `logging.googleapis.com` ):** Captures gateway access logs, security audit logs, and dry-run policy evaluation events.
      - **Cloud Monitoring API ( `monitoring.googleapis.com` ):** Tracks gateway health, latency, throughput, error rates, and configures operational alerts.
      - **Observability API ( `observability.googleapis.com` ):** Provides unified observability and operational dashboards for agent and gateway activity.
      - **Telemetry API ( `telemetry.googleapis.com` ):** Collects and streams runtime telemetry and performance metrics across platform components.
      - **Cloud Trace API ( `cloudtrace.googleapis.com` ):** Provides distributed tracing to inspect multi-hop requests across agents and backends.
  - **Agent runtime APIs:**
      - **Vertex AI API ( `aiplatform.googleapis.com` ):** Powers Agent Runtime agents, foundation models, and integrated platform services.
      - **Discovery Engine API ( `discoveryengine.googleapis.com` ):** Powers Gemini Enterprise apps, search, grounding, and knowledge retrieval tools.
      - **Cloud Storage API ( `storage.googleapis.com` ):** Stores agent configurations, prompt templates, artifacts, and file attachments.
  - **Full scope & platform integration APIs:**
      - **App Hub API ( `apphub.googleapis.com` ):** Organizes, discovers, and governs application-centric agent platform resources.
      - **App Topology API ( `apptopology.googleapis.com` ):** Visualizes dependency maps and service topologies across agents, gateways, and backends.
      - **Cloud API Registry ( `cloudapiregistry.googleapis.com` ):** Catalogs enterprise APIs and services that agents connect to through the gateway.
      - **Notebooks API ( `notebooks.googleapis.com` ):** Supports agent prototyping and evaluation in Vertex AI Workbench and Colab Enterprise.
      - **Text-to-Speech API ( `texttospeech.googleapis.com` ):** Provides speech synthesis for voice-enabled agents and multimodal pipelines.
      - **Dataform API ( `dataform.googleapis.com` ):** Manages data preparation and transformation workflows leveraged by data agents.

## Plan your Agent Gateway deployment

Use this section to plan your Agent Gateway deployment and understand governance architecture requirements. You can revisit these steps as you register new destinations, add new access control policies, or deploy more agents.

### Choose your deployment mode

Agent Gateway supports two deployment modes:

  - **Client-to-Agent (ingress)** : Secures communications from clients to your agents running on Google Cloud.
  - **Agent-to-Anywhere (egress)** : Secures communications from your agents to external targets, public APIs, and MCP servers.

### Select your runtime, project, and region of deployment

Agent Gateway governs traffic from agents running on Gemini Enterprise and Runtime.

  - **Agent Runtime** : Agent Gateway supports both Agent-to-Anywhere (egress) and Client-to-Agent (ingress) modes. In Agent-to-Anywhere mode, agents can be either in the same project as the gateway or in a different one. In Client-to-Agent mode, agents must be in the same project as the gateway. In either mode, agents must be in the same region as the gateway.

  - **Gemini Enterprise** : Agent Gateway supports only Agent-to-Anywhere (egress) mode. With Gemini Enterprise, each gateway governs agentic interactions only within the scope of the project and region it is deployed in.

To govern agents across Gemini Enterprise and Runtime, you can use a single Agent Gateway instance. Alternatively, you can also deploy independent Agent Gateway instances for Gemini Enterprise and Runtime.

#### Sample deployment patterns

Here are some sample deployment patterns for your consideration:

  - Cross-project governance for Runtime agents  
    In this deployment pattern, you deploy an Agent-to-Anywhere (egress) Agent Gateway in a dedicated governance project. Runtime agents are deployed in separate projects in the same region as the gateway and can belong to any folder within your organization.
    
    To set up cross-project egress governance, you configure the following resources:
    
    In the **central governance project** :
    
      - Create the Agent Gateway. Ensure that the gateway is associated with an Agent Registry instance.
      - Register cross-project agents along with any tools, servers, or endpoints with the Agent Registry attached to the gateway.
      - Grant cross-project IAM permissions to the Runtime service agent of each project where the agents are based so that agents in these projects can bind to the gateway in the governance project. For an example, see [Route Runtime traffic through Agent Gateway](https://docs.cloud.google.com/gemini-enterprise-agent-platform/scale/runtime/agent-gateway-runtime-deploy) .
      - Configure IAP policies, Principal Access Boundaries, and SPIFFE-compatible workload identities to govern and secure egress traffic to authorized endpoints.
      - Create any Model Armor templates you want to use for egress.
      - If you want to [egress to a VPC network](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/gateways/set-up-vpc-connectivity) , you can create the PSC network attachment and DNS peering configuration in the governance project.
    
    In the **Agent Runtime projects** :
    
      - Deploy the agents and bind them to the central gateway in the governance project.
    
    Note that cross-project governance is supported only for Runtime with Agent-to-Anywhere (egress) gateways; Gemini Enterprise is not supported.

  - Shared governance for Gemini Enterprise and Runtime agents  
    In this deployment pattern, all traffic from Gemini Enterprise apps and Runtime agents routes through a single Agent Gateway.
    
    Here is a sample deployment:
    
      - The Gemini Enterprise app is deployed as a `global` deployment.
      - Runtime agents are deployed within a single region ( `us-central1` ) that [corresponds to the Gemini Enterprise deployment](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/gateways/agent-gateway-ge-deploy#plan-ge-agw) .
      - The Agent Gateway is deployed in the same region ( `us-central1` ).
      - Both `global` and `us-central1` Agent Registry instances can be associated with the Agent Gateway. Agents and destinations must be registered with the Agent Registry instances associated with the gateway.

  - Independent governance for Gemini Enterprise and Runtime agents  
    In this deployment pattern, each region has a dedicated Agent Gateway to monitor and govern agent traffic, ensuring regional isolation:
    
      - The Gemini Enterprise app is deployed as a global or multi-region deployment (in `global` , `us` , or `eu` ).
      - Runtime agents are deployed in each region where needed.
      - Agent Gateway instances are deployed in each region where agents and apps are located.
      - You must register your agents and destinations in the Agent Registry instances associated with each gateway.

### Set up agent identity

Every agent governed by Agent Gateway requires its own unique Agent Identity (a SPIFFE ID). Because IAM access policies depend on this workload identity, traffic from unidentified agents is blocked by default.

You can provision an Agent Identity when you deploy an agent in Runtime or assign it to existing agent workloads. For detailed instructions, see [Use Agent Identity with Runtime](https://docs.cloud.google.com/gemini-enterprise-agent-platform/scale/runtime/agent-identity) .

### Register your agents and destination resources

To enable secure communication, you must identify your Agent Registry instance and register the resources that your gateway will govern.

1.  Identify the Agent Registry instances that you will be using. An Agent Gateway can be associated with up to two registries (one global registry and one regional or multi-regional registry):
    
      - **Agent Runtime agents** are regional resources and are typically registered in regional registries matching their deployment region. Note that cross-project agents must be registered in the registry associated with the central governance project where the Agent Gateway is deployed.
      - **Gemini Enterprise agents** are global or multi-region resources and are registered in global or multi-regional registries (such as `global` , `us` , or `eu` ).
    
    Ensure that the registry instances you associate with your Agent Gateway are the ones where your agents, endpoints, and servers are registered.
    
    > **Note:** Regional and multi-regional entries take precedence over global entries when Agent Gateway resolves a destination URL to a registry entry. This is to help resolve conflicts that can occur when regional, multi-regional, and global registries contain entries with identical interface URLs.

2.  Register your agents with Agent Registry. If you haven't already created the agent, you must complete this step later. For instructions, see [Register agents](https://docs.cloud.google.com/agent-registry/register-agents) .

3.  Recommended: Identify and register all tools, MCP servers, and API endpoints your agents will call (including [essential platform APIs](https://docs.cloud.google.com/gemini-enterprise-agent-platform/scale/runtime/agent-gateway-runtime-deploy) ). Agent access to destinations always requires an IAM Access policy granting the `iap.resources.egressViaIAP` permission to the agent identity. We recommend registering resources in Agent Registry so that you can enforce granular, per-resource policies and tool-level controls. For destinations that are not registered, you must grant this permission to the agent by configuring policies for [unregistered endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/policies/iam-overview-uap#unregistered-resources) .
    
    Destinations in a different project than the gateway must be registered with the Agent Registry in the gateway project. Such destinations are only valid for Runtime agents in Agent-to-Anywhere mode.
    
    For instructions, see the following guides:
    
      - [Register MCP servers](https://docs.cloud.google.com/agent-registry/register-mcp-servers)
      - [Register endpoints](https://docs.cloud.google.com/agent-registry/register-endpoints)

### Configure access control policies

Every Agent Gateway requires an associated authorization policy.

  - IAM (Agent-to-Anywhere mode only)  
    Configure an IAM policy that assigns the `iap.resources.egressViaIAP` permission to your agent identity principal for each of the destination resources that you registered in Agent Registry.
    
    By default, Agent Gateway blocks all traffic unless an IAM access policy explicitly authorizes agent access to [destination resources](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/policies/iam-overview-uap#destination-resources) by granting the `iap.resources.egressViaIAP` permission to the agent identity.
    
    Registering destinations in Agent Registry is recommended because it lets you scope policies to specific resources and apply fine-grained tool controls. If destinations are not registered in Agent Registry, you must grant the `iap.resources.egressViaIAP` permission to the agent by configuring a policy for [unregistered endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/policies/iam-overview-uap#unregistered-resources) .
    
    Because registries can be global, multi-regional, or regional, ensure that any registry-wide binding matches the registry instance (or instances) configured for your Agent Gateway.
    
    For instructions, see [Create IAM agent policies](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/policies/configure-iam-policies-uap) .
    
    To validate your configuration without blocking traffic, we recommend that you deploy IAP in dry-run mode initially.
    
    > **Note:** Turn off enforcement for the **Disable binding access policy to resource** ( `constraints/iam.managed.disableAccessPolicyBindings` ) managed organization policy constraint. By default, this boolean constraint is enabled for new organizations, and will prevent you from binding an IAM Unified Access Policy to a resource. For more information, see [Updating policies with boolean rules](https://docs.cloud.google.com/organization-policy/apply-policies#boolean_constraints) .

  - Model Armor  
    (Optional) If your deployment requires safeguarding against prompt injection attacks, jailbreaks, toxic content, or sensitive data leakage, you should plan your Model Armor guardrail integration and create templates with the safety filters you require.
    
    For more information, see the following documents:
    
      - [Configure Model Armor on a gateway](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/configure-model-armor)
      - [Delegate authorization using Service Extensions](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/gateways/delegate-authorization#configure-authz-ma)

  - Semantic Governance Policies  
    (Optional) You can opt to add natural language-based context-aware controls on your agents to enable protections against toxic combinations of tools.
    
    We recommend that you start by deploying Semantic Governance Policies in dry-run mode so that you can validate your configuration without blocking traffic. For details, see [Configure semantic governance policies](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/policies/configure-semantic-governance) .

  - Custom authorization engines  
    (Optional) If you want to delegate authorization to custom authorization engines or third party systems by using Service Extensions, you should ensure that the custom authorization engines are available when deploying the gateway.

Model Armor, Semantic Governance Policies, and any other custom authorization engines can be enabled either during initial Agent Gateway setup or attached post-deployment as an incremental security policy update.

## Configure Agent Gateway in Agent-to-Anywhere (egress) mode

This section shows you how to set up an Agent Gateway for [Agent-to-Anywhere](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/gateways/agent-gateway-overview#modes) communications.

Use the following steps to create an Agent Gateway resource.

### Google Cloud console

1.  In the Google Cloud console, go to the **Agent Gateway** page.

2.  Click **Add gateway** .

3.  Enter a **Name** .

4.  From the **Region** list, select a region.

5.  For **Deployment mode** , verify that **Google-managed** is selected.

6.  For **Agent registries** , select at least one registry from the list. If you want to select two registries, one must be a global registry and the other can be either a regional or multi-regional registry.For guidance on which registry to choose for your deployment, see [Plan your Agent Gateway deployment](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/gateways/set-up-agent-gateway#plan-agw) .

7.  From the **Governed Access Path** list, select **Agent-to-Anywhere (Agent Egress)** .

8.  In the **Access Authorization** section, choose how traffic is handled by IAP:
    
      - To deploy the gateway in a dry-run mode where the gateway permits all traffic through and only generates [audit logs](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/gateways/monitor-agent-gateway) , select **Audit-only** . Your IAM policies are not enforced by IAP in dry-run mode. Once you gain confidence, you can disable dry-run mode to enforce IAM policies.
      - To block requests that don't have an explicit `Allow` IAM policy, select **Enforce policies** . This option is recommended for production environments.
      - For **Policy model** , select **Unified Access Policy** .
    
    > **Note:** We strongly recommend using Unified Access Policy for advanced, expressive, and fine-grained access control. To replace a legacy Allow policy on an existing gateway, navigate to the Policies UI and manually redefine your rules under the Unified Access Policy tab. For more information, see [Create IAM agent policies](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/policies/configure-iam-policies-uap) .

9.  Optional: In the **AI Security** section, configure additional security:
    
    1.  To protect AI model interactions with Model Armor, turn on **Enable Model Armor** .
    
    2.  Select a [template](https://docs.cloud.google.com/model-armor/manage-templates) that applies to incoming requests to the gateway from the list.
    
    3.  To use a different template for responses, clear **Use same template for requests and responses** and select a template from the list.
        
        > **Important:** When you're using Model Armor, you must grant the Agent Gateway service account the permissions required to be able to use the Model Armor templates. For details, see [Delegate authorization to Model Armor](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/gateways/delegate-authorization#configure-authz-ma) .

10. Click **Add Gateway** .

### gcloud

You define Agent Gateways declaratively using YAML.

1.  Define the resource and save the configuration to a YAML file. For this example, we use `my-agent-gateway-egress.yaml` .
    
        name: AGENT_GATEWAY_NAME
        protocols:
          - MCP
        googleManaged:
          governedAccessPath: AGENT_TO_ANYWHERE
        registries:
          - AGENT_REGISTRY_URI_1
          - OPTIONAL_AGENT_REGISTRY_URI_2
    
    Replace the following:
    
      - `  AGENT_GATEWAY_NAME  ` : The name of the Agent Gateway resource.
    
      - `  AGENT_REGISTRY_URI_1  ` and `  OPTIONAL_AGENT_REGISTRY_URI_2  ` : The paths to the Agent Registry instances to be associated with the gateway. You can configure up to two registries for an Agent Gateway. When configuring two registries, one must be a global registry and the other can be either a regional or multi-regional registry. For guidance on which registry to choose for your deployment, see [Plan your Agent Gateway deployment](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/gateways/set-up-agent-gateway#plan-agw) . The registry paths must be formatted as follows:
        
          - Regional registries: ` //agentregistry.googleapis.com/projects/ PROJECT_ID /locations/ REGION  `
          - Global registries: `//agentregistry.googleapis.com/projects/ PROJECT_ID /locations/global`
          - Multi-region registries: ` //agentregistry.googleapis.com/projects/ PROJECT_ID /locations/ MULTI_REGION  `

2.  Run the following command to create an Agent Gateway resource based on the YAML specification:
    
        gcloud network-services agent-gateways import AGENT_GATEWAY_NAME \
         --source="my-agent-gateway-egress.yaml" \
         --location=LOCATION
    
    Replace `  LOCATION  ` with the location where you want to create the Agent Gateway resource. For example, `us-central1` .
    
    Note that for Gemini Enterprise, you must deploy Agent Gateway in a region that corresponds to your multi-region setup. For the supported location mappings, see [Route Gemini Enterprise traffic through Agent Gateway](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/gateways/agent-gateway-ge-deploy#route-traffic) .

3.  Create an authorization policy to enforce centralized access control and governance policies on traffic passing through the Agent Gateway. The following steps show you how to configure an authorization policy that uses IAP.
    
    1.  Configure an authorization extension that points to IAP. Define the extension in a YAML file, such as `iap-request-authz-extension.yaml` . Use the sample values provided:
        
            cat >iap-request-authz-extension.yaml <<EOF
            name: AUTHORIZATION_EXTENSION_NAME
            service: iap.googleapis.com
            failOpen: false
            timeout: 1s
            metadata:
              iapPolicyVersion: "V2"
            EOF
        
        If you want to deploy the extension in a dry run *audit-only* mode to test the authorization policy without enforcing it, you can specify the `iamEnforcementMode` field inside the `metadata` block. This lets you verify your policy and minimize the risk of disrupting traffic due to configuration errors:
        
            cat >iap-request-authz-extension.yaml <<EOF
            name: AUTHORIZATION_EXTENSION_NAME
            service: iap.googleapis.com
            failOpen: false
            timeout: 1s
            metadata:
              iapPolicyVersion: "V2"
              iamEnforcementMode: "DRY_RUN"
            EOF
        
        Remove the `iamEnforcementMode: "DRY_RUN"` field from the `metadata` block when you're ready to start enforcing policies.
        
        > **Note:** We strongly recommend using Unified Access Policy ( `iapPolicyVersion: "V2"` ) for advanced, expressive, and fine-grained access control. To replace a legacy Allow policy ( `iapPolicyVersion: "V1"` ) on an existing gateway, navigate to the Policies UI and manually redefine your rules under the Unified Access Policy tab. For more information, see [Create IAM agent policies](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/policies/configure-iam-policies-uap) .
    
    2.  Import the YAML configuration file to an authorization extension.
        
            gcloud beta service-extensions authz-extensions import AUTHORIZATION_EXTENSION_NAME \
              --source=iap-request-authz-extension.yaml \
              --location=LOCATION
        
        Replace `  AUTHORIZATION_EXTENSION_NAME  ` with the name of the authorization extension—for example, `my-iap-request-authz-ext` .
    
    3.  Define an authorization policy in a YAML file, such as `iap-request-authz-policy.yaml` , to associate the extension with your gateway:
        
            cat >iap-request-authz-policy.yaml <<EOF
            name: AUTHORIZATION_POLICY_NAME
            target:
              resources:
                - "projects/PROJECT_ID/locations/LOCATION/agentGateways/AGENT_GATEWAY_NAME"
            policyProfile: REQUEST_AUTHZ
            action: CUSTOM
            customProvider:
              authzExtension:
                resources:
                  - "projects/PROJECT_ID/locations/LOCATION/authzExtensions/AUTHORIZATION_EXTENSION_NAME"
            EOF
        
        Replace the following:
        
          - `  AUTHORIZATION_POLICY_NAME  ` : the name of the authorization policy—for example, `my-iap-request-authz-policy`
          - `  PROJECT_ID  ` : the [project ID](https://docs.cloud.google.com/resource-manager/docs/creating-managing-projects#identifying_projects)
    
    4.  Import the YAML configuration file to an authorization policy.
        
            gcloud network-security authz-policies import AUTHORIZATION_POLICY_NAME \
              --source=iap-request-authz-policy.yaml \
              --location=LOCATION

4.  Optional: If you want to configure Model Armor guardrails to help protect your deployment against prompt injection attacks and sensitive data leaks, see [Delegate authorization to Model Armor](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/gateways/delegate-authorization#configure-authz-ma) .

<!-- end list -->

1.  After an Agent Gateway has been created, it serves as the primary connection point for routing agent traffic within your project and chosen region. You can now use this endpoint to establish secure, encrypted, and authenticated communication channels between agents and their destinations (tools, other agents, or other endpoints).
    
    Review the [Plan your Agent Gateway deployment](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/gateways/set-up-agent-gateway#plan-agw) section on this page again and make sure that your agents are registered with Agent Registry and that your agent has been granted the `iap.resources.egressViaIAP` permission for all the destinations it is attempting to connect to. If you encounter connectivity issues, see [Troubleshoot Agent Gateway connectivity](https://docs.cloud.google.com/gemini-enterprise-agent-platform/troubleshooting/troubleshoot-agent-gateway) .

Next, learn how to [deploy agents and route traffic through Agent Gateway](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/gateways/set-up-agent-gateway#route-traffic) .

### Optional: Configure VPC connectivity

To configure your Agent Gateway so that it can privately communicate with a VPC network in your organization, see [Set up VPC connectivity for Agent Gateway](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/gateways/set-up-vpc-connectivity) .

**VPC Service Controls enforcement** : Setting up VPC connectivity is required to enable VPC Service Controls perimeter enforcement for Agent Gateway deployments. The connectivity template must be configured in `ALL_TRAFFIC` egress mode.

> **Important:** VPC Service Controls is only supported for Agent Gateway deployments created after September 8, 2026 that use the agent connectivity template to configure VPC connectivity.

## Configure Agent Gateway in Client-to-Agent (ingress) mode

This section shows you how to set up an Agent Gateway for [Client-to-Agent](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/gateways/agent-gateway-overview#modes) communications.

Use the following steps to create an Agent Gateway resource.

### Google Cloud console

1.  In the Google Cloud console, go to the **Agent Gateway** page.

2.  Click **Add gateway** .

3.  Enter a **Name** .

4.  From the **Region** list, select a region.

5.  For **Deployment mode** , verify that **Google-managed** is selected.

6.  Leave the **Agent registry** setting as is. The registry isn't used for ingress.

7.  From the **Governed Access Path** list, select **Client-to-Agent (ingress)** .

8.  Optional: In the **AI Security** section, configure additional security:
    
    1.  To protect AI model interactions with Model Armor, turn on **Enable Model Armor** .
        
        > **Note:** If your Model Armor templates are in a different project from the gateway, you'll need to manually grant certain permissions to the Agent Gateway service account. For details, see [Delegate authorization to Model Armor](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/gateways/delegate-authorization#configure-authz-ma) .
    
    2.  Select a [template](https://docs.cloud.google.com/model-armor/manage-templates) that applies to incoming requests to the gateway from the list.
    
    3.  To use a different template for responses, clear **Use same template for requests and responses** and select a template from the list.

9.  Click **Add Gateway** .

### gcloud

You define Agent Gateways declaratively using YAML.

1.  Define the resource and save the configuration to a YAML file. For this example, we use `my-agent-gateway-ingress.yaml` .
    
        name: AGENT_GATEWAY_NAME
        protocols:
          - MCP
        googleManaged:
          governedAccessPath: CLIENT_TO_AGENT
    
    Replace AGENT\_GATEWAY\_NAME with a name for the Agent Gateway resource.

2.  Run the following command to create an Agent Gateway resource based on the YAML specification:
    
        gcloud network-services agent-gateways import AGENT_GATEWAY_NAME \
         --source="my-agent-gateway-ingress.yaml" \
         --location=LOCATION
    
    Replace `  LOCATION  ` with the location where you want to create the Agent Gateway resource. For example, `us-central1` .

After an Agent Gateway has been created, it serves as the primary connection point for routing traffic to agents in your project and chosen region.

Next, learn how to deploy agents and route traffic through Agent Gateway.

## Deploy agents and route traffic through Agent Gateway

To deploy a Agent Runtime agent that routes traffic through Agent Gateway, see [Route traffic through Agent Gateway](https://docs.cloud.google.com/gemini-enterprise-agent-platform/scale/runtime/agent-gateway-runtime-deploy) .

To deploy a Gemini Enterprise agent that routes traffic through Agent Gateway, see [Route Gemini Enterprise traffic through Agent Gateway](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/gateways/agent-gateway-ge-deploy) .

## Codelabs

For end-to-end demonstrations on how to set up and use Agent Gateway, see the following codelabs:

  - **[Govern agentic workloads with Agent Platform](https://codelabs.developers.google.com/cloudnet-agent-gateway)** : Learn how to deploy a governed ADK agent on Agent Runtime.
  - **[Agent Gateway egress from Agent Runtime to Google Cloud MCP servers](https://codelabs.developers.google.com/agw-cuj-arun-egress-gmcp)** : Learn how to configure Agent Gateway in Agent-to-Anywhere mode to govern ADK agent calls to a Google Cloud MCP servers.
  - **[Agent Gateway egress from Agent Runtime to external MCP servers](https://codelabs.developers.google.com/agw-cuj-arun-egress-emcp)** : Learn how to configure Agent Gateway in Agent-to-Anywhere mode to govern ADK agent calls to external MCP servers.
  - **[Agent Gateway egress from Agent Runtime to VPC network](https://codelabs.developers.google.com/agw-cuj-arun-egress-vpc)** : Learn how to configure Agent Gateway in Agent-to-Anywhere mode to govern ADK agent calls to destinations in a VPC network.

## What's next

Guide

### [Route Agent Runtime traffic through Agent Gateway](https://docs.cloud.google.com/gemini-enterprise-agent-platform/scale/runtime/agent-gateway-runtime-deploy)

Learn how to route Agent Runtime traffic through Agent Gateway for secure and governed connectivity.

Guide

### [Delegate authorization for Agent Gateway](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/gateways/delegate-authorization)

Learn how to delegate authorization for Agent Gateway to IAP, Model Armor, or your own custom authorization service.

Guide

### [Monitor Agent Gateway](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/gateways/monitor-agent-gateway)

Learn how to monitor Agent Gateway.

Troubleshooting

### [Troubleshoot Agent Gateway](https://docs.cloud.google.com/gemini-enterprise-agent-platform/troubleshooting/troubleshoot-agent-gateway)

Learn how to troubleshoot Agent Gateway connectivity.

Guide

### [Route Gemini Enterprise traffic through Agent Gateway](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/gateways/agent-gateway-ge-deploy)

Learn how to route Gemini Enterprise traffic through Agent Gateway.
