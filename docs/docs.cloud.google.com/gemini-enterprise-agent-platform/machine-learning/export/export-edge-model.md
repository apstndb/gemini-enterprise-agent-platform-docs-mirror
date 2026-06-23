---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/export/export-edge-model
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/export/export-edge-model
title: Export AutoML Edge models
description: Use Gemini Enterprise Agent Platform to export your image and video AutoML Edge models to Cloud Storage.
data_source: docs.cloud.google.com
---

This page describes how to use Gemini Enterprise Agent Platform to export your image AutoML Edge models to Cloud Storage.

For information about exporting tabular models, see [Exporting an AutoML tabular model](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/export/export-model-tabular) .

## Introduction

After you have [trained](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/automl-edge-console) an AutoML Edge model you can, in some cases, export the model in different formats, depending on how you want to use it. The exported model files are saved in a Cloud Storage bucket, and can they be used for prediction in the environment of your choosing.

You cannot use an Edge model in Agent Platform to serve predictions; you must deploy Edge model to an external device to get predictions.

## Export a model

Use the following code samples to identify an AutoML Edge model, specify an output file storage location, and then send the export model request.

> **Note:** The `tflite-runtime` PyPI package is no longer maintained for Windows and macOS. For these platforms, you can use the [full TensorFlow package](https://www.tensorflow.org/install/) , or [build the `tflite-runtime` package from source](https://developers.google.com/edge/litert/build/cmake_pip) .

### Image

Select the tab below for your objective:

### Classification

Trained AutoML Edge image classification models can be exported in the following formats:

  - **TF Lite** - Export your model as a TF Lite package to run your model on edge or mobile devices.
  - **Edge TPU TF Lite** - Export your model as a TF Lite package to run your model on Edge TPU devices.
  - **Container** - Export your model as a TF Saved Model to run on a Docker container.
  - **Core ML** - Export an .mlmodel file to run your model on iOS and macOS devices.
  - **Tensorflow.js** - Export your model as a TensorFlow.js package to run your model in the browser and in Node.js.

Select the tab below for your language or environment:

### Console

1.  In the Google Cloud console, in the Agent Platform section, go to the **Models** page.
2.  Click the version number of the AutoML Edge model you want to export to open its details page.
3.  Click **Export** .
4.  In the **Export model** side window, specify the location in Cloud Storage to store Edge model export output.
5.  Click **Export** .
6.  Click **Done** to close the **Export model** side window.

### REST

Before using any of the request data, make the following replacements:

  - LOCATION : Your project's location.
  - PROJECT : Your [project ID](https://docs.cloud.google.com/resource-manager/docs/creating-managing-projects#identifiers) .
  - MODEL\_ID : The ID number of the trained AutoML Edge model you are exporting.
  - EXPORT\_FORMAT : The type of Edge model you are exporting. For this objective the options are:
      - `tflite` (TF Lite) - Export your model as a TF Lite package to run your model on edge or mobile devices.
      - `tf-saved-model` (Container) - Export your model as a TF Saved Model to run on a Docker container.
      - `tf-js` (Tensorflow.js) - Export your model as a TensorFlow.js package to run your model in the browser and in Node.js.
  - OUTPUT\_BUCKET : The path to the Cloud Storage bucket directory where you want to store your Edge model files.

### Java

Before trying this sample, follow the Java setup instructions in the [Agent Platform quickstart using client libraries](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/start/client-libraries) . For more information, see the [Agent Platform Java API reference documentation](https://docs.cloud.google.com/java/docs/reference/google-cloud-aiplatform/latest/com.google.cloud.aiplatform.v1) .

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
    
    public class ExportModelSample {
    
      public static void main(String[] args)
          throws IOException, InterruptedException, ExecutionException, TimeoutException {
        // TODO(developer): Replace these variables before running the sample.
        String project = "YOUR_PROJECT_ID";
        String modelId = "YOUR_MODEL_ID";
        String gcsDestinationOutputUriPrefix = "gs://YOUR_GCS_SOURCE_BUCKET/path_to_your_destination/";
        String exportFormat = "YOUR_EXPORT_FORMAT";
        exportModelSample(project, modelId, gcsDestinationOutputUriPrefix, exportFormat);
      }
    
      static void exportModelSample(
          String project, String modelId, String gcsDestinationOutputUriPrefix, String exportFormat)
          throws IOException, InterruptedException, ExecutionException, TimeoutException {
        ModelServiceSettings modelServiceSettings =
            ModelServiceSettings.newBuilder()
                .setEndpoint("us-central1-aiplatform.googleapis.com:443")
                .build();
    
        // Initialize client that will be used to send requests. This client only needs to be created
        // once, and can be reused for multiple requests. After completing all of your requests, call
        // the "close" method on the client to safely clean up any remaining background resources.
        try (ModelServiceClient modelServiceClient = ModelServiceClient.create(modelServiceSettings)) {
          String location = "us-central1";
          GcsDestination.Builder gcsDestination = GcsDestination.newBuilder();
          gcsDestination.setOutputUriPrefix(gcsDestinationOutputUriPrefix);
    
          ModelName modelName = ModelName.of(project, location, modelId);
          ExportModelRequest.OutputConfig outputConfig =
              ExportModelRequest.OutputConfig.newBuilder()
                  .setExportFormatId(exportFormat)
                  .setArtifactDestination(gcsDestination)
                  .build();
    
          OperationFuture<ExportModelResponse, ExportModelOperationMetadata> exportModelResponseFuture =
              modelServiceClient.exportModelAsync(modelName, outputConfig);
          System.out.format(
              "Operation name: %s\n", exportModelResponseFuture.getInitialFuture().get().getName());
          System.out.println("Waiting for operation to finish...");
          ExportModelResponse exportModelResponse =
              exportModelResponseFuture.get(300, TimeUnit.SECONDS);
    
          System.out.format("Export Model Response: %s\n", exportModelResponse);
        }
      }
    }

### Node.js

Before trying this sample, follow the Node.js setup instructions in the [Agent Platform quickstart using client libraries](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/start/client-libraries) . For more information, see the [Agent Platform Node.js API reference documentation](https://docs.cloud.google.com/nodejs/docs/reference/aiplatform/latest) .

To authenticate to Agent Platform, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

    /**
     * TODO(developer): Uncomment these variables before running the sample.\
       (Not necessary if passing values as arguments)
     */
    
    // const modelId = 'YOUR_MODEL_ID';
    // const gcsDestinationOutputUriPrefix ='YOUR_GCS_DEST_OUTPUT_URI_PREFIX';
    //    eg. "gs://<your-gcs-bucket>/destination_path"
    // const exportFormat = 'YOUR_EXPORT_FORMAT';
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
    
    async function exportModel() {
      // Configure the name resources
      const name = `projects/${project}/locations/${location}/models/${modelId}`;
      // Configure the outputConfig resources
      const outputConfig = {
        exportFormatId: exportFormat,
        gcsDestination: {
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
      const result = response.result;
    
      console.log(`Export model response : ${JSON.stringify(result)}`);
    }
    exportModel();

### Python

To learn how to install or update the Vertex AI SDK for Python, see [Install the Vertex AI SDK for Python](https://docs.cloud.google.com/vertex-ai/docs/start/use-vertex-ai-python-sdk) . For more information, see the [Python API reference documentation](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest) .

    from google.cloud import aiplatform
    
    
    def export_model_sample(
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
        client = aiplatform.gapic.ModelServiceClient(client_options=client_options)
        output_config = {
            "artifact_destination": {
                "output_uri_prefix": gcs_destination_output_uri_prefix
            },
            # For information about export formats: https://cloud.google.com/ai-platform-unified/docs/export/export-edge-model#aiplatform_export_model_sample-drest
            "export_format_id": "tf-saved-model",
        }
        name = client.model_path(project=project, location=location, model=model_id)
        response = client.export_model(name=name, output_config=output_config)
        print("Long running operation:", response.operation.name)
        print("output_info:", response.metadata.output_info)
        export_model_response = response.result(timeout=timeout)
        print("export_model_response:", export_model_response)

### Classification

Trained AutoML Edge image classification models can be exported in the following formats:

  - **TF Lite** - Export your model as a TF Lite package to run your model on edge or mobile devices.
  - **Edge TPU TF Lite** - Export your model as a TF Lite package to run your model on Edge TPU devices.
  - **Container** - Export your model as a TF Saved Model to run on a Docker container.
  - **Core ML** - Export an .mlmodel file to run your model on iOS and macOS devices.
  - **Tensorflow.js** - Export your model as a TensorFlow.js package to run your model in the browser and in Node.js.

Select the tab below for your language or environment:

### Console

1.  In the Google Cloud console, in the Agent Platform section, go to the **Models** page.
2.  Click the version number of the AutoML Edge model you want to export to open its details page.
3.  Click **Export** .
4.  In the **Export model** side window, specify the location in Cloud Storage to store Edge model export output.
5.  Click **Export** .
6.  Click **Done** to close the **Export model** side window.

### REST

Before using any of the request data, make the following replacements:

  - LOCATION : Your project's location.
  - PROJECT : Your [project ID](https://docs.cloud.google.com/resource-manager/docs/creating-managing-projects#identifiers) .
  - MODEL\_ID : The ID number of the trained AutoML Edge model you are exporting.
  - EXPORT\_FORMAT : The type of Edge model you are exporting. For this objective the options are:
      - `tflite` (TF Lite) - Export your model as a TF Lite package to run your model on edge or mobile devices.
      - `tf-saved-model` (Container) - Export your model as a TF Saved Model to run on a Docker container.
      - `tf-js` (Tensorflow.js) - Export your model as a TensorFlow.js package to run your model in the browser and in Node.js.
  - OUTPUT\_BUCKET : The path to the Cloud Storage bucket directory where you want to store your Edge model files.

### Java

Before trying this sample, follow the Java setup instructions in the [Agent Platform quickstart using client libraries](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/start/client-libraries) . For more information, see the [Agent Platform Java API reference documentation](https://docs.cloud.google.com/java/docs/reference/google-cloud-aiplatform/latest/com.google.cloud.aiplatform.v1) .

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
    
    public class ExportModelSample {
    
      public static void main(String[] args)
          throws IOException, InterruptedException, ExecutionException, TimeoutException {
        // TODO(developer): Replace these variables before running the sample.
        String project = "YOUR_PROJECT_ID";
        String modelId = "YOUR_MODEL_ID";
        String gcsDestinationOutputUriPrefix = "gs://YOUR_GCS_SOURCE_BUCKET/path_to_your_destination/";
        String exportFormat = "YOUR_EXPORT_FORMAT";
        exportModelSample(project, modelId, gcsDestinationOutputUriPrefix, exportFormat);
      }
    
      static void exportModelSample(
          String project, String modelId, String gcsDestinationOutputUriPrefix, String exportFormat)
          throws IOException, InterruptedException, ExecutionException, TimeoutException {
        ModelServiceSettings modelServiceSettings =
            ModelServiceSettings.newBuilder()
                .setEndpoint("us-central1-aiplatform.googleapis.com:443")
                .build();
    
        // Initialize client that will be used to send requests. This client only needs to be created
        // once, and can be reused for multiple requests. After completing all of your requests, call
        // the "close" method on the client to safely clean up any remaining background resources.
        try (ModelServiceClient modelServiceClient = ModelServiceClient.create(modelServiceSettings)) {
          String location = "us-central1";
          GcsDestination.Builder gcsDestination = GcsDestination.newBuilder();
          gcsDestination.setOutputUriPrefix(gcsDestinationOutputUriPrefix);
    
          ModelName modelName = ModelName.of(project, location, modelId);
          ExportModelRequest.OutputConfig outputConfig =
              ExportModelRequest.OutputConfig.newBuilder()
                  .setExportFormatId(exportFormat)
                  .setArtifactDestination(gcsDestination)
                  .build();
    
          OperationFuture<ExportModelResponse, ExportModelOperationMetadata> exportModelResponseFuture =
              modelServiceClient.exportModelAsync(modelName, outputConfig);
          System.out.format(
              "Operation name: %s\n", exportModelResponseFuture.getInitialFuture().get().getName());
          System.out.println("Waiting for operation to finish...");
          ExportModelResponse exportModelResponse =
              exportModelResponseFuture.get(300, TimeUnit.SECONDS);
    
          System.out.format("Export Model Response: %s\n", exportModelResponse);
        }
      }
    }

### Node.js

Before trying this sample, follow the Node.js setup instructions in the [Agent Platform quickstart using client libraries](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/start/client-libraries) . For more information, see the [Agent Platform Node.js API reference documentation](https://docs.cloud.google.com/nodejs/docs/reference/aiplatform/latest) .

To authenticate to Agent Platform, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

    /**
     * TODO(developer): Uncomment these variables before running the sample.\
       (Not necessary if passing values as arguments)
     */
    
    // const modelId = 'YOUR_MODEL_ID';
    // const gcsDestinationOutputUriPrefix ='YOUR_GCS_DEST_OUTPUT_URI_PREFIX';
    //    eg. "gs://<your-gcs-bucket>/destination_path"
    // const exportFormat = 'YOUR_EXPORT_FORMAT';
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
    
    async function exportModel() {
      // Configure the name resources
      const name = `projects/${project}/locations/${location}/models/${modelId}`;
      // Configure the outputConfig resources
      const outputConfig = {
        exportFormatId: exportFormat,
        gcsDestination: {
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
      const result = response.result;
    
      console.log(`Export model response : ${JSON.stringify(result)}`);
    }
    exportModel();

### Python

To learn how to install or update the Vertex AI SDK for Python, see [Install the Vertex AI SDK for Python](https://docs.cloud.google.com/vertex-ai/docs/start/use-vertex-ai-python-sdk) . For more information, see the [Python API reference documentation](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest) .

    from google.cloud import aiplatform
    
    
    def export_model_sample(
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
        client = aiplatform.gapic.ModelServiceClient(client_options=client_options)
        output_config = {
            "artifact_destination": {
                "output_uri_prefix": gcs_destination_output_uri_prefix
            },
            # For information about export formats: https://cloud.google.com/ai-platform-unified/docs/export/export-edge-model#aiplatform_export_model_sample-drest
            "export_format_id": "tf-saved-model",
        }
        name = client.model_path(project=project, location=location, model=model_id)
        response = client.export_model(name=name, output_config=output_config)
        print("Long running operation:", response.operation.name)
        print("output_info:", response.metadata.output_info)
        export_model_response = response.result(timeout=timeout)
        print("export_model_response:", export_model_response)

### Object detection

> **Note:** AutoML Edge object detection is in maintenance mode. Only severe failures will be addressed. We recommend migrating to alternative solutions such as open source (OSS) models.

Trained AutoML Edge image object detection models can be exported in the following formats:

  - **TF Lite** - Export your model as a TF Lite package to run your model on edge or mobile devices.
  - **Container** - Export your model as a TF Saved Model to run on a Docker container.
  - **Tensorflow.js** - Export your model as a TensorFlow.js package to run your model in the browser and in Node.js.

Select the tab below for your language or environment:

### Console

1.  In the Google Cloud console, in the Agent Platform section, go to the **Models** page.
2.  Click the version number of the AutoML Edge model you want to export to open its details page.
3.  Select the **Deploy & Test** tab to view the available export formats.
4.  Select your desired export model format from the **Use your edge-optimized model** section.
5.  In the **Export model** side window, specify the location in Cloud Storage to store Edge model export output.
6.  Click **Export** .
7.  Click **Done** to close the **Export model** side window.

### REST

Before using any of the request data, make the following replacements:

  - LOCATION : Your project's location.
  - PROJECT : .
  - MODEL\_ID : The ID number of the trained AutoML Edge model you are exporting.
  - EXPORT\_FORMAT : The type of Edge model you are exporting. For this objective the options are:
      - `tflite` (TF Lite) - Export your model as a TF Lite package to run your model on edge or mobile devices.
      - `tf-saved-model` (Container) - Export your model as a TF Saved Model to run on a Docker container.
      - `tf-js` (Tensorflow.js) - Export your model as a TensorFlow.js package to run your model in the browser and in Node.js.
  - OUTPUT\_BUCKET : The path to the Cloud Storage bucket directory where you want to store your Edge model files.

### Java

Before trying this sample, follow the Java setup instructions in the [Agent Platform quickstart using client libraries](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/start/client-libraries) . For more information, see the [Agent Platform Java API reference documentation](https://docs.cloud.google.com/java/docs/reference/google-cloud-aiplatform/latest/com.google.cloud.aiplatform.v1) .

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
    
    public class ExportModelSample {
    
      public static void main(String[] args)
          throws IOException, InterruptedException, ExecutionException, TimeoutException {
        // TODO(developer): Replace these variables before running the sample.
        String project = "YOUR_PROJECT_ID";
        String modelId = "YOUR_MODEL_ID";
        String gcsDestinationOutputUriPrefix = "gs://YOUR_GCS_SOURCE_BUCKET/path_to_your_destination/";
        String exportFormat = "YOUR_EXPORT_FORMAT";
        exportModelSample(project, modelId, gcsDestinationOutputUriPrefix, exportFormat);
      }
    
      static void exportModelSample(
          String project, String modelId, String gcsDestinationOutputUriPrefix, String exportFormat)
          throws IOException, InterruptedException, ExecutionException, TimeoutException {
        ModelServiceSettings modelServiceSettings =
            ModelServiceSettings.newBuilder()
                .setEndpoint("us-central1-aiplatform.googleapis.com:443")
                .build();
    
        // Initialize client that will be used to send requests. This client only needs to be created
        // once, and can be reused for multiple requests. After completing all of your requests, call
        // the "close" method on the client to safely clean up any remaining background resources.
        try (ModelServiceClient modelServiceClient = ModelServiceClient.create(modelServiceSettings)) {
          String location = "us-central1";
          GcsDestination.Builder gcsDestination = GcsDestination.newBuilder();
          gcsDestination.setOutputUriPrefix(gcsDestinationOutputUriPrefix);
    
          ModelName modelName = ModelName.of(project, location, modelId);
          ExportModelRequest.OutputConfig outputConfig =
              ExportModelRequest.OutputConfig.newBuilder()
                  .setExportFormatId(exportFormat)
                  .setArtifactDestination(gcsDestination)
                  .build();
    
          OperationFuture<ExportModelResponse, ExportModelOperationMetadata> exportModelResponseFuture =
              modelServiceClient.exportModelAsync(modelName, outputConfig);
          System.out.format(
              "Operation name: %s\n", exportModelResponseFuture.getInitialFuture().get().getName());
          System.out.println("Waiting for operation to finish...");
          ExportModelResponse exportModelResponse =
              exportModelResponseFuture.get(300, TimeUnit.SECONDS);
    
          System.out.format("Export Model Response: %s\n", exportModelResponse);
        }
      }
    }

### Node.js

Before trying this sample, follow the Node.js setup instructions in the [Agent Platform quickstart using client libraries](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/start/client-libraries) . For more information, see the [Agent Platform Node.js API reference documentation](https://docs.cloud.google.com/nodejs/docs/reference/aiplatform/latest) .

To authenticate to Agent Platform, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

    /**
     * TODO(developer): Uncomment these variables before running the sample.\
       (Not necessary if passing values as arguments)
     */
    
    // const modelId = 'YOUR_MODEL_ID';
    // const gcsDestinationOutputUriPrefix ='YOUR_GCS_DEST_OUTPUT_URI_PREFIX';
    //    eg. "gs://<your-gcs-bucket>/destination_path"
    // const exportFormat = 'YOUR_EXPORT_FORMAT';
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
    
    async function exportModel() {
      // Configure the name resources
      const name = `projects/${project}/locations/${location}/models/${modelId}`;
      // Configure the outputConfig resources
      const outputConfig = {
        exportFormatId: exportFormat,
        gcsDestination: {
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
      const result = response.result;
    
      console.log(`Export model response : ${JSON.stringify(result)}`);
    }
    exportModel();

### Python

To learn how to install or update the Vertex AI SDK for Python, see [Install the Vertex AI SDK for Python](https://docs.cloud.google.com/vertex-ai/docs/start/use-vertex-ai-python-sdk) . For more information, see the [Python API reference documentation](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest) .

    from google.cloud import aiplatform
    
    
    def export_model_sample(
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
        client = aiplatform.gapic.ModelServiceClient(client_options=client_options)
        output_config = {
            "artifact_destination": {
                "output_uri_prefix": gcs_destination_output_uri_prefix
            },
            # For information about export formats: https://cloud.google.com/ai-platform-unified/docs/export/export-edge-model#aiplatform_export_model_sample-drest
            "export_format_id": "tf-saved-model",
        }
        name = client.model_path(project=project, location=location, model=model_id)
        response = client.export_model(name=name, output_config=output_config)
        print("Long running operation:", response.operation.name)
        print("output_info:", response.metadata.output_info)
        export_model_response = response.result(timeout=timeout)
        print("export_model_response:", export_model_response)

## Get status of the operation

### Image

Use the following code to get the status of the export operation. This code is the same for all objectives:

### REST

Before using any of the request data, make the following replacements:

  - LOCATION : Your project's location.
  - PROJECT : .
  - OPERATION\_ID :The ID of the target operation. This ID is typically contained in the response to the original request.

HTTP method and URL:

    GET https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT/locations/LOCATION/operations/OPERATION_ID

To send your request, choose one of these options:

#### curl

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) , or by using [Cloud Shell](https://docs.cloud.google.com/shell/docs) , which automatically logs you into the `gcloud` CLI . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Execute the following command:

    curl -X GET \
         -H "Authorization: Bearer $(gcloud auth print-access-token)" \
         "https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT/locations/LOCATION/operations/OPERATION_ID"

#### PowerShell

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Execute the following command:

    $cred = gcloud auth print-access-token
    $headers = @{ "Authorization" = "Bearer $cred" }
    
    Invoke-WebRequest `
        -Method GET `
        -Headers $headers `
        -Uri "https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT/locations/LOCATION/operations/OPERATION_ID" | Select-Object -Expand Content

You should see output similar to the following for a completed operation:

    {
      "name": "projects/PROJECT/locations/LOCATION/models/MODEL_ID/operations/OPERATION_ID",
      "metadata": {
        "@type": "type.googleapis.com/google.cloud.aiplatform.v1.ExportModelOperationMetadata",
        "genericMetadata": {
          "createTime": "2020-10-12T20:53:40.130785Z",
          "updateTime": "2020-10-12T20:53:40.793983Z"
        },
        "outputInfo": {
          "artifactOutputUri": "gs://OUTPUT_BUCKET/model-MODEL_ID/EXPORT_FORMAT/YYYY-MM-DDThh:mm:ss.sssZ"
        }
      },
      "done": true,
      "response": {
        "@type": "type.googleapis.com/google.cloud.aiplatform.v1.ExportModelResponse"
      }
    }

## Output files

### Image

Select the tab below for your model format:

### TF Lite

The `OUTPUT_BUCKET` you specified in the request determines where the output files are stored. The directory format where the output files are stored follows the format:

  - gs:// OUTPUT\_BUCKET /model- MODEL\_ID / **tflite** / YYYY-MM-DDThh:mm:ss.sssZ /

**Files:**

1.  `model.tflite` : A file containing a version of the model that is ready to be used with TensorFlow Lite.

> **Key point** : Unlike previous export behavior in AutoML Vision, exporting this format in Gemini Enterprise Agent Platform does not produce a label file ( `dict.txt` ) as one of the output files. This information is now included in the `.tflite` file itself. For information about extracting this information, see the following TensorFlow documentation:
> 
>   - [TensorFlow Lite inference with metadata](https://ai.google.dev/edge/litert/inference_with_metadata/overview)
>   - [Generate model interfaces with TensorFlow Lite code generator](https://ai.google.dev/edge/litert/inference_with_metadata/codegen)
>   - [Adding metadata to TensorFlow Lite models](https://ai.google.dev/edge/litert/models/metadata)

### Edge TPU

The `OUTPUT_BUCKET` you specified in the request determines where the output files are stored. The directory format where the output files are stored follows the format:

  - gs:// OUTPUT\_BUCKET /model- MODEL\_ID / **edgetpu-tflite** / YYYY-MM-DDThh:mm:ss.sssZ /

**Files:**

1.  `edgetpu_model.tflite` : A file containing a version of the model for TensorFlow Lite, passed through the Edge TPU compiler to be compatible with the Edge TPU.

> **Key point** : Unlike previous export behavior in AutoML Vision, exporting this format in Gemini Enterprise Agent Platform does not produce a label file ( `dict.txt` ) as one of the output files. This information is now included in the `.tflite` file itself. For information about extracting this information, see the following TensorFlow documentation:
> 
>   - [TensorFlow Lite inference with metadata](https://ai.google.dev/edge/litert/inference_with_metadata/overview)
>   - [Generate model interfaces with TensorFlow Lite code generator](https://ai.google.dev/edge/litert/inference_with_metadata/codegen)
>   - [Adding metadata to TensorFlow Lite models](https://ai.google.dev/edge/litert/models/metadata)

### Container

The `OUTPUT_BUCKET` you specified in the request determines where the output files are stored. The directory format where the output files are stored follows the format:

  - gs:// OUTPUT\_BUCKET /model- MODEL\_ID / **tf-saved-model** / YYYY-MM-DDThh:mm:ss.sssZ /

**Files:**

1.  `saved_model.pb` : A protocol buffer file containing the graph definition and the weights of the model.

### Core ML

The `OUTPUT_BUCKET` you specified in the request determines where the output files are stored. The directory format where the output files are stored follows the format:

  - gs:// OUTPUT\_BUCKET /model- MODEL\_ID / **core-ml** / YYYY-MM-DDThh:mm:ss.sssZ /

**Files:**

1.  `dict.txt` : A label file. Each line in the label file `dict.txt` represents a label of the predictions returned by the model, in the same order they were requested.
    
    **Sample `dict.txt`**
    
        roses
        daisy
        tulips
        dandelion
        sunflowers

2.  `model.mlmodel` : A file specifying a Core ML model.

### Tensorflow.js

The `OUTPUT_BUCKET` you specified in the request determines where the output files are stored. The directory format where the output files are stored follows the format:

  - gs:// OUTPUT\_BUCKET /model- MODEL\_ID / **tf-js** / YYYY-MM-DDThh:mm:ss.sssZ /

**Files:**

1.  `dict.txt` : A label file. Each line in the label file `dict.txt` represents a label of the predictions returned by the model, in the same order they were requested.
    
    **Sample `dict.txt`**
    
        roses
        daisy
        tulips
        dandelion
        sunflowers

2.  `group1-shard1of3.bin` : A binary file.

3.  `group1-shard2of3.bin` : A binary file.

4.  `group1-shard3of3.bin` : A binary file.

5.  `model.json` : A JSON file representation of a model.
    
    **Sample** `model.json` (shortened for clarity)
    
        {
          "format": "graph-model",
          "generatedBy": "2.4.0",
          "convertedBy": "TensorFlow.js Converter v1.7.0",
          "userDefinedMetadata": {
            "signature": {
              "inputs": {
                "image:0": {
                  "name": "image:0",
                  "dtype": "DT_FLOAT",
                  "tensorShape": {
                    "dim": [
                      {
                        "size": "1"
                      },
                      {
                        "size": "224"
                      },
                      {
                        "size": "224"
                      },
                      {
                        "size": "3"
                      }
                    ]
                  }
                }
              },
              "outputs": {
                "scores:0": {
                  "name": "scores:0",
                  "dtype": "DT_FLOAT",
                  "tensorShape": {
                    "dim": [
                      {
                        "size": "1"
                      },
                      {
                        "size": "5"
                      }
                    ]
                  }
                }
              }
            }
          },
          "modelTopology": {
            "node": [
              {
                "name": "image",
                "op": "Placeholder",
                "attr": {
                  "dtype": {
                    "type": "DT_FLOAT"
                  },
                  "shape": {
                    "shape": {
                      "dim": [
                        {
                          "size": "1"
                        },
                        {
                          "size": "224"
                        },
                        {
                          "size": "224"
                        },
                        {
                          "size": "3"
                        }
                      ]
                    }
                  }
                }
              },
              {
                "name": "mnas_v4_a_1/feature_network/feature_extractor/Mean/reduction_indices",
                "op": "Const",
                "attr": {
                  "value": {
                    "tensor": {
                      "dtype": "DT_INT32",
                      "tensorShape": {
                        "dim": [
                          {
                            "size": "2"
                          }
                        ]
                      }
                    }
                  },
                  "dtype": {
                    "type": "DT_INT32"
                  }
                }
              },
              ...
              {
                "name": "scores",
                "op": "Identity",
                "input": [
                  "Softmax"
                ],
                "attr": {
                  "T": {
                    "type": "DT_FLOAT"
                  }
                }
              }
            ],
            "library": {},
            "versions": {}
          },
          "weightsManifest": [
            {
              "paths": [
                "group1-shard1of3.bin",
                "group1-shard2of3.bin",
                "group1-shard3of3.bin"
              ],
              "weights": [
                {
                  "name": "mnas_v4_a_1/feature_network/feature_extractor/Mean/reduction_indices",
                  "shape": [
                    2
                  ],
                  "dtype": "int32"
                },
                {
                  "name": "mnas_v4_a/output/fc/tf_layer/kernel",
                  "shape": [
                    1280,
                    5
                  ],
                  "dtype": "float32"
                },
                ...
                {
                  "name": "mnas_v4_a_1/feature_network/lead_cell_17/op_0/conv2d_0/Conv2D_weights",
                  "shape": [
                    1,
                    1,
                    320,
                    1280
                  ],
                  "dtype": "float32"
                },
                {
                  "name": "mnas_v4_a_1/feature_network/cell_14/op_0/expand_0/Conv2D_bn_offset",
                  "shape": [
                    1152
                  ],
                  "dtype": "float32"
                }
              ]
            }
          ]
        }
