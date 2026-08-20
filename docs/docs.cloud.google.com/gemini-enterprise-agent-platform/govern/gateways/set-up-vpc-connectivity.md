---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/govern/gateways/set-up-vpc-connectivity
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/gateways/set-up-vpc-connectivity
title: Set up VPC connectivity for Agent Gateway
description: Secure and govern AI agent connectivity with Agent Gateway. Centralize access policies, mTLS, and Model Context Protocol (MCP) security for agent-to-agent and agent-to-tool interactions across diverse runtimes.
data_source: docs.cloud.google.com
---

This document guides you through the process of updating your Agent Gateway so that it can privately communicate with a VPC network in your organization.

## Required roles and permissions

To configure VPC connectivity for Agent Gateway, ensure that the identity used for provisioning and the gateway service agent have the required roles.

In a standalone project where the gateway, network attachment, and VPC network reside in the same project, standard Agent Gateway permissions apply. For details, see [Required permissions](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/gateways/set-up-agent-gateway#required-roles) .

### Shared VPC or cross-project deployments

If you are using a [Shared VPC](https://docs.cloud.google.com/vpc/docs/shared-vpc) or cross-project setup where the target VPC network, network attachment, or private DNS zones reside in a central host project ( TARGET\_VPC\_PROJECT\_ID ), the following roles are required:

**Table:** Permissions needed for Shared VPC or cross-project deployments

Principal or identity

Grant on project

Required IAM role

Purpose

**Provisioning identity <sup>1</sup>**  
(User account or deployment service account)

Host project ( TARGET\_VPC\_PROJECT\_ID )

  - Compute Network Viewer ( `roles/compute.networkViewer` )
  - DNS Reader ( `roles/dns.reader` )

Allows backend validation of the target VPC network, subnets, network attachment, and private DNS zones during gateway creation or updates.

**Network attachment creator**  
(Administrator creating the PSC attachment)

Host project ( TARGET\_VPC\_PROJECT\_ID )

  - Compute Network User ( `roles/compute.networkUser` )

Allows using a Shared VPC subnet in the host project to create a Private Service Connect network attachment.

**Network attachment in the service project (Recommended)**

**Agent Gateway Service Agent <sup>2</sup>**

Host project ( TARGET\_VPC\_PROJECT\_ID )

  - Compute Network User ( `roles/compute.networkUser` )
  - DNS Peer ( `roles/dns.peer` )

Allows the Agent Gateway service agent to use the host project subnet for the network attachment, connect the Private Service Connect interface to route egress traffic, and peer with private Cloud DNS zones in the host project.

**Network attachment in the host project**

**Agent Gateway Service Agent <sup>2</sup>**

Host project ( TARGET\_VPC\_PROJECT\_ID )

  - Compute Network Admin ( `roles/compute.networkAdmin` ), or a custom role with:
      - `compute.networkAttachments.get`
      - `compute.networkAttachments.update`
      - `compute.regionOperations.get`
  - DNS Peer ( `roles/dns.peer` )

Allows the Agent Gateway service agent to update the host project network attachment to allow the connection from the Agent Gateway tenant project, to route egress traffic, and peer with private Cloud DNS zones in the host project.

<sup>1</sup> For the provisioning identity, basic project-level roles such as Viewer ( `roles/viewer` ) or Editor ( `roles/editor` ) on the host project are also sufficient.

<sup>2</sup> The Agent Gateway Service Agent is formatted as: `service- AGENT_GATEWAY_PROJECT_NUMBER @gcp-sa-agentgateway.iam.gserviceaccount.com` .

## Configure VPC connectivity

Perform the following steps:

1.  Create an Agent Gateway in `AGENT_TO_ANYWHERE` mode by following the instructions at [Configure Agent Gateway in Agent-to-Anywhere (Egress) mode](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/gateways/set-up-agent-gateway#config-agent-to-anywhere) .
    
    > **Note:** Network configuration ( `networkConfig` ) is only supported for Google-managed gateways ( `googleManaged` ) in `AGENT_TO_ANYWHERE` mode.

2.  Create a Private Service Connect network attachment in the VPC network that you want to connect to.
    
    Note the following requirements:
    
      - **Connection preference** : Configure the network attachment to [automatically accept connections](https://docs.cloud.google.com/vpc/docs/about-network-attachments#connection-policies) ( `--connection-preference=ACCEPT_AUTOMATIC` ).
    
      - **Same VPC network requirement** : The network attachment subnet and the target network configured for DNS peering ( `targetNetwork` ) *must be in the exact same VPC network* . If the network attachment's subnet belongs to a different network than the DNS peering target network, configuration validation fails.
    
      - **Network attachment immutability** : Once an Agent Gateway is configured with a network attachment, the `networkAttachment` field can't be modified on that gateway. To switch to a different network attachment, you must delete and recreate the Agent Gateway resource.
    
      - **Certificate requirement** : The endpoint that you connect to must support HTTPS with a publicly signed or trusted certificate. If Agent Gateway is unable to validate the certificate, the connection fails.
    
      - **Subnet requirements** : Note the following requirements for the network attachment subnet:
        
          - Agent Gateway requires a minimum `/28` subnet for the network attachment. A `/28` subnet provides 12 usable IP addresses, which is sufficient for a single Agent Gateway instance. If you plan to connect multiple gateways to the same network attachment or subnet, use a larger subnet (such as `/26` or `/24` ) to avoid IP address exhaustion.
        
          - The network attachment subnet supports all [valid ranges](https://docs.cloud.google.com/vpc/docs/subnets#valid-ranges) . However, Agent Gateway can only send traffic to the following subnet ranges:
            
              - RFC 1918: `10.0.0.0/8` , `172.16.0.0/12` , `192.168.0.0/16`
              - RFC 6598: `100.64.0.0/10`
              - Class E: `240.0.0.0/4`
              - `private.googleapis.com` : `199.36.153.8/30`
              - `restricted.googleapis.com` : `199.36.153.4/30`
              - **PSC endpoints for Google APIs** : If you deploy a custom Private Service Connect endpoint for Google APIs using an internal private IP address in your VPC network, traffic to this endpoint is routed through your VPC network. Ensure that Cloud DNS peering is configured in the connectivity template so that Agent Gateway correctly resolves Google API domains to your internal PSC endpoint IP address.
        
        Requests to standard public Google API endpoints are handled automatically using Private Google Access within the managed service environment. Internet-bound traffic isn't routed through your VPC network.
    
      - **Shared VPC setup requirements** :
        
        In a Shared VPC architecture, you can create the network attachment in either the service project (recommended) or the host project:
        
          - **Recommended: Network attachment in service project** :
            
            1.  [Create the subnet](https://docs.cloud.google.com/vpc/docs/create-modify-vpc-networks#add-subnets) in the host project.
            2.  [Create the network attachment](https://docs.cloud.google.com/vpc/docs/create-manage-network-attachments#create-network-attachments) in the service project, referencing the host project's subnet.
        
          - **Network attachment in host project** :
            
            1.  [Create the subnet](https://docs.cloud.google.com/vpc/docs/create-modify-vpc-networks#add-subnets) in the host project.
            2.  [Create the network attachment](https://docs.cloud.google.com/vpc/docs/create-manage-network-attachments#create-network-attachments) in the host project.
        
        Note the URI of the network attachment. You'll need it when you update the PSC\_NETWORK\_ATTACHMENT\_URI attribute of the connectivity template resource in a later step.

3.  Configure DNS peering for the service that you are connecting to. With DNS peering, your agents can connect to services in the target VPC network using stable, human-readable DNS names instead of IP addresses. DNS peering lets Agent Gateway resolve DNS names using the records from a Cloud DNS private zone in your VPC.
    
    1.  Set up your private DNS zone for DNS resolution and traffic routing. To add DNS records to your private DNS zone, see [Add a resource record set](https://docs.cloud.google.com/dns/docs/records#add-rrset) .
    
    2.  Gather the DNS information to enable peering:
        
          - **Domain name** : The domain name for DNS peering. Each domain must end with a trailing dot ( `.` ) (for example, `example.com.` or `corp.internal.` ).
          - **Specific domain suffixes only** : Specify only the specific domain suffixes that your agents need to reach in the target VPC network. Don't use root or catch-all wildcard domains (such as `.` ) or Google service domains (such as `googleapis.com.` ). Using these domains routes all gateway DNS traffic to your private VPC, which can cause unexpected issues.
          - **Exact match zones required** : The private Cloud DNS zones in the target VPC network must have exact match zones for the domain suffixes configured for peering.
          - **Target project ID** : The project ID of the host or target project.
          - **Target network URI** : The full resource URI of the VPC network in the target project. This **must be the same VPC network** that contains the network attachment.

4.  Update your Agent Gateway to include the network attachment and DNS peering information. For this example, we update the `my-agent-gateway-vpc-egress.yaml` YAML file as follows:
    
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
          targetProject: TARGET_VPC_PROJECT_ID
          targetNetwork: TARGET_VPC_NETWORK_URI
    ```
    
    Replace the following:
    
      - `  AGENT_GATEWAY_NAME  ` : The name of the Agent Gateway resource.
      - `  AGENT_REGISTRY_PATH  ` : The path to the Agent Registry. For Agent Runtime agents, use a regional registry ( ` //agentregistry.googleapis.com/projects/ PROJECT_ID /locations/ REGION  ` ). For Gemini Enterprise, use the global, multi-region, or regional registry that corresponds to your deployment (for example, `//agentregistry.googleapis.com/projects/ PROJECT_ID /locations/global` ).
      - `  PSC_NETWORK_ATTACHMENT_URI  ` : The PSC interface network attachment for connectivity to VPCs. If the network attachment is created in a project (such as the Shared VPC host project) different from where you deployed the agent, you need to pass the full path of your network attachment: ` projects/ TARGET_VPC_PROJECT_ID /regions/ REGION /networkAttachments/ ATTACHMENT_NAME  ` . Note: This field is immutable once configured.
      - `  DOMAIN_NAME  ` : A specific domain suffix for DNS peering (for example, `example.com.` or `corp.internal.` ). This value is required, must end with a trailing dot ( `.` ), and must have an exact match private Cloud DNS managed zone authorized for the target network. Don't use root or wildcard domains (such as `.` ) or Google service domains (such as `googleapis.com.` ).
      - `  TARGET_VPC_PROJECT_ID  ` : The target project for DNS peering (such as the Shared VPC host project).
      - `  TARGET_VPC_NETWORK_URI  ` : The target network where you created the network attachment. This must be of the form: ` projects/ TARGET_VPC_PROJECT_ID /global/networks/ NETWORK_NAME  ` . The project in this path must match `  TARGET_VPC_PROJECT_ID  ` , and the network must be the **exact same VPC network** where the network attachment is created.

5.  Run the following command to update the resource based on the YAML specification:
    
        gcloud network-services agent-gateways import AGENT_GATEWAY_NAME \
            --source="my-agent-gateway-vpc-egress.yaml" \
            --location=LOCATION
    
    Replace `  LOCATION  ` with the location where you want to create the Agent Gateway resource. For example, `europe-west1` .

## What's next

Guide

### [Route Agent Runtime traffic through Agent Gateway](https://docs.cloud.google.com/gemini-enterprise-agent-platform/scale/runtime/agent-gateway-runtime-deploy)

Learn how to route Agent Runtime traffic through Agent Gateway for secure and governed connectivity.

Codelab

### [Codelab: Govern agentic workloads with Agent Platform](https://codelabs.developers.google.com/cloudnet-agent-gateway)

Learn how to govern agentic workloads with Agent Gateway on Gemini Enterprise Agent Platform.

Codelab

### [Codelab: Agent Gateway egress from Agent Runtime to VPC networks](https://codelabs.developers.google.com/agw-cuj-arun-egress-vpc)

Learn about Agent Gateway egress governance for AI agents accessing destinations in a VPC network.

Guide

### [Delegate authorization for Agent Gateway](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/gateways/delegate-authorization)

Learn how to delegate authorization for Agent Gateway to IAP, Model Armor, or your own custom authorization service.

Guide

### [Monitor Agent Gateway](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/gateways/monitor-agent-gateway)

Learn how to monitor Agent Gateway.

Guide

### [Route Gemini Enterprise traffic through Agent Gateway](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/gateways/agent-gateway-ge-deploy)

Learn how to route Gemini Enterprise traffic through Agent Gateway.
