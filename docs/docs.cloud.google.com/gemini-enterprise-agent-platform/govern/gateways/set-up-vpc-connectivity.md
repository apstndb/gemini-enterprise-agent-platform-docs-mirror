---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/govern/gateways/set-up-vpc-connectivity
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/gateways/set-up-vpc-connectivity
title: Set up VPC connectivity for Agent Gateway
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

When you deploy an Agent Gateway with a connectivity template, the gateway uses a Private Service Connect interface to route outbound agent traffic into your designated VPC network.

### VPC egress modes

You configure how the gateway routes traffic through your network attachment using the `vpcEgress` setting in your connectivity template.

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

### DNS resolution and traffic routing

By default, Agent Gateway resolves domain names using public recursive DNS. If your agents need to access internal workloads, private tools, or Google APIs hosted on private domain names in your VPC network (such as `corp.internal.` or PSC endpoints), you can configure Cloud DNS peering to forward DNS queries to your network's private Cloud DNS managed zones.

The following table summarizes Cloud DNS peering requirements and traffic routing behavior for different destinations when VPC connectivity is configured in `ALL_TRAFFIC` mode:

| Traffic destination                                            | Cloud DNS peering required?              | DNS resolution                                                                                                                                  | Egress path                                                                                                                                                                                                                                                 |
|----------------------------------------------------------------|------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Private IP services** (RFC 1918 / internal)                  | **Yes** (for example, `corp.internal.` ) | Resolves using Cloud DNS peering with your target VPC network's private Cloud DNS managed zone.                                                 | Traffic enters your VPC network through the network attachment to connect to internal workloads.                                                                                                                                                            |
| **Public hostnames with private IPs** (Split-horizon DNS)      | **No**                                   | Resolves using standard public recursive DNS at the gateway proxy without requiring Cloud DNS peering.                                          | Traffic enters your VPC network through the network attachment to connect to internal workloads.                                                                                                                                                            |
| **Public internet & SaaS APIs** (External domains)             | **No**                                   | Resolves using standard public recursive DNS at the gateway proxy without requiring Cloud DNS peering.                                          | Traffic enters your VPC network through the network attachment and exits to the public internet using Cloud NAT configured on the subnet.                                                                                                                   |
| **Google Cloud APIs** (standard, without VPC Service Controls) | **No**                                   | Resolves using standard public recursive DNS at the gateway proxy without requiring Cloud DNS peering.                                          | Traffic enters your VPC network through the network attachment and is routed privately using Private Google Access enabled on the subnet, without using Cloud NAT or DNS peering.                                                                           |
| **Google Cloud APIs** (with VPC Service Controls)              | **Yes** (for `googleapis.com.` )         | Resolves to the restricted Google API range ( `199.36.153.4/30` ) or internal Private Service Connect endpoints using a private Cloud DNS zone. | Traffic enters your VPC network through the network attachment to enforce VPC Service Controls perimeter security rules <sup>[1](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/gateways/set-up-vpc-connectivity#vpcsc-note)</sup> . |

**Table:** DNS resolution and traffic routing in `ALL_TRAFFIC` mode

<sup>1</sup> If requests fail with VPC Service Controls violations such as `NETWORK_NOT_IN_SAME_SERVICE_PERIMETER` or `SECURITY_POLICY_VIOLATED` on `compute.googleapis.com` or `dns.googleapis.com` that reference the host project, verify that the host project is in the same perimeter as the gateway project.

### TLS certificate requirements

When routing egress traffic over HTTPS, Agent Gateway validates the destination server's TLS certificate chain during the TLS handshake. Certificate requirements for HTTPS connections depend on whether your target endpoints use publicly trusted Certificate Authorities (CAs) or private/self-signed CAs.

- **Public CAs** : By default, Agent Gateway trusts certificates issued by [publicly trusted Certificate Authorities (CAs)](https://docs.cloud.google.com/load-balancing/docs/backend-authenticated-tls-backend-mtls#public-roots-of-trust) that meet standard [server certificate requirements](https://docs.cloud.google.com/load-balancing/docs/backend-authenticated-tls-backend-mtls#certificate-requirements) (including a Subject Alternative Name (SAN) matching the target hostname).

- **Private CAs and self-signed certificates** : If your target destination (agents, tools, or MCP servers in your VPC network) uses a private CA or internal PKI, you can configure custom trust anchors using the `tlsConfig` setting in your connectivity template. By referencing a Certificate Manager `TrustConfig` resource, you can configure Agent Gateway to trust only specific private CAs, or, combine private root CAs with publicly trusted CAs to establish trust for both public and private endpoints.

  When using `trustConfig` s to route traffic to destinations that use private CAs, you must rotate the PEM files manually. Automated rotation of PEM files using secret managers, such as [Google Cloud's Secret Manager](https://docs.cloud.google.com/secret-manager/docs/overview) , is not supported.

If Agent Gateway is unable to [validate the certificate chain](https://docs.cloud.google.com/load-balancing/docs/backend-authenticated-tls-backend-mtls#validation-steps) , the connection fails.

## Required roles and permissions

To configure VPC connectivity for Agent Gateway, ensure that the identity used for provisioning and the gateway service agent have the required roles.

### Standalone project deployments

In a standalone project where the gateway, network attachment, and VPC network reside in the same project, standard Agent Gateway permissions apply. For details, see [Required permissions](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/gateways/set-up-agent-gateway#required-roles) .

### Shared VPC or cross-project deployments

If you are using a [Shared VPC](https://docs.cloud.google.com/vpc/docs/shared-vpc) or cross-project setup where the target VPC network, network attachment, or private DNS zones reside in a central host project ( ` TARGET_VPC_PROJECT_ID ` ), the following roles are required in addition to [standard Agent Gateway permissions](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/gateways/set-up-agent-gateway#required-roles) :

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
<td>Host project ( <var translate="no"> TARGET_VPC_PROJECT_ID </var> )</td>
<td><ul>
<li>Compute Network Viewer ( <code>roles/ compute. networkViewer</code> )</li>
<li>DNS Reader ( <code>roles/ dns. reader</code> )</li>
<li>Network Connectivity Regional Endpoint Admin ( <code>roles/ networkconnectivity. regionalEndpointAdmin</code> )</li>
<li>Network Connectivity Consumer Network Admin ( <code>roles/ networkconnectivity. consumerNetworkAdmin</code> )</li>
</ul></td>
<td>Allows backend validation of the target VPC network, subnets, network attachment, and private DNS zones during gateway creation or updates.</td>
</tr>
<tr class="even">
<td><strong>Network attachment creator</strong><br />
(Administrator creating the PSC attachment)</td>
<td>Host project ( <var translate="no"> TARGET_VPC_PROJECT_ID </var> )</td>
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
<td>Host project ( <var translate="no"> TARGET_VPC_PROJECT_ID </var> )</td>
<td><ul>
<li>Compute Network User ( <code>roles/ compute. networkUser</code> )</li>
<li>DNS peer ( <code>roles/ dns. peer</code> )</li>
</ul></td>
<td>Allows the Agent Gateway service agent to use the host project subnet for the network attachment, connect the Private Service Connect interface to route egress traffic, and peer with private Cloud DNS zones in the host project.</td>
</tr>
<tr class="odd">
<td><strong>Network attachment in the host project</strong></td>
<td></td>
<td></td>
<td></td>
</tr>
<tr class="even">
<td><strong>Agent Gateway Service Agent <sup>2</sup></strong></td>
<td>Host project ( <var translate="no"> TARGET_VPC_PROJECT_ID </var> )</td>
<td><ul>
<li>Compute Network Admin ( <code>roles/ compute. networkAdmin</code> ), or a custom role with:
<ul>
<li><code>compute. networkAttachments. get</code></li>
<li><code>compute. networkAttachments. update</code></li>
<li><code>compute. regionOperations. get</code></li>
</ul></li>
<li>DNS peer ( <code>roles/ dns. peer</code> )</li>
</ul></td>
<td>Allows the Agent Gateway service agent to update the host project network attachment to allow the connection from the Agent Gateway tenant project, to route egress traffic, and peer with private Cloud DNS zones in the host project.</td>
</tr>
</tbody>
</table>

**Table:** Permissions needed for Shared VPC and cross-project deployments

<sup>1</sup> For the provisioning identity, basic project-level roles such as Viewer ( `roles/viewer` ) or Editor ( `roles/editor` ) on the host project are also sufficient.

<sup>2</sup> The Agent Gateway Service Agent is formatted as: `service- `` AGENT_GATEWAY_PROJECT_NUMBER `` @gcp-sa-agentgateway.iam.gserviceaccount.com` .

## Configure VPC connectivity

> **Important:** If you have an existing Agent Gateway that was created without an Agent Gateway connectivity template, you must delete the gateway and recreate it with a new connectivity template.

To deploy an Agent Gateway with a connectivity template, perform the following steps:

1.  **Create a Private Service Connect network attachment** in your target VPC network.

    Ensure that your network attachment meets the following requirements:

    - **Connection preference** : Configure the network attachment to [automatically accept connections](https://docs.cloud.google.com/vpc/docs/about-network-attachments#connection-policies) ( `--connection-preference=ACCEPT_AUTOMATIC` ) .
    - **Same VPC network requirement** : The network attachment subnet and the target network configured for DNS peering ( `targetNetwork` ) *must be in the exact same VPC network* . If the network attachment's subnet belongs to a different network than the DNS peering target network, configuration validation fails.
    - **Subnet requirements** : Note the following requirements for the network attachment subnet:
      - **Subnet range** : The network attachment subnet supports all [valid ranges](https://docs.cloud.google.com/vpc/docs/subnets#valid-ranges) .
      - **Subnet size** : Agent Gateway requires a minimum `/28` subnet for the network attachment. A `/28` subnet provides 12 usable IP addresses, which is sufficient for a single Agent Gateway instance. If you plan to connect multiple gateways to the same network attachment or subnet, use a larger subnet (such as `/26` or `/24` ) to avoid IP address exhaustion.
      - **Private Google Access requirement** : You must enable [Private Google Access](https://docs.cloud.google.com/vpc/docs/configure-private-google-access) ( `private_ip_google_access = true` ) on the subnet hosting the network attachment.
    - **Shared VPC deployments** : For Shared VPC deployments, see [Shared VPC deployment topologies](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/gateways/set-up-vpc-connectivity#shared-vpc-topologies) .

    Note the URI of the network attachment. You'll need it when you update the ` PSC_NETWORK_ATTACHMENT_URI ` attribute of the connectivity template resource in a later step.

2.  **Set up DNS peering (Optional)** : DNS peering lets Agent Gateway resolve DNS names using records from a Cloud DNS private managed zone in your VPC network. DNS peering is required only when your agents need to resolve private internal domain names (such as `corp.internal.` ) or enforce VPC Service Controls for Google APIs ( `googleapis.com.` ). It is not required for public internet domains or standard Google APIs without VPC Service Controls.

    Agent Gateway supports [transitive DNS peering](https://docs.cloud.google.com/dns/docs/zones/zones-overview#dns_peering_limitations_and_key_points) only up to a single transitive hop, which means a maximum of three VPC networks. For example, `vpc-net-a` (the Agent Gateway tenant network) can peer to `vpc-net-b` (attached network), which in turn peers to `vpc-net-c` (remote network) to resolve DNS queries across the chain.

    To set up DNS peering, perform the following steps:

    1.  [Set up your private DNS zone](https://docs.cloud.google.com/dns/docs/zones/zones-overview) in your target VPC network. To add DNS records to your private DNS zone, see [Add a resource record set](https://docs.cloud.google.com/dns/docs/records#add-rrset) .

    2.  Gather the following information to configure the connectivity template to enable peering:

        - **Target network URI ( `targetNetwork` )** : The full resource URI of the target VPC network. This **must be the same VPC network** that contains the network attachment.

        - **Domain names** : One or more domain suffixes for DNS peering. Each domain must end with a trailing dot ( `.` ) (for example, `corp.internal.` or `googleapis.com.` ).

          For additional guidance on how to configure the `domains` field, see [DNS peering domain patterns](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/gateways/set-up-vpc-connectivity#dns-peering-domain-patterns) . For cross-project deployments such as Shared VPC, see [Cross-project DNS zone and peering requirements](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/gateways/set-up-vpc-connectivity#dns-zone-type) .

3.  **Set up TLS trust configuration (only for destinations with private CAs and self-signed certificates)** :

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

4.  **Deploy the Agent Gateway**

    1.  **Create the connectivity template configuration file** :

        Create a YAML file named `agw-connectivity-template.yaml` :

        ```
        name: projects/AGENT_GATEWAY_PROJECT_NUMBER/locations/LOCATION/agentConnectivityTemplates/CONNECTIVITY_TEMPLATE_NAME
        accessPath: AGENT_TO_ANYWHERE
        deploymentModel: CENTRALIZED
        egressNetworkConfig:
          networkAttachment: PSC_NETWORK_ATTACHMENT_URI
          dnsPeeringConfig:
            domains:
              - DOMAIN_NAME
            targetNetwork: TARGET_VPC_NETWORK_URI
          vpcEgress: VPC_EGRESS_MODE
          tlsConfig:
            trustConfig: projects/AGENT_GATEWAY_PROJECT_NUMBER/locations/LOCATION/trustConfigs/TRUST_CONFIG_NAME
            additionalRoots: ADDITIONAL_ROOTS_OPTION
        ```

        Replace the following:

        - `AGENT_GATEWAY_PROJECT_NUMBER` : The numeric project number of the Google Cloud project where the gateway is deployed. To retrieve your project number, run: `gcloud projects describe `` PROJECT_ID `` --format="value(projectNumber)"` .

        - `LOCATION` : The region for the connectivity template (for example, `europe-west1` ).

        - `CONNECTIVITY_TEMPLATE_NAME` : The name of the connectivity template resource.

        - `accessPath` : The [governed access path](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/gateways/set-up-agent-gateway#choose-mode) for the connectivity template. Set to `AGENT_TO_ANYWHERE` (connectivity templates are supported only for egress gateways).

        - `deploymentModel` : The deployment model for the gateway. Set to `CENTRALIZED` .

        - `PSC_NETWORK_ATTACHMENT_URI` : The PSC interface network attachment for connectivity to VPCs. If the network attachment is created in a project different from where you deployed the gateway (such as the Shared VPC host project), pass the full path of your network attachment: `projects/ `` TARGET_VPC_PROJECT_ID `` /regions/ `` REGION `` /networkAttachments/ `` ATTACHMENT_NAME` .

          > **Note:** This field is immutable once configured on both the connectivity template and the Agent Gateway. You can't change the network attachment of an existing gateway by switching to a different connectivity template.

        - `DOMAIN_NAME` : (Optional) One or more domain suffixes for DNS peering (for example, `corp.internal.` , `googleapis.com.` , or `.` ). Add a list item under `domains` for each domain suffix that you want to peer. Each value must end with a trailing dot ( `.` ) and have a corresponding private Cloud DNS managed zone authorized for the target network.

          For additional guidance on how to configure the `domains` field, see [DNS peering domain patterns](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/gateways/set-up-vpc-connectivity#dns-peering-domain-patterns) .

        - `TARGET_VPC_NETWORK_URI` : The target VPC network where you created the network attachment. This must be of the form: `projects/ `` TARGET_VPC_PROJECT_ID `` /global/networks/ `` TARGET_VPC_NETWORK_NAME` . Always specify `targetNetwork` using the project ID ( `TARGET_VPC_PROJECT_ID` ) rather than the project number.

        - `VPC_EGRESS_MODE` : Set the [egress routing mode](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/gateways/set-up-vpc-connectivity#how-it-works) . Set to either `PRIVATE_RANGES_ONLY` or `ALL_TRAFFIC` .

        - `tlsConfig` : (Optional) The TLS configuration for server certificate validation when connecting to private endpoints over HTTPS:

          - `TRUST_CONFIG_NAME` : The name of the Certificate Manager `TrustConfig` resource containing your private CA certificates or trust anchors.
          - `ADDITIONAL_ROOTS_OPTION` : Specifies whether to trust publicly trusted CA roots in addition to your custom trust config. Set to `PUBLICLY_TRUSTED_ROOTS` (default) to trust both, certificates validated by the `trustConfig` parameter, and all publicly trusted CAs. Set to `NO_ADDITIONAL_ROOTS` to trust only the certificates validated by the `trustConfig` parameter.

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

        - `AGENT_GATEWAY_PROJECT_NUMBER` : The numeric project number of the Google Cloud project where you created the gateway and connectivity template. To retrieve your project number, run: `gcloud projects describe `` PROJECT_ID `` --format="value(projectNumber)"` .

        - `LOCATION` : The location of the connectivity template (for example, `europe-west1` ).

        - `CONNECTIVITY_TEMPLATE_NAME` : The name of the connectivity template resource.

        - `AGENT_REGISTRY_PATH` : The path to the Agent Registry. You can configure up to two registries for an Agent Gateway. When configuring two registries, one must be a global registry and the other can be either a regional or multi-regional registry. The registry paths must be formatted as follows:

          - Regional registries: `//agentregistry.googleapis.com/projects/ `` PROJECT_ID `` /locations/ `` REGION`
          - Global registries: `//agentregistry.googleapis.com/projects/ `` PROJECT_ID `` /locations/global`
          - Multi-region registries: `//agentregistry.googleapis.com/projects/ `` PROJECT_ID `` /locations/ `` MULTI_REGION`

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

A connectivity template can't be modified while it is referenced by an Agent Gateway.

- To update mutable VPC egress settings (such as the DNS peering configuration, VPC egress mode, or TLS configuration), you need to create a new connectivity template that uses the *same* `networkAttachment` and update the Agent Gateway to reference the new template.

- The `networkAttachment` itself is immutable once configured on an Agent Gateway. To switch to a different network attachment (or target VPC network), you must create a new connectivity template and a new Agent Gateway.

### Shared VPC deployment topologies

In a [Shared VPC](https://docs.cloud.google.com/vpc/docs/shared-vpc) architecture, you can create the network attachment in either the service project (recommended) or the host project:

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

- For Shared VPC deployments, the host project that owns the network attachment's subnet and the `dnsPeeringConfig.targetNetwork` must be in the same service perimeter as the project where you deploy the Agent Gateway. This applies even when you create the network attachment in the service project, because the subnet and VPC network still belong to the host project. If your private DNS zones are hosted in a separate DNS project, include that project in the perimeter too.

### DNS peering domain patterns

This section describes domain resolution patterns and options for configuring the `domains` field in a connectivity template.

**Domain name configuration** : Configure the `domains` field in the connectivity template based on the following considerations:

- **Private internal domains** : To resolve private internal services hosted in your VPC network (for example, `service.corp.internal` ), specify your internal domain suffix (such as `corp.internal.` ). An exact-match private Cloud DNS managed zone for this domain must be authorized for the target VPC network.

- **Split-horizon DNS (Public domain with RFC 1918 IP)** : If you use a public DNS zone to host records pointing to internal private IPs (such as `mcp.example.com` resolving to an RFC 1918 address for Certificate Manager public certificates), the gateway resolves these records automatically using public recursive DNS without requiring DNS peering.

- **Google Cloud APIs with VPC Service Controls** : When `ALL_TRAFFIC` is configured to enforce VPC Service Controls, Google API requests must resolve to the `restricted.googleapis.com` IP range ( `199.36.153.4/30` ) or to internal PSC endpoints. Create a private Cloud DNS zone in your VPC network mapping `*.googleapis.com` to `restricted.googleapis.com` , and include `googleapis.com.` in the `domains` field of your connectivity template.

- **Multi-domain resolution patterns** : If your deployment requires resolving multiple private domain suffixes, choose one of the following patterns:

  - **Peer multiple individual domains** : Specify a list of domain suffixes in the `domains` field of `dnsPeeringConfig` (for example, `corp.internal.` , `prod.internal.` , and `googleapis.com.` ). Each domain in the list must end with a trailing dot ( `.` ) and have a corresponding private Cloud DNS managed zone authorized for the target VPC network.

  - **Consolidated parent suffix (Recommended)** : Consolidate internal services under a shared parent domain suffix (such as `*.internal.` or `*.corp.internal.` ) and include that parent domain in the `domains` list.

  - **Catch-all root peering with a Private Forwarding Zone** : Include `"."` in the `domains` field of the connectivity template, and configure a Cloud DNS **Private Forwarding Zone** for the root domain ( `.` ) in your VPC network pointing to an upstream recursive resolver (such as `8.8.8.8` or an internal enterprise resolver). More specific private zones in your VPC match first by longest suffix match, while unmatched public queries resolve through the upstream forwarder.

    > **Caution:** Avoid configuring an *authoritative* private zone for the root domain ( `.` ). An authoritative root zone only resolves records defined within it and returns `NXDOMAIN` for all other domains, which can prevent external SaaS endpoints and Google Cloud APIs from resolving.

### Cross-project DNS zone and peering requirements

The connectivity template's `dnsPeeringConfig` setting doesn't support direct cross-project Cloud DNS peering. When you import the connectivity template, validation fails if the `targetNetwork` is in a different project than the `networkAttachment` , or if you rely on cross-project DNS zone binding from a service or external project.

The managed zone for the domain must be created in the *host project* that owns `targetNetwork` . The managed zone can be any of the following zone types:

- **Authoritative private zone**
- **Forwarding zone**
- **Cloud DNS peering zone** : Must be associated with the host project VPC network and target a destination VPC network. The destination VPC must resolve the query directly using an authoritative private zone. Forwarding the query to another DNS peering zone (chaining) is unsupported and results in an `NXDOMAIN` error.

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
