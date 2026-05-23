---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/create-public-endpoint
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/create-public-endpoint
title: Create a public endpoint
description: Create a public endpoint in Gemini Enterprise Agent Platform.
data_source: docs.cloud.google.com
---

To deploy a model by using the gcloud CLI or Gemini Enterprise API, you first need to create a [public endpoint](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/choose-endpoint-type) .

If you already have an existing public endpoint, you can skip this step and proceed to [Deploy a model by using the gcloud CLI or Gemini Enterprise API](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/deploy-model-api) .

This document describes the process for creating a new public endpoint.

## Create a dedicated public endpoint (recommended)

The default request timeout for a dedicated public endpoint is 10 minutes. In the Gemini Enterprise API and Agent Platform SDK for Python, you can optionally specify a different request timeout by adding a `clientConnectionConfig` object containing a new [`inferenceTimeout`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.endpoints#ClientConnectionConfig) value, as shown in the following example. The maximum timeout value is 3600 seconds (1 hour).

### Google Cloud console

In the Google Cloud console, in the Agent Platform section, go to the **Online prediction** page.  

Click add **Create** .

In the **New endpoint** pane:

1.  Enter the **Endpoint name** .
2.  Select **Standard** for the access type.
3.  Select the **Enable dedicated DNS** checkbox.
4.  Click **Continue** .

Click **Done** .

### REST

Before using any of the request data, make the following replacements:

  - LOCATION\_ID : Your region.
  - PROJECT\_ID : Your \[project ID\](/resource-manager/docs/creating-managing-projects\#identifiers). .
  - ENDPOINT\_NAME : The display name for the endpoint.
  - INFERENCE\_TIMEOUT\_SECS : (Optional) Number of seconds in the optional `  inferenceTimeout  ` field.

HTTP method and URL:

    POST https://LOCATION_ID-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION_ID/endpoints

Request JSON body:

    {
      "display_name": "ENDPOINT_NAME",
      "dedicatedEndpointEnabled": true,
      "clientConnectionConfig": {
        "inferenceTimeout": {
          "seconds": INFERENCE_TIMEOUT_SECS
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
         "https://LOCATION_ID-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION_ID/endpoints"

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
        -Uri "https://LOCATION_ID-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION_ID/endpoints" | Select-Object -Expand Content

You should receive a JSON response similar to the following:

    {
      "name": "projects/PROJECT_NUMBER/locations/LOCATION_ID/endpoints/ENDPOINT_ID/operations/OPERATION_ID",
      "metadata": {
        "@type": "type.googleapis.com/google.cloud.aiplatform.v1.CreateEndpointOperationMetadata",
        "genericMetadata": {
          "createTime": "2020-11-05T17:45:42.812656Z",
          "updateTime": "2020-11-05T17:45:42.812656Z"
        }
      }
    }

You can poll for the status of the operation until the response includes `"done": true` .

### Python

Before trying this sample, follow the Python setup instructions in the [Agent Platform quickstart using client libraries](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/start/client-libraries) .

To authenticate to Agent Platform, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

Replace the following:

  - PROJECT\_ID : Your project ID.
  - LOCATION\_ID : The region where you are using Agent Platform.
  - ENDPOINT\_NAME : The display name for the endpoint.
  - INFERENCE\_TIMEOUT\_SECS : (Optional) Number of seconds in the optional [`inference_timeout`](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.Endpoint#google_cloud_aiplatform_Endpoint_create) value.

<!-- end list -->

    from google.cloud import aiplatform
    
    PROJECT_ID = "PROJECT_ID"
    LOCATION = "LOCATION_ID"
    ENDPOINT_NAME = "ENDPOINT_NAME"
    INFERENCE_TIMEOUT_SECS = "INFERENCE_TIMEOUT_SECS"
    
    aiplatform.init(
        project=PROJECT_ID,
        location=LOCATION,
        api_endpoint=ENDPOINT_NAME,
    )
    
    dedicated_endpoint = aiplatform.Endpoint.create(
        display_name=DISPLAY_NAME,
        dedicated_endpoint_enabled=True,
        sync=True,
        inference_timeout=INFERENCE_TIMEOUT_SECS,
    )

### Inference timeout configuration

The default timeout duration for inference requests is 600 seconds (10 minutes). This timeout will be applied if an explicit inference timeout is not specified during endpoint creation. The maximum permissible timeout value is one hour.

To configure the inference timeout during endpoint creation, use the `inference_timeout` parameter as demonstrated in the following code snippet:

    timeout_endpoint = aiplatform.Endpoint.create(
        display_name="dedicated-endpoint-with-timeout",
        dedicated_endpoint_enabled=True,
        inference_timeout=1800,  # Unit: Seconds
    )

Modifications to the inference timeout setting after endpoint creation can be performed using the `EndpointService.UpdateEndpointLongRunning` method. The `EndpointService.UpdateEndpoint` method does not support this modification.

### Request-response Logging

The request-response logging feature captures API interactions. However, to comply with BigQuery limitations, payloads exceeding 10MB in size will be excluded from the logs.

To enable and configure request-response logging during endpoint creation, use the following parameters as illustrated in the subsequent code snippet:

    logging_endpoint = aiplatform.Endpoint.create(
        display_name="dedicated-endpoint-with-logging",
        dedicated_endpoint_enabled=True,
        enable_request_response_logging=True,
        request_response_logging_sampling_rate=1.0,  # Default: 0.0
        request_response_logging_bq_destination_table="bq://test_logging",
        # If not set, a new BigQuery table will be created with the name:
        # bq://{project_id}.logging_{endpoint_display_name}_{endpoint_id}.request_response_logging
    )

Modifications to the request-response logging settings after endpoint creation can be performed using the `EndpointService.UpdateEndpointLongRunning` method. The `EndpointService.UpdateEndpoint` method does not support this modification.

## Create a shared public endpoint

### Google Cloud console

In the Google Cloud console, in the Agent Platform section, go to the **Online prediction** page.  

Click add **Create** .

In the **New endpoint** pane:

1.  Enter the **Endpoint name** .
2.  Select **Standard** for the access type.
3.  Click **Continue** .

Click **Done** .

### gcloud

The following example uses the [`gcloud ai endpoints create` command](https://docs.cloud.google.com/sdk/gcloud/reference/ai/endpoints/create) :

    gcloud ai endpoints create \
        --region=LOCATION_ID \
        --display-name=ENDPOINT_NAME

Replace the following:

  - LOCATION\_ID : The region where you are using Agent Platform.
  - ENDPOINT\_NAME : The display name for the endpoint.

The Google Cloud CLI tool might take a few seconds to create the endpoint.

### REST

Before using any of the request data, make the following replacements:

  - LOCATION\_ID : Your region.
  - PROJECT\_ID : Your \[project ID\](/resource-manager/docs/creating-managing-projects\#identifiers). .
  - ENDPOINT\_NAME : The display name for the endpoint.

HTTP method and URL:

    POST https://LOCATION_ID-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION_ID/endpoints

Request JSON body:

    {
      "display_name": "ENDPOINT_NAME"
    }

To send your request, expand one of these options:

#### curl (Linux, macOS, or Cloud Shell)

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) , or by using [Cloud Shell](https://docs.cloud.google.com/shell/docs) , which automatically logs you into the `gcloud` CLI . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Save the request body in a file named `request.json` , and execute the following command:

    curl -X POST \
         -H "Authorization: Bearer $(gcloud auth print-access-token)" \
         -H "Content-Type: application/json; charset=utf-8" \
         -d @request.json \
         "https://LOCATION_ID-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION_ID/endpoints"

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
        -Uri "https://LOCATION_ID-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION_ID/endpoints" | Select-Object -Expand Content

You should receive a JSON response similar to the following:

    {
      "name": "projects/PROJECT_NUMBER/locations/LOCATION_ID/endpoints/ENDPOINT_ID/operations/OPERATION_ID",
      "metadata": {
        "@type": "type.googleapis.com/google.cloud.aiplatform.v1.CreateEndpointOperationMetadata",
        "genericMetadata": {
          "createTime": "2020-11-05T17:45:42.812656Z",
          "updateTime": "2020-11-05T17:45:42.812656Z"
        }
      }
    }

You can poll for the status of the operation until the response includes `"done": true` .

### Terraform

The following sample uses the [`google_vertex_ai_endpoint`](https://registry.terraform.io/providers/hashicorp/google/latest/docs/resources/vertex_ai_endpoint) Terraform resource to create an endpoint.

To learn how to apply or remove a Terraform configuration, see [Basic Terraform commands](https://docs.cloud.google.com/docs/terraform/basic-commands) .

    # Endpoint name must be unique for the project
    resource "random_id" "endpoint_id" {
      byte_length = 4
    }
    
    resource "google_vertex_ai_endpoint" "default" {
      name         = substr(random_id.endpoint_id.dec, 0, 10)
      display_name = "sample-endpoint"
      description  = "A sample Vertex AI endpoint"
      location     = "us-central1"
      labels = {
        label-one = "value-one"
      }
    }

### Java

Before trying this sample, follow the Java setup instructions in the [Agent Platform quickstart using client libraries](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/start/client-libraries) .

To authenticate to Agent Platform, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

    import com.google.api.gax.longrunning.OperationFuture;
    import com.google.cloud.aiplatform.v1.CreateEndpointOperationMetadata;
    import com.google.cloud.aiplatform.v1.Endpoint;
    import com.google.cloud.aiplatform.v1.EndpointServiceClient;
    import com.google.cloud.aiplatform.v1.EndpointServiceSettings;
    import com.google.cloud.aiplatform.v1.LocationName;
    import java.io.IOException;
    import java.util.concurrent.ExecutionException;
    import java.util.concurrent.TimeUnit;
    import java.util.concurrent.TimeoutException;
    
    public class CreateEndpointSample {
    
      public static void main(String[] args)
          throws IOException, InterruptedException, ExecutionException, TimeoutException {
        // TODO(developer): Replace these variables before running the sample.
        String project = "YOUR_PROJECT_ID";
        String endpointDisplayName = "YOUR_ENDPOINT_DISPLAY_NAME";
        createEndpointSample(project, endpointDisplayName);
      }
    
      static void createEndpointSample(String project, String endpointDisplayName)
          throws IOException, InterruptedException, ExecutionException, TimeoutException {
        EndpointServiceSettings endpointServiceSettings =
            EndpointServiceSettings.newBuilder()
                .setEndpoint("us-central1-aiplatform.googleapis.com:443")
                .build();
    
        // Initialize client that will be used to send requests. This client only needs to be created
        // once, and can be reused for multiple requests. After completing all of your requests, call
        // the "close" method on the client to safely clean up any remaining background resources.
        try (EndpointServiceClient endpointServiceClient =
            EndpointServiceClient.create(endpointServiceSettings)) {
          String location = "us-central1";
          LocationName locationName = LocationName.of(project, location);
          Endpoint endpoint = Endpoint.newBuilder().setDisplayName(endpointDisplayName).build();
    
          OperationFuture<Endpoint, CreateEndpointOperationMetadata> endpointFuture =
              endpointServiceClient.createEndpointAsync(locationName, endpoint);
          System.out.format("Operation name: %s\n", endpointFuture.getInitialFuture().get().getName());
          System.out.println("Waiting for operation to finish...");
          Endpoint endpointResponse = endpointFuture.get(300, TimeUnit.SECONDS);
    
          System.out.println("Create Endpoint Response");
          System.out.format("Name: %s\n", endpointResponse.getName());
          System.out.format("Display Name: %s\n", endpointResponse.getDisplayName());
          System.out.format("Description: %s\n", endpointResponse.getDescription());
          System.out.format("Labels: %s\n", endpointResponse.getLabelsMap());
          System.out.format("Create Time: %s\n", endpointResponse.getCreateTime());
          System.out.format("Update Time: %s\n", endpointResponse.getUpdateTime());
        }
      }
    }

### Node.js

Before trying this sample, follow the Node.js setup instructions in the [Agent Platform quickstart using client libraries](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/start/client-libraries) .

To authenticate to Agent Platform, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

    /**
     * TODO(developer): Uncomment these variables before running the sample.\
     * (Not necessary if passing values as arguments)
     */
    
    // const endpointDisplayName = 'YOUR_ENDPOINT_DISPLAY_NAME';
    // const project = 'YOUR_PROJECT_ID';
    // const location = 'YOUR_PROJECT_LOCATION';
    
    // Imports the Google Cloud Endpoint Service Client library
    const {EndpointServiceClient} = require('@google-cloud/aiplatform');
    
    // Specifies the location of the api endpoint
    const clientOptions = {
      apiEndpoint: 'us-central1-aiplatform.googleapis.com',
    };
    
    // Instantiates a client
    const endpointServiceClient = new EndpointServiceClient(clientOptions);
    
    async function createEndpoint() {
      // Configure the parent resource
      const parent = `projects/${project}/locations/${location}`;
      const endpoint = {
        displayName: endpointDisplayName,
      };
      const request = {
        parent,
        endpoint,
      };
    
      // Get and print out a list of all the endpoints for this resource
      const [response] = await endpointServiceClient.createEndpoint(request);
      console.log(`Long running operation : ${response.name}`);
    
      // Wait for operation to complete
      await response.promise();
      const result = response.result;
    
      console.log('Create endpoint response');
      console.log(`\tName : ${result.name}`);
      console.log(`\tDisplay name : ${result.displayName}`);
      console.log(`\tDescription : ${result.description}`);
      console.log(`\tLabels : ${JSON.stringify(result.labels)}`);
      console.log(`\tCreate time : ${JSON.stringify(result.createTime)}`);
      console.log(`\tUpdate time : ${JSON.stringify(result.updateTime)}`);
    }
    createEndpoint();

### Python

To learn how to install or update the Vertex AI SDK for Python, see [Install the Vertex AI SDK for Python](https://docs.cloud.google.com/vertex-ai/docs/start/use-vertex-ai-python-sdk) . For more information, see the [Python API reference documentation](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest) .

    def create_endpoint_sample(
        project: str,
        display_name: str,
        location: str,
    ):
        aiplatform.init(project=project, location=location)
    
        endpoint = aiplatform.Endpoint.create(
            display_name=display_name,
            project=project,
            location=location,
        )
    
        print(endpoint.display_name)
        print(endpoint.resource_name)
        return endpoint

## What's next

  - [Deploy a model by using the gcloud CLI or Gemini Enterprise API](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/deploy-model-api) .
  - Learn how to [get an online inference](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/get-online-predictions) .
