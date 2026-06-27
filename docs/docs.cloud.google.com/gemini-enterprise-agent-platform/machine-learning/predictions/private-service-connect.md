---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/private-service-connect
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/private-service-connect
title: Use dedicated private endpoints based on Private Service Connect for online inference
description: Learn about using Private Service Connect endpoints for online inference.
data_source: docs.cloud.google.com
---

The information in this page applies to custom-trained models and AutoML models. For Model Garden deployment, see [Use models in Model Garden](https://docs.cloud.google.com/vertex-ai/generative-ai/docs/model-garden/use-models#deploy_a_model_to_a_private_endpoint) .

Private Service Connect lets you deploy your custom-trained Gemini Enterprise Agent Platform model and serve online inferences securely to multiple consumer projects and VPC networks without the need for public IP addresses, public internet access, or an explicitly peered internal IP address range.

We recommend Private Service Connect for online inference use cases that have the following requirements:

  - Require private and secure connections
  - Require low latency
  - Don't need to be publicly accessible

> **Note:** Tuned Gemini models can only be deployed to shared public endpoints, not Private Service Connect endpoints.

Private Service Connect uses a forwarding rule in your VPC network to send traffic unidirectionally to the Agent Platform online inference service. The forwarding rule connects to a [service attachment](https://docs.cloud.google.com/vpc/docs/private-service-connect#service-attachments) that exposes the Agent Platform service to your VPC network. For more information, see [About accessing Agent Platform services through Private Service Connect](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/psc-endpoints) . To learn more about setting up Private Service Connect, see the [Private Service Connect overview](https://docs.cloud.google.com/vpc/docs/private-service-connect) in the Virtual Private Cloud (VPC) documentation.

Dedicated private endpoints support both HTTP and gRPC communication protocols. For gRPC requests, the x-vertex-ai-endpoint-id header must be included for proper endpoint identification. The following APIs are supported:

  - Predict
  - RawPredict
  - StreamRawPredict
  - Chat Completion (Model Garden only)

You can send online inference requests to a dedicated private endpoint by using the Agent Platform SDK for Python. For details, see [Get online inferences](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/private-service-connect#get_online_inferences) .

## Required roles

To get the permission that you need to create a Private Service Connect endpoint, ask your administrator to grant you the [Agent Platform User](https://docs.cloud.google.com/iam/docs/roles-permissions/aiplatform#aiplatform.user) ( `roles/aiplatform.user` ) IAM role on your project. For more information about granting roles, see [Manage access to projects, folders, and organizations](https://docs.cloud.google.com/iam/docs/granting-changing-revoking-access) .

This predefined role contains the `aiplatform.endpoints.create` permission, which is required to create a Private Service Connect endpoint.

You might also be able to get this permission with [custom roles](https://docs.cloud.google.com/iam/docs/creating-custom-roles) or other [predefined roles](https://docs.cloud.google.com/iam/docs/roles-overview#predefined) .

For more information about Gemini Enterprise Agent Platform roles and permissions, see [Agent Platform access control with IAM](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/access-control) and [Gemini Enterprise Agent Platform IAM permissions](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/iam-permissions) .

## Create the online inference endpoint

Use one of the following methods to create an online inference endpoint with Private Service Connect enabled.

The default request timeout for a Private Service Connect endpoint is 10 minutes. In the Agent Platform SDK for Python, you can optionally specify a different request timeout by specifying a new [`inference_timeout`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.endpoints#ClientConnectionConfig) value, as shown in the following example. The maximum timeout value is 3600 seconds (1 hour).

### Console

1.  In the Google Cloud console, in Agent Platform, go to the **Online prediction** page.

2.  Click **Create** .

3.  Provide a display name for the endpoint.

4.  Select radio\_button\_checked **Private** .

5.  Select radio\_button\_checked **Private Service Connect** .

6.  Click **Select project IDs** .

7.  Select projects to add to the allowlist for the endpoint.

8.  Click **Continue** .

9.  Choose your model specifications. For more information, see [Deploy a model to an endpoint](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/deployment) .

10. Click **Create** to create your endpoint and deploy your model to it.

11. Make a note of the endpoint ID in the response.

### API

### REST

Before using any of the request data, make the following replacements:

  - `VERTEX_AI_PROJECT_ID` : the ID of the Google Cloud project where you're creating the online prediction endpoint.
  - `REGION` : the region where you're using Gemini Enterprise Agent Platform.
  - `VERTEX_AI_ENDPOINT_NAME` : the display name for the online prediction endpoint.
  - `ALLOWED_PROJECTS` : a comma-separated list of Google Cloud project IDs, each enclosed in quotation marks, for example, `["PROJECTID1", "PROJECTID2"]` . If a project isn't contained in this list, you won't be able to send prediction requests to the Agent Platform endpoint from it. Make sure to include VERTEX\_AI\_PROJECT\_ID in this list so that you can call the endpoint from the same project it's in.
  - INFERENCE\_TIMEOUT\_SECS : (Optional) Number of seconds in the optional `  inferenceTimeout  ` field.

HTTP method and URL:

    POST https://REGION-aiplatform.googleapis.com/v1/projects/VERTEX_AI_PROJECT_ID/locations/REGION/endpoints

Request JSON body:

    {
      "displayName": "VERTEX_AI_ENDPOINT_NAME",
      "privateServiceConnectConfig": {
        "enablePrivateServiceConnect": true,
        "projectAllowlist": ["ALLOWED_PROJECTS"],
        "clientConnectionConfig": {
          "inferenceTimeout": {
            "seconds": INFERENCE_TIMEOUT_SECS
          }
        }
      }
    }

To send your request, expand one of these options:

#### curl (Linux, macOS, or Cloud Shell)

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) , or by using [Cloud Shell](https://docs.cloud.google.com/shell/docs) , which automatically logs you into the `gcloud` CLI . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Save the request body in a file named `request.json` , and execute the following command:

    curl -X POST \
         -H "Authorization: Bearer $(gcloud auth print-access-token)" \
         -H "Content-Type: application/json; charset=utf-8" \
         -d @request.json \
         "https://REGION-aiplatform.googleapis.com/v1/projects/VERTEX_AI_PROJECT_ID/locations/REGION/endpoints"

#### PowerShell (Windows)

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Save the request body in a file named `request.json` , and execute the following command:

    $cred = gcloud auth print-access-token
    $headers = @{ "Authorization" = "Bearer $cred" }
    
    Invoke-WebRequest `
        -Method POST `
        -Headers $headers `
        -ContentType: "application/json; charset=utf-8" `
        -InFile request.json `
        -Uri "https://REGION-aiplatform.googleapis.com/v1/projects/VERTEX_AI_PROJECT_ID/locations/REGION/endpoints" | Select-Object -Expand Content

You should receive a JSON response similar to the following:

    {
      "name": "projects/VERTEX_AI_PROJECT_NUMBER/locations/REGION/endpoints/ENDPOINT_ID/operations/OPERATION_ID",
      "metadata": {
        "@type": "type.googleapis.com/google.cloud.aiplatform.v1.CreateEndpointOperationMetadata",
        "genericMetadata": {
          "createTime": "2020-11-05T17:45:42.812656Z",
          "updateTime": "2020-11-05T17:45:42.812656Z"
        }
      }
    }

Make a note of the `  ENDPOINT_ID  ` .

### Python

Before trying this sample, follow the Python setup instructions in the [Agent Platform quickstart using client libraries](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/start/client-libraries) .

To authenticate to Agent Platform, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

Replace the following:

  - `VERTEX_AI_PROJECT_ID` : the ID of the Google Cloud project where you're creating the online inference endpoint
  - `REGION` : the region where you're using Gemini Enterprise Agent Platform
  - `VERTEX_AI_ENDPOINT_NAME` : the display name for the online inference endpoint
  - `ALLOWED_PROJECTS` : a comma-separated list of Google Cloud project IDs, each enclosed in quotation marks. For example, `["PROJECTID1", "PROJECTID2"]` . If a project isn't contained in this list, you won't be able to send inference requests to the Agent Platform endpoint from it. Make sure to include VERTEX\_AI\_PROJECT\_ID in this list so that you can call the endpoint from the same project it's in.
  - `INFERENCE_TIMEOUT_SECS` : (Optional) Number of seconds in the optional [`inference_timeout`](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.Endpoint#google_cloud_aiplatform_Endpoint_create) value.

<!-- end list -->

    PROJECT_ID = "VERTEX_AI_PROJECT_ID"
    REGION = "REGION"
    VERTEX_AI_ENDPOINT_NAME = "VERTEX_AI_ENDPOINT_NAME"
    INFERENCE_TIMEOUT_SECS = "INFERENCE_TIMEOUT_SECS"
    
    from google.cloud import aiplatform
    
    aiplatform.init(project=PROJECT_ID, location=REGION)
    
    # Create the forwarding rule in the consumer project
    psc_endpoint = aiplatform.PrivateEndpoint.create(
    display_name=VERTEX_AI_ENDPOINT_NAME,
    project=PROJECT_ID,
    location=REGION,
    private_service_connect_config=aiplatform.PrivateEndpoint.PrivateServiceConnectConfig(
        project_allowlist=["ALLOWED_PROJECTS"],
        ),
    inference_timeout=INFERENCE_TIMEOUT_SECS,
    )

Make a note of the `ENDPOINT_ID` at the end of the returned endpoint URI:

    INFO:google.cloud.aiplatform.models:To use this PrivateEndpoint in another session:
    INFO:google.cloud.aiplatform.models:endpoint = aiplatform.PrivateEndpoint('projects/VERTEX_AI_PROJECT_ID/locations/REGION/endpoints/ENDPOINT_ID')

## Create the online inference endpoint with PSC automation

Online inference integrates with [service connectivity automation](https://docs.cloud.google.com/vpc/docs/about-service-connectivity-automation) , which lets you configure inference endpoints with PSC automation. This simplifies the process by automatically creating PSC endpoints, and is particularly beneficial for ML developers who lack permissions to create network resources such as forwarding rules within a project.

To get started, your network administrator must establish a [service connection policy](https://docs.cloud.google.com/vpc/docs/about-service-connection-policies) . This policy is a one-time configuration per project and network that lets Gemini Enterprise Agent Platform (service class `gcp-vertexai` ) generate PSC endpoints within your projects and networks.

Next, you can create endpoints using the PSC automation configuration and then deploy your models. Once the deployment is complete, the relevant PSC endpoint information is accessible within the endpoints.

### Limitations

  - A regional limit of 500 endpoints applies to PSC automation configurations.
  - PSC automation results are purged when no model is deployed or is in the process of being deployed to the endpoint. Upon cleanup and subsequent model deployment, new automation results feature distinct IP addresses and forwarding rules.

### Create a service connection policy

You must be a network administrator to create the [service connection policy](https://docs.cloud.google.com/vpc/docs/about-service-connection-policies) . A Service connection policy is required to let Agent Platform create PSC endpoints in your networks. Without a valid policy, the automation fails with a `CONNECTION_POLICY_MISSING` error.

1.  Create your service connection policy.
    
      - POLICY\_NAME : A user-specified name for the policy.
    
      - PROJECT\_ID : The ID of the service project where you are creating Gemini Enterprise Agent Platform resources.
    
      - VPC\_PROJECT : The project ID where your client VPC is located. For single VPC setup, this is the same as `$PROJECT` . For Shared VPC setup, this is the VPC host project.
    
      - NETWORK\_NAME : The name of the network to deploy to.
    
      - REGION : The network's region.
    
      - PSC\_SUBNETS : The Private Service Connect subnets to use.
    
    <!-- end list -->
    
        gcloud network-connectivity service-connection-policies create POLICY_NAME \
            --project=VPC_PROJECT \
            --network=projects/PROJECT_ID/global/networks/NETWORK_NAME \
            --service-class=gcp-vertexai --region=REGION --subnets=PSC_SUBNETS

2.  View your service connection policy.
    
        gcloud network-connectivity service-connection-policies list \
            --project=VPC_PROJECT -–region=REGION
    
    For a single VPC setup, a sample looks like this:
    
    ``` 
        gcloud network-connectivity service-connection-policies create test-policy \
            --network=default \
            --project=YOUR_PROJECT_ID \
            --region=us-central1 \
            --service-class=gcp-vertexai \
            --subnets=default \
            --psc-connection-limit=500 \
            --description=test
    ```

### Create the online inference endpoint with PSC automation config

In the `PSCAutomationConfig` , check to be sure that the `projectId` is in the allowlist.

### REST

Before using any of the request data, make the following replacements:

  - REGION : The region where you're using Agent Platform.
  - VERTEX\_AI\_PROJECT\_ID : The ID of the Google Cloud project where you're creating the online inference endpoint.
  - VERTEX\_AI\_ENDPOINT\_NAME : The display name for the online prediction endpoint.
  - NETWORK\_NAME : the full resource name, including the project ID, instead of the project number.

HTTP method and URL:

    POST https://REGION-aiplatform.googleapis.com/v1/projects/VERTEX_AI_PROJECT_ID/locations/REGION/endpoints

Request JSON body:

    {
      {
        displayName: "VERTEX_AI_ENDPOINT_NAME",
        privateServiceConnectConfig: {
          enablePrivateServiceConnect: true,
          projectAllowlist: ["VERTEX_AI_PROJECT_ID"],
          pscAutomationConfigs: [
            { "project_id": "VERTEX_AI_PROJECT_ID", "network": "projects/VERTEX_AI_PROJECT_ID/global/networks/NETWORK_NAME" },
          ],
        },
      },

To send your request, expand one of these options:

#### curl (Linux, macOS, or Cloud Shell)

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) , or by using [Cloud Shell](https://docs.cloud.google.com/shell/docs) , which automatically logs you into the `gcloud` CLI . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Save the request body in a file named `request.json` , and execute the following command:

    curl -X POST \
         -H "Authorization: Bearer $(gcloud auth print-access-token)" \
         -H "Content-Type: application/json; charset=utf-8" \
         -d @request.json \
         "https://REGION-aiplatform.googleapis.com/v1/projects/VERTEX_AI_PROJECT_ID/locations/REGION/endpoints"

#### PowerShell (Windows)

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Save the request body in a file named `request.json` , and execute the following command:

    $cred = gcloud auth print-access-token
    $headers = @{ "Authorization" = "Bearer $cred" }
    
    Invoke-WebRequest `
        -Method POST `
        -Headers $headers `
        -ContentType: "application/json; charset=utf-8" `
        -InFile request.json `
        -Uri "https://REGION-aiplatform.googleapis.com/v1/projects/VERTEX_AI_PROJECT_ID/locations/REGION/endpoints" | Select-Object -Expand Content

You should receive a JSON response similar to the following:

    {
      "name": "projects/VERTEX_AI_PROJECT_NUMBER/locations/REGION/endpoints/ENDPOINT_ID/operations/OPERATION_ID",
      "metadata": {
        "@type": "type.googleapis.com/google.cloud.aiplatform.v1.CreateEndpointOperationMetadata",
        "genericMetadata": {
          "createTime": "2020-11-05T17:45:42.812656Z",
          "updateTime": "2020-11-05T17:45:42.812656Z"
        }
      }
    }

Make a note of the `  ENDPOINT_ID  ` .

### Python

Before trying this sample, follow the Python setup instructions in the [Agent Platform quickstart using client libraries](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/start/client-libraries) .

To authenticate to Agent Platform, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

Replace the following:

  - `VERTEX_AI_PROJECT_ID` : the ID of the Google Cloud project where you're creating the online inference endpoint
  - `REGION` : the region where you're using Gemini Enterprise Agent Platform
  - `VERTEX_AI_ENDPOINT_NAME` : the display name for the online inference endpoint
  - `NETWORK_NAME` : the full resource name, including the project ID, instead of the project number.

<!-- end list -->

    PROJECT_ID = "VERTEX_AI_PROJECT_ID"
    REGION = "REGION"
    VERTEX_AI_ENDPOINT_NAME = "VERTEX_AI_ENDPOINT_NAME"
    
    from google.cloud import aiplatform
    
    aiplatform.init(project=PROJECT_ID, location=REGION)
    
    config =
    aiplatform.compat.types.service_networking.PrivateServiceConnectConfig(
            enable_private_service_connect=True,
            project_allowlist="VERTEX_AI_PROJECT_ID"
            psc_automation_configs=[
                aiplatform.compat.types.service_networking.PSCAutomationConfig(
                    project_id="VERTEX_AI_PROJECT_ID"
    network=projects/"VERTEX_AI_PROJECT_ID"/global/networks/"NETWORK_NAME",
                )
            ]
        )
    psc_endpoint = aiplatform.PrivateEndpoint.create(
         display_name="VERTEX_AI_ENDPOINT_NAME"
         private_service_connect_config=config,
    )

## Deploy the model

After you create your online inference endpoint with Private Service Connect enabled, deploy your model to it, following the steps outlined in [Deploy a model to an endpoint](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/deployment#deploy_a_model_to_an_endpoint) .

## Create PSC Endpoint Manually

### Get the service attachment URI

When you deploy your model, a service attachment is created for the online inference endpoint. This service attachment represents the Agent Platform online inference service that's being exposed to your VPC network. Run the [`gcloud ai endpoints describe` command](https://docs.cloud.google.com/sdk/gcloud/reference/ai/endpoints/describe) to get the service attachment URI.

1.  List only the `serviceAttachment` value from the endpoint details:
    
        gcloud ai endpoints describe ENDPOINT_ID \
        --project=VERTEX_AI_PROJECT_ID \
        --region=REGION \
        | grep -i serviceAttachment
    
    Replace the following:
    
      - `ENDPOINT_ID` : the ID of your online inference endpoint
      - `VERTEX_AI_PROJECT_ID` : the ID of the Google Cloud project where you created your online inference endpoint
      - `REGION` : the region for this request
    
    The output is similar to the following:
    
        serviceAttachment: projects/ac74a9f84c2e5f2a1-tp/regions/us-central1/serviceAttachments/gkedpm-c6e6a854a634dc99472bb802f503c1

2.  Make a note of the entire string in the `serviceAttachment` field. This is the service attachment URI.

### Create a forwarding rule

You can reserve an internal IP address and [create a forwarding rule](https://docs.cloud.google.com/vpc/docs/configure-private-service-connect-services#create-endpoint) with that address. To create the forwarding rule, you need the service attachment URI from the previous step.

1.  To reserve an internal IP address for the forwarding rule, use the [`gcloud compute addresses create` command](https://docs.cloud.google.com/sdk/gcloud/reference/compute/addresses/create) :
    
        gcloud compute addresses create ADDRESS_NAME \
        --project=VPC_PROJECT_ID \
        --region=REGION \
        --subnet=SUBNETWORK \
        --addresses=INTERNAL_IP_ADDRESS
    
    Replace the following:
    
      - `ADDRESS_NAME` : a name for the internal IP address
    
      - `VPC_PROJECT_ID` : the ID of the Google Cloud project that hosts your VPC network. If your online inference endpoint and your Private Service Connect forwarding rule are hosted in the same project, use `  VERTEX_AI_PROJECT_ID  ` for this parameter.
    
      - `REGION` : the Google Cloud region where the Private Service Connect forwarding rule is to be created
    
      - `SUBNETWORK` : the name of the VPC subnet that contains the IP address
    
      - `INTERNAL_IP_ADDRESS` : the internal IP address to reserve. This parameter is optional.
        
          - If this parameter is specified, the IP address must be within the subnet's primary IP address range. The IP address can be an [RFC 1918](https://datatracker.ietf.org/doc/html/rfc1918) address or a subnet with non-RFC ranges.
          - If this parameter is omitted, an internal IP address is allocated automatically.
          - For more information, see [Reserve a new static internal IPv4 or IPv6 address](https://docs.cloud.google.com/vpc/docs/reserve-static-internal-ip-address#reservenewip) .

2.  To verify that the IP address is reserved, use the [`gcloud compute addresses list` command](https://docs.cloud.google.com/sdk/gcloud/reference/compute/addresses/list) :
    
        gcloud compute addresses list --filter="name=(ADDRESS_NAME)" \
        --project=VPC_PROJECT_ID
    
    In the response, verify that a `RESERVED` status appears for the IP address.

3.  To create the forwarding rule and point it to the online inference service attachment, use the [`gcloud compute forwarding-rules create` command](https://docs.cloud.google.com/sdk/gcloud/reference/compute/forwarding-rules/create) :
    
        gcloud compute forwarding-rules create PSC_FORWARDING_RULE_NAME \
            --address=ADDRESS_NAME \
            --project=VPC_PROJECT_ID \
            --region=REGION \
            --network=VPC_NETWORK_NAME \
            --target-service-attachment=SERVICE_ATTACHMENT_URI
    
    Replace the following:
    
      - `PSC_FORWARDING_RULE_NAME` : a name for the forwarding rule
      - `VPC_NETWORK_NAME` : the name of the VPC network where the endpoint is to be created
      - `SERVICE_ATTACHMENT_URI` : the service attachment that you made a note of earlier

4.  To verify that the service attachment accepts the endpoint, use the [`gcloud compute forwarding-rules describe` command](https://docs.cloud.google.com/sdk/gcloud/reference/compute/forwarding-rules/describe) :
    
        gcloud compute forwarding-rules describe PSC_FORWARDING_RULE_NAME \
        --project=VPC_PROJECT_ID \
        --region=REGION
    
    In the response, verify that an `ACCEPTED` status appears in the `pscConnectionStatus` field.

### Get the internal IP address

If you didn't specify a value for `  INTERNAL_IP_ADDRESS  ` when you created the forwarding rule, you can get the address that was allocated automatically by using the [`gcloud compute forwarding-rules describe` command](https://docs.cloud.google.com/sdk/gcloud/reference/compute/forwarding-rules/describe) :

    gcloud compute forwarding-rules describe PSC_FORWARDING_RULE_NAME \
    --project=VERTEX_AI_PROJECT_ID \
    --region=REGION \
    | grep -i IPAddress

Replace the following:

  - `VERTEX_AI_PROJECT_ID` : your project ID
  - `REGION` : the region name for this request

## Optional: Get PSC endpoint from PSC automation result

You can get the generated IP address and forwarding rule from the inference endpoint. Here's an example:

    "privateServiceConnectConfig": {
      "enablePrivateServiceConnect": true,
      "projectAllowlist": [
        "your-project-id",
      ],
      "pscAutomationConfigs": [
        {
          "projectId": "your-project-id",
          "network": "projects/your-project-id/global/networks/default",
          "ipAddress": "10.128.15.209",
          "forwardingRule": "https://www.googleapis.com/compute/v1/projects/your-project-id/regions/us-central1/forwardingRules/sca-auto-fr-47b0d6a4-eaff-444b-95e6-e4dc1d10101e",
          "state": "PSC_AUTOMATION_STATE_SUCCESSFUL"
        },
      ]
    }

Here are some error handling details.

  - Automation failure doesn't affect the outcome of the model deployment.
  - The success or failure of the operation is indicated in the state.
      - If successful, the IP address and forwarding rule is displayed.
      - If unsuccessful, an error message is displayed.
  - Automation configurations are removed when no models are deployed or in the process of being deployed to the endpoint. This results in a change to the IP address and forwarding rule if a model is deployed later.
  - Failed automation won't recover. In case of failure, you can still create the PSC endpoint manually, see [Create PSC Endpoint Manually](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/private-service-connect#create-psc-endpoint-manually) .

## Get online inferences

Getting online inferences from an endpoint with Private Service Connect is similar to [getting online inferences](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/get-online-predictions) from public endpoints, except for the following considerations:

  - The request must be sent from a project that was specified in the `projectAllowlist` when the online inference endpoint was created.

  - If [global access](https://cloud.google.com/blog/products/networking/access-managed-services-globally-with-private-service-connect) isn't enabled, the request must be sent from the same region.

  - There are two ports open, 443 with TLS using self-signed certificate and 80 without TLS. Both ports support HTTP and gRPC. All traffic remains on your private network and doesn't traverse the public internet.

  - The best practice is to use HTTPS with the self-signed certificate obtained from Gemini Enterprise Agent Platform online inference or to deploy your own self-signed certificate.

  - To obtain inferences, a connection must be established using the endpoint's static IP address, unless a DNS record is created for the internal IP address. For example, send the [`predict`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.endpoints/predict) requests to the following endpoint:
    
        http://INTERNAL_IP_ADDRESS/v1/projects/VERTEX_AI_PROJECT_ID/locations/REGION/endpoints/ENDPOINT_ID:predict
    
    Replace `INTERNAL_IP_ADDRESS` with the internal IP address that you reserved earlier.

  - For gRPC requests: To ensure proper endpoint identification for gRPC requests, it is necessary to include the header `x-vertex-ai-endpoint-id` . This is required as endpoint information is not conveyed within the request path for gRPC communication.

### Create a DNS record for the internal IP address

We recommend that you create a DNS record so that you can get online inferences from your endpoint without needing to specify the internal IP address.

For more information, see [Other ways to configure DNS](https://docs.cloud.google.com/vpc/docs/configure-private-service-connect-services#other-dns) .

1.  Create a private DNS zone by using the [`gcloud dns managed-zones create` command](https://docs.cloud.google.com/sdk/gcloud/reference/dns/managed-zones/create) . This zone is associated with the VPC network that the forwarding rule was created in.
    
        DNS_NAME_SUFFIX="prediction.p.vertexai.goog."  # DNS names have "." at the end.
        gcloud dns managed-zones create ZONE_NAME \
        --project=VPC_PROJECT_ID \
        --dns-name=$DNS_NAME_SUFFIX \
        --networks=VPC_NETWORK_NAME \
        --visibility=private \
        --description="A DNS zone for Agent Platform endpoints using Private Service Connect."

    Replace the following:
    
      - `ZONE_NAME` : the name of the DNS zone

2.  To create a DNS record in the zone, use the [`gcloud dns record-sets create` command](https://docs.cloud.google.com/sdk/gcloud/reference/dns/record-sets/create) :
    
        DNS_NAME=ENDPOINT_ID-REGION-VERTEX_AI_PROJECT_NUMBER.$DNS_NAME_SUFFIX
        gcloud dns record-sets create $DNS_NAME \
        --rrdatas=INTERNAL_IP_ADDRESS \
        --zone=ZONE_NAME \
        --type=A \
        --ttl=60 \
        --project=VPC_PROJECT_ID
    
    Replace the following:
    
      - `VERTEX_AI_PROJECT_NUMBER` : the project number for your `  VERTEX_AI_PROJECT_ID  ` project. You can locate this project number in the Google Cloud console. For more information, see [Identifying projects](https://docs.cloud.google.com/resource-manager/docs/creating-managing-projects#identifying_projects) .
      - `INTERNAL_IP_ADDRESS` : the internal IP address of your online inference endpoint
    
    Now you can send your [`predict`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.endpoints/predict) requests to:
    
        http://ENDPOINT_ID-REGION-VERTEX_AI_PROJECT_NUMBER.prediction.p.vertexai.goog/v1/projects/VERTEX_AI_PROJECT_ID/locations/REGION/endpoints/ENDPOINT_ID:predict

## Support for Transport Layer Security (TLS) certificates

Gemini Enterprise Agent Platform online inference is secured using a self-signed certificate. Because this certificate is not signed by a trusted CA (certificate authority), clients attempting to establish an HTTPS connection must be explicitly configured to trust it. The self-signed certificate obtained from the Gemini Enterprise Agent Platform online inference endpoint is valid for 10 years. Because this certificate is not unique to a specific endpoint, a single certificate may be used for all trust store integrations. Following are the high-level steps required to establish an HTTPS connection to Gemini Enterprise Agent Platform online inference:

1.  **Configure DNS** : The self-signed certificate includes the subject alternative name (SAN) `*.prediction.p.vertexai.goog` . You must create a DNS record in your network that matches this format.
    
    For implementation details, see [Create a DNS record for the internal IP address](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/private-service-connect#create-dns-record) .

2.  **Establish client trust** : The client must download the self-signed certificate and add it to its local trust store.

3.  **Establish HTTPS connection** : Establishing an HTTPS connection to Gemini Enterprise Agent Platform online inference requires using the fully qualified domain name (FQDN). This is necessary because the service uses a wildcard SSL certificate valid for the domain `*.prediction.p.vertexai.goog` .

The following steps demonstrate how to download the Gemini Enterprise Agent Platform online inference certificate and add it to the local trust store on Debian-based Linux systems such as Debian 11 and Ubuntu.

1.  Update OS packages and install OpenSSL:
    
        sudo apt update && sudo apt install openssl

2.  Run the following command from your home directory to download the Gemini Enterprise Agent Platform online inference certificate and save it to a file named `vertex_certificate.crt` in your current directory. Make the following replacements:
    
      - ENDPOINT\_ID : ID of the deployed model endpoint
      - REGION : the region where your endpoint resides
      - VERTEX\_AI\_PROJECT\_NUMBER : the project number for your project. You can locate this project number in the Google Cloud console. For more information, see [Identifying projects](https://docs.cloud.google.com/resource-manager/docs/creating-managing-projects#identifying_projects) .
    
    <!-- end list -->
    
        openssl s_client -showcerts -connect \
        ENDPOINT_ID-REGION-VERTEX_AI_PROJECT_NUMBER.prediction.p.vertexai.goog:443 </dev/null | \
        openssl x509 -outform pem -out vertex_certificate.crt

3.  Move the certificate to the system trust store:
    
        sudo mv vertex_certificate.crt /usr/local/share/ca-certificates

4.  Update the Certificate Manager's list of trusted CAs. You should see output confirming that one certificate was added.
    
        sudo update-ca-certificates

5.  Send a `predict` request to the following URL, making these replacements:
    
      - INTERNAL\_IP\_ADDRESS : the internal IP address of your online inference endpoint
      - VERTEX\_AI\_PROJECT\_ID : the project ID for your project
    
    <!-- end list -->
    
        https://ENDPOINT_ID-REGION-VERTEX_AI_PROJECT_NUMBER.prediction.p.vertexai.goog/v1/projects/VERTEX_AI_PROJECT_ID/locations/REGION/endpoints/ENDPOINT_ID:predict

## Custom certificate support for TLS

For organizations needing precise control over certificate management and rotation for Gemini Enterprise Agent Platform online inference endpoints, you can use a customer-managed certificate with an external or internal regional Google Cloud Application Load Balancer (HTTPS).

Following are the high-level deployment steps:

1.  Create a certificate in one of the following ways:
    
      - **Generate a self-signed certificate (or use your CA) for a custom domain.** Custom domains don't need to follow a specific format.
      - **Use [Certificate Manager](https://docs.cloud.google.com/certificate-manager/docs/overview) for a Google-managed certificate.** Google-managed certificates have limitations on the length of supported domain names. For more information, see [Domain name length limitations for Google-managed certificates](https://docs.cloud.google.com/gemini-enterprise-agent-platform/docs/quotas#domain_name_length_limitations_for_google-managed_certificates) .

2.  Deploy a regional Application Load Balancer (HTTPS):
    
      - Configure the [load balancer](https://docs.cloud.google.com/load-balancing/docs/l7-internal) to use your customer-managed certificate for its HTTPS frontend.
      - Set the backend service to a [Private Service Connect (PSC) Network Endpoint Group (NEG)](https://docs.cloud.google.com/vpc/docs/access-apis-managed-services-private-service-connect-backends#neg-published-service) . This NEG will point to the service attachment published service of your Gemini Enterprise Agent Platform model endpoint.

3.  Configure DNS:
    
      - Add an A record to your DNS zone. The zone can be public or private.
      - This record must map your fully qualified custom domain (for example, `example.com` ) to the IP address of the regional Application Load Balancer.

4.  Update the local trust store:
    
      - For the client to authenticate the server, the Application Load Balancer's certificate (or its issuing CA) must be imported into the local trust store.

Now you can send your predict requests to the fully qualified custom domain:

    https://example.com/v1/projects/VERTEX_AI_PROJECT_ID/locations/REGION/endpoints/ENDPOINT_ID:predict

## Examples of getting online inferences

The following sections provide examples of how you can send the [predict](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.PrivateEndpoint#google_cloud_aiplatform_PrivateEndpoint_predict) request using Python.

### First example

    psc_endpoint = aiplatform.PrivateEndpoint("projects/VERTEX_AI_PROJECT_ID/locations/REGION/endpoints/ENDPOINT_ID")
    REQUEST_FILE = "PATH_TO_INPUT_FILE"
    import json
    
    import urllib3
    
    urllib3.disable_warnings(urllib3.exceptions.InsecureRequestWarning)
    
    with open(REQUEST_FILE) as json_file:
        data = json.load(json_file)
        response = psc_endpoint.predict(
            instances=data["instances"], endpoint_override=INTERNAL_IP_ADDRESS
        )
    print(response)

Replace `PATH_TO_INPUT_FILE` with a path to a JSON file containing the request input.

### Second example

    import json
    import requests
    import urllib3
    import google.auth.transport.requests
    
    urllib3.disable_warnings(urllib3.exceptions.InsecureRequestWarning)
    
    REQUEST_FILE = "PATH_TO_INPUT_FILE"
    
    # Programmatically get credentials and generate an access token
    creds, project = google.auth.default()
    auth_req = google.auth.transport.requests.Request()
    creds.refresh(auth_req)
    access_token = creds.token
    # Note: the credential lives for 1 hour by default
    # After expiration, it must be refreshed
    # See https://cloud.google.com/docs/authentication/token-types#access-tokens
    # for token lifetimes.
    
    with open(REQUEST_FILE) as json_file:
        data = json.load(json_file)
        url = "https://INTERNAL_IP_ADDRESS/v1/projects/VERTEX_AI_PROJECT_ID/locations/REGION/endpoints/ENDPOINT_ID:predict"
        headers = {
          "Content-Type": "application/json",
          "Authorization": f"Bearer {access_token}"  # Add access token to headers
        }
        payload = {
          "instances": data["instances"],
        }
    
    response = requests.post(url, headers=headers, json=payload, verify=False)
    
    print(response.json())

### Third example

The following is an example of how you can send the [predict](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.PrivateEndpoint#google_cloud_aiplatform_PrivateEndpoint_predict) request to the DNS zone using Python:

    REQUEST_FILE = "PATH_TO_INPUT_FILE"
    import json
    
    import urllib3
    
    urllib3.disable_warnings(urllib3.exceptions.InsecureRequestWarning)
    
    with open(REQUEST_FILE) as json_file:
        data = json.load(json_file)
        response = psc_endpoint.predict(
            instances=data["instances"], endpoint_override=DNS_NAME
        )
    print(response)

Replace `DNS_NAME` with the DNS name that you specified in the `gcloud dns record-sets create` command.

## Best practices

When a new endpoint is deployed, the service attachment might be updated. Always check the service attachment and PSC endpoint status before making the inference call. Following are best practices for doing this:

  - If an endpoint has no active deployments, Gemini Enterprise Agent Platform might delete the service attachment and recreate it. Make sure the PSC endpoint is in a connected state (by recreating the forwarding rule) when the service attachment is recreated.
  - When an endpoint has an active deployed model, the service attachment doesn't change. To keep the service attachment, create a traffic split and gradually migrate traffic to the new model version, before undeploying the earlier version.
  - Gemini Enterprise Agent Platform allows up to 1,000 connections per service attachment.
  - The forwarding rule has a quota limit as well. For details, see [Cloud Load Balancing quotas and limits](https://docs.cloud.google.com/load-balancing/docs/quotas#forwarding_rules) .

## Limitations

Agent Platform endpoints with Private Service Connect are subject to the following limitations:

  - Deployment of tuned Gemini models isn't supported.
  - Private egress from within the endpoint isn't supported. Because Private Service Connect forwarding rules are unidirectional, other private Google Cloud workloads aren't accessible inside your container.
  - An endpoint's `projectAllowlist` value can't be changed.
  - Vertex Explainable AI isn't supported.
  - Before you delete an endpoint, you must undeploy your model from that endpoint.
  - If all models are undeployed for more than 10 minutes, the service attachment might be deleted. Check the [Private Service Connect connection status](https://docs.cloud.google.com/python/docs/reference/compute/latest/google.cloud.compute_v1.types.ForwardingRule.PscConnectionStatus) ; if it's `CLOSED` , recreate the forwarding rule.
  - After you've deleted your endpoint, you won't be able to reuse that endpoint name for up to 7 days.
  - A project can have up to 10 different `projectAllowlist` values in its Private Service Connect configurations.

## What's next

  - [Deploy a model to an endpoint](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/deployment)
  - [Get online inferences](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/get-online-predictions)
