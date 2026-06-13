---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/deploy-model-api
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/deploy-model-api
title: Deploy a model by using the gcloud CLI or Gemini Enterprise API
description: Deploy a model to a public endpoint by using the gcloud CLI or Gemini Enterprise API.
data_source: docs.cloud.google.com
---

To deploy a model to a [public endpoint](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/create-public-endpoint) by using the gcloud CLI or Gemini Enterprise API, you need to get the endpoint ID for an existing endpoint and then deploy the model to it.

## Get the endpoint ID

You need the endpoint ID to deploy the model.

### gcloud

The following example uses the [`gcloud ai endpoints list` command](https://docs.cloud.google.com/sdk/gcloud/reference/ai/endpoints/list) :

``` 
  gcloud ai endpoints list \
      --region=LOCATION_ID \
      --filter=display_name=ENDPOINT_NAME
```

Replace the following:

  - LOCATION\_ID : The region where you are using Agent Platform.
  - ENDPOINT\_NAME : The display name for the endpoint.

Note the number that appears in the `ENDPOINT_ID` column. Use this ID in the following step.

### REST

Before using any of the request data, make the following replacements:

  - LOCATION\_ID : The region where you are using Agent Platform.
  - PROJECT\_ID : Your \[project ID\](/resource-manager/docs/creating-managing-projects\#identifiers). .
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

### Python

To learn how to install or update the Vertex AI SDK for Python, see [Install the Vertex AI SDK for Python](https://docs.cloud.google.com/vertex-ai/docs/start/use-vertex-ai-python-sdk) . For more information, see the [Python API reference documentation](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest) .

Replace the following:

  - PROJECT\_ID : Your project ID.
  - LOCATION\_ID : The region where you are using Agent Platform.
  - ENDPOINT\_NAME : The display name for the endpoint.

<!-- end list -->

    from google.cloud import aiplatform
    
    PROJECT_ID = "PROJECT_ID"
    LOCATION = "LOCATION_ID"
    ENDPOINT_NAME = "ENDPOINT_NAME"
    
    aiplatform.init(
        project=PROJECT_ID,
        location=LOCATION,
    )
    
    endpoint = aiplatform.Endpoint.list( filter='display_name=ENDPOINT_NAME', )
    endpoint_id = endpoint.name.split("/")[-1]

## Deploy the model

When you deploy a model, you give the deployed model an ID to distinguish it from other models deployed to the endpoint.

Select the tab below for your language or environment:

### gcloud

The following examples use the [`gcloud ai endpoints deploy-model` command](https://docs.cloud.google.com/sdk/gcloud/reference/ai/endpoints/deploy-model) .

The following example deploys a `Model` to an `Endpoint` without using GPUs to accelerate prediction serving and without splitting traffic between multiple `DeployedModel` resources:

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
  - PROJECT\_ID : Your \[project ID\](/resource-manager/docs/creating-managing-projects\#identifiers). .
  - ENDPOINT\_ID : The ID for the endpoint.
  - MODEL\_ID : The ID for the model to be deployed.
  - DEPLOYED\_MODEL\_NAME : A name for the `DeployedModel` . You can use the display name of the `Model` for the `DeployedModel` as well.
  - MACHINE\_TYPE : Optional. The machine resources used for each node of this deployment. Its default setting is `n1-standard-2` . [Learn more about machine types.](https://docs.cloud.google.com/vertex-ai/docs/predictions/configure-compute)
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

## Get operation status

Some requests start long-running operations that require time to complete. These requests return an operation name, which you can use to view the operation's status or cancel the operation. Agent Platform provides helper methods to make calls against long-running operations. For more information, see [Working with long-running operations](https://docs.cloud.google.com/gemini-enterprise-agent-platform/general/long-running-operations) .

## What's next

  - Learn how to [get an online inference](https://docs.cloud.google.com/vertex-ai/docs/predictions/get-online-predictions) .
  - Learn about [private endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/using-private-endpoints) .
