---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/scale/sandbox/configure-vpc-sc
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/scale/sandbox/configure-vpc-sc
title: Configure VPC Service Controls and Private Service Connect with sandboxes
description: Learn how to configure VPC Service Controls (VPC-SC) and Private Service Connect (PSC-E / PSC-I) for Gemini Enterprise Agent Platform sandboxes.
data_source: docs.cloud.google.com
---

Control an Agent Platform sandbox's private ingress and internet egress with [Private Service Connect](https://docs.cloud.google.com/vpc/docs/private-service-connect) (PSC-E / PSC-I). These controls make the sandbox compliant with [VPC Service Controls](https://docs.cloud.google.com/vpc-service-controls/docs/overview) inside a perimeter or without a perimeter.

> **Note:** For VPC Service Controls as it applies to the broader Agent Runtime and other Agent Platform services, see [VPC Service Controls with Agent Platform](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/vpc-service-controls) .

## Overview

[VPC Service Controls](https://docs.cloud.google.com/vpc-service-controls/docs/overview) lets you define a service perimeter that isolates Google Cloud resources to mitigate the risk of data exfiltration. The Gemini Enterprise Agent Platform sandbox gives your agents a secure, isolated compute environment to run untrusted code, drive a web browser (computer use), or execute a custom container image. The sandbox exposes an interactive data plane and makes outbound calls, so it is governed with two Private Service Connect controls: private ingress (PSC-E) and egress control (PSC-I).

When you run the sandbox inside a perimeter, the following stay protected within your boundary:

  - Data your agent reads or writes during a sandbox session (files on the sandbox disk, in-memory state).
  - Sandbox [snapshots](https://docs.cloud.google.com/gemini-enterprise-agent-platform/scale/sandbox/manage-snapshots) that capture disk and in-memory state and are stored automatically in a Cloud Storage bucket.
  - Requests and responses exchanged with the sandbox data plane (for example, computer-use commands and screenshots).
  - Custom container images pulled from Artifact Registry.
  - Calls the sandbox makes to Google APIs (for example, Cloud Storage or Agent Platform).

You can also set up ingress and egress control without a VPC Service Controls perimeter, since the PSC-E (private ingress) and PSC-I (egress) are what makes a sandbox VPC Service Controls-compliant. To set up ingress and egress without a VPC Service Controls perimeter, skip to [Control sandbox egress with a Private Service Connect interface (PSC-I)](https://docs.cloud.google.com/gemini-enterprise-agent-platform/scale/sandbox/configure-vpc-sc#control-egress) .

## Limitations and considerations

  - Private ingress can be enabled for exactly one consumer project, and it must be the same user project the sandbox runs in.
  - Only private resolution through DNS peering is supported; public DNS forwarding is disabled to prevent tunneling.
  - Request and response logging is not available for resources protected by VPC Service Controls.
  - Programmatic and console access from outside the perimeter is denied unless the caller is on an access level.

## Before you begin

  - Create or identify the VPC Service Controls [service perimeter](https://docs.cloud.google.com/vpc-service-controls/docs/create-service-perimeters) that contains your project. In order for the sandboxes to be secured by the VPC Service Controls perimeter, your Google Cloud project must be in the perimeter before you create the sandboxes.
  - Enable the Agent Platform API ( `aiplatform.googleapis.com` ) in your project.
  - Have a VPC network in the region where you run sandboxes.
  - Confirm you hold the required roles:
      - [Access Context Manager admin](https://docs.cloud.google.com/vpc-service-controls/docs/access-control#required_roles) role for the perimeter
      - Compute Network Admin ( `roles/compute.networkAdmin` ) in the project that owns the network attachment.

## Add Agent Platform to your service perimeter

Add the Agent Platform API to the list of restricted services in your VPC Service Controls perimeter. This protects Agent Platform (including the sandbox control plane) and blocks public internet access to the API unless the caller is on an [access level](https://docs.cloud.google.com/vpc-service-controls/docs/use-access-levels) .

1.  Open **VPC Service Controls** in the Google Cloud console and edit your perimeter.
2.  Under **Restricted services** , add **Vertex AI API** ( `aiplatform.googleapis.com` ).
3.  Ensure dependencies your sandbox uses are in the same perimeter—typically **Cloud Storage** ( `storage.googleapis.com` ) and **Artifact Registry** ( `artifactregistry.googleapis.com` , for custom container images). Snapshot storage is handled for you automatically.
4.  To restore access for trusted users outside the perimeter (for example, your corporate network), attach an access level to the perimeter.

## Optional: Configure private access to Google APIs

Inside the VPC Service Controls perimeter, the sandbox reaches Google APIs privately over the restricted virtual IP address (VIP). From your own VPC and on-premises networks, use the restricted VIP as well so requests never traverse the public internet.

  - Route `*.googleapis.com` to the restricted VIP `199.36.153.4/30` and enable [Private Google Access](https://docs.cloud.google.com/vpc/docs/private-google-access) on the subnets that call Google APIs.
  - Create Cloud DNS private zones for `googleapis.com` (and, if you pull images, `pkg.dev` / `gcr.io` ) that resolve to the restricted VIP.

> **Note:** If you use Private Service Connect for Google APIs, you can define a custom endpoint IP and DNS name. See [Configure Private Service Connect for Google APIs](https://docs.cloud.google.com/vpc/docs/configure-private-service-connect-apis) .

## Control sandbox egress with a Private Service Connect interface (PSC-I)

To let the sandbox reach the internet or private services, bridge its egress into your VPC with a Private Service Connect interface, then govern that traffic with your own egress controls.

Every resource in this step is created in the user project that owns the sandbox or in its Shared VPC host project. Egress is directed to the single VPC network and network attachment you set on the template.

### Create the network attachment

Create the network attachment for the sandbox:

    # A dedicated subnet for the PSC interface (minimum /28)
    gcloud compute networks subnets create sandbox-psc-subnet \
        --network=YOUR_VPC \
        --range=10.0.0.0/28 \
        --region=REGION
    
    # The network attachment the sandbox connects into
    gcloud compute networks network-attachments create sandbox-egress-na \
        --region=REGION \
        --connection-preference=ACCEPT_AUTOMATIC \
        --subnets=sandbox-psc-subnet

### Reference the attachment from the sandbox template

Set the egress fields on the `SandboxEnvironmentTemplate` so the sandbox routes egress through your VPC:

    from vertexai import Client
    
    client = Client(project="PROJECT_ID", location="REGION",
                    http_options={"api_version": "v1beta1"})
    
    templates = client.agent_engines.sandboxes.templates
    op = templates.create(
        name=agent_instance_name,
        display_name="cu-vpcsc-template",
        config={
            "custom_container_environment": {
                "custom_container_spec": {"image_uri": "IMAGE_URI"},
                "ports": [{"port": 8080, "protocol": "TCP"}],
            },
            "egress_control_config": {
                "internet_access": True, # Enables outbound access from the sandbox. With VPC-SC, that traffic is bridged into your VPC.
                "customer_vpc_network":
                    "projects/PROJECT_ID/global/networks/YOUR_VPC", # The VPC network in your project that egress is bridged into. Checked by VPC-SC at creation time.
                "network_attachment":
                    "projects/PROJECT_ID/regions/REGION/networkAttachments/sandbox-egress-na", # The network attachment that accepts the sandbox's PSC interface.
            },
        },
    )

The PSC interface builds the private path into your VPC, and the platform automatically steers the sandbox's egress onto it when `internet_access` is enabled.

To set up and govern the path out of your VPC, decide if you need internet or private-only egress:

  - [**Internet egress:**](https://docs.cloud.google.com/gemini-enterprise-agent-platform/scale/sandbox/configure-vpc-sc#set-up-internet-egress) For internet egress, Cloud NAT is required, plus destination control using Cloud Next Generation Firewall (Cloud NGFW) rules or Secure Web Proxy.
  - [**Private-only egress**](https://docs.cloud.google.com/gemini-enterprise-agent-platform/scale/sandbox/configure-vpc-sc#setup-private-egress) (reach services in your VPC or on-premises, no internet): Cloud NAT isn't required. You only need routes, a firewall rule, and DNS peering.

#### Set up for internet egress and govern destinations

The sandbox enters your VPC on an internal (RFC 1918) address, so it needs [Cloud NAT](https://docs.cloud.google.com/nat/docs/overview) to reach the internet. Reserve a static egress IP if your destinations allow-list by source IP.

    # Reserve a static egress IP (optional, for destination-side allow-listing)
    gcloud compute addresses create sandbox-egress-ip --region=REGION
    
    # Cloud Router + NAT for the region, scoped to the PSC subnet
    gcloud compute routers create sandbox-egress-router \
        --network=YOUR_VPC --region=REGION
    
    gcloud compute routers nats create sandbox-egress-nat \
        --router=sandbox-egress-router --region=REGION \
        --nat-external-ip-pool=sandbox-egress-ip \
        --nat-custom-subnet-ip-ranges=sandbox-psc-subnet

To restrict which destinations the sandbox may reach as its traffic transits your VPC, choose the level of control you need:

  - [**Cloud NGFW**](https://docs.cloud.google.com/firewall/docs/about-firewalls) (network-level): a global network firewall policy with allow rules (FQDN objects are supported) plus a default-deny for everything else:
    
        gcloud compute network-firewall-policies create sandbox-egress-policy --global
        
        # Allow only the destinations your agent needs (by FQDN)
        gcloud compute network-firewall-policies rules create 1000 \
            --firewall-policy=sandbox-egress-policy --global-firewall-policy \
            --direction=EGRESS --action=allow --layer4-configs=tcp:443 \
            --dest-fqdns=api.partner.example.com
        
        # Default-deny the rest of egress
        gcloud compute network-firewall-policies rules create 65000 \
            --firewall-policy=sandbox-egress-policy --global-firewall-policy \
            --direction=EGRESS --action=deny --layer4-configs=all \
            --dest-ip-ranges=0.0.0.0/0
        
        gcloud compute network-firewall-policies associations create \
            --firewall-policy=sandbox-egress-policy --global-firewall-policy \
            --network=YOUR_VPC

  - [**Secure Web Proxy**](https://docs.cloud.google.com/secure-web-proxy/docs/overview) (application/L7): deploy Secure Web Proxy as the egress inspection point in your VPC for TLS-aware, per-URL policy, and route the PSC subnet's egress through it.

#### Set up for private-only egress

If the sandbox only needs private services in your VPC or on-premises, make sure your VPC has a route to the destination, allow it with an egress firewall rule from the PSC subnet ( `10.0.0.0/28` ), and [resolve the service name through DNS peering](https://docs.cloud.google.com/dns/docs/zones/zones-overview#peering-zones) .

### Set up DNS peering

Give the sandbox name resolution through your VPC instead of public resolvers (this also blocks DNS-tunnel exfiltration). Create a Cloud DNS private zone in your VPC with the records the sandbox needs, then configure [DNS peering](https://docs.cloud.google.com/dns/docs/zones/zones-overview#peering-zones) so the sandbox resolves names from that zone.

### Grant the service agent access (Shared VPC)

If the network attachment lives in a different project (for example, a Shared VPC host project), grant the Agent Platform sandbox service agent permission to use it:

    # Sandbox service agent
    service-PROJECT_NUMBER@gcp-sa-vertex-sandbox.iam.gserviceaccount.com
    
    # On the project that owns the network attachment
    gcloud projects add-iam-policy-binding NETWORK_PROJECT_ID \
        --member="serviceAccount:service-PROJECT_NUMBER@gcp-sa-vertex-sandbox.iam.gserviceaccount.com" \
        --role="roles/compute.networkAdmin"

## Enable private ingress with Private Service Connect (PSC-E)

Interactive workloads expose a data plane that a client must connect to. Reach that data plane over a private Private Service Connect endpoint (PSC-E) in your VPC instead of over the public internet.

### Declare the allowed consumer project

Set the ingress configuration on the template with the consumer project allowed to connect. Only the same user project that the sandbox runs in can have private ingress to the sandbox VPC.

Connect to the sandbox from a VPC in that same project:

    config = {
        # ...custom_container_environment, egress_control_config...
        "ingress_control_config": {
            "private_service_connect_config": {
                # Must be the same project the sandbox runs in.
                "enable_private_service_connect": True,
            }
        },
    }

### Create the PSC endpoint in your VPC

After the sandbox is created, read the service attachment from its connection info and target it with a forwarding rule (PSC endpoint) in your VPC:

    # The sandbox returns a service attachment to connect to
    service_attachment = sandbox.connection_info.service_attachment

    # Reserve an internal IP and create the PSC endpoint
    gcloud compute addresses create sandbox-ingress-ip \
        --region=REGION --subnet=YOUR_SUBNET
    
    gcloud compute forwarding-rules create sandbox-ingress-ep \
        --region=REGION \
        --network=YOUR_VPC \
        --address=sandbox-ingress-ip \
        --target-service-attachment=SERVICE_ATTACHMENT_URI

Clients in that project's VPC (or reachable through it) now connect to the sandbox through the endpoint's private IP (for example, a client connecting over the sandbox WebSocket or CDP port).

## What's next

  - Read the [Sandbox overview](https://docs.cloud.google.com/gemini-enterprise-agent-platform/scale/sandbox) and [Custom containers (BYOC)](https://docs.cloud.google.com/gemini-enterprise-agent-platform/scale/sandbox/custom-containers) .
  - Learn how [Private Service Connect interfaces work with Agent Runtime](https://docs.cloud.google.com/gemini-enterprise-agent-platform/scale/runtime/private-service-connect-interface) .
  - Review [VPC Service Controls troubleshooting](https://docs.cloud.google.com/vpc-service-controls/docs/troubleshooting) .
  - Follow the [Agent Engine PSC interface codelab](https://codelabs.developers.google.com/agent-engine-psc-interface-private) for an end-to-end egress walkthrough.
