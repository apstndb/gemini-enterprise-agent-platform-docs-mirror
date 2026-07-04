---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/vpc-service-controls
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/vpc-service-controls
title: VPC Service Controls with Gemini Enterprise Agent Platform
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

[VPC Service Controls](https://docs.cloud.google.com/vpc-service-controls/docs/overview) can help you mitigate the risk of data exfiltration from Gemini Enterprise Agent Platform. Use VPC Service Controls to create a *service perimeter* that protects the resources and data that you specify. For example, when you use VPC Service Controls to protect Agent Platform, the following artifacts can't leave your service perimeter:

  - Training data for an AutoML model or custom model
  - Models that you created
  - Models that you searched by using Neural Architecture Search on Agent Platform
  - Requests for online inferences
  - Results from a batch inference request
  - Gemini models

## Controlling access to Google APIs

Agent Platform APIs, as outlined in [Accessing Gemini Enterprise Agent Platform from on-premises and multicloud](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/netsec-overview#support-table) , encompass a range of accessibility options, including public internet, Private Service Connect for Google APIs, and Private Google Access.

### Public access

By default, these public APIs are reachable from the internet; however, IAM permissions are required for use. While features like Private Service Connect for Google APIs and Private Google Access facilitate private communication over hybrid network architectures, they don't eliminate public internet accessibility for Agent Platform APIs.

To establish granular control over API access and explicitly restrict public internet exposure, the implementation of VPC Service Controls becomes essential. When you establish a VPC Service Controls (VPC-SC) perimeter and include the Gemini Enterprise in its protected services, all public internet access to your Agent Platform instance is automatically blocked. As a result, users attempting to access Agent Platform services programmatically or using the Google Google Cloud console are denied access unless they are included in an allowlist.

To restore access for authorized sources outside the perimeter (for example, users in your corporate offices), see [Allow public endpoint access to protected resources from outside a VPC Service Controls perimeter](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/vpcsc-public-endpoint#select_the_access_level) for deployment instructions.

### Private access

Organizations that need to restrict public Google APIs to private access can use VPC Service Controls in combination with Private Service Connect for Google APIs (VPC Service Controls bundle) or Private Google Access. When deployed over hybrid networking and within Google Cloud, both options enable private access to Google APIs from on-premises. However, Private Service Connect for Google APIs also offers flexibility in defining a custom IP address and DNS endpoint name.

As a best practice, use the restricted Virtual IP (VIP) with Private Service Connect for Google APIs or Private Google Access to provide a private network route for requests to Google Cloud services without exposing the requests to the internet. The restricted VIP supports all of the APIs that VPC Service Controls can protect that require considerations for on-premises and VPC networks. Following are some examples:

  - [Allow multicloud access to protected resources from private endpoint outside a VPC Service Controls perimeter](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/vpc-psc-i-multicloud-access)
  - [Learn how to use a customer PSC Google APIs endpoint](https://docs.cloud.google.com/vpc/docs/configure-private-service-connect-apis#using-endpoints) (VPC network example)
  - [On-premises network example](https://docs.cloud.google.com/vpc-service-controls/docs/private-connectivity#on-premises_network_example)

## Controlling API access through private services access

The following Agent Platform APIs deployed with private services access require additional networking configuration when implemented in an environment protected with VPC Service Controls:

  - Vector Search (index query)
  - Custom training (data plane)
  - Agent Platform Pipelines
  - Private online prediction endpoints

For example, Agent Platform Pipelines is a Google-managed (producer) service, deployed in a single-tenant project and VPC network with the ability to scale supported services based on consumer requirements. Communication between the producer and consumer networks is established with VPC Network Peering, except for internet egress, which is routed through the producer network.

In the producer network a default route exists that allows for internet egress, in addition to unrestricted access to Google APIs. Updating the producer network to support the restricted VIP requires enabling [VPC Service Controls for peerings](https://docs.cloud.google.com/sdk/gcloud/reference/services/vpc-peerings/enable-vpc-service-controls) , which performs the following actions on all [supported services](https://docs.cloud.google.com/vpc/docs/private-services-access#private-services-supported-services) deployed in your service networking producer network:

  - Removes the IPv4 default route (destination `0.0.0.0/0` , next hop default internet gateway).
  - Creates Cloud DNS-managed private zones and authorizes those zones for the service producer VPC network. The zones include `googleapis.com` , `pkg.dev` , `gcr.io` , and other necessary domains or host names for Google APIs and services that are compatible with VPC Service Controls.
  - Record data in the zones resolves all host names to `199.36.153.4` , `199.36.153.5` , `199.36.153.6` , and `199.36.153.7` .

An alternate method for removing the default route from the producer network without impacting existing Google-managed services is to use [HA VPN over Cloud Interconnect](https://cloud.google.com/architecture/ccn-distributed-apps-design/connectivity#inter-vpc-connectivity-for-centralized-services) consisting of the following steps:

1.  Deploy a services VPC network in addition with HA VPN to the consumer VPC network.
2.  Deploy Google-managed services in the services VPC network.
3.  Enable [VPC Service Controls for peerings](https://docs.cloud.google.com/sdk/gcloud/reference/services/vpc-peerings/enable-vpc-service-controls) .
4.  Advertise the private services access subnet as a [custom route advertisement](https://docs.cloud.google.com/network-connectivity/docs/router/how-to/advertising-custom-ip) from the Cloud Router if the managed services requires on-premises reachability.
5.  Update the service networking VPC network peering with the [export custom routes](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/vpc-peering#export-custom-routes) option.

## VPC Service Controls support for Generative AI tuning pipelines

VPC Service Controls support is provided in the tuning pipeline of the following models:

  - `text-bison for PaLM 2`
  - `BERT`
  - `T5`
  - The `textembedding-gecko` family of models.

## Using VPC Service Controls with Gemini Enterprise Agent Platform Pipelines

The service perimeter blocks access from Agent Platform to third-party APIs and services on the internet. If you're using [Google Cloud Pipeline components or creating your own custom pipeline components](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/pipelines/introduction#pipeline-component) for use with Agent Platform Pipelines, you can't install PyPI dependencies from the public [Python Package Index (PyPI) registry](https://pypi.org/) . Instead, you must do one of the following:

  - [Use custom containers](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/vpc-service-controls#use-custom-containers) .
  - [Install packages from an Artifact Registry repository](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/vpc-service-controls#install-packages-ar-repo) .

### Use custom containers

As a production software best practice, component authors should use containerized Python components and build the dependencies into their container image, so no live installation is required during a pipeline run. One way to do this is as follows:

1.  Build your own container image with Kubeflow Pipelines SDK and other packages pre-installed. For example, you can use `us-docker.pkg.dev/vertex-ai/training/tf-cpu.2-17:latest` as the base layer of your image and add an extra layer to install the packages at container build time.

2.  Update your component definition code to set the `base_image` path and the `install_kfp_package` flag to `False` . This flag instructs the KFP compiler not to inject a pip install kfp command into the container command line, because the Kubeflow Pipelines SDK package is already installed in the image. For example:
    
        @component(
            base_image='gcr.io/deeplearning-platform-release/tf-cpu.2-17',
            install_kfp_package=False,
        )
        def my_component(...):
            ...

### Install packages from an Artifact Registry repository

Alternatively, you can create an Artifact Registry repository in your project, store Python packages in it, and configure your Agent Platform environment to install from it as outlined in this section. For more information, see [Manage Python packages](https://docs.cloud.google.com/artifact-registry/docs/python/manage-packages#additional_information) .

#### Configure roles and permissions

1.  The service account for your Agent Platform environment must have the `iam.serviceAccountUser` role.
2.  If you install custom PyPI packages from a repository in your project's network, and this repository does not have a public IP address:
    1.  Assign permissions to access this repository to the environment's service account.
    2.  Make sure that connectivity to this repository is configured in your project.

#### Create the repository

1.  [Create an Artifact Registry repository in VPC mode](https://docs.cloud.google.com/artifact-registry/docs/securing-with-vpc-sc#ar-vpc) in your project.
2.  Store the required Python packages in the repository.

#### Configure the Agent Platform environment to install from the repository

To install custom PyPI packages from one or more Artifact Registry repositories, make a call similar to the following to `@dsl.component` :

    @dsl.component(packages_to_install=["tensorflow"],
    pip_index_urls=['https://us-central1-python.pkg.dev/mygcpproject1/pypi-repo1/simple', 'https://us-central1-python.pkg.dev/mygcpproject2/pypi-repo2/simple'],)
    def hello_world(text: str) -> str:
        import my_package
        import tensorflow
    
        return my_package.hello_world(text)

## Using VPC Service Controls with PSC Interface

The following Agent Platform APIs deployed with private services connect interface require additional networking configuration when implemented in an environment protected with VPC Service Controls:

  - Custom training (data plane)
  - Agent Platform Pipelines
  - Private online inference endpoints
  - Agent Runtime

Agent Platform producers' service ability to access the public internet depends on your project's security configuration, specifically whether or not you are using VPC Service Controls:

  - **Without VPC Service Controls** : The Google-managed tenant hosting Agent Platform retains its default internet access. This outbound traffic egresses directly from the secure, Google-managed environment where your producer service runs. The exception to this behavior is Agent Runtime, which doesn't provide internet egress. Instead, you're required to deploy a proxy VM with an RFC 1918 address for internet egress.

  - **With VPC Service Controls** : When your project is enclosed in a VPC Service Controls (VPC-SC) perimeter, the Google-managed environment hosting Agent Platform has its default internet access blocked. This restriction is a security measure designed to prevent data exfiltration. To enable Agent Platform to access the public internet in this scenario, you must explicitly configure a secure egress path that routes the traffic through your VPC network.

The recommended method involves:

1.  Deploying a proxy server inside your VPC perimeter within an RFC 1918 subnet.
2.  Creating a Cloud NAT gateway to allow the proxy VM to reach the internet.
3.  Defining the proxy server (IP address or FQDN) in your runtime environment.

There is no prescribed or preferred network proxy for this task. You may use any suitable solution. Examples include: [Squid proxy](http://www.squid-cache.org/) , [HAProxy](https://www.haproxy.com/) , [Envoy](https://www.envoyproxy.io/) , and [TinyProxy](https://tinyproxy.github.io/) .

## Service perimeter creation

For an overview of creating a service perimeter, see [Create a service perimeter](https://docs.cloud.google.com/vpc-service-controls/docs/create-service-perimeters) in the VPC Service Controls documentation.

### Adding restricted services to your perimeter

When establishing a service perimeter, we recommend that you include all restricted services as a [security best practice](https://docs.cloud.google.com/vpc-service-controls/docs/enable) . This comprehensive approach helps to minimize potential vulnerabilities and unauthorized access. However, there might be scenarios where your organization has specific requirements focused on safeguarding Gemini Enterprise Agent Platform and its interconnected APIs. In such cases, you have the flexibility to select and include only the specific Agent Platform APIs that are essential for your operations.

Agent Platform APIs that you can incorporate into your service perimeter include the following:

  - [Gemini Enterprise Agent Platform](https://docs.cloud.google.com/vpc-service-controls/docs/supported-products#table_agent_platform) supports the following services and features:
      - Batch inference
      - Datasets
      - Agent Platform Feature Store (Bigtable online serving)
      - Agent Platform Feature Store (optimized online serving) ( [Deprecated](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/deprecations) )
      - Generative AI on Gemini Enterprise Agent Platform (Gemini)
      - Model Registry
      - Online inference
      - Open model tuning
      - Vector Search (index creation)
      - Vector Search (index query)
      - Custom training (control plane)
      - Custom training (data plane)
      - Agent Platform Pipelines
      - Private online inference endpoints
      - Colab Enterprise
      - Agent Runtime
      - Managed training clusters
  - [Notebooks API](https://docs.cloud.google.com/vpc-service-controls/docs/supported-products#table_notebooks) supports the following service:
      - Gemini Enterprise Agent Platform Workbench

## Limitations

The following limitations apply when you use VPC Service Controls:

  - URL context live fetching is disabled for VPC-SC projects so that the data exfiltration is blocked.
  - For data labeling, you must add labelers' IP addresses to an [access level](https://docs.cloud.google.com/vpc-service-controls/docs/use-access-levels) .
  - For Google Cloud Pipeline Components, the components launch containers that check their base image for all requirements. The KFP package, as well as any packages listed in the `packages_to_install` argument are the requirements for a container. If any specified requirements aren't already present in the base image (either provided or custom), the component attempts to download them from the [Python Package Index (PyPI)](https://pypi.org/) . Because the service perimeter blocks access from Gemini Enterprise Agent Platform to third-party APIs and services on the internet, the download fails with `Connection to pypi.org timed out` . For ways to avoid this error, see [Using VPC Service Controls with Agent Platform Pipelines](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/vpc-service-controls#vpcsc-agent-platform-pipelines) .
  - When using VPC Service Controls with custom kernels in Agent Platform Workbench, you must instead configure DNS peering to send requests for `*.notebooks.googleusercontent.com` to the subnet 199.36.153.8/30 ( `private.googleapis.com` ) instead of 199.36.153.4/30 ( `restricted.googleapis.com` ).
  - When using VPC Service Controls with Gemini Enterprise Agent Platform Inference, endpoints must be created after the project is added to the service perimeter. If an endpoint is created in a project that is not part of a service perimeter, and afterward that project is added to a service perimeter, then attempting to deploy a model to that endpoint will fail. If the endpoint is a [shared public endpoint](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/choose-endpoint-type) then sending a request to the endpoint will fail as well. Similarly attempting to deploy a model to an endpoint will fail if the endpoint was created in a project that was part of a service perimeter, and afterward the project is removed.
  - When using VPC Service Controls with Agent Runtime, the project must be part of a service perimeter before you deploy the agent. If an agent is deployed before the project is added to a perimeter, the agent won't be secured by VPC Service Controls and continues to have access to the public internet.
  - Model Garden 1-click public (dedicated endpoint) deployments aren't supported within a VPC-SC environment. Instead, use a [private endpoint](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/choose-endpoint-type) that supports VPC Service Controls. For more information, see [Deploy a model to a private endpoint](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/model-garden/use-models#deploy_a_model_to_a_private_endpoint) .
  - [Request and response logging](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/capabilities/request-response-logging) isn't available with VPC Service Controls.

## What's next

  - Watch the [VPC Service Controls: How to segment your cloud projects in shared VPC](https://www.youtube.com/watch?v=ASR7xF5jAys) video.
  - Watch the [How to use dry run mode in VPC Service Controls](https://www.youtube.com/watch?v=_l-ei3ZlgWc) video.
  - Watch the [VPC Service Controls: Private IP support to create granular access controls](https://youtu.be/5MmVyXtQji8) video.
  - Learn more about [VPC Service Controls](https://docs.cloud.google.com/vpc-service-controls/docs/overview) .
  - Learn more about [VPC Service Controls required roles](https://docs.cloud.google.com/vpc-service-controls/docs/access-control#required_roles) .
  - Learn about [troubleshooting VPC Service Controls issues](https://docs.cloud.google.com/vpc-service-controls/docs/troubleshooting) .
  - Learn about [deploying a proxy VM to access the internet from the customer's VPC](https://codelabs.developers.google.com/agent-engine-psc-interface-private#0) .
