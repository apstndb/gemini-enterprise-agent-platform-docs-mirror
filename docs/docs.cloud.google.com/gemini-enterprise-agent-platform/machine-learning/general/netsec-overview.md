---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/netsec-overview
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/netsec-overview
title: Gemini Enterprise Agent Platform networking access overview
description: Learn about Gemini Enterprise Agent Platform's enterprise networking options to safely access resources from on-premises or multi cloud environments, protect artifacts from exfiltration, and configure network traffic.
data_source: docs.cloud.google.com
---

Gemini Enterprise Agent Platform supports enterprise networking options for accessing Gemini Enterprise Agent Platform endpoints and services that help you:

  - Safely access your Gemini Enterprise Agent Platform resources from an on-premises or multi cloud environment.
  - Protect your Gemini Enterprise Agent Platform artifacts from exfiltration.
  - Configure network traffic for your Gemini Enterprise Agent Platform resources.

This page is intended for enterprise networking architects and administrators who are already familiar with Google Cloud networking concepts.

## Public access for Gemini Enterprise Agent Platform

Gemini Enterprise Agent Platform services that are accessible from the internet have a checkmark in the **Public internet** column of the [Accessing Gemini Enterprise Agent Platform from on-premises and multi cloud](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/netsec-overview#access-methods) table. The APIs for these services resolve to the fully qualified domain name `  REGION -aiplatform.googleapis.com ` , which returns publicly routable IP addresses.

## Private access options for Gemini Enterprise Agent Platform

Gemini Enterprise Agent Platform supports the following options for accessing Gemini Enterprise Agent Platform endpoints and services privately, without assigning external IP addresses to your Google Cloud resources:

  - [Gemini Enterprise Agent Platform deployed with Private Service Connect (PSC)](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/psc-endpoints) enables secure, private, and explicit access to Gemini Enterprise Agent Platform services, eliminating the need for complex configurations like VPC peering that result in peered network route table exchange and IP address allocation. This makes it easier to connect to services. It's a key solution for both service consumers and producers, simplifying network management and enhancing security. Private Service Connect offers the following features:
      - **PSC Endpoints** : A consumer can create a forwarding rule in their VPC that references the service attachment. This creates a private IP address within their network, allowing internal resources (like VMs) and cross-cloud clients over hybrid networking to access Gemini Enterprise Agent Platform.
      - **PSC Backends** : A consumer can use a PSC network endpoint group (NEG) as a backend for an internal or external regional load balancer. This unlocks load balancer features such as:
          - Logging and monitoring of ingress traffic
          - Traffic management
          - Google Cloud Armor integration
          - Transitivity over VPC peering
  - [Private Service Connect endpoints for Google APIs](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/googleapi-access-methods#psc) let your Google Cloud resources or on-premises systems connect to an endpoint in your VPC network, which forwards requests to Google APIs and services.
  - [Private Google Access](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/googleapi-access-methods#pga) :
      - Lets your Google Cloud resources connect to the [standard external IP addresses or Private Google Access domains and virtual IP (VIP) addresses](https://docs.cloud.google.com/vpc/docs/configure-private-google-access#config) for Google APIs and services through the VPC network's default internet gateway.
      - Lets your on-premises hosts connect to Google APIs and services through a Cloud VPN tunnel or VLAN attachment by using one of the [Private Google Access-specific domains and VIPs](https://docs.cloud.google.com/vpc/docs/private-google-access-hybrid#private-vips) .
  - [Gemini Enterprise Agent Platform deployed with private services access (PSA)](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/private-services-access) enables a private connection between your Virtual Private Cloud (VPC) network and service producer's (Gemini Enterprise Agent Platform) VPC network. The underlying infrastructure of private services access is VPC peering between the consumer and producer network, allowing route exchange between the networks. Following are features and limitations of private services access (PSA):
      - PSA is built on top of VPC Network Peering. When you set up PSA, Google Cloud establishes a peering connection between your VPC network and the service producer's VPC network.
      - A key requirement of PSA is that you, the service consumer, must allocate a dedicated internal IP address range for the service producer's use. This range is reserved and cannot be used in your own VPC, which helps prevent IP address conflicts.
      - Once the connection is established, the service producer provisions your requested resources within their own VPC network, using an IP address from the address range you allocated. These resources are isolated to your project.
      - VPC peering is not transitive.
      - Private Service Connect, through endpoints, backends, or an interface, provides significant enhancements compared to private services access, including network transitivity and lower consumption of IP addresses. Therefore, Private Service Connect is the recommended solution.
  - [Gemini Enterprise Agent Platform deployed with PSC interface](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/psc-interfaces) enables traffic flows from the service producer's (Gemini Enterprise Agent Platform) network out to the consumer's network. This is useful for scenarios where a managed service needs to interact with resources in the customer's VPC, on-premises, or multicloud networks.

## Gemini Enterprise Agent Platform access methods

The following table shows the supported access methods for connecting from on-premises and multi cloud environments to Gemini Enterprise Agent Platform services. In this table, a checkmark indicates that an access method is supported. For more information about using an access method with a specific Gemini Enterprise Agent Platform service, click the *Learn more* link.

<table style="width:100%;">
<colgroup>
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
</colgroup>
<thead>
<tr class="header">
<th>Gemini Enterprise Agent Platform product</th>
<th>Public internet</th>
<th>Private Service Connect for Google APIs</th>
<th>Private Google Access</th>
<th>Private services access</th>
<th>Private Service Connect endpoint</th>
<th>Private Service Connect interface</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Batch inferences</td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
</tr>
<tr class="even">
<td>Datasets</td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
</tr>
<tr class="odd">
<td>Vertex AI Feature Store (Bigtable online serving)</td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
</tr>
<tr class="even">
<td>Vertex AI Feature Store (optimized online serving) ( <a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/deprecations">Deprecated</a> )</td>
<td></td>
<td></td>
<td></td>
<td></td>
<td><br />
<a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/featurestore/latest/online-serving-types#optimized_private">Learn more</a></td>
<td></td>
</tr>
<tr class="odd">
<td>Claude / Anthropic on Agent Platform</td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
</tr>
<tr class="even">
<td>Generative AI on Gemini Enterprise Agent Platform (Gemini)</td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
</tr>
<tr class="odd">
<td>Model Registry</td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
</tr>
<tr class="even">
<td>Online inference - dedicated public endpoint</td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
</tr>
<tr class="odd">
<td>Online inference - shared public endpoint</td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
</tr>
<tr class="even">
<td>Online inference - dedicated private endpoint</td>
<td></td>
<td></td>
<td></td>
<td></td>
<td><br />
<a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/private-service-connect">Learn more</a></td>
<td></td>
</tr>
<tr class="odd">
<td>Online inference - private endpoint</td>
<td></td>
<td></td>
<td></td>
<td><br />
<a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/using-private-endpoints">Learn more</a></td>
<td></td>
<td></td>
</tr>
<tr class="even">
<td>Vector Search (index creation)</td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
</tr>
<tr class="odd">
<td>Vector Search (index query)</td>
<td></td>
<td></td>
<td></td>
<td></td>
<td><br />
<a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/matching-engine/match-eng-setup/private-service-connect">Learn more</a></td>
<td></td>
</tr>
<tr class="even">
<td>Ray on Agent Platform (data plane)</td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td><br />
<a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/open-source/ray/create-cluster#use-psc-i-egress">Learn more</a></td>
</tr>
<tr class="odd">
<td>Agent Platform Pipelines, custom training, Ray on Agent Platform (control plane)</td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
</tr>
<tr class="even">
<td>Custom training (data plane)</td>
<td></td>
<td></td>
<td></td>
<td><br />
<a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/using-private-ip">Learn more</a></td>
<td></td>
<td><br />
<a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/psc-i-egress">Learn more</a></td>
</tr>
<tr class="odd">
<td>Agent Platform Pipelines</td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td><br />
<a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/pipelines/configure-private-service-connect">Learn more</a></td>
</tr>
<tr class="even">
<td>Agent Runtime</td>
<td></td>
<td></td>
<td></td>
<td></td>
<td></td>
<td><br />
<a href="https://docs.cloud.google.com/vertex-ai/generative-ai/docs/agent-engine/deploy#psc-i">Learn more</a></td>
</tr>
</tbody>
</table>

## Securing your Gemini Enterprise Agent Platform resources

To reduce the risk of data exfiltration for your Gemini Enterprise Agent Platform resources, you can place them within a service perimeter using VPC Service Controls.

  - To understand VPC Service Controls, see [Overview of VPC Service Controls](https://docs.cloud.google.com/vpc-service-controls/docs/overview) .
  - For detailed guidance, see [VPC Service Controls with Gemini Enterprise Agent Platform](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/vpc-service-controls) .
  - To understand costs, review [pricing](https://cloud.google.com/vpc-service-controls/pricing) .

## What's next

  - Learn how to [Set up VPC Network Peering](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/vpc-peering) for Gemini Enterprise Agent Platform.

  - Learn how to [Set up connectivity from Gemini Enterprise Agent Platform to Other Networks](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/hybrid-connectivity) .

  - For general guidance and best practices for configuring your VPC networks, see [Connecting multiple VPC networks](https://cloud.google.com/architecture/best-practices-vpc-design#connecting_multiple_networks) .

  - Learn more about using [Google Cloud Network Connectivity products](https://docs.cloud.google.com/network-connectivity/docs/how-to/choose-product#google-cloud) such as Cloud VPN, Cloud Interconnect, and Cloud Router to connect your non-Google Cloud (on-premises or multi cloud) network to a Google Cloud Virtual Private Cloud (VPC) host network.
