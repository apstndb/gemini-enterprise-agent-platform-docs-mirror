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

After an Agent Gateway has been created, it serves as the primary connection point for routing agent traffic within your project and chosen region. You can now use this endpoint to establish secure, encrypted, and authenticated communication channels between agents and their destinations (tools, other agents, or other endpoints).

Next, learn how to [deploy agents and route traffic through Agent Gateway](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/gateways/set-up-agent-gateway#route-traffic) .

### Configure VPC connectivity

To configure Agent Gateway for private outbound communication with a VPC network in your organization, you must perform the following additional steps:

1.  Create a Private Service Connect network attachment in the VPC network that you want to connect to.
    
    Note the following requirements:
    
      - Agent Gateway requires a minimum `/28` subnetwork for the network attachment.
    
      - Agent Gateway can only send to the following subnet ranges. Therefore, the subnet of the network attachment must fall within these ranges:
        
          - `10.0.0.0/8`
          - `172.16.0.0/12`
          - `192.168.0.0/16`
    
      - Agent Gateway *can't* send traffic to the following subnet ranges. Therefore, if you use the `10.0.0.0/8` range for the network attachment, you must ensure that it doesn't overlap with the following subnet ranges:
        
          - `10.0.0.0/24`
          - `10.0.1.0/24`
          - `10.0.2.0/24`
    
    For instructions, see [Create and manage Private Service Connect network attachments](https://docs.cloud.google.com/vpc/docs/create-manage-network-attachments) .
    
    If you have a Shared VPC setup, note the additional permissions required as documented in the [Using Private Service Connect interface with Shared VPC](https://docs.cloud.google.com/gemini-enterprise-agent-platform/scale/runtime/private-service-connect-interface#using-with-vpc-shared-vpc) section.
    
    Note the URI of the network attachment. You'll need it when you update the Agent Gateway resource.

2.  Configure DNS peering for the service that you are connecting to. With DNS peering, your agents can connect to services in the target VPC network using stable, human-readable DNS names instead of IP addresses. DNS peering lets Agent Gateway resolve DNS names using the records from a Cloud DNS private zone in your VPC.
    
    1.  Set up your private DNS zone for DNS resolution and traffic routing. To add DNS records to your private DNS zone, see [Add a resource record set](https://docs.cloud.google.com/dns/docs/records#add-rrset) .
    
    2.  If you're using a Shared VPC setup and the target project and VPC network are in a different project than the gateway, assign the DNS `Peer(roles/dns.peer)` role to the Agent Gateway service account.
        
        Perform this step in the project where the Agent Gateway was created.
        
            gcloud alpha projects add-iam-policy-binding TARGET_PROJECT_ID \
             --member=serviceAccount:service-GATEWAY_PROJECT_NUMBER@gcp-sa-agentgateway.iam.gserviceaccount.com \
             --role=roles/dns.peer
    
    3.  Gather the DNS information to enable peering. This includes the domain name, the target project ID, and the name of the VPC network you want to connect to. You'll need this information when you update the Agent Gateway resource.

3.  Update your Agent Gateway to include the network attachment and DNS peering information. Edit the `my-agent-gateway-egress.yaml` YAML file as follows:
    
    ``` 
      name: AGENT_GATEWAY_NAME
      protocols:
        - MCP
      googleManaged:
        governedAccessPath: AGENT_TO_ANYWHERE
      registries:
        - AGENT_REGISTRY_PATH
      networkConfig:
        egress:
          networkAttachment: PSC_NETWORK_ATTACHMENT_URI
        dnsPeeringConfig:
          domains:
            - DOMAIN_NAME
          targetProject: TARGET_PROJECT_ID
          targetNetwork: TARGET_NETWORK_URI
    ```
    
    Replace the following:
    
      - `  AGENT_GATEWAY_NAME  ` : The name of the Agent Gateway resource.
      - `  AGENT_REGISTRY_PATH  ` : The path to the Agent Registry. For Agent Runtime agents, use a regional registry ( ` //agentregistry.googleapis.com/projects/ PROJECT_ID /locations/ REGION  ` ). For Gemini Enterprise, use the project's global registry ( `//agentregistry.googleapis.com/projects/ PROJECT_ID /locations/global` ).
      - `  PSC_NETWORK_ATTACHMENT_URI  ` : The PSC interface network attachment for connectivity to VPCs. If the network attachment is created in a project (such as the Shared VPC host project) different from where you deployed the agent, you need to pass the full path of your network attachment.
      - `  DOMAIN_NAME  ` : A domain name for DNS peering. This value is required and must end with a dot ( `.` ).
      - `  TARGET_PROJECT_ID  ` : The target project for DNS peering.
      - `  TARGET_NETWORK_URI  ` : The target network where you created the network attachment. This must be of the form: ` projects/ TARGET_PROJECT_ID /global/networks/ NETWORK_NAME  ` .

4.  Run the following command to update the resource based on the YAML specification:
    
        gcloud alpha network-services agent-gateways import AGENT_GATEWAY_NAME \
            --source="my-agent-gateway.yaml" \
            --location=LOCATION
    
    Replace `  LOCATION  ` with the location where you want to create the Agent Gateway resource. For example, `us-central1` .

### Configure authorization policies

In Agent-to-Anywhere mode, you can use authorization policies to enforce centralized access control and governance policies on traffic passing through Agent Gateway.

You can either enable these policies while creating the gateway as shown in the previous section, or add them to a pre-deployed gateway as demonstrated in [Delegate authorization with Service Extensions](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/gateways/delegate-authorization) .

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
