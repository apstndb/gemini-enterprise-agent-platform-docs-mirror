---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/vpcsc-separate-perimeters
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/vpcsc-separate-perimeters
title: Allow access to protected resources from private endpoint inside a VPC Service Controls perimeter
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

In Shared VPC architectures, the host project's network is shared with the service project. Until recently, this prevented separating these projects into different perimeters. With the introduction of private IP address-based ingress and egress rules, host and service projects can now reside in separate perimeters while maintaining controlled access through these rules.

## Reference architecture

The following attributes are used in the service policy:

  - VPC Service Controls perimeters
  - Access Context Manager private IP addresses
  - Ingress and egress rules

In the networking component, this architecture uses a [Private Service Connect endpoint](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/googleapi-access-methods#psc) to access Google APIs.

![Architectural diagram of using VPC Service Controls to create a service perimeter.](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/images/vertex-vpcsc-cuj3.png)

In this reference architecture, ingress and egress rules and private IP addresses are used to control access between Compute Engine instances and the Agent Platform API for the following service perimeters and projects:

| Perimeter                  | Projects inside perimeter                     |
| -------------------------- | --------------------------------------------- |
| `aiml-host-perimeter`      | `aiml-host-project`                           |
| `high-trust-svc-perimeter` | `ph-fm-svc-project-1`                         |
| `low-trust-svc-perimeter`  | `ph-fm-svc-project-2` , `ph-fm-svc-project-3` |

Access to the Agent Platform API from each service project's own Compute Engine instances is controlled by VPC Service Controls ingress and egress rules. These rules use Access Context Manager access levels that are configured with private IP addresses to allow the subnets shared with each service project access to their respective perimeters.

## Optional: Create an access level for organizational public traffic

If your end users require access to Gemini Enterprise Agent Platform through the Google Cloud console, follow the instructions in this section to create an access level for use in VPC Service Controls. However, if access to APIs is strictly programmatic from private sources (such as on premises with [Private Google Access for on-premises](https://docs.cloud.google.com/vpc/docs/configure-private-google-access-hybrid) or Cloud Workstations), then the access level is not required.

In this reference architecture we're using a CIDR range, `corp-public-block` , to allow organization employee traffic to access Google Cloud console.

Access Context Manager allows Google Cloud organization administrators to define fine-grained, attribute-based access control for resources in Google Cloud.

Access levels describe the requirements for requests to be honored. Examples include:

  - Device type and operating system (requires a Chrome Enterprise Premium license)
  - IP address
  - Geolocations
  - User identity

If this is the organization's first time using Access Context Manager, its administrators must define an [access policy](https://docs.cloud.google.com/access-context-manager/docs/overview#access-policies) , which is a container for [access levels](https://docs.cloud.google.com/access-context-manager/docs/overview#access-levels) and service perimeters. This is done as follows:

1.  In the project selector at the top of the Google Cloud console, click the **All** tab, and then select your organization.
2.  Create a basic access level by following the directions in the [Create a basic access level](https://docs.cloud.google.com/access-context-manager/docs/create-basic-access-level) page. Specify the following options:
    1.  Under **Create conditions in** , choose **Basic mode** .
    2.  In the **Access level title** field, enter `corp-public-block` .
    3.  In the **Conditions** section, for **When condition is met, return** option, choose **TRUE** .
    4.  Under **IP Subnetworks** , choose **Public IP** .
    5.  For the IP address range, specify your external CIDR range that requires access into the VPC Service Controls perimeter.

## Build the VPC Service Controls service perimeter

When you [create a service perimeter](https://docs.cloud.google.com/vpc-service-controls/docs/create-service-perimeters) , one way that you can allow access to protected services from outside the perimeter is by creating access levels (using IP addresses, in our example). In this reference architecture, multiple services perimeters are created that use ingress and egress rules to control access to Agent Platform API and Compute Engine API communication as follows:

  - The subnet for compute resources belonging to service project `ph-fm-svc-project-1` is allowed access to the Agent Platform API and Compute Engine API in `ph-fm-svc-project-1` from the `aiml-host-project` .
  - The subnet for compute resources belonging to service projects `ph-fm-svc-project-2` and `ph-fm-svc-project-3` are allowed access to the Agent Platform API and Compute Engine API in project `ph-fm-svc-project-2` and project `ph-fm-svc-project-3` from the `aiml-host-project` .

Each service project is allowed access to the Compute Engine API in the host project (because bidirectional flows occur between the host project and service projects when compute resources are created in a given service project).

In this reference architecture, an access level for each subnet is created to use ingress and egress rules to permit the required flows between the host project perimeter and each service project perimeter.

### Create access level `gce-subnet-1`

1.  In the project selector at the top of the Google Cloud console, click the **All** tab, and then select your organization.
2.  Create a basic access level by following the directions in the [Create a basic access level](https://docs.cloud.google.com/access-context-manager/docs/create-basic-access-level) page. Specify the following options:
    1.  Under **Create conditions in** , choose **Basic mode** .
    2.  In the **Access level title** field, enter `gce-subnet-1` .
    3.  In the **Conditions** section, for **When condition is met, return** option, choose **TRUE** .
    4.  Under **IP Subnetworks** , choose **Private IP** .
    5.  Select **VPC Networks** , identify your **project** , and select your **VPC name** .
    6.  For the **IP Subnetworks** , select your CIDR range representing the subnet that the host project shared with `ph-fm-svc-project-1` .

### Create access level `gce-subnet-2`

1.  In the project selector at the top of the Google Cloud console, click the **All** tab, and then select your organization.
2.  Create a basic access level by following the directions in the [Create a basic access level](https://docs.cloud.google.com/access-context-manager/docs/create-basic-access-level) page. Specify the following options:
    1.  Under **Create conditions in** , choose **Basic mode** .
    2.  In the **Access level title** field, enter `gce-subnet-2` .
    3.  In the **Conditions** section, for **When condition is met, return** option, choose **TRUE** .
    4.  Under **IP Subnetworks** , choose **Private IP** .
    5.  Select **VPC Networks** , identify your **project** , and select your **VPC name** .
    6.  For the **IP Subnetworks** , select your CIDR range representing the subnet that the host project shared with `ph-fm-svc-project-2` .

### Create access level `gce-subnet-3`

1.  In the project selector at the top of the Google Cloud console, click the **All** tab, and then select your organization.
2.  Create a basic access level by following the directions in the [Create a basic access level](https://docs.cloud.google.com/access-context-manager/docs/create-basic-access-level) page. Specify the following options:
    1.  Under **Create conditions in** , choose **Basic mode** .
    2.  In the **Access level title** field, enter `gce-subnet-3` .
    3.  In the **Conditions** section, for **When condition is met, return** option, choose **TRUE** .
    4.  Under **IP Subnetworks** , choose **Private IP** .
    5.  Select **VPC Networks** , identify your **project** , and select your **VPC name** .
    6.  For the **IP Subnetworks** , select your CIDR range representing the subnet that the host project shared with `ph-fm-svc-project-3` .

## Configuration steps for `aiml-host-perimeter`

### Select the configuration type for the new perimeter

In this section, you create a VPC Service Controls ( `aiml-host-perimeter` ) service perimeter in [dry run mode](https://docs.cloud.google.com/vpc-service-controls/docs/service-perimeters#dry-run-mode) . In dry run mode, the perimeter logs violations as though the perimeters are enforced but doesn't prevent access to restricted services. Using dry run mode before switching to enforced mode is recommended as a best practice.

1.  In the Google Cloud console navigation menu, click **Security** , and then click **VPC Service Controls** .

2.  If prompted, select your organization, folder, or project.

3.  On the **VPC Service Controls** page, click **Dry run mode** .

4.  Click **New perimeter** .

5.  On the **New VPC Service Perimeter** tab, in the **Perimeter Name** box, type a name for the perimeter, for example, `aiml-host-perimeter` .
    
    A perimeter name can have a maximum length of 50 characters, must start with a letter, and can contain only ASCII Latin letters ( `a-z` , `A-Z` ), numbers ( `0-9` ), and underscores ( `_` ). The perimeter name is case-sensitive and must be unique within an access policy.

6.  Accept the default settings for the perimeter.

### Select the resources to protect

1.  Click **Resources to protect** .
2.  To add projects or VPC networks that you want to secure within the perimeter, do the following:
    1.  Click **Add Resources** .
    2.  To add projects to the perimeter, in the **Add resources** pane, click **Add project** .
        1.  Select the project you want to add, in this case `aiml-host-project` .
        2.  Click **Add selected resources** . The added projects appear in the **Projects** section.

### Select the restricted services

In this reference architecture, the scope of restricted APIs is limited, enabling only the necessary APIs required for Gemini Enterprise Agent Platform. However, as a best practice, we recommend that you restrict all services when you create a perimeter to mitigate the risk of data exfiltration from Google Cloud services.

> **Note:** This example shows a pattern for a basic Gemini Enterprise Agent Platform implementation. If you're using additional Gemini Enterprise Agent Platform or Gemini services, add those services to the list of restricted services.

To select the services to secure within the perimeter, do the following:

1.  Click **Restricted Services** .
2.  In the **Restricted Services** pane, click **Add services** .
3.  In the **Specify services to restrict** dialog, select Compute Engine API.
4.  Click **Add Compute Engine API** .

### Optional: Select the VPC accessible services

The **VPC accessible services** setting limits the set of services that are accessible from network endpoints inside your service perimeter. In this reference architecture, we're keeping the default setting of **All Services** .

### Optional: Select the access level

If you created a corporate CIDR access level in an earlier section, do the following to allow access to protected resources from outside the perimeter:

1.  Click **Access Levels** .

2.  Click the **Choose Access Level** box.
    
    You can also [add access levels](https://docs.cloud.google.com/vpc-service-controls/docs/manage-service-perimeters#add-access-level) after a perimeter has been created.

3.  Select the checkbox corresponding to the access level. (In this reference architecture, this is `corp-public-block` .)

### Configure the ingress policy

Bidirectional communication happens between a host project and a service project when compute resources are created in a given service project, because the host project owns the VPC network containing the subnet that is shared with the service project. In this section, you configure an ingress rule that permits all three service projects access to compute resources in the host project for these flows.

1.  In the left menu, click **Ingress policy** .
2.  Click **Add rule** .
3.  In the **Ingress rule** pane, do the following:
    1.  For **FROM attributes** , select the following FROM attributes of the API client:
        1.  **Identity** : Any identity
        2.  **Source** : Projects ( `ph-fm-svc-project-1` , `ph-fm-svc-project-2` , `ph-fm-svc-project-3` )
    2.  For **TO attributes** , select the following TO attributes of Google Cloud services and resources:
        1.  **Project** : All projects
        2.  **Services** : Selected services
        3.  **Selected services** : Compute Engine API
        4.  **Methods** : All methods

### Configure the egress policy

In this section, you configure two egress rules.

#### First egress rule

Because the host project owns the subnet shared with `ph-fm-svc-project-1` , an egress rule is required to permit that subnet to access the perimeter of `ph-fm-svc-project-1` from the host project's perimeter. The corporate access level enables the bidirectional communication required for compute instance creation when an end user creates compute resources in a service project using the configured access level.

1.  In the left menu, click **Egress policy** .
2.  Click **Add rule** .
3.  In the **Egress rule** pane, do the following:
    1.  For **FROM attributes** , select the following FROM attributes of the API client:
        1.  **Identity** : Any identity
        2.  Select **Enable access level egress sources** .
        3.  **Access levels** `corp-public-block` and `gce-subnet-1` .
    2.  For **TO attributes** , select the following TO attributes of Google Cloud services and resources:
        1.  **Project** : Selected projects
        2.  **Add project** : `ph-fm-svc-project-1`
        3.  **Services** : All services

#### Second egress rule

Because the host project owns the subnets shared with `ph-fm-svc-project-2` and `ph-fm-svc-project-3` , an egress rule is required to permit those subnets to access the service projects' perimeter from the host project's perimeter. The corporate access level enables bidirectional communication required for compute instance creation when an end user creates compute resources in a service project using the configured access level.

1.  In the left menu, click **Egress policy** .
2.  Click **Add rule** .
3.  In the **Egress rule** pane, do the following:
    1.  For **FROM attributes** , select the following FROM attributes of the API client:
        1.  **Identity** : Any identity
        2.  Select **Enable access level egress sources** .
        3.  **Access levels** `corp-public-block` , `gce-subnet-2` , and `gce-subnet-3` .
    2.  For **TO attributes** , select the following TO attributes of Google Cloud services and resources:
        1.  **Project** : Selected projects
        2.  **Add project** : `ph-fm-svc-project-2` , `ph-fm-svc-project-3`
        3.  **Services** : All services

### Create the perimeter

Once you have completed the preceding configuration steps, create the perimeter by clicking **Create perimeter** .

## Configuration steps for `high-trust-svc-perimeter`

### Select the configuration type for the new perimeter

1.  In the Google Cloud console navigation menu, click **Security** , and then click **VPC Service Controls** .

2.  If prompted, select your organization, folder, or project.

3.  On the **VPC Service Controls** page, click **Dry run mode** .

4.  Click **New perimeter** .

5.  On the **New VPC Service Perimeter** tab, in the **Perimeter Name** box, type a name for the perimeter, for example, `high-trust-svc-perimeter` .
    
    A perimeter name can have a maximum length of 50 characters, must start with a letter, and can contain only ASCII Latin letters ( `a-z` , `A-Z` ), numbers ( `0-9` ), and underscores ( `_` ). The perimeter name is case-sensitive and must be unique within an access policy.

6.  Accept the default settings for the perimeter.

### Select the resources to protect

1.  Click **Resources to protect** .
2.  To add projects or VPC networks that you want to secure within the perimeter, do the following:
    1.  Click **Add Resources** .
    2.  To add projects to the perimeter, in the **Add resources** pane, click **Add project** .
        1.  Select the project you want to add, in this case `ph-fm-svc-project-1` .
        2.  Click **Add selected resources** . The added projects appear in the **Projects** section.

### Select the restricted services

In this reference architecture, the scope of restricted APIs is limited, enabling only the necessary APIs required for Gemini. However, as a best practice, we recommend that you restrict all services when you create a perimeter to mitigate the risk of data exfiltration from Google Cloud services.

> **Note:** This example shows a pattern for a basic Gemini Enterprise Agent Platform implementation. If you're using additional Gemini Enterprise Agent Platform or Gemini services, add those services to the list of restricted services.

To select the services to secure within the perimeter, do the following:

1.  Click **Restricted Services** .
2.  In the **Restricted Services** pane, click **Add services** .
3.  In the **Specify services to restrict** dialog, select Compute Engine API.
4.  Click **Add Compute Engine API** .
5.  In the **Restricted Services** pane, click **Add services** .
6.  In the **Specify services to restrict** dialog, select Agent Platform API.
7.  Click **Add Agent Platform API** .

### Optional: Select the VPC accessible services

The **VPC accessible services** setting limits the set of services that are accessible from network endpoints inside your service perimeter. In this reference architecture, we're keeping the default setting of **All Services** .

### Optional: Select the access level

If you created a corporate CIDR access level in an earlier section, do the following to allow access to protected resources from outside the perimeter:

1.  Click **Access Levels** .

2.  Click the **Choose Access Level** box.
    
    You can also [add access levels](https://docs.cloud.google.com/vpc-service-controls/docs/manage-service-perimeters#add-access-level) after a perimeter has been created.

3.  Select the checkbox corresponding to the access level. (In this reference architecture, this is `corp-public-block` .)

### Configure the ingress policy

Because the host project owns the subnet shared with `ph-fm-svc-project-1` , an ingress rule is required to permit that subnet access to `ph-fm-svc-project-1` 's perimeter from the host project. This enables `ph-fm-svc-project-1` 's compute instances to access managed service within `ph-fm-svc-project-1` .

1.  In the left menu, click **Ingress policy** .
2.  Click **Add rule** .
3.  In the **Ingress rule** pane, do the following:
    1.  For **FROM attributes** , select the following FROM attributes of the API client:
        1.  **Identity** : Any identity
        2.  **Source** : Access level
        3.  **Access level** : `gce-subnet-1`
    2.  For **TO attributes** , select the following TO attributes of Google Cloud services and resources:
        1.  **Project** : All projects
        2.  **Services** : All services

### Configure the egress policy

Because the host project owns the subnet shared with `ph-fm-svc-project-1` , an egress rule is required to permit the bidirectional communication that happens between the service project and its host project when compute resources are created in the service project.

1.  In the left menu, click **Egress policy** .
2.  Click **Add rule** .
3.  In the **Egress rule** pane, do the following:
    1.  For **FROM attributes** , select the following FROM attributes of the API client:
        1.  **Identity** : Any identity
    2.  For **TO attributes** , select the following TO attributes of Google Cloud services and resources:
        1.  **Project** : Selected projects
        2.  **Add project** : `aiml-host-project`
        3.  **Services** : Selected services
        4.  **Selected services** : Compute Engine API
        5.  **Methods** : All methods

### Create the perimeter

Once you have completed the preceding configuration steps, create the perimeter by clicking **Create perimeter** .

## Configuration steps for `low-trust-svc-perimeter`

### Select the configuration type for the new perimeter

1.  In the Google Cloud console navigation menu, click **Security** , and then click **VPC Service Controls** .

2.  If prompted, select your organization, folder, or project.

3.  On the **VPC Service Controls** page, click **Dry run mode** .

4.  Click **New perimeter** .

5.  On the **New VPC Service Perimeter** tab, in the **Perimeter Name** box, type a name for the perimeter, for example, `low-trust-svc-perimeter` .
    
    A perimeter name can have a maximum length of 50 characters, must start with a letter, and can contain only ASCII Latin letters ( `a-z` , `A-Z` ), numbers ( `0-9` ), and underscores ( `_` ). The perimeter name is case-sensitive and must be unique within an access policy.

6.  Accept the default settings for the perimeter.

### Select the resources to protect

1.  Click **Resources to protect** .
2.  To add projects or VPC networks that you want to secure within the perimeter, do the following:
    1.  Click **Add Resources** .
    2.  To add projects to the perimeter, in the **Add resources** pane, click **Add project** .
        1.  Select the project you want to add. For this reference architecture, choose the following:
              - `ph-fm-svc-project-2`
              - `ph-fm-svc-project-3`
        2.  Click **Add selected resources** . The added projects appear in the **Projects** section.

### Select the restricted services

In this reference architecture, the scope of restricted APIs is limited, enabling only the necessary APIs required for Gemini. However, as a best practice, we recommend that you restrict all services when you create a perimeter to mitigate the risk of data exfiltration from Google Cloud services.

> **Note:** This example shows a pattern for a basic Gemini Enterprise Agent Platform implementation. If you're using additional Gemini Enterprise Agent Platform or Gemini services, add those services to the list of restricted services.

To select the services to secure within the perimeter, do the following:

1.  Click **Restricted Services** .
2.  In the **Restricted Services** pane, click **Add services** .
3.  In the **Specify services to restrict** dialog, select Compute Engine API.
4.  Click **Add Compute Engine API** .
5.  In the **Restricted Services** pane, click **Add services** .
6.  In the **Specify services to restrict** dialog, select Agent Platform API.
7.  Click **Add Agent Platform API** .

### Optional: Select the VPC accessible services

The **VPC accessible services** setting limits the set of services that are accessible from network endpoints inside your service perimeter. In this reference architecture, we're keeping the default setting of **All Services** .

### Optional: Select the access level

If you created a corporate CIDR access level in an earlier section, do the following to allow access to protected resources from outside the perimeter:

1.  Click **Access Levels** .

2.  Click the **Choose Access Level** box.
    
    You can also [add access levels](https://docs.cloud.google.com/vpc-service-controls/docs/manage-service-perimeters#add-access-level) after a perimeter has been created.

3.  Select the checkbox corresponding to the access level. (In this reference architecture, this is `corp-public-block` .)

### Configure the ingress policy

Because the host project owns the subnet shared with `ph-fm-svc-project-2` and `ph-fm-svc-project-3` , an ingress rule is required to grant those subnets access to the service project's perimeter from the host project. This enables these service projects' compute instances to access managed service within `ph-fm-svc-project-2` and `ph-fm-svc-project-3` .

1.  In the left menu, click **Ingress policy** .
2.  Click **Add rule** .
3.  In the **Ingress rule** pane, do the following:
    1.  For **FROM attributes** , select the following FROM attributes of the API client:
        1.  **Identity** : Any identity
        2.  **Source** : Access level
        3.  **Access level** : `gce-subnet-2` , `gce-subnet-3`
    2.  For **TO attributes** , select the following TO attributes of Google Cloud services and resources:
        1.  **Project** : All projects
        2.  **Services** : All services

### Configure the egress policy

Because the host project owns the subnet shared with `ph-fm-svc-project-２` and `ph-fm-svc-project-3` , an egress rule is required to permit the bidirectional communication that happens between the service projects and their host project when compute resources are created in the service projects.

1.  In the left menu, click **Egress policy** .
2.  Click **Add rule** .
3.  In the **Egress rule** pane, do the following:
    1.  For **FROM attributes** , select the following FROM attributes of the API client:
        1.  **Identity** : Any identity
    2.  For **TO attributes** , select the following TO attributes of Google Cloud services and resources:
        1.  **Project** : Selected projects
        2.  **Add project** : `aiml-host-project`
        3.  **Services** : Selected services
        4.  **Selected services** : Compute Engine API
        5.  **Methods** : All methods

### Create the perimeter

Once you have completed the preceding configuration steps, create the perimeter by clicking **Create perimeter** .

## Configure the network

### Use a Private Service Connect endpoint to access Google APIs

Private Service Connect to access Google APIs is an alternative to using Private Google Access or the public domain names for Google APIs. In this case, the producer is Google.

Using Private Service Connect lets you do the following:

  - Create one or more internal IP addresses to access Google APIs for different use cases.
  - Direct your on-premises traffic to specific IP addresses and regions when accessing Google APIs.
  - Create a custom endpoint DNS name to be used to resolve Google APIs.

In the reference architecture, a Private Service Connect Google API endpoint named `restricted` with IP address `192.168.10.2` is deployed with the target VPC Service Controls, used as a Virtual IP (VIP) to access restricted services configured in the VPC Service Controls perimeter. The Private Service Connect endpoint is deployed in the host project, `aiml-host-project` .

### Access Gemini Pro from Compute Engine instances

When you create a Private Service Connect endpoint, Service Directory creates DNS records in a [`p.googleapis.com` private zone](https://docs.cloud.google.com/vpc/docs/configure-private-service-connect-apis#configure-p-dns) . The records point to the endpoint IP address, and use the format `  SERVICE-ENDPOINT .p.googleapis.com ` that equates to the fully qualified domain name that's used to access the Agent Platform API: `  LOCATION -aiplatform-restricted.p.googleapis.com ` .

### Validate the network configuration

From the Compute Engine instances deployed in the service projects, the following procedure is used to update the Agent Platform API to use the custom fully qualified domain name and perform validation.

1.  Initialize your Python environment variables as follows:
    
        PROJECT_ID="ph-fm-svc-project-1"
        LOCATION_ID="us-central1"
        API_ENDPOINT="us-central1-aiplatform-restricted.p.googleapis.com"
        MODEL_ID="gemini-2.0-flash-exp"
        GENERATE_CONTENT_API="streamGenerateContent"

2.  Using a text editor, create a `request.json` file containing the following JSON:
    
        {
          "contents": [
            {
              "role": "user",
              "parts": [
                {
                  "text": "what weight more 1kg feathers vs 1kg stones"
                }
              ]
            }
          ],
          "generationConfig": {
            "temperature": 1,
            "maxOutputTokens": 8192,
            "topP": 0.95,
            "seed": 0
          },
          "safetySettings": [
            {
              "category": "HARM_CATEGORY_HATE_SPEECH",
              "threshold": "OFF"
            },
            {
              "category": "HARM_CATEGORY_DANGEROUS_CONTENT",
              "threshold": "OFF"
            },
            {
              "category": "HARM_CATEGORY_SEXUALLY_EXPLICIT",
              "threshold": "OFF"
            },
            {
              "category": "HARM_CATEGORY_HARASSMENT",
              "threshold": "OFF"
            }
          ]
        }

3.  Make the following cURL request to the Gemini Enterprise Agent Platform Gemini API:
    
        curl \
        -X POST \
        -H "Content-Type: application/json" \
        -H "Authorization: Bearer $(gcloud auth print-access-token)" \
        "https://${API_ENDPOINT}/v1/projects/${PROJECT_ID}/locations/${LOCATION_ID}/publishers/google/models/${MODEL_ID}:${GENERATE_CONTENT_API}" -d '@request.json'

### Validate your perimeter in dry run mode

In this reference architecture, the service perimeter is configured in dry run mode, letting you test the effect of access policy without enforcement. This means that you can see how your policies would impact your environment if they were active, but without the risk of disrupting legitimate traffic.

To learn how to validate your perimeter in dry run mode, watch the [VPC Service Controls dry run logging](https://www.google.com/url?sa=D&q=https%3A%2F%2Fwww.youtube.com%2Fwatch%3Fv%3D_l-ei3ZlgWc) YouTube video.

After validating your perimeter in dry run mode, [switch it to enforced mode](https://docs.cloud.google.com/vpc-service-controls/docs/manage-dry-run-configurations#enforce-configuration) .
