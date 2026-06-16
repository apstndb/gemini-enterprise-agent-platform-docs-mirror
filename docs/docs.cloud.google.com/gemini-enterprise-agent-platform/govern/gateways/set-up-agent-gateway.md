---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/govern/gateways/set-up-agent-gateway
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/gateways/set-up-agent-gateway
title: Set up Agent Gateway
description: Secure and govern AI agent connectivity with Agent Gateway. Centralize access policies, mTLS, and Model Context Protocol (MCP) security for agent-to-agent and agent-to-tool interactions across diverse runtimes.
data_source: docs.cloud.google.com
---

> **Private Preview — Agent Gateway**
> 
> This feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](https://cloud.google.com/terms/service-terms#1) . This feature provides capabilities to govern and secure AI Agents, so the "Agentic AI Services" Service Specific Terms apply. Pre-GA features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .
> 
> To request access to use Agent Gateway with Agent Runtime, see the [access request page](https://forms.gle/ZLNYKUDW7j2B4a8K7) .

This page guides you through the process of creating an Agent Gateway resource. If you haven't already done so, review the conceptual basics and the core components of an Agent Gateway deployment. See [Agent Gateway overview](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/gateways/agent-gateway-overview) .

## Required permissions

The following permissions are required to create and manage Agent Gateways. You can get these permissions either with [custom roles](https://docs.cloud.google.com/iam/docs/creating-custom-roles) or by using other [predefined roles](https://docs.cloud.google.com/iam/docs/roles-overview#predefined) .

#### Required permissions

  - `compute.networkAttachments.list`
  - `compute.regions.list`
  - `modelarmor.templates.list`
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

## Required APIs

Enable the following APIs in the Google Cloud project that you are using for this guide. These APIs let you access the full suite of capabilities offered by Gemini Enterprise Agent Platform.

#### Required APIs

  - Compute Engine API ( `compute.googleapis.com` )
  - Network Security API ( `networksecurity.googleapis.com` )
  - Network Services API ( `networkservices.googleapis.com` )
  - Cloud DNS API ( `dns.googleapis.com` )
  - Identity and Access Management API ( `iam.googleapis.com` )
  - Agent Registry API ( `agentregistry.googleapis.com` )
  - Vertex AI API ( `aiplatform.googleapis.com` )
  - Discovery Engine API ( `discoveryengine.googleapis.com` )
  - Cloud Storage API ( `storage.googleapis.com` )
  - Model Armor API ( `modelarmor.googleapis.com` )
  - Observability API ( `observability.googleapis.com` )
  - Telemetry API ( `telemetry.googleapis.com` )
  - Cloud Monitoring API ( `monitoring.googleapis.com` )
  - Cloud Trace API ( `cloudtrace.googleapis.com` )
  - Cloud Logging API ( `logging.googleapis.com` )
  - App Hub API ( `apphub.googleapis.com` )
  - App Topology API ( `apptopology.googleapis.com` )
  - Cloud API Registry ( `cloudapiregistry.googleapis.com` )
  - Notebooks API ( `notebooks.googleapis.com` )
  - Text-to-Speech API ( `texttospeech.googleapis.com` )
  - Dataform API ( `dataform.googleapis.com` )

## Configure Agent Gateway in Agent-to-Anywhere (Egress) mode

> **Note:** For an end-to-end codelab that explores how to govern communications initiated by an agent on Gemini Enterprise Agent Platform, see [Codelab: Govern agentic workloads with Agent Platform](https://codelabs.developers.google.com/cloudnet-agent-gateway) .

This section shows you how to set up an Agent Gateway for [Agent-to-Anywhere](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/gateways/agent-gateway-overview#modes) communications.

Note that a single Agent Gateway cannot simultaneously support both Gemini Enterprise and Agent Runtime integrations. Instead, you must deploy two mutually exclusive gateways: one configured with a global registry for Gemini Enterprise, and another with a regional registry for Agent Runtime.

Use the following steps to create an Agent Gateway resource.

### Google Cloud console

1.  In the Google Cloud console, go to the **Agent Gateway** page.

2.  Click **Add gateway** .

3.  Enter a **Name** .

4.  From the **Region** list, select a region.

5.  For **Deployment mode** , verify that **Google-managed** is selected.

6.  For **Agent Registry** , select a registry from the list. For Agent Runtime agents, select a regional registry ( ` //agentregistry.googleapis.com/projects/ PROJECT_ID /locations/ REGION  ` ). For Gemini Enterprise, select the project's global registry ( `//agentregistry.googleapis.com/projects/ PROJECT_ID /locations/global` ).

7.  From the **Governed Access Path** list, select **Agent-to-Anywhere (Agent Egress)** .

8.  In the **Access Authorization** section, choose how traffic is handled by IAP:
    
      - To deploy the gateway in a dry-run mode where the gateway permits all traffic through and only generates [audit logs](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/gateways/monitor-agent-gateway) , select **Audit-only** . Your IAM policies are not enforced by IAP in dry-run mode. Once you gain confidence, you can disable dry-run mode to enforce IAM policies.
      - To block requests that don't have an explicit `Allow` IAM policy, select **Enforce policies** . This option is recommended for production environments.

9.  Optional: In the **AI Security** section, configure additional security:
    
    1.  To protect AI model interactions with Model Armor, turn on **Enable Model Armor** .
    
    2.  Select a [template](https://docs.cloud.google.com/model-armor/manage-templates) that applies to incoming requests to the gateway from the list.
    
    3.  To use a different template for responses, clear **Use same template for requests and responses** and select a template from the list.
        
        > **Note:** If your Model Armor templates are in a different project from the gateway, you'll need to manually grant certain permissions to the Agent Gateway service account. For details, see [Delegate authorization to Model Armor](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/gateways/delegate-authorization#configure-authz-ma) .

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
          - AGENT_REGISTRY_PATH
    
    Replace the following:
    
      - `  AGENT_GATEWAY_NAME  ` : The name of the Agent Gateway resource.
      - `  AGENT_REGISTRY_PATH  ` : The path to the Agent Registry. For Agent Runtime agents, use a regional registry ( ` //agentregistry.googleapis.com/projects/ PROJECT_ID /locations/ REGION  ` ). For Gemini Enterprise, use the project's global registry ( `//agentregistry.googleapis.com/projects/ PROJECT_ID /locations/global` ).

2.  Run the following command to create an Agent Gateway resource based on the YAML specification:
    
        gcloud alpha network-services agent-gateways import AGENT_GATEWAY_NAME \
         --source="my-agent-gateway-egress.yaml" \
         --location=LOCATION
    
    Replace `  LOCATION  ` with the location where you want to create the Agent Gateway resource. For example, `us-central1` .
    
    Note that for Gemini Enterprise, you must deploy Agent Gateway in a region that corresponds to your multi-region setup. For the supported location mappings, see [Route Gemini Enterprise traffic through Agent Gateway](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/gateways/agent-gateway-ge-deploy#route-traffic) .

3.  Create an authorization policy to enforce centralized access control and governance policies on traffic passing through the Agent Gateway. The following steps show you how to configure an authorization policy that uses IAP.
    
    1.  Configure an authorization extension that points to IAP. Define the extension in a YAML file, such as `iap-request-authz-extension.yaml` .
        
        To validate the policy configuration and routing without disrupting traffic, we recommend that you first deploy the extension in dry-run (audit-only) mode. To do this, you specify `DRY_RUN` in the `iamEnforcementMode` field as shown in the example.
        
            cat >iap-request-authz-extension.yaml <<EOF
            name: AUTHORIZATION_EXTENSION_NAME
            service: iap.googleapis.com
            failOpen: true
            timeout: 1s
            metadata:
              iamEnforcementMode: "DRY_RUN"
              iapPolicyVersion: "V1"
            EOF
    
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
        
            gcloud beta network-security authz-policies import AUTHORIZATION_POLICY_NAME \
              --source=iap-request-authz-policy.yaml \
              --location=LOCATION

4.  Optional: If you want to configure Model Armor guardrails to help protect your deployment against prompt injection attacks and sensitive data leaks, see [Delegate authorization to Model Armor](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/gateways/delegate-authorization#model_armor) .

After an Agent Gateway has been created, it serves as the primary connection point for routing agent traffic within your project and chosen region. You can now use this endpoint to establish secure, encrypted, and authenticated communication channels between agents and their destinations (tools, other agents, or other endpoints).

Next, learn how to [deploy agents and route traffic through Agent Gateway](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/gateways/set-up-agent-gateway#route-traffic) .

### Optional: Configure VPC connectivity

To learn how to configure your Agent Gateway so that it can privately communicate with a VPC network in your organization, see [Set up VPC connectivity for Agent Gateway](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/gateways/set-up-vpc-connectivity) .

## Configure Agent Gateway in Client-to-Agent (Ingress) mode

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
    
        gcloud alpha network-services agent-gateways import AGENT_GATEWAY_NAME \
         --source="my-agent-gateway-ingress.yaml" \
         --location=LOCATION
    
    Replace `  LOCATION  ` with the location where you want to create the Agent Gateway resource. For example, `us-central1` .

After an Agent Gateway has been created, it serves as the primary connection point for routing traffic to agents in your project and chosen region.

Next, learn how to deploy agents and route traffic through Agent Gateway.

## Deploy agents and route traffic through Agent Gateway

To deploy a Agent Runtime agent that routes traffic through Agent Gateway, see [Route traffic through Agent Gateway](https://docs.cloud.google.com/gemini-enterprise-agent-platform/scale/runtime/agent-gateway-runtime-deploy) .

To deploy a Gemini Enterprise agent that routes traffic through Agent Gateway, see [Route Gemini Enterprise traffic through Agent Gateway](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/gateways/agent-gateway-ge-deploy) .

## What's next

Guide

### [Route agent traffic through Agent Gateway](https://docs.cloud.google.com/gemini-enterprise-agent-platform/scale/runtime/agent-gateway-runtime-deploy)

Learn how to route Agent Platform Runtime traffic through Agent Gateway for secure and governed connectivity.

Codelab

### [Codelab: Govern agentic workloads with Agent Platform](https://codelabs.developers.google.com/cloudnet-agent-gateway)

Learn how to govern agentic workloads with Agent Gateway on Gemini Enterprise Agent Platform.

Guide

### [Delegate authorization for Agent Gateway](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/gateways/delegate-authorization)

Learn how to delegate authorization for Agent Gateway to IAP, Model Armor, or your own custom authorization service.

Guide

### [Monitor Agent Gateway](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/gateways/monitor-agent-gateway)

Learn how to monitor Agent Gateway.

Guide

### [Route Gemini Enterprise traffic through Agent Gateway](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/gateways/agent-gateway-ge-deploy)

Learn how to route Gemini Enterprise traffic through Agent Gateway.
