---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/psc-endpoints
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/psc-endpoints
title: About accessing Gemini Enterprise Agent Platform services through Private Service Connect endpoints
description: Learn about Gemini Enterprise Agent Platform service producers that require connection through Private Service Connect endpoints, supporting unidirectional communication from service consumers' workloads to Google-managed Gemini Enterprise Agent Platform services via internal IP addresses and NAT, which allows access without leaving VPC networks or using external IP addresses.
data_source: docs.cloud.google.com
---

Some Gemini Enterprise Agent Platform service producers require you to connect to their services through [Private Service Connect endpoints](https://docs.cloud.google.com/vpc/docs/private-service-connect#endpoints) . These services are listed in the [Gemini Enterprise Agent Platform access methods](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/netsec-overview#access-methods) table. They support unidirectional communication from a service consumer's on-premises, multicloud, and VPC workloads to Google-managed Gemini Enterprise Agent Platform services. Clients connect to the endpoint by using internal IP addresses. Private Service Connect performs network address translation (NAT) to route requests to the service.

Service consumers can use their own internal IP addresses to access these Gemini Enterprise Agent Platform services without leaving their VPC networks or using external IP addresses by creating a consumer endpoint. The endpoint connects to services in another VPC network using a Private Service Connect forwarding rule.

On the service producer's side of the private connection, there is a VPC network where your service resources are provisioned. This network is created exclusively for you and contains only your resources.

The following diagram shows a Vector Search architecture in which the Vector Search API is enabled and managed in a service project ( `serviceproject` ) as part of a [Shared VPC](https://docs.cloud.google.com/vpc/docs/shared-vpc) deployment. The Vector Search Compute Engine resources are deployed as a Google-managed Infrastructure-as-a-Service (IaaS) in the service producer's VPC network.

Private Service Connect endpoints are deployed in the service consumer's VPC network ( `hostproject` ) for index query, in addition to [Private Service Connect endpoints for Google APIs](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/googleapi-access-methods#psc) for private index creation.

For more information, see [Private Service Connect endpoints](https://docs.cloud.google.com/vpc/docs/private-service-connect#endpoints) .

![image](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/images/vertex-ai-psc-endpoints.png)

Before you configure Private Service Connect endpoints, learn about access [considerations](https://docs.cloud.google.com/vpc/docs/about-accessing-vpc-hosted-services-endpoints#limitations) .

## Private Service Connect endpoint deployment options

A Private Service Connect service attachment is generated from the producer service (such as Gemini Enterprise Agent Platform). As a consumer, you can gain access to the service producer by deploying a consumer endpoint in one or more VPC networks.

## Deployment considerations

The following sections discuss considerations for communication from your on-premises, multicloud, and VPC workloads to Google-managed Gemini Enterprise Agent Platform services.

### Private Service Connect backends

Google does not support using [Private Service Connect backends](https://docs.cloud.google.com/vpc/docs/access-apis-managed-services-private-service-connect-backends) with Gemini Enterprise Agent Platform online prediction endpoints.

### IP advertisement

  - When you use Private Service Connect to connect to services in another VPC network, you choose an IP address from a [regular subnet](https://docs.cloud.google.com/vpc/docs/subnets#purpose) in your VPC network.

  - By default, the Cloud Router will advertise regular VPC subnets unless custom advertisement mode is configured. For more information, see [Custom advertisement mode](https://docs.cloud.google.com/network-connectivity/docs/router/concepts/advertised-routes#overview-am-custom) .

  - The IP address for the consumer endpoint must be in the same region as the service producer's service attachment. For more information, see [Service attachments](https://docs.cloud.google.com/vpc/docs/private-service-connect#service-attachments) and [Access published services through endpoints](https://docs.cloud.google.com/vpc/docs/configure-private-service-connect-services) .

### Firewall rules

You must update the firewall rules for the VPC network that connects your on-premises and multicloud environments to Google Cloud to allow egress traffic to the Private Service Connect endpoint subnet. For more information, see [Firewall rules](https://docs.cloud.google.com/vpc/docs/manage-security-private-service-connect-consumers#firewall-rules) .

### ServiceAttachment reuse

> **Note:** This section describes network resource reuse and is different from [model co-hosting](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/model-co-hosting) , which describes compute resource reuse with `DeploymentResourcePool` .

When multiple Gemini Enterprise Agent Platform prediction endpoints are configured to use Private Service Connect with identical project allowlists, they might share the same `ServiceAttachment` resource. This allows consumer projects in the allowlist to connect to these prediction endpoints through the same `ServiceAttachment` . This reuse isn't guaranteed.

If prediction endpoints use different project allowlists, they use different `ServiceAttachment` resources to ensure that connections are only accepted from projects on their respective allowlists.

When multiple prediction endpoints share a `ServiceAttachment` , we recommend that you create and reuse one Private Service Connect endpoint for that `ServiceAttachment` , rather than creating a separate Private Service Connect endpoint for each prediction endpoint.
