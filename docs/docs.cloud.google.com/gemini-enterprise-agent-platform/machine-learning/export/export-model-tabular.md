---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/export/export-model-tabular
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/export/export-model-tabular
title: Export AutoML tabular models
description: Export your AutoML tabular model to Cloud Storage, download the model, and then use Docker to make the model available for predictions in Gemini Enterprise Agent Platform.
data_source: docs.cloud.google.com
---

This page describes how to use Gemini Enterprise Agent Platform to export your AutoML tabular model to Cloud Storage, download the model to an on-premises server or a server hosted by another cloud provider, and then use Docker to make the model available for predictions.

For information about exporting image and video Edge models, see [Export AutoML Edge models](https://docs.cloud.google.com/vertex-ai/docs/export/export-edge-model) .

After exporting your tabular model, if you want to import it back into Agent Platform, see [Import models to Agent Platform](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/model-registry/import-model) .

## Limitations

Exporting AutoML tabular models has the following limitations:

  - You can export AutoML tabular classification and regression models only. Exporting AutoML tabular forecasting models isn't supported.

  - Vertex Explainable AI isn't available using exported tabular models. If you need to use Vertex Explainable AI, you must serve predictions from a model hosted by Agent Platform.

  - The exported tabular model can run only on x86 architecture CPUs that support Advanced Vector Extensions (AVX) instruction sets.

## Export process

The steps for exporting your model are:

1.  [Set up your environment](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/export/export-model-tabular#before-you-begin) .
2.  [Export the model](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/export/export-model-tabular#export) .
3.  [Pull and run the model server](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/export/export-model-tabular#pull-and-run-server) .
4.  [Request predictions](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/export/export-model-tabular#get-predictions) .

## Before you begin

Before you can complete this task, you must have completed the following tasks:

  - Set up your project as described in [Set up a project and a development environment](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/start/cloud-environment) .
  - [Train the model](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training-overview#automl) that you want to download.
  - Install and initialize the [Google Cloud CLI](https://docs.cloud.google.com/sdk/docs) on the server you will use to run the exported model.
  - Install [Docker](https://hub.docker.com/search/?type=edition&offering=community) on your server.

## Export the model

### Console

1.  In the Google Cloud console, in the Agent Platform section, go to the **Models** page.

2.  Click the tabular model you want to export to open its details page.

3.  Click **Export** in the button bar to export your model.

4.  Select or create a Cloud Storage folder in the desired location.
    
    The bucket must meet the [bucket requirements](https://docs.cloud.google.com/gemini-enterprise-agent-platform/docs/general/locations#buckets) .
    
    You cannot export a model to a top-level bucket. You must use at least one level of folder.
    
    For best results, create a new, empty folder. You will copy the entire contents of the folder in a later step.

5.  Click **Export** .
    
    You will download the exported model to your server in the next section.

### REST

You use the [models.export](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.models/export) method to export a model to Cloud Storage.

Before using any of the request data, make the following replacements:

  - LOCATION : Your region.

  - PROJECT : Your [project ID](https://docs.cloud.google.com/resource-manager/docs/creating-managing-projects#identifiers) .

  - MODEL\_ID : the ID of the model you want to export.

  - GCS\_DESTINATION : your destination folder in Cloud Storage. For example, `gs://export-bucket/exports` .
    
    You cannot export a model to a top-level bucket. You must use at least one level of folder.
    
    The folder must conform to the [bucket requirements](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/locations#buckets) .
    
    For best results, create a new folder. You will copy the entire contents of the folder in a later step.

HTTP method and URL:

    POST https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT/locations/LOCATION/models/MODEL_ID:export

Request JSON body:

    {
      "outputConfig": {
        "exportFormatId": "tf-saved-model",
        "artifactDestination": {
          "outputUriPrefix": "GCS_DESTINATION"
        }
      }
    }

To send your request, choose one of these options:

#### curl

Save the request body in a file named `request.json` , and execute the following command:

    curl -X POST \
         -H "Authorization: Bearer $(gcloud auth print-access-token)" \
         -H "Content-Type: application/json; charset=utf-8" \
         -d @request.json \
         "https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT/locations/LOCATION/models/MODEL_ID:export"

#### PowerShell

Save the request body in a file named `request.json` , and execute the following command:

    $cred = gcloud auth print-access-token
    $headers = @{ "Authorization" = "Bearer $cred" }
    
    Invoke-WebRequest `
        -Method POST `
        -Headers $headers `
        -ContentType: "application/json; charset=utf-8" `
        -InFile request.json `
        -Uri "https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT/locations/LOCATION/models/MODEL_ID:export" | Select-Object -Expand Content

You should receive a JSON response similar to the following:

    {
      "name": "projects/PROJECT_NUMBER/locations/LOCATION/models/MODEL_ID/operations/OPERATION_ID",
      "metadata": {
        "@type": "type.googleapis.com/google.cloud.aiplatform.v1.ExportModelOperationMetadata",
        "genericMetadata": {
          "createTime": "2020-10-12T20:53:40.130785Z",
          "updateTime": "2020-10-12T20:53:40.130785Z"
        },
        "outputInfo": {
          "artifactOutputUri": "gs://OUTPUT_BUCKET/model-MODEL_ID/EXPORT_FORMAT/YYYY-MM-DDThh:mm:ss.sssZ"
        }
      }
    }

### Java

Before trying this sample, follow the Java setup instructions in the [Agent Platform quickstart using client libraries](https://docs.cloud.google.com/vertex-ai/docs/start/client-libraries) . For more information, see the [Agent Platform Java API reference documentation](https://docs.cloud.google.com/java/docs/reference/google-cloud-aiplatform/latest/com.google.cloud.aiplatform.v1) .

To authenticate to Agent Platform, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

    import com.google.api.gax.longrunning.OperationFuture;
    import com.google.cloud.aiplatform.v1.ExportModelOperationMetadata;
    import com.google.cloud.aiplatform.v1.ExportModelRequest;
    import com.google.cloud.aiplatform.v1.ExportModelResponse;
    import com.google.cloud.aiplatform.v1.GcsDestination;
    import com.google.cloud.aiplatform.v1.ModelName;
    import com.google.cloud.aiplatform.v1.ModelServiceClient;
    import com.google.cloud.aiplatform.v1.ModelServiceSettings;
    import java.io.IOException;
    import java.util.concurrent.ExecutionException;
    import java.util.concurrent.TimeUnit;
    import java.util.concurrent.TimeoutException;
    
    public class ExportModelTabularClassificationSample {
      public static void main(String[] args)
          throws InterruptedException, ExecutionException, TimeoutException, IOException {
        // TODO(developer): Replace these variables before running the sample.
        String gcsDestinationOutputUriPrefix = "gs://your-gcs-bucket/destination_path";
        String project = "YOUR_PROJECT_ID";
        String modelId = "YOUR_MODEL_ID";
        exportModelTableClassification(gcsDestinationOutputUriPrefix, project, modelId);
      }
    
      static void exportModelTableClassification(
          String gcsDestinationOutputUriPrefix, String project, String modelId)
          throws IOException, ExecutionException, InterruptedException, TimeoutException {
        ModelServiceSettings modelServiceSettings =
            ModelServiceSettings.newBuilder()
                .setEndpoint("us-central1-aiplatform.googleapis.com:443")
                .build();
    
        // Initialize client that will be used to send requests. This client only needs to be created
        // once, and can be reused for multiple requests. After completing all of your requests, call
        // the "close" method on the client to safely clean up any remaining background resources.
        try (ModelServiceClient modelServiceClient = ModelServiceClient.create(modelServiceSettings)) {
          String location = "us-central1";
          ModelName modelName = ModelName.of(project, location, modelId);
    
          GcsDestination.Builder gcsDestination = GcsDestination.newBuilder();
          gcsDestination.setOutputUriPrefix(gcsDestinationOutputUriPrefix);
          ExportModelRequest.OutputConfig outputConfig =
              ExportModelRequest.OutputConfig.newBuilder()
                  .setExportFormatId("tf-saved-model")
                  .setArtifactDestination(gcsDestination)
                  .build();
    
          OperationFuture<ExportModelResponse, ExportModelOperationMetadata> exportModelResponseFuture =
              modelServiceClient.exportModelAsync(modelName, outputConfig);
          System.out.format(
              "Operation name: %s\n", exportModelResponseFuture.getInitialFuture().get().getName());
          System.out.println("Waiting for operation to finish...");
          ExportModelResponse exportModelResponse =
              exportModelResponseFuture.get(300, TimeUnit.SECONDS);
          System.out.format(
              "Export Model Tabular Classification Response: %s", exportModelResponse.toString());
        }
      }
    }

### Node.js

Before trying this sample, follow the Node.js setup instructions in the [Agent Platform quickstart using client libraries](https://docs.cloud.google.com/vertex-ai/docs/start/client-libraries) . For more information, see the [Agent Platform Node.js API reference documentation](https://docs.cloud.google.com/nodejs/docs/reference/aiplatform/latest) .

To authenticate to Agent Platform, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

    /**
     * TODO(developer): Uncomment these variables before running the sample.\
     * (Not necessary if passing values as arguments)
     */
    
    // const gcsDestinationOutputUriPrefix ='YOUR_GCS_DESTINATION_\
    // OUTPUT_URI_PREFIX'; eg. "gs://<your-gcs-bucket>/destination_path"
    // const modelId = 'YOUR_MODEL_ID';
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
    
    async function exportModelTabularClassification() {
      // Configure the name resources
      const name = `projects/${project}/locations/${location}/models/${modelId}`;
      // Configure the outputConfig resources
      const outputConfig = {
        exportFormatId: 'tf-saved-model',
        artifactDestination: {
          outputUriPrefix: gcsDestinationOutputUriPrefix,
        },
      };
      const request = {
        name,
        outputConfig,
      };
    
      // Export Model request
      const [response] = await modelServiceClient.exportModel(request);
      console.log(`Long running operation : ${response.name}`);
    
      // Wait for operation to complete
      await response.promise();
      console.log(`Export model response : ${JSON.stringify(response.result)}`);
    }
    exportModelTabularClassification();

### Python

To learn how to install or update the Vertex AI SDK for Python, see [Install the Vertex AI SDK for Python](https://docs.cloud.google.com/vertex-ai/docs/start/use-vertex-ai-python-sdk) . For more information, see the [Python API reference documentation](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest) .

    from google.cloud import aiplatform_v1beta1
    
    
    def export_model_tabular_classification_sample(
        project: str,
        model_id: str,
        gcs_destination_output_uri_prefix: str,
        location: str = "us-central1",
        api_endpoint: str = "us-central1-aiplatform.googleapis.com",
        timeout: int = 300,
    ):
        # The AI Platform services require regional API endpoints.
        client_options = {"api_endpoint": api_endpoint}
        # Initialize client that will be used to create and send requests.
        # This client only needs to be created once, and can be reused for multiple requests.
        client = aiplatform_v1beta1.ModelServiceClient(client_options=client_options)
        gcs_destination = {"output_uri_prefix": gcs_destination_output_uri_prefix}
        output_config = {
            "artifact_destination": gcs_destination,
            "export_format_id": "tf-saved-model",
        }
        name = client.model_path(project=project, location=location, model=model_id)
        response = client.export_model(name=name, output_config=output_config)
        print("Long running operation:", response.operation.name)
        print("output_info:", response.metadata.output_info)
        export_model_response = response.result(timeout=timeout)
        print("export_model_response:", export_model_response)

### Get the status of an export operation

Some requests start long-running operations that require time to complete. These requests return an operation name, which you can use to view the operation's status or cancel the operation. Agent Platform provides helper methods to make calls against long-running operations. For more information, see [Working with long-running operations](https://docs.cloud.google.com/vertex-ai/docs/general/long-running-operations) .

## Pull and run the model server

In this task, you will download your exported model from Cloud Storage and start the Docker container, so your model is ready to receive prediction requests.

To pull and run the model server:

1.  On the machine where you will run the model, change to the directory where you want to save the exported model.

2.  Download the exported model:
    
        gcloud storage cp <var>gcs-destination</var> . --recursive
    
    Where gcs-destination is the path to the location of the exported model in Cloud Storage.
    
    The model is copied to your current directory, under the following path:
    
    `./model-<model-id>/tf-saved-model/<export-timestamp>`
    
    The path may contain either `tf-saved-model` or `custom-trained` .

3.  Rename the directory so the timestamp is removed.
    
        mv model-<model-id>/tf-saved-model/<export-timestamp> model-<model-id>/tf-saved-model/<new-dir-name>
    
    The timestamp makes the directory invalid for Docker.

4.  Pull the model server Docker image.
    
        sudo docker pull MODEL_SERVER_IMAGE
    
    The model server image to pull is located in the `environment.json` file in exported model directory. It should have the following path:
    
    `./model-<model-id>/tf-saved-model/<new-dir-name>/environment.json`

5.  Start the Docker container, using the directory name you just created:
    
        docker run -v `pwd`/model-<model-id>/tf-saved-model/<new-dir-name>:/models/default -p 8080:8080 -it MODEL_SERVER_IMAGE

You can stop the model server at any time by using `Ctrl-C` .

### Update the model server docker container

Because you download the model server Docker container when you export the model, you must explicitly update the model server to get updates and bug fixes. You should update the model server periodically, using the following command:

    docker pull MODEL_SERVER_IMAGE

Make sure the Docker image URI matches the URI of the Docker image that you pulled previously.

## Get predictions from the exported model

The model server in the Agent Platform image container handles prediction requests and returns prediction results.

Batch prediction is not available for exported models.

### Prediction data format

You provide the data ( `payload` field) for your prediction request the following JSON format:

    { "instances": [ { "column_name_1": value, "column_name_2": value, … } , … ] }

> **Note:** Exported Agent Platform models don't validate the data format of prediction requests. This means that an otherwise well-formed prediction request with missing columns, errors in the column names, or even a request for a completely different model returns a (flawed or potentially meaningless) prediction. Make sure your prediction requests to exported models are correct.

The following example shows a request with three columns: a categorical column, a numeric array, and a struct. The request includes two rows.

    {
      "instances": [
        {
          "categorical_col": "mouse",
          "num_array_col": [
            1,
            2,
            3
          ],
          "struct_col": {
            "foo": "piano",
            "bar": "2019-05-17T23:56:09.05Z"
          }
        },
        {
          "categorical_col": "dog",
          "num_array_col": [
            5,
            6,
            7
          ],
          "struct_col": {
            "foo": "guitar",
            "bar": "2019-06-17T23:56:09.05Z"
          }
        }
      ]
    }

### Make the prediction request

1.  Put your request data into a text file, for example, `tmp/request.json` .
    
    The number of rows of data in the prediction request, called the *mini-batch size* , affects the prediction latency and throughput. The larger the mini- batch size, the higher the latency and throughput. For reduced latency, use a smaller mini-batch size. For increased throughput, increase the mini-batch size. The most commonly used mini-batch sizes are 1, 32, 64, 128, 256, 512, and 1024.

2.  Request the prediction:
    
        curl -X POST --data @/tmp/request.json http://localhost:8080/predict

### Prediction results format

The format of your results depends on your model objective.

#### Classification model results

Prediction results for classification models (binary and multi-class) return a probability score for each potential value of the target column. You must determine how you want to use the scores. For example, to get a binary classification from the provided scores, you would identify a threshold value. If there are two classes, "A" and "B", you should classify the example as "A" if the score for "A" is greater than the chosen threshold, and "B" otherwise. For imbalanced datasets, the threshold might approach 100% or 0%.

The results payload for a classification model look similar to this example:

    {
      "predictions": [
        {
          "scores": [
            0.539999994635582,
            0.2599999845027924,
            0.2000000208627896
          ],
          "classes": [
            "apple",
            "orange",
            "grape"
          ]
        },
        {
          "scores": [
            0.23999999463558197,
            0.35999998450279236,
            0.40000002086278963
          ],
          "classes": [
            "apple",
            "orange",
            "grape"
          ]
        }
      ]
    }

#### Regression model results

A predicted value is returned for each valid row of the prediction request. Prediction intervals are not returned for exported models.

The results payload for a regression model look similar to this example:

    {
      "predictions": [
        {
          "value": -304.3663330078125,
          "lower_bound": -56.32196807861328,
          "upper_bound": 126.51904296875
        },
        {
          "value": -112.3663330078125,
          "lower_bound": 16.32196807861328,
          "upper_bound": 255.51904296875
        }
      ]
    }

## What's next

  - Learn how to [import your exported tabular model back into Agent Platform](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/model-registry/import-model) .
