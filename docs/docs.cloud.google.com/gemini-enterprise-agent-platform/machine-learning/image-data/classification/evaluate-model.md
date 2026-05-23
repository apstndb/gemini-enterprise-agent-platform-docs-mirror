---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/image-data/classification/evaluate-model
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/image-data/classification/evaluate-model
title: Evaluate and iterate AutoML image classification models
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

This page shows you how to evaluate your AutoML image classification models so that you can iterate on your model.

Gemini Enterprise Agent Platform provides model evaluation metrics to help you determine the performance of your models, such as precision and recall metrics. Agent Platform calculates evaluation metrics by using the [test set](https://docs.cloud.google.com/vertex-ai/docs/general/ml-use) .

## How you use model evaluation metrics

Model evaluation metrics provide quantitative measurements of how your model performed on the test set. How you interpret and use those metrics depends on your business need and the problem your model is trained to solve. For example, you might have a lower tolerance for false positives than for false negatives or the other way around. These kinds of questions affect which metrics you would focus on.

For more information about iterating on your model to improve its performance, see [Iterating on your model](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/image-data/classification/evaluate-model#iterate) .

## Evaluation metrics returned by Agent Platform

Agent Platform returns several different evaluation metrics such as precision, recall, and confidence thresholds. The metrics that Agent Platform returns depend on your model's objective. For example, Agent Platform provides different evaluation metrics for an image classification model compared to an image object detection model.

A schema file, downloadable from a Cloud Storage location, determines which evaluation metrics Agent Platform provides for each objective. The following tabs provide links to the schema files and describes the evaluation metrics for each model objective.

You can view and download schema files from the following Cloud Storage location:  
[gs://google-cloud-aiplatform/schema/modelevaluation/](https://console.cloud.google.com/storage/browser/google-cloud-aiplatform/schema/modelevaluation)

  - **AuPRC** : The [area under the precision-recall (PR) curve](https://developers.google.com/machine-learning/glossary#pr-auc-area-under-the-pr-curve) , also referred to as average precision. This value ranges from zero to one, where a higher value indicates a higher-quality model.
  - **Log loss** : The cross-entropy between the model inferences and the target values. This ranges from zero to infinity, where a lower value indicates a higher-quality model.
  - **Confidence threshold** : A confidence score that determines which inferences to return. A model returns inferences that are at this value or higher. A higher confidence threshold increases precision but lowers recall. Agent Platform returns confidence metrics at different threshold values to show how the threshold affects [precision](https://developers.google.com/machine-learning/glossary#precision) and [recall](https://developers.google.com/machine-learning/glossary#recall) .
  - **Recall** : The fraction of inferences with this class that the model correctly predicted. Also called *true positive rate* .
  - **Precision** : The fraction of classification inferences produced by the model that were correct.
  - **Confusion matrix** : A [confusion matrix](https://developers.google.com/machine-learning/glossary#confusion-matrix) shows how often a model correctly predicted a result. For incorrectly predicted results, the matrix shows what the model predicted instead. The confusion matrix helps you understand where your model is "confusing" two results.

## Getting evaluation metrics

You can get an aggregate set of evaluation metrics for your model and, for some objectives, evaluation metrics for a particular class or label. Evaluation metrics for a particular class or label is also known as an *evaluation slice* . The following content describes how to get aggregate evaluation metrics and evaluation slices by using the Google Cloud console or API.

### Google Cloud console

1.  In the Google Cloud console, in the Agent Platform section, go to the **Models** page.

2.  In the **Region** drop-down, select the region where your model is located.

3.  From the list of models, click your model, which opens the model's **Evaluate** tab.
    
    In the **Evaluate** tab, you can view your model's aggregate evaluation metrics, such as the **Average precision** and **Recall** .
    
    If the model objective has evaluation slices, the console shows a list of labels. You can click a label to view evaluation metrics for that label, as shown in the following example:
    
    ![label selection in console](https://docs.cloud.google.com/static/gemini-enterprise-agent-platform/machine-learning/training/images/evaluate-label.png)
    
    ( [Preview](https://cloud.google.com/terms/service-terms#1) ) For each label, you can view predicted images grouped as true positives, false positives, and false negatives. Each image has a L2-squared distance metric that measures how similar the image is from the training images. An image labeled with an **Outlier** badge is relatively dissimilar from all training images. To improve model performance, you should consider adding more training images that are similar to the outliers.

### API

API requests for getting evaluation metrics is the same for each data type and objective, but the outputs are different. The following samples show the same request but different responses.

#### Getting aggregate model evaluation metrics

The aggregate model evaluation metrics provide information about the model as a whole. To see information about a specific slice, list the [model evaluation slices](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/image-data/classification/evaluate-model#list-slices) .

To view aggregate model evaluation metrics, use the [`projects.locations.models.evaluations.get`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.models.evaluations) method.

Agent Platform returns an array of confidence metrics. Each element shows evaluation metrics at a different `confidenceThreshold` value (starting from 0 and going up to 1). By viewing different threshold values, you can see how the threshold affects other metrics such as precision and recall.

Select a tab that corresponds to your language or environment:

### REST

Before using any of the request data, make the following replacements:

  - LOCATION : Region where your model is stored.
  - PROJECT : Your \[project ID\](/resource-manager/docs/creating-managing-projects\#identifiers). .
  - MODEL\_ID : The ID of the model resource .
  - PROJECT\_NUMBER : Your project's automatically generated [project number](https://docs.cloud.google.com/resource-manager/docs/creating-managing-projects#identifiers) .
  - EVALUATION\_ID : ID for the model evaluation (appears in the response).

HTTP method and URL:

    GET https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT/locations/LOCATION/models/MODEL_ID/evaluations

To send your request, choose one of these options:

#### curl

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) , or by using [Cloud Shell](https://docs.cloud.google.com/shell/docs) , which automatically logs you into the `gcloud` CLI . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Execute the following command:

    curl -X GET \
         -H "Authorization: Bearer $(gcloud auth print-access-token)" \
         "https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT/locations/LOCATION/models/MODEL_ID/evaluations"

#### PowerShell

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Execute the following command:

    $cred = gcloud auth print-access-token
    $headers = @{ "Authorization" = "Bearer $cred" }
    
    Invoke-WebRequest `
        -Method GET `
        -Headers $headers `
        -Uri "https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT/locations/LOCATION/models/MODEL_ID/evaluations" | Select-Object -Expand Content

You should receive a JSON response similar to the following:

#### Response

    {
      "modelEvaluations": [
        {
          "name": "projects/PROJECT_NUMBER/locations/LOCATION/models/MODEL_ID/evaluations/EVALUATION_ID",
          "metricsSchemaUri": "gs://google-cloud-aiplatform/schema/modelevaluation/classification_metrics_1.0.0.yaml",
          "metrics": {
            "auPrc": 0.9946683,
            "logLoss": 0.043421753,
            "confidenceMetrics": [
              {
                "recall": 1,
                "precision": 0.2
              },
              {
                "confidenceThreshold": 0.05,
                "recall": 0.98637605,
                "precision": 0.8960396
              },
              {
                "confidenceThreshold": 0.1,
                "recall": 0.98637605,
                "precision": 0.92346936
              },
              {
                "confidenceThreshold": 0.15,
                "recall": 0.9782016,
                "precision": 0.93979055
              },
              ...
            ],
            "confusionMatrix": {
              "annotationSpecs": [
                {
                  "id": "216348703974227968",
                  "displayName": "tulips"
                },
                {
                  "id": "1369270208581074944",
                  "displayName": "dandelion"
                },
                {
                  "id": "2522191713187921920",
                  "displayName": "sunflowers"
                },
                {
                  "id": "4828034722401615872",
                  "displayName": "daisy"
                },
                {
                  "id": "7133877731615309824",
                  "displayName": "roses"
                }
              ],
              "rows": [
                [
                  78,
                  0,
                  0,
                  0,
                  2
                ],
                [
                  0,
                  89,
                  0,
                  1,
                  0
                ],
                [
                  1,
                  0,
                  67,
                  1,
                  1
                ],
                [
                  0,
                  1,
                  0,
                  61,
                  1
                ],
                [
                  6,
                  0,
                  0,
                  0,
                  58
                ]
              ]
            }
          },
          "createTime": "2020-10-08T23:35:54.559702Z",
          "sliceDimensions": [
            "annotationSpec"
          ]
        }
      ]
    }

### Java

Before trying this sample, follow the Java setup instructions in the [Agent Platform quickstart using client libraries](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/start/client-libraries) .

To authenticate to Agent Platform, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

    import com.google.cloud.aiplatform.v1.ModelEvaluation;
    import com.google.cloud.aiplatform.v1.ModelEvaluationName;
    import com.google.cloud.aiplatform.v1.ModelServiceClient;
    import com.google.cloud.aiplatform.v1.ModelServiceSettings;
    import java.io.IOException;
    
    public class GetModelEvaluationImageClassificationSample {
    
      public static void main(String[] args) throws IOException {
        // TODO(developer): Replace these variables before running the sample.
        // To obtain evaluationId run the code block below after setting modelServiceSettings.
        //
        // try (ModelServiceClient modelServiceClient = ModelServiceClient.create(modelServiceSettings))
        // {
        //   String location = "us-central1";
        //   ModelName modelFullId = ModelName.of(project, location, modelId);
        //   ListModelEvaluationsRequest modelEvaluationsrequest =
        //   ListModelEvaluationsRequest.newBuilder().setParent(modelFullId.toString()).build();
        //   for (ModelEvaluation modelEvaluation :
        //     modelServiceClient.listModelEvaluations(modelEvaluationsrequest).iterateAll()) {
        //       System.out.format("Model Evaluation Name: %s%n", modelEvaluation.getName());
        //   }
        // }
        String project = "YOUR_PROJECT_ID";
        String modelId = "YOUR_MODEL_ID";
        String evaluationId = "YOUR_EVALUATION_ID";
        getModelEvaluationImageClassificationSample(project, modelId, evaluationId);
      }
    
      static void getModelEvaluationImageClassificationSample(
          String project, String modelId, String evaluationId) throws IOException {
        ModelServiceSettings modelServiceSettings =
            ModelServiceSettings.newBuilder()
                .setEndpoint("us-central1-aiplatform.googleapis.com:443")
                .build();
    
        // Initialize client that will be used to send requests. This client only needs to be created
        // once, and can be reused for multiple requests. After completing all of your requests, call
        // the "close" method on the client to safely clean up any remaining background resources.
        try (ModelServiceClient modelServiceClient = ModelServiceClient.create(modelServiceSettings)) {
          String location = "us-central1";
          ModelEvaluationName modelEvaluationName =
              ModelEvaluationName.of(project, location, modelId, evaluationId);
    
          ModelEvaluation modelEvaluation = modelServiceClient.getModelEvaluation(modelEvaluationName);
    
          System.out.println("Get Model Evaluation Image Classification Response");
          System.out.format("Model Name: %s\n", modelEvaluation.getName());
          System.out.format("Metrics Schema Uri: %s\n", modelEvaluation.getMetricsSchemaUri());
          System.out.format("Metrics: %s\n", modelEvaluation.getMetrics());
          System.out.format("Create Time: %s\n", modelEvaluation.getCreateTime());
          System.out.format("Slice Dimensions: %s\n", modelEvaluation.getSliceDimensionsList());
        }
      }
    }

### Node.js

Before trying this sample, follow the Node.js setup instructions in the [Agent Platform quickstart using client libraries](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/start/client-libraries) .

To authenticate to Agent Platform, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

    /**
     * TODO(developer): Uncomment these variables before running the sample
     * (not necessary if passing values as arguments). To obtain evaluationId,
     * instantiate the client and run the following the commands.
     */
    // const parentName = `projects/${project}/locations/${location}/models/${modelId}`;
    // const evalRequest = {
    //   parent: parentName
    // };
    // const [evalResponse] = await modelServiceClient.listModelEvaluations(evalRequest);
    // console.log(evalResponse);
    
    // const modelId = 'YOUR_MODEL_ID';
    // const evaluationId = 'YOUR_EVALUATION_ID';
    // const project = 'YOUR_PROJECT_ID';
    // const location = 'YOUR_PROJECT_LOCATION';
    
    // Imports the Google Cloud Model Service Client library
    const {ModelServiceClient} = require('@google-cloud/aiplatform');
    
    // Specifies the location of the api endpoint
    const clientOptions = {
      apiEndpoint: 'us-central1-aiplatform.googleapis.com',
    };
    
    // Instantiates a client
    const modelServiceClient = new ModelServiceClient(clientOptions);
    
    async function getModelEvaluationImageClassification() {
      // Configure the name resources
      const name = `projects/${project}/locations/${location}/models/${modelId}/evaluations/${evaluationId}`;
      const request = {
        name,
      };
    
      // Create get model evaluation request
      const [response] = await modelServiceClient.getModelEvaluation(request);
    
      console.log('Get model evaluation image classification response');
      console.log(`\tName : ${response.name}`);
      console.log(`\tMetrics schema uri : ${response.metricsSchemaUri}`);
      console.log(`\tMetrics : ${JSON.stringify(response.metrics)}`);
      console.log(`\tCreate time : ${JSON.stringify(response.createTime)}`);
      console.log(`\tSlice dimensions : ${response.sliceDimensions}`);
    
      const modelExplanation = response.modelExplanation;
      if (modelExplanation === null) {
        console.log(`\tModel explanation: ${JSON.stringify(modelExplanation)}`);
      } else {
        const meanAttributions = modelExplanation.meanAttributions;
        for (const meanAttribution of meanAttributions) {
          console.log('\t\tMean attribution');
          console.log(
            `\t\t\tBaseline output value : \
               ${meanAttribution.baselineOutputValue}`
          );
          console.log(
            `\t\t\tInstance output value : \
               ${meanAttribution.instanceOutputValue}`
          );
          console.log(
            `\t\t\tFeature attributions : \
               ${JSON.stringify(meanAttribution.featureAttributions)}`
          );
          console.log(`\t\t\tOutput index : ${meanAttribution.outputIndex}`);
          console.log(
            `\t\t\tOutput display name : \
               ${meanAttribution.outputDisplayName}`
          );
          console.log(
            `\t\t\tApproximation error : \
               ${meanAttribution.approximationError}`
          );
        }
      }
    }
    getModelEvaluationImageClassification();

### Python

To learn how to install or update the Vertex AI SDK for Python, see [Install the Vertex AI SDK for Python](https://docs.cloud.google.com/vertex-ai/docs/start/use-vertex-ai-python-sdk) . For more information, see the [Python API reference documentation](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest) .

    from google.cloud import aiplatform
    
    
    def get_model_evaluation_image_classification_sample(
        project: str,
        model_id: str,
        evaluation_id: str,
        location: str = "us-central1",
        api_endpoint: str = "us-central1-aiplatform.googleapis.com",
    ):
        """
        To obtain evaluation_id run the following commands where LOCATION
        is the region where the model is stored, PROJECT is the project ID,
        and MODEL_ID is the ID of your model.
    
        model_client = aiplatform.gapic.ModelServiceClient(
            client_options={
                'api_endpoint':'LOCATION-aiplatform.googleapis.com'
                }
            )
        evaluations = model_client.list_model_evaluations(parent='projects/PROJECT/locations/LOCATION/models/MODEL_ID')
        print("evaluations:", evaluations)
        """
        # The AI Platform services require regional API endpoints.
        client_options = {"api_endpoint": api_endpoint}
        # Initialize client that will be used to create and send requests.
        # This client only needs to be created once, and can be reused for multiple requests.
        client = aiplatform.gapic.ModelServiceClient(client_options=client_options)
        name = client.model_evaluation_path(
            project=project, location=location, model=model_id, evaluation=evaluation_id
        )
        response = client.get_model_evaluation(name=name)
        print("response:", response)

#### Listing all evaluation slices

The [`projects.locations.models.evaluations.slices.list`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.models.evaluations.slices/list) method lists all evaluation slices for your model. You must have the model's evaluation ID, which you can get when you [view the aggregated evaluation metrics](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/image-data/classification/evaluate-model#aggregate) .

You can use model evaluation slices to determine how the model performed on a specific label. The `value` field tells you which label the metrics are for.

Agent Platform returns an array of confidence metrics. Each element shows evaluation metrics at a different `confidenceThreshold` value (starting from 0 and going up to 1). By viewing different threshold values, you can see how the threshold affects other metrics such as precision and recall.

### REST

Before using any of the request data, make the following replacements:

  - LOCATION : Region where Model is located. For example, `us-central1` .
  - PROJECT : .
  - MODEL\_ID : The ID of your model.
  - EVALUATION\_ID : ID of the model evaluation that contains the evaluation slices to list.

HTTP method and URL:

    GET https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT/locations/LOCATION/models/MODEL_ID/evaluations/EVALUATION_ID/slices

To send your request, choose one of these options:

#### curl

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) , or by using [Cloud Shell](https://docs.cloud.google.com/shell/docs) , which automatically logs you into the `gcloud` CLI . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Execute the following command:

    curl -X GET \
         -H "Authorization: Bearer $(gcloud auth print-access-token)" \
         "https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT/locations/LOCATION/models/MODEL_ID/evaluations/EVALUATION_ID/slices"

#### PowerShell

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Execute the following command:

    $cred = gcloud auth print-access-token
    $headers = @{ "Authorization" = "Bearer $cred" }
    
    Invoke-WebRequest `
        -Method GET `
        -Headers $headers `
        -Uri "https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT/locations/LOCATION/models/MODEL_ID/evaluations/EVALUATION_ID/slices" | Select-Object -Expand Content

You should receive a JSON response similar to the following:

#### Response

    {
      "modelEvaluationSlices": [
        {
          "name": "projects/123456789012/locations/us-central1/models/1232584574060974976/evaluations/1234057709820346880/slices/123455414369100579",
          "slice": {
            "dimension": "annotationSpec",
            "value": "daisy"
          },
          "metricsSchemaUri": "gs://google-cloud-aiplatform/schema/modelevaluation/classification_metrics_1.0.0.yaml",
          "metrics": {
            "auPrc": 0.99713016,
            "auRoc": 0.99942565,
            "logLoss": 0.025896452,
            "confidenceMetrics": [
              {
                "recall": 1,
                "precision": 0.17166212
              },
              {
                "confidenceThreshold": 0.05,
                "recall": 1,
                "precision": 0.9402985
              },
              {
                "confidenceThreshold": 0.1,
                "recall": 1,
                "precision": 0.95454544
              },
              ...
          },
          "createTime": "2020-10-08T23:35:54.770876Z"
        },
        {
          "name": "projects/123456789012/locations/us-central1/models/1232584574060974976/evaluations/1234057709820346880/slices/123455414369101230",
          "slice": {
            "dimension": "annotationSpec",
            "value": "sunflowers"
          },
          "metricsSchemaUri": "gs://google-cloud-aiplatform/schema/modelevaluation/classification_metrics_1.0.0.yaml",
          "metrics": {
            "auPrc": 0.99369764,
            "auRoc": 0.9978355,
            "logLoss": 0.049820196,
            "confidenceMetrics": [
              {
                "recall": 1,
                "precision": 0.1907357
              },
              {
                "confidenceThreshold": 0.05,
                "recall": 0.95714283,
                "precision": 0.9852941
              },
              {
                "confidenceThreshold": 0.1,
                "recall": 0.95714283,
                "precision": 0.9852941
              },
              ...
          },
          "createTime": "2020-10-08T23:35:54.770876Z"
        }
      ]
    }

### Java

Before trying this sample, follow the Java setup instructions in the [Agent Platform quickstart using client libraries](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/start/client-libraries) .

To authenticate to Agent Platform, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

    import com.google.cloud.aiplatform.v1.ModelEvaluationName;
    import com.google.cloud.aiplatform.v1.ModelEvaluationSlice;
    import com.google.cloud.aiplatform.v1.ModelEvaluationSlice.Slice;
    import com.google.cloud.aiplatform.v1.ModelServiceClient;
    import com.google.cloud.aiplatform.v1.ModelServiceSettings;
    import java.io.IOException;
    
    public class ListModelEvaluationSliceSample {
    
      public static void main(String[] args) throws IOException {
        // TODO(developer): Replace these variables before running the sample.
        // To obtain evaluationId run the code block below after setting modelServiceSettings.
        //
        // try (ModelServiceClient modelServiceClient = ModelServiceClient.create(modelServiceSettings))
        // {
        //   String location = "us-central1";
        //   ModelName modelFullId = ModelName.of(project, location, modelId);
        //   ListModelEvaluationsRequest modelEvaluationsrequest =
        //   ListModelEvaluationsRequest.newBuilder().setParent(modelFullId.toString()).build();
        //   for (ModelEvaluation modelEvaluation :
        //     modelServiceClient.listModelEvaluations(modelEvaluationsrequest).iterateAll()) {
        //       System.out.format("Model Evaluation Name: %s%n", modelEvaluation.getName());
        //   }
        // }
        String project = "YOUR_PROJECT_ID";
        String modelId = "YOUR_MODEL_ID";
        String evaluationId = "YOUR_EVALUATION_ID";
        listModelEvaluationSliceSample(project, modelId, evaluationId);
      }
    
      static void listModelEvaluationSliceSample(String project, String modelId, String evaluationId)
          throws IOException {
        ModelServiceSettings modelServiceSettings =
            ModelServiceSettings.newBuilder()
                .setEndpoint("us-central1-aiplatform.googleapis.com:443")
                .build();
    
        // Initialize client that will be used to send requests. This client only needs to be created
        // once, and can be reused for multiple requests. After completing all of your requests, call
        // the "close" method on the client to safely clean up any remaining background resources.
        try (ModelServiceClient modelServiceClient = ModelServiceClient.create(modelServiceSettings)) {
          String location = "us-central1";
          ModelEvaluationName modelEvaluationName =
              ModelEvaluationName.of(project, location, modelId, evaluationId);
    
          for (ModelEvaluationSlice modelEvaluationSlice :
              modelServiceClient.listModelEvaluationSlices(modelEvaluationName).iterateAll()) {
            System.out.format("Model Evaluation Slice Name: %s\n", modelEvaluationSlice.getName());
            System.out.format("Metrics Schema Uri: %s\n", modelEvaluationSlice.getMetricsSchemaUri());
            System.out.format("Metrics: %s\n", modelEvaluationSlice.getMetrics());
            System.out.format("Create Time: %s\n", modelEvaluationSlice.getCreateTime());
    
            Slice slice = modelEvaluationSlice.getSlice();
            System.out.format("Slice Dimensions: %s\n", slice.getDimension());
            System.out.format("Slice Value: %s\n\n", slice.getValue());
          }
        }
      }
    }

### Node.js

Before trying this sample, follow the Node.js setup instructions in the [Agent Platform quickstart using client libraries](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/start/client-libraries) .

To authenticate to Agent Platform, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

    /**
     * TODO(developer): Uncomment these variables before running the sample
     * (not necessary if passing values as arguments). To obtain evaluationId,
     * instantiate the client and run the following the commands.
     */
    // const parentName = `projects/${project}/locations/${location}/models/${modelId}`;
    // const evalRequest = {
    //   parent: parentName
    // };
    // const [evalResponse] = await modelServiceClient.listModelEvaluations(evalRequest);
    // console.log(evalResponse);
    
    // const modelId = 'YOUR_MODEL_ID';
    // const evaluationId = 'YOUR_EVALUATION_ID';
    // const project = 'YOUR_PROJECT_ID';
    // const location = 'YOUR_PROJECT_LOCATION';
    
    // Imports the Google Cloud Model Service Client library
    const {ModelServiceClient} = require('@google-cloud/aiplatform');
    
    // Specifies the location of the api endpoint
    const clientOptions = {
      apiEndpoint: 'us-central1-aiplatform.googleapis.com',
    };
    
    // Instantiates a client
    const modelServiceClient = new ModelServiceClient(clientOptions);
    
    async function listModelEvaluationSlices() {
      // Configure the parent resources
      const parent = `projects/${project}/locations/${location}/models/${modelId}/evaluations/${evaluationId}`;
      const request = {
        parent,
      };
    
      // Get and print out a list of all the evaluation slices for this resource
      const [response] =
        await modelServiceClient.listModelEvaluationSlices(request);
      console.log('List model evaluation response', response);
      console.log(response);
    }
    listModelEvaluationSlices();

### Python

To learn how to install or update the Vertex AI SDK for Python, see [Install the Vertex AI SDK for Python](https://docs.cloud.google.com/vertex-ai/docs/start/use-vertex-ai-python-sdk) . For more information, see the [Python API reference documentation](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest) .

    from google.cloud import aiplatform
    
    
    def list_model_evaluation_slices_sample(
        project: str,
        model_id: str,
        evaluation_id: str,
        location: str = "us-central1",
        api_endpoint: str = "us-central1-aiplatform.googleapis.com",
    ):
        """
        To obtain evaluation_id run the following commands where LOCATION
        is the region where the model is stored, PROJECT is the project ID,
        and MODEL_ID is the ID of your model.
    
        model_client = aiplatform.gapic.ModelServiceClient(
            client_options={
                'api_endpoint':'LOCATION-aiplatform.googleapis.com'
                }
            )
        evaluations = model_client.list_model_evaluations(parent='projects/PROJECT/locations/LOCATION/models/MODEL_ID')
        print("evaluations:", evaluations)
        """
        # The AI Platform services require regional API endpoints.
        client_options = {"api_endpoint": api_endpoint}
        # Initialize client that will be used to create and send requests.
        # This client only needs to be created once, and can be reused for multiple requests.
        client = aiplatform.gapic.ModelServiceClient(client_options=client_options)
        parent = client.model_evaluation_path(
            project=project, location=location, model=model_id, evaluation=evaluation_id
        )
        response = client.list_model_evaluation_slices(parent=parent)
        for model_evaluation_slice in response:
            print("model_evaluation_slice:", model_evaluation_slice)

#### Getting metrics for a single slice

To view evaluation metrics for a single slice, use the [`projects.locations.models.evaluations.slices.get`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.models.evaluations.slices/get) method. You must have the slice ID, which is provided when you [list all slices](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/image-data/classification/evaluate-model#list-slices) . The following sample applies to all data types and objectives.

### REST

Before using any of the request data, make the following replacements:

  - LOCATION : Region where Model is located. For example, us-central1.
  - PROJECT : .
  - MODEL\_ID : The ID of your model.
  - EVALUATION\_ID : ID of the model evaluation that contains the evaluation slice to retrieve.
  - SLICE\_ID : ID of an evaluation slice to get.
  - PROJECT\_NUMBER : Your project's automatically generated [project number](https://docs.cloud.google.com/resource-manager/docs/creating-managing-projects#identifiers) .
  - EVALUATION\_METRIC\_SCHEMA\_FILE\_NAME : The name of a schema file that defines the evaluation metrics to return such as `classification_metrics_1.0.0` .

HTTP method and URL:

    GET https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT/locations/LOCATION/models/MODEL_ID/evaluations/EVALUATION_ID/slices/SLICE_ID

To send your request, choose one of these options:

#### curl

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) , or by using [Cloud Shell](https://docs.cloud.google.com/shell/docs) , which automatically logs you into the `gcloud` CLI . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Execute the following command:

    curl -X GET \
         -H "Authorization: Bearer $(gcloud auth print-access-token)" \
         "https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT/locations/LOCATION/models/MODEL_ID/evaluations/EVALUATION_ID/slices/SLICE_ID"

#### PowerShell

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Execute the following command:

    $cred = gcloud auth print-access-token
    $headers = @{ "Authorization" = "Bearer $cred" }
    
    Invoke-WebRequest `
        -Method GET `
        -Headers $headers `
        -Uri "https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT/locations/LOCATION/models/MODEL_ID/evaluations/EVALUATION_ID/slices/SLICE_ID" | Select-Object -Expand Content

You should receive a JSON response similar to the following:

#### Response

    {
      "name": "projects/PROJECT_NUMBER/locations/LOCATION/models/MODEL_ID/evaluations/EVALUATION_ID/slices/SLICE_ID",
      "slice": {
        "dimension": "annotationSpec",
        "value": "a particular class or label"
      },
      "metricsSchemaUri": "gs://google-cloud-aiplatform/schema/modelevaluation/EVALUATION_METRIC_SCHEMA_FILE_NAME.yaml",
      "metrics": {
        evaluation metrics for the slice
      },
      "createTime": "2020-10-08T23:35:54.770876Z"
    }

### Java

Before trying this sample, follow the Java setup instructions in the [Agent Platform quickstart using client libraries](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/start/client-libraries) .

To authenticate to Agent Platform, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

    import com.google.cloud.aiplatform.v1.ModelEvaluationSlice;
    import com.google.cloud.aiplatform.v1.ModelEvaluationSlice.Slice;
    import com.google.cloud.aiplatform.v1.ModelEvaluationSliceName;
    import com.google.cloud.aiplatform.v1.ModelServiceClient;
    import com.google.cloud.aiplatform.v1.ModelServiceSettings;
    import java.io.IOException;
    
    public class GetModelEvaluationSliceSample {
    
      public static void main(String[] args) throws IOException {
        // TODO(developer): Replace these variables before running the sample.
        // To obtain evaluationId run the code block below after setting modelServiceSettings.
        //
        // try (ModelServiceClient modelServiceClient = ModelServiceClient.create(modelServiceSettings))
        // {
        //   String location = "us-central1";
        //   ModelName modelFullId = ModelName.of(project, location, modelId);
        //   ListModelEvaluationsRequest modelEvaluationsrequest =
        //   ListModelEvaluationsRequest.newBuilder().setParent(modelFullId.toString()).build();
        //   for (ModelEvaluation modelEvaluation :
        //     modelServiceClient.listModelEvaluations(modelEvaluationsrequest).iterateAll()) {
        //       System.out.format("Model Evaluation Name: %s%n", modelEvaluation.getName());
        //   }
        // }
        String project = "YOUR_PROJECT_ID";
        String modelId = "YOUR_MODEL_ID";
        String evaluationId = "YOUR_EVALUATION_ID";
        String sliceId = "YOUR_SLICE_ID";
        getModelEvaluationSliceSample(project, modelId, evaluationId, sliceId);
      }
    
      static void getModelEvaluationSliceSample(
          String project, String modelId, String evaluationId, String sliceId) throws IOException {
        ModelServiceSettings modelServiceSettings =
            ModelServiceSettings.newBuilder()
                .setEndpoint("us-central1-aiplatform.googleapis.com:443")
                .build();
    
        // Initialize client that will be used to send requests. This client only needs to be created
        // once, and can be reused for multiple requests. After completing all of your requests, call
        // the "close" method on the client to safely clean up any remaining background resources.
        try (ModelServiceClient modelServiceClient = ModelServiceClient.create(modelServiceSettings)) {
          String location = "us-central1";
          ModelEvaluationSliceName modelEvaluationSliceName =
              ModelEvaluationSliceName.of(project, location, modelId, evaluationId, sliceId);
    
          ModelEvaluationSlice modelEvaluationSlice =
              modelServiceClient.getModelEvaluationSlice(modelEvaluationSliceName);
    
          System.out.println("Get Model Evaluation Slice Response");
          System.out.format("Model Evaluation Slice Name: %s\n", modelEvaluationSlice.getName());
          System.out.format("Metrics Schema Uri: %s\n", modelEvaluationSlice.getMetricsSchemaUri());
          System.out.format("Metrics: %s\n", modelEvaluationSlice.getMetrics());
          System.out.format("Create Time: %s\n", modelEvaluationSlice.getCreateTime());
    
          Slice slice = modelEvaluationSlice.getSlice();
          System.out.format("Slice Dimensions: %s\n", slice.getDimension());
          System.out.format("Slice Value: %s\n", slice.getValue());
        }
      }
    }

### Node.js

Before trying this sample, follow the Node.js setup instructions in the [Agent Platform quickstart using client libraries](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/start/client-libraries) .

To authenticate to Agent Platform, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

    /**
     * TODO(developer): Uncomment these variables before running the sample
     * (not necessary if passing values as arguments). To obtain evaluationId,
     * instantiate the client and run the following the commands.
     */
    // const parentName = `projects/${project}/locations/${location}/models/${modelId}`;
    // const evalRequest = {
    //   parent: parentName
    // };
    // const [evalResponse] = await modelServiceClient.listModelEvaluations(evalRequest);
    // console.log(evalResponse);
    
    // const modelId = 'YOUR_MODEL_ID';
    // const evaluationId = 'YOUR_EVALUATION_ID';
    // const sliceId = 'YOUR_SLICE_ID';
    // const project = 'YOUR_PROJECT_ID';
    // const location = 'YOUR_PROJECT_LOCATION';
    
    // Imports the Google Cloud Model Service client library
    const {ModelServiceClient} = require('@google-cloud/aiplatform');
    // Specifies the location of the api endpoint
    const clientOptions = {
      apiEndpoint: 'us-central1-aiplatform.googleapis.com',
    };
    // Specifies the location of the api endpoint
    const modelServiceClient = new ModelServiceClient(clientOptions);
    
    async function getModelEvaluationSlice() {
      // Configure the parent resource
      const name = `projects/${project}/locations/${location}/models/${modelId}/evaluations/${evaluationId}/slices/${sliceId}`;
      const request = {
        name,
      };
    
      // Get and print out a list of all the endpoints for this resource
      const [response] =
        await modelServiceClient.getModelEvaluationSlice(request);
    
      console.log('Get model evaluation slice');
      console.log(`\tName : ${response.name}`);
      console.log(`\tMetrics_Schema_Uri : ${response.metricsSchemaUri}`);
      console.log(`\tMetrics : ${JSON.stringify(response.metrics)}`);
      console.log(`\tCreate time : ${JSON.stringify(response.createTime)}`);
    
      console.log('Slice');
      const slice = response.slice;
      console.log(`\tDimension :${slice.dimension}`);
      console.log(`\tValue :${slice.value}`);
    }
    getModelEvaluationSlice();

### Python

To learn how to install or update the Vertex AI SDK for Python, see [Install the Vertex AI SDK for Python](https://docs.cloud.google.com/vertex-ai/docs/start/use-vertex-ai-python-sdk) . For more information, see the [Python API reference documentation](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest) .

    from google.cloud import aiplatform
    
    
    def get_model_evaluation_slice_sample(
        project: str,
        model_id: str,
        evaluation_id: str,
        slice_id: str,
        location: str = "us-central1",
        api_endpoint: str = "us-central1-aiplatform.googleapis.com",
    ):
        """
        To obtain evaluation_id run the following commands where LOCATION
        is the region where the model is stored, PROJECT is the project ID,
        and MODEL_ID is the ID of your model.
    
        model_client = aiplatform.gapic.ModelServiceClient(
            client_options={
                'api_endpoint':'LOCATION-aiplatform.googleapis.com'
                }
            )
        evaluations = model_client.list_model_evaluations(parent='projects/PROJECT/locations/LOCATION/models/MODEL_ID')
        print("evaluations:", evaluations)
        """
        # The AI Platform services require regional API endpoints.
        client_options = {"api_endpoint": api_endpoint}
        # Initialize client that will be used to create and send requests.
        # This client only needs to be created once, and can be reused for multiple requests.
        client = aiplatform.gapic.ModelServiceClient(client_options=client_options)
        name = client.model_evaluation_slice_path(
            project=project,
            location=location,
            model=model_id,
            evaluation=evaluation_id,
            slice=slice_id,
        )
        response = client.get_model_evaluation_slice(name=name)
        print("response:", response)

## Iterate on your model

Model evaluation metrics provide a starting point for debugging your model when the model isn't meeting your expectations. For example, low precision and recall scores can indicate that your model needs additional training data or has inconsistent labels. Perfect precision and recall can indicate that the test data is too easy to predict and might not generalize well.

You can iterate on your training data and create a new model. After you create a new model, you can compare the evaluation metrics between the existing model and the new model.

The following suggestions can help you improve models that label items, such as classification or detection models:

  - Consider adding more examples or a wider range of examples in your training data. For example, for an image classification model, you might include wider angle images, higher or lower resolution images, or different points of view. For more guidance, see [Preparing data](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/image-data/classification/prepare-data) .
  - Consider removing classes or labels that don't have a lot of examples. Insufficient examples prevent the model from consistently and confidently making predictions about those classes or labels.
  - Machines can't interpret the name of your classes or labels and don't understand the nuances between them, such as "door" and "door\_with\_knob." You must provide data to help machines recognize such nuances.
  - Augment your data with more examples of true positives and true negatives, especially examples that are close to a decision boundary to mitigate model confusion.
  - Specify your own data split (training, validation, and test). Agent Platform randomly assigns items to each set. Therefore, near-duplicates can be allocated in the training and validation sets, which could lead to overfitting and then poor performance on the test set. For more information about setting your own data split, see [About data splits for AutoML models](https://docs.cloud.google.com/vertex-ai/docs/general/ml-use) .
  - If your model's evaluation metrics include a confusion matrix, you can see if the model is confusing two labels, where the model is predicting a particular label significantly more than the true label. Review your data and make sure the examples are correctly labeled.
  - If you had a short training time (low maximum number of node hours), you might get a higher-quality model by allowing it to train for a longer period of time (higher maximum number of node hours).
