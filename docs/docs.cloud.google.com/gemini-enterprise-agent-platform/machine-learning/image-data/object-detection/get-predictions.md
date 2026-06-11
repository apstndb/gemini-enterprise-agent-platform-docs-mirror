---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/image-data/object-detection/get-predictions
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/image-data/object-detection/get-predictions
title: Get inferences from a image object detection model
description: Learn how to get inferences from an image object detection model.
data_source: docs.cloud.google.com
---

This page shows you how to get online (real-time) inferences and batch inferences from your image object detection models using the Google Cloud console or the Agent Platform API.

## Difference between online and batch inferences

Online inferences are synchronous requests made to a model endpoint. Use online inferences when you are making requests in response to application input or in situations that require timely inference.

Batch inferences are asynchronous requests. You request batch inferences directly from the model resource without needing to deploy the model to an endpoint. For image data, use batch inferences when you don't require an immediate response and want to process accumulated data by using a single request.

## Get online inferences

### Deploy a model to an endpoint

You must deploy a model to an endpoint before that model can be used to serve online inferences. Deploying a model associates physical resources with the model so it can serve online inferences with low latency.

You can deploy more than one model to an endpoint, and you can deploy a model to more than one endpoint. For more information about options and use cases for deploying models, see [About deploying models](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/deployment) .

Use one of the following methods to deploy a model:

### Google Cloud console

1.  In the Google Cloud console, in the Agent Platform section, go to the **Models** page.

2.  Click the name of the model you want to deploy to open its details page.

3.  Select the **Deploy & Test** tab.
    
    If your model is already deployed to any endpoints, they are listed in the **Deploy your model** section.

4.  Click **Deploy to endpoint** .

5.  To deploy your model to a new endpoint, select radio\_button\_checked **Create new endpoint** and provide a name for the new endpoint. To deploy your model to an existing endpoint, select radio\_button\_checked **Add to existing endpoint** and select the endpoint from the drop-down list.
    
    You can add more than one model to an endpoint, and you can add a model to more than one endpoint. [Learn more](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/deployment) .

6.  If you deploy your model to an existing endpoint that has one or more models deployed to it, you must update the **Traffic split** percentage for the model you are deploying and the already deployed models so that all of the percentages add up to 100%.

7.  Select **AutoML Image** and configure as follows:
    
    1.  If you're deploying your model to a new endpoint, accept 100 for the **Traffic split** . Otherwise, adjust the traffic split values for all models on the endpoint so they add up to 100.
    
    2.  Enter the **Number of compute nodes** you want to provide for your model.
        
        This is the number of nodes available to this model at all times. You are charged for the nodes, even without inference traffic. See the [pricing page](https://docs.cloud.google.com/gemini-enterprise-agent-platform/pricing) .
    
    3.  Learn how to [change the default settings for inference logging](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/online-prediction-logging#enabling-and-disabling) .
    
    4.  ***Classification** models only (optional)* : In the **Explainability options** section, select check\_box **Enable feature attributions for this model** to enable [Vertex Explainable AI](https://docs.cloud.google.com/vertex-ai/docs/explainable-ai/overview) . Accept existing [visualization settings](https://docs.cloud.google.com/vertex-ai/docs/explainable-ai/visualization-settings-automl-icn) or choose new values and click **Done** .
        
        Deploying AutoML image classification models with Vertex Explainable AI configured and performing inferences with explanations is optional. Enabling Vertex Explainable AI at deployment time incurs additional costs based on the deployed node count and deployment time. See [Pricing](https://docs.cloud.google.com/gemini-enterprise-agent-platform/pricing) for more information.
    
    5.  Click **Done** for your model, and when all the **Traffic split** percentages are correct, click **Continue** .
        
        The region where your model deploys is displayed. This must be the region where you created your model.
    
    6.  Click **Deploy** to deploy your model to the endpoint.

### API

When you deploy a model using the Agent Platform API, you complete the following steps:

1.  Create an endpoint if needed.
2.  Get the endpoint ID.
3.  Deploy the model to the endpoint.

### Create an endpoint

If you are deploying a model to an existing endpoint, you can skip this step.

### gcloud

The following example uses the [`gcloud ai endpoints create` command](https://docs.cloud.google.com/sdk/gcloud/reference/ai/endpoints/create) :

    gcloud ai endpoints create \
      --region=LOCATION \
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

### Retrieve the endpoint ID

You need the endpoint ID to deploy the model.

### gcloud

The following example uses the [`gcloud ai endpoints list` command](https://docs.cloud.google.com/sdk/gcloud/reference/ai/endpoints/list) :

    gcloud ai endpoints list \
      --region=LOCATION \
      --filter=display_name=ENDPOINT_NAME

Replace the following:

  - LOCATION\_ID : The region where you are using Agent Platform.
  - ENDPOINT\_NAME : The display name for the endpoint.

Note the number that appears in the `ENDPOINT_ID` column. Use this ID in the following step.

### REST

Before using any of the request data, make the following replacements:

  - LOCATION\_ID : The region where you are using Agent Platform.
  - PROJECT\_ID : .
  - ENDPOINT\_NAME : The display name for the endpoint.

HTTP method and URL:

    GET https://LOCATION_ID-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION_ID/endpoints?filter=display_name=ENDPOINT_NAME

To send your request, expand one of these options:

#### curl (Linux, macOS, or Cloud Shell)

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) , or by using [Cloud Shell](https://docs.cloud.google.com/shell/docs) , which automatically logs you into the `gcloud` CLI . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Execute the following command:

    curl -X GET \
         -H "Authorization: Bearer $(gcloud auth print-access-token)" \
         "https://LOCATION_ID-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION_ID/endpoints?filter=display_name=ENDPOINT_NAME"

#### PowerShell (Windows)

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Execute the following command:

    $cred = gcloud auth print-access-token
    $headers = @{ "Authorization" = "Bearer $cred" }
    
    Invoke-WebRequest `
        -Method GET `
        -Headers $headers `
        -Uri "https://LOCATION_ID-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION_ID/endpoints?filter=display_name=ENDPOINT_NAME" | Select-Object -Expand Content

You should receive a JSON response similar to the following:

    {
      "endpoints": [
        {
          "name": "projects/PROJECT_NUMBER/locations/LOCATION_ID/endpoints/ENDPOINT_ID",
          "displayName": "ENDPOINT_NAME",
          "etag": "AMEw9yPz5pf4PwBHbRWOGh0PcAxUdjbdX2Jm3QO_amguy3DbZGP5Oi_YUKRywIE-BtLx",
          "createTime": "2020-04-17T18:31:11.585169Z",
          "updateTime": "2020-04-17T18:35:08.568959Z"
        }
      ]
    }

Note the ENDPOINT\_ID .

### Deploy the model

Select the tab below for your language or environment:

### gcloud

The following examples use the [`gcloud ai endpoints deploy-model` command](https://docs.cloud.google.com/sdk/gcloud/reference/ai/endpoints/deploy-model) .

The following example deploys a `Model` to an `Endpoint` without splitting traffic between multiple `DeployedModel` resources:

Before using any of the command data below, make the following replacements:

  - ENDPOINT\_ID : The ID for the endpoint.
  - LOCATION\_ID : The region where you are using Agent Platform.
  - MODEL\_ID : The ID for the model to be deployed.
  - DEPLOYED\_MODEL\_NAME : A name for the `DeployedModel` . You can use the display name of the `Model` for the `DeployedModel` as well.
  - MIN\_REPLICA\_COUNT : The minimum number of nodes for this deployment. The node count can be increased or decreased as required by the inference load, up to the maximum number of nodes and never fewer than this number of nodes.
  - MAX\_REPLICA\_COUNT : The maximum number of nodes for this deployment. The node count can be increased or decreased as required by the inference load, up to this number of nodes and never fewer than the minimum number of nodes. If you omit the `--max-replica-count` flag, then maximum number of nodes is set to the value of `--min-replica-count` .

Execute the [gcloud ai endpoints deploy-model](https://docs.cloud.google.com/sdk/gcloud/reference/ai/endpoints/deploy-model) command:

#### Linux, macOS, or Cloud Shell

> **Note:** Ensure you have initialized the Google Cloud CLI with authentication and a project by running either [gcloud init](https://docs.cloud.google.com/sdk/gcloud/reference/init) ; or [gcloud auth login](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) and [gcloud config set project](https://docs.cloud.google.com/sdk/gcloud/reference/config/set) .

    gcloud ai endpoints deploy-model ENDPOINT_ID\
      --region=LOCATION_ID \
      --model=MODEL_ID \
      --display-name=DEPLOYED_MODEL_NAME \
      --min-replica-count=MIN_REPLICA_COUNT \
      --max-replica-count=MAX_REPLICA_COUNT \
      --traffic-split=0=100

#### Windows (PowerShell)

> **Note:** Ensure you have initialized the Google Cloud CLI with authentication and a project by running either [gcloud init](https://docs.cloud.google.com/sdk/gcloud/reference/init) ; or [gcloud auth login](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) and [gcloud config set project](https://docs.cloud.google.com/sdk/gcloud/reference/config/set) .

    gcloud ai endpoints deploy-model ENDPOINT_ID`
      --region=LOCATION_ID `
      --model=MODEL_ID `
      --display-name=DEPLOYED_MODEL_NAME `
      --min-replica-count=MIN_REPLICA_COUNT `
      --max-replica-count=MAX_REPLICA_COUNT `
      --traffic-split=0=100

#### Windows (cmd.exe)

> **Note:** Ensure you have initialized the Google Cloud CLI with authentication and a project by running either [gcloud init](https://docs.cloud.google.com/sdk/gcloud/reference/init) ; or [gcloud auth login](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) and [gcloud config set project](https://docs.cloud.google.com/sdk/gcloud/reference/config/set) .

    gcloud ai endpoints deploy-model ENDPOINT_ID^
      --region=LOCATION_ID ^
      --model=MODEL_ID ^
      --display-name=DEPLOYED_MODEL_NAME ^
      --min-replica-count=MIN_REPLICA_COUNT ^
      --max-replica-count=MAX_REPLICA_COUNT ^
      --traffic-split=0=100

#### Splitting traffic

The `--traffic-split=0=100` flag in the preceding examples sends 100% of prediction traffic that the `Endpoint` receives to the new `DeployedModel` , which is represented by the temporary ID `0` . If your `Endpoint` already has other `DeployedModel` resources, then you can split traffic between the new `DeployedModel` and the old ones. For example, to send 20% of traffic to the new `DeployedModel` and 80% to an older one, run the following command.

Before using any of the command data below, make the following replacements:

  - OLD\_DEPLOYED\_MODEL\_ID : the ID of the existing `DeployedModel` .

Execute the [gcloud ai endpoints deploy-model](https://docs.cloud.google.com/sdk/gcloud/reference/ai/endpoints/deploy-model) command:

#### Linux, macOS, or Cloud Shell

> **Note:** Ensure you have initialized the Google Cloud CLI with authentication and a project by running either [gcloud init](https://docs.cloud.google.com/sdk/gcloud/reference/init) ; or [gcloud auth login](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) and [gcloud config set project](https://docs.cloud.google.com/sdk/gcloud/reference/config/set) .

    gcloud ai endpoints deploy-model ENDPOINT_ID\
      --region=LOCATION_ID \
      --model=MODEL_ID \
      --display-name=DEPLOYED_MODEL_NAME \ 
      --min-replica-count=MIN_REPLICA_COUNT \
      --max-replica-count=MAX_REPLICA_COUNT \
      --traffic-split=0=20,OLD_DEPLOYED_MODEL_ID=80

#### Windows (PowerShell)

> **Note:** Ensure you have initialized the Google Cloud CLI with authentication and a project by running either [gcloud init](https://docs.cloud.google.com/sdk/gcloud/reference/init) ; or [gcloud auth login](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) and [gcloud config set project](https://docs.cloud.google.com/sdk/gcloud/reference/config/set) .

    gcloud ai endpoints deploy-model ENDPOINT_ID`
      --region=LOCATION_ID `
      --model=MODEL_ID `
      --display-name=DEPLOYED_MODEL_NAME \ 
      --min-replica-count=MIN_REPLICA_COUNT `
      --max-replica-count=MAX_REPLICA_COUNT `
      --traffic-split=0=20,OLD_DEPLOYED_MODEL_ID=80

#### Windows (cmd.exe)

> **Note:** Ensure you have initialized the Google Cloud CLI with authentication and a project by running either [gcloud init](https://docs.cloud.google.com/sdk/gcloud/reference/init) ; or [gcloud auth login](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) and [gcloud config set project](https://docs.cloud.google.com/sdk/gcloud/reference/config/set) .

    gcloud ai endpoints deploy-model ENDPOINT_ID^
      --region=LOCATION_ID ^
      --model=MODEL_ID ^
      --display-name=DEPLOYED_MODEL_NAME \ 
      --min-replica-count=MIN_REPLICA_COUNT ^
      --max-replica-count=MAX_REPLICA_COUNT ^
      --traffic-split=0=20,OLD_DEPLOYED_MODEL_ID=80

### REST

Deploy the model.

Before using any of the request data, make the following replacements:

  - LOCATION\_ID : The region where you are using Agent Platform.
  - PROJECT\_ID : .
  - ENDPOINT\_ID : The ID for the endpoint.
  - MODEL\_ID : The ID for the model to be deployed.
  - DEPLOYED\_MODEL\_NAME : A name for the `DeployedModel` . You can use the display name of the `Model` for the `DeployedModel` as well.
  - MIN\_REPLICA\_COUNT : The minimum number of nodes for this deployment. The node count can be increased or decreased as required by the inference load, up to the maximum number of nodes and never fewer than this number of nodes.
  - MAX\_REPLICA\_COUNT : The maximum number of nodes for this deployment. The node count can be increased or decreased as required by the inference load, up to this number of nodes and never fewer than the minimum number of nodes.
  - TRAFFIC\_SPLIT\_THIS\_MODEL : The percentage of the prediction traffic to this endpoint to be routed to the model being deployed with this operation. Defaults to 100. All traffic percentages must add up to 100. [Learn more about traffic splits](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/deployment#models-endpoint) .
  - DEPLOYED\_MODEL\_ID\_N : Optional. If other models are deployed to this endpoint, you must update their traffic split percentages so that all percentages add up to 100.
  - TRAFFIC\_SPLIT\_MODEL\_N : The traffic split percentage value for the deployed model id key.
  - PROJECT\_NUMBER : Your project's automatically generated [project number](https://docs.cloud.google.com/resource-manager/docs/creating-managing-projects#identifiers)

HTTP method and URL:

    POST https://LOCATION_ID-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION_ID/endpoints/ENDPOINT_ID:deployModel

Request JSON body:

    {
      "deployedModel": {
        "model": "projects/PROJECT_ID/locations/LOCATION_ID/models/MODEL_ID",
        "displayName": "DEPLOYED_MODEL_NAME",
        "automaticResources": {
           "minReplicaCount": MIN_REPLICA_COUNT,
           "maxReplicaCount": MAX_REPLICA_COUNT
         }
      },
      "trafficSplit": {
        "0": TRAFFIC_SPLIT_THIS_MODEL,
        "DEPLOYED_MODEL_ID_1": TRAFFIC_SPLIT_MODEL_1,
        "DEPLOYED_MODEL_ID_2": TRAFFIC_SPLIT_MODEL_2
      },
    }

To send your request, expand one of these options:

#### curl (Linux, macOS, or Cloud Shell)

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) , or by using [Cloud Shell](https://docs.cloud.google.com/shell/docs) , which automatically logs you into the `gcloud` CLI . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Save the request body in a file named `request.json` , and execute the following command:

    curl -X POST \
         -H "Authorization: Bearer $(gcloud auth print-access-token)" \
         -H "Content-Type: application/json; charset=utf-8" \
         -d @request.json \
         "https://LOCATION_ID-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION_ID/endpoints/ENDPOINT_ID:deployModel"

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
        -Uri "https://LOCATION_ID-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION_ID/endpoints/ENDPOINT_ID:deployModel" | Select-Object -Expand Content

You should receive a JSON response similar to the following:

    {
      "name": "projects/PROJECT_ID/locations/LOCATION_ID/endpoints/ENDPOINT_ID/operations/OPERATION_ID",
      "metadata": {
        "@type": "type.googleapis.com/google.cloud.aiplatform.v1.DeployModelOperationMetadata",
        "genericMetadata": {
          "createTime": "2020-10-19T17:53:16.502088Z",
          "updateTime": "2020-10-19T17:53:16.502088Z"
        }
      }
    }

### Java

Before trying this sample, follow the Java setup instructions in the [Agent Platform quickstart using client libraries](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/start/client-libraries) .

To authenticate to Agent Platform, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

    import com.google.api.gax.longrunning.OperationFuture;
    import com.google.api.gax.longrunning.OperationTimedPollAlgorithm;
    import com.google.api.gax.retrying.RetrySettings;
    import com.google.cloud.aiplatform.v1.AutomaticResources;
    import com.google.cloud.aiplatform.v1.DedicatedResources;
    import com.google.cloud.aiplatform.v1.DeployModelOperationMetadata;
    import com.google.cloud.aiplatform.v1.DeployModelResponse;
    import com.google.cloud.aiplatform.v1.DeployedModel;
    import com.google.cloud.aiplatform.v1.EndpointName;
    import com.google.cloud.aiplatform.v1.EndpointServiceClient;
    import com.google.cloud.aiplatform.v1.EndpointServiceSettings;
    import com.google.cloud.aiplatform.v1.MachineSpec;
    import com.google.cloud.aiplatform.v1.ModelName;
    import com.google.cloud.aiplatform.v1.stub.EndpointServiceStubSettings;
    import java.io.IOException;
    import java.util.HashMap;
    import java.util.Map;
    import java.util.concurrent.ExecutionException;
    import java.util.concurrent.TimeUnit;
    import java.util.concurrent.TimeoutException;
    import org.threeten.bp.Duration;
    
    public class DeployModelSample {
    
      public static void main(String[] args)
          throws IOException, InterruptedException, ExecutionException, TimeoutException {
        // TODO(developer): Replace these variables before running the sample.
        String project = "YOUR_PROJECT_ID";
        String deployedModelDisplayName = "YOUR_DEPLOYED_MODEL_DISPLAY_NAME";
        String endpointId = "YOUR_ENDPOINT_NAME";
        String modelId = "YOUR_MODEL_ID";
        int timeout = 900;
        deployModelSample(project, deployedModelDisplayName, endpointId, modelId, timeout);
      }
    
      static void deployModelSample(
          String project,
          String deployedModelDisplayName,
          String endpointId,
          String modelId,
          int timeout)
          throws IOException, InterruptedException, ExecutionException, TimeoutException {
    
        // Set long-running operations (LROs) timeout
        final OperationTimedPollAlgorithm operationTimedPollAlgorithm =
            OperationTimedPollAlgorithm.create(
                RetrySettings.newBuilder()
                    .setInitialRetryDelay(Duration.ofMillis(5000L))
                    .setRetryDelayMultiplier(1.5)
                    .setMaxRetryDelay(Duration.ofMillis(45000L))
                    .setInitialRpcTimeout(Duration.ZERO)
                    .setRpcTimeoutMultiplier(1.0)
                    .setMaxRpcTimeout(Duration.ZERO)
                    .setTotalTimeout(Duration.ofSeconds(timeout))
                    .build());
    
        EndpointServiceStubSettings.Builder endpointServiceStubSettingsBuilder =
            EndpointServiceStubSettings.newBuilder();
        endpointServiceStubSettingsBuilder
            .deployModelOperationSettings()
            .setPollingAlgorithm(operationTimedPollAlgorithm);
        EndpointServiceStubSettings endpointStubSettings = endpointServiceStubSettingsBuilder.build();
        EndpointServiceSettings endpointServiceSettings =
            EndpointServiceSettings.create(endpointStubSettings);
        endpointServiceSettings =
            endpointServiceSettings.toBuilder()
                .setEndpoint("us-central1-aiplatform.googleapis.com:443")
                .build();
    
        // Initialize client that will be used to send requests. This client only needs to be created
        // once, and can be reused for multiple requests. After completing all of your requests, call
        // the "close" method on the client to safely clean up any remaining background resources.
        try (EndpointServiceClient endpointServiceClient =
            EndpointServiceClient.create(endpointServiceSettings)) {
          String location = "us-central1";
          EndpointName endpointName = EndpointName.of(project, location, endpointId);
          // key '0' assigns traffic for the newly deployed model
          // Traffic percentage values must add up to 100
          // Leave dictionary empty if endpoint should not accept any traffic
          Map<String, Integer> trafficSplit = new HashMap<>();
          trafficSplit.put("0", 100);
          ModelName modelName = ModelName.of(project, location, modelId);
          AutomaticResources automaticResourcesInput =
              AutomaticResources.newBuilder().setMinReplicaCount(1).setMaxReplicaCount(1).build();
          DeployedModel deployedModelInput =
              DeployedModel.newBuilder()
                  .setModel(modelName.toString())
                  .setDisplayName(deployedModelDisplayName)
                  .setAutomaticResources(automaticResourcesInput)
                  .build();
    
          OperationFuture<DeployModelResponse, DeployModelOperationMetadata> deployModelResponseFuture =
              endpointServiceClient.deployModelAsync(endpointName, deployedModelInput, trafficSplit);
          System.out.format(
              "Operation name: %s\n", deployModelResponseFuture.getInitialFuture().get().getName());
          System.out.println("Waiting for operation to finish...");
          DeployModelResponse deployModelResponse = deployModelResponseFuture.get(20, TimeUnit.MINUTES);
    
          System.out.println("Deploy Model Response");
          DeployedModel deployedModel = deployModelResponse.getDeployedModel();
          System.out.println("\tDeployed Model");
          System.out.format("\t\tid: %s\n", deployedModel.getId());
          System.out.format("\t\tmodel: %s\n", deployedModel.getModel());
          System.out.format("\t\tDisplay Name: %s\n", deployedModel.getDisplayName());
          System.out.format("\t\tCreate Time: %s\n", deployedModel.getCreateTime());
    
          DedicatedResources dedicatedResources = deployedModel.getDedicatedResources();
          System.out.println("\t\tDedicated Resources");
          System.out.format("\t\t\tMin Replica Count: %s\n", dedicatedResources.getMinReplicaCount());
    
          MachineSpec machineSpec = dedicatedResources.getMachineSpec();
          System.out.println("\t\t\tMachine Spec");
          System.out.format("\t\t\t\tMachine Type: %s\n", machineSpec.getMachineType());
          System.out.format("\t\t\t\tAccelerator Type: %s\n", machineSpec.getAcceleratorType());
          System.out.format("\t\t\t\tAccelerator Count: %s\n", machineSpec.getAcceleratorCount());
    
          AutomaticResources automaticResources = deployedModel.getAutomaticResources();
          System.out.println("\t\tAutomatic Resources");
          System.out.format("\t\t\tMin Replica Count: %s\n", automaticResources.getMinReplicaCount());
          System.out.format("\t\t\tMax Replica Count: %s\n", automaticResources.getMaxReplicaCount());
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
    
    // const modelId = "YOUR_MODEL_ID";
    // const endpointId = 'YOUR_ENDPOINT_ID';
    // const deployedModelDisplayName = 'YOUR_DEPLOYED_MODEL_DISPLAY_NAME';
    // const project = 'YOUR_PROJECT_ID';
    // const location = 'YOUR_PROJECT_LOCATION';
    
    const modelName = `projects/${project}/locations/${location}/models/${modelId}`;
    const endpoint = `projects/${project}/locations/${location}/endpoints/${endpointId}`;
    // Imports the Google Cloud Endpoint Service Client library
    const {EndpointServiceClient} = require('@google-cloud/aiplatform');
    
    // Specifies the location of the api endpoint:
    const clientOptions = {
      apiEndpoint: 'us-central1-aiplatform.googleapis.com',
    };
    
    // Instantiates a client
    const endpointServiceClient = new EndpointServiceClient(clientOptions);
    
    async function deployModel() {
      // Configure the parent resource
      // key '0' assigns traffic for the newly deployed model
      // Traffic percentage values must add up to 100
      // Leave dictionary empty if endpoint should not accept any traffic
      const trafficSplit = {0: 100};
      const deployedModel = {
        // format: 'projects/{project}/locations/{location}/models/{model}'
        model: modelName,
        displayName: deployedModelDisplayName,
        automaticResources: {minReplicaCount: 1, maxReplicaCount: 1},
      };
      const request = {
        endpoint,
        deployedModel,
        trafficSplit,
      };
    
      // Get and print out a list of all the endpoints for this resource
      const [response] = await endpointServiceClient.deployModel(request);
      console.log(`Long running operation : ${response.name}`);
    
      // Wait for operation to complete
      await response.promise();
      const result = response.result;
    
      console.log('Deploy model response');
      const modelDeployed = result.deployedModel;
      console.log('\tDeployed model');
      if (!modelDeployed) {
        console.log('\t\tId : {}');
        console.log('\t\tModel : {}');
        console.log('\t\tDisplay name : {}');
        console.log('\t\tCreate time : {}');
    
        console.log('\t\tDedicated resources');
        console.log('\t\t\tMin replica count : {}');
        console.log('\t\t\tMachine spec {}');
        console.log('\t\t\t\tMachine type : {}');
        console.log('\t\t\t\tAccelerator type : {}');
        console.log('\t\t\t\tAccelerator count : {}');
    
        console.log('\t\tAutomatic resources');
        console.log('\t\t\tMin replica count : {}');
        console.log('\t\t\tMax replica count : {}');
      } else {
        console.log(`\t\tId : ${modelDeployed.id}`);
        console.log(`\t\tModel : ${modelDeployed.model}`);
        console.log(`\t\tDisplay name : ${modelDeployed.displayName}`);
        console.log(`\t\tCreate time : ${modelDeployed.createTime}`);
    
        const dedicatedResources = modelDeployed.dedicatedResources;
        console.log('\t\tDedicated resources');
        if (!dedicatedResources) {
          console.log('\t\t\tMin replica count : {}');
          console.log('\t\t\tMachine spec {}');
          console.log('\t\t\t\tMachine type : {}');
          console.log('\t\t\t\tAccelerator type : {}');
          console.log('\t\t\t\tAccelerator count : {}');
        } else {
          console.log(
            `\t\t\tMin replica count : \
              ${dedicatedResources.minReplicaCount}`
          );
          const machineSpec = dedicatedResources.machineSpec;
          console.log('\t\t\tMachine spec');
          console.log(`\t\t\t\tMachine type : ${machineSpec.machineType}`);
          console.log(
            `\t\t\t\tAccelerator type : ${machineSpec.acceleratorType}`
          );
          console.log(
            `\t\t\t\tAccelerator count : ${machineSpec.acceleratorCount}`
          );
        }
    
        const automaticResources = modelDeployed.automaticResources;
        console.log('\t\tAutomatic resources');
        if (!automaticResources) {
          console.log('\t\t\tMin replica count : {}');
          console.log('\t\t\tMax replica count : {}');
        } else {
          console.log(
            `\t\t\tMin replica count : \
              ${automaticResources.minReplicaCount}`
          );
          console.log(
            `\t\t\tMax replica count : \
              ${automaticResources.maxReplicaCount}`
          );
        }
      }
    }
    deployModel();

### Python

To learn how to install or update the Vertex AI SDK for Python, see [Install the Vertex AI SDK for Python](https://docs.cloud.google.com/vertex-ai/docs/start/use-vertex-ai-python-sdk) . For more information, see the [Python API reference documentation](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest) .

    def deploy_model_with_automatic_resources_sample(
        project,
        location,
        model_name: str,
        endpoint: Optional[aiplatform.Endpoint] = None,
        deployed_model_display_name: Optional[str] = None,
        traffic_percentage: Optional[int] = 0,
        traffic_split: Optional[Dict[str, int]] = None,
        min_replica_count: int = 1,
        max_replica_count: int = 1,
        metadata: Optional[Sequence[Tuple[str, str]]] = (),
        sync: bool = True,
    ):
        """
        model_name: A fully-qualified model resource name or model ID.
              Example: "projects/123/locations/us-central1/models/456" or
              "456" when project and location are initialized or passed.
        """
    
        aiplatform.init(project=project, location=location)
    
        model = aiplatform.Model(model_name=model_name)
    
        model.deploy(
            endpoint=endpoint,
            deployed_model_display_name=deployed_model_display_name,
            traffic_percentage=traffic_percentage,
            traffic_split=traffic_split,
            min_replica_count=min_replica_count,
            max_replica_count=max_replica_count,
            metadata=metadata,
            sync=sync,
        )
    
        model.wait()
    
        print(model.display_name)
        print(model.resource_name)
        return model

Learn how to [change the default settings for inference logging](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/online-prediction-logging#enabling-and-disabling) .

## Get operation status

Some requests start long-running operations that require time to complete. These requests return an operation name, which you can use to view the operation's status or cancel the operation. Agent Platform provides helper methods to make calls against long-running operations. For more information, see [Working with long-running operations](https://docs.cloud.google.com/gemini-enterprise-agent-platform/general/long-running-operations) .

### Make an online inference using your deployed model

To make an online inference, submit one or more test items to a model for analysis, and the model returns results that are based on your model's objective. For more information about inference results, see the [Interpret results](https://docs.cloud.google.com/vertex-ai/docs/predictions/interpreting-results-automl) page.

### Console

Use the Google Cloud console to request an online inference. Your model must be deployed to an endpoint.

1.  In the Google Cloud console, in the Agent Platform section, go to the **Models** page.

2.  From the list of models, click the name of the model to request inferences from.

3.  Select the **Deploy & test** tab.

4.  Under the **Test your model** section, add test items to request an inference.
    
    AutoML models for image objectives require you to upload an image to request an inference.
    
    For information about local feature importance, see [Get explanations](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/image-data/object-detection/get-predictions#explanations-api) .
    
    After the inference is complete, Gemini Enterprise Agent Platform returns the results in the console.

### API

Use the Agent Platform API to request an online inference. Your model must be deployed to an endpoint.

Image data type objectives include classification and object detection.

**Edge model inference:** When you use AutoML image Edge models for inference, you must convert any non-JPEG inference file to a JPEG file before you send the inference request.

### gcloud

1.  Create a file named `request.json` with the following contents:
    
        {
          "instances": [{
            "content": "CONTENT"
          }],
          "parameters": {
            "confidenceThreshold": THRESHOLD_VALUE,
            "maxPredictions": MAX_PREDICTIONS
          }
        }
    
    Replace the following:
    
      - CONTENT : The [base64-encoded](https://docs.cloud.google.com/gemini-enterprise-agent-platform/tutorials/base64-encode) image content.
      - THRESHOLD\_VALUE Optional: The model returns only predictions that have confidence scores with at least this value.
      - MAX\_PREDICTIONS Optional: The model returns up to this many predictions with the highest confidence scores.

2.  Run the following command:
    
        gcloud ai endpoints predict ENDPOINT_ID \
          --region=LOCATION_ID \
          --json-request=request.json
    
    Replace the following:
    
      - ENDPOINT\_ID : The ID for the endpoint.
      - LOCATION\_ID : The region where you are using Agent Platform.

### REST

Before using any of the request data, make the following replacements:

  - LOCATION\_ID : Region where Endpoint is located. For example, `us-central1` .
  - PROJECT\_ID : .
  - ENDPOINT\_ID : The ID for the endpoint.
  - CONTENT : The [base64-encoded](https://docs.cloud.google.com/gemini-enterprise-agent-platform/tutorials/base64-encode) image content.
  - THRESHOLD\_VALUE Optional: The model returns only predictions that have confidence scores with at least this value.
  - MAX\_PREDICTIONS Optional: The model returns up to this many predictions with the highest confidence scores.

HTTP method and URL:

    POST https://LOCATION_ID-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION_ID/endpoints/ENDPOINT_ID:predict

Request JSON body:

    {
      "instances": [{
        "content": "CONTENT"
      }],
      "parameters": {
        "confidenceThreshold": THRESHOLD_VALUE,
        "maxPredictions": MAX_PREDICTIONS
      }
    }

To send your request, choose one of these options:

#### curl

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) , or by using [Cloud Shell](https://docs.cloud.google.com/shell/docs) , which automatically logs you into the `gcloud` CLI . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Save the request body in a file named `request.json` , and execute the following command:

    curl -X POST \
         -H "Authorization: Bearer $(gcloud auth print-access-token)" \
         -H "Content-Type: application/json; charset=utf-8" \
         -d @request.json \
         "https://LOCATION_ID-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION_ID/endpoints/ENDPOINT_ID:predict"

#### PowerShell

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Save the request body in a file named `request.json` , and execute the following command:

    $cred = gcloud auth print-access-token
    $headers = @{ "Authorization" = "Bearer $cred" }
    
    Invoke-WebRequest `
        -Method POST `
        -Headers $headers `
        -ContentType: "application/json; charset=utf-8" `
        -InFile request.json `
        -Uri "https://LOCATION_ID-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION_ID/endpoints/ENDPOINT_ID:predict" | Select-Object -Expand Content

You should receive a JSON response similar to the following:

    {
      "predictions": [
        {
          "confidences": [
            0.975873291,
            0.972160876,
            0.879488528,
            0.866532683,
            0.686478078
          ],
          "displayNames": [
            "Salad",
            "Salad",
            "Tomato",
            "Tomato",
            "Salad"
          ],
          "ids": [
            "7517774415476555776",
            "7517774415476555776",
            "2906088397049167872",
            "2906088397049167872",
            "7517774415476555776"
          ],
          "bboxes": [
            [
              0.0869686604,
              0.977020741,
              0.395135701,
              1
            ],
            [
              0,
              0.488701463,
              0.00157663226,
              0.512249
            ],
            [
              0.361617863,
              0.509664357,
              0.772928834,
              0.914706349
            ],
            [
              0.310678929,
              0.45781514,
              0.565507233,
              0.711237729
            ],
            [
              0.584359646,
              1,
              0.00116168708,
              0.130817384
            ]
          ]
        }
      ],
      "deployedModelId": "3860570043075002368"
    }

### Java

Before trying this sample, follow the Java setup instructions in the [Agent Platform quickstart using client libraries](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/start/client-libraries) .

To authenticate to Agent Platform, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

    import com.google.cloud.aiplatform.util.ValueConverter;
    import com.google.cloud.aiplatform.v1.EndpointName;
    import com.google.cloud.aiplatform.v1.PredictResponse;
    import com.google.cloud.aiplatform.v1.PredictionServiceClient;
    import com.google.cloud.aiplatform.v1.PredictionServiceSettings;
    import com.google.cloud.aiplatform.v1.schema.predict.instance.ImageObjectDetectionPredictionInstance;
    import com.google.cloud.aiplatform.v1.schema.predict.params.ImageObjectDetectionPredictionParams;
    import com.google.cloud.aiplatform.v1.schema.predict.prediction.ImageObjectDetectionPredictionResult;
    import com.google.protobuf.Value;
    import java.io.IOException;
    import java.nio.charset.StandardCharsets;
    import java.nio.file.Files;
    import java.nio.file.Paths;
    import java.util.ArrayList;
    import java.util.Base64;
    import java.util.List;
    
    public class PredictImageObjectDetectionSample {
    
      public static void main(String[] args) throws IOException {
        // TODO(developer): Replace these variables before running the sample.
        String project = "YOUR_PROJECT_ID";
        String fileName = "YOUR_IMAGE_FILE_PATH";
        String endpointId = "YOUR_ENDPOINT_ID";
        predictImageObjectDetection(project, fileName, endpointId);
      }
    
      static void predictImageObjectDetection(String project, String fileName, String endpointId)
          throws IOException {
        PredictionServiceSettings settings =
            PredictionServiceSettings.newBuilder()
                .setEndpoint("us-central1-aiplatform.googleapis.com:443")
                .build();
    
        // Initialize client that will be used to send requests. This client only needs to be created
        // once, and can be reused for multiple requests. After completing all of your requests, call
        // the "close" method on the client to safely clean up any remaining background resources.
        try (PredictionServiceClient predictionServiceClient =
            PredictionServiceClient.create(settings)) {
          String location = "us-central1";
          EndpointName endpointName = EndpointName.of(project, location, endpointId);
    
          byte[] contents = Base64.getEncoder().encode(Files.readAllBytes(Paths.get(fileName)));
          String content = new String(contents, StandardCharsets.UTF_8);
    
          ImageObjectDetectionPredictionParams params =
              ImageObjectDetectionPredictionParams.newBuilder()
                  .setConfidenceThreshold((float) (0.5))
                  .setMaxPredictions(5)
                  .build();
    
          ImageObjectDetectionPredictionInstance instance =
              ImageObjectDetectionPredictionInstance.newBuilder().setContent(content).build();
    
          List<Value> instances = new ArrayList<>();
          instances.add(ValueConverter.toValue(instance));
    
          PredictResponse predictResponse =
              predictionServiceClient.predict(endpointName, instances, ValueConverter.toValue(params));
          System.out.println("Predict Image Object Detection Response");
          System.out.format("\tDeployed Model Id: %s\n", predictResponse.getDeployedModelId());
    
          System.out.println("Predictions");
          for (Value prediction : predictResponse.getPredictionsList()) {
    
            ImageObjectDetectionPredictionResult.Builder resultBuilder =
                ImageObjectDetectionPredictionResult.newBuilder();
    
            ImageObjectDetectionPredictionResult result =
                (ImageObjectDetectionPredictionResult)
                    ValueConverter.fromValue(resultBuilder, prediction);
    
            for (int i = 0; i < result.getIdsCount(); i++) {
              System.out.printf("\tDisplay name: %s\n", result.getDisplayNames(i));
              System.out.printf("\tConfidences: %f\n", result.getConfidences(i));
              System.out.printf("\tIDs: %d\n", result.getIds(i));
              System.out.printf("\tBounding boxes: %s\n", result.getBboxes(i));
            }
          }
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
    
    // const filename = "YOUR_PREDICTION_FILE_NAME";
    // const endpointId = "YOUR_ENDPOINT_ID";
    // const project = 'YOUR_PROJECT_ID';
    // const location = 'YOUR_PROJECT_LOCATION';
    const aiplatform = require('@google-cloud/aiplatform');
    const {instance, params, prediction} =
      aiplatform.protos.google.cloud.aiplatform.v1.schema.predict;
    
    // Imports the Google Cloud Prediction Service Client library
    const {PredictionServiceClient} = aiplatform.v1;
    
    // Specifies the location of the api endpoint
    const clientOptions = {
      apiEndpoint: 'us-central1-aiplatform.googleapis.com',
    };
    
    // Instantiates a client
    const predictionServiceClient = new PredictionServiceClient(clientOptions);
    
    async function predictImageObjectDetection() {
      // Configure the endpoint resource
      const endpoint = `projects/${project}/locations/${location}/endpoints/${endpointId}`;
    
      const parametersObj = new params.ImageObjectDetectionPredictionParams({
        confidenceThreshold: 0.5,
        maxPredictions: 5,
      });
      const parameters = parametersObj.toValue();
    
      const fs = require('fs');
      const image = fs.readFileSync(filename, 'base64');
      const instanceObj = new instance.ImageObjectDetectionPredictionInstance({
        content: image,
      });
    
      const instanceVal = instanceObj.toValue();
      const instances = [instanceVal];
      const request = {
        endpoint,
        instances,
        parameters,
      };
    
      // Predict request
      const [response] = await predictionServiceClient.predict(request);
    
      console.log('Predict image object detection response');
      console.log(`\tDeployed model id : ${response.deployedModelId}`);
      const predictions = response.predictions;
      console.log('Predictions :');
      for (const predictionResultVal of predictions) {
        const predictionResultObj =
          prediction.ImageObjectDetectionPredictionResult.fromValue(
            predictionResultVal
          );
        for (const [i, label] of predictionResultObj.displayNames.entries()) {
          console.log(`\tDisplay name: ${label}`);
          console.log(`\tConfidences: ${predictionResultObj.confidences[i]}`);
          console.log(`\tIDs: ${predictionResultObj.ids[i]}`);
          console.log(`\tBounding boxes: ${predictionResultObj.bboxes[i]}\n\n`);
        }
      }
    }
    predictImageObjectDetection();

### Python

To learn how to install or update the Vertex AI SDK for Python, see [Install the Vertex AI SDK for Python](https://docs.cloud.google.com/vertex-ai/docs/start/use-vertex-ai-python-sdk) . For more information, see the [Python API reference documentation](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest) .

    import base64
    
    from google.cloud import aiplatform
    from google.cloud.aiplatform.gapic.schema import predict
    
    
    def predict_image_object_detection_sample(
        project: str,
        endpoint_id: str,
        filename: str,
        location: str = "us-central1",
        api_endpoint: str = "us-central1-aiplatform.googleapis.com",
    ):
        # The AI Platform services require regional API endpoints.
        client_options = {"api_endpoint": api_endpoint}
        # Initialize client that will be used to create and send requests.
        # This client only needs to be created once, and can be reused for multiple requests.
        client = aiplatform.gapic.PredictionServiceClient(client_options=client_options)
        with open(filename, "rb") as f:
            file_content = f.read()
    
        # The format of each instance should conform to the deployed model's prediction input schema.
        encoded_content = base64.b64encode(file_content).decode("utf-8")
        instance = predict.instance.ImageObjectDetectionPredictionInstance(
            content=encoded_content,
        ).to_value()
        instances = [instance]
        # See gs://google-cloud-aiplatform/schema/predict/params/image_object_detection_1.0.0.yaml for the format of the parameters.
        parameters = predict.params.ImageObjectDetectionPredictionParams(
            confidence_threshold=0.5,
            max_predictions=5,
        ).to_value()
        endpoint = client.endpoint_path(
            project=project, location=location, endpoint=endpoint_id
        )
        response = client.predict(
            endpoint=endpoint, instances=instances, parameters=parameters
        )
        print("response")
        print(" deployed_model_id:", response.deployed_model_id)
        # See gs://google-cloud-aiplatform/schema/predict/prediction/image_object_detection_1.0.0.yaml for the format of the predictions.
        predictions = response.predictions
        for prediction in predictions:
            print(" prediction:", dict(prediction))

## Get batch inferences

To make a batch inference request, you specify an input source and an output format where Gemini Enterprise Agent Platform stores inference results. Batch inferences for the AutoML image model type require an input [JSON Lines](https://jsonlines.org/) file and the name of a Cloud Storage bucket to store the output.

> **Note:** To minimize processing time when you use the Google Cloud console to create batch inferences, we recommend that you select input and output locations that are in the same region as your model. If you use the API to create batch inferences, send requests to a service endpoint (such as `https://us-central1-aiplatform.googleapis.com` ) that is in the same region or geographically close to your input and output locations.

### Input data requirements

The input for batch requests specifies the items to send to your model for inference. For image object detection models, you can use a JSON Lines file to specify a list of images to make inferences about and then store the JSON Lines file in a Cloud Storage bucket. The following sample shows a single line in an input JSON Lines file:

    {"content": "gs://sourcebucket/datasets/images/source_image.jpg", "mimeType": "image/jpeg"}

### Request a batch inference

For batch inference requests, you can use the Google Cloud console or the Agent Platform API. Depending on the number of input items that you've submitted, a batch inference task can take some time to complete.

### Google Cloud console

Use the Google Cloud console to request a batch inference.

1.  In the Google Cloud console, in the Agent Platform section, go to the **Batch predictions** page.

2.  Click **Create** to open the **New batch prediction** window and complete the following steps:
    
    1.  Enter a name for the batch inference.
    2.  For **Model name** , select the name of the model to use for this batch inference.
    3.  For **Source path** , specify the Cloud Storage location where your JSON Lines input file is located.
    4.  For the **Destination path** , specify a Cloud Storage location where the batch inference results are stored. The **Output** format is determined by your model's objective. AutoML models for image objectives output JSON Lines files.

### API

Use the Agent Platform API to send batch inference requests.

### REST

Before using any of the request data, make the following replacements:

  - LOCATION\_ID : Region where Model is stored and batch inference job is executed. For example, `us-central1` .
  - PROJECT\_ID :
  - BATCH\_JOB\_NAME : Display name for the batch job
  - MODEL\_ID : The ID for the model to use for making inferences
  - THRESHOLD\_VALUE (optional): Gemini Enterprise Agent Platform returns only inferences that have confidence scores with at least this value. The default is `0.0` .
  - MAX\_PREDICTIONS (optional): Gemini Enterprise Agent Platform returns up to this many inferences starting with the inferences that have highest confidence scores. The default is `10` .
  - URI : Cloud Storage URI where your input JSON Lines file is located.
  - BUCKET : Your Cloud Storage bucket
  - PROJECT\_NUMBER : Your project's automatically generated [project number](https://docs.cloud.google.com/resource-manager/docs/creating-managing-projects#identifiers)

HTTP method and URL:

    POST https://LOCATION_ID-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION_ID/batchPredictionJobs

Request JSON body:

    {
        "displayName": "BATCH_JOB_NAME",
        "model": "projects/PROJECT/locations/LOCATION/models/MODEL_ID",
        "modelParameters": {
          "confidenceThreshold": THRESHOLD_VALUE,
          "maxPredictions": MAX_PREDICTIONS
        },
        "inputConfig": {
            "instancesFormat": "jsonl",
            "gcsSource": {
                "uris": ["URI"],
            },
        },
        "outputConfig": {
            "predictionsFormat": "jsonl",
            "gcsDestination": {
                "outputUriPrefix": "OUTPUT_BUCKET",
            },
        },
    }

To send your request, choose one of these options:

#### curl

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) , or by using [Cloud Shell](https://docs.cloud.google.com/shell/docs) , which automatically logs you into the `gcloud` CLI . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Save the request body in a file named `request.json` , and execute the following command:

    curl -X POST \
         -H "Authorization: Bearer $(gcloud auth print-access-token)" \
         -H "Content-Type: application/json; charset=utf-8" \
         -d @request.json \
         "https://LOCATION_ID-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION_ID/batchPredictionJobs"

#### PowerShell

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Save the request body in a file named `request.json` , and execute the following command:

    $cred = gcloud auth print-access-token
    $headers = @{ "Authorization" = "Bearer $cred" }
    
    Invoke-WebRequest `
        -Method POST `
        -Headers $headers `
        -ContentType: "application/json; charset=utf-8" `
        -InFile request.json `
        -Uri "https://LOCATION_ID-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION_ID/batchPredictionJobs" | Select-Object -Expand Content

You should receive a JSON response similar to the following:

    {
      "name": "projects/PROJECT_NUMBER/locations/LOCATION_ID/batchPredictionJobs/BATCH_JOB_ID",
      "displayName": "BATCH_JOB_NAME",
      "model": "projects/PROJECT_ID/locations/LOCATION_ID/models/MODEL_ID",
      "inputConfig": {
        "instancesFormat": "jsonl",
        "gcsSource": {
          "uris": [
            "CONTENT"
          ]
        }
      },
      "outputConfig": {
        "predictionsFormat": "jsonl",
        "gcsDestination": {
          "outputUriPrefix": "BUCKET"
        }
      },
      "state": "JOB_STATE_PENDING",
      "createTime": "2020-05-30T02:58:44.341643Z",
      "updateTime": "2020-05-30T02:58:44.341643Z",
      "modelDisplayName": "MODEL_NAME",
      "modelObjective": "MODEL_OBJECTIVE"
    }

You can poll for the status of the batch job using the BATCH\_JOB\_ID until the job `state` is `JOB_STATE_SUCCEEDED` .

### Python

To learn how to install or update the Vertex AI SDK for Python, see [Install the Vertex AI SDK for Python](https://docs.cloud.google.com/vertex-ai/docs/start/use-vertex-ai-python-sdk) . For more information, see the [Python API reference documentation](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest) .

    def create_batch_prediction_job_sample(
        project: str,
        location: str,
        model_resource_name: str,
        job_display_name: str,
        gcs_source: Union[str, Sequence[str]],
        gcs_destination: str,
        sync: bool = True,
    ):
        aiplatform.init(project=project, location=location)
    
        my_model = aiplatform.Model(model_resource_name)
    
        batch_prediction_job = my_model.batch_predict(
            job_display_name=job_display_name,
            gcs_source=gcs_source,
            gcs_destination_prefix=gcs_destination,
            sync=sync,
        )
    
        batch_prediction_job.wait()
    
        print(batch_prediction_job.display_name)
        print(batch_prediction_job.resource_name)
        print(batch_prediction_job.state)
        return batch_prediction_job

### Retrieve batch inference results

Gemini Enterprise Agent Platform sends batch inference output to your specified destination.

When a batch inference task is complete, the output of the inference is stored in the Cloud Storage bucket that you specified in your request.

### Example batch inference results

The following an example batch inference results from a image object detection model.

**Important:** Bounding boxes are specified as:

`"bboxes": [ [xMin, xMax, yMin, yMax], ...]`

Where `xMin` and `xMax` are the minimum and maximum x values and `yMin` and `yMax` are the minimum and maximum y values respectively.

    {
      "instance": {"content": "gs://bucket/image.jpg", "mimeType": "image/jpeg"},
      "prediction": {
        "ids": [1, 2],
        "displayNames": ["cat", "dog"],
        "bboxes":  [
          [0.1, 0.2, 0.3, 0.4],
          [0.2, 0.3, 0.4, 0.5]
        ],
        "confidences": [0.7, 0.5]
      }
    }
