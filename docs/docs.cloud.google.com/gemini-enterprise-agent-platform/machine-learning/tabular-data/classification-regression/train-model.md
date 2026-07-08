---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tabular-data/classification-regression/train-model
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tabular-data/classification-regression/train-model
title: Train a classification or regression model
description: Train a classification or regression model from a tabular dataset in Gemini Enterprise Agent Platform.
data_source: docs.cloud.google.com
---

This page shows you how to train a classification or regression model from a tabular dataset using either the Google Cloud console or the Agent Platform API.

## Before you begin

Before you train a model, you must complete the following:

  - [Prepare your training data](https://docs.cloud.google.com/gemini-enterprise-agent-platform/tabular-data/classification-regression/prepare-data)
  - [Create an Agent Platform dataset](https://docs.cloud.google.com/gemini-enterprise-agent-platform/tabular-data/classification-regression/create-dataset) .

## Train a model

### Google Cloud console

1.  In the Google Cloud console, in the Agent Platform section, go to the **Datasets** page.

2.  Click the name of the dataset you want to use to train your model to open its details page.

3.  If your data type uses annotation sets, select the annotation set you want to use for this model.

4.  Click **Train new model** .

5.  Select **Other** .

6.  In the **Train new model** page, complete the following steps:
    
    1.  Select the model training method.
        
          - `AutoML` is a good choice for a wide range of use cases.
        
        Click **Continue** .
    
    2.  Enter the display name for your new model.
    
    3.  Select your target column.
        
        The target column is the value that the model will predict.
        
        Learn more about [target column requirements](https://docs.cloud.google.com/gemini-enterprise-agent-platform/tabular-data/classification-regression/prepare-data#data-structure) .
    
    4.  **Optional** : To export your test dataset to BigQuery, check **Export test dataset to BigQuery** and provide the name of the table.
    
    5.  **Optional** : To choose how to split the data between training, test, and validation sets, open the **Advanced options** . You can choose between the following data split options:
        
          - **Random** (Default): Agent Platform randomly selects the rows associated with each of the data sets. By default, Agent Platform selects 80% of your data rows for the training set, 10% for the validation set, and 10% for the test set.
          - **Manual** : Agent Platform selects data rows for each of the data sets based on the values in a data split column. Provide the name of the data split column.
          - **Chronological** : Agent Platform splits data based on the timestamp in a time column. Provide the name of the time column.
        
        Learn more about [data splits](https://docs.cloud.google.com/gemini-enterprise-agent-platform/tabular-data/data-splits) .
    
    6.  Click **Continue** .
    
    7.  **Optional:** Click **Generate statistics** . Generating statistics populates the **Transformation** dropdown menus.
    
    8.  On the Training options page, review your column list and exclude any columns from training that should not be used to train the model.
    
    9.  Review the transformations selected for your included features, along with whether invalid data is allowed, and make any required updates.
        
        Learn more about [transformations](https://docs.cloud.google.com/gemini-enterprise-agent-platform/datasets/data-types-tabular#transformations) and [invalid data](https://docs.cloud.google.com/gemini-enterprise-agent-platform/datasets/data-types-tabular#null-values) .
    
    10. If you want to specify a weight column, or change your optimization objective from the default, open the **Advanced options** and make your selections.
        
        Learn more about [weight columns](https://docs.cloud.google.com/gemini-enterprise-agent-platform/tabular-data/classification-regression/prepare-data#weight) and [optimization objectives](https://docs.cloud.google.com/gemini-enterprise-agent-platform/tabular-data/classification-regression/train-model#optimization-objectives) .
    
    11. Click **Continue** .
    
    12. In the **Compute and pricing** window, configure as follows:
        
        Enter the maximum number of hours you want your model to train for.
        
        This setting helps you put a cap on the training costs. The actual time elapsed can be longer than this value, because there are other operations involved in creating a new model.
        
        Suggested training time is related to the size of your training data. The table below shows suggested training time ranges by row count; a large number of columns will also increase the required training time.
        
        | Rows                   | Suggested training time |
        | ---------------------- | ----------------------- |
        | Less than 100,000      | 1-3 hours               |
        | 100,000 - 1,000,000    | 1-6 hours               |
        | 1,000,000 - 10,000,000 | 1-12 hours              |
        | More than 10,000,000   | 3 - 24 hours            |
        

        For information about training pricing, see the [pricing page](https://cloud.google.com/products/gemini-enterprise-agent-platform/pricing#tabular-data) .
    
    13. Click **Start Training** .
        
        Model training can take many hours, depending on the size and complexity of your data and your training budget, if you specified one. You can close this tab and return to it later. You will receive an email when your model has completed training.
        
        > Tabular training data in Cloud Storage or BigQuery is not imported into Agent Platform. (When you import from local files, they are imported into Cloud Storage.) When you create a dataset with tabular data, the data is associated with the dataset. Changes you make to your data source in Cloud Storage or BigQuery after dataset creation are incorporated into models subsequently trained with that dataset. A snapshot of the dataset is taken when model training begins.

### API

> Tabular training data in Cloud Storage or BigQuery is not imported into Agent Platform. (When you import from local files, they are imported into Cloud Storage.) When you create a dataset with tabular data, the data is associated with the dataset. Changes you make to your data source in Cloud Storage or BigQuery after dataset creation are incorporated into models subsequently trained with that dataset. A snapshot of the dataset is taken when model training begins.

Select a tabular data type objective.

### Classification

Select a tab for your language or environment:

### REST

You use the [trainingPipelines.create](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.trainingPipelines/create) command to train a model.

Train the model.

Before using any of the request data, make the following replacements:

  - LOCATION : Your region.
  - PROJECT : Your [project ID](https://docs.cloud.google.com/resource-manager/docs/creating-managing-projects#identifiers) .
  - TRAININGPIPELINE\_DISPLAY\_NAME : Display name for the training pipeline created for this operation.
  - TARGET\_COLUMN : The column (value) you want this model to predict.
  - WEIGHT\_COLUMN : (Optional) The weight column. [Learn more](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tabular-data/classification-regression/prepare-data#weight) .
  - TRAINING\_BUDGET : The maximum amount of time you want the model to train, in milli node hours (1,000 milli node hours equals one node hour).
  - OPTIMIZATION\_OBJECTIVE : Required only if you do not want the default optimization objective for your prediction type. [Learn more](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tabular-data/classification-regression/train-model#optimization-objectives) .
  - TRANSFORMATION\_TYPE : The transformation type is provided for each column used to train the model. [Learn more](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/datasets/data-types-tabular#transformations) .
  - COLUMN\_NAME : The name of the column with the specified transformation type. Every column used to train the model must be specified.
  - MODEL\_DISPLAY\_NAME : Display name for the newly trained model.
  - DATASET\_ID : ID for the training Dataset.
  - You can provide a `Split` object to control your data split. For information about controlling data split, see [Controlling the data split using REST](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tabular-data/classification-regression/train-model#data-split) .
  - PROJECT\_NUMBER : Your project's automatically generated [project number](https://docs.cloud.google.com/resource-manager/docs/creating-managing-projects#identifiers)

HTTP method and URL:

    POST https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT/locations/LOCATION/trainingPipelines

Request JSON body:

    {
        "displayName": "TRAININGPIPELINE_DISPLAY_NAME",
        "trainingTaskDefinition": "gs://google-cloud-aiplatform/schema/trainingjob/definition/automl_tabular_1.0.0.yaml",
        "trainingTaskInputs": {
            "targetColumn": "TARGET_COLUMN",
            "weightColumn": "WEIGHT_COLUMN",
            "predictionType": "classification",
            "trainBudgetMilliNodeHours": TRAINING_BUDGET,
            "optimizationObjective": "OPTIMIZATION_OBJECTIVE",
            "transformations": [
                {"TRANSFORMATION_TYPE_1":  {"column_name" : "COLUMN_NAME_1"} },
                {"TRANSFORMATION_TYPE_2":  {"column_name" : "COLUMN_NAME_2"} },
                ...
        },
        "modelToUpload": {"displayName": "MODEL_DISPLAY_NAME"},
        "inputDataConfig": {
          "datasetId": "DATASET_ID",
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
         "https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT/locations/LOCATION/trainingPipelines"

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
        -Uri "https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT/locations/LOCATION/trainingPipelines" | Select-Object -Expand Content

You should receive a JSON response similar to the following:

    {
      "name": "projects/PROJECT_NUMBER/locations/us-central1/trainingPipelines/4567",
      "displayName": "myModelName",
      "trainingTaskDefinition": "gs://google-cloud-aiplatform/schema/trainingjob/definition/automl_tabular_1.0.0.yaml",
      "modelToUpload": {
        "displayName": "myModelName"
      },
      "state": "PIPELINE_STATE_PENDING",
      "createTime": "2020-08-18T01:22:57.479336Z",
      "updateTime": "2020-08-18T01:22:57.479336Z"
    }

### Java

Before trying this sample, follow the Java setup instructions in the [Agent Platform quickstart using client libraries](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/start/client-libraries) . For more information, see the [Agent Platform Java API reference documentation](https://docs.cloud.google.com/java/docs/reference/google-cloud-aiplatform/latest/com.google.cloud.aiplatform.v1) .

To authenticate to Agent Platform, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

    import com.google.cloud.aiplatform.util.ValueConverter;
    import com.google.cloud.aiplatform.v1.DeployedModelRef;
    import com.google.cloud.aiplatform.v1.EnvVar;
    import com.google.cloud.aiplatform.v1.FilterSplit;
    import com.google.cloud.aiplatform.v1.FractionSplit;
    import com.google.cloud.aiplatform.v1.InputDataConfig;
    import com.google.cloud.aiplatform.v1.LocationName;
    import com.google.cloud.aiplatform.v1.Model;
    import com.google.cloud.aiplatform.v1.ModelContainerSpec;
    import com.google.cloud.aiplatform.v1.PipelineServiceClient;
    import com.google.cloud.aiplatform.v1.PipelineServiceSettings;
    import com.google.cloud.aiplatform.v1.Port;
    import com.google.cloud.aiplatform.v1.PredefinedSplit;
    import com.google.cloud.aiplatform.v1.PredictSchemata;
    import com.google.cloud.aiplatform.v1.TimestampSplit;
    import com.google.cloud.aiplatform.v1.TrainingPipeline;
    import com.google.cloud.aiplatform.v1.schema.trainingjob.definition.AutoMlTablesInputs;
    import com.google.cloud.aiplatform.v1.schema.trainingjob.definition.AutoMlTablesInputs.Transformation;
    import com.google.cloud.aiplatform.v1.schema.trainingjob.definition.AutoMlTablesInputs.Transformation.AutoTransformation;
    import com.google.rpc.Status;
    import java.io.IOException;
    import java.util.ArrayList;
    
    public class CreateTrainingPipelineTabularClassificationSample {
    
      public static void main(String[] args) throws IOException {
        // TODO(developer): Replace these variables before running the sample.
        String project = "YOUR_PROJECT_ID";
        String modelDisplayName = "YOUR_DATASET_DISPLAY_NAME";
        String datasetId = "YOUR_DATASET_ID";
        String targetColumn = "TARGET_COLUMN";
        createTrainingPipelineTableClassification(project, modelDisplayName, datasetId, targetColumn);
      }
    
      static void createTrainingPipelineTableClassification(
          String project, String modelDisplayName, String datasetId, String targetColumn)
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
          LocationName locationName = LocationName.of(project, location);
          String trainingTaskDefinition =
              "gs://google-cloud-aiplatform/schema/trainingjob/definition/automl_tables_1.0.0.yaml";
    
          // Set the columns used for training and their data types
          Transformation transformation1 =
              Transformation.newBuilder()
                  .setAuto(AutoTransformation.newBuilder().setColumnName("sepal_width").build())
                  .build();
          Transformation transformation2 =
              Transformation.newBuilder()
                  .setAuto(AutoTransformation.newBuilder().setColumnName("sepal_length").build())
                  .build();
          Transformation transformation3 =
              Transformation.newBuilder()
                  .setAuto(AutoTransformation.newBuilder().setColumnName("petal_length").build())
                  .build();
          Transformation transformation4 =
              Transformation.newBuilder()
                  .setAuto(AutoTransformation.newBuilder().setColumnName("petal_width").build())
                  .build();
    
          ArrayList<Transformation> transformationArrayList = new ArrayList<>();
          transformationArrayList.add(transformation1);
          transformationArrayList.add(transformation2);
          transformationArrayList.add(transformation3);
          transformationArrayList.add(transformation4);
    
          AutoMlTablesInputs autoMlTablesInputs =
              AutoMlTablesInputs.newBuilder()
                  .setTargetColumn(targetColumn)
                  .setPredictionType("classification")
                  .addAllTransformations(transformationArrayList)
                  .setTrainBudgetMilliNodeHours(8000)
                  .build();
    
          FractionSplit fractionSplit =
              FractionSplit.newBuilder()
                  .setTrainingFraction(0.8)
                  .setValidationFraction(0.1)
                  .setTestFraction(0.1)
                  .build();
    
          InputDataConfig inputDataConfig =
              InputDataConfig.newBuilder()
                  .setDatasetId(datasetId)
                  .setFractionSplit(fractionSplit)
                  .build();
          Model modelToUpload = Model.newBuilder().setDisplayName(modelDisplayName).build();
    
          TrainingPipeline trainingPipeline =
              TrainingPipeline.newBuilder()
                  .setDisplayName(modelDisplayName)
                  .setTrainingTaskDefinition(trainingTaskDefinition)
                  .setTrainingTaskInputs(ValueConverter.toValue(autoMlTablesInputs))
                  .setInputDataConfig(inputDataConfig)
                  .setModelToUpload(modelToUpload)
                  .build();
    
          TrainingPipeline trainingPipelineResponse =
              pipelineServiceClient.createTrainingPipeline(locationName, trainingPipeline);
    
          System.out.println("Create Training Pipeline Tabular Classification Response");
          System.out.format("\tName: %s\n", trainingPipelineResponse.getName());
          System.out.format("\tDisplay Name: %s\n", trainingPipelineResponse.getDisplayName());
          System.out.format(
              "\tTraining Task Definition: %s\n", trainingPipelineResponse.getTrainingTaskDefinition());
          System.out.format(
              "\tTraining Task Inputs: %s\n", trainingPipelineResponse.getTrainingTaskInputs());
          System.out.format(
              "\tTraining Task Metadata: %s\n", trainingPipelineResponse.getTrainingTaskMetadata());
    
          System.out.format("\tState: %s\n", trainingPipelineResponse.getState());
          System.out.format("\tCreate Time: %s\n", trainingPipelineResponse.getCreateTime());
          System.out.format("\tStart Time: %s\n", trainingPipelineResponse.getStartTime());
          System.out.format("\tEnd Time: %s\n", trainingPipelineResponse.getEndTime());
          System.out.format("\tUpdate Time: %s\n", trainingPipelineResponse.getUpdateTime());
          System.out.format("\tLabels: %s\n", trainingPipelineResponse.getLabelsMap());
    
          InputDataConfig inputDataConfigResponse = trainingPipelineResponse.getInputDataConfig();
          System.out.println("\tInput Data Config");
          System.out.format("\t\tDataset Id: %s\n", inputDataConfigResponse.getDatasetId());
          System.out.format(
              "\t\tAnnotations Filter: %s\n", inputDataConfigResponse.getAnnotationsFilter());
    
          FractionSplit fractionSplitResponse = inputDataConfigResponse.getFractionSplit();
          System.out.println("\t\tFraction Split");
          System.out.format(
              "\t\t\tTraining Fraction: %s\n", fractionSplitResponse.getTrainingFraction());
          System.out.format(
              "\t\t\tValidation Fraction: %s\n", fractionSplitResponse.getValidationFraction());
          System.out.format("\t\t\tTest Fraction: %s\n", fractionSplitResponse.getTestFraction());
    
          FilterSplit filterSplit = inputDataConfigResponse.getFilterSplit();
          System.out.println("\t\tFilter Split");
          System.out.format("\t\t\tTraining Fraction: %s\n", filterSplit.getTrainingFilter());
          System.out.format("\t\t\tValidation Fraction: %s\n", filterSplit.getValidationFilter());
          System.out.format("\t\t\tTest Fraction: %s\n", filterSplit.getTestFilter());
    
          PredefinedSplit predefinedSplit = inputDataConfigResponse.getPredefinedSplit();
          System.out.println("\t\tPredefined Split");
          System.out.format("\t\t\tKey: %s\n", predefinedSplit.getKey());
    
          TimestampSplit timestampSplit = inputDataConfigResponse.getTimestampSplit();
          System.out.println("\t\tTimestamp Split");
          System.out.format("\t\t\tTraining Fraction: %s\n", timestampSplit.getTrainingFraction());
          System.out.format("\t\t\tValidation Fraction: %s\n", timestampSplit.getValidationFraction());
          System.out.format("\t\t\tTest Fraction: %s\n", timestampSplit.getTestFraction());
          System.out.format("\t\t\tKey: %s\n", timestampSplit.getKey());
    
          Model modelResponse = trainingPipelineResponse.getModelToUpload();
          System.out.println("\tModel To Upload");
          System.out.format("\t\tName: %s\n", modelResponse.getName());
          System.out.format("\t\tDisplay Name: %s\n", modelResponse.getDisplayName());
          System.out.format("\t\tDescription: %s\n", modelResponse.getDescription());
          System.out.format("\t\tMetadata Schema Uri: %s\n", modelResponse.getMetadataSchemaUri());
          System.out.format("\t\tMeta Data: %s\n", modelResponse.getMetadata());
          System.out.format("\t\tTraining Pipeline: %s\n", modelResponse.getTrainingPipeline());
          System.out.format("\t\tArtifact Uri: %s\n", modelResponse.getArtifactUri());
    
          System.out.format(
              "\t\tSupported Deployment Resources Types: %s\n",
              modelResponse.getSupportedDeploymentResourcesTypesList().toString());
          System.out.format(
              "\t\tSupported Input Storage Formats: %s\n",
              modelResponse.getSupportedInputStorageFormatsList().toString());
          System.out.format(
              "\t\tSupported Output Storage Formats: %s\n",
              modelResponse.getSupportedOutputStorageFormatsList().toString());
    
          System.out.format("\t\tCreate Time: %s\n", modelResponse.getCreateTime());
          System.out.format("\t\tUpdate Time: %s\n", modelResponse.getUpdateTime());
          System.out.format("\t\tLables: %s\n", modelResponse.getLabelsMap());
          PredictSchemata predictSchemata = modelResponse.getPredictSchemata();
    
          System.out.println("\tPredict Schemata");
          System.out.format("\t\tInstance Schema Uri: %s\n", predictSchemata.getInstanceSchemaUri());
          System.out.format(
              "\t\tParameters Schema Uri: %s\n", predictSchemata.getParametersSchemaUri());
          System.out.format(
              "\t\tPrediction Schema Uri: %s\n", predictSchemata.getPredictionSchemaUri());
    
          for (Model.ExportFormat supportedExportFormat :
              modelResponse.getSupportedExportFormatsList()) {
            System.out.println("\tSupported Export Format");
            System.out.format("\t\tId: %s\n", supportedExportFormat.getId());
          }
          ModelContainerSpec containerSpec = modelResponse.getContainerSpec();
    
          System.out.println("\tContainer Spec");
          System.out.format("\t\tImage Uri: %s\n", containerSpec.getImageUri());
          System.out.format("\t\tCommand: %s\n", containerSpec.getCommandList());
          System.out.format("\t\tArgs: %s\n", containerSpec.getArgsList());
          System.out.format("\t\tPredict Route: %s\n", containerSpec.getPredictRoute());
          System.out.format("\t\tHealth Route: %s\n", containerSpec.getHealthRoute());
    
          for (EnvVar envVar : containerSpec.getEnvList()) {
            System.out.println("\t\tEnv");
            System.out.format("\t\t\tName: %s\n", envVar.getName());
            System.out.format("\t\t\tValue: %s\n", envVar.getValue());
          }
    
          for (Port port : containerSpec.getPortsList()) {
            System.out.println("\t\tPort");
            System.out.format("\t\t\tContainer Port: %s\n", port.getContainerPort());
          }
    
          for (DeployedModelRef deployedModelRef : modelResponse.getDeployedModelsList()) {
            System.out.println("\tDeployed Model");
            System.out.format("\t\tEndpoint: %s\n", deployedModelRef.getEndpoint());
            System.out.format("\t\tDeployed Model Id: %s\n", deployedModelRef.getDeployedModelId());
          }
    
          Status status = trainingPipelineResponse.getError();
          System.out.println("\tError");
          System.out.format("\t\tCode: %s\n", status.getCode());
          System.out.format("\t\tMessage: %s\n", status.getMessage());
        }
      }
    }

### Node.js

Before trying this sample, follow the Node.js setup instructions in the [Agent Platform quickstart using client libraries](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/start/client-libraries) . For more information, see the [Agent Platform Node.js API reference documentation](https://docs.cloud.google.com/nodejs/docs/reference/aiplatform/latest) .

To authenticate to Agent Platform, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

    /**
     * TODO(developer): Uncomment these variables before running the sample.\
     * (Not necessary if passing values as arguments)
     */
    
    // const datasetId = 'YOUR_DATASET_ID';
    // const modelDisplayName = 'YOUR_MODEL_DISPLAY_NAME';
    // const trainingPipelineDisplayName = 'YOUR_TRAINING_PIPELINE_DISPLAY_NAME';
    // const targetColumn = 'YOUR_TARGET_COLUMN';
    // const project = 'YOUR_PROJECT_ID';
    // const location = 'YOUR_PROJECT_LOCATION';
    const aiplatform = require('@google-cloud/aiplatform');
    const {definition} =
      aiplatform.protos.google.cloud.aiplatform.v1.schema.trainingjob;
    
    // Imports the Google Cloud Pipeline Service Client library
    const {PipelineServiceClient} = aiplatform.v1;
    // Specifies the location of the api endpoint
    const clientOptions = {
      apiEndpoint: 'us-central1-aiplatform.googleapis.com',
    };
    
    // Instantiates a client
    const pipelineServiceClient = new PipelineServiceClient(clientOptions);
    
    async function createTrainingPipelineTablesClassification() {
      // Configure the parent resource
      const parent = `projects/${project}/locations/${location}`;
    
      const transformations = [
        {auto: {column_name: 'sepal_width'}},
        {auto: {column_name: 'sepal_length'}},
        {auto: {column_name: 'petal_length'}},
        {auto: {column_name: 'petal_width'}},
      ];
      const trainingTaskInputsObj = new definition.AutoMlTablesInputs({
        targetColumn: targetColumn,
        predictionType: 'classification',
        transformations: transformations,
        trainBudgetMilliNodeHours: 8000,
        disableEarlyStopping: false,
        optimizationObjective: 'minimize-log-loss',
      });
      const trainingTaskInputs = trainingTaskInputsObj.toValue();
    
      const modelToUpload = {displayName: modelDisplayName};
      const inputDataConfig = {
        datasetId: datasetId,
        fractionSplit: {
          trainingFraction: 0.8,
          validationFraction: 0.1,
          testFraction: 0.1,
        },
      };
      const trainingPipeline = {
        displayName: trainingPipelineDisplayName,
        trainingTaskDefinition:
          'gs://google-cloud-aiplatform/schema/trainingjob/definition/automl_tables_1.0.0.yaml',
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
    
      console.log('Create training pipeline tabular classification response');
      console.log(`Name : ${response.name}`);
      console.log('Raw response:');
      console.log(JSON.stringify(response, null, 2));
    }
    createTrainingPipelineTablesClassification();

### Python

To learn how to install or update the Vertex AI SDK for Python, see [Install the Vertex AI SDK for Python](https://docs.cloud.google.com/vertex-ai/docs/start/use-vertex-ai-python-sdk) . For more information, see the [Python API reference documentation](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest) .

    def create_training_pipeline_tabular_classification_sample(
        project: str,
        display_name: str,
        dataset_id: str,
        location: str = "us-central1",
        model_display_name: str = None,
        target_column: str = "target_column",
        training_fraction_split: float = 0.8,
        validation_fraction_split: float = 0.1,
        test_fraction_split: float = 0.1,
        budget_milli_node_hours: int = 8000,
        disable_early_stopping: bool = False,
        sync: bool = True,
    ):
        aiplatform.init(project=project, location=location)
    
        tabular_classification_job = aiplatform.AutoMLTabularTrainingJob(
            display_name=display_name, optimization_prediction_type="classification"
        )
    
        my_tabular_dataset = aiplatform.TabularDataset(dataset_name=dataset_id)
    
        model = tabular_classification_job.run(
            dataset=my_tabular_dataset,
            target_column=target_column,
            training_fraction_split=training_fraction_split,
            validation_fraction_split=validation_fraction_split,
            test_fraction_split=test_fraction_split,
            budget_milli_node_hours=budget_milli_node_hours,
            model_display_name=model_display_name,
            disable_early_stopping=disable_early_stopping,
            sync=sync,
        )
    
        model.wait()
    
        print(model.display_name)
        print(model.resource_name)
        print(model.uri)
        return model

### Regression

Select a tab for your language or environment:

### REST

You use the [trainingPipelines.create](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.trainingPipelines/create) command to train a model.

Train the model.

Before using any of the request data, make the following replacements:

  - LOCATION : Your region.
  - PROJECT : .
  - TRAININGPIPELINE\_DISPLAY\_NAME : Display name for the training pipeline created for this operation.
  - TARGET\_COLUMN : The column (value) you want this model to predict.
  - WEIGHT\_COLUMN : (Optional) The weight column. [Learn more](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tabular-data/classification-regression/prepare-data#weight) .
  - TRAINING\_BUDGET : The maximum amount of time you want the model to train, in milli node hours (1,000 milli node hours equals one node hour).
  - OPTIMIZATION\_OBJECTIVE : Required only if you do not want the default optimization objective for your prediction type. [Learn more](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tabular-data/classification-regression/train-model#optimization-objectives) .
  - TRANSFORMATION\_TYPE : The transformation type is provided for each column used to train the model. [Learn more](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/datasets/data-types-tabular#transformations) .
  - COLUMN\_NAME : The name of the column with the specified transformation type. Every column used to train the model must be specified.
  - MODEL\_DISPLAY\_NAME : Display name for the newly trained model.
  - DATASET\_ID : ID for the training Dataset.
  - You can provide a `Split` object to control your data split. For information about controlling data split, see [Controlling the data split using REST](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tabular-data/classification-regression/train-model#data-split) .
  - PROJECT\_NUMBER : Your project's automatically generated [project number](https://docs.cloud.google.com/resource-manager/docs/creating-managing-projects#identifiers)

HTTP method and URL:

    POST https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT/locations/LOCATION/trainingPipelines

Request JSON body:

    {
        "displayName": "TRAININGPIPELINE_DISPLAY_NAME",
        "trainingTaskDefinition": "gs://google-cloud-aiplatform/schema/trainingjob/definition/automl_tabular_1.0.0.yaml",
        "trainingTaskInputs": {
            "targetColumn": "TARGET_COLUMN",
            "weightColumn": "WEIGHT_COLUMN",
            "predictionType": "regression",
            "trainBudgetMilliNodeHours": TRAINING_BUDGET,
            "optimizationObjective": "OPTIMIZATION_OBJECTIVE",
            "transformations": [
                {"TRANSFORMATION_TYPE_1":  {"column_name" : "COLUMN_NAME_1"} },
                {"TRANSFORMATION_TYPE_2":  {"column_name" : "COLUMN_NAME_2"} },
                ...
        },
        "modelToUpload": {"displayName": "MODEL_DISPLAY_NAME"},
        "inputDataConfig": {
          "datasetId": "DATASET_ID",
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
         "https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT/locations/LOCATION/trainingPipelines"

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
        -Uri "https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT/locations/LOCATION/trainingPipelines" | Select-Object -Expand Content

You should receive a JSON response similar to the following:

    {
      "name": "projects/PROJECT_NUMBER/locations/us-central1/trainingPipelines/4567",
      "displayName": "myModelName",
      "trainingTaskDefinition": "gs://google-cloud-aiplatform/schema/trainingjob/definition/automl_tabular_1.0.0.yaml",
      "modelToUpload": {
        "displayName": "myModelName"
      },
      "state": "PIPELINE_STATE_PENDING",
      "createTime": "2020-08-18T01:22:57.479336Z",
      "updateTime": "2020-08-18T01:22:57.479336Z"
    }

### Java

Before trying this sample, follow the Java setup instructions in the [Agent Platform quickstart using client libraries](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/start/client-libraries) . For more information, see the [Agent Platform Java API reference documentation](https://docs.cloud.google.com/java/docs/reference/google-cloud-aiplatform/latest/com.google.cloud.aiplatform.v1) .

To authenticate to Agent Platform, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

    import com.google.cloud.aiplatform.util.ValueConverter;
    import com.google.cloud.aiplatform.v1.DeployedModelRef;
    import com.google.cloud.aiplatform.v1.EnvVar;
    import com.google.cloud.aiplatform.v1.FilterSplit;
    import com.google.cloud.aiplatform.v1.FractionSplit;
    import com.google.cloud.aiplatform.v1.InputDataConfig;
    import com.google.cloud.aiplatform.v1.LocationName;
    import com.google.cloud.aiplatform.v1.Model;
    import com.google.cloud.aiplatform.v1.ModelContainerSpec;
    import com.google.cloud.aiplatform.v1.PipelineServiceClient;
    import com.google.cloud.aiplatform.v1.PipelineServiceSettings;
    import com.google.cloud.aiplatform.v1.Port;
    import com.google.cloud.aiplatform.v1.PredefinedSplit;
    import com.google.cloud.aiplatform.v1.PredictSchemata;
    import com.google.cloud.aiplatform.v1.TimestampSplit;
    import com.google.cloud.aiplatform.v1.TrainingPipeline;
    import com.google.cloud.aiplatform.v1.schema.trainingjob.definition.AutoMlTablesInputs;
    import com.google.cloud.aiplatform.v1.schema.trainingjob.definition.AutoMlTablesInputs.Transformation;
    import com.google.cloud.aiplatform.v1.schema.trainingjob.definition.AutoMlTablesInputs.Transformation.AutoTransformation;
    import com.google.cloud.aiplatform.v1.schema.trainingjob.definition.AutoMlTablesInputs.Transformation.TimestampTransformation;
    import com.google.rpc.Status;
    import java.io.IOException;
    import java.util.ArrayList;
    
    public class CreateTrainingPipelineTabularRegressionSample {
    
      public static void main(String[] args) throws IOException {
        // TODO(developer): Replace these variables before running the sample.
        String project = "YOUR_PROJECT_ID";
        String modelDisplayName = "YOUR_DATASET_DISPLAY_NAME";
        String datasetId = "YOUR_DATASET_ID";
        String targetColumn = "TARGET_COLUMN";
        createTrainingPipelineTableRegression(project, modelDisplayName, datasetId, targetColumn);
      }
    
      static void createTrainingPipelineTableRegression(
          String project, String modelDisplayName, String datasetId, String targetColumn)
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
          LocationName locationName = LocationName.of(project, location);
          String trainingTaskDefinition =
              "gs://google-cloud-aiplatform/schema/trainingjob/definition/automl_tables_1.0.0.yaml";
    
          // Set the columns used for training and their data types
          ArrayList<Transformation> tranformations = new ArrayList<>();
          tranformations.add(
              Transformation.newBuilder()
                  .setAuto(AutoTransformation.newBuilder().setColumnName("STRING_5000unique_NULLABLE"))
                  .build());
          tranformations.add(
              Transformation.newBuilder()
                  .setAuto(AutoTransformation.newBuilder().setColumnName("INTEGER_5000unique_NULLABLE"))
                  .build());
          tranformations.add(
              Transformation.newBuilder()
                  .setAuto(AutoTransformation.newBuilder().setColumnName("FLOAT_5000unique_NULLABLE"))
                  .build());
          tranformations.add(
              Transformation.newBuilder()
                  .setAuto(AutoTransformation.newBuilder().setColumnName("FLOAT_5000unique_REPEATED"))
                  .build());
          tranformations.add(
              Transformation.newBuilder()
                  .setAuto(AutoTransformation.newBuilder().setColumnName("NUMERIC_5000unique_NULLABLE"))
                  .build());
          tranformations.add(
              Transformation.newBuilder()
                  .setAuto(AutoTransformation.newBuilder().setColumnName("BOOLEAN_2unique_NULLABLE"))
                  .build());
          tranformations.add(
              Transformation.newBuilder()
                  .setTimestamp(
                      TimestampTransformation.newBuilder()
                          .setColumnName("TIMESTAMP_1unique_NULLABLE")
                          .setInvalidValuesAllowed(true))
                  .build());
          tranformations.add(
              Transformation.newBuilder()
                  .setAuto(AutoTransformation.newBuilder().setColumnName("DATE_1unique_NULLABLE"))
                  .build());
          tranformations.add(
              Transformation.newBuilder()
                  .setAuto(AutoTransformation.newBuilder().setColumnName("TIME_1unique_NULLABLE"))
                  .build());
          tranformations.add(
              Transformation.newBuilder()
                  .setTimestamp(
                      TimestampTransformation.newBuilder()
                          .setColumnName("DATETIME_1unique_NULLABLE")
                          .setInvalidValuesAllowed(true))
                  .build());
          tranformations.add(
              Transformation.newBuilder()
                  .setAuto(
                      AutoTransformation.newBuilder()
                          .setColumnName("STRUCT_NULLABLE.STRING_5000unique_NULLABLE"))
                  .build());
          tranformations.add(
              Transformation.newBuilder()
                  .setAuto(
                      AutoTransformation.newBuilder()
                          .setColumnName("STRUCT_NULLABLE.INTEGER_5000unique_NULLABLE"))
                  .build());
          tranformations.add(
              Transformation.newBuilder()
                  .setAuto(
                      AutoTransformation.newBuilder()
                          .setColumnName("STRUCT_NULLABLE.FLOAT_5000unique_NULLABLE"))
                  .build());
          tranformations.add(
              Transformation.newBuilder()
                  .setAuto(
                      AutoTransformation.newBuilder()
                          .setColumnName("STRUCT_NULLABLE.FLOAT_5000unique_REQUIRED"))
                  .build());
          tranformations.add(
              Transformation.newBuilder()
                  .setAuto(
                      AutoTransformation.newBuilder()
                          .setColumnName("STRUCT_NULLABLE.FLOAT_5000unique_REPEATED"))
                  .build());
          tranformations.add(
              Transformation.newBuilder()
                  .setAuto(
                      AutoTransformation.newBuilder()
                          .setColumnName("STRUCT_NULLABLE.NUMERIC_5000unique_NULLABLE"))
                  .build());
          tranformations.add(
              Transformation.newBuilder()
                  .setAuto(
                      AutoTransformation.newBuilder()
                          .setColumnName("STRUCT_NULLABLE.TIMESTAMP_1unique_NULLABLE"))
                  .build());
    
          AutoMlTablesInputs trainingTaskInputs =
              AutoMlTablesInputs.newBuilder()
                  .addAllTransformations(tranformations)
                  .setTargetColumn(targetColumn)
                  .setPredictionType("regression")
                  .setTrainBudgetMilliNodeHours(8000)
                  .setDisableEarlyStopping(false)
                  // supported regression optimisation objectives: minimize-rmse,
                  // minimize-mae, minimize-rmsle
                  .setOptimizationObjective("minimize-rmse")
                  .build();
    
          FractionSplit fractionSplit =
              FractionSplit.newBuilder()
                  .setTrainingFraction(0.8)
                  .setValidationFraction(0.1)
                  .setTestFraction(0.1)
                  .build();
    
          InputDataConfig inputDataConfig =
              InputDataConfig.newBuilder()
                  .setDatasetId(datasetId)
                  .setFractionSplit(fractionSplit)
                  .build();
          Model modelToUpload = Model.newBuilder().setDisplayName(modelDisplayName).build();
    
          TrainingPipeline trainingPipeline =
              TrainingPipeline.newBuilder()
                  .setDisplayName(modelDisplayName)
                  .setTrainingTaskDefinition(trainingTaskDefinition)
                  .setTrainingTaskInputs(ValueConverter.toValue(trainingTaskInputs))
                  .setInputDataConfig(inputDataConfig)
                  .setModelToUpload(modelToUpload)
                  .build();
    
          TrainingPipeline trainingPipelineResponse =
              pipelineServiceClient.createTrainingPipeline(locationName, trainingPipeline);
    
          System.out.println("Create Training Pipeline Tabular Regression Response");
          System.out.format("\tName: %s\n", trainingPipelineResponse.getName());
          System.out.format("\tDisplay Name: %s\n", trainingPipelineResponse.getDisplayName());
          System.out.format(
              "\tTraining Task Definition: %s\n", trainingPipelineResponse.getTrainingTaskDefinition());
          System.out.format(
              "\tTraining Task Inputs: %s\n", trainingPipelineResponse.getTrainingTaskInputs());
          System.out.format(
              "\tTraining Task Metadata: %s\n", trainingPipelineResponse.getTrainingTaskMetadata());
    
          System.out.format("\tState: %s\n", trainingPipelineResponse.getState());
          System.out.format("\tCreate Time: %s\n", trainingPipelineResponse.getCreateTime());
          System.out.format("\tStart Time: %s\n", trainingPipelineResponse.getStartTime());
          System.out.format("\tEnd Time: %s\n", trainingPipelineResponse.getEndTime());
          System.out.format("\tUpdate Time: %s\n", trainingPipelineResponse.getUpdateTime());
          System.out.format("\tLabels: %s\n", trainingPipelineResponse.getLabelsMap());
    
          InputDataConfig inputDataConfigResponse = trainingPipelineResponse.getInputDataConfig();
          System.out.println("\tInput Data Config");
          System.out.format("\t\tDataset Id: %s\n", inputDataConfigResponse.getDatasetId());
          System.out.format(
              "\t\tAnnotations Filter: %s\n", inputDataConfigResponse.getAnnotationsFilter());
    
          FractionSplit fractionSplitResponse = inputDataConfigResponse.getFractionSplit();
          System.out.println("\t\tFraction Split");
          System.out.format(
              "\t\t\tTraining Fraction: %s\n", fractionSplitResponse.getTrainingFraction());
          System.out.format(
              "\t\t\tValidation Fraction: %s\n", fractionSplitResponse.getValidationFraction());
          System.out.format("\t\t\tTest Fraction: %s\n", fractionSplitResponse.getTestFraction());
    
          FilterSplit filterSplit = inputDataConfigResponse.getFilterSplit();
          System.out.println("\t\tFilter Split");
          System.out.format("\t\t\tTraining Fraction: %s\n", filterSplit.getTrainingFilter());
          System.out.format("\t\t\tValidation Fraction: %s\n", filterSplit.getValidationFilter());
          System.out.format("\t\t\tTest Fraction: %s\n", filterSplit.getTestFilter());
    
          PredefinedSplit predefinedSplit = inputDataConfigResponse.getPredefinedSplit();
          System.out.println("\t\tPredefined Split");
          System.out.format("\t\t\tKey: %s\n", predefinedSplit.getKey());
    
          TimestampSplit timestampSplit = inputDataConfigResponse.getTimestampSplit();
          System.out.println("\t\tTimestamp Split");
          System.out.format("\t\t\tTraining Fraction: %s\n", timestampSplit.getTrainingFraction());
          System.out.format("\t\t\tValidation Fraction: %s\n", timestampSplit.getValidationFraction());
          System.out.format("\t\t\tTest Fraction: %s\n", timestampSplit.getTestFraction());
          System.out.format("\t\t\tKey: %s\n", timestampSplit.getKey());
    
          Model modelResponse = trainingPipelineResponse.getModelToUpload();
          System.out.println("\tModel To Upload");
          System.out.format("\t\tName: %s\n", modelResponse.getName());
          System.out.format("\t\tDisplay Name: %s\n", modelResponse.getDisplayName());
          System.out.format("\t\tDescription: %s\n", modelResponse.getDescription());
          System.out.format("\t\tMetadata Schema Uri: %s\n", modelResponse.getMetadataSchemaUri());
          System.out.format("\t\tMeta Data: %s\n", modelResponse.getMetadata());
          System.out.format("\t\tTraining Pipeline: %s\n", modelResponse.getTrainingPipeline());
          System.out.format("\t\tArtifact Uri: %s\n", modelResponse.getArtifactUri());
    
          System.out.format(
              "\t\tSupported Deployment Resources Types: %s\n",
              modelResponse.getSupportedDeploymentResourcesTypesList().toString());
          System.out.format(
              "\t\tSupported Input Storage Formats: %s\n",
              modelResponse.getSupportedInputStorageFormatsList().toString());
          System.out.format(
              "\t\tSupported Output Storage Formats: %s\n",
              modelResponse.getSupportedOutputStorageFormatsList().toString());
    
          System.out.format("\t\tCreate Time: %s\n", modelResponse.getCreateTime());
          System.out.format("\t\tUpdate Time: %s\n", modelResponse.getUpdateTime());
          System.out.format("\t\tLables: %s\n", modelResponse.getLabelsMap());
          PredictSchemata predictSchemata = modelResponse.getPredictSchemata();
    
          System.out.println("\tPredict Schemata");
          System.out.format("\t\tInstance Schema Uri: %s\n", predictSchemata.getInstanceSchemaUri());
          System.out.format(
              "\t\tParameters Schema Uri: %s\n", predictSchemata.getParametersSchemaUri());
          System.out.format(
              "\t\tPrediction Schema Uri: %s\n", predictSchemata.getPredictionSchemaUri());
    
          for (Model.ExportFormat supportedExportFormat :
              modelResponse.getSupportedExportFormatsList()) {
            System.out.println("\tSupported Export Format");
            System.out.format("\t\tId: %s\n", supportedExportFormat.getId());
          }
          ModelContainerSpec containerSpec = modelResponse.getContainerSpec();
    
          System.out.println("\tContainer Spec");
          System.out.format("\t\tImage Uri: %s\n", containerSpec.getImageUri());
          System.out.format("\t\tCommand: %s\n", containerSpec.getCommandList());
          System.out.format("\t\tArgs: %s\n", containerSpec.getArgsList());
          System.out.format("\t\tPredict Route: %s\n", containerSpec.getPredictRoute());
          System.out.format("\t\tHealth Route: %s\n", containerSpec.getHealthRoute());
    
          for (EnvVar envVar : containerSpec.getEnvList()) {
            System.out.println("\t\tEnv");
            System.out.format("\t\t\tName: %s\n", envVar.getName());
            System.out.format("\t\t\tValue: %s\n", envVar.getValue());
          }
    
          for (Port port : containerSpec.getPortsList()) {
            System.out.println("\t\tPort");
            System.out.format("\t\t\tContainer Port: %s\n", port.getContainerPort());
          }
    
          for (DeployedModelRef deployedModelRef : modelResponse.getDeployedModelsList()) {
            System.out.println("\tDeployed Model");
            System.out.format("\t\tEndpoint: %s\n", deployedModelRef.getEndpoint());
            System.out.format("\t\tDeployed Model Id: %s\n", deployedModelRef.getDeployedModelId());
          }
    
          Status status = trainingPipelineResponse.getError();
          System.out.println("\tError");
          System.out.format("\t\tCode: %s\n", status.getCode());
          System.out.format("\t\tMessage: %s\n", status.getMessage());
        }
      }
    }

### Node.js

Before trying this sample, follow the Node.js setup instructions in the [Agent Platform quickstart using client libraries](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/start/client-libraries) . For more information, see the [Agent Platform Node.js API reference documentation](https://docs.cloud.google.com/nodejs/docs/reference/aiplatform/latest) .

To authenticate to Agent Platform, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

    /**
     * TODO(developer): Uncomment these variables before running the sample.\
     * (Not necessary if passing values as arguments)
     */
    
    // const datasetId = 'YOUR_DATASET_ID';
    // const modelDisplayName = 'YOUR_MODEL_DISPLAY_NAME';
    // const trainingPipelineDisplayName = 'YOUR_TRAINING_PIPELINE_DISPLAY_NAME';
    // const targetColumn = 'YOUR_TARGET_COLUMN';
    // const project = 'YOUR_PROJECT_ID';
    // const location = 'YOUR_PROJECT_LOCATION';
    const aiplatform = require('@google-cloud/aiplatform');
    const {definition} =
      aiplatform.protos.google.cloud.aiplatform.v1.schema.trainingjob;
    
    // Imports the Google Cloud Pipeline Service Client library
    const {PipelineServiceClient} = aiplatform.v1;
    // Specifies the location of the api endpoint
    const clientOptions = {
      apiEndpoint: 'us-central1-aiplatform.googleapis.com',
    };
    
    // Instantiates a client
    const pipelineServiceClient = new PipelineServiceClient(clientOptions);
    
    async function createTrainingPipelineTablesRegression() {
      // Configure the parent resource
      const parent = `projects/${project}/locations/${location}`;
    
      const transformations = [
        {auto: {column_name: 'STRING_5000unique_NULLABLE'}},
        {auto: {column_name: 'INTEGER_5000unique_NULLABLE'}},
        {auto: {column_name: 'FLOAT_5000unique_NULLABLE'}},
        {auto: {column_name: 'FLOAT_5000unique_REPEATED'}},
        {auto: {column_name: 'NUMERIC_5000unique_NULLABLE'}},
        {auto: {column_name: 'BOOLEAN_2unique_NULLABLE'}},
        {
          timestamp: {
            column_name: 'TIMESTAMP_1unique_NULLABLE',
            invalid_values_allowed: true,
          },
        },
        {auto: {column_name: 'DATE_1unique_NULLABLE'}},
        {auto: {column_name: 'TIME_1unique_NULLABLE'}},
        {
          timestamp: {
            column_name: 'DATETIME_1unique_NULLABLE',
            invalid_values_allowed: true,
          },
        },
        {auto: {column_name: 'STRUCT_NULLABLE.STRING_5000unique_NULLABLE'}},
        {auto: {column_name: 'STRUCT_NULLABLE.INTEGER_5000unique_NULLABLE'}},
        {auto: {column_name: 'STRUCT_NULLABLE.FLOAT_5000unique_NULLABLE'}},
        {auto: {column_name: 'STRUCT_NULLABLE.FLOAT_5000unique_REQUIRED'}},
        {auto: {column_name: 'STRUCT_NULLABLE.FLOAT_5000unique_REPEATED'}},
        {auto: {column_name: 'STRUCT_NULLABLE.NUMERIC_5000unique_NULLABLE'}},
        {auto: {column_name: 'STRUCT_NULLABLE.BOOLEAN_2unique_NULLABLE'}},
        {auto: {column_name: 'STRUCT_NULLABLE.TIMESTAMP_1unique_NULLABLE'}},
      ];
    
      const trainingTaskInputsObj = new definition.AutoMlTablesInputs({
        transformations,
        targetColumn,
        predictionType: 'regression',
        trainBudgetMilliNodeHours: 8000,
        disableEarlyStopping: false,
        optimizationObjective: 'minimize-rmse',
      });
      const trainingTaskInputs = trainingTaskInputsObj.toValue();
    
      const modelToUpload = {displayName: modelDisplayName};
      const inputDataConfig = {
        datasetId: datasetId,
        fractionSplit: {
          trainingFraction: 0.8,
          validationFraction: 0.1,
          testFraction: 0.1,
        },
      };
      const trainingPipeline = {
        displayName: trainingPipelineDisplayName,
        trainingTaskDefinition:
          'gs://google-cloud-aiplatform/schema/trainingjob/definition/automl_tables_1.0.0.yaml',
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
    
      console.log('Create training pipeline tabular regression response');
      console.log(`Name : ${response.name}`);
      console.log('Raw response:');
      console.log(JSON.stringify(response, null, 2));
    }
    createTrainingPipelineTablesRegression();

### Python

To learn how to install or update the Vertex AI SDK for Python, see [Install the Vertex AI SDK for Python](https://docs.cloud.google.com/vertex-ai/docs/start/use-vertex-ai-python-sdk) . For more information, see the [Python API reference documentation](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest) .

    def create_training_pipeline_tabular_regression_sample(
        project: str,
        display_name: str,
        dataset_id: str,
        location: str = "us-central1",
        model_display_name: str = "my_model",
        target_column: str = "target_column",
        training_fraction_split: float = 0.8,
        validation_fraction_split: float = 0.1,
        test_fraction_split: float = 0.1,
        budget_milli_node_hours: int = 8000,
        disable_early_stopping: bool = False,
        sync: bool = True,
    ):
        aiplatform.init(project=project, location=location)
    
        tabular_regression_job = aiplatform.AutoMLTabularTrainingJob(
            display_name=display_name, optimization_prediction_type="regression"
        )
    
        my_tabular_dataset = aiplatform.TabularDataset(dataset_name=dataset_id)
    
        model = tabular_regression_job.run(
            dataset=my_tabular_dataset,
            target_column=target_column,
            training_fraction_split=training_fraction_split,
            validation_fraction_split=validation_fraction_split,
            test_fraction_split=test_fraction_split,
            budget_milli_node_hours=budget_milli_node_hours,
            model_display_name=model_display_name,
            disable_early_stopping=disable_early_stopping,
            sync=sync,
        )
    
        model.wait()
    
        print(model.display_name)
        print(model.resource_name)
        print(model.uri)
        return model

## Control the data split using REST

You can control how your training data is split between the training, validation, and test sets. When you use the Agent Platform API, use the [`Split` object](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.trainingPipelines#InputDataConfig) to determine your data split. The `Split` object can be included in the `inputDataConfig` object as one of several object types, each of which provides a different way to split the training data.

The methods you use to split your data depend on your data type:

  - `FractionSplit` :
    
      - TRAINING\_FRACTION : The fraction of the training data to use for the training set.
      - VALIDATION\_FRACTION : The fraction of the training data to use for the validation set.
      - TEST\_FRACTION : The fraction of the training data to use for the test set.
    
    If you specify any of the fractions, specify all. The fractions must add up to 1.0. [Learn more](https://docs.cloud.google.com/gemini-enterprise-agent-platform/tabular-data/data-splits) .
    
        "fractionSplit": {
        "trainingFraction": TRAINING_FRACTION,
        "validationFraction": VALIDATION_FRACTION,
        "testFraction": TEST_FRACTION
        },

  - `PredefinedSplit` :
    
      - DATA\_SPLIT\_COLUMN : The column containing the data split values ( `TRAIN` , `VALIDATION` , `TEST` ).
    
    Manually specify the data split for each row by using a split column. [Learn more](https://docs.cloud.google.com/gemini-enterprise-agent-platform/tabular-data/data-splits) .
    
        "predefinedSplit": {
          "key": DATA_SPLIT_COLUMN
        },

  - `TimestampSplit` :
    
      - TRAINING\_FRACTION : The percentage of the training data to use for the training set. Defaults to 0.80.
      - VALIDATION\_FRACTION : The percentage of the training data to use for the validation set. Defaults to 0.10.
      - TEST\_FRACTION : The percentage of the training data to use for the test set. Defaults to 0.10.
      - TIME\_COLUMN : The column containing the timestamps.
    
    If you specify any of the fractions, specify all. The fractions must add up to 1.0. [Learn more](https://docs.cloud.google.com/gemini-enterprise-agent-platform/tabular-data/data-splits) .
    
        "timestampSplit": {
          "trainingFraction": TRAINING_FRACTION,
          "validationFraction": VALIDATION_FRACTION,
          "testFraction": TEST_FRACTION,
          "key": TIME_COLUMN
        }

## Optimization objectives for classification or regression models

When you train a model, Agent Platform selects a default optimization objective based on your model type and the data type used for your target column.

Classification models are best for:

| Optimization objective | API value                      | Use this objective if you want to...                                                                                                               |
| ---------------------- | ------------------------------ | -------------------------------------------------------------------------------------------------------------------------------------------------- |
| AUC ROC                | `maximize-au-roc`              | Maximize the area under the receiver operating characteristic (ROC) curve. Distinguishes between classes. Default value for binary classification. |
| Log loss               | `minimize-log-loss`            | Keep inferences probabilities as accurate as possible. Only supported objective for multi-class classification.                                    |
| AUC PR                 | `maximize-au-prc`              | Maximize the area under the precision-recall curve. Optimizes results for inferences for the less common class.                                    |
| Precision at Recall    | `maximize-precision-at-recall` | Optimize precision at a specific recall value.                                                                                                     |
| Recall at Precision    | `maximize-recall-at-precision` | Optimize recall at a specific precision value.                                                                                                     |

Regression models are best for:

| Optimization objective | API value        | Use this objective if you want to...                                                                                                                                        |
| ---------------------- | ---------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| RMSE                   | `minimize-rmse`  | Minimize root-mean-squared error (RMSE). Captures more extreme values accurately. Default value.                                                                            |
| MAE                    | `minimize-mae`   | Minimize mean-absolute error (MAE). Views extreme values as outliers with less impact on model.                                                                             |
| RMSLE                  | `minimize-rmsle` | Minimize root-mean-squared log error (RMSLE). Penalizes error on relative size rather than absolute value. Useful when both predicted and actual values can be quite large. |

## What's next

  - [Evaluate your model](https://docs.cloud.google.com/gemini-enterprise-agent-platform/tabular-data/classification-regression/evaluate-model) .
  - Learn how to [export your model](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/export/export-model-tabular) .
