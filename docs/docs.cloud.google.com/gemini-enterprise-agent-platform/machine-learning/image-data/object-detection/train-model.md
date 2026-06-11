---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/image-data/object-detection/train-model
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/image-data/object-detection/train-model
title: Train an image object detection model
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

[Video](https://www.youtube.com/watch?v=d8FtBAxDZ9A)

This page shows you how to train an AutoML object detection model from an image dataset using either the Google Cloud console or the Agent Platform API.

## Train an AutoML model

### Google Cloud console

1.  In the Google Cloud console, in the Agent Platform section, go to the **Datasets** page.

2.  Click the name of the dataset you want to use to train your model to open its details page.

3.  Click **Train new model** .

4.  For the training method, select radio\_button\_checked **AutoML** .

5.  In the **Choose where to use the model** section, choose the model host location: radio\_button\_checked **Cloud** , radio\_button\_checked **Edge** , or radio\_button\_checked **Agent Platform Vision** .

6.  Click **Continue** .

7.  Enter a name for the model.

8.  If you want manually set how your training data is split, expand **Advanced options** and select a data split option. For more information, see [About data splits for AutoML models](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/ml-use) .

9.  Click **Start Training** .
    
    Model training can take many hours, depending on the size and complexity of your data and your training budget, if you specified one. You can close this tab and return to it later. You will receive an email when your model has completed training.

### API

Select the tab below for your language or environment:

### REST

Before using any of the request data, make the following replacements:

  - LOCATION : Region where dataset is located and Model is created. For example, `us-central1` .
  - PROJECT : Your \[project ID\](/resource-manager/docs/creating-managing-projects\#identifiers). .
  - TRAININGPIPELINE\_DISPLAYNAME : Required. A display name for the trainingPipeline.
  - DATASET\_ID : The ID number for the dataset to use for training.
  - `fractionSplit` : Optional. One of several possible ML use [split options](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.trainingPipelines#inputdataconfig) for your data. For `fractionSplit` , values must sum to 1. For example:
      - `{"trainingFraction": "0.7","validationFraction": "0.15","testFraction": "0.15"}`
  - MODEL\_DISPLAYNAME <sup>\*</sup> : A display name for the model uploaded (created) by the TrainingPipeline.
  - MODEL\_DESCRIPTION <sup>\*</sup> : A description for the model.
  - modelToUpload.labels <sup>\*</sup> : Any set of key-value pairs to organize your models. For example:
      - "env": "prod"
      - "tier": "backend"
  - MODELTYPE <sup>†</sup> : The type of Cloud-hosted model to train. The options are:
      - `CLOUD_1` - A model best tailored to be used within Google Cloud, and which *cannot* be exported. Compared to the CLOUD\_HIGH\_ACCURACY\_1 and CLOUD\_LOW\_LATENCY\_1 models above, it is expected to have higher prediction quality and lower latency.
      - `CLOUD_HIGH_ACCURACY_1` - A model best tailored to be used within Google Cloud, and which *cannot* be exported. This model is expected to have a higher latency, but should also have a higher prediction quality than other cloud models.
      - `CLOUD_LOW_LATENCY_1` - A model best tailored to be used within Google Cloud, and which cannot be exported. This model is expected to have a low latency, but may have lower prediction quality than other cloud models.
    Other model type options can be found in the [reference documentation](https://cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/google.cloud.aiplatform.v1/schema/trainingjob.definition#modeltype_1) .
  - NODE\_HOUR\_BUDGET <sup>†</sup> : The actual training cost will be equal or less than this value. For Cloud models the budget must be: 20,000 - 900,000 milli node hours (inclusive). The default value is 216,000 which represents one day in wall time, assuming 9 nodes are used.
  - PROJECT\_NUMBER : Your project's automatically generated [project number](https://docs.cloud.google.com/resource-manager/docs/creating-managing-projects#identifiers)

|    |                                                                                                    |
| -- | -------------------------------------------------------------------------------------------------- |
| \* | Schema file's description you specify in `trainingTaskDefinition` describes the use of this field. |
| †  | Schema file you specify in `trainingTaskDefinition` declares and describes this field.             |

HTTP method and URL:

    POST https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT/locations/LOCATION/trainingPipelines

Request JSON body:

    {
      "displayName": "TRAININGPIPELINE_DISPLAYNAME",
      "inputDataConfig": {
        "datasetId": "DATASET_ID",
        "fractionSplit": {
          "trainingFraction": "DECIMAL",
          "validationFraction": "DECIMAL",
          "testFraction": "DECIMAL"
        }
      },
      "modelToUpload": {
        "displayName": "MODEL_DISPLAYNAME",
        "description": "MODEL_DESCRIPTION",
        "labels": {
          "KEY": "VALUE"
        }
      },
      "trainingTaskDefinition": "gs://google-cloud-aiplatform/schema/trainingjob/definition/automl_image_object_detection_1.0.0.yaml",
      "trainingTaskInputs": {
        "modelType": ["MODELTYPE"],
        "budgetMilliNodeHours": NODE_HOUR_BUDGET
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
         "https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT/locations/LOCATION/trainingPipelines"

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
        -Uri "https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT/locations/LOCATION/trainingPipelines" | Select-Object -Expand Content

The response contains information about specifications as well as the TRAININGPIPELINE\_ID .

#### Response

    {
      "name": "projects/PROJECT_NUMBER/locations/LOCATION/trainingPipelines/TRAININGPIPELINE_ID",
      "displayName": "TRAININGPIPELINE_DISPLAYNAME",
      "inputDataConfig": {
        "datasetId": "DATASET_ID",
        "fractionSplit": {
          "trainingFraction": 0.7,
          "validationFraction": 0.15,
          "testFraction": 0.15
        }
      },
      "trainingTaskDefinition": "gs://google-cloud-aiplatform/schema/trainingjob/definition/automl_image_object_detection_1.0.0.yaml",
      "trainingTaskInputs": {
        "modelType": "MODELTYPE",
        "budgetMilliNodeHours": "NODE_HOUR_BUDGET"
      },
      "modelToUpload": {
        "displayName": "MODEL_DISPLAYNAME",
        "labels": {
          "KEY1": "VALUE1",
          "KEY2": "VALUE2"
        }
      },
      "state": "PIPELINE_STATE_PENDING",
      "createTime": "2020-07-14T17:16:55.098953Z",
      "updateTime": "2020-07-14T17:16:55.098953Z"
    }

### Java

Before trying this sample, follow the Java setup instructions in the [Agent Platform quickstart using client libraries](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/start/client-libraries) .

To authenticate to Agent Platform, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

    import com.google.cloud.aiplatform.util.ValueConverter;
    import com.google.cloud.aiplatform.v1.DeployedModelRef;
    import com.google.cloud.aiplatform.v1.EnvVar;
    import com.google.cloud.aiplatform.v1.FilterSplit;
    import com.google.cloud.aiplatform.v1.FractionSplit;
    import com.google.cloud.aiplatform.v1.InputDataConfig;
    import com.google.cloud.aiplatform.v1.LocationName;
    import com.google.cloud.aiplatform.v1.Model;
    import com.google.cloud.aiplatform.v1.Model.ExportFormat;
    import com.google.cloud.aiplatform.v1.ModelContainerSpec;
    import com.google.cloud.aiplatform.v1.PipelineServiceClient;
    import com.google.cloud.aiplatform.v1.PipelineServiceSettings;
    import com.google.cloud.aiplatform.v1.Port;
    import com.google.cloud.aiplatform.v1.PredefinedSplit;
    import com.google.cloud.aiplatform.v1.PredictSchemata;
    import com.google.cloud.aiplatform.v1.TimestampSplit;
    import com.google.cloud.aiplatform.v1.TrainingPipeline;
    import com.google.cloud.aiplatform.v1.schema.trainingjob.definition.AutoMlImageObjectDetectionInputs;
    import com.google.cloud.aiplatform.v1.schema.trainingjob.definition.AutoMlImageObjectDetectionInputs.ModelType;
    import com.google.rpc.Status;
    import java.io.IOException;
    
    public class CreateTrainingPipelineImageObjectDetectionSample {
    
      public static void main(String[] args) throws IOException {
        // TODO(developer): Replace these variables before running the sample.
        String trainingPipelineDisplayName = "YOUR_TRAINING_PIPELINE_DISPLAY_NAME";
        String project = "YOUR_PROJECT_ID";
        String datasetId = "YOUR_DATASET_ID";
        String modelDisplayName = "YOUR_MODEL_DISPLAY_NAME";
        createTrainingPipelineImageObjectDetectionSample(
            project, trainingPipelineDisplayName, datasetId, modelDisplayName);
      }
    
      static void createTrainingPipelineImageObjectDetectionSample(
          String project, String trainingPipelineDisplayName, String datasetId, String modelDisplayName)
          throws IOException {
        PipelineServiceSettings pipelineServiceSettings =
            PipelineServiceSettings.newBuilder()
                .setEndpoint("us-central1-aiplatform.googleapis.com:443")
                .build();
    
        // Initialize client that will be used to send requests. This client only needs to be created
        // once, and can be reused for multiple requests. After completing all of your requests, call
        // the "close" method on the client to safely clean up any remaining background resources.
        try (PipelineServiceClient pipelineServiceClient =
            PipelineServiceClient.create(pipelineServiceSettings)) {
          String location = "us-central1";
          String trainingTaskDefinition =
              "gs://google-cloud-aiplatform/schema/trainingjob/definition/"
                  + "automl_image_object_detection_1.0.0.yaml";
          LocationName locationName = LocationName.of(project, location);
    
          AutoMlImageObjectDetectionInputs autoMlImageObjectDetectionInputs =
              AutoMlImageObjectDetectionInputs.newBuilder()
                  .setModelType(ModelType.CLOUD_HIGH_ACCURACY_1)
                  .setBudgetMilliNodeHours(20000)
                  .setDisableEarlyStopping(false)
                  .build();
    
          InputDataConfig trainingInputDataConfig =
              InputDataConfig.newBuilder().setDatasetId(datasetId).build();
          Model model = Model.newBuilder().setDisplayName(modelDisplayName).build();
          TrainingPipeline trainingPipeline =
              TrainingPipeline.newBuilder()
                  .setDisplayName(trainingPipelineDisplayName)
                  .setTrainingTaskDefinition(trainingTaskDefinition)
                  .setTrainingTaskInputs(ValueConverter.toValue(autoMlImageObjectDetectionInputs))
                  .setInputDataConfig(trainingInputDataConfig)
                  .setModelToUpload(model)
                  .build();
    
          TrainingPipeline trainingPipelineResponse =
              pipelineServiceClient.createTrainingPipeline(locationName, trainingPipeline);
    
          System.out.println("Create Training Pipeline Image Object Detection Response");
          System.out.format("Name: %s\n", trainingPipelineResponse.getName());
          System.out.format("Display Name: %s\n", trainingPipelineResponse.getDisplayName());
    
          System.out.format(
              "Training Task Definition %s\n", trainingPipelineResponse.getTrainingTaskDefinition());
          System.out.format(
              "Training Task Inputs: %s\n", trainingPipelineResponse.getTrainingTaskInputs());
          System.out.format(
              "Training Task Metadata: %s\n", trainingPipelineResponse.getTrainingTaskMetadata());
          System.out.format("State: %s\n", trainingPipelineResponse.getState());
    
          System.out.format("Create Time: %s\n", trainingPipelineResponse.getCreateTime());
          System.out.format("StartTime %s\n", trainingPipelineResponse.getStartTime());
          System.out.format("End Time: %s\n", trainingPipelineResponse.getEndTime());
          System.out.format("Update Time: %s\n", trainingPipelineResponse.getUpdateTime());
          System.out.format("Labels: %s\n", trainingPipelineResponse.getLabelsMap());
    
          InputDataConfig inputDataConfig = trainingPipelineResponse.getInputDataConfig();
          System.out.println("Input Data Config");
          System.out.format("Dataset Id: %s", inputDataConfig.getDatasetId());
          System.out.format("Annotations Filter: %s\n", inputDataConfig.getAnnotationsFilter());
    
          FractionSplit fractionSplit = inputDataConfig.getFractionSplit();
          System.out.println("Fraction Split");
          System.out.format("Training Fraction: %s\n", fractionSplit.getTrainingFraction());
          System.out.format("Validation Fraction: %s\n", fractionSplit.getValidationFraction());
          System.out.format("Test Fraction: %s\n", fractionSplit.getTestFraction());
    
          FilterSplit filterSplit = inputDataConfig.getFilterSplit();
          System.out.println("Filter Split");
          System.out.format("Training Filter: %s\n", filterSplit.getTrainingFilter());
          System.out.format("Validation Filter: %s\n", filterSplit.getValidationFilter());
          System.out.format("Test Filter: %s\n", filterSplit.getTestFilter());
    
          PredefinedSplit predefinedSplit = inputDataConfig.getPredefinedSplit();
          System.out.println("Predefined Split");
          System.out.format("Key: %s\n", predefinedSplit.getKey());
    
          TimestampSplit timestampSplit = inputDataConfig.getTimestampSplit();
          System.out.println("Timestamp Split");
          System.out.format("Training Fraction: %s\n", timestampSplit.getTrainingFraction());
          System.out.format("Validation Fraction: %s\n", timestampSplit.getValidationFraction());
          System.out.format("Test Fraction: %s\n", timestampSplit.getTestFraction());
          System.out.format("Key: %s\n", timestampSplit.getKey());
    
          Model modelResponse = trainingPipelineResponse.getModelToUpload();
          System.out.println("Model To Upload");
          System.out.format("Name: %s\n", modelResponse.getName());
          System.out.format("Display Name: %s\n", modelResponse.getDisplayName());
          System.out.format("Description: %s\n", modelResponse.getDescription());
    
          System.out.format("Metadata Schema Uri: %s\n", modelResponse.getMetadataSchemaUri());
          System.out.format("Metadata: %s\n", modelResponse.getMetadata());
          System.out.format("Training Pipeline: %s\n", modelResponse.getTrainingPipeline());
          System.out.format("Artifact Uri: %s\n", modelResponse.getArtifactUri());
    
          System.out.format(
              "Supported Deployment Resources Types: %s\n",
              modelResponse.getSupportedDeploymentResourcesTypesList());
          System.out.format(
              "Supported Input Storage Formats: %s\n",
              modelResponse.getSupportedInputStorageFormatsList());
          System.out.format(
              "Supported Output Storage Formats: %s\n",
              modelResponse.getSupportedOutputStorageFormatsList());
    
          System.out.format("Create Time: %s\n", modelResponse.getCreateTime());
          System.out.format("Update Time: %s\n", modelResponse.getUpdateTime());
          System.out.format("Labels: %sn\n", modelResponse.getLabelsMap());
    
          PredictSchemata predictSchemata = modelResponse.getPredictSchemata();
          System.out.println("Predict Schemata");
          System.out.format("Instance Schema Uri: %s\n", predictSchemata.getInstanceSchemaUri());
          System.out.format("Parameters Schema Uri: %s\n", predictSchemata.getParametersSchemaUri());
          System.out.format("Prediction Schema Uri: %s\n", predictSchemata.getPredictionSchemaUri());
    
          for (ExportFormat exportFormat : modelResponse.getSupportedExportFormatsList()) {
            System.out.println("Supported Export Format");
            System.out.format("Id: %s\n", exportFormat.getId());
          }
    
          ModelContainerSpec modelContainerSpec = modelResponse.getContainerSpec();
          System.out.println("Container Spec");
          System.out.format("Image Uri: %s\n", modelContainerSpec.getImageUri());
          System.out.format("Command: %s\n", modelContainerSpec.getCommandList());
          System.out.format("Args: %s\n", modelContainerSpec.getArgsList());
          System.out.format("Predict Route: %s\n", modelContainerSpec.getPredictRoute());
          System.out.format("Health Route: %s\n", modelContainerSpec.getHealthRoute());
    
          for (EnvVar envVar : modelContainerSpec.getEnvList()) {
            System.out.println("Env");
            System.out.format("Name: %s\n", envVar.getName());
            System.out.format("Value: %s\n", envVar.getValue());
          }
    
          for (Port port : modelContainerSpec.getPortsList()) {
            System.out.println("Port");
            System.out.format("Container Port: %s\n", port.getContainerPort());
          }
    
          for (DeployedModelRef deployedModelRef : modelResponse.getDeployedModelsList()) {
            System.out.println("Deployed Model");
            System.out.format("Endpoint: %s\n", deployedModelRef.getEndpoint());
            System.out.format("Deployed Model Id: %s\n", deployedModelRef.getDeployedModelId());
          }
    
          Status status = trainingPipelineResponse.getError();
          System.out.println("Error");
          System.out.format("Code: %s\n", status.getCode());
          System.out.format("Message: %s\n", status.getMessage());
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
    
    // const datasetId = 'YOUR_DATASET_ID';
    // const modelDisplayName = 'YOUR_MODEL_DISPLAY_NAME';
    // const trainingPipelineDisplayName = 'YOUR_TRAINING_PIPELINE_DISPLAY_NAME';
    // const project = 'YOUR_PROJECT_ID';
    // const location = 'YOUR_PROJECT_LOCATION';
    
    const aiplatform = require('@google-cloud/aiplatform');
    const {definition} =
      aiplatform.protos.google.cloud.aiplatform.v1.schema.trainingjob;
    const ModelType = definition.AutoMlImageObjectDetectionInputs.ModelType;
    
    // Imports the Google Cloud Pipeline Service Client library
    const {PipelineServiceClient} = aiplatform.v1;
    
    // Specifies the location of the api endpoint
    const clientOptions = {
      apiEndpoint: 'us-central1-aiplatform.googleapis.com',
    };
    
    // Instantiates a client
    const pipelineServiceClient = new PipelineServiceClient(clientOptions);
    
    async function createTrainingPipelineImageObjectDetection() {
      // Configure the parent resource
      const parent = `projects/${project}/locations/${location}`;
    
      const trainingTaskInputsObj =
        new definition.AutoMlImageObjectDetectionInputs({
          disableEarlyStopping: false,
          modelType: ModelType.CLOUD_1,
          budgetMilliNodeHours: 20000,
        });
    
      const trainingTaskInputs = trainingTaskInputsObj.toValue();
      const modelToUpload = {displayName: modelDisplayName};
      const inputDataConfig = {datasetId: datasetId};
      const trainingPipeline = {
        displayName: trainingPipelineDisplayName,
        trainingTaskDefinition:
          'gs://google-cloud-aiplatform/schema/trainingjob/definition/automl_image_object_detection_1.0.0.yaml',
        trainingTaskInputs,
        inputDataConfig,
        modelToUpload,
      };
      const request = {
        parent,
        trainingPipeline,
      };
    
      // Create training pipeline request
      const [response] =
        await pipelineServiceClient.createTrainingPipeline(request);
    
      console.log('Create training pipeline image object detection response');
      console.log(`Name : ${response.name}`);
      console.log('Raw response:');
      console.log(JSON.stringify(response, null, 2));
    }
    createTrainingPipelineImageObjectDetection();

### Python

To learn how to install or update the Vertex AI SDK for Python, see [Install the Vertex AI SDK for Python](https://docs.cloud.google.com/vertex-ai/docs/start/use-vertex-ai-python-sdk) . For more information, see the [Python API reference documentation](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest) .

    from google.cloud import aiplatform
    from google.cloud.aiplatform.gapic.schema import trainingjob
    
    
    def create_training_pipeline_image_object_detection_sample(
        project: str,
        display_name: str,
        dataset_id: str,
        model_display_name: str,
        location: str = "us-central1",
        api_endpoint: str = "us-central1-aiplatform.googleapis.com",
    ):
        # The AI Platform services require regional API endpoints.
        client_options = {"api_endpoint": api_endpoint}
        # Initialize client that will be used to create and send requests.
        # This client only needs to be created once, and can be reused for multiple requests.
        client = aiplatform.gapic.PipelineServiceClient(client_options=client_options)
        training_task_inputs = trainingjob.definition.AutoMlImageObjectDetectionInputs(
            model_type="CLOUD_HIGH_ACCURACY_1",
            budget_milli_node_hours=20000,
            disable_early_stopping=False,
        ).to_value()
    
        training_pipeline = {
            "display_name": display_name,
            "training_task_definition": "gs://google-cloud-aiplatform/schema/trainingjob/definition/automl_image_object_detection_1.0.0.yaml",
            "training_task_inputs": training_task_inputs,
            "input_data_config": {"dataset_id": dataset_id},
            "model_to_upload": {"display_name": model_display_name},
        }
        parent = f"projects/{project}/locations/{location}"
        response = client.create_training_pipeline(
            parent=parent, training_pipeline=training_pipeline
        )
        print("response:", response)

## Control the data split using REST

You can control how your training data is split between the training, validation, and test sets. When using the Agent Platform API, use the [`Split` object](https://docs.cloud.google.com/vertex-ai/docs/reference/rest/v1/projects.locations.trainingPipelines#InputDataConfig) to determine your data split. The `Split` object can be included in the `InputConfig` object as one of several object types, each of which provides a different way to split the training data. You can select one method only.

`FractionSplit` :

  - TRAINING\_FRACTION : The fraction of the training data to be used for the training set.
  - VALIDATION\_FRACTION : The fraction of the training data to be used for the validation set. Not used for video data.
  - TEST\_FRACTION : The fraction of the training data to be used for the test set.

If any of the fractions are specified, all must be specified. The fractions must add up to 1.0. The [default values for the fractions](https://docs.cloud.google.com/vertex-ai/docs/general/ml-use#default) differ depending on your data type. [Learn more](https://docs.cloud.google.com/vertex-ai/docs/general/ml-use#percentages) .

    "fractionSplit": {
      "trainingFraction": TRAINING_FRACTION,
      "validationFraction": VALIDATION_FRACTION,
      "testFraction": TEST_FRACTION
    },

`FilterSplit` :

  - TRAINING\_FILTER : Data items that match this filter are used for the training set.
  - VALIDATION\_FILTER : Data items that match this filter are used for the validation set. Must be "-" for video data.
  - TEST\_FILTER : Data items that match this filter are used for the test set.

These filters can be used with the `ml_use` label, or with any labels you apply to your data. Learn more about using [the ml-use label](https://docs.cloud.google.com/vertex-ai/machine-learning/general/ml-use#ml-use) and [other labels](https://docs.cloud.google.com/vertex-ai/machine-learning/general/ml-use#filter) to filter your data.

The following example shows how to use the `filterSplit` object with the `ml_use` label, with the validation set included:

    "filterSplit": {
    "trainingFilter": "labels.aiplatform.googleapis.com/ml_use=training",
    "validationFilter": "labels.aiplatform.googleapis.com/ml_use=validation",
    "testFilter": "labels.aiplatform.googleapis.com/ml_use=test"
    }
