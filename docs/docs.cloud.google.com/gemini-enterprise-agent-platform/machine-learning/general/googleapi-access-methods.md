---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/googleapi-access-methods
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/googleapi-access-methods
title: About accessing the Agent Platform API
description: Learn about public and private access options for connecting to APIs in Google's production environment from within {{dynamic_data.site_values.cloud_name}} or from hybrid networks.
data_source: docs.cloud.google.com
---

Your applications can connect to APIs in Google's production environment from within Google Cloud or from hybrid (on-premises and multicloud) networks. Google Cloud offers the following public and private access options, which offer global reachability and SSL/TLS security:

1.  [Public internet access](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/googleapi-access-methods#internet) : Send traffic to `  REGION -aiplatform.googleapis.com ` .
2.  [Private Service Connect endpoints for Google APIs](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/googleapi-access-methods#psc) : Use a user-defined internal IP address such as `10.0.0.100` to access `  REGION -aiplatform.googleapis.com ` or an assigned DNS name such as `aiplatform-genai1.p.googleapis.com` .

The following diagram illustrates these access options.

![Architectural diagram of accessing Agent Platform API by public and private methods](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/images/vertex-ai-access-google-apis.png)

Some Gemini Enterprise Agent Platform service producers require you to connect to their services through [Private Service Connect endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/psc-endpoints) or [Private Service Connect interfaces](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/psc-interfaces) . These services are listed in the [Private access options for Gemini Enterprise Agent Platform](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/netsec-overview#access-methods) table.

## Choosing between regional and global Gemini Enterprise Agent Platform endpoints

The regional Gemini Enterprise Agent Platform endpoint ( `  REGION -aiplatform.googleapis.com ` ) is the standard way to access Google APIs. For applications deployed across multiple Google Cloud regions, you should strongly consider using the global endpoint ( `aiplatform.googleapis.com` ) for a consistent API call and more robust design, unless your desired model or feature is only available regionally. The benefits of using the global endpoint include the following:

  - **Model and Feature Availability** : Some of the latest, specialized, or region-specific models and features within Gemini Enterprise Agent Platform are initially, or permanently, offered only through a regional endpoint (for example, `us-central1-aiplatform.googleapis.com` ). If your application depends on one of these specific resources, you must use the regional endpoint corresponding to that resource's location. This is the primary constraint when determining your endpoint strategy.
  - **Simplification of multiregion design** : If a model supports the global endpoint, using it eliminates the need for your application to dynamically switch the API endpoint based on its current deployment region. A single, static configuration works for all regions, greatly simplifying deployment, testing, and operations.
  - Rate-limiting mitigation (avoiding `429` errors): For supported models, routing requests through the global endpoint distributes the traffic internally across Google's network to the nearest available regional service. This distribution can often help alleviate localized service congestion or regional rate limit ( `429` ) errors, leveraging Google's backbone for internal load balancing.

To check the global availability of partner models, refer to the [Global tab](https://docs.cloud.google.com/vertex-ai/generative-ai/docs/learn/locations#supported_models) in the Google Cloud model endpoint locations table, which also lists [regional locations](https://docs.cloud.google.com/vertex-ai/generative-ai/docs/learn/locations#google_model_endpoint_locations) .

## Gemini Enterprise Agent Platform Shared VPC considerations

Using a [Shared VPC](https://docs.cloud.google.com/vpc/docs/shared-vpc) is a Google Cloud best practice for establishing strong network and organizational governance. This model separates responsibilities by designating a central host project, managed by network security administrators, and multiple service projects, consumed by application teams.

This separation allows network administrators to centrally manage and enforce network security (including firewall rules, subnets, and routes) while delegating resource creation and management (for example, VMs, GKE clusters, and billing) to the service projects.

A Shared VPC unlocks a multilayered approach to segmentation by enabling the following:

  - **Administrative and billing segmentation** : Each service project (for example, "Finance-AI-Project" or "Marketing-AI-Project") has its own billing, quotas, and resource ownership. This prevents a single team from consuming the entire organization's quota and provides clear cost attribution.

  - **IAM and access segmentation** : You can apply granular Identity and Access Management (IAM) permissions at the project level, for example:
    
      - The "Finance Users" Google Group is granted the roles/aiplatform.user role only in the "Finance-AI-Project."
      - The "Marketing Users" Google Group is granted the same role only in the "Marketing-AI-Project."
      - This configuration ensures that users in the finance group can only access the Gemini Enterprise Agent Platform endpoints, models, and resources associated with their own project. They are completely isolated from the marketing team's AI workloads.

  - **API-level enforcement** : The Gemini Enterprise API endpoint itself is designed to enforce this project-based segmentation. As shown in the API call structure, the project ID is a required part of the URI:
    
        https://aiplatform.googleapis.com/v1/projects/${PROJECT_ID}/locations/global/publishers/google/models/${MODEL_ID}:streamGenerateContent

When a user makes this call, the system validates that the authenticated identity has the necessary IAM permissions for the specific `${PROJECT_ID}` provided in the URL. If the user has permissions only for "Finance-AI-Project" but attempts to call the API using the "Marketing-AI-Project" ID, the request will be denied. This approach provides a robust and scalable framework, ensuring that as your organization adopts AI, you maintain clear separation of duties, costs, and security boundaries.

## Public internet access to the Agent Platform API

If your application uses a Google service listed in the [table of supported access methods for Gemini Enterprise Agent Platform](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/netsec-overview#access-methods) as public internet, your application can access the API by performing a DNS lookup against the [service endpoint](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#service-endpoint) ( `  REGION -aiplatform.googleapis.com ` or `aiplatform.googleapis.com` ), which returns publicly routable virtual IP addresses. You can use the API from any location in the world as long as you have an internet connection. However, traffic that is sent from Google Cloud resources to those IP addresses remains within Google's network. To restrict public access to the Gemini Enterprise API, [VPC Service Controls](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/vpc-service-controls) are required.

### Private Service Connect endpoints for the Agent Platform API

With Private Service Connect, you can create private endpoints using global internal IP addresses within your VPC network. You can assign DNS names to these internal IP addresses with meaningful names like `aiplatform-genai1.p.googleapis.com` and `bigtable-adsteam.p.googleapis.com` . These names and IP addresses are internal to your VPC network and any on-premises networks that are connected to it through hybrid networking services. You can control which traffic goes to which endpoint, and can demonstrate that traffic stays within Google Cloud.

  - You can create a user-defined global Private Service Connect endpoint IP address (/32). For more information, see [IP address requirements](https://docs.cloud.google.com/vpc/docs/about-accessing-google-apis-endpoints#ip-address-requirements) .
  - You create the Private Service Connect endpoint in the same VPC network as the Cloud Router.
  - You can assign DNS names to these internal IP addresses with meaningful names like `aiplatform-prodpsc.p.googleapis.com` . For more information, see [About accessing Google APIs through endpoints](https://docs.cloud.google.com/vpc/docs/about-accessing-google-apis-endpoints) .
  - In a Shared VPC, deploy the Private Service Connect endpoint in the host project.

## Deployment considerations

Following are some important considerations that affect how you use Private Google Access and Private Service Connect to access the Agent Platform API.

### Private Google Access

As a best practice, you should [enable Private Google Access](https://docs.cloud.google.com/vpc/docs/configure-private-google-access#config-pga) on VPC subnets to allow compute resources (such as Compute Engine and GKE VM instances) that don't have external IP addresses to reach Google Cloud APIs and services (such as Gemini Enterprise Agent Platform, Cloud Storage, and BigQuery).

### IP advertisement

You must advertise the Private Google Access subnet range or the Private Service Connect endpoint IP address to on-premises and multicloud environments from the Cloud Router as a custom advertised route. For more information, see [Advertise custom IP ranges](https://docs.cloud.google.com/network-connectivity/docs/router/how-to/advertising-custom-ip) .

### Firewall rules

You must ensure that the firewall configuration of on-premises and multicloud environments allows outbound traffic from the IP addresses of Private Google Access or Private Service Connect subnets.

### DNS configuration

  - Your on-premises network must have DNS zones and records configured so that a request to `  REGION -aiplatform.googleapis.com ` or `aiplatform.googleapis.com` resolves to the [Private Google Access subnet](https://docs.cloud.google.com/vpc/docs/configure-private-google-access-hybrid#config-domain) or the [Private Service Connect endpoint](https://docs.cloud.google.com/vpc/docs/configure-private-service-connect-apis#on-premises) IP address.
  - You can create Cloud DNS managed private zones and use a Cloud DNS inbound server policy, or you can configure on-premises name servers. For example, you can use [BIND](https://wikipedia.org/wiki/BIND) or [Microsoft Active Directory DNS](https://learn.microsoft.com/windows-server/networking/dns/dns-top) .
  - If your on-premises network is connected to a VPC network, you can use Private Service Connect to access Google APIs and services from on-premises hosts using the internal IP address of the endpoint. For more information, see [Access the endpoint from on-premises hosts](https://docs.cloud.google.com/vpc/docs/configure-private-service-connect-apis#on-premises) .
