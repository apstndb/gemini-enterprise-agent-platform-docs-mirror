---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tabular-data/classification-regression/get-online-predictions
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tabular-data/classification-regression/get-online-predictions
title: Get online inferences for AutoML models
description: Get online (real-time) inferences and explanations from your AutoML tabular classification or regression models in Agent Platform.
data_source: docs.cloud.google.com
---

This page shows you how to get online (real-time) inferences and explanations from your trained AutoML tabular classification or regression models using the Google Cloud console or the Agent Platform API.

An online inference is a synchronous request as opposed to a [batch inference](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tabular-data/classification-regression/get-batch-predictions) , which is an asynchronous request. Use online inferences when you make requests in response to application input or in other situations where you require timely inference.

You must [deploy a model](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tabular-data/classification-regression/get-online-predictions#deploy-model) to an endpoint before you can use that model to serve online inferences. Deploying a model associates physical resources with the model so it can serve online inferences with low latency.

The topics covered are:

1.  [Deploy a model](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tabular-data/classification-regression/get-online-predictions#deploy-model) to an endpoint
2.  Get an [online inference](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tabular-data/classification-regression/get-online-predictions#online-inference) using your deployed model
3.  Get an [online explanation](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tabular-data/classification-regression/get-online-predictions#online-explanation) using your deployed model

## Before you begin

Before you can get online inferences, you must first [train](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tabular-data/classification-regression/train-model) a classification or regression model and [evaluate](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tabular-data/classification-regression/evaluate-model) it for accuracy.

## Deploy a model to an endpoint

You can deploy more than one model to an endpoint, and you can deploy a model to more than one endpoint. For more information about options and use cases for deploying models, see [About deploying models](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/deployment) .

Use one of the following methods to deploy a model:

### Google Cloud console

1.  In the Google Cloud console, in the Agent Platform section, go to the **Models** page.

2.  Click the name of the model you want to deploy to open its details page.

3.  Select the **Deploy & Test** tab.
    
    If your model is already deployed to any endpoints, they are listed in the **Deploy your model** section.

4.  Click **Deploy to endpoint** .

5.  In the **Define your endpoint** page, configure as follows:
    
    1.  You can choose to deploy your model to a new endpoint or an existing endpoint.
        
          - To deploy your model to a new endpoint, select radio\_button\_checked **Create new endpoint** and provide a name for the new endpoint.
          - To deploy your model to an existing endpoint, select radio\_button\_checked **Add to existing endpoint** and select the endpoint from the drop-down list.
          - You can add more than one model to an endpoint, and you can add a model to more than one endpoint. [Learn more](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/deployment) .
    
    2.  Click **Continue** .

6.  In the **Model settings** page, configure as follows:
    
    1.  If you're deploying your model to a new endpoint, accept 100 for the **Traffic split** . If you're deploying your model to an existing endpoint that has one or more models deployed to it, you must update the **Traffic split** percentage for the model you are deploying and the already deployed models so that all of the percentages add up to 100%.
    
    2.  Enter the **Minimum number of compute nodes** you want to provide for your model.
        
        This is the number of nodes available to this model at all times. You are charged for the nodes used, whether to handle inference load or for standby (minimum) nodes, even without inference traffic. See the [pricing page](https://cloud.google.com/products/gemini-enterprise-agent-platform/pricing) .
    
    3.  Select your **Machine type** .
        
        Larger machine resources will increase your inference performance and increase costs.
    
    4.  Learn how to [change the default settings for inference logging](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/online-prediction-logging#enabling-and-disabling) .
    
    5.  Click **Continue**

7.  In the **Model monitoring** page, click **Continue** .

8.  In the **Monitoring objectives** page, configure as follows:
    
    1.  Enter the location of your training data.
    2.  Enter the name of the target column.

9.  Click **Deploy** to deploy your model to the endpoint.

### API

When you deploy a model using the Agent Platform API, you complete the following steps:

1.  Create an endpoint if needed.
2.  Get the endpoint ID.
3.  Deploy the model to the endpoint.

### Create an endpoint

If you are deploying a model to an existing endpoint, you can skip this step.

### gcloud

The following example uses the [`gcloud ai endpoints create` command](https://docs.cloud.google.com/sdk/gcloud/reference/ai/endpoints/create) :

``` 
  gcloud ai endpoints create \
    --region=LOCATION \
    --display-name=ENDPOINT_NAME
```

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

### Get the endpoint ID

You need the endpoint ID to deploy the model.

### gcloud

The following example uses the [`gcloud ai endpoints list` command](https://docs.cloud.google.com/sdk/gcloud/reference/ai/endpoints/list) :

``` 
  gcloud ai endpoints list \
    --region=LOCATION \
    --filter=display_name=ENDPOINT_NAME
```

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

The following example deploys a `Model` to an `Endpoint` without using GPUs to accelerate prediction serving and without splitting traffic between multiple `DeployedModel` resources:

Before using any of the command data below, make the following replacements:

  - ENDPOINT\_ID : The ID for the endpoint.
  - LOCATION\_ID : The region where you are using Agent Platform.
  - MODEL\_ID : The ID for the model to be deployed.
  - DEPLOYED\_MODEL\_NAME : A name for the `DeployedModel` . You can use the display name of the `Model` for the `DeployedModel` as well.
  - MACHINE\_TYPE : Optional. The machine resources used for each node of this deployment. Its default setting is `n1-standard-2` . [Learn more about machine types.](https://docs.cloud.google.com/gemini-enterprise-agent-platform/predictions/configure-compute)
  - MIN\_REPLICA\_COUNT : The minimum number of nodes for this deployment. The node count can be increased or decreased as required by the inference load, up to the maximum number of nodes and never fewer than this number of nodes. This value must be greater than or equal to 1. If the `--min-replica-count` flag is omitted, the value defaults to 1.
  - MAX\_REPLICA\_COUNT : The maximum number of nodes for this deployment. The node count can be increased or decreased as required by the inference load, up to this number of nodes and never fewer than the minimum number of nodes. If you omit the `--max-replica-count` flag, then maximum number of nodes is set to the value of `--min-replica-count` .

Execute the [gcloud ai endpoints deploy-model](https://docs.cloud.google.com/sdk/gcloud/reference/ai/endpoints/deploy-model) command:

#### Linux, macOS, or Cloud Shell

> **Note:** Ensure you have initialized the Google Cloud CLI with authentication and a project by running either [gcloud init](https://docs.cloud.google.com/sdk/gcloud/reference/init) ; or [gcloud auth login](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) and [gcloud config set project](https://docs.cloud.google.com/sdk/gcloud/reference/config/set) .

    gcloud ai endpoints deploy-model ENDPOINT_ID\
      --region=LOCATION_ID \
      --model=MODEL_ID \
      --display-name=DEPLOYED_MODEL_NAME \
      --machine-type=MACHINE_TYPE \
      --min-replica-count=MIN_REPLICA_COUNT \
      --max-replica-count=MAX_REPLICA_COUNT \
      --traffic-split=0=100

#### Windows (PowerShell)

> **Note:** Ensure you have initialized the Google Cloud CLI with authentication and a project by running either [gcloud init](https://docs.cloud.google.com/sdk/gcloud/reference/init) ; or [gcloud auth login](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) and [gcloud config set project](https://docs.cloud.google.com/sdk/gcloud/reference/config/set) .

    gcloud ai endpoints deploy-model ENDPOINT_ID`
      --region=LOCATION_ID `
      --model=MODEL_ID `
      --display-name=DEPLOYED_MODEL_NAME `
      --machine-type=MACHINE_TYPE `
      --min-replica-count=MIN_REPLICA_COUNT `
      --max-replica-count=MAX_REPLICA_COUNT `
      --traffic-split=0=100

#### Windows (cmd.exe)

> **Note:** Ensure you have initialized the Google Cloud CLI with authentication and a project by running either [gcloud init](https://docs.cloud.google.com/sdk/gcloud/reference/init) ; or [gcloud auth login](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) and [gcloud config set project](https://docs.cloud.google.com/sdk/gcloud/reference/config/set) .

    gcloud ai endpoints deploy-model ENDPOINT_ID^
      --region=LOCATION_ID ^
      --model=MODEL_ID ^
      --display-name=DEPLOYED_MODEL_NAME ^
      --machine-type=MACHINE_TYPE ^
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
      --machine-type=MACHINE_TYPE \
      --min-replica-count=MIN_REPLICA_COUNT \
      --max-replica-count=MAX_REPLICA_COUNT \
      --traffic-split=0=20,OLD_DEPLOYED_MODEL_ID=80

#### Windows (PowerShell)

> **Note:** Ensure you have initialized the Google Cloud CLI with authentication and a project by running either [gcloud init](https://docs.cloud.google.com/sdk/gcloud/reference/init) ; or [gcloud auth login](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) and [gcloud config set project](https://docs.cloud.google.com/sdk/gcloud/reference/config/set) .

    gcloud ai endpoints deploy-model ENDPOINT_ID`
      --region=LOCATION_ID `
      --model=MODEL_ID `
      --display-name=DEPLOYED_MODEL_NAME \ 
      --machine-type=MACHINE_TYPE `
      --min-replica-count=MIN_REPLICA_COUNT `
      --max-replica-count=MAX_REPLICA_COUNT `
      --traffic-split=0=20,OLD_DEPLOYED_MODEL_ID=80

#### Windows (cmd.exe)

> **Note:** Ensure you have initialized the Google Cloud CLI with authentication and a project by running either [gcloud init](https://docs.cloud.google.com/sdk/gcloud/reference/init) ; or [gcloud auth login](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) and [gcloud config set project](https://docs.cloud.google.com/sdk/gcloud/reference/config/set) .

    gcloud ai endpoints deploy-model ENDPOINT_ID^
      --region=LOCATION_ID ^
      --model=MODEL_ID ^
      --display-name=DEPLOYED_MODEL_NAME \ 
      --machine-type=MACHINE_TYPE ^
      --min-replica-count=MIN_REPLICA_COUNT ^
      --max-replica-count=MAX_REPLICA_COUNT ^
      --traffic-split=0=20,OLD_DEPLOYED_MODEL_ID=80

### REST

You use the [endpoints.predict](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.endpoints/predict) method to request an online inference.

Deploy the model.

Before using any of the request data, make the following replacements:

  - LOCATION\_ID : The region where you are using Agent Platform.
  - PROJECT\_ID : .
  - ENDPOINT\_ID : The ID for the endpoint.
  - MODEL\_ID : The ID for the model to be deployed.
  - DEPLOYED\_MODEL\_NAME : A name for the `DeployedModel` . You can use the display name of the `Model` for the `DeployedModel` as well.
  - MACHINE\_TYPE : Optional. The machine resources used for each node of this deployment. Its default setting is `n1-standard-2` . [Learn more about machine types.](https://docs.cloud.google.com/gemini-enterprise-agent-platform/predictions/configure-compute)
  - ACCELERATOR\_TYPE : The type of accelerator to be attached to the machine. Optional if ACCELERATOR\_COUNT is not specified or is zero. Not recommended for AutoML models or custom-trained models that are using non-GPU images. [Learn more](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/configure-compute#gpus) .
  - ACCELERATOR\_COUNT : The number of accelerators for each replica to use. Optional. Should be zero or unspecified for AutoML models or custom-trained models that are using non-GPU images.
  - MIN\_REPLICA\_COUNT : The minimum number of nodes for this deployment. The node count can be increased or decreased as required by the inference load, up to the maximum number of nodes and never fewer than this number of nodes. This value must be greater than or equal to 1.
  - MAX\_REPLICA\_COUNT : The maximum number of nodes for this deployment. The node count can be increased or decreased as required by the inference load, up to this number of nodes and never fewer than the minimum number of nodes.
  - REQUIRED\_REPLICA\_COUNT : Optional. The required number of nodes for this deployment to be marked as successful. Must be greater than or equal to 1 and fewer than or equal to the minimum number of nodes. If not specified, the default value is the minimum number of nodes.
  - TRAFFIC\_SPLIT\_THIS\_MODEL : The percentage of the prediction traffic to this endpoint to be routed to the model being deployed with this operation. Defaults to 100. All traffic percentages must add up to 100. [Learn more about traffic splits](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/deployment#models-endpoint) .
  - DEPLOYED\_MODEL\_ID\_N : Optional. If other models are deployed to this endpoint, you must update their traffic split percentages so that all percentages add up to 100.
  - TRAFFIC\_SPLIT\_MODEL\_N : The traffic split percentage value for the deployed model id key.
  - PROJECT\_NUMBER : Your project's automatically generated [project number](https://docs.cloud.google.com/resource-manager/docs/creating-managing-projects#identifiers)

HTTP method and URL:

    POST https://LOCATION_ID-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION_ID/endpoints/ENDPOINT_ID:deployModel

Request JSON body:

    {
      "deployedModel": {
        "model": "projects/PROJECT/locations/us-central1/models/MODEL_ID",
        "displayName": "DEPLOYED_MODEL_NAME",
        "dedicatedResources": {
           "machineSpec": {
             "machineType": "MACHINE_TYPE",
             "acceleratorType": "ACCELERATOR_TYPE",
             "acceleratorCount": "ACCELERATOR_COUNT"
           },
           "minReplicaCount": MIN_REPLICA_COUNT,
           "maxReplicaCount": MAX_REPLICA_COUNT,
           "requiredReplicaCount": REQUIRED_REPLICA_COUNT
         },
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
      "name": "projects/PROJECT_ID/locations/LOCATION/endpoints/ENDPOINT_ID/operations/OPERATION_ID",
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
    import com.google.cloud.aiplatform.v1.DedicatedResources;
    import com.google.cloud.aiplatform.v1.DeployModelOperationMetadata;
    import com.google.cloud.aiplatform.v1.DeployModelResponse;
    import com.google.cloud.aiplatform.v1.DeployedModel;
    import com.google.cloud.aiplatform.v1.EndpointName;
    import com.google.cloud.aiplatform.v1.EndpointServiceClient;
    import com.google.cloud.aiplatform.v1.EndpointServiceSettings;
    import com.google.cloud.aiplatform.v1.MachineSpec;
    import com.google.cloud.aiplatform.v1.ModelName;
    import java.io.IOException;
    import java.util.HashMap;
    import java.util.Map;
    import java.util.concurrent.ExecutionException;
    
    public class DeployModelCustomTrainedModelSample {
    
      public static void main(String[] args)
          throws IOException, ExecutionException, InterruptedException {
        // TODO(developer): Replace these variables before running the sample.
        String project = "PROJECT";
        String endpointId = "ENDPOINT_ID";
        String modelName = "MODEL_NAME";
        String deployedModelDisplayName = "DEPLOYED_MODEL_DISPLAY_NAME";
        deployModelCustomTrainedModelSample(project, endpointId, modelName, deployedModelDisplayName);
      }
    
      static void deployModelCustomTrainedModelSample(
          String project, String endpointId, String model, String deployedModelDisplayName)
          throws IOException, ExecutionException, InterruptedException {
        EndpointServiceSettings settings =
            EndpointServiceSettings.newBuilder()
                .setEndpoint("us-central1-aiplatform.googleapis.com:443")
                .build();
        String location = "us-central1";
    
        // Initialize client that will be used to send requests. This client only needs to be created
        // once, and can be reused for multiple requests. After completing all of your requests, call
        // the "close" method on the client to safely clean up any remaining background resources.
        try (EndpointServiceClient client = EndpointServiceClient.create(settings)) {
          MachineSpec machineSpec = MachineSpec.newBuilder().setMachineType("n1-standard-2").build();
          DedicatedResources dedicatedResources =
              DedicatedResources.newBuilder().setMinReplicaCount(1).setMachineSpec(machineSpec).build();
    
          String modelName = ModelName.of(project, location, model).toString();
          DeployedModel deployedModel =
              DeployedModel.newBuilder()
                  .setModel(modelName)
                  .setDisplayName(deployedModelDisplayName)
                  // `dedicated_resources` must be used for non-AutoML models
                  .setDedicatedResources(dedicatedResources)
                  .build();
          // key '0' assigns traffic for the newly deployed model
          // Traffic percentage values must add up to 100
          // Leave dictionary empty if endpoint should not accept any traffic
          Map<String, Integer> trafficSplit = new HashMap<>();
          trafficSplit.put("0", 100);
          EndpointName endpoint = EndpointName.of(project, location, endpointId);
          OperationFuture<DeployModelResponse, DeployModelOperationMetadata> response =
              client.deployModelAsync(endpoint, deployedModel, trafficSplit);
    
          // You can use OperationFuture.getInitialFuture to get a future representing the initial
          // response to the request, which contains information while the operation is in progress.
          System.out.format("Operation name: %s\n", response.getInitialFuture().get().getName());
    
          // OperationFuture.get() will block until the operation is finished.
          DeployModelResponse deployModelResponse = response.get();
          System.out.format("deployModelResponse: %s\n", deployModelResponse);
        }
      }
    }

### Python

To learn how to install or update the Vertex AI SDK for Python, see [Install the Vertex AI SDK for Python](https://docs.cloud.google.com/vertex-ai/docs/start/use-vertex-ai-python-sdk) . For more information, see the [Python API reference documentation](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest) .

    def deploy_model_with_dedicated_resources_sample(
        project,
        location,
        model_name: str,
        machine_type: str,
        endpoint: Optional[aiplatform.Endpoint] = None,
        deployed_model_display_name: Optional[str] = None,
        traffic_percentage: Optional[int] = 0,
        traffic_split: Optional[Dict[str, int]] = None,
        min_replica_count: int = 1,
        max_replica_count: int = 1,
        accelerator_type: Optional[str] = None,
        accelerator_count: Optional[int] = None,
        explanation_metadata: Optional[explain.ExplanationMetadata] = None,
        explanation_parameters: Optional[explain.ExplanationParameters] = None,
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
    
        # The explanation_metadata and explanation_parameters should only be
        # provided for a custom trained model and not an AutoML model.
        model.deploy(
            endpoint=endpoint,
            deployed_model_display_name=deployed_model_display_name,
            traffic_percentage=traffic_percentage,
            traffic_split=traffic_split,
            machine_type=machine_type,
            min_replica_count=min_replica_count,
            max_replica_count=max_replica_count,
            accelerator_type=accelerator_type,
            accelerator_count=accelerator_count,
            explanation_metadata=explanation_metadata,
            explanation_parameters=explanation_parameters,
            metadata=metadata,
            sync=sync,
        )
    
        model.wait()
    
        print(model.display_name)
        print(model.resource_name)
        return model

### Node.js

Before trying this sample, follow the Node.js setup instructions in the [Agent Platform quickstart using client libraries](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/start/client-libraries) .

To authenticate to Agent Platform, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

    const automl = require('@google-cloud/automl');
    const client = new automl.v1beta1.AutoMlClient();
    
    /**
     * Demonstrates using the AutoML client to create a model.
     * TODO(developer): Uncomment the following lines before running the sample.
     */
    // const projectId = '[PROJECT_ID]' e.g., "my-gcloud-project";
    // const computeRegion = '[REGION_NAME]' e.g., "us-central1";
    // const datasetId = '[DATASET_ID]' e.g., "TBL2246891593778855936";
    // const tableId = '[TABLE_ID]' e.g., "1991013247762825216";
    // const columnId = '[COLUMN_ID]' e.g., "773141392279994368";
    // const modelName = '[MODEL_NAME]' e.g., "testModel";
    // const trainBudget = '[TRAIN_BUDGET]' e.g., "1000",
    // `Train budget in milli node hours`;
    
    // A resource that represents Google Cloud Platform location.
    const projectLocation = client.locationPath(projectId, computeRegion);
    
    // Get the full path of the column.
    const columnSpecId = client.columnSpecPath(
      projectId,
      computeRegion,
      datasetId,
      tableId,
      columnId
    );
    
    // Set target column to train the model.
    const targetColumnSpec = {name: columnSpecId};
    
    // Set tables model metadata.
    const tablesModelMetadata = {
      targetColumnSpec: targetColumnSpec,
      trainBudgetMilliNodeHours: trainBudget,
    };
    
    // Set datasetId, model name and model metadata for the dataset.
    const myModel = {
      datasetId: datasetId,
      displayName: modelName,
      tablesModelMetadata: tablesModelMetadata,
    };
    
    // Create a model with the model metadata in the region.
    client
      .createModel({parent: projectLocation, model: myModel})
      .then(responses => {
        const initialApiResponse = responses[1];
        console.log(`Training operation name: ${initialApiResponse.name}`);
        console.log('Training started...');
      })
      .catch(err => {
        console.error(err);
      });

Learn how to [change the default settings for inference logging](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/online-prediction-logging#enabling-and-disabling) .

### Get operation status

Some requests start long-running operations that require time to complete. These requests return an operation name, which you can use to view the operation's status or cancel the operation. Agent Platform provides helper methods to make calls against long-running operations. For more information, see [Working with long-running operations](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/long-running-operations) .

## Get an online inference using your deployed model

To make an online inference, submit one or more test items to a model for analysis, and the model returns results that are based on your model's objective. Use the Google Cloud console or the Agent Platform API to request an online inference.

### Google Cloud console

1.  In the Google Cloud console, in the Agent Platform section, go to the **Models** page.

2.  From the list of models, click the name of the model to request inferences from.

3.  Select the **Deploy & test** tab.

4.  Under the **Test your model** section, add test items to request an inference. The baseline inference data is filled in for you, or you can enter your own inference data and click **Predict** .
    
    After the inference is complete, Gemini Enterprise Agent Platform returns the results in the console.

### API: Classification

### gcloud

1.  Create a file named `request.json` with the following contents:
    
    ``` 
          {
      "instances": [
        {
          PREDICTION_DATA_ROW
        }
      ]
    }
        
    ```
    
    Replace the following:
    
      - PREDICTION\_DATA\_ROW : A JSON object with keys as the feature names and values as the corresponding feature values. For example, for a dataset with three features - a number, an array of strings, and a category - the row of data might look like the following example request:
        
            "length":3.6,
            "material":"cotton",
            "tag_array": ["abc","def"]
        
        A value must be provided for every feature included in training. The format of the data used for inference must match the format used for training. Refer to [Data format for inferences](https://docs.cloud.google.com/gemini-enterprise-agent-platform/datasets/data-types-tabular#format-for-prediction) for details.

2.  Run the following command:
    
        gcloud ai endpoints predict ENDPOINT_ID \
          --region=LOCATION_ID \
          --json-request=request.json
    
    Replace the following:
    
      - ENDPOINT\_ID : The ID for the endpoint.
      - LOCATION\_ID : The region where you are using Agent Platform.

### REST

You use the [endpoints.predict](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.endpoints/predict) method to request an online inference.

Before using any of the request data, make the following replacements:

  - LOCATION\_ID : Region where Endpoint is located. For example, `us-central1` .

  - PROJECT\_ID : .

  - ENDPOINT\_ID : The ID for the endpoint.

  - PREDICTION\_DATA\_ROW : A JSON object with keys as the feature names and values as the corresponding feature values. For example, for a dataset with three features - a number, an array of strings, and a category - the row of data might look like the following example request:
    
        "length":3.6,
        "material":"cotton",
        "tag_array": ["abc","def"]
    
    A value must be provided for every feature included in training. The format of the data used for inference must match the format used for training. Refer to [Data format for inferences](https://docs.cloud.google.com/gemini-enterprise-agent-platform/datasets/data-types-tabular#format-for-prediction) for details.

  - DEPLOYED\_MODEL\_ID : Output by the `predict` method, and accepted as input by the `explain` method. The ID of the model used to generate the inference. If you need to request explanations for a previously requested inference, and you have more than one model deployed, you can use this ID to ensure that the explanations are returned for the same model that provided the previous inference.

HTTP method and URL:

    POST https://LOCATION_ID-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION_ID/endpoints/ENDPOINT_ID:predict

Request JSON body:

    {
      "instances": [
        {
          PREDICTION_DATA_ROW
        }
      ]
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

``` 
   {
     "predictions": [
      {
         "scores": [
           0.96771615743637085,
           0.032283786684274673
         ],
         "classes": [
           "0",
           "1"
         ]
      }
     ]
     "deployedModelId": "2429510197"
   }
   
```

### Java

Before trying this sample, follow the Java setup instructions in the [Agent Platform quickstart using client libraries](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/start/client-libraries) .

To authenticate to Agent Platform, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

    import com.google.cloud.aiplatform.util.ValueConverter;
    import com.google.cloud.aiplatform.v1.EndpointName;
    import com.google.cloud.aiplatform.v1.PredictResponse;
    import com.google.cloud.aiplatform.v1.PredictionServiceClient;
    import com.google.cloud.aiplatform.v1.PredictionServiceSettings;
    import com.google.cloud.aiplatform.v1.schema.predict.prediction.TabularClassificationPredictionResult;
    import com.google.protobuf.ListValue;
    import com.google.protobuf.Value;
    import com.google.protobuf.util.JsonFormat;
    import java.io.IOException;
    import java.util.List;
    
    public class PredictTabularClassificationSample {
    
      public static void main(String[] args) throws IOException {
        // TODO(developer): Replace these variables before running the sample.
        String project = "YOUR_PROJECT_ID";
        String instance = "[{ “feature_column_a”: “value”, “feature_column_b”: “value”}]";
        String endpointId = "YOUR_ENDPOINT_ID";
        predictTabularClassification(instance, project, endpointId);
      }
    
      static void predictTabularClassification(String instance, String project, String endpointId)
          throws IOException {
        PredictionServicPredictionServiceSettingsceSettings =
            PredictionServicPredictionServiceSettings          .setEndpoint("us-central1-aiplatform.googleapis.com:443")
                .build();
    
        // Initialize client that will be used to send requests. This client only needs to be created
        // once, and can be reused for multiple requests. After completing all of your requests, call
        // the "close" method on the client to safely clean up any remaining background resources.
        try (PredictionServicPredictionServiceClientceClient =
            PredictionServicPredictionServiceClientonServiceSettings)) {
          String location = "us-central1";
          EndpointName endEndpointNameEndpointName.of(EndpointNameation, endpointId);
    
          ListValue.BuildeListValueue = ListValue.newBuiListValue     JsonFormat.parseJsonFormatinstance, listValue);
          List<Value> instanListValuelistValue.getValuesList();
    
          Value parametersValuelue.newBuilderValuetListValue(listValue).build();
          PredictResponse PredictResponse =
              predictionServiceClient.predict(endpointName, instanceList, parameters);
          System.out.println("Predict Tabular Classification Response");
          System.out.format("\tDeployed Model Id: %s\n", predictResponse.predictResponse.getDeployedModelId().out.println("Predictions");
          for (Value predictionValueedictResponse.predictResponse.getPredictionsList()larClassificTabularClassificationPredictionResultuilder =
                TabularClassificTabularClassificationPredictionResult       TabularClassificTabularClassificationPredictionResult      (TabularClassificTabularClassificationPredictionResult  ValueConverter.fValueConvertertBuilder, prediction);
    
            for (int i = 0; i < result.getClasseresult.getClassesCount()   System.out.printf("\tClass: %s", result.getClasseresult.getClasses(i)tem.out.printf("\tScore: %f", result.getScoresresult.getScores(i)   }
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
    
    // const endpointId = 'YOUR_ENDPOINT_ID';
    // const project = 'YOUR_PROJECT_ID';
    // const location = 'YOUR_PROJECT_LOCATION';
    const aiplatform = require('@google-cloud/aiplatform');
    const {prediction} =
      aiplatform.protos.google.cloud.aiplatform.v1.schema.predict;
    
    // Imports the Google Cloud Prediction service client
    const {PredictionServiceClient} = aiplatform.v1;
    
    // Import the helper module for converting arbitrary protobuf.Value objects.
    const {helpers} = aiplatform;
    
    // Specifies the location of the api endpoint
    const clientOptions = {
      apiEndpoint: 'us-central1-aiplatform.googleapis.com',
    };
    
    // Instantiates a client
    const predictionServiceClient = new PredictionServiceClient(clientOptions);
    
    async function predictTablesClassification() {
      // Configure the endpoint resource
      const endpoint = `projects/${project}/locations/${location}/endpoints/${endpointId}`;
      const parameters = helpers.toValue({});
    
      const instance = helpers.toValue({
        petal_length: '1.4',
        petal_width: '1.3',
        sepal_length: '5.1',
        sepal_width: '2.8',
      });
    
      const instances = [instance];
      const request = {
        endpoint,
        instances,
        parameters,
      };
    
      // Predict request
      const [response] = await predictionServiceClient.predict(request);
    
      console.log('Predict tabular classification response');
      console.log(`\tDeployed model id : ${response.deployedModelId}\n`);
      const predictions = response.predictions;
      console.log('Predictions :');
      for (const predictionResultVal of predictions) {
        const predictionResultObj =
          prediction.TabularClassificationPredictionResult.fromValue(
            predictionResultVal
          );
        for (const [i, class_] of predictionResultObj.classes.entries()) {
          console.log(`\tClass: ${class_}`);
          console.log(`\tScore: ${predictionResultObj.scores[i]}\n\n`);
        }
      }
    }
    predictTablesClassification();

### Python

To learn how to install or update the Vertex AI SDK for Python, see [Install the Vertex AI SDK for Python](https://docs.cloud.google.com/vertex-ai/docs/start/use-vertex-ai-python-sdk) . For more information, see the [Python API reference documentation](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest) .

    def predict_tabular_classification_sample(
        project: str,
        location: str,
        endpoint_name: str,
        instances: List[Dict],
    ):
        """
        Args
            project: Your project ID or project number.
            location: Region where Endpoint is located. For example, 'us-central1'.
            endpoint_name: A fully qualified endpoint name or endpoint ID. Example: "projects/123/locations/us-central1/endpoints/456" or
                   "456" when project and location are initialized or passed.
            instances: A list of one or more instances (examples) to return a prediction for.
        """
        aiplatform.init(project=project, location=location)
    
        endpoint = aiplatform.Endpoint(endpoint_name)
    
        response = endpoint.predict(instances=instances)
    
        for prediction_ in response.predictions:
            print(prediction_)

### API: Regression

### gcloud

1.  Create a file named \`request.json\` with the following contents:
    
    ``` 
          {
      "instances": [
        {
          PREDICTION_DATA_ROW
        }
      ]
    }
        
    ```
    
    Replace the following:
    
      - PREDICTION\_DATA\_ROW : A JSON object with keys as the feature names and values as the corresponding feature values. For example, for a dataset with three features - a number, an array of numbers, and a category - the row of data might look like the following example request:
        
            "age":3.6,
            "sq_ft":5392,
            "code": "90331"
        
        A value must be provided for every feature included in training. The format of the data used for inference must match the format used for training. Refer to [Data format for inferences](https://docs.cloud.google.com/gemini-enterprise-agent-platform/datasets/data-types-tabular#format-for-prediction) for details.

2.  Run the following command:
    
        gcloud ai endpoints predict ENDPOINT_ID \
          --region=LOCATION_ID \
          --json-request=request.json
    
    Replace the following:
    
      - ENDPOINT\_ID : The ID for the endpoint.
      - LOCATION\_ID : The region where you are using Agent Platform.

### REST

You use the [endpoints.predict](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.endpoints/predict) method to request an online inference.

Before using any of the request data, make the following replacements:

  - LOCATION\_ID : Region where Endpoint is located. For example, `us-central1` .

  - PROJECT\_ID : .

  - ENDPOINT\_ID : The ID for the endpoint.

  - PREDICTION\_DATA\_ROW : A JSON object with keys as the feature names and values as the corresponding feature values. For example, for a dataset with three features - a number, an array of numbers, and a category - the row of data might look like the following example request:
    
        "age":3.6,
        "sq_ft":5392,
        "code": "90331"
    
    A value must be provided for every feature included in training. The format of the data used for inference must match the format used for training. Refer to [Data format for inferences](https://docs.cloud.google.com/gemini-enterprise-agent-platform/datasets/data-types-tabular#format-for-prediction) for details.

  - DEPLOYED\_MODEL\_ID : Output by the `predict` method, and accepted as input by the `explain` method. The ID of the model used to generate the inference. If you need to request explanations for a previously requested inference, and you have more than one model deployed, you can use this ID to ensure that the explanations are returned for the same model that provided the previous inference.

HTTP method and URL:

    POST https://LOCATION_ID-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION_ID/endpoints/ENDPOINT_ID:predict

Request JSON body:

    {
      "instances": [
        {
          PREDICTION_DATA_ROW
        }
      ]
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
        [
          {
            "value": 65.14233,
            "lower_bound": 4.6572,
            "upper_bound": 164.0279
          }
        ]
      ],
      "deployedModelId": "DEPLOYED_MODEL_ID"
    }

### Java

Before trying this sample, follow the Java setup instructions in the [Agent Platform quickstart using client libraries](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/start/client-libraries) .

To authenticate to Agent Platform, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

    import com.google.cloud.aiplatform.util.ValueConverter;
    import com.google.cloud.aiplatform.v1.EndpointName;
    import com.google.cloud.aiplatform.v1.PredictResponse;
    import com.google.cloud.aiplatform.v1.PredictionServiceClient;
    import com.google.cloud.aiplatform.v1.PredictionServiceSettings;
    import com.google.cloud.aiplatform.v1.schema.predict.prediction.TabularRegressionPredictionResult;
    import com.google.protobuf.ListValue;
    import com.google.protobuf.Value;
    import com.google.protobuf.util.JsonFormat;
    import java.io.IOException;
    import java.util.List;
    
    public class PredictTabularRegressionSample {
    
      public static void main(String[] args) throws IOException {
        // TODO(developer): Replace these variables before running the sample.
        String project = "YOUR_PROJECT_ID";
        String instance = "[{ “feature_column_a”: “value”, “feature_column_b”: “value”}]";
        String endpointId = "YOUR_ENDPOINT_ID";
        predictTabularRegression(instance, project, endpointId);
      }
    
      static void predictTabularRegression(String instance, String project, String endpointId)
          throws IOException {
        PredictionServicPredictionServiceSettingsceSettings =
            PredictionServicPredictionServiceSettings          .setEndpoint("us-central1-aiplatform.googleapis.com:443")
                .build();
    
        // Initialize client that will be used to send requests. This client only needs to be created
        // once, and can be reused for multiple requests. After completing all of your requests, call
        // the "close" method on the client to safely clean up any remaining background resources.
        try (PredictionServicPredictionServiceClientceClient =
            PredictionServicPredictionServiceClientonServiceSettings)) {
          String location = "us-central1";
          EndpointName endEndpointNameEndpointName.of(EndpointNameation, endpointId);
    
          ListValue.BuildeListValueue = ListValue.newBuiListValue     JsonFormat.parseJsonFormatinstance, listValue);
          List<Value> instanListValuelistValue.getValuesList();
    
          Value parametersValuelue.newBuilderValuetListValue(listValue).build();
          PredictResponse PredictResponse =
              predictionServiceClient.predict(endpointName, instanceList, parameters);
          System.out.println("Predict Tabular Regression Response");
          System.out.format("\tDisplay Model Id: %s\n", predictResponse.predictResponse.getDeployedModelId().out.println("Predictions");
          for (Value predictionValueedictResponse.predictResponse.getPredictionsList()larRegressioTabularRegressionPredictionResultuilder =
                TabularRegressioTabularRegressionPredictionResult        TabularRegressioTabularRegressionPredictionResult      (TabularRegressioTabularRegressionPredictionResult.fValueConvertertBuilder, prediction);
    
            System.out.printf("\tUpper bound: %f\n", result.getUpperBresult.getUpperBound()m.out.printf("\tLower bound: %f\n", result.getLowerBresult.getLowerBound()m.out.printf("\tValue: %f\n", result.getValue(result.getValue()
      }
    }

### Node.js

Before trying this sample, follow the Node.js setup instructions in the [Agent Platform quickstart using client libraries](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/start/client-libraries) .

To authenticate to Agent Platform, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

    /**
     * TODO(developer): Uncomment these variables before running the sample.\
     * (Not necessary if passing values as arguments)
     */
    
    // const endpointId = 'YOUR_ENDPOINT_ID';
    // const project = 'YOUR_PROJECT_ID';
    // const location = 'YOUR_PROJECT_LOCATION';
    const aiplatform = require('@google-cloud/aiplatform');
    const {prediction} =
      aiplatform.protos.google.cloud.aiplatform.v1.schema.predict;
    
    // Imports the Google Cloud Prediction service client
    const {PredictionServiceClient} = aiplatform.v1;
    
    // Import the helper module for converting arbitrary protobuf.Value objects.
    const {helpers} = aiplatform;
    
    // Specifies the location of the api endpoint
    const clientOptions = {
      apiEndpoint: 'us-central1-aiplatform.googleapis.com',
    };
    
    // Instantiates a client
    const predictionServiceClient = new PredictionServiceClient(clientOptions);
    
    async function predictTablesRegression() {
      // Configure the endpoint resource
      const endpoint = `projects/${project}/locations/${location}/endpoints/${endpointId}`;
      const parameters = helpers.toValue({});
    
      // TODO (erschmid): Make this less painful
      const instance = helpers.toValue({
        BOOLEAN_2unique_NULLABLE: false,
        DATETIME_1unique_NULLABLE: '2019-01-01 00:00:00',
        DATE_1unique_NULLABLE: '2019-01-01',
        FLOAT_5000unique_NULLABLE: 1611,
        FLOAT_5000unique_REPEATED: [2320, 1192],
        INTEGER_5000unique_NULLABLE: '8',
        NUMERIC_5000unique_NULLABLE: 16,
        STRING_5000unique_NULLABLE: 'str-2',
        STRUCT_NULLABLE: {
          BOOLEAN_2unique_NULLABLE: false,
          DATE_1unique_NULLABLE: '2019-01-01',
          DATETIME_1unique_NULLABLE: '2019-01-01 00:00:00',
          FLOAT_5000unique_NULLABLE: 1308,
          FLOAT_5000unique_REPEATED: [2323, 1178],
          FLOAT_5000unique_REQUIRED: 3089,
          INTEGER_5000unique_NULLABLE: '1777',
          NUMERIC_5000unique_NULLABLE: 3323,
          TIME_1unique_NULLABLE: '23:59:59.999999',
          STRING_5000unique_NULLABLE: 'str-49',
          TIMESTAMP_1unique_NULLABLE: '1546387199999999',
        },
        TIMESTAMP_1unique_NULLABLE: '1546387199999999',
        TIME_1unique_NULLABLE: '23:59:59.999999',
      });
    
      const instances = [instance];
      const request = {
        endpoint,
        instances,
        parameters,
      };
    
      // Predict request
      const [response] = await predictionServiceClient.predict(request);
    
      console.log('Predict tabular regression response');
      console.log(`\tDeployed model id : ${response.deployedModelId}`);
      const predictions = response.predictions;
      console.log('\tPredictions :');
      for (const predictionResultVal of predictions) {
        const predictionResultObj =
          prediction.TabularRegressionPredictionResult.fromValue(
            predictionResultVal
          );
        console.log(`\tUpper bound: ${predictionResultObj.upper_bound}`);
        console.log(`\tLower bound: ${predictionResultObj.lower_bound}`);
        console.log(`\tLower bound: ${predictionResultObj.value}`);
      }
    }
    predictTablesRegression();

### Python

To learn how to install or update the Vertex AI SDK for Python, see [Install the Vertex AI SDK for Python](https://docs.cloud.google.com/vertex-ai/docs/start/use-vertex-ai-python-sdk) . For more information, see the [Python API reference documentation](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest) .

    def predict_tabular_regression_sample(
        project: str,
        location: str,
        endpoint_name: str,
        instances: List[Dict],
    ):
        aiplatform.init(project=project, location=location)
    
        endpoint = aiplatform.Endpoint(endpoint_name)
    
        response = endpoint.predict(instances=instances)
    
        for prediction_ in response.predictions:
            print(prediction_)

## Interpret prediction results

### Classification

Classification models return a confidence score.

The confidence score communicates how strongly your model associates each class or label with a test item. The higher the number, the higher the model's confidence that the label should be applied to that item. You decide how high the confidence score must be for you to accept the model's results.

### Regression

Regression models return an inference value. For BigQuery destinations, they also return a inference interval. The inference interval provides a range of values that the model has 95% confidence contain the actual result.

## Get an online explanation using your deployed model

You can request an inference with explanations (also called feature attributions) to see how your model arrived at an inference. The local feature importance values tell you how much each feature contributed to the inference result. Feature attributions are included in Agent Platform inferences through [Vertex Explainable AI](https://docs.cloud.google.com/gemini-enterprise-agent-platform/tabular-data/classification-explanations) .

### Console

When you use the Google Cloud console to request an online inference, the local feature importance values are automatically returned.

If you used the pre-filled prediction values, the local feature importance values are all zero. This is because the pre-filled values are the baseline prediction data, so the prediction returned is the baseline prediction value.

> **Note:** You might need to scroll the parameter window to the right to see the local feature importance results.

### gcloud

1.  Create a file named `request.json` with the following contents:
    
        {
          "instances": [
            {
              PREDICTION_DATA_ROW
            }
          ]
        }
    
    Replace the following:
    
      - PREDICTION\_DATA\_ROW : A JSON object with keys as the feature names and values as the corresponding feature values. For example, for a dataset with three features - a number, an array of strings, and a category - the row of data might look like the following example request:
        
            "length":3.6,
            "material":"cotton",
            "tag_array": ["abc","def"]
        
        A value must be provided for every feature included in training. The format of the data used for inference must match the format used for training. Refer to [Data format for inferences](https://docs.cloud.google.com/gemini-enterprise-agent-platform/datasets/data-types-tabular#format-for-prediction) for details.

2.  Run the following command:
    
        gcloud ai endpoints explain ENDPOINT_ID \
          --region=LOCATION_ID \
          --json-request=request.json
    
    Replace the following:
    
      - ENDPOINT\_ID : The ID for the endpoint.
      - LOCATION\_ID : The region where you are using Agent Platform.
    
    Optionally, if you want to send an explanation request to a specific `DeployedModel` on the `Endpoint` , you can specify the `--deployed-model-id` flag:
    
        gcloud ai endpoints explain ENDPOINT_ID \
          --region=LOCATION \
          --deployed-model-id=DEPLOYED_MODEL_ID \
          --json-request=request.json
    
    In addition to the placeholders described previously, replace the following:
    
      - DEPLOYED\_MODEL\_ID Optional: The ID of the deployed model for which you want to get explanations. The ID is included in the `predict` method's response. If you need to request explanations for a particular model and you have more than one model deployed to the same endpoint, you can use this ID to ensure that the explanations are returned for that particular model.

### REST

The following example shows an online inference request for a tabular classification model with local feature attributions. The request format is the same for regression models.

Before using any of the request data, make the following replacements:

  - LOCATION : Region where Endpoint is located. For example, `us-central1` .

  - PROJECT : .

  - ENDPOINT\_ID : The ID for the endpoint.

  - PREDICTION\_DATA\_ROW : A JSON object with keys as the feature names and values as the corresponding feature values. For example, for a dataset with three features - a number, an array of strings, and a category - the row of data might look like the following example request:
    
        "length":3.6,
        "material":"cotton",
        "tag_array": ["abc","def"]
    
    A value must be provided for every feature included in training. The format of the data used for inference must match the format used for training. Refer to [Data format for inferences](https://docs.cloud.google.com/gemini-enterprise-agent-platform/datasets/data-types-tabular#format-for-prediction) for details.

  - DEPLOYED\_MODEL\_ID (optional): The ID of the deployed model for which you want to get explanations. The ID is included in the `predict` method's response. If you need to request explanations for a particular model and you have more than one model deployed to the same endpoint, you can use this ID to ensure that the explanations are returned for that particular model.

HTTP method and URL:

    POST https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT/locations/LOCATION/endpoints/ENDPOINT_ID:explain

Request JSON body:

    {
      "instances": [
        {
          PREDICTION_DATA_ROW
        }
      ],
      "deployedModelId": "DEPLOYED_MODEL_ID"
    }

To send your request, choose one of these options:

#### curl

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) , or by using [Cloud Shell](https://docs.cloud.google.com/shell/docs) , which automatically logs you into the `gcloud` CLI . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Save the request body in a file named `request.json` , and execute the following command:

    curl -X POST \
         -H "Authorization: Bearer $(gcloud auth print-access-token)" \
         -H "Content-Type: application/json; charset=utf-8" \
         -d @request.json \
         "https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT/locations/LOCATION/endpoints/ENDPOINT_ID:explain"

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
        -Uri "https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT/locations/LOCATION/endpoints/ENDPOINT_ID:explain" | Select-Object -Expand Content

### Python

To learn how to install or update the Vertex AI SDK for Python, see [Install the Vertex AI SDK for Python](https://docs.cloud.google.com/vertex-ai/docs/start/use-vertex-ai-python-sdk) . For more information, see the [Python API reference documentation](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest) .

    def explain_sample(project: str, location: str, endpoint_id: str, instance_dict: Dict):
    
        aiplatform.init(project=project, location=location)
    
        endpoint = aiplatform.Endpoint(endpoint_id)
    
        response = endpoint.explain(instances=[instance_dict], parameters={})
    
        for explanation in response.explanations:
            print(" explanation")
            # Feature attributions.
            attributions = explanation.attributions
            for attribution in attributions:
                print("  attribution")
                print("   baseline_output_value:", attribution.baseline_output_value)
                print("   instance_output_value:", attribution.instance_output_value)
                print("   output_display_name:", attribution.output_display_name)
                print("   approximation_error:", attribution.approximation_error)
                print("   output_name:", attribution.output_name)
                output_index = attribution.output_index
                for output_index in output_index:
                    print("   output_index:", output_index)
    
        for prediction in response.predictions:
            print(prediction)

*Get explanations for a previously returned prediction*

Because explanations increase resource usage, you might want to reserve requesting explanations for situations when you specifically need them. Sometimes, it can be helpful to request explanations for an inference result you've already received, perhaps because the inference was an outlier or did not make sense.

If all of your inferences are coming from the same model, you can simply resend the request data, with explanations requested this time. However, if you have multiple models returning inferences, you must make sure you send the explanation request to the correct model. You can view explanations for a particular model by including the deployed model's ID `deployedModelID` in your request, which is included in the response of the original inference request. Note that the deployed model ID is different from the model ID.

## Interpret explanation results

To calculate local feature importance, first the *baseline inference score* is calculated. Baseline values are computed from the training data, using the median value for numeric features and the mode for categorical features. The inference generated from the baseline values is the *baseline inference score* . Baseline values are calculated once for a model and do not change.

For a specific inference, the local feature importance for each feature tells you how much that feature added to or subtracted from the result as compared with the baseline inference score. The sum of all of the feature importance values equals the difference between the baseline inference score and the inference result.

For classification models, the score is always between 0.0 and 1.0, inclusive. Therefore, local feature importance values for classification models are always between -1.0 and 1.0 (inclusive).

For examples of feature attribution queries and to learn more, see [Feature Attributions for Classification and Regression](https://docs.cloud.google.com/gemini-enterprise-agent-platform/tabular-data/classification-explanations) .

## Example output for inferences and explanations

### Classification

The return payload for an online inference from a tabular classification model with feature importance looks similar to the following example.

The `instanceOutputValue` of `0.928652400970459` is the confidence score of the highest-scoring class, in this case `class_a` . The `baselineOutputValue` field contains the baseline inference score, `0.808652400970459` . The feature that contributed most strongly to this result was `feature_3` .

    {
    "predictions": [
      {
        "scores": [
          0.928652400970459,
          0.071347599029541
        ],
        "classes": [
          "class_a",
          "class_b"
        ]
      }
    ]
    "explanations": [
      {
        "attributions": [
          {
            "baselineOutputValue": 0.808652400970459,
            "instanceOutputValue": 0.928652400970459,
            "approximationError":  0.0058915703929231,
            "featureAttributions": {
              "feature_1": 0.012394922231235,
              "feature_2": 0.050212341234556,
              "feature_3": 0.057392736534209,
            },
            "outputIndex": [
              0
            ],
            "outputName": "scores"
          }
        ],
      }
    ]
    "deployedModelId": "234567"
    }

### Regression

The return payload for an online inference with feature importance from a AutoML tabular regression model looks similar to the following example.

The `instanceOutputValue` of `1795.1246466281819` is the predicted value, with the `lower_bound` and `upper_bound` fields providing the 95% confidence interval. The `baselineOutputValue` field contains the baseline inference score, `1788.7423095703125` . The feature that contributed most strongly to this result was `feature_3` .

    {
    "predictions": [
      {
        "value": 1795.1246466281819,
        "lower_bound": 246.32196807861328,
        "upper_bound": 8677.51904296875
      }
    ]
    "explanations": [
      {
        "attributions": [
          {
            "baselineOutputValue": 1788.7423095703125,
            "instanceOutputValue": 1795.1246466281819,
            "approximationError": 0.0038215703911553,
            "featureAttributions": {
              "feature_1": 0.123949222312359,
              "feature_2": 0.802123412345569,
              "feature_3": 5.456264423211472,
            },
            "outputIndex": [
              -1
            ]
          }
        ]
      }
    ],
    "deployedModelId": "345678"
    }

## What's next

  - Learn how to [export your model](https://docs.cloud.google.com/gemini-enterprise-agent-platform/export/export-model-tabular) .
