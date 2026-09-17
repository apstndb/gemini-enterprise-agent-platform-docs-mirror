---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/govern/gateways/set-up-vpc-connectivity
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/gateways/set-up-vpc-connectivity
title: Set up VPC connectivity for Agent Gateway
description: Secure and govern AI agent connectivity with Agent Gateway. Centralize access policies, mTLS, and Model Context Protocol (MCP) security for agent-to-agent and agent-to-tool interactions across diverse runtimes.
data_source: docs.cloud.google.com
---

This document guides you through the process of configuring VPC connectivity when deploying an Agent Gateway so that it can privately communicate with a VPC network in your organization.

Setting up VPC connectivity lets you do the following:

  - **Enforce VPC egress for traffic** : You can configure how the gateway routes traffic through your Private Service Connect network attachment into your VPC network using the `vpcEgress` setting:
    
      - **Traffic to private IP address ranges** ( `PRIVATE_RANGES_ONLY` ): Routes traffic destined only for certain private IP address ranges into your VPC network. For the specific IP address ranges, see [Subnet requirements](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/gateways/set-up-vpc-connectivity#subnet-reqs) .
    
      - **Traffic to all IP address ranges** ( `ALL_TRAFFIC` ): Routes all outbound traffic originating from your agents through your VPC network, including traffic destined for public and non-RFC 1918 IP address ranges.
        
        Because this setting routes all outbound traffic into your VPC, you're responsible for managing its routing and security. Ensure that your VPC network has a default route ( `0.0.0.0/0` ) to forward this traffic to your outbound gateways or security appliances (such as next-hop firewalls or Cloud Interconnect interfaces).

  - **Static source IP address range for egress traffic** : When you enable VPC connectivity, egress traffic originating from Agent Gateway uses the private IP address range of the subnet assigned to your Private Service Connect interface network attachment as its source IP address. This static source IP range lets you configure firewall policies for your VPC network to govern traffic coming from the gateway. When `vpcEgress` is set to `ALL_TRAFFIC` , you can enable internet egress for traffic routed through your VPC by configuring [Cloud NAT](https://docs.cloud.google.com/nat/docs/overview) on the subnet assigned to your Private Service Connect network attachment.

  - **Custom DNS resolution** : You can resolve internal private domain names and external domain names directly from your agents. With Cloud DNS peering configured on your agent connectivity template, your agents can connect to services in the target VPC network using stable, human-readable internal DNS names instead of IP addresses. For public domain names and external SaaS endpoints, DNS queries resolve using standard recursive resolution without requiring DNS peering.

  - **Perimeter security and data exfiltration protection** : Enforce VPC Service Controls service perimeters for agent communications. To support VPC Service Controls, egress must be set to `ALL_TRAFFIC` in your agent connectivity template. When configured with `ALL_TRAFFIC` mode, all agent traffic is routed through your private VPC network attachment:
    
      - **Standard Google APIs (without VPC Service Controls)** : If you aren't enforcing a VPC Service Controls perimeter, Cloud DNS peering is not required for `googleapis.com.` . Google API requests resolve through public recursive DNS and are automatically routed privately using Private Google Access enabled on the network attachment subnet.
      - **With VPC Service Controls perimeters** : If enforcing a VPC Service Controls perimeter, requests to Google APIs must be directed to the `restricted.googleapis.com` IP range ( `199.36.153.4/30` ) or Private Service Connect endpoints in your VPC network using a private Cloud DNS zone and Cloud DNS peering for `googleapis.com.` .

To configure VPC connectivity from your Agent Gateway, you create a resource called an *agent connectivity template* ( `AgentConnectivityTemplate` ) where you define and manage egress networking settings for your Agent Gateway instances. For steps, see [Configure VPC connectivity](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/gateways/set-up-vpc-connectivity#configure-vpc-connectivity) .

## Required roles and permissions

To configure VPC connectivity for Agent Gateway, ensure that the identity used for provisioning and the gateway service agent have the required roles.

In a standalone project where the gateway, network attachment, and VPC network reside in the same project, standard Agent Gateway permissions apply. For details, see [Required permissions](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/gateways/set-up-agent-gateway#required-roles) .

### Shared VPC or cross-project deployments

If you are using a [Shared VPC](https://docs.cloud.google.com/vpc/docs/shared-vpc) or cross-project setup where the target VPC network, network attachment, or private DNS zones reside in a central host project ( TARGET\_VPC\_PROJECT\_ID ), the following roles are required:

**Table:** Permissions needed for Shared VPC and cross-project deployments

Principal or identity

Grant on project

Required IAM role

Purpose

**Provisioning identity <sup>1</sup>**  
(User account or deployment service account)

Host project ( TARGET\_VPC\_PROJECT\_ID )

  - Compute Network Viewer ( `roles/compute.networkViewer` )
  - DNS Reader ( `roles/dns.reader` )
  - Network Connectivity Regional Endpoint Admin ( `roles/networkconnectivity.regionalEndpointAdmin` )
  - Network Connectivity Consumer Network Admin ( `roles/networkconnectivity.consumerNetworkAdmin` )

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

> **Important:** If you have an existing Agent Gateway that was created without a connectivity template, you must delete the gateway and recreate it with a new connectivity template.

To deploy an Agent Gateway with an agent connectivity template, perform the following steps:

1.  Create a Private Service Connect network attachment in the VPC network that you want to connect to.
    
    Note the following requirements:
    
      - **Connection preference** : Configure the network attachment to [automatically accept connections](https://docs.cloud.google.com/vpc/docs/about-network-attachments#connection-policies) ( `--connection-preference=ACCEPT_AUTOMATIC` ).
    
      - **Same VPC network requirement** : The network attachment subnet and the target network configured for DNS peering ( `targetNetwork` ) *must be in the exact same VPC network* . If the network attachment's subnet belongs to a different network than the DNS peering target network, configuration validation fails.
    
      - **Certificate requirement** : The endpoint that you connect to must support HTTP or HTTPS with a publicly signed or trusted certificate. If Agent Gateway is unable to validate the certificate, the connection fails.
    
      - **Subnet requirements** : Note the following requirements for the network attachment subnet:
        
          - Agent Gateway requires a minimum `/28` subnet for the network attachment. A `/28` subnet provides 12 usable IP addresses, which is sufficient for a single Agent Gateway instance. If you plan to connect multiple gateways to the same network attachment or subnet, use a larger subnet (such as `/26` or `/24` ) to avoid IP address exhaustion.
        
          - **Private Google Access requirement** : You must enable [Private Google Access](https://docs.cloud.google.com/vpc/docs/configure-private-google-access) ( `private_ip_google_access = true` ) on the subnet hosting the network attachment. When `ALL_TRAFFIC` is enabled, Private Google Access ensures that outbound requests to Google APIs ( `*.googleapis.com` ) are routed privately within Google's network directly from your VPC network without requiring Cloud DNS peering or Cloud NAT.
        
          - The network attachment subnet supports all [valid ranges](https://docs.cloud.google.com/vpc/docs/subnets#valid-ranges) . Traffic routing behavior depends on the `vpcEgress` setting configured in your agent connectivity template:
            
              - `PRIVATE_RANGES_ONLY` (default): Agent Gateway routes traffic destined only for the following private IP address ranges through your VPC network:
                
                  - RFC 1918: `10.0.0.0/8` , `172.16.0.0/12` , `192.168.0.0/16`
                  - RFC 6598: `100.64.0.0/10`
                  - Class E: `240.0.0.0/4`
                  - `private.googleapis.com` : `199.36.153.8/30`
                  - `restricted.googleapis.com` : `199.36.153.4/30`
                  - **PSC endpoints for Google APIs** : If you deploy a custom Private Service Connect endpoint for Google APIs using an internal private IP address in your VPC network, traffic to this endpoint is routed through your VPC network. Ensure that Cloud DNS peering is configured in the connectivity template so that Agent Gateway correctly resolves Google API domains to your internal PSC endpoint IP address.
                
                Requests to standard public Google API endpoints are handled automatically using Private Google Access within the managed service environment. Internet-bound traffic isn't routed through your VPC network.
            
              - `ALL_TRAFFIC` : All outbound traffic originating from your agents is routed through the VPC network attachment, including public internet, external SaaS APIs, and non-RFC 1918 addresses. To support VPC Service Controls, egress must be set to `ALL_TRAFFIC` .
                
                In `ALL_TRAFFIC` mode:
                
                  - **Public internet and SaaS traffic** : Resolves using standard public recursive DNS without requiring Cloud DNS peering. Outbound traffic enters your VPC network and exits to the public internet using Cloud NAT configured on the network attachment subnet.
                  - **Internal private services** : Resolves private domain names (such as `corp.internal.` ) to RFC 1918 IP addresses using Cloud DNS peering with your private Cloud DNS managed zone.
                  - **Standard Google Cloud APIs (without VPC Service Controls)** : If you aren't using VPC Service Controls, Cloud DNS peering is not required for `googleapis.com.` . Requests to Google APIs resolve to default public VIPs and are routed privately through Private Google Access enabled on the network attachment subnet, bypassing Cloud NAT.
                  - **Google Cloud APIs (with VPC Service Controls)** : Directs requests to the `restricted.googleapis.com` range ( `199.36.153.4/30` ) or internal PSC endpoints in your VPC network. Configuring Cloud DNS peering for `googleapis.com.` ensures that your agents resolve Google APIs to the restricted VIP range, enforcing perimeter security.
            
            The following table summarizes how DNS resolution and traffic routing operate across different traffic destinations:
            
            <table>
            <colgroup>
            <col style="width: 25%" />
            <col style="width: 25%" />
            <col style="width: 25%" />
            <col style="width: 25%" />
            </colgroup>
            <thead>
            <tr class="header">
            <th>Traffic destination</th>
            <th>Cloud DNS peering required</th>
            <th>Resolution behavior</th>
            <th>Egress path ( <code dir="ltr" translate="no">ALL_TRAFFIC</code> )</th>
            </tr>
            </thead>
            <tbody>
            <tr class="odd">
            <td><strong>Private IP services</strong><br />
            (RFC 1918 / internal)</td>
            <td><strong>Yes</strong> (for example, <code dir="ltr" translate="no">domain: "corp.internal."</code> )</td>
            <td>Resolved by the target VPC network's private Cloud DNS zone.</td>
            <td>Enters VPC network through network attachment to internal workloads.</td>
            </tr>
            <tr class="even">
            <td><strong>Public hostnames with private IPs</strong><br />
            (Split-horizon DNS)</td>
            <td><strong>No</strong></td>
            <td>Resolved by public recursive DNS at the gateway proxy.</td>
            <td>Enters VPC network through network attachment to internal workloads.</td>
            </tr>
            <tr class="odd">
            <td><strong>Public internet &amp; SaaS APIs</strong><br />
            (External domains)</td>
            <td><strong>No</strong></td>
            <td>Resolved by public recursive DNS at the gateway proxy.</td>
            <td>Enters VPC network through network attachment and exits using Cloud NAT.</td>
            </tr>
            <tr class="even">
            <td><strong>Google Cloud APIs</strong><br />
            (standard, without VPC Service Controls)</td>
            <td><strong>No</strong></td>
            <td>Resolved by public recursive DNS at the gateway proxy.</td>
            <td>Enters VPC network through network attachment and routed privately using Private Google Access on the subnet.</td>
            </tr>
            <tr class="odd">
            <td><strong>Google Cloud APIs</strong><br />
            (with VPC Service Controls)</td>
            <td><strong>Yes</strong> (for <code dir="ltr" translate="no">googleapis.com.</code> )</td>
            <td>Resolved to the restricted range ( <code dir="ltr" translate="no">199.36.153.4/30</code> ) or PSC endpoint using a private zone.</td>
            <td>Enters VPC network through network attachment; VPC Service Controls perimeter enforced.</td>
            </tr>
            </tbody>
            </table>
    
      - **Shared VPC setup requirements** :
        
        In a Shared VPC architecture, you can create the network attachment in either the service project (recommended) or the host project:
        
          - **Recommended: Network attachment in service project** :
            
            1.  [Create the subnet](https://docs.cloud.google.com/vpc/docs/create-modify-vpc-networks#add-subnets) in the host project.
            2.  [Create the network attachment](https://docs.cloud.google.com/vpc/docs/create-manage-network-attachments#create-network-attachments) in the service project, referencing the host project's subnet.
        
          - **Network attachment in host project** :
            
            1.  [Create the subnet](https://docs.cloud.google.com/vpc/docs/create-modify-vpc-networks#add-subnets) in the host project.
            2.  [Create the network attachment](https://docs.cloud.google.com/vpc/docs/create-manage-network-attachments#create-network-attachments) in the host project.
        
        Note the URI of the network attachment. You'll need it when you update the PSC\_NETWORK\_ATTACHMENT\_URI attribute of the connectivity template resource in a later step.

2.  Configure DNS peering for the service that you are connecting to. With DNS peering, your agents can connect to services in the target VPC network using stable, human-readable DNS names instead of IP addresses. DNS peering lets Agent Gateway resolve DNS names using the records from a Cloud DNS private zone in your VPC.
    
    1.  Set up your private DNS zone for DNS resolution and traffic routing. To add DNS records to your private DNS zone, see [Add a resource record set](https://docs.cloud.google.com/dns/docs/records#add-rrset) .
    
    2.  Gather the following information to enable peering based on your traffic requirements:
        
          - **Target network URI** : The full resource URI of the VPC network. This **must be the same VPC network** that contains the network attachment.
        
          - **Domain name** : The domain name for DNS peering. Each domain must end with a trailing dot ( `.` ) (for example, `corp.internal.` or `googleapis.com.` ). Note the following requirements by traffic type:
            
              - **Private internal domains** : To resolve private internal services hosted in your VPC network (for example, `service.corp.internal` ), specify your internal domain suffix (such as `corp.internal.` ). An exact-match private Cloud DNS managed zone for this domain must be authorized for the target VPC network.
            
              - **Public internet and SaaS endpoints** : Do not configure DNS peering for public domain names. The gateway resolves public domains using standard recursive DNS without requiring DNS peering.
            
              - **Split-horizon DNS (Public domain with RFC 1918 IP)** : If you use a public DNS zone to host records pointing to internal private IPs (such as `mcp.example.com` resolving to an RFC 1918 address for Certificate Manager public certificates), the gateway resolves these records automatically using public recursive DNS without requiring DNS peering.
            
              - **Google Cloud APIs** :
                
                  - **Standard Google APIs (without VPC Service Controls)** : Don't configure DNS peering for `googleapis.com.` . When `ALL_TRAFFIC` is enabled, Google API requests resolve through public recursive DNS and are handled privately by Private Google Access enabled on the network attachment subnet.
                  - **With VPC Service Controls** : When `ALL_TRAFFIC` is configured to enforce VPC Service Controls, Google API requests must resolve to the `restricted.googleapis.com` IP range ( `199.36.153.4/30` ) or internal PSC endpoints. Create a private Cloud DNS zone in your VPC network mapping `*.googleapis.com` to `restricted.googleapis.com` , and specify `domain: "googleapis.com."` in your agent connectivity template.
            
              - **Multi-domain resolution patterns** : As the agent connectivity template supports a single domain, if your deployment requires resolving multiple private domain suffixes, choose one of the following patterns:
                
                  - **Consolidated parent suffix (Recommended)** : Consolidate internal services under a shared parent domain suffix (such as `*.internal.` or `*.corp.internal.` ) and peer that parent domain.
                
                  - **Catch-all root peering with a Private Forwarding Zone** : Set `domain: "."` in the connectivity template, and configure a Cloud DNS **Private Forwarding Zone** for the root domain ( `.` ) in your VPC network pointing to an upstream recursive resolver (such as `8.8.8.8` or an internal enterprise resolver). More specific private zones in your VPC match first by longest suffix match, while unmatched public queries resolve through the upstream forwarder.
                    
                    > **Caution:** Avoid configuring an *authoritative* private zone for the root domain ( `.` ). An authoritative root zone only resolves records defined within it and returns `NXDOMAIN` for all other domains, which can prevent external SaaS endpoints and Google Cloud APIs from resolving.

3.  Create a YAML configuration file named `agw-connectivity-template.yaml` to define the connectivity template:
    
        name: projects/AGENT_GATEWAY_PROJECT_NUMBER/locations/LOCATION/agentConnectivityTemplates/CONNECTIVITY_TEMPLATE_NAME
        accessPath: AGENT_TO_ANYWHERE
        deploymentModel: CENTRALIZED
        egressNetworkConfig:
          networkAttachment: PSC_NETWORK_ATTACHMENT_URI
          dnsPeeringConfig:
            domain: DOMAIN_NAME
            targetNetwork: TARGET_VPC_NETWORK_URI
          vpcEgress: VPC_EGRESS_MODE
    
    Replace the following:
    
      - `  AGENT_GATEWAY_PROJECT_NUMBER  ` : The numeric project number of the Google Cloud project where the gateway is deployed. To retrieve your project number, run: `gcloud projects describe PROJECT_ID --format="value(projectNumber)"` .
    
      - `  LOCATION  ` : The location for the agent connectivity template (for example, `europe-west1` ).
    
      - `  CONNECTIVITY_TEMPLATE_NAME  ` : The name of the agent connectivity template resource.
    
      - `deploymentModel` : The deployment model for the gateway. Set to `CENTRALIZED` .
    
      - `  PSC_NETWORK_ATTACHMENT_URI  ` : The PSC interface network attachment for connectivity to VPCs. If the network attachment is created in a project different from where you deployed the gateway (such as the Shared VPC host project), pass the full path of your network attachment: ` projects/ TARGET_VPC_PROJECT_ID /regions/ REGION /networkAttachments/ ATTACHMENT_NAME  ` .
        
        > **Note:** This field is immutable once configured.
    
      - `  DOMAIN_NAME  ` : (Optional) The domain suffix for DNS peering (for example, `corp.internal.` , `googleapis.com.` , or `.` ). This value must end with a trailing dot ( `.` ) and have a corresponding private Cloud DNS managed zone authorized for the target network:
        
          - For internal workloads, specify your private domain suffix (such as `corp.internal.` ).
          - For VPC Service Controls under `ALL_TRAFFIC` , specify `googleapis.com.` to resolve Google APIs to the restricted IP range ( `199.36.153.4/30` ). If you aren't using VPC Service Controls, don't configure DNS peering for `googleapis.com.` ; standard Google APIs are handled automatically by Private Google Access on the subnet.
          - For multi-domain resolution, you can specify `.` if you have configured a Cloud DNS Private Forwarding Zone for the root domain pointing to a recursive resolver. Don't use `.` with an authoritative private zone.
        
        > **Note:** Don't configure DNS peering for public internet or external SaaS domains.
    
      - `  TARGET_VPC_NETWORK_URI  ` : The target VPC network where you created the network attachment. This must be of the form: ` projects/ TARGET_VPC_PROJECT_ID /global/networks/ TARGET_VPC_NETWORK_NAME  ` . This network must be the *exact same VPC network* where the network attachment is created.
    
      - `  VPC_EGRESS_MODE  ` : The egress traffic routing setting. Set to `PRIVATE_RANGES_ONLY` (default) to route traffic destined for private IP ranges through your VPC network, or set to `ALL_TRAFFIC` to route all outbound agent traffic (including public internet addresses) through your VPC network. To support VPC Service Controls, egress must be set to `ALL_TRAFFIC` .

4.  Run the following command to create the agent connectivity template:
    
        gcloud network-services agent-connectivity-templates import CONNECTIVITY_TEMPLATE_NAME \
            --source="agw-connectivity-template.yaml" \
            --location=LOCATION
    
    Replace the following:
    
      - `  CONNECTIVITY_TEMPLATE_NAME  ` : The name of the agent connectivity template resource.
      - `  LOCATION  ` : The location where you want to create the agent connectivity template resource. For example, `europe-west1` .

5.  Define a new Agent Gateway resource by creating a gateway YAML configuration file (for example, `my-agent-gateway-vpc-egress.yaml` ) that references the connectivity template:
    
        name: AGENT_GATEWAY_NAME
        protocols:
          - MCP
        googleManaged:
          governedAccessPath: AGENT_TO_ANYWHERE
        agentConnectivityTemplate: projects/AGENT_GATEWAY_PROJECT_NUMBER/locations/LOCATION/agentConnectivityTemplates/CONNECTIVITY_TEMPLATE_NAME
        registries:
          - AGENT_REGISTRY_PATH
    
    Replace the following:
    
      - `  AGENT_GATEWAY_NAME  ` : The name of the Agent Gateway resource.
      - `  AGENT_GATEWAY_PROJECT_NUMBER  ` : The numeric project number of the Google Cloud project where you created the gateway and connectivity template. To retrieve your project number, run: `gcloud projects describe PROJECT_ID --format="value(projectNumber)"` .
      - `  LOCATION  ` : The location of the agent connectivity template (for example, `europe-west1` ).
      - `  CONNECTIVITY_TEMPLATE_NAME  ` : The name of the agent connectivity template resource.
      - `  AGENT_REGISTRY_PATH  ` : The path to the Agent Registry. For Agent Runtime agents, use a regional registry ( ` //agentregistry.googleapis.com/projects/ AGENT_GATEWAY_PROJECT_NUMBER /locations/ REGION  ` ). For Gemini Enterprise, use the global, multi-region, or regional registry that corresponds to your deployment (for example, `//agentregistry.googleapis.com/projects/ AGENT_GATEWAY_PROJECT_NUMBER /locations/global` ).

6.  Run the following command to create the Agent Gateway resource based on the YAML specification:
    
        gcloud network-services agent-gateways import AGENT_GATEWAY_NAME \
            --source="my-agent-gateway-vpc-egress.yaml" \
            --location=LOCATION
    
    Replace `  LOCATION  ` with the location where you want to create the Agent Gateway resource. For example, `europe-west1` .
    
    > **Important:** To make updates to any of your VPC egress settings (such as the network attachment, subnet, DNS peering configuration, or VPC egress mode), you must create a new connectivity template with the updated configuration and update the Agent Gateway to reference the new template.

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
