---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/vpc-psc-i-setup
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/vpc-psc-i-setup
title: Set up a Private Service Connect interface for Gemini Enterprise Agent Platform resources
description: Learn how to set up a Private Service Connect interface for Gemini Enterprise Agent Platform resources.
data_source: docs.cloud.google.com
---

This guide shows how to set up a [Private Service Connect interface](https://docs.cloud.google.com/vpc/docs/about-private-service-connect-interfaces) for Gemini Enterprise Agent Platform resources.

You can configure Private Service Connect interface connections for certain resources in Gemini Enterprise Agent Platform, including:

  - [Ray on Vertex AI](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/open-source/ray-on-vertex-ai/create-cluster#enable_interface)
  - [Custom training](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/psc-i-egress)
  - [Gemini Enterprise Agent Platform Pipelines](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/pipelines/configure-private-service-connect)
  - [Agent Runtime](https://docs.cloud.google.com/vertex-ai/generative-ai/docs/agent-engine/deploy#psc-i)

Unlike [VPC peering](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/vpc-peering) connections, Private Service Connect interface connections are transitive. This requires fewer IP addresses in the consumer VPC network. This allows greater flexibility in connecting to other VPC networks in your Google Cloud project and on-premises.

This guide is for network administrators familiar with Google Cloud networking concepts.

## Objectives

This guide covers the following tasks:

  - Configure a consumer VPC network, subnet, and network attachment.
  - Add firewall rules to your Google Cloud network host project.
  - Create a Agent Platform resource specifying the network attachment to use a Private Service Connect interface.

## Before you begin

Use the following instructions to create or select a Google Cloud project and configure it for use with Gemini Enterprise Agent Platform and Private Service Connect.

1.  If you're not the project owner and don't have the [Project IAM Admin ( `roles/resourcemanager.projectIamAdmin` )](https://docs.cloud.google.com/resource-manager/docs/access-control-proj#resourcemanager.projectIamAdmin) role, ask the owner to grant you an IAM role that includes the `compute.networkAttachments.update` , `compute.networkAttachments.update` , and `compute.regionOperations.get` permissions: for example, the Compute Network Admin ( `roles/compute.networkAdmin` ) role, to manage networking resources.
2.  Assign the required roles to the [AI Platform Service Agent](https://docs.cloud.google.com/iam/docs/service-agents#ai-platform-service-agent) . For details about which roles to grant in different scenarios, see the [Gemini Enterprise Agent Platform service agent required role](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/vpc-psc-i-setup#service-agent-required-role) section of this document.

## Set up a VPC network and subnet

> **Note:** If you already have an existing VPC network, ensure the subnet IPv4 range is in the [valid RFC 1918 ranges](https://docs.cloud.google.com/vpc/docs/subnets#valid-ranges) , and then go to the [Create a network attachment section](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/vpc-psc-i-setup#create-network-attachment) .

Follow the configuration steps to create a new VPC network if you don't have an existing network.

1.  [Create a VPC network:](https://docs.cloud.google.com/vpc/docs/create-modify-vpc-networks#gcloud_1)
    
        gcloud compute networks create NETWORK \
            --subnet-mode=custom
    
    Replace NETWORK with a name for the VPC network.

2.  [Create a subnet:](https://docs.cloud.google.com/vpc/docs/create-modify-vpc-networks#add-subnets)
    
        gcloud compute networks subnets create SUBNET_NAME \
            --network=NETWORK \
            --range=PRIMARY_RANGE \
            --region=REGION
    
    Replace the following:
    
      - SUBNET\_NAME : a name for the subnet.
    
      - PRIMARY\_RANGE : the primary IPv4 range for the new subnet, in CIDR notation.
        
        The following are the IP requirements and limitations for Agent Platform:
        
          - Agent Platform recommends a `/28` subnetwork.
        
          - The subnet of the network attachment supports RFC 1918 and non RFC 1918 addresses with the exception of subnets 100.64.0.0/20 and 240.0.0.0/4.
        
          - Agent Platform can only connect to RFC 1918 IP address ranges that are routable from the specified network.
        
          - Agent Platform can't reach a privately used public IP address or these non-RFC 1918 ranges:
            
              - `100.64.0.0/20`
              - `192.0.0.0/24`
              - `192.0.2.0/24`
              - `198.18.0.0/15`
              - `198.51.100.0/24`
              - `203.0.113.0/24`
              - `240.0.0.0/4`
        
        For more information, see [IPv4 subnet ranges](https://docs.cloud.google.com/vpc/docs/subnets#manually_created_subnet_ip_ranges) .
    
      - REGION : the Google Cloud region where you create the new subnet.

## Create a network attachment

In a Shared VPC deployment, create the subnet used for the Network Attachment in the Host Project, then create the Private Service Connect Network Attachment in the Service Project.

The following example shows how to [Create a network attachment](https://docs.cloud.google.com/vpc/docs/create-manage-network-attachments) that automatically accepts connections.

``` 
   gcloud compute network-attachments create NETWORK_ATTACHMENT_NAME \
       --region=REGION \
       --connection-preference=ACCEPT_AUTOMATIC \
       --subnets=SUBNET_NAME
```

Replace NETWORK\_ATTACHMENT\_NAME with a name for the network attachment.

If the network attachment is created in a project different from the Service Project, you need to pass the full network attachment path when calling the Gemini Enterprise.

## Gemini Enterprise Agent Platform service agent required role

In the project where you create the network attachment, grant the `compute.networkAdmin` role to the [Gemini Enterprise Agent Platform service agent](https://docs.cloud.google.com/vertex-ai/docs/general/access-control#service-agents) of the same project. Enable the Agent Platform API in this project in advance if it differs from the service project where you use Agent Platform.

If you specify a [Shared VPC](https://docs.cloud.google.com/vpc/docs/provisioning-shared-vpc#setting_up) network for Agent Platform to use and you create a network attachment in a service project, then grant the [Agent Platform service agent](https://docs.cloud.google.com/vertex-ai/docs/general/access-control#service-agents) in the service project where you use Agent Platform the `compute.networkUser` role to your VPC host project.

## Configure firewall rules

The system applies [Ingress firewall rules](https://docs.cloud.google.com/firewall/docs/firewalls) in the consumer VPC to enable communication with the Private Service Connect interface network attachment subnet from compute and on-premises endpoints.

Configuring firewall rules is optional. However, we recommend that you set common firewall rules as shown in the following examples.

1.  Create a firewall rule that allows SSH access on TCP port 22:
    
        gcloud compute firewall-rules create NETWORK-firewall1 \
            --network NETWORK \
            --allow tcp:22

2.  Create a firewall rule that allows HTTPS traffic on TCP port 443:
    
        gcloud compute firewall-rules create NETWORK-firewall2 \
            --network NETWORK \
            --allow tcp:443

3.  Create a firewall rule that allows ICMP traffic (such as ping requests):
    
        gcloud compute firewall-rules create NETWORK-firewall3 \
            --network NETWORK \
            --allow icmp

## Set up a private DNS peering

To enable Vertex AI Training jobs or Agent Runtime agents configured with PSC-I to resolve private DNS records in customer-managed Cloud DNS zones, the Agent Platform API offers a user-configurable mechanism for specifying which DNS domains to peer with Google internal resources. Make the following additional configurations:

1.  Assign the DNS `Peer(roles/dns.peer)` role to the [AI Platform Service Agent](https://docs.cloud.google.com/vertex-ai/docs/general/access-control#service-agents) account of the project where you're using Vertex AI Training or Agent Runtime services. If you specify a [Shared VPC](https://docs.cloud.google.com/vpc/docs/provisioning-shared-vpc#setting_up) network for Gemini Enterprise Agent Platform to use and create a network attachment in a service project, then grant the [AI Platform Service Agent](https://docs.cloud.google.com/vertex-ai/docs/general/access-control#service-agents) in the service project where you use Agent Platform the DNS `Peer(roles/dns.peer)` role in your VPC host project.

2.  Create a firewall rule that allows all ICMP, TCP, and UDP traffic (optional):
    
        gcloud compute firewall-rules create NETWORK-firewall4 \
            --network NETWORK
            --allow tcp:0-65535,udp:0-65535,icmp
            --source-ranges IP_RANGES

3.  Set up your private DNS zone for DNS resolution and traffic routing. To add DNS records to your private DNS zone, see [Add a resource record set](https://docs.cloud.google.com/dns/docs/records#add-rrset) .

## Troubleshooting

This section covers some common issues for configuring Private Service Connect with Gemini Enterprise Agent Platform.

When configuring Agent Platform with a Shared VPC, create the network attachment in the service project where you use Agent Platform. This approach helps prevent certain error messages, such as:

    _Please make sure that the Agent Platform API is enabled for the
    project_, by ensuring the
    necessary permissions and APIs are enabled in the correct project.

## What's next

  - Learn how to use Private Service Connect interface egress for [Ray on Vertex AI](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/open-source/ray-on-vertex-ai/create-cluster) .
  - Learn how to use Private Service Connect interface egress for [custom training](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/psc-i-egress) .
  - Learn how to use Private Service Connect interface egress for [Agent Platform Pipelines](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/pipelines/configure-private-service-connect) .
  - Learn how to use Private Service Connect interface egress for [Agent Runtime](https://docs.cloud.google.com/vertex-ai/generative-ai/docs/agent-engine/deploy#psc-i)
