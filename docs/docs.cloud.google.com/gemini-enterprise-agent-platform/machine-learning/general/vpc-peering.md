---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/vpc-peering
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/vpc-peering
title: Set up VPC Network Peering
description: Learn how to set up VPC Network Peering to peer with Gemini Enterprise Agent Platform resources.
data_source: docs.cloud.google.com
---

You can configure Gemini Enterprise Agent Platform to peer with [Virtual Private Cloud (VPC)](https://docs.cloud.google.com/vpc/docs/vpc-peering) to connect directly with certain resources in Agent Platform, including:

  - [Custom training](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/using-private-ip)
  - [NFS shares for custom training](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/train-nfs-share)
  - [Private inference endpoints](https://docs.cloud.google.com/vertex-ai/docs/predictions/using-private-endpoints)
  - [Ray on Agent Platform](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/open-source/ray/create-cluster#use-psc-i-egress)
  - [Vector matching online queries](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search/setup/vpc#vpc-network-peering-setup)
  - [Pipelines](https://docs.cloud.google.com/vertex-ai/docs/pipelines/use-components#set_up)

This guide shows how to set up [VPC Network Peering](https://docs.cloud.google.com/vpc/docs/vpc-peering) to peer your network with Agent Platform resources. This guide is recommended for networking administrators who are already familiar with Google Cloud networking concepts.

## Overview

This guide covers the following tasks:

  - Configure [private services access](https://docs.cloud.google.com/vpc/docs/configure-private-services-access) for the VPC. This establishes a peering connection between your VPC and Google's shared VPC network.
  - Consider the IP range you need to reserve for Agent Platform.
  - If applicable, export custom routes so that Agent Platform can import them.

## Before you begin

  - Select a VPC that you want to peer with Agent Platform resources. Agent Platform can be peered with only one network per region at a time.

  - Select or create a Google Cloud project to use for Agent Platform.

  - [Verify that billing is enabled for your Google Cloud project](https://docs.cloud.google.com/billing/docs/how-to/verify-billing-enabled#confirm_billing_is_enabled_on_a_project) .

  - Enable the Compute Engine API, Agent Platform API, and Service Networking APIs.
    
    **Roles required to enable APIs**
    
    To enable APIs, you need the Service Usage Admin IAM role ( `roles/serviceusage.serviceUsageAdmin` ), which contains the `serviceusage.services.enable` permission. [Learn how to grant roles](https://docs.cloud.google.com/iam/docs/granting-changing-revoking-access) .

  - Optionally, you can use [Shared VPC](https://docs.cloud.google.com/vpc/docs/shared-vpc) . If you use Shared VPC, you usually use Agent Platform in a separate Google Cloud project than your VPC host project. Enable the Compute Engine API and Service Networking APIs in both projects. Learn how to [provision Shared VPC](https://docs.cloud.google.com/vpc/docs/provisioning-shared-vpc) .

  - Install the [gcloud CLI](https://docs.cloud.google.com/sdk/docs) if you want to run the `gcloud` examples in this guide.

### Required roles

If you are not a project owner or editor, make sure you have the [Compute Network Admin role](https://docs.cloud.google.com/compute/docs/access/iam#compute.networkAdmin) ( `roles/compute.networkAdmin` ), which includes the required roles you need to manage networking resources.

### Peering with an on-premises network

For VPC Network Peering with an on-premises network, there are additional steps:

1.  Connect your on-premises network to your VPC. You can use a [VPN tunnel](https://docs.cloud.google.com/network-connectivity/docs/vpn/how-to/adding-a-tunnel) or [Interconnect](https://docs.cloud.google.com/network-connectivity/docs/interconnect/concepts/overview) .
2.  Set up [custom routes](https://docs.cloud.google.com/vpc/docs/routes#custom-routes) from the VPC to your on-premises network.
3.  Export your custom routes so that Agent Platform can import them.

## Set up private services access for your VPC

When you set up private services access, you establish a private connection between your network and a network owned by Google or a third party service ( *service producers* ). In this case, Agent Platform is a service producer. To set up [private services access](https://docs.cloud.google.com/vpc/docs/configure-private-services-access) , you [reserve an IP range](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/vpc-peering#reserving-ip-ranges) for service producers, and then create a peering connection with Agent Platform.

If you already have a VPC with [private services access](https://docs.cloud.google.com/vpc/docs/configure-private-services-access) configured, move on to [exporting custom routes](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/vpc-peering#export-custom-routes) .

1.  Set environment variables for your project ID, the name of your reserved range, and the name of your network. If you use Shared VPC, use the project ID of your VPC host project. Otherwise, use the project ID of Google Cloud project you use for Agent Platform.

2.  [Enable the required APIs](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/vpc-peering#before_you_begin) . If you use Shared VPC, see [Use Shared VPC with Agent Platform](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/vpc-peering#shared-vpc) .

3.  Set a reserved range using [`gcloud compute addresses create`](https://docs.cloud.google.com/sdk/gcloud/reference/compute/addresses/create) .

4.  Establish a peering connection between your VPC host project and Google's Service Networking, using [`gcloud services vpc-peerings connect`](https://docs.cloud.google.com/sdk/gcloud/reference/services/vpc-peerings/connect) .
    
    For [private inference endpoints](https://docs.cloud.google.com/vertex-ai/docs/predictions/using-private-endpoints) , we recommended reserving at least a `/21` block for the subnet for model hosting. Reserving a smaller block can result in deployment errors due to insufficient IP addresses.
    
    The `172.16.0.0/16` subnet is reserved for Vertex AI Training. You must specify a subnet that doesn't overlap with this CIDR range.
    
        PROJECT_ID=YOUR_PROJECT_ID
        gcloud config set project $PROJECT_ID
        
        # This is for display only; you can name the range anything.
        PEERING_RANGE_NAME=google-reserved-range
        
        NETWORK=YOUR_NETWORK_NAME
        
        # NOTE: `prefix-length=16` means a CIDR block with mask /16 will be
        # reserved for use by Google services, such as Agent Platform.
        gcloud compute addresses create $PEERING_RANGE_NAME \
          --global \
          --prefix-length=16 \
          --description="peering range for Google service" \
          --network=$NETWORK \
          --purpose=VPC_PEERING
        
        # Create the VPC connection.
        gcloud services vpc-peerings connect \
          --service=servicenetworking.googleapis.com \
          --network=$NETWORK \
          --ranges=$PEERING_RANGE_NAME \
          --project=$PROJECT_ID

Learn more about [private services access](https://docs.cloud.google.com/vpc/docs/private-services-access) .

> **Note:** Privately used public IP ranges are not imported by default. If you want to use these ranges, you must [enable import of privately-used public IP ranges](https://docs.cloud.google.com/vpc/docs/configure-private-services-access#import-export-pub) .

> **Note:** Agent Platform uses the same Private Services Access as [Cloud SQL](https://docs.cloud.google.com/sql/docs/sqlserver/configure-private-services-access) . If you configure both in the same VPC network, ensure that you allocate enough IP addresses for both services. Alternatively, you can nominate a subset of the reservation for training jobs to use by passing the [`reserved_ip_ranges`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/pipelines/request-gcp-machine-resources) parameter.

### Use Shared VPC with Agent Platform

If you use Shared VPC in your project, see how to [Provision Shared VPC](https://docs.cloud.google.com/vpc/docs/provisioning-shared-vpc) and make sure to complete the following steps:

1.  Enable the Compute Engine API and Service Networking APIs in the host and service project. Agent Platform API must be enabled for the service project.

2.  Create the VPC Network Peering connection between your VPC and Google services within the host project.

3.  During Agent Platform creation, you must specify the name of the network that you want Agent Platform to have access to Shared VPC.

4.  Verify that the service or user account used has the role [Compute Network User role](https://docs.cloud.google.com/compute/docs/access/iam#compute.networkUser) ( `roles/compute.networkUser` ).

### Reserve IP ranges for Agent Platform

When you reserve an IP range for service producers, the range can be used by Agent Platform and other services. If you connect with multiple service producers using the same range, allocate a larger range to accommodate them, in order to avoid IP exhaustion.

Refer to the [Subnet recommendations](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/private-services-access#subnet-recommendations) table to ensure that the IP reservation for Private Services Access is wide enough accommodate your workload.

If a job is launched with the [`--network`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/reference/rest/v1/CustomJobSpec) parameter, it will launch in a Google-managed network that is peered to your VPC:

`--network = "projects/${host_project}/global/networks/${network}"`

Any jobs that don't need to access your networks can be launched without this declaration, thus preserving your IP allocations.

If you are unable to reserve a wide enough IP range, consider migrating from [Gemini Enterprise Agent Platform with Private Services Access](https://docs.cloud.google.com/vpc/docs/configure-private-services-access#troubleshooting) to [Gemini Enterprise Agent Platform with Private Service Connect](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/vpc-psc-i-setup)

## Export custom routes

If you use custom routes, you need to export them so that Agent Platform can import them. If you don't use custom routes, skip this section.

To export custom routes, you [update the peering connection](https://docs.cloud.google.com/vpc/docs/using-vpc-peering#update-peer-connection) in your VPC. Exporting custom routes sends all [eligible static and dynamic routes](https://docs.cloud.google.com/vpc/docs/vpc-peering#considerations) that are in your VPC network, such as routes to your on-premises network, to service producers' networks (Agent Platform in this case). This establishes the necessary connections and allows training jobs to send traffic back to your on-premises network.

Ensure that your on-premises network has routes *back* to the IP address ranges allocated for Agent Platform so that responses are correctly routed back to Agent Platform. For example, use Cloud Router custom route advertisements that include the Agent Platform IP address ranges.

Learn more about [private connections with on-premises networks](https://docs.cloud.google.com/vpc/docs/private-services-access#on-premises-connectivity) .

### Console

1.  Go to the VPC Network Peering page in the Google Cloud console.  
2.  Select the peering connection to update.
3.  Click **Edit** .
4.  Select **Export custom routes** .

### gcloud

1.  Find the name of the peering connection to update. If you have multiple peering connections, omit the `--format` flag.
    
        gcloud services vpc-peerings list \
          --network=$NETWORK \
          --service=servicenetworking.googleapis.com \
          --project=$PROJECT_ID \
          --format "value(peering)"

2.  Update the peering connection to export custom routes.
    
        gcloud compute networks peerings update PEERING-NAME \
            --network=$NETWORK \
            --export-custom-routes \
            --project=$PROJECT_ID

## Check the status of your peering connections

To see that peering connections are active, you can list them using the following command:

    gcloud compute networks peerings list --network $NETWORK

You should see that the state of the peering you just created is `ACTIVE` . Learn more about [active peering connections](https://docs.cloud.google.com/vpc/docs/peer-two-networks#peering-becomes-active) .

## Troubleshooting

This section lists some common issues for configuring VPC Network Peering with Agent Platform.

  - When you configure Agent Platform to use a Shared VPC network, specify the network URI in the following way.
    
    "projects/ YOUR\_SHARED\_VPC\_HOST\_PROJECT /global/networks/ YOUR\_SHARED\_VPC\_NETWORK "

  - If you specify a [Shared VPC network](https://docs.cloud.google.com/vpc/docs/provisioning-shared-vpc#setting_up) for Agent Platform to use, then make sure that any user or Service Account actors for Agent Platform in the service project have `compute.networkUser` role granted in your host project.

  - Make sure that you've allocated a sufficient IP range for all service producers your network connects to, including Agent Platform.

  - If you encounter the error messages `IP_SPACE_EXHAUSTED` , `RANGES_EXHAUSTED` , or `PEERING_RANGE_EXHAUSTED` you must increase the amount of available IP addresses for the `servicenetworking` reservation in your network. You can [add a new range](https://docs.cloud.google.com/vpc/docs/configure-private-services-access#modifying-connection) to the existing VPC Network Peering configuration or delete some Agent Platform resources to release allocated IP addresses.

  - Connection Timeouts: After exporting custom routes, connections from Agent Platform will be routed through your network to reach endpoints in other networks. However, those endpoints may not route through your network to send responses *back* to Agent Platform. Make sure that you also add static or dynamic routes in those networks for the return-path to the Agent Platform allocated IP range.

  - Connection Timeouts / Host Unreachable errors: Since [transitive peering is not supported](https://docs.cloud.google.com/vpc/docs/vpc-peering#transit-network) , connections from Agent Platform won't be able to reach endpoints in other networks that are directly peered to your network, even with "Export custom routes" enabled. Work with your network administrator to make sure that there are no attempts to route directly your network from one directly peered network to another. If needed, you may replace one of these peering hops with a solution that supports static or dynamic routes.

  - Host Unreachable DNS errors: If your Gemini Enterprise Agent Platform job needs to resolve hostnames in your VPC, ensure that you have completed the configuration to [Share private DNS zones with service producers](https://docs.cloud.google.com/vpc/docs/configure-private-services-access#dns-peering) .

  - If your pipeline job fails to create with "internal error" identified in Logs Explorer, ensure you have a VPC network deployed in addition to the private services access subnet.

  - You can check which services are using which IP addresses so that, for example, you can see which services are using large blocks of IP addresses and avoid IP address exhaustion.

  - If you encounter the error `Unable to create an instance within a Shared VPC network` , see [Troubleshooting Agent Platform Workbench](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/troubleshooting-workbench?component=any#create-shared-vpc-instances) .

  - If you encounter the error message `For the peered network $network_name, couldn't find a free blocks in allocated IP ranges. This is needed to create the cluster.` , you must increase the amount of available allocated ranges for the service. You can accomplish this in the following ways:
    
      - [Add a new allocated range to your network](https://docs.cloud.google.com/vpc/docs/configure-private-services-access#procedure) and [add it to your `servicenetworking-googleapis-com` private connection](https://docs.cloud.google.com/vpc/docs/configure-private-services-access#modifying-connection) . Note that the minimum required allocated range size is `/18` .
      - Delete existing unused Agent Platform resources to release allocated IP addresses.
      - Use [Network Analyzer](https://docs.cloud.google.com/network-intelligence-center/docs/network-analyzer/overview) to identify subnet utilization and potential issues.

For additional troubleshooting information, refer to [VPC Network Peering troubleshooting guide](https://docs.cloud.google.com/vpc/docs/using-vpc-peering#troubleshooting) .

## What's next

  - Learn [how to use private IP for custom training](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/using-private-ip) .
  - Learn [how to use private endpoints for inference](https://docs.cloud.google.com/vertex-ai/docs/predictions/using-private-endpoints) .
  - Learn more about [VPC Network Peering](https://docs.cloud.google.com/vpc/docs/vpc-peering) .
  - See [reference architectures and best practices](https://docs.cloud.google.com/solutions/best-practices-vpc-design#shared-service) for VPC design.
