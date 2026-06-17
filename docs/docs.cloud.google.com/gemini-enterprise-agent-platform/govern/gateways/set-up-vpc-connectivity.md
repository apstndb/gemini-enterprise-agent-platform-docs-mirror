---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/govern/gateways/set-up-vpc-connectivity
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/gateways/set-up-vpc-connectivity
title: Set up VPC connectivity for Agent Gateway
description: Secure and govern AI agent connectivity with Agent Gateway. Centralize access policies, mTLS, and Model Context Protocol (MCP) security for agent-to-agent and agent-to-tool interactions across diverse runtimes.
data_source: docs.cloud.google.com
---

> **Private Preview — Agent Gateway**
> 
> This feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](https://cloud.google.com/terms/service-terms#1) . This feature provides capabilities to govern and secure AI Agents, so the "Agentic AI Services" Service Specific Terms apply. Pre-GA features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .
> 
> To request access to use Agent Gateway with Agent Runtime, see the [access request page](https://forms.gle/ZLNYKUDW7j2B4a8K7) .

This document guides you through the process of updating your Agent Gateway so that it can privately communicate with a VPC network in your organization.

Perform the following steps:

1.  Create an Agent Gateway in `AGENT_TO_ANYWHERE` mode by following the instructions at [Configure Agent Gateway in Agent-to-Anywhere (Egress) mode](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/gateways/set-up-agent-gateway#config-agent-to-anywhere) .

2.  Create a Private Service Connect network attachment in the VPC network that you want to connect to.
    
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

3.  Configure DNS peering for the service that you are connecting to. With DNS peering, your agents can connect to services in the target VPC network using stable, human-readable DNS names instead of IP addresses. DNS peering lets Agent Gateway resolve DNS names using the records from a Cloud DNS private zone in your VPC.
    
    1.  Set up your private DNS zone for DNS resolution and traffic routing. To add DNS records to your private DNS zone, see [Add a resource record set](https://docs.cloud.google.com/dns/docs/records#add-rrset) .
    
    2.  If you're using a Shared VPC setup and the target project and VPC network are in a different project than the gateway, assign the DNS `Peer(roles/dns.peer)` role to the Agent Gateway service account.
        
        Perform this step in the project where the Agent Gateway was created.
        
            gcloud alpha projects add-iam-policy-binding TARGET_PROJECT_ID \
             --member=serviceAccount:service-GATEWAY_PROJECT_NUMBER@gcp-sa-agentgateway.iam.gserviceaccount.com \
             --role=roles/dns.peer
    
    3.  Gather the DNS information to enable peering. This includes the domain name, the target project ID, and the name of the VPC network you want to connect to. You'll need this information when you update the Agent Gateway resource.

4.  Create an Agent Gateway that includes the network attachment and DNS peering information. Create the `my-agent-gateway-vpc-egress.yaml` YAML file as follows:
    
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

5.  Run the following command to update the resource based on the YAML specification:
    
        gcloud alpha network-services agent-gateways import AGENT_GATEWAY_NAME \
            --source="my-agent-gateway-vpc-egress.yaml" \
            --location=LOCATION
    
    Replace `  LOCATION  ` with the location where you want to create the Agent Gateway resource. For example, `us-central1` .

## What's next

Guide

### [Route Agent Runtime traffic through Agent Gateway](https://docs.cloud.google.com/gemini-enterprise-agent-platform/scale/runtime/agent-gateway-runtime-deploy)

Learn how to route Agent Runtime traffic through Agent Gateway for secure and governed connectivity.

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
