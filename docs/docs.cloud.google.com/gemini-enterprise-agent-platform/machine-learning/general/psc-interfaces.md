---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/psc-interfaces
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/psc-interfaces
title: About accessing Gemini Enterprise Agent Platform services through Private Service Connect interfaces
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Some Gemini Enterprise Agent Platform [service producers](https://docs.cloud.google.com/vpc/docs/private-service-connect) require you to connect to their services through [Private Service Connect interfaces](https://docs.cloud.google.com/vpc/docs/about-private-service-connect-interfaces) . These services are listed in the [Gemini Enterprise Agent Platform access methods](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/netsec-overview#access-methods) table.

When a Private Service Connect interface is created, a VM instance with at least two network interfaces is also created. The first interface connects to a subnet in a producer VPC network. The second interface requests a connection to the [network attachment](https://docs.cloud.google.com/vpc/docs/about-network-attachments) subnet in a consumer network. If accepted, this interface is assigned an internal IP address from the consumer subnet.

On the service producer's side of the private connection, there is a VPC network where your service resources are provisioned. This network is created exclusively for you and contains only your resources. Connectivity between the producer and consumer network is established through the Private Service Connect interface.

The following diagram shows a Gemini Enterprise Agent Platform Pipelines architecture in which the Gemini Enterprise is enabled and managed in the consumer's network. The Gemini Enterprise Agent Platform Pipelines resources are deployed as a Google-managed infrastructure as a service (IaaS) in the service producer's VPC network. Since the Private Service Connect interface is deployed with an IP address from the consumer's subnet, the producer's network has access to the consumer's learned routes that can span VPC networks, multicloud environments, and on-premises networks.

![image](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/images/vertex-ai-psc-interfaces.png)

## Features and limitations

The following are features and limitations of Private Service Connect (PSC) interfaces:

  - The service consumer creates a network attachment in their VPC network, which is a resource that represents their side of the private connection.

  - The service producer creates the managed resource with a PSC interface that references the consumer's network attachment.

  - Once the consumer accepts the connection, the PSC interface is assigned an internal IP address from a subnet in the consumer's VPC network, allowing for secure, private, and bidirectional communication.

  - The [subnet of the network attachment](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/vpc-psc-i-setup#set-up-vpc-network) supports RFC 1918 and non RFC 1918 addresses with the exception of subnets `100.64.0.0/10` and `240.0.0.0/4` .

  - Gemini Enterprise Agent Platform can only connect to RFC 1918 IP address ranges that are routable from the specified network.

  - Private Service Connect interfaces don't support external IP addresses.

  - Gemini Enterprise Agent Platform can't reach a privately used public IP address or these non-RFC 1918 ranges:
    
      - `100.64.0.0/10`
      - `192.0.0.0/24`
      - `192.0.2.0/24`
      - `198.18.0.0/15`
      - `198.51.100.0/24`
      - `203.0.113.0/24`
      - `240.0.0.0/4`

## Private Service Connect connection preference

Private Service Connect offers a connection preference when deploying a network attachment that determines whether connection requests from a producer are automatically accepted or require manual approval. In Gemini Enterprise Agent Platform, accessing a network attachment with the preference "Automatically accept connections for all projects" ( `ACCEPT_AUTOMATIC` ) or "Accept connections for selected projects" ( `ACCEPT_MANUAL` ) are treated as follows:

  - A network attachment configured with the `ACCEPT_MANUAL` connection preference is supported in Gemini Enterprise Agent Platform without configuring the Gemini Enterprise Agent Platform project ID in the accepted project.
  - Gemini Enterprise Agent Platform uses the permissions ( `compute.networkAttachments.update` and `compute.regionOperations.get` ) to authorize the tenant project hosting Gemini Enterprise Agent Platform to use the network attachment for PSC Interface deployment for both `ACCEPT_AUTOMATIC` and `ACCEPT_MANUAL` connection preferences.

To learn more about IAM and deployment guidelines, see [Set up a Private Service Connect interface for Gemini Enterprise Agent Platform resources](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/vpc-psc-i-setup) .

## Private Service Connect interface deployment options

To create a Private Service Connect interface, first deploy a subnet within the consumer VPC that shares the same region as your producer service. Check the specific service requirements to make sure there are no subnet ranges that you should avoid. Then create a network attachment that references the subnet. We recommend that you dedicate the subnet allocated for the network attachment exclusively to Private Service Connect interface deployments.

The following pages discuss specific use cases for Gemini Enterprise Agent Platform Private Service Connect interfaces:

  - [Configure Private Service Connect interface for a pipeline](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/pipelines/configure-private-service-connect)
  - [Use Private Service Connect interface for Gemini Enterprise Agent Platform Training](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/psc-i-egress)
  - [Create a Ray cluster on Gemini Enterprise Agent Platform](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/open-source/ray-on-vertex-ai/create-cluster#enable_interface)
  - [Using Private Service Connect interface with Agent Runtime](https://docs.cloud.google.com/vertex-ai/generative-ai/docs/agent-engine/private-service-connect-interface)

## VPC Service Controls considerations

Gemini Enterprise Agent Platform producers' service ability to access the public internet depends on your project's security configuration, specifically whether you're using VPC Service Controls.

  - **Without VPC Service Controls** : The Google managed tenting hosting Gemini Enterprise Agent Platform retains its default internet access. This outbound traffic egresses directly from the secure, Google-managed environment where your producer service runs. The exception to this behavior is Agent Runtime, which doesn't provide internet egress. Instead, you're required to deploy a proxy VM with an RFC 1918 address for internet egress.
  - **With VPC Service Controls** : When your project is part of a VPC Service Controls perimeter, the Google-managed tenting hosting Gemini Enterprise Agent Platform default internet access is blocked by the perimeter to prevent data exfiltration. To allow the to access the public internet in this scenario, you must explicitly configure a secure egress path that routes traffic through your VPC network. The recommended way to achieve this is by setting up a proxy server inside your VPC perimeter and creating a Cloud NAT gateway to allow the proxy VM to access the internet.

To learn more about VPC Service Controls considerations, see [VPC Service Controls with Gemini Enterprise Agent Platform](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/vpc-service-controls) .

## Deployment considerations

The following are considerations for communication from your on-premises, multicloud, and VPC workloads to Google-managed Gemini Enterprise Agent Platform services.

### Gemini Enterprise Agent Platform subnet recommendations

The following table lists the recommended subnet ranges for Gemini Enterprise Agent Platform services that support Private Service Connect interfaces.

| Gemini Enterprise Agent Platform feature | Recommended subnet range |
| ---------------------------------------- | ------------------------ |
| Agent Platform Pipelines                 | /28                      |
| Custom training jobs                     | /28                      |
| Ray on Agent Platform                    | /28                      |
| Agent Runtime                            | /28                      |

### IP advertisement

  - When you use the Private Service Connect interface to connect to services in the consumer VPC network, you choose an IP address from a [list of supported IP ranges](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/vpc-psc-i-setup#set-up-vpc-network) in your VPC network.
  - By default, the Cloud Router will advertise regular VPC subnets unless custom advertisement mode is configured. For more information, see [Custom advertisement](https://docs.cloud.google.com/network-connectivity/docs/router/concepts/advertised-routes#am-custom) .
  - A connection between a network attachment and a Private Service Connect interface is [transitive](https://docs.cloud.google.com/vpc/docs/about-private-service-connect-interfaces#other-networks) . Workloads in the producer VPC network can communicate with workloads that are connected to the consumer VPC network.

### Firewall rules

Private Service Connect interfaces are created and managed by a producer organization, but they are located in a consumer VPC network. For consumer-side security, we recommend firewall rules that are based on IP address ranges from the consumer VPC network. You must update firewall rules to allow the network attachment subnet access to the consumer's network. For more information, see [Limit producer-to-consumer ingress](https://docs.cloud.google.com/vpc/docs/configure-security-network-attachments#producer-to-consumer-ingress) .

### Domain name resolution

Using a Private Service Connect interface alone requires connecting to services through their internal IP addresses. This isn't a recommended practice for production systems, because IP addresses can change, leading to brittle configurations.

By implementing DNS peering, Gemini Enterprise Agent Platform producers can instead resolve and connect to services in your VPC and on-premises or multicloud networks. This is achieved by querying records from a Cloud DNS private zone within your VPC network, which ensures stable, reliable service access even if underlying IP addresses are modified.

For more information, see [Set up a private DNS peering](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/vpc-psc-i-setup#set-up-private-dns-peering) .

## What's next

  - Learn about [network attachment specifications](https://docs.cloud.google.com/vpc/docs/about-network-attachments#specifications) .
  - Try a [codelab on using Private Service Connect interfaces with Agent Platform Pipelines](https://codelabs.developers.google.com/psc-interface-pipelines) .
  - Try a [codelab on using an explicit proxy to reach non-rfc1918 endpoints with Agent Platform Pipelines](https://codelabs.developers.google.com/pipelines-psc-interface-proxy) .
