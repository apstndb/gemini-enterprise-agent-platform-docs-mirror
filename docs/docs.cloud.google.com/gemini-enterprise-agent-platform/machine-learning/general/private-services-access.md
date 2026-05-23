---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/private-services-access
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/private-services-access
title: About accessing Gemini Enterprise Agent Platform services through private services access
description: Learn about accessing Gemini Enterprise Agent Platform services through private services access.
data_source: docs.cloud.google.com
---

Note: Use Private Service Connect (PSC) for Gemini Enterprise Agent Platform services that support it, as it's the recommended connection method. Only use private services access for services where PSC is not an option.

Gemini Enterprise Agent Platform services that have a checkmark in the **Private services access** column of the [Private access options for Gemini Enterprise Agent Platform](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/netsec-overview#private_access_options_for) table require you to connect to their services through [private services access](https://docs.cloud.google.com/vpc/docs/configure-private-services-access) .

These Google-managed Gemini Enterprise Agent Platform services support bidirectional communication with a service consumer's on-premises, multicloud, and VPC workloads.

This private communication happens exclusively by using internal IP addresses. VM instances don't need internet access or external IP addresses to reach services that are available through private services access.

Gemini Enterprise Agent Platform provides services that are hosted in a Google-managed VPC network. Private services access lets you reach the internal IP addresses of these Gemini Enterprise Agent Platform and third-party services through a VPC Network Peering connection.

The following diagram shows a [custom training](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/overview) architecture in which Agent Platform APIs for training jobs and pipeline jobs are enabled and managed in a service project ( `serviceproject` ) as part of a [Shared VPC](https://docs.cloud.google.com/vpc/docs/shared-vpc) deployment. These components are deployed as a Google-managed Infrastructure-as-a-Service (IaaS) in the service producer's VPC network. The service consumer's VPC network ( `hostproject` ) accesses these services through a private services access connection.

![image](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/images/vertex-ai-private-services-access.png)

## Private services access deployment options

You can create a new private connection or modify an existing one. Before you configure private services access, understand the [considerations](https://docs.cloud.google.com/vpc/docs/configure-private-services-access#considerations) for choosing a VPC network and IP address range.

To create a new private connection, you must first create an [allocated IP range](https://docs.cloud.google.com/vpc/docs/configure-private-services-access#procedure) and then create a [private connection](https://docs.cloud.google.com/vpc/docs/configure-private-services-access#creating-connection) between your VPC network and Google-managed Gemini Enterprise Agent Platform services.

Alternatively, you can modify an existing connection. For more information, see [Modify a private connection](https://docs.cloud.google.com/vpc/docs/configure-private-services-access#modifying-connection) .

### Gemini Enterprise Agent Platform subnet recommendations

The following table lists the recommended subnet ranges for Gemini Enterprise Agent Platform services.

| Gemini Enterprise Agent Platform feature                                                                                                                    | Recommended subnet range |
| ----------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------ |
| [Managed notebook instances](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/workbench/managed/networking#reserve-ip-range) | /29                      |
| Gemini Enterprise Agent Platform Pipelines                                                                                                                  | /21                      |
| [Custom training jobs](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/using-private-ip#reserving-ip-ranges)       | /19                      |
| Vector Search online queries                                                                                                                                | /16                      |
| [Private services access endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/using-private-endpoints)    | /21                      |

## Deployment considerations

Following are some important considerations that affect how you establish communication between your on-premises, multicloud, and VPC workloads and Google-managed Gemini Enterprise Agent Platform services.

### IP advertisement

You must advertise the private services access subnet range from the Cloud Router as a custom advertised route. For more information, see [Advertise custom IP ranges](https://docs.cloud.google.com/network-connectivity/docs/router/how-to/advertising-custom-ip) .

### VPC Network Peering

The service producer's network might not have the correct routes to direct traffic to your on-premises network. By default, the service producer's network only learns the subnet routes from your VPC network. Therefore, any request that's not from a subnet IP range is dropped by the service producer.

For this reason, in your VPC network, you must [update the peering connection](https://docs.cloud.google.com/vpc/docs/using-vpc-peering#update-peer-connection) to export custom routes to the service producer's network. Exporting routes sends all eligible static and dynamic routes that are in your VPC network, such as routes to your on-premises network, to the service producer's network. The service producer's network automatically imports them and then can send traffic back to your on-premises network through the VPC network.

### Firewall rules

You must update the firewall rules for the VPC network that connects your on-premises and multicloud environments to Google Cloud to allow ingress traffic from and egress traffic to private services access subnets.
