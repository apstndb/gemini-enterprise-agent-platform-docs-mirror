---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tabular-data/classification-regression/evaluate-model
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tabular-data/classification-regression/evaluate-model
title: Evaluate AutoML classification and regression models
description: Evaluate AutoML classification and regression models in Agent Platform.
data_source: docs.cloud.google.com
---

This page shows you how to evaluate your AutoML classification and regression models.

Gemini Enterprise Agent Platform provides model evaluation metrics to help you determine the performance of your models, such as precision and recall metrics. Agent Platform calculates evaluation metrics by using the [test set](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tabular-data/data-splits) .

## Before you begin

Before you evaluate your model, [train the model](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tabular-data/classification-regression/train-model) .

## How you use model evaluation metrics

Model evaluation metrics provide quantitative measurements of how your model performed on the test set. How you interpret and use those metrics depends on your business need and the problem your model is trained to solve. For example, you might have a lower tolerance for false positives than for false negatives or the other way around. These kinds of questions affect which metrics you focus on.

## Get evaluation metrics

You can get an aggregate set of [evaluation metrics](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tabular-data/classification-regression/evaluate-model#metrics) for your model and, for some objectives, evaluation metrics for a particular class or label. Evaluation metrics for a particular class or label is also known as an *evaluation slice* . The following content describes how to get aggregate evaluation metrics and evaluation slices by using the Google Cloud console or API.

### Google Cloud console

1.  In the Google Cloud console, in the Agent Platform section, go to the **Models** page.

2.  In the **Region** drop-down, select the region where your model is located.

3.  From the list of models, click your model, which opens the model's **Evaluate** tab.
    
    In the **Evaluate** tab, you can view your model's aggregate evaluation metrics, such as the **Average precision** and **Recall** .
    
    If the model objective has evaluation slices, the console shows a list of labels. You can click a label to view evaluation metrics for that label, as shown in the following example:
    
    ![label selection in console](https://docs.cloud.google.com/static/gemini-enterprise-agent-platform/machine-learning/tabular-data/classification-regression/images/evaluate-label.png)

### API

API requests for getting evaluation metrics are the same for each data type and objective, but the outputs are different. The following samples show the same request but different responses.

#### Get aggregate model evaluation metrics

The aggregate model evaluation metrics provide information about the model as a whole. To see information about a specific slice, list the [model evaluation slices](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tabular-data/classification-regression/evaluate-model#list-slices) .

To view aggregate model evaluation metrics, use the [`projects.locations.models.evaluations.get`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.models.evaluations) method.

Select the tab below for your objective:

### Classification

Agent Platform returns an array of confidence metrics. Each element shows evaluation metrics at a different `confidenceThreshold` value (starting from 0 and going up to 1). By viewing different threshold values, you can see how the threshold affects other metrics such as precision and recall.

Select a tab that corresponds to your language or environment:

### REST

Before using any of the request data, make the following replacements:

  - LOCATION : Region where your model is stored.
  - PROJECT : Your [project ID](https://docs.cloud.google.com/resource-manager/docs/creating-managing-projects#identifiers) .
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
            "auPrc": 0.97762364,
            "auRoc": 0.97566897,
            "logLoss": 0.19153881,
            "confidenceMetrics": [
              {
                "recall": 1,
                "precision": 0.5,
                "falsePositiveRate": 1,
                "f1Score": 0.6666667,
                "recallAt1": 0.90911126,
                "precisionAt1": 0.90911126,
                "falsePositiveRateAt1": 0.09088874,
                "f1ScoreAt1": 0.90911126,
                "truePositiveCount": "4467",
                "falsePositiveCount": "4467"
              },
              {
                "confidenceThreshold": 0.003269856,
                "recall": 0.9997761,
                "precision": 0.56993365,
                "falsePositiveRate": 0.7544213,
                "f1Score": 0.7260018,
                "recallAt1": 0.90911126,
                "precisionAt1": 0.90911126,
                "falsePositiveRateAt1": 0.09088874,
                "f1ScoreAt1": 0.90911126,
                "truePositiveCount": "4466",
                "falsePositiveCount": "3370",
                "falseNegativeCount": "1",
                "trueNegativeCount": "1097"
              },
              {
                "confidenceThreshold": 0.1103351,
                "recall": 0.9899261,
                "precision": 0.79819494,
                "falsePositiveRate": 0.25027984,
                "f1Score": 0.8837814,
                "recallAt1": 0.90911126,
                "precisionAt1": 0.90911126,
                "falsePositiveRateAt1": 0.09088874,
                "f1ScoreAt1": 0.90911126,
                "truePositiveCount": "4422",
                "falsePositiveCount": "1118",
                "falseNegativeCount": "45",
                "trueNegativeCount": "3349"
              },
              ...
            ],
            "confusionMatrix": {
              "annotationSpecs": [
                {
                  "displayName": "1"
                },
                {
                  "displayName": "2"
                }
              ],
              "rows": [
                [
                  3817,
                  140
                ],
                [
                  266,
                  244
                ]
              ]
            }
          },
          "createTime": "2020-10-09T00:19:15.463930Z",
          "sliceDimensions": [
            "annotationSpec"
          ],
          "modelExplanation": {
            "meanAttributions": [
              {
                "featureAttributions": {
                  "Age": 0.022972771897912025,
                  "Job": 0.031542550772428513,
                  "MaritalStatus": 0.015506803058087826,
                  "Education": 0.019189134240150452,
                  "Default": 0.00021766019926872104,
                  "Balance": 0.031217793002724648,
                  "Housing": 0.06786702573299408,
                  "Loan": 0.0072592208161950111,
                  "Contact": 0.083566240966320038,
                  "Day": 0.074894927442073822,
                  "Month": 0.19679982960224152,
                  "Duration": 0.35500210523605347,
                  "Campaign": 0.033425047993659973,
                  "PDays": 0.013902961276471615,
                  "Previous": 0.0061685866676270962,
                  "POutcome": 0.040467333048582077
                }
              }
            ]
          }
        }
      ]
    }

### Java

Before trying this sample, follow the Java setup instructions in the [Agent Platform quickstart using client libraries](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/start/client-libraries) . For more information, see the [Agent Platform Java API reference documentation](https://docs.cloud.google.com/java/docs/reference/google-cloud-aiplatform/latest/com.google.cloud.aiplatform.v1) .

To authenticate to Agent Platform, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

    import com.google.cloud.aiplatform.v1.ModelEvaluation;
    import com.google.cloud.aiplatform.v1.ModelEvaluationName;
    import com.google.cloud.aiplatform.v1.ModelServiceClient;
    import com.google.cloud.aiplatform.v1.ModelServiceSettings;
    import java.io.IOException;
    
    public class GetModelEvaluationTabularClassificationSample {
    
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
        getModelEvaluationTabularClassification(project, modelId, evaluationId);
      }
    
      static void getModelEvaluationTabularClassification(
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
    
          System.out.println("Get Model Evaluation Tabular Classification Response");
          System.out.format("\tName: %s\n", modelEvaluation.getName());
          System.out.format("\tMetrics Schema Uri: %s\n", modelEvaluation.getMetricsSchemaUri());
          System.out.format("\tMetrics: %s\n", modelEvaluation.getMetrics());
          System.out.format("\tCreate Time: %s\n", modelEvaluation.getCreateTime());
          System.out.format("\tSlice Dimensions: %s\n", modelEvaluation.getSliceDimensionsList());
        }
      }
    }

### Node.js

Before trying this sample, follow the Node.js setup instructions in the [Agent Platform quickstart using client libraries](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/start/client-libraries) . For more information, see the [Agent Platform Node.js API reference documentation](https://docs.cloud.google.com/nodejs/docs/reference/aiplatform/latest) .

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
    
    async function getModelEvaluationTabularClassification() {
      // Configure the parent resources
      const name = `projects/${project}/locations/${location}/models/${modelId}/evaluations/${evaluationId}`;
      const request = {
        name,
      };
    
      // Get model evaluation request
      const [response] = await modelServiceClient.getModelEvaluation(request);
    
      console.log('Get model evaluation tabular classification response');
      console.log(`\tName : ${response.name}`);
      console.log(`\tMetrics schema uri : ${response.metricsSchemaUri}`);
      console.log(`\tMetrics : ${JSON.stringify(response.metrics)}`);
      console.log(`\tCreate time : ${JSON.stringify(response.createTime)}`);
      console.log(`\tSlice dimensions : ${response.sliceDimensions}`);
    
      const modelExplanation = response.modelExplanation;
      console.log('\tModel explanation');
      if (!modelExplanation) {
        console.log('\t\t{}');
      } else {
        const meanAttributions = modelExplanation.meanAttributions;
        if (!meanAttributions) {
          console.log('\t\t\t []');
        } else {
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
    }
    getModelEvaluationTabularClassification();

### Python

To learn how to install or update the Vertex AI SDK for Python, see [Install the Vertex AI SDK for Python](https://docs.cloud.google.com/vertex-ai/docs/start/use-vertex-ai-python-sdk) . For more information, see the [Python API reference documentation](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest) .

    from google.cloud import aiplatform
    
    
    def get_model_evaluation_tabular_classification_sample(
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

### Regression

Select a tab that corresponds to your language or environment:

### REST

Before using any of the request data, make the following replacements:

  - LOCATION : Region where your model is stored.
  - PROJECT : .
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
          "metricsSchemaUri": "gs://google-cloud-aiplatform/schema/modelevaluation/regression_metrics_1.0.0.yaml",
          "metrics": {
            "rootMeanSquaredError": 2553.6309,
            "meanAbsoluteError": 1373.3932,
            "meanAbsolutePercentageError": "Infinity",
            "rSquared": 0.060764354,
            "rootMeanSquaredLogError": "NaN"
          },
          "createTime": "2020-10-09T01:20:37.045482Z",
          "modelExplanation": {
            "meanAttributions": [
              {
                "featureAttributions": {
                  "Age": 0.22535169124603271,
                  "Job": 0.049311652779579163,
                  "MaritalStatus": 0.033439181745052338,
                  "Education": 0.10934026539325714,
                  "Default": 0.021301545202732086,
                  "Housing": 0.0631907731294632,
                  "Loan": 0.055760543793439865,
                  "Contact": 0.010930608958005905,
                  "Day": 0.14066702127456665,
                  "Month": 0.17570944130420685,
                  "Duration": 0.054339192807674408,
                  "Campaign": 0.015468073077499866,
                  "PDays": 0.020416950806975365,
                  "Previous": 0.0037290120963007212,
                  "POutcome": 0.0040646209381520748,
                  "Deposit": 0.016979435458779335
                }
              }
            ]
          }
        }
      ]
    }

### Java

Before trying this sample, follow the Java setup instructions in the [Agent Platform quickstart using client libraries](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/start/client-libraries) . For more information, see the [Agent Platform Java API reference documentation](https://docs.cloud.google.com/java/docs/reference/google-cloud-aiplatform/latest/com.google.cloud.aiplatform.v1) .

To authenticate to Agent Platform, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

    import com.google.cloud.aiplatform.v1.ModelEvaluation;
    import com.google.cloud.aiplatform.v1.ModelEvaluationName;
    import com.google.cloud.aiplatform.v1.ModelServiceClient;
    import com.google.cloud.aiplatform.v1.ModelServiceSettings;
    import java.io.IOException;
    
    public class GetModelEvaluationTabularRegressionSample {
    
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
        getModelEvaluationTabularRegression(project, modelId, evaluationId);
      }
    
      static void getModelEvaluationTabularRegression(
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
    
          System.out.println("Get Model Evaluation Tabular Regression Response");
          System.out.format("\tName: %s\n", modelEvaluation.getName());
          System.out.format("\tMetrics Schema Uri: %s\n", modelEvaluation.getMetricsSchemaUri());
          System.out.format("\tMetrics: %s\n", modelEvaluation.getMetrics());
          System.out.format("\tCreate Time: %s\n", modelEvaluation.getCreateTime());
          System.out.format("\tSlice Dimensions: %s\n", modelEvaluation.getSliceDimensionsList());
        }
      }
    }

### Node.js

Before trying this sample, follow the Node.js setup instructions in the [Agent Platform quickstart using client libraries](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/start/client-libraries) . For more information, see the [Agent Platform Node.js API reference documentation](https://docs.cloud.google.com/nodejs/docs/reference/aiplatform/latest) .

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
    
    async function getModelEvaluationTabularRegression() {
      // Configure the parent resources
      const name = `projects/${project}/locations/${location}/models/${modelId}/evaluations/${evaluationId}`;
      const request = {
        name,
      };
    
      // Get model evaluation request
      const [response] = await modelServiceClient.getModelEvaluation(request);
    
      console.log('Get model evaluation tabular regression response');
      console.log(`\tName : ${response.name}`);
      console.log(`\tMetrics schema uri : ${response.metricsSchemaUri}`);
      console.log(`\tMetrics : ${JSON.stringify(response.metrics)}`);
      console.log(`\tCreate time : ${JSON.stringify(response.createTime)}`);
      console.log(`\tSlice dimensions : ${response.sliceDimensions}`);
    
      const modelExplanation = response.modelExplanation;
      console.log('\tModel explanation');
      if (!modelExplanation) {
        console.log('\t\t{}');
      } else {
        const meanAttributions = modelExplanation.meanAttributions;
        if (!meanAttributions) {
          console.log('\t\t\t []');
        } else {
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
    }
    getModelEvaluationTabularRegression();

### Python

To learn how to install or update the Vertex AI SDK for Python, see [Install the Vertex AI SDK for Python](https://docs.cloud.google.com/vertex-ai/docs/start/use-vertex-ai-python-sdk) . For more information, see the [Python API reference documentation](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest) .

    from google.cloud import aiplatform
    
    
    def get_model_evaluation_tabular_regression_sample(
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

#### List all evaluation slices (classification models only)

The [`projects.locations.models.evaluations.slices.list`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.models.evaluations.slices/list) method lists all evaluation slices for your model. You must have the model's evaluation ID, which you can get when you [view the aggregated evaluation metrics](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tabular-data/classification-regression/evaluate-model#aggregate) .

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
          "name": "projects/693884908213/locations/us-central1/models/705305922892726272/evaluations/4515484958386859492/slices/1785244630562158241",
          "slice": {
            "dimension": "annotationSpec",
            "value": "2"
          },
          "metricsSchemaUri": "gs://google-cloud-aiplatform/schema/modelevaluation/classification_metrics_1.0.0.yaml",
          "metrics": {
            "auPrc": 0.6108714,
            "auRoc": 0.9362428,
            "logLoss": 0.9680687,
            "confidenceMetrics": [
              {
                "recall": 1,
                "precision": 0.11417058,
                "falsePositiveRate": 1,
                "f1Score": 0.20494273,
                "recallAt1": 0.47843137,
                "precisionAt1": 0.6354167,
                "falsePositiveRateAt1": 0.035380337,
                "f1ScoreAt1": 0.5458613,
                "truePositiveCount": "510",
                "falsePositiveCount": "3957"
              },
              {
                "confidenceThreshold": 0.003269856,
                "recall": 0.9980392,
                "precision": 0.15108341,
                "falsePositiveRate": 0.7227698,
                "f1Score": 0.26243877,
                "recallAt1": 0.47843137,
                "precisionAt1": 0.6354167,
                "falsePositiveRateAt1": 0.035380337,
                "f1ScoreAt1": 0.5458613,
                "truePositiveCount": "509",
                "falsePositiveCount": "2860",
                "falseNegativeCount": "1",
                "trueNegativeCount": "1097"
              },
              {
                "confidenceThreshold": 0.016592776,
                "recall": 0.9882353,
                "precision": 0.23344141,
                "falsePositiveRate": 0.41824615,
                "f1Score": 0.37766954,
                "recallAt1": 0.47843137,
                "precisionAt1": 0.6354167,
                "falsePositiveRateAt1": 0.035380337,
                "f1ScoreAt1": 0.5458613,
                "truePositiveCount": "504",
                "falsePositiveCount": "1655",
                "falseNegativeCount": "6",
                "trueNegativeCount": "2302"
              },
              ...
            ]
          },
          "createTime": "2020-10-09T00:19:15.480435Z"
        },
        {
          "name": "projects/693884908213/locations/us-central1/models/705305922892726272/evaluations/4515484958386859492/slices/8107013027312442123",
          "slice": {
            "dimension": "annotationSpec",
            "value": "1"
          },
          "metricsSchemaUri": "gs://google-cloud-aiplatform/schema/modelevaluation/classification_metrics_1.0.0.yaml",
          "metrics": {
            "auPrc": 0.9916441,
            "auRoc": 0.93830043,
            "logLoss": 0.09145534,
            "confidenceMetrics": [
              {
                "recall": 1,
                "precision": 0.8858294,
                "falsePositiveRate": 1,
                "f1Score": 0.93945867,
                "recallAt1": 0.96461964,
                "precisionAt1": 0.9348518,
                "falsePositiveRateAt1": 0.52156866,
                "f1ScoreAt1": 0.94950247,
                "truePositiveCount": "3957",
                "falsePositiveCount": "510"
              },
              {
                "confidenceThreshold": 0.064618945,
                "recall": 0.9997473,
                "precision": 0.88639927,
                "falsePositiveRate": 0.9941176,
                "f1Score": 0.93966746,
                "recallAt1": 0.96461964,
                "precisionAt1": 0.9348518,
                "falsePositiveRateAt1": 0.52156866,
                "f1ScoreAt1": 0.94950247,
                "truePositiveCount": "3956",
                "falsePositiveCount": "507",
                "falseNegativeCount": "1",
                "trueNegativeCount": "3"
              },
              ...

### Java

Before trying this sample, follow the Java setup instructions in the [Agent Platform quickstart using client libraries](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/start/client-libraries) . For more information, see the [Agent Platform Java API reference documentation](https://docs.cloud.google.com/java/docs/reference/google-cloud-aiplatform/latest/com.google.cloud.aiplatform.v1) .

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

Before trying this sample, follow the Node.js setup instructions in the [Agent Platform quickstart using client libraries](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/start/client-libraries) . For more information, see the [Agent Platform Node.js API reference documentation](https://docs.cloud.google.com/nodejs/docs/reference/aiplatform/latest) .

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

#### Get metrics for a single slice

To view evaluation metrics for a single slice, use the [`projects.locations.models.evaluations.slices.get`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.models.evaluations.slices/get) method. You must have the slice ID, which is provided when you [list all slices](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tabular-data/classification-regression/evaluate-model#list-slices) . The following sample applies to all data types and objectives.

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

Before trying this sample, follow the Java setup instructions in the [Agent Platform quickstart using client libraries](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/start/client-libraries) . For more information, see the [Agent Platform Java API reference documentation](https://docs.cloud.google.com/java/docs/reference/google-cloud-aiplatform/latest/com.google.cloud.aiplatform.v1) .

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

Before trying this sample, follow the Node.js setup instructions in the [Agent Platform quickstart using client libraries](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/start/client-libraries) . For more information, see the [Agent Platform Node.js API reference documentation](https://docs.cloud.google.com/nodejs/docs/reference/aiplatform/latest) .

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

## Model evaluation metrics

Agent Platform returns several different evaluation metrics, such as precision, recall, and confidence thresholds. The metrics that Agent Platform returns depend on your model's objective. For example, Agent Platform provides different evaluation metrics for an image classification model compared to an image object detection model.

A schema file determines which evaluation metrics Agent Platform provides for each objective.

You can view and download schema files from the following Cloud Storage location:  
[gs://google-cloud-aiplatform/schema/modelevaluation/](https://console.cloud.google.com/storage/browser/google-cloud-aiplatform/schema/modelevaluation)

The evaluation metrics are:

### Classification

  - **AuPRC** : The [area under the precision-recall (PR) curve](https://developers.google.com/machine-learning/glossary#pr-auc-area-under-the-pr-curve) , also referred to as average precision. This value ranges from zero to one, where a higher value indicates a higher-quality model.
  - **AuROC** : The [area under receiver operating characteristic curve](https://developers.google.com/machine-learning/glossary#auc-area-under-the-roc-curve) . This ranges from zero to one, where a higher value indicates a higher-quality model.
  - **Log loss** : The cross-entropy between the model inferences and the target values. This ranges from zero to infinity, where a lower value indicates a higher-quality model.
  - **Confidence threshold** : A confidence score that determines which inferences to return. A model returns inferences that are at this value or higher. A higher confidence threshold increases precision but lowers recall. Agent Platform returns confidence metrics at different threshold values to show how the threshold affects [precision](https://developers.google.com/machine-learning/glossary#precision) and [recall](https://developers.google.com/machine-learning/glossary#recall) .
  - **Recall** : The fraction of inferences with this class that the model correctly predicted. Also called *true positive rate* .
  - **Recall at 1** : The recall (true positive rate) when only considering the label that has the highest inference score and not below the confidence threshold for each example.
  - **Precision** : The fraction of classification inferences produced by the model that were correct.
  - **Precision at 1** : The precision when only considering the label that has the highest inference score and not below the confidence threshold for each example.
  - **F1 score** : The harmonic mean of precision and recall. F1 is a useful metric if you're looking for a balance between precision and recall and there's an uneven class distribution.
  - **F1 score at 1** : The harmonic mean of recall at 1 and precision at 1.
  - **True negative count** : The number of times a model correctly predicted a negative class.
  - **True positive count** : The number of times a model correctly predicted a positive class.
  - **False negative count** : The number of times a model mistakenly predicted a negative class.
  - **False positive count** : The number of times a model mistakenly predicted a positive class.
  - **False positive rate** : The fraction of incorrectly predicted results out of all predicted results.
  - **False positive rate at 1** : The false positive rate when only considering the label that has the highest inference score and not below the confidence threshold for each example.
  - **Confusion matrix** : A [confusion matrix](https://developers.google.com/machine-learning/glossary#confusion-matrix) shows how often a model correctly predicted a result. For incorrectly predicted results, the matrix shows what the model predicted instead. The confusion matrix helps you understand where your model is "confusing" two results.
  - **Model feature attributions** : Agent Platform shows you how much each feature impacts a model. The values are provided as a percentage for each feature: the higher the percentage, the more impact the feature had on model training. Review this information to ensure that all of the most important features make sense for your data and business problem. To learn more, see [Feature attributions for classification and regression](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tabular-data/classification-explanations) .

### Regression

  - **MAE** : The mean absolute error (MAE) is the average absolute difference between the target values and the predicted values. This metric ranges from zero to infinity; a lower value indicates a higher quality model.
  - **RMSE** : The root-mean-squared error is the square root of the average squared difference between the target and predicted values. RMSE is more sensitive to outliers than MAE,so if you're concerned about large errors, then RMSE can be a more useful metric to evaluate. Similar to MAE, a smaller value indicates a higher quality model (0 represents a perfect predictor).
  - **RMSLE** : The root-mean-squared logarithmic error metric is similar to RMSE, except that it uses the natural logarithm of the predicted and actual values plus 1. RMSLE penalizes under-inference more heavily than over-inference. It can also be a good metric when you don't want to penalize differences for large inference values more heavily than for small inference values. This metric ranges from zero to infinity; a lower value indicates a higher quality model. The RMSLE evaluation metric is returned only if all label and predicted values are non-negative.
  - **r^2** : r squared (r^2) is the square of the Pearson correlation coefficient between the labels and predicted values. This metric ranges between zero and one. A higher value indicates a closer fit to the regression line.
  - **MAPE** : Mean absolute percentage error (MAPE) is the average absolute percentage difference between the labels and the predicted values. This metric ranges between zero and infinity; a lower value indicates a higher quality model.  
    MAPE is not shown if the target column contains any 0 values. In this case, MAPE is undefined.
  - **Model feature attributions** : Agent Platform shows you how much each feature impacts a model. The values are provided as a percentage for each feature: the higher the percentage, the more impact the feature had on model training. Review this information to ensure that all of the most important features make sense for your data and business problem. To learn more, see [Feature attributions for classification and regression](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tabular-data/classification-explanations) .

## What's next

Once you're ready to make predictions with your classification or regression model, you have two options:

  - [Make online (real-time) predictions using your model](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tabular-data/classification-regression/get-online-predictions) .
  - [Get batch predictions directly from your model](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tabular-data/classification-regression/get-batch-predictions) .

Additionally, you can:

  - [View the architecture of your model](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tabular-data/classification-regression/logging) .
  - Learn how to [export your model](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/export/export-model-tabular) .
