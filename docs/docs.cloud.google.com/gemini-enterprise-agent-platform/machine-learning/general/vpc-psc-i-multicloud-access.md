---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/vpc-psc-i-multicloud-access
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/vpc-psc-i-multicloud-access
title: Allow multicloud access to protected resources from private endpoint outside a VPC Service Controls perimeter
description: Learn how to enable multicloud access to protected resources from a private endpoint outside a VPC Service Controls perimeter.
data_source: docs.cloud.google.com
---

## Reference architecture

In the following reference architecture, a Shared VPC is deployed with a Gemini model in the service project, `ph-fm-svc-project` (foundation model service project) with the service policy attributes allowing private access to Agent Platform API from AWS:

  - A single VPC Service Controls perimeter
  - Project-defined user identity

![Architectural diagram of using VPC Service Controls to create a service perimeter.](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/images/vertex-vpcsc-cuj2.png)

## Optional: Create the access level

If your end users require access to Gemini Enterprise Agent Platform through the Google Cloud console, follow the instructions in this section to create a VPC Service Controls access level. However, if programmatic access to APIs is from private sources (such as on premises with Private Google Access or Cloud Workstations), then the access level is not required.

In this reference architecture we're using a corporate CIDR range, `corp-public-block` , to allow corp employee traffic to access Google Cloud console.

Access Context Manager allows Google Cloud organization administrators to define fine-grained, attribute-based access control for projects and resources in Google Cloud.

Access levels describe the requirements for requests to be honored. Examples include:

  - Device type and operating system (requires [Chrome Enterprise Premium](https://docs.cloud.google.com/chrome-enterprise-premium/docs/overview) license)
  - IP address
  - User identity

If this is the organization's first time using Access Context Manager, then administrators must define an [access policy](https://docs.cloud.google.com/access-context-manager/docs/overview#access-policies) , which is a container for [access levels](https://docs.cloud.google.com/access-context-manager/docs/overview#access-levels) and service perimeters.

1.  In the project selector at the top of the Google Cloud console, click the **All** tab, and then select your organization.

2.  Create a basic access level by following the directions in the [Create a basic access level](https://docs.cloud.google.com/access-context-manager/docs/create-basic-access-level) page. Specify the following options:
    
    1.  Under **Create conditions in** , choose **Basic mode** .
    2.  In the **Access level title** field, enter `corp-public-block` .
    3.  In the **Conditions** section, for the **When condition is met, return** option, choose **TRUE** .
    4.  Under **IP Subnetworks** , choose **Public IP** .
    5.  For the IP address range, specify your external CIDR range that requires access into the VPC Service Controls perimeter.

## Build the VPC Service Controls service perimeter

When you [create a service perimeter](https://docs.cloud.google.com/vpc-service-controls/docs/create-service-perimeters#external-access) , you allow access to protected services from outside the perimeter by specifying the protected projects. When using VPC Service Controls with Shared VPC, you create one large perimeter including both the host and service projects. (If you only select the service project in your perimeter, network endpoints belonging to service projects appear to be outside the perimeter, because the subnets are associated only with the host project.)

### Select the configuration type for the new perimeter

In this section, you create a VPC Service Controls service perimeter in [dry run mode](https://docs.cloud.google.com/vpc-service-controls/docs/service-perimeters#dry-run-mode) . In dry run mode, the perimeter logs violations as though the perimeters are enforced but don't prevent access to restricted services. Using dry run mode before [switching to enforced mode](https://docs.cloud.google.com/vpc-service-controls/docs/manage-dry-run-configurations#enforce-configuration) is recommended as a best practice.

1.  In the Google Cloud console navigation menu, click **Security** , and then click **VPC Service Controls** .

2.  On the **VPC Service Controls** page, click **Dry run mode** .

3.  Click **New perimeter** .

4.  On the **New VPC Service Perimeter** tab, in the **Perimeter Name** box, type a name for the perimeter. Otherwise, accept the default values.
    
    A perimeter name can have a maximum length of 50 characters, must start with a letter, and can contain only ASCII Latin letters (a-z, A-Z), numbers (0-9), or underscores (\_). The perimeter name is case-sensitive and must be unique within an access policy.

### Select the resources to protect

1.  Click **Resources to protect** .

2.  To add projects or VPC networks that you want to secure within the perimeter, do the following:
    
    1.  Click **Add Resources** .
    
    2.  To add projects to the perimeter, in the **Add resources** pane, click **Add project** .
        
        1.  To select a project, in the **Add projects** dialog, select that project's checkbox. In this reference architecture, we select the following projects:
            
              - `infra-host-project`
              - `aiml-host-project`
              - `ph-fm-svc-project`
        
        2.  Click **Add selected resources** . The added projects appear in the **Projects** section.

### Select the restricted services

In this reference architecture, the scope of restricted APIs is limited, enabling only the necessary APIs required for Gemini. However, as a best practice, we recommend that you restrict all services when you create a perimeter to mitigate the risk of data exfiltration from Google Cloud services.

> **Note:** This example shows a pattern for a basic Agent Platform implementation. If you're using additional Agent Platform or Gemini services, add those services to the list of restricted services.

To select the services to secure within the perimeter, do the following:

1.  Click **Restricted Services** .

2.  In the **Restricted Services** pane, click **Add services** .

3.  In the **Specify services to restrict** dialog, select **Agent Platform API** .

4.  Click **Add Agent Platform API** .

### Optional: Select the VPC accessible services

The **VPC accessible services** setting limits the set of services that are accessible from network endpoints inside your service perimeter. In this reference architecture, we're keeping the default setting of **All Services** .

### Optional: Select the access level

If you created a corporate CIDR access level in an earlier section, do the following to allow access to protected resources from outside the perimeter:

1.  Click **Access Levels** .

2.  Click the **Choose Access Level** box.
    
    You can also [add access levels](https://docs.cloud.google.com/vpc-service-controls/docs/manage-service-perimeters#add-access-level) after a perimeter has been created.

3.  Select the checkbox corresponding to the access level. (In this reference architecture, this is `corp-public-block` .)

### Ingress and egress policies

In this reference architecture, there's no need to specify any settings in the **Ingress Policy** or **Egress Policy** panes.

### Create the perimeter

Once you have completed the preceding configuration steps, create the perimeter by clicking **Create perimeter** .

## Configure network connectivity between AWS and Google APIs

### Configure Private Service Connect for Google APIs

Private Service Connect to access Google APIs is an alternative to using Private Google Access or the public domain names for Google APIs. In this case, the producer is Google.

Using Private Service Connect lets you do the following:

  - Create one or more internal IP addresses to access Google APIs for different use cases.
  - Direct on-premises traffic to specific IP addresses and regions when accessing Google APIs.
  - Create a custom endpoint DNS name used to resolve Google APIs.

In the reference architecture, a Private Service Connect Google API endpoint named `restricted` , with IP Address `10.10.10.3,` is deployed with the target VPC-SC, used as a Virtual IP (VIP) to access restricted services configured in the VPC-SC Perimeter. Targeting non-restricted services with the VIP is not supported. For more information, see [About accessing the Agent Platform API | Google Cloud](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/googleapi-access-methods#psc) .

### Configure AWS VPC network

Network connectivity between Amazon Web Services (AWS) and Google Cloud is established using High-Availability Virtual Private Network (HA VPN) tunnels. This secure connection facilitates private communication between the two cloud environments. However, to enable seamless routing and communication between resources in AWS and Google Cloud, the Border Gateway Protocol (BGP) is employed.

In the Google Cloud environment, a custom route advertisement is required. This custom route specifically advertises the Private Service Connect Google API IP address to the AWS network. By advertising this IP address, AWS can establish a direct route to the Google API, bypassing the public internet and improving performance.

In the reference architecture, a Sagemaker instance is deployed with an association with the AWS VPC where the VPN is established with Google Cloud. Border Gateway Protocol (BGP) is used to advertise routes across HA VPN between AWS and Google Cloud network. As a result, Google Cloud and AWS can route bidirectional traffic over VPN. For more information about setting up HA VPN connections, see [Create HA VPN connections between Google Cloud and AWS](https://docs.cloud.google.com/network-connectivity/docs/vpn/tutorials/create-ha-vpn-connections-google-cloud-aws) .

### Configure Route 53 updates

Create a private hosted zone named `p.googleapis.com` in AWS Route 53 and add the fully qualified domain name `  REGION -aiplatform-restricted.p.googleapis.com ` with the IP address `10.10.10.3` (Private Service Connect Googleapis IP) as the DNS A record. When the Jupyter Notebook SDK performs a DNS lookup for Agent Platform API to reach Gemini, Route 53 returns the Private Service Connect Google APIs IP address. Jupyter Notebook uses the IP address obtained from Route 53 to establish a connection to the Private Service Connect Google APIs endpoint routed through HA VPN into Google Cloud.

### Configure Sagemaker updates

This reference architecture uses [Amazon SageMaker Notebook instances](https://docs.aws.amazon.com/sagemaker/latest/dg/nbi.html) to access the Agent Platform API. However, you can achieve the same setup with other compute services supporting VPC, such as [Amazon EC2](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/concepts.html) or [AWS Lambda](https://docs.aws.amazon.com/lambda/latest/dg/welcome.html) .

To authenticate your requests, you can either use a Google Cloud service account key or use [Workload Identity Federation](https://docs.cloud.google.com/iam/docs/workload-identity-federation) . For information about setting up Workload Identity Federation, see [On-premises or another cloud provider](https://cloud.google.com/docs/authentication/provide-credentials-adc#on-prem) .

The Jupyter Notebook instance invokes an API call to the Gemini model hosted in Google Cloud by performing a DNS resolution to the custom Private Service Connect Google APIs fully qualified domain name `  REGION -aiplatform-restricted.p.googleapis.com ` overriding the default fully qualified domain name ( `  REGION -aiplatform.googleapis.com ` ).

The Agent Platform API can be called using Rest, gRPC or SDK. To use the Private Service Connect customer fully qualified domain name, update the API\_ENDPOINT in Jupyter Notebook with the following:

### Instructions for using Vertex AI SDK for Python

1.  Install the SDK:
    
        pip install --upgrade google-genai

2.  Import the dependencies:
    
        from google.cloud import genai
        from google.genai.types import (
           GenerateContentConfig,
           HarmBlockThreshold,
           HarmCategory,
           Part,
           SafetySetting
        )

3.  Initialize the following environment variables:
    
        PROJECT_ID="ph-fm-svc-projects" # Google Cloud Project ID
        LOCATION_ID="us-central1" # Enter Agent Platform Gemini region such as us-central1
        API_ENDPOINT="https://us-central1-aiplatform-restricted.p.googleapis.com" # PSC Endpoint
        MODEL_ID="gemini-2.0-flash-001" # Gemini Model ID

4.  Initialize the Vertex AI SDK for Python:
    
        from google import genai
        client= genai.Client(vertexai=True, project=PROJECT_ID, location=LOCATION_ID, http_options={'base_url': API_ENDPOINT})

5.  Make the following request to the Gemini Enterprise Agent Platform Gemini API:
    
        prompt = "which weighs more, 1kg feathers or 1kg stones"
        
        safety_settings = [
            SafetySetting(
                category=HarmCategory.HARM_CATEGORY_DANGEROUS_CONTENT,
                threshold=HarmBlockThreshold.BLOCK_LOW_AND_ABOVE,
            ),
            SafetySetting(
                category=HarmCategory.HARM_CATEGORY_HARASSMENT,
                threshold=HarmBlockThreshold.BLOCK_LOW_AND_ABOVE,
            ),
            SafetySetting(
                category=HarmCategory.HARM_CATEGORY_HATE_SPEECH,
                threshold=HarmBlockThreshold.BLOCK_LOW_AND_ABOVE,
            ),
            SafetySetting(
                category=HarmCategory.HARM_CATEGORY_SEXUALLY_EXPLICIT,
                threshold=HarmBlockThreshold.BLOCK_LOW_AND_ABOVE,
            ),
        ]
        
        response = client.models.generate_content(
            model=MODEL_ID,
            contents=prompt,
            config=GenerateContentConfig(
                safety_settings=safety_settings,
            ),
        )
        
        # Response will be `None` if it is blocked.
        print(response.text)
    
    At this point, you can perform an API call to Gemini from [Jupyter notebook](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tutorials/tabular-bq-prediction/create-notebook) to access Gemini hosted in Google Cloud. If the call is successful, the output looks like the following:
    
        They weigh the same. Both weigh 1 kilogram.

### Instructions for using the Gemini Enterprise Agent Platform REST API

In this section, you set up some important variables that are used throughout the process. These variables store information about your project, the location of your resources, the specific Gemini model and the PSC endpoint you want to use. Open a terminal window inside a JupyterLab notebook to execute the following commands:

1.  Open a terminal window inside a [Jupyter notebook](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tutorials/tabular-bq-prediction/create-notebook) .

2.  Initialize the following environment variables:
    
        export PROJECT_ID="ph-fm-svc-projects"
        export LOCATION_ID="us-central1"
        export API_ENDPOINT="us-central1-aiplatform-restricted.p.googleapis.com" export MODEL_ID="gemini-1.5-flash-002"

3.  Use a text editor such as `vim` or `nano` to create a new file named `request.json` that contains the following formatted request for the Gemini Enterprise Agent Platform Gemini API:
    
        {
            "contents": [
                {
                    "role": "user",
                    "parts": [
                        {
                            "text": "which weighs more, 1kg feathers or 1kg stones"
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

4.  Make the following curl request to the Gemini Enterprise Agent Platform Gemini API:
    
        curl -v \
        -X POST \
        -H "Content-Type: application/json" \
        -H "Authorization: Bearer $(gcloud auth print-access-token)" \
        "https://$API_ENDPOINT/v1/projects/$PROJECT_ID/locations/$LOCATION_ID/publishers/google/models/$MODEL_ID:streamGenerateContent" -d '@request.json'

## Validate your perimeter in dry run mode

In this reference architecture, the service perimeter is configured in dry run mode, letting you test the effect of access policy without enforcement. This means that you can see how your policies would impact your environment if they were active, but without the risk of disrupting legitimate traffic.

After validating your perimeter in dry run mode, [switch it to enforced mode](https://docs.cloud.google.com/vpc-service-controls/docs/manage-dry-run-configurations#enforce-configuration) .

## What's next

  - Learn how to [Use `p.googleapis.com` DNS names](https://docs.cloud.google.com/vpc/docs/configure-private-service-connect-apis#configure-p-dns) .
  - To learn how to validate your perimeter in dry run mode, watch [the VPC Service Controls dry run logging video](https://www.youtube.com/watch?v=_l-ei3ZlgWc) .
  - Learn how to use the [Gemini Enterprise Agent Platform REST API](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest) .
  - Learn more about using the [Vertex AI SDK for Python](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/python-sdk/use-vertex-ai-python-sdk) .
