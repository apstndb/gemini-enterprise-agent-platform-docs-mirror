---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/govern/gateways/set-up-vpc-connectivity
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/gateways/set-up-vpc-connectivity
title: Set up Agent Gateway with VPC connectivity
description: Secure and govern AI agent connectivity with Agent Gateway. Centralize access policies, mTLS, and Model Context Protocol (MCP) security for agent-to-agent and agent-to-tool interactions across diverse runtimes.
data_source: docs.cloud.google.com
---

This document guides you through the process of configuring VPC connectivity when deploying an Agent Gateway so that it can privately communicate with a VPC network in your organization.

Setting up VPC connectivity lets you do the following:

- **Enforce VPC egress for traffic** : Route traffic originating from your agents through your Private Service Connect network attachment into your VPC network using `PRIVATE_RANGES_ONLY` or `ALL_TRAFFIC` mode.
- **Static source IP address range** : Egress traffic uses the private IP address range of your Private Service Connect network attachment subnet as its source IP address. This static source IP range lets you configure firewall policies for your VPC network to govern traffic coming from the gateway.
- **Custom DNS resolution** : Resolve internal private domain names and external domain names directly from your agents using Cloud DNS peering.
- **Perimeter security** : Protect agent communications using VPC Service Controls service perimeters.
- **Private or self-signed certificate validation** : Connect to destinations that use private CAs or self-signed certificates.

To configure VPC connectivity, you create an *Agent Gateway connectivity template* ( `AgentConnectivityTemplate` ) where you define and manage egress networking settings for your Agent Gateway instances.

## How VPC connectivity works

Agent Gateway runs in a Google-managed environment. To let agents privately access internal resources such as databases, enterprise tools, or on-premises systems without exposing them to the public internet, you can establish private VPC connectivity.

To connect Agent Gateway to your VPC network, you create a Private Service Connect network attachment in a dedicated subnet within your network. You then define an Agent Gateway connectivity template ( `AgentConnectivityTemplate` ) that references this network attachment and apply the template to your gateway.

When you deploy an Agent Gateway instance with a connectivity template, Google provisions a Private Service Connect interface that connects the gateway to your network attachment. Outbound traffic from your agents flows through this interface into your VPC network, using source IP addresses allocated from your network attachment subnet. This configuration lets your existing VPC routing rules, firewall policies, Cloud NAT gateways, and VPC Service Controls service perimeters govern and secure all egress traffic from your agents.

### VPC egress modes

The `vpcEgress` setting in your connectivity template controls which outbound traffic from your agents routes through your network attachment into your VPC network, and which traffic exits directly through Google-managed network paths.

Depending on your organization's security posture and routing requirements, you can configure one of two egress modes:

- **Traffic to private IP address ranges ( `PRIVATE_RANGES_ONLY` )** : Routes traffic destined only for private IP address ranges into your VPC network. Outbound traffic is routed into your VPC network only if the destination IP address falls into one of the following ranges:

  - **RFC 1918** : `10.0.0.0/8` , `172.16.0.0/12` , `192.168.0.0/16`
  - **RFC 6598** : `100.64.0.0/10`
  - **Class E** : `240.0.0.0/4`
  - **`private.googleapis.com`** : `199.36.153.8/30`
  - **`restricted.googleapis.com`** : `199.36.153.4/30`
  - **PSC endpoints for Google APIs** : If you deploy a custom Private Service Connect endpoint for Google APIs using an internal private IP address in your VPC network, traffic to this endpoint is routed through your VPC network. Ensure that Cloud DNS peering is configured in the connectivity template so that Agent Gateway correctly resolves Google API domains to your internal PSC endpoint IP address.

  Requests to standard public Google APIs are handled automatically using Private Google Access, and internet-bound traffic is routed directly through Agent Gateway rather than through your VPC network.

- **Traffic to all IP address ranges ( `ALL_TRAFFIC` )** : Routes all outbound traffic originating from your agents through your VPC network, including public internet, external SaaS APIs, and non-RFC 1918 addresses.

  - **Routing and security** : Because this setting routes all outbound traffic into your VPC, you're responsible for managing its routing and security. Ensure that your VPC network has a default route ( `0.0.0.0/0` ) to forward this traffic to your outbound gateways or security appliances (such as next-hop firewalls or Cloud Interconnect interfaces).
  - **Public internet egress** : The Agent Gateway sends outbound traffic into your VPC network, where it exits to the public internet through a [Cloud NAT gateway](https://docs.cloud.google.com/nat/docs/overview) on the Private Service Connect network attachment subnet. If you assign [static external IP addresses](https://docs.cloud.google.com/nat/docs/ports-and-addresses#addresses) to the Cloud NAT gateway, remote services can allowlist your agents' egress traffic based on these source IP addresses.
  - **VPC Service Controls** : Egress mode must be set to `ALL_TRAFFIC` to support VPC Service Controls service perimeters.

### Private DNS resolution and traffic routing

By default, Agent Gateway resolves domain names using public recursive DNS. If your agents need to access internal workloads, private tools, or Google APIs hosted on private domain names in your VPC network (such as `corp.internal.` or PSC endpoints), you can configure Cloud DNS peering in your connectivity template.

When you configure Cloud DNS peering, DNS resolution and outbound packet routing operate independently:

- **DNS resolution path ( `dnsPeeringConfig.targetNetwork` )** : Agent Gateway uses Cloud DNS peering to forward DNS queries for your configured `domains` to your target VPC network ( `targetNetwork` ). Depending on your network architecture, you configure `targetNetwork` using one of two options relative to the network attachment subnet:

  - **Same VPC network** : The target network is the same VPC network that contains your network attachment subnet. Use this option for standalone (single-project) or Shared VPC deployments.

  - **Separate VPC network (such as a central DNS hub)** : The target network is in another project, such as a central DNS hub network (bypassing spoke Cloud DNS). Use this option in hub-and-spoke architectures where your organization centralizes DNS resolution in a dedicated hub project separate from the spoke network that hosts your network attachment.

  With either option, `targetNetwork` can resolve DNS queries in one of two ways:

  - **Direct resolution (one peering hop)** : `targetNetwork` answers queries using authoritative private zones, [cross-project bound zones](https://docs.cloud.google.com/dns/docs/zones/cross-project-binding) , or forwarding zones authorized for `targetNetwork` .
  - **Transitive Cloud DNS peering (two peering hops)** : `targetNetwork` matches a Cloud DNS peering zone that forwards queries to another VPC network. Because Agent Gateway supports [transitive DNS peering](https://docs.cloud.google.com/dns/docs/zones/zones-overview#dns_peering_limitations_and_key_points) up to a single transitive hop (a maximum of two Cloud DNS peering hops across three VPC networks), the peering connection from Agent Gateway to `targetNetwork` uses the first hop (hop 1), and the peering zone from `targetNetwork` to the destination network uses the second hop (hop 2). That destination network must answer queries using authoritative private zones or forwarding zones, and can't forward queries across a third peering hop.

- **Traffic egress path ( `networkAttachment` )** : Regardless of which network you specify in `targetNetwork` , outbound packets enter the VPC network of your Private Service Connect network attachment subnet. If your destination workloads reside in another network (for example, behind a central hub connected with VPC Network Peering and HA VPN or Cloud Interconnect with Cloud Router), ensure that IP routing and firewall rules allow traffic between the network attachment subnet and the resolved destination IP addresses.

The following table summarizes Cloud DNS peering requirements and traffic routing behavior for different destinations when VPC connectivity is configured in `ALL_TRAFFIC` mode:

| Traffic destination                                            | Cloud DNS peering required?              | DNS resolution                                                                                                                                  | Egress path                                                                                                                                                                                                                                                 |
|----------------------------------------------------------------|------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Private IP services** (RFC 1918 / internal)                  | **Yes** (for example, `corp.internal.` ) | Resolves using Cloud DNS peering with your target VPC network, either directly or across one transitive Cloud DNS peering hop.                  | Traffic enters the network attachment's VPC network and follows its routes to internal or peered workloads.                                                                                                                                                 |
| **Public hostnames with private IPs** (Split-horizon DNS)      | **No**                                   | Resolves using standard public recursive DNS at the gateway proxy without requiring Cloud DNS peering.                                          | Traffic enters your VPC network through the network attachment to connect to internal workloads.                                                                                                                                                            |
| **Public internet & SaaS APIs** (External domains)             | **No**                                   | Resolves using standard public recursive DNS at the gateway proxy without requiring Cloud DNS peering.                                          | Traffic enters your VPC network through the network attachment and exits to the public internet using Cloud NAT configured on the subnet.                                                                                                                   |
| **Google Cloud APIs** (standard, without VPC Service Controls) | **No**                                   | Resolves using standard public recursive DNS at the gateway proxy without requiring Cloud DNS peering.                                          | Traffic enters your VPC network through the network attachment and is routed privately using Private Google Access enabled on the subnet, without using Cloud NAT or DNS peering.                                                                           |
| **Google Cloud APIs** (with VPC Service Controls)              | **Yes** (for `googleapis.com.` )         | Resolves to the restricted Google API range ( `199.36.153.4/30` ) or internal Private Service Connect endpoints using a private Cloud DNS zone. | Traffic enters your VPC network through the network attachment to enforce VPC Service Controls perimeter security rules <sup>[1](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/gateways/set-up-vpc-connectivity#vpcsc-note)</sup> . |

**Table:** DNS resolution and traffic routing in `ALL_TRAFFIC` mode

<sup>1</sup> If requests fail with VPC Service Controls violations such as `NETWORK_NOT_IN_SAME_SERVICE_PERIMETER` or `SECURITY_POLICY_VIOLATED` on `compute.googleapis.com` or `dns.googleapis.com` that reference the host project, verify that the host project is in the same perimeter as the gateway project.

### TLS certificate requirements

When routing egress traffic over HTTPS, Agent Gateway validates the destination server's TLS certificate chain during the TLS handshake. Certificate requirements for HTTPS connections depend on whether your target endpoints use publicly trusted Certificate Authorities (CAs) or private/self-signed CAs.

- **Public CAs** : By default, Agent Gateway trusts certificates issued by [publicly trusted Certificate Authorities (CAs)](https://docs.cloud.google.com/load-balancing/docs/backend-authenticated-tls-backend-mtls#public-roots-of-trust) that meet standard [server certificate requirements](https://docs.cloud.google.com/load-balancing/docs/backend-authenticated-tls-backend-mtls#certificate-requirements) (including a Subject Alternative Name (SAN) matching the target hostname).

- **Private CAs and self-signed certificates** : If your target destination (agents, tools, or MCP servers in your VPC network) uses a private CA or internal PKI, you can configure custom trust anchors using the `tlsConfig` setting in your connectivity template.

  By referencing a Certificate Manager `TrustConfig` resource, you can configure Agent Gateway to trust only specific private CAs, or combine private root CAs with publicly trusted CAs ( `PUBLICLY_TRUSTED_ROOTS` ). This establishes trust for both public and private endpoints.

  If your agents connect to Google Cloud APIs ( `*.googleapis.com` ) or other public HTTPS endpoints, you must set `additionalRoots` to `PUBLICLY_TRUSTED_ROOTS` ; without this setting, Agent Gateway doesn't trust Google-signed certificates for `googleapis.com` .

  Note the following limitations when using `tlsConfig` :

  - When using `trustConfig` s to route traffic to destinations that use private CAs, you must rotate the PEM files manually. Automated rotation of PEM files using secret managers, such as [Google Cloud's Secret Manager](https://docs.cloud.google.com/secret-manager/docs/overview) , is not supported.
  - The `trustConfig` field is immutable once configured on a connectivity template, and Agent Gateway doesn't automatically pick up changes made to `tlsConfig` (such as updating `additionalRoots` ) on an attached connectivity template. For instructions on updating TLS settings, see [Updating VPC egress settings](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/gateways/set-up-vpc-connectivity#updating-egress-settings) .

If Agent Gateway is unable to [validate the certificate chain](https://docs.cloud.google.com/load-balancing/docs/backend-authenticated-tls-backend-mtls#validation-steps) , the connection fails.

## Required roles and permissions

To configure VPC connectivity for Agent Gateway, ensure that the identity used for provisioning and the gateway service agent have the required roles.

### Standalone project deployments

In a standalone project where the gateway, network attachment, and VPC network reside in the same project, standard Agent Gateway permissions apply. For details, see [Required permissions](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/gateways/set-up-agent-gateway#required-roles) .

If you configure a network attachment, the identity that creates or updates the gateway or agent connectivity template (your user account or deployment service account) must also hold the `compute.networkAttachments.use` permission on the network attachment, for example through the Compute Network Admin role ( `roles/compute.networkAdmin` ) on the project that contains the network attachment. Compute Network User isn't sufficient. Without this permission, the request fails with a `PERMISSION_DENIED` error that names the network attachment.

In addition, if you configure DNS peering, Agent Gateway validates the DNS peering configuration (and any network attachment and its subnetwork) by using the Agent Gateway service agent ( `service- `` AGENT_GATEWAY_PROJECT_NUMBER `` @gcp-sa-agentgateway.iam.gserviceaccount.com` ). Grant the service agent the following roles on your project:

- Compute Network Viewer ( `roles/compute.networkViewer` )
- DNS Reader ( `roles/dns.reader` )

These roles aren't granted automatically. Network attachments alone, without DNS peering, don't require them.

Without these roles, creating or updating a gateway or agent connectivity template that configures DNS peering fails validation with an `INVALID_ARGUMENT` error that names the service agent and the missing role.

### Shared VPC or cross-project deployments

In a [Shared VPC](https://docs.cloud.google.com/vpc/docs/shared-vpc) deployment, you can provision the Agent Gateway in either a service project or the host project. If you provision the gateway in the host project (where the Shared VPC network, subnet, and network attachment also reside), [standalone project permissions](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/gateways/set-up-vpc-connectivity#standalone-project-permissions) apply (unless `targetNetwork` resides in a separate DNS hub project).

If you provision the Agent Gateway in a service project while the Shared VPC network, subnet, network attachment, or private DNS zones reside in the host project ( `HOST_PROJECT_ID` ), or if `targetNetwork` resides in a separate central DNS hub project ( `DNS_HUB_PROJECT_ID` ), identities in the service project don't automatically have permissions to validate, attach to, or peer with networking and DNS resources in those projects. Grant the following roles in addition to [standard Agent Gateway permissions](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/gateways/set-up-agent-gateway#required-roles) :

<table>
<caption><strong>Table:</strong> Permissions needed for Shared VPC and cross-project deployments</caption>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Principal or identity</th>
<th>Grant on project</th>
<th>Required IAM role</th>
<th>Purpose</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><strong>Provisioning identity <sup>1</sup></strong><br />
(User account or deployment service account)</td>
<td>Host project ( <var translate="no">HOST_PROJECT_ID</var> )</td>
<td><ul>
<li>Compute Network Viewer ( <code>roles/ compute. networkViewer</code> )</li>
<li>DNS Reader ( <code>roles/ dns. reader</code> )</li>
<li>Network Connectivity Regional Endpoint Admin ( <code>roles/ networkconnectivity. regionalEndpointAdmin</code> )</li>
<li>Network Connectivity Consumer Network Admin ( <code>roles/ networkconnectivity. consumerNetworkAdmin</code> )</li>
<li>Compute Network Admin ( <code>roles/ compute. networkAdmin</code> ) on the project that contains the network attachment, for the <code>compute. networkAttachments. use</code> permission</li>
</ul></td>
<td>Lets the provisioning identity view the host project network and private DNS resources, for example in the Google Cloud console, manage the regional endpoint, and use the network attachment. The Agent Gateway service agent, not the provisioning identity, validates the target VPC network, subnets, network attachment, and private DNS zones during gateway creation or updates.</td>
</tr>
<tr class="even">
<td><strong>Network attachment creator</strong><br />
(Administrator creating the PSC attachment)</td>
<td>Host project ( <var translate="no">HOST_PROJECT_ID</var> )</td>
<td><ul>
<li>Compute Network User ( <code>roles/ compute. networkUser</code> )</li>
</ul></td>
<td>Allows using a Shared VPC subnet in the host project to create a Private Service Connect network attachment.</td>
</tr>
<tr class="odd">
<td><strong>Network attachment in the service project (Recommended)</strong></td>
<td></td>
<td></td>
<td></td>
</tr>
<tr class="even">
<td><strong>Agent Gateway Service Agent <sup>2</sup></strong></td>
<td>Host project ( <var translate="no">HOST_PROJECT_ID</var> )</td>
<td><ul>
<li>Compute Network User ( <code>roles/ compute. networkUser</code> )</li>
<li>Compute Network Viewer ( <code>roles/ compute. networkViewer</code> ), when using DNS peering</li>
<li>DNS Reader ( <code>roles/ dns. reader</code> ), when using DNS peering</li>
<li>DNS Peer ( <code>roles/ dns. peer</code> ), when using DNS peering</li>
</ul></td>
<td>Allows the Agent Gateway service agent to use the host project subnet for the network attachment, connect the Private Service Connect interface to route egress traffic, and peer with private Cloud DNS zones in the host project, and lets the service agent validate the target VPC network, subnets, and private DNS zones during gateway creation or updates.</td>
</tr>
<tr class="odd">
<td><strong>Agent Gateway Service Agent <sup>2</sup></strong></td>
<td>Service project ( <var translate="no">AGENT_GATEWAY_PROJECT_ID</var> )</td>
<td><ul>
<li>Compute Network Viewer ( <code>roles/ compute. networkViewer</code> )</li>
</ul></td>
<td>Lets the service agent read the network attachment, which resides in the service project, when it validates a DNS peering configuration during gateway creation or updates. The service agent's default role doesn't include <code>compute. networkAttachments. get</code> .</td>
</tr>
<tr class="even">
<td><strong>Network attachment in the host project</strong></td>
<td></td>
<td></td>
<td></td>
</tr>
<tr class="odd">
<td><strong>Agent Gateway Service Agent <sup>2</sup></strong></td>
<td>Host project ( <var translate="no">HOST_PROJECT_ID</var> )</td>
<td><ul>
<li>Compute Network Admin ( <code>roles/ compute. networkAdmin</code> ), or a custom role with:
<ul>
<li><code>compute. networkAttachments. get</code></li>
<li><code>compute. networkAttachments. update</code></li>
<li><code>compute. regionOperations. get</code></li>
<li><code>compute. networks. get</code> , when using DNS peering</li>
<li><code>compute. subnetworks. get</code> , when using DNS peering</li>
</ul></li>
<li>DNS Reader ( <code>roles/ dns. reader</code> ), when using DNS peering</li>
<li>DNS Peer ( <code>roles/ dns. peer</code> ), when using DNS peering</li>
</ul></td>
<td>Allows the Agent Gateway service agent to update the host project network attachment to allow the connection from the Agent Gateway tenant project, to route egress traffic, and peer with private Cloud DNS zones in the host project, and lets the service agent validate the target VPC network, subnets, network attachment, and private DNS zones during gateway creation or updates.</td>
</tr>
<tr class="even">
<td><strong>Cross-project DNS hub topology ( <code>targetNetwork</code> in a separate project)</strong></td>
<td></td>
<td></td>
<td></td>
</tr>
<tr class="odd">
<td><strong>Agent Gateway Service Agent <sup>2</sup></strong></td>
<td>DNS hub project ( <var translate="no">DNS_HUB_PROJECT_ID</var> )</td>
<td><ul>
<li>Compute Network Viewer ( <code>roles/ compute. networkViewer</code> )</li>
<li>DNS Reader ( <code>roles/ dns. reader</code> )</li>
<li>DNS Peer ( <code>roles/ dns. peer</code> )</li>
</ul></td>
<td>Lets the Agent Gateway service agent validate the hub VPC network and its private Cloud DNS zones (including peering hop distance), and peer with private Cloud DNS zones in the hub network. Grant these DNS roles on the hub project instead of the standalone or host project when <code>targetNetwork</code> is in a separate project. For setup steps, see <a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/gateways/set-up-vpc-connectivity#set-up-dns-peering">Set up DNS peering</a> .</td>
</tr>
</tbody>
</table>

**Table:** Permissions needed for Shared VPC and cross-project deployments

<sup>1</sup> For the provisioning identity, basic project-level roles such as Viewer ( `roles/viewer` ) or Editor ( `roles/editor` ) on the host project are also sufficient.

<sup>2</sup> The Agent Gateway Service Agent is formatted as: `service- `` AGENT_GATEWAY_PROJECT_NUMBER `` @gcp-sa-agentgateway.iam.gserviceaccount.com` , where `AGENT_GATEWAY_PROJECT_NUMBER` is the project number of the project where you provision the Agent Gateway. For Shared VPC deployments, this project can be either a service project or the host project.

If you connect multiple Agent Runtime service projects to an Agent Gateway host project, you must also grant cross-project access on the gateway project to each Agent Runtime service agent. For large-scale deployments, see [Scale Agent Runtime service projects with a Google group](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/gateways/set-up-vpc-connectivity#scale-runtime-service-projects) .

## Configure VPC connectivity

> **Important:** If you have an existing Agent Gateway that was created without an Agent Gateway connectivity template, you must delete the gateway and recreate it with a new connectivity template.

To deploy an Agent Gateway with a connectivity template, complete the steps in the following sections.

### Create a Private Service Connect network attachment

Create a Private Service Connect network attachment in your target VPC network.

Ensure that your network attachment meets the following requirements:

- **Connection preference** : Configure the network attachment to [automatically accept connections](https://docs.cloud.google.com/vpc/docs/about-network-attachments#connection-policies) ( `--connection-preference=ACCEPT_AUTOMATIC` ) .
- **VPC network MTU support** : Agent Gateway supports a [maximum transmission unit (MTU)](https://docs.cloud.google.com/vpc/docs/mtu) of up to 1,500 bytes for the VPC network that contains the network attachment's subnet. If that VPC network uses a larger MTU, such as jumbo frames, then [contact Cloud Customer Care](https://docs.cloud.google.com/support/docs/customer-care-procedures) to align the Agent Gateway producer service with your custom VPC MTU.
- **Subnet requirements** : Note the following requirements for the network attachment subnet:
  - **Subnet range** : The network attachment subnet supports all [valid ranges](https://docs.cloud.google.com/vpc/docs/subnets#valid-ranges) .
  - **Subnet size** : Agent Gateway requires a minimum `/28` subnet for the network attachment. A `/28` subnet provides 12 usable IP addresses, which is sufficient for a single Agent Gateway instance. If you plan to connect multiple gateways to the same network attachment or subnet, use a larger subnet (such as `/26` or `/24` ) to avoid IP address exhaustion.
  - **Private Google Access requirement** : You must enable [Private Google Access](https://docs.cloud.google.com/vpc/docs/configure-private-google-access) ( `private_ip_google_access = true` ) on the subnet hosting the network attachment.
- **Shared VPC deployments** : For Shared VPC deployments, see [Shared VPC deployment topologies](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/gateways/set-up-vpc-connectivity#shared-vpc-topologies) .

Note the complete resource URI of the network attachment (for example, `projects/ `` NETWORK_ATTACHMENT_PROJECT_NUMBER `` /regions/ `` NETWORK_ATTACHMENT_REGION `` /networkAttachments/ `` NETWORK_ATTACHMENT_NAME` ). You'll need it when you create the connectivity template resource in a later step.

### Optional: Set up DNS peering

Complete this section only if your agents need to resolve private internal domain names (such as `corp.internal.` ) or enforce VPC Service Controls for Google APIs ( `googleapis.com.` ). If you're configuring cross-project DNS peering, read [Private DNS resolution and traffic routing](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/gateways/set-up-vpc-connectivity#dns-resolution-traffic-routing) and grant the cross-project service agent roles in [Shared VPC or cross-project deployments](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/gateways/set-up-vpc-connectivity#shared-vpc-permissions) .

To set up DNS peering, perform the following steps:

1.  Choose your target VPC network ( `targetNetwork` ), which is either the VPC network that contains your network attachment subnet or a separate network such as a central DNS hub, and configure private Cloud DNS zones using one of the following options:

    - **Direct resolution on `targetNetwork` (one peering hop)** : Use this option when `targetNetwork` resolves queries directly in standalone, Shared VPC, or single-hub deployments. Authorize [private managed zones](https://docs.cloud.google.com/dns/docs/zones#create-private-zone) (and [add your DNS records](https://docs.cloud.google.com/dns/docs/records#add-rrset) ) or [forwarding zones](https://docs.cloud.google.com/dns/docs/zones/forwarding-zones) for `targetNetwork` , either in the same project as `targetNetwork` or in a separate DNS project using [cross-project binding](https://docs.cloud.google.com/dns/docs/zones/cross-project-binding) .

    - **Transitive peering from `targetNetwork` to another VPC network (two peering hops)** : Use this option when `targetNetwork` (your attached network or a central DNS hub network) forwards queries to a destination VPC network that hosts or forwards DNS records:

      1.  In the destination project, authorize [authoritative private zones](https://docs.cloud.google.com/dns/docs/zones#create-private-zone) (and [add your DNS records](https://docs.cloud.google.com/dns/docs/records#add-rrset) ) or [forwarding zones](https://docs.cloud.google.com/dns/docs/zones/forwarding-zones) for the destination VPC network.

      2.  In the `targetNetwork` project, verify that `targetNetwork` has no conflicting zone for the same DNS name, and then [create a peering zone](https://docs.cloud.google.com/dns/docs/zones/peering-zones) authorized for `targetNetwork` that targets the destination VPC network (for example, for a specific private domain suffix or the root `.` domain).

          > **Caution:** A root ( `.` ) peering zone affects *every* workload in `targetNetwork` , not only Agent Gateway. All DNS queries in `targetNetwork` , including Google Cloud API names ( `*.googleapis.com` ), resolve in the destination VPC network's DNS view. Make sure that the destination network can resolve public names, or scope both the peering zone and the connectivity template `domains` list to a specific private domain suffix instead of `.` .

2.  Gather the following information to configure the connectivity template in [Deploy the Agent Gateway](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/gateways/set-up-vpc-connectivity#deploy-agent-gateway) :

    - **Target network URI ( `targetNetwork` )** : Note the full resource URI of the target VPC network in the following format: `projects/ `` TARGET_VPC_PROJECT_ID `` /global/networks/ `` TARGET_VPC_NETWORK_NAME` . Depending on your deployment topology, `TARGET_VPC_PROJECT_ID` is one of the following project IDs:

      - `AGENT_GATEWAY_PROJECT_ID` for standalone deployments where `targetNetwork` is in the same project.
      - `HOST_PROJECT_ID` for Shared VPC deployments where `targetNetwork` is the host network.
      - `DNS_HUB_PROJECT_ID` when `targetNetwork` is in a separate central DNS hub project.

    - **Domain names ( `domains` )** : One or more domain suffixes ending with a trailing dot ( `.` ), such as `corp.internal.` , `googleapis.com.` , or `.` (when forwarding all queries to a root forwarding or root peering zone in `targetNetwork` ).

      For peering domain patterns and validation rules, see [DNS peering domain patterns](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/gateways/set-up-vpc-connectivity#dns-peering-domain-patterns) and [Cross-project DNS zone and peering requirements](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/gateways/set-up-vpc-connectivity#dns-zone-type) .

### Optional: Set up TLS trust configuration

If your target destination uses a private CA or self-signed certificate, you need to create a `TrustConfig` resource in Certificate Manager. The `TrustConfig` resource defines the trust anchors and certificates that Agent Gateway uses to validate TLS connections.

1.  Prepare your certificate files in PEM format:

    - **Trust store** : Root or intermediate CA certificates in PEM format. Agent Gateway trusts any server certificate whose chain of trust leads to one of these CA certificates. *The trust store must contain at least one root or intermediate CA certificate.*
    - **Allowlisted certificates (Optional)** : Server certificates in PEM format that you want to explicitly trust, such as a self-signed certificate.

2.  Run the following command to create the `TrustConfig` resource. The `TrustConfig` must be created in the same project and region as the Agent Gateway and the connectivity template.

    ```
    gcloud certificate-manager trust-configs create TRUST_CONFIG_NAME \
        --location=LOCATION \
        --trust-store="trust-anchors=ROOT_CERT_FILE" \
        --allowlisted-certificates=ALLOWLISTED_CERT_FILE
    ```

    Replace the following:

    - `TRUST_CONFIG_NAME` : A name for the `TrustConfig` resource.
    - `LOCATION` : The region for the trust config (for example, `europe-west1` ). This must be the same region as the Agent Gateway and the connectivity template.
    - `ROOT_CERT_FILE` : The path to your PEM-encoded root or intermediate CA certificate.
    - `ALLOWLISTED_CERT_FILE` : (Optional) The path to a PEM-encoded certificate that you want to explicitly trust. If you aren't using allowlisted certificates, omit this flag.

    For more information on managing trust configs, see [Create and manage trust configs](https://docs.cloud.google.com/certificate-manager/docs/trust-configs) .

### Deploy the Agent Gateway

Deploy the Agent Gateway with your VPC connectivity settings:

### Console

1.  In the Google Cloud console, go to the **Gateways** page.

2.  Click **Add gateway** .

3.  In the **Name** field, enter a name for the gateway.

4.  In the **Region** list, select a region.

5.  For **Deployment mode** , verify that **Google-managed** is selected.

6.  The **Agent registry** field is automatically populated with the URI of the regional registry that matches your Agent Gateway region.

7.  In the **Governed Access Path** list, select **Agent-to-Anywhere (egress)** .

8.  In the **Access Authorization** section, configure how traffic is handled by Identity-Aware Proxy (IAP):

    - To deploy the gateway in a dry-run mode where the gateway permits all traffic through and only generates [audit logs](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/gateways/monitor-agent-gateway) , select **Audit-only** .

    - To block requests that don't have an explicit `Allow` IAM policy, select **Enforce policies** . This option is recommended for production environments.

    - For **Policy model** , select **Unified Access Policy** .

9.  Optional: In the **AI Security** section, configure additional security:

    1.  To protect AI model interactions with Model Armor, click the **Enable Model Armor** toggle to the on position.
    2.  Select a [template](https://docs.cloud.google.com/model-armor/manage-templates) for incoming requests to the gateway.
    3.  To use a different template for responses, clear the **Use same template for requests and responses** checkbox, and then select a template from the list.

10. In the **Connectivity template** section, make the following changes:

    1.  To route outbound gateway traffic through a private VPC network, click the **Route egress traffic through a VPC network** toggle to the on position, and then do the following:

        1.  For **Network attachment** , enter the full URI of the network attachment you created in the target VPC network: `projects/ `` TARGET_VPC_PROJECT_ID `` /regions/ `` REGION `` /networkAttachments/ `` ATTACHMENT_NAME`

        2.  For **VPC egress** , select one of the following:

            - **Private ranges only** : Allow only private IP traffic.
            - **All traffic** : Allow both private and public IP traffic. This option is required for VPC Service Controls compliance.

    2.  Optional: To set up DNS peering, select the **Enable DNS peering** checkbox, and then do the following:

        1.  For **Domains** , enter one or more domain suffixes for DNS peering. Each domain must end with a trailing dot ( `.` ), for example, `corp.internal.` or `googleapis.com.` .
        2.  For **Target network** , enter the full URI of the target VPC network where you created the network attachment: `projects/ `` TARGET_VPC_PROJECT_ID `` /global/networks/ `` TARGET_VPC_NETWORK_NAME` .

    3.  Optional: To connect to destinations that use private CAs or self-signed certificates, click the **Use a custom TLS trust config** toggle to the on position, and then do the following:

        1.  In the **Trust config** field, enter the URI of the trust config that you created earlier, using the following format: `projects/ `` AGENT_GATEWAY_PROJECT_NUMBER `` /locations/ `` REGION `` /trustConfigs/ `` TRUST_CONFIG_NAME` .

        2.  For **Additional roots** , select one of the following:

            - **Publicly trusted roots** : Trust certificates validated by the **Trust config** setting and all publicly trusted CAs.
            - **No additional roots** : Trust only certificates validated by the **Trust config** setting.

11. Click **Add Gateway** .

### gcloud

1.  **Create the connectivity template configuration file** :

    Create a YAML file named `agw-connectivity-template.yaml` :

    ```
    name: projects/AGENT_GATEWAY_PROJECT_NUMBER/locations/LOCATION/agentConnectivityTemplates/CONNECTIVITY_TEMPLATE_NAME
    accessPath: AGENT_TO_ANYWHERE
    deploymentModel: CENTRALIZED
    egressNetworkConfig:
      networkAttachment: projects/NETWORK_ATTACHMENT_PROJECT_NUMBER/regions/NETWORK_ATTACHMENT_REGION/networkAttachments/NETWORK_ATTACHMENT_NAME
      dnsPeeringConfig:
        domains:
          - DOMAIN_NAME
        targetNetwork: projects/TARGET_VPC_PROJECT_ID/global/networks/TARGET_VPC_NETWORK_NAME
      vpcEgress: VPC_EGRESS_MODE
      tlsConfig:
        trustConfig: projects/AGENT_GATEWAY_PROJECT_NUMBER/locations/LOCATION/trustConfigs/TRUST_CONFIG_NAME
        additionalRoots: ADDITIONAL_ROOTS_OPTION
    ```

    Replace the following:

    - `AGENT_GATEWAY_PROJECT_NUMBER` : The project number of the Google Cloud project where you provision the Agent Gateway. To retrieve your project number, run: `gcloud projects describe `` PROJECT_ID `` --format="value(projectNumber)"` .

    - `LOCATION` : The region for the connectivity template (for example, `europe-west1` ).

    - `CONNECTIVITY_TEMPLATE_NAME` : The name of the connectivity template resource.

    - `accessPath` : The [governed access path](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/gateways/set-up-agent-gateway#choose-mode) for the connectivity template. Set to `AGENT_TO_ANYWHERE` (connectivity templates are supported only for egress gateways).

    - `deploymentModel` : The deployment model for the gateway. Set to `CENTRALIZED` .

    - `networkAttachment` : The full resource URI of the Private Service Connect network attachment:

      - `NETWORK_ATTACHMENT_PROJECT_NUMBER` : The project number of the project where you created the network attachment. This project might be the same as the Agent Gateway project, or a different project if you provision the Agent Gateway in a Shared VPC service project and create the network attachment in the Shared VPC host project.
      - `NETWORK_ATTACHMENT_REGION` : The region that contains the network attachment.
      - `NETWORK_ATTACHMENT_NAME` : The network attachment name.

      > **Note:** The `networkAttachment` field is immutable once configured on both the connectivity template and the Agent Gateway. You can't change the network attachment of an existing gateway by switching to a different connectivity template.

    - `DOMAIN_NAME` : (Optional) One or more domain suffixes for DNS peering (for example, `corp.internal.` , `googleapis.com.` , or `.` ). Add a list item under `domains` for each domain suffix that you want to peer. Each value must end with a trailing dot ( `.` ) and have a corresponding private Cloud DNS managed zone authorized for the target network.

      For additional guidance on how to configure the `domains` field, see [DNS peering domain patterns](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/gateways/set-up-vpc-connectivity#dns-peering-domain-patterns) .

    - `targetNetwork` : (Optional) The full resource URI of the target VPC network for DNS peering. Depending on your deployment topology, this is either the VPC network that contains the network attachment subnet, or a VPC network in a separate DNS hub project:

      - `TARGET_VPC_PROJECT_ID` : The project ID of the project that owns the target VPC network: `AGENT_GATEWAY_PROJECT_ID` for standalone deployments, `HOST_PROJECT_ID` for Shared VPC host networks, or `DNS_HUB_PROJECT_ID` for a separate DNS hub network. Always specify `targetNetwork` using the project ID rather than the project number.
      - `TARGET_VPC_NETWORK_NAME` : The name of the target VPC network.

    - `VPC_EGRESS_MODE` : Set the [egress routing mode](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/gateways/set-up-vpc-connectivity#how-it-works) . Set to either `PRIVATE_RANGES_ONLY` or `ALL_TRAFFIC` .

    - `tlsConfig` : (Optional) The TLS configuration for server certificate validation when connecting to private endpoints over HTTPS:

      - `TRUST_CONFIG_NAME` : The name of the Certificate Manager `TrustConfig` resource containing your private CA certificates or trust anchors.
      - `ADDITIONAL_ROOTS_OPTION` : Specifies whether to trust publicly trusted CA roots in addition to your custom trust config:
      - Set to `PUBLICLY_TRUSTED_ROOTS` (default) to trust both certificates validated by the `trustConfig` parameter and all publicly trusted CAs. You must set `additionalRoots` to `PUBLICLY_TRUSTED_ROOTS` if your agents also connect to Google Cloud APIs ( `*.googleapis.com` ) or other public HTTPS endpoints; without this setting, Agent Gateway won't trust Google-signed certificates for `googleapis.com` .
      - Set to `NO_ADDITIONAL_ROOTS` to trust only the certificates validated by the `trustConfig` parameter.

      > **Note:** The `trustConfig` field is immutable once configured on a connectivity template, and Agent Gateway doesn't automatically pick up in-place changes to `tlsConfig` (such as updating `additionalRoots` ) while the connectivity template is attached to a gateway. To update TLS settings, see [Updating VPC egress settings](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/gateways/set-up-vpc-connectivity#updating-egress-settings) .

2.  **Create the connectivity template** :

    Run the following command to create the connectivity template:

    ```
    gcloud network-services agent-connectivity-templates import CONNECTIVITY_TEMPLATE_NAME \
        --source="agw-connectivity-template.yaml" \
        --location=LOCATION
    ```

    Replace the following:

    - `CONNECTIVITY_TEMPLATE_NAME` : The name of the connectivity template resource.
    - `LOCATION` : The location where you want to create the connectivity template resource. For example, `europe-west1` .

3.  **Define the Agent Gateway resource** :

    Define a new Agent Gateway resource in `AGENT_TO_ANYWHERE` mode by creating a gateway YAML configuration file (for example, `my-agent-gateway-vpc-egress.yaml` ) that references the connectivity template:

    ```
    name: AGENT_GATEWAY_NAME
    protocols:
      - MCP
    googleManaged:
      governedAccessPath: AGENT_TO_ANYWHERE
    agentConnectivityTemplate: projects/AGENT_GATEWAY_PROJECT_NUMBER/locations/LOCATION/agentConnectivityTemplates/CONNECTIVITY_TEMPLATE_NAME
    registries:
      - AGENT_REGISTRY_PATH
    ```

    Replace the following:

    - `AGENT_GATEWAY_NAME` : The name of the Agent Gateway resource.

    - `AGENT_GATEWAY_PROJECT_NUMBER` : The project number of the Google Cloud project where you provision the Agent Gateway and connectivity template. For Shared VPC deployments, this project can be either a service project or the host project. To retrieve your project number, run: `gcloud projects describe `` PROJECT_ID `` --format="value(projectNumber)"` .

    - `LOCATION` : The location of the connectivity template (for example, `europe-west1` ).

    - `CONNECTIVITY_TEMPLATE_NAME` : The name of the connectivity template resource.

      - `AGENT_REGISTRY_PATH` : The path to the regional Agent Registry instance in the same project and region as the gateway, formatted as `//agentregistry.googleapis.com/projects/ `` PROJECT_ID `` /locations/ `` LOCATION` . For guidance, see [Plan your Agent Gateway deployment](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/gateways/set-up-agent-gateway#plan-agw) .

4.  **Import and deploy Agent Gateway** :

    Run the following command to create the Agent Gateway resource based on the YAML specification:

    ```
    gcloud network-services agent-gateways import AGENT_GATEWAY_NAME \
        --source="my-agent-gateway-vpc-egress.yaml" \
        --location=LOCATION
    ```

    Replace `LOCATION` with the location where you want to create the Agent Gateway resource. For example, `europe-west1` .

## Architecture and networking considerations

This section provides architectural guidance and advanced networking patterns for deploying Agent Gateway with VPC connectivity.

### Updating VPC egress settings

A connectivity template can't be modified in place while it is referenced by an Agent Gateway, and Agent Gateway doesn't automatically pick up changes made to an attached connectivity template:

- **Updating DNS peering, VPC egress mode, or TLS settings ( `tlsConfig` )** : On a connectivity template, the `tlsConfig.trustConfig` field is immutable once configured, and in-place updates to `tlsConfig` (such as adding or changing `additionalRoots` ) aren't picked up by an attached Agent Gateway. To update the DNS peering configuration (including switching `targetNetwork` to a different VPC network or project), VPC egress mode, or `tlsConfig` settings on an existing gateway, create a new connectivity template that references the *same* `networkAttachment` with the updated settings, and run `gcloud network-services agent-gateways import` to point the Agent Gateway at the new template. This update completes in place without recreating the gateway or redeploying connected agents.

- **Changing the network attachment** : The `networkAttachment` itself is immutable once configured on both the connectivity template and the Agent Gateway. To switch to a different network attachment, you must create a new connectivity template and a new Agent Gateway.

### Shared VPC deployment topologies

In a [Shared VPC](https://docs.cloud.google.com/vpc/docs/shared-vpc) architecture, you can provision the Agent Gateway in either a service project or the host project. When you provision the Agent Gateway in a service project, you can create the network attachment in either the service project (recommended) or the host project:

- **Recommended: Network attachment in service project** :
  1.  [Create the subnet](https://docs.cloud.google.com/vpc/docs/create-modify-vpc-networks#add-subnets) in the host project.
  2.  [Create the network attachment](https://docs.cloud.google.com/vpc/docs/create-manage-network-attachments#create-network-attachments) in the service project, referencing the host project's subnet.
- **Network attachment in host project** :
  1.  [Create the subnet](https://docs.cloud.google.com/vpc/docs/create-modify-vpc-networks#add-subnets) in the host project.
  2.  [Create the network attachment](https://docs.cloud.google.com/vpc/docs/create-manage-network-attachments#create-network-attachments) in the host project.

### VPC Service Controls compliance

To enforce VPC Service Controls perimeters for agent communications, ensure the following:

- Set `vpcEgress` to `ALL_TRAFFIC` in your connectivity template.

- Direct Google API requests to either the `restricted.googleapis.com` IP range ( `199.36.153.4/30` ) or to an internal Private Service Connect endpoint for Google APIs.

- Configure DNS resolution for `googleapis.com` . Create a private Cloud DNS zone in your VPC network mapping `*.googleapis.com` to `restricted.googleapis.com` , and include `googleapis.com.` in the `domains` field of your connectivity template.

  For more details about DNS configuration, see [Configure DNS for googleapis.com](https://docs.cloud.google.com/vpc/docs/configure-private-google-access#dns-config-google-apis) in the Private Google Access documentation.

- For Shared VPC and cross-project DNS hub-and-spoke deployments, every project in the egress and DNS resolution path, including the project that owns the network attachment's subnet, the project that owns the `targetNetwork` , and any separate project that hosts cross-project or peered private Cloud DNS zones, must be in the same service perimeter as the project where you deploy the Agent Gateway. This applies even when you create the network attachment in a Shared VPC service project, because the subnet and VPC network still belong to the host project.

### DNS peering domain patterns

This section describes domain resolution patterns and options for configuring the `domains` field in a connectivity template.

**Domain name configuration** : Configure the `domains` field in the connectivity template based on the following considerations:

- **Private internal domains** : To resolve private internal services hosted in your VPC network (for example, `service.corp.internal` ), specify your internal domain suffix (such as `corp.internal.` ). A matching private Cloud DNS managed zone (exact match or parent suffix) must be authorized for or reachable within one DNS peering hop from the target VPC network.

- **Split-horizon DNS (Public domain with RFC 1918 IP)** : If you use a public DNS zone to host records pointing to internal private IPs (such as `mcp.example.com` resolving to an RFC 1918 address for Certificate Manager public certificates), the gateway resolves these records automatically using public recursive DNS without requiring DNS peering.

- **Google Cloud APIs with VPC Service Controls** : When `ALL_TRAFFIC` is configured to enforce VPC Service Controls, Google API requests must resolve to the `restricted.googleapis.com` IP range ( `199.36.153.4/30` ) or to internal PSC endpoints. Create a private Cloud DNS zone in your VPC network mapping `*.googleapis.com` to `restricted.googleapis.com` , and include `googleapis.com.` in the `domains` field of your connectivity template.

- **Multi-domain resolution patterns** : If your deployment requires resolving multiple private domain suffixes, choose one of the following patterns:

  - **Peer multiple individual domains** : Specify a list of domain suffixes in the `domains` field of `dnsPeeringConfig` (for example, `corp.internal.` , `prod.internal.` , and `googleapis.com.` ). Each domain in the list must end with a trailing dot ( `.` ) and have a matching private Cloud DNS managed zone authorized for or peered with the target VPC network.

  - **Consolidated parent suffix (Recommended)** : Consolidate internal services under a shared parent domain suffix (such as `*.internal.` or `*.corp.internal.` ) and include that parent domain in the `domains` list.

  - **Catch-all root peering with a forwarding or peering zone** : Include `"."` in the `domains` field of the connectivity template, and configure one of the following root ( `.` ) zones in your target VPC network ( `targetNetwork` ):

    - A Cloud DNS **private forwarding zone** pointing to an upstream recursive resolver (such as `8.8.8.8` or an internal enterprise resolver), where more specific private zones in your target VPC network match first by longest suffix match.
    - A Cloud DNS **peering zone** in a central DNS hub network (see [Set up DNS peering](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/gateways/set-up-vpc-connectivity#set-up-dns-peering) ) targeting a third VPC network that resolves both internal private zones and public names.

    > **Caution:** Avoid configuring an *authoritative* private zone for the root domain ( `.` ). An authoritative root zone only resolves records defined within it and returns `NXDOMAIN` for all other domains, which can prevent external SaaS endpoints and Google Cloud APIs from resolving.

### Cross-project DNS zone and peering requirements

The connectivity template's `dnsPeeringConfig` setting supports cross-project DNS topologies across both VPC networks and Cloud DNS zone projects:

- **Cross-project `targetNetwork` (decoupled from `networkAttachment` )** : When `targetNetwork` resides in a different project from the Agent Gateway (such as a Shared VPC host project or central DNS hub project), Agent Gateway validates the target network and its zones using the Agent Gateway service agent. Grant the required service agent roles on the `targetNetwork` project as described in [Shared VPC or cross-project deployments](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/gateways/set-up-vpc-connectivity#shared-vpc-permissions) .

- **Cross-project DNS zone binding** : Private Cloud DNS managed zones authorized for `targetNetwork` can reside in the project that owns `targetNetwork` or in a separate DNS project using [cross-project binding](https://docs.cloud.google.com/dns/docs/zones/cross-project-binding) .

  When a private zone resides in a separate project that Agent Gateway doesn't inspect, such as a separate cross-project DNS binding project, or a second-hop peered project where the Agent Gateway service agent lacks the `roles/dns.reader` role, Agent Gateway skips zone verification and allows the configuration. Ensure that you correctly specify the suffixes in `domains` , because domain typos for zones in those projects aren't caught during template creation and fail with `NXDOMAIN` at runtime.

- **Supported zone types and two-hop peering limit** : Each domain configured in `domains` can resolve in `targetNetwork` through any of the following managed zone types:

  - **Authoritative private zone** : Resolves records defined directly in the zone.
  - **Forwarding zone** : Forwards queries to configured private forwarding targets or upstream resolvers.
  - **Cloud DNS peering zone (second peering hop)** : Cloud DNS follows at most [two peering hops](https://docs.cloud.google.com/dns/docs/zones/zones-overview#dns_peering_limitations_and_key_points) , and Agent Gateway's managed peering zone to `targetNetwork` uses the first hop. If `targetNetwork` matches a Cloud DNS peering zone (hop 2) targeting a third VPC network, that destination network must answer the query using an **authoritative private zone** or a **forwarding zone** . Forwarding the query through another peering zone to a fourth network (a third peering hop) or forming a peering cycle fails validation (or fails to resolve at runtime).

If your workload spoke network peers to a central DNS hub that in turn peers to a third project, point `targetNetwork` directly at the DNS hub network to stay within two peering hops. For setup steps, see [Set up DNS peering](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/gateways/set-up-vpc-connectivity#set-up-dns-peering) .

### Scale Agent Runtime service projects with a Google group

If you connect multiple Agent Runtime service projects to an Agent Gateway host project and grant cross-project access to each service agent individually, you must update the host project's IAM policy every time you add a project. In large-scale deployments, you might also reach [IAM policy limits](https://docs.cloud.google.com/iam/quotas#limits) as you add role bindings.

To avoid updating the host project's IAM policy for every new service project, you can instead manage access through a single Google security group:

1.  **Create a security group** : [Create a security group](https://docs.cloud.google.com/identity/docs/how-to/update-group-to-security-group) either [in the Google Admin console](https://knowledge.workspace.google.com/admin/groups/control-access-to-sensitive-data-with-security-groups) or by running the [`gcloud identity groups create`](https://docs.cloud.google.com/sdk/gcloud/reference/identity/groups/create) command.

    > **Note:** To add [service agents](https://docs.cloud.google.com/iam/docs/service-account-types#service-agents) to a Google group, you must turn on the [external members](https://support.google.com/a/answer/167097#zippy=%2Ccan-external-users-participate-in-groups) option for the group.

2.  **Grant the group access to the Agent Gateway host project** : Bind the group to the Network Services Viewer role ( `roles/networkservices.viewer` ) on `AGENT_GATEWAY_PROJECT_ID` :

    ```
    gcloud projects add-iam-policy-binding AGENT_GATEWAY_PROJECT_ID \
        --member="group:GROUP_EMAIL" \
        --role="roles/networkservices.viewer"
    ```

    Replace the following:

    - `AGENT_GATEWAY_PROJECT_ID` : The project ID of the Agent Gateway host project.
    - `GROUP_EMAIL` : The email address of your security group (for example, `agw-cross-project-runtime@example.com` ).

3.  **Add each service project's Agent Runtime service agent to the group** : For each Agent Runtime service project, add its service agent to the security group by running the [`gcloud identity groups memberships add`](https://docs.cloud.google.com/sdk/gcloud/reference/identity/groups/memberships/add) command as follows:

    ```
    gcloud identity groups memberships add \
        --group-email="GROUP_EMAIL" \
        --member-email="service-AGENT_RUNTIME_PROJECT_NUMBER@gcp-sa-aiplatform.iam.gserviceaccount.com"
    ```

    Replace `AGENT_RUNTIME_PROJECT_NUMBER` with the project number of the Agent Runtime service project.

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

### [Manage Agent Gateway](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/gateways/manage-agent-gateways)

Learn how to view, update, disassociate, and delete Agent Gateway resources.

Guide

### [Monitor Agent Gateway](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/gateways/monitor-agent-gateway)

Learn how to monitor Agent Gateway.

Guide

### [Route Gemini Enterprise traffic through Agent Gateway](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/gateways/agent-gateway-ge-deploy)

Learn how to route Gemini Enterprise traffic through Agent Gateway.
