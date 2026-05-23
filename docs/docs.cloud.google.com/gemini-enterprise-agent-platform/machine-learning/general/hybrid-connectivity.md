---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/hybrid-connectivity
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/hybrid-connectivity
title: Set up connectivity from Agent Platform to other networks
description: Learn about options for extending the reach of Agent Platform services deployed with private services access.
data_source: docs.cloud.google.com
---

This document begins by outlining options for extending the reach of Agent Platform services deployed with [private services access](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/private-services-access) .

This is followed by a brief discussion of motivations for deploying the services to a [Private Service Connect endpoint](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/psc-endpoints) in case that is a better fit for your needs.

Because private services access hosts Agent Platform services in a managed network that is peered to your, make sure that you are familiar with the material at [VPC peerings](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/vpc-peering) before reading the rest of this document.

By default, the peering configuration only allows the peered Agent Platform network to reach endpoints in your local subnets. Exporting custom routes allows the producer network to reach other networks to which *your* network has static or dynamic routes.

Because [transitive peering is not supported](https://docs.cloud.google.com/vpc/docs/vpc-peering#transit-network) , connections from Agent Platform is not able to reach endpoints in other networks that are directly peered to your network, even with "Export custom routes" enabled. In the example shown in the following diagram, packets can traverse Peering Connection \#1 but not Peering Connection \#2.

![With transitive peering](https://docs.cloud.google.com/static/gemini-enterprise-agent-platform/machine-learning/general/images/transitive-peering.png)

To enable Agent Platform to reach User Network \#2, replace Peering Connection \#2 with VPN \#2 as shown in the following diagram.

![Without transitive peering](https://docs.cloud.google.com/static/gemini-enterprise-agent-platform/machine-learning/general/images/no-transitive-peering.png)

Enabling custom routes in Peering Connection \#1 allows IP packets from the Agent Platform network to reach User Network \#2.

To allow response packets from User Network \#2 to be routed back to the Agent Platform network, the return route also needs to exist in the routing table for User Network \#2. VPN routes are exchanged using Border Gateway Protocol (BGP) on Cloud Routers, we can [customize the BGP configuration](https://docs.cloud.google.com/network-connectivity/docs/router/how-to/advertising-custom-ip) in User \#1 to advertise a route to the Agent Platform network range of `10.1.0.0/16` to its peer User Network \#2.

Note that you are able to edit both sides of the VPN \#1 BGP configuration to allow the on-premises network and the Agent Platform network to learn routes to each other. Because there is no attempt to transmit forward-path packets from the Agent Platform network, nor the response packets over *sequential* peering connections with respect to any single network, none of these forwarding attempts are explicitly blocked.

## Set up Connectivity from Agent Platform to the internet

If no network is specified when launching a workload, the workload runs in a separate Google-managed producer project.

If a network is specified, the workload runs in a producer project that is peered to the consumer project.

By default, the Agent Platform network has its own route to the internet and the producer network has its own default route to the internet.

To force outbound connections from the producer network to be routed through your network, you can enable [VPC Service Controls for peerings](https://docs.cloud.google.com/sdk/gcloud/reference/beta/services/vpc-peerings/enable-vpc-service-controls) . Note that this is a separate configuration from [VPC Service Controls](https://docs.cloud.google.com/vpc-service-controls/docs/overview) .

Enabling VPC Service Controls for peerings causes the following changes in the Agent Platform network:

  - Deletes the default internet route.
  - Creates a route for destination `199.36.153.4/30` with default internet gateway next hop.
  - Creates a Cloud DNS managed private zone for `*.googleapis.com` with appropriate records to map host names to one of those four addresses.
  - Authorizes that zone for the `servicenetworking` VPC network to use.

With this change in place, you can export the default route from your network to ensure that outbound connections to the internet are routed through your VPC network. This change also lets you apply any needed policies to the outbound traffic from Agent Platform.

> **Note:** Because enabling VPC Service Controls for peerings deletes the default route in the producer project, the workload doesn't have an external IP address. This means that these connections must be routed through a NAT instance or web proxy in your VPC network to access the Internet.

You can query the state of VPC Service Controls for Peerings by running the following command;

    gcloud services vpc-peerings get-vpc-service-controls \
      --network YOUR_NETWORK

This will return `enabled: true` if the configuration is enabled and empty list ( `{}` ) if it is disabled.

### Working with VPC Service Controls

If a network is specified for the workload and [VPC Service Controls](https://docs.cloud.google.com/vpc-service-controls/docs/overview) is enabled, the workload runs in a producer network that is peered to the consumer project and that is subject to the same policies as the consumer network.

If these policies block outbound traffic, then the workload similarly won't be able to reach the internet. In this case, you must follow the steps in the previous section to force outbound traffic from the workload to pass through a NAT instance in your VPC network.

## Set up Connectivity from Agent Platform using proxies

Another pattern for controlling the outbound IP from Agent Platform is to force outbound connections from workloads to go through a web proxy that you control. This also allows inspection of outbound connections for compliance.

However, using a third party proxy forces the user to manage the proxy's certificate to authentication complaints. Furthermore, these proxies may not propose a list of cipher suites that intersects with what Agent Platform SDKs and APIs expect.

Google Cloud now offers a [Secure Web Proxy](https://docs.cloud.google.com/secure-web-proxy/docs/overview) to facilitate this pattern. You may now follow the [Deploy a Secure Web Proxy instance](https://docs.cloud.google.com/secure-web-proxy/docs/quickstart) quickstart guide and adapt your workloads to use that for outbounding connections. These connections will appear to originate from the proxy's source IP address.

> **Note:** Pipeline components require the [KFP library](https://pypi.org/project/kfp/) to start.

If the KFP library isn't already installed in the component image, the pipeline tries to install it *before* running any code in which you might have specified a proxy.

If the pipeline depends on the proxy to install packages from the internet, this attempt will fail and you might see an error like the following:

    Could not find a version that satisfies the requirement kfp==2.7.0

In cases such as this, when you're unable to install KFP before running your code, you must use an image with KFP already installed.

You may add KFP to any base image and push it to your repository.

The following Dockerfile example adds KFP to the `python:3.8` base image.

    FROM python:3.8
    RUN pip install kfp==2.7.0

You can then configure the pipeline `@component` to use this image:

    @component(base_image="$PATH_TO_YOUR_REPOSITORY:YOUR_IMAGE")

Once the pipeline component is running, your code can freely install other packages by going through the proxy. The following example installs `numpy` using a proxy at `https://10.10.10.10:443` .

    import subprocess
    subprocess.call(['pip', 'install', '--proxy', 'https://10.10.10.10:443', 'numpy'])`

## Set up allowlists for API access

For transactions between Gemini Enterprise Agent Platform workloads and Google APIs, you must allow access from the workloads to the IP ranges used by Google APIs. For this, you may run the provided [script to return IP addresses for default domains](https://docs.cloud.google.com/vpc/docs/access-apis-external-ip#ip-addr-defaults) .

## Providing hybrid connectivity with Private Service Connect

Deploying Agent Platform services with [private services access](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/private-services-access) has several limitations.

  - You might need to [reserve large pools of private IP addresses](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/using-private-ip#reserving-ip-ranges) per workload while also avoiding conflicts with your VPC addressing.
      - Running multiple workloads in parallel might still cause a [RANGES\_EXHAUSTED](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/troubleshooting?component=any#ranges_exhausted_ranges_not_reserved) even after correct initial configuration.
  - Networking deployment and troubleshooting complexity:
      - Because transitive peering is not supported, you need to deploy complex workarounds to grant connectivity between different networks peered to your VPC network.
      - The state of the routing table in the producer environment is not immediately obvious. Because you don't have access to the tenant project, it is often difficult to determine what targets a Agent Platform workload can actually reach without extensive testing.

An alternative pattern is to deploy these services to a [Private Service Connect endpoint](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/psc-endpoints) .

  - The service consumes a single IP address within your VPC network, allowing you to preserve private address space for your own use.
  - Because the Agent Platform service IP is in your own network, it is simpler to [create and run connectivity Tests](https://docs.cloud.google.com/network-intelligence-center/docs/connectivity-tests/how-to/running-connectivity-tests) to assess it's reachability to and from elsewhere in your environment.
