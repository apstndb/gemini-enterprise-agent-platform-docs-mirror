---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/image-data/classification/create-dataset
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/image-data/classification/create-dataset
title: Create a dataset for training image classification models
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

[Video](https://www.youtube.com/watch?v=CN2X6oIlnmI)

This page shows you how to create an Agent Platform dataset from your image data so you can start training classification models. You can create a dataset using either the Google Cloud console or the Agent Platform API.

## Create an empty dataset and import or associate your data

### Google Cloud console

Use the following instructions to create an empty dataset and either import or associate your data.

1.  In the Google Cloud console, in the Agent Platform section, go to the **Datasets** page.

2.  Click **Create** to open the create dataset details page.

3.  Modify the **Dataset name** field to create a descriptive dataset display name.

4.  Select the **Image** tab.  

5.  Select single-label or multi-label image classification as your objective.

6.  Select a region from the **Region** drop-down list.

7.  Click **Create** to create your empty dataset, and advance to the data import page.

8.  Choose one of the following options from the **Select an import method** section:
    
    ### Upload data from your computer
    
    1.  In the **Select an import method** section, choose to upload data from your computer.
    2.  Click **Select files** and choose all the local files to upload to a Cloud Storage bucket.
    3.  In the **Select a Cloud Storage path** section click **Browse** to choose a Cloud Storage bucket location to upload your data to.
    
    ### Upload an import file from your computer
    
    1.  Click radio\_button\_checked **Upload an import file from your computer** .
    2.  Click **Select files** and choose the local import file to upload to a Cloud Storage bucket.
    3.  In the **Select a Cloud Storage path** section click **Browse** to choose a Cloud Storage bucket location to upload your file to.
    
    ### Select an import file from Cloud Storage
    
    1.  Click radio\_button\_checked **Select an import file from Cloud Storage** .
    2.  In the **Select a Cloud Storage path** section click **Browse** to choose the import file in Cloud Storage.

9.  Click **Continue** .
    
    Data import can take several hours, depending on the size of your data. You can close this tab and return to it later. You will receive an email when your data is imported.

### API

In order to create a machine learning model you must first have a representative collection of data to train with. After importing data you can make modifications and start model training.

## Create a dataset

Use the following samples to create a dataset for your data.

### REST

Before using any of the request data, make the following replacements:

  - LOCATION : Region where the dataset will be stored. This must be a region that supports dataset resources. For example, `us-central1` . See [List of available locations](https://docs.cloud.google.com/vertex-ai/machine-learning/general/locations) .
  - PROJECT : Your \[project ID\](/resource-manager/docs/creating-managing-projects\#identifiers). .
  - DATASET\_NAME : Name for the dataset.

HTTP method and URL:

    POST https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/datasets

Request JSON body:

    {
      "display_name": "DATASET_NAME",
      "metadata_schema_uri": "gs://google-cloud-aiplatform/schema/dataset/metadata/image_1.0.0.yaml"
    }

To send your request, choose one of these options:

#### curl

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) , or by using [Cloud Shell](https://docs.cloud.google.com/shell/docs) , which automatically logs you into the `gcloud` CLI . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Save the request body in a file named `request.json` , and execute the following command:

    curl -X POST \
         -H "Authorization: Bearer $(gcloud auth print-access-token)" \
         -H "Content-Type: application/json; charset=utf-8" \
         -d @request.json \
         "https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/datasets"

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
        -Uri "https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/datasets" | Select-Object -Expand Content

You should see output similar to the following. You can use the OPERATION\_ID in the response to [get the status](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/image-data/classification/create-dataset#get-operation) of the operation.

    {
      "name": "projects/PROJECT_NUMBER/locations/LOCATION/datasets/DATASET_ID/operations/OPERATION_ID",
      "metadata": {
        "@type": "type.googleapis.com/google.cloud.aiplatform.v1.CreateDatasetOperationMetadata",
        "genericMetadata": {
          "createTime": "2020-07-07T21:27:35.964882Z",
          "updateTime": "2020-07-07T21:27:35.964882Z"
        }
      }
    }

### Terraform

The following sample uses the [`google_vertex_ai_dataset`](https://registry.terraform.io/providers/hashicorp/google/latest/docs/resources/vertex_ai_dataset) Terraform resource to create an image dataset named `image-dataset` .

To learn how to apply or remove a Terraform configuration, see [Basic Terraform commands](https://docs.cloud.google.com/docs/terraform/basic-commands) .

    resource "google_vertex_ai_dataset" "image_dataset" {
      display_name        = "image-dataset"
      metadata_schema_uri = "gs://google-cloud-aiplatform/schema/dataset/metadata/image_1.0.0.yaml"
      region              = "us-central1"
    }

### Java

Before trying this sample, follow the Java setup instructions in the [Agent Platform quickstart using client libraries](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/start/client-libraries) .

To authenticate to Agent Platform, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

    import com.google.api.gax.longrunning.OperationFuture;
    import com.google.cloud.aiplatform.v1.CreateDatasetOperationMetadata;
    import com.google.cloud.aiplatform.v1.Dataset;
    import com.google.cloud.aiplatform.v1.DatasetServiceClient;
    import com.google.cloud.aiplatform.v1.DatasetServiceSettings;
    import com.google.cloud.aiplatform.v1.LocationName;
    import java.io.IOException;
    import java.util.concurrent.ExecutionException;
    import java.util.concurrent.TimeUnit;
    import java.util.concurrent.TimeoutException;
    
    public class CreateDatasetImageSample {
    
      public static void main(String[] args)
          throws IOException, InterruptedException, ExecutionException, TimeoutException {
        // TODO(developer): Replace these variables before running the sample.
        String project = "YOUR_PROJECT_ID";
        String datasetDisplayName = "YOUR_DATASET_DISPLAY_NAME";
        createDatasetImageSample(project, datasetDisplayName);
      }
    
      static void createDatasetImageSample(String project, String datasetDisplayName)
          throws IOException, InterruptedException, ExecutionException, TimeoutException {
        DatasetServiceSettings datasetServiceSettings =
            DatasetServiceSettings.newBuilder()
                .setEndpoint("us-central1-aiplatform.googleapis.com:443")
                .build();
    
        // Initialize client that will be used to send requests. This client only needs to be created
        // once, and can be reused for multiple requests. After completing all of your requests, call
        // the "close" method on the client to safely clean up any remaining background resources.
        try (DatasetServiceClient datasetServiceClient =
            DatasetServiceClient.create(datasetServiceSettings)) {
          String location = "us-central1";
          String metadataSchemaUri =
              "gs://google-cloud-aiplatform/schema/dataset/metadata/image_1.0.0.yaml";
          LocationName locationName = LocationName.of(project, location);
          Dataset dataset =
              Dataset.newBuilder()
                  .setDisplayName(datasetDisplayName)
                  .setMetadataSchemaUri(metadataSchemaUri)
                  .build();
    
          OperationFuture<Dataset, CreateDatasetOperationMetadata> datasetFuture =
              datasetServiceClient.createDatasetAsync(locationName, dataset);
          System.out.format("Operation name: %s\n", datasetFuture.getInitialFuture().get().getName());
          System.out.println("Waiting for operation to finish...");
          Dataset datasetResponse = datasetFuture.get(120, TimeUnit.SECONDS);
    
          System.out.println("Create Image Dataset Response");
          System.out.format("Name: %s\n", datasetResponse.getName());
          System.out.format("Display Name: %s\n", datasetResponse.getDisplayName());
          System.out.format("Metadata Schema Uri: %s\n", datasetResponse.getMetadataSchemaUri());
          System.out.format("Metadata: %s\n", datasetResponse.getMetadata());
          System.out.format("Create Time: %s\n", datasetResponse.getCreateTime());
          System.out.format("Update Time: %s\n", datasetResponse.getUpdateTime());
          System.out.format("Labels: %s\n", datasetResponse.getLabelsMap());
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
    
    // const datasetDisplayName = "YOUR_DATASTE_DISPLAY_NAME";
    // const project = 'YOUR_PROJECT_ID';
    // const location = 'YOUR_PROJECT_LOCATION';
    
    // Imports the Google Cloud Dataset Service Client library
    const {DatasetServiceClient} = require('@google-cloud/aiplatform');
    
    // Specifies the location of the api endpoint
    const clientOptions = {
      apiEndpoint: 'us-central1-aiplatform.googleapis.com',
    };
    
    // Instantiates a client
    const datasetServiceClient = new DatasetServiceClient(clientOptions);
    
    async function createDatasetImage() {
      // Configure the parent resource
      const parent = `projects/${project}/locations/${location}`;
      // Configure the dataset resource
      const dataset = {
        displayName: datasetDisplayName,
        metadataSchemaUri:
          'gs://google-cloud-aiplatform/schema/dataset/metadata/image_1.0.0.yaml',
      };
      const request = {
        parent,
        dataset,
      };
    
      // Create Dataset Request
      const [response] = await datasetServiceClient.createDataset(request);
      console.log(`Long running operation: ${response.name}`);
    
      // Wait for operation to complete
      await response.promise();
      const result = response.result;
    
      console.log('Create dataset image response');
      console.log(`Name : ${result.name}`);
      console.log(`Display name : ${result.displayName}`);
      console.log(`Metadata schema uri : ${result.metadataSchemaUri}`);
      console.log(`Metadata : ${JSON.stringify(result.metadata)}`);
      console.log(`Labels : ${JSON.stringify(result.labels)}`);
    }
    createDatasetImage();

### Python

To learn how to install or update the Vertex AI SDK for Python, see [Install the Vertex AI SDK for Python](https://docs.cloud.google.com/vertex-ai/docs/start/use-vertex-ai-python-sdk) . For more information, see the [Python API reference documentation](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest) .

The following sample uses the Vertex AI SDK for Python to both create a dataset and import data. If you run this sample code, then you can skip the [Import data section](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/image-data/classification/create-dataset#import-data) of this guide.

This particular sample imports data for single-label classification. If your model has a different objective, then you must adjust the code.

    from typing import List, Union
    
    from google.cloud import aiplatform
    
    
    def create_and_import_dataset_image_sample(
        project: str,
        location: str,
        display_name: str,
        src_uris: Union[str, List[str]],
        sync: bool = True,
    ):
        """
        src_uris -- a string or list of strings, e.g.
            ["gs://bucket1/source1.jsonl", "gs://bucket7/source4.jsonl"]
        """
    
        aiplatform.init(project=project, location=location)
    
        ds = aiplatform.ImageDataset.create(
            display_name=display_name,
            gcs_source=src_uris,
            import_schema_uri=aiplatform.schema.dataset.ioformat.image.single_label_classification,
            sync=sync,
        )
    
        ds.wait()
    
        print(ds.display_name)
        print(ds.resource_name)
        return ds

## Import data

After you create an empty dataset you can import your data into the dataset. If you used the Vertex AI SDK for Python to create the dataset, then you might have already imported data when you created the dataset. If so, you can skip this section.

Select the tab below for your objective:

### Single-label classification

### REST

Before using any of the request data, make the following replacements:

  - LOCATION : Region where the dataset is located. For example, `us-central1` .
  - PROJECT\_ID : .
  - DATASET\_ID : ID of the dataset.
  - IMPORT\_FILE\_URI : Path to the CSV or [JSON Lines](https://jsonlines.org/) file in Cloud Storage that lists data items stored in Cloud Storage to use for model training; for import file formats and limitations, see [Preparing image data](https://docs.cloud.google.com/vertex-ai/docs/datasets/prepare-image) .

HTTP method and URL:

    POST https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/datasets/DATASET_ID:import

Request JSON body:

    {
      "import_configs": [
        {
          "gcs_source": {
            "uris": "IMPORT_FILE_URI"
          },
         "import_schema_uri" : "gs://google-cloud-aiplatform/schema/dataset/ioformat/image_classification_multi_label_io_format_1.0.0.yaml"
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
         "https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/datasets/DATASET_ID:import"

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
        -Uri "https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/datasets/DATASET_ID:import" | Select-Object -Expand Content

You should see output similar to the following. You can use the OPERATION\_ID in the response to [get the status](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/image-data/classification/create-dataset#get-operation) of the operation.

    {
      "name": "projects/PROJECT_NUMBER/locations/LOCATION/datasets/DATASET_ID/operations/OPERATION_ID",
      "metadata": {
        "@type": "type.googleapis.com/google.cloud.aiplatform.v1.ImportDataOperationMetadata",
        "genericMetadata": {
          "createTime": "2020-07-08T20:32:02.543801Z",
          "updateTime": "2020-07-08T20:32:02.543801Z"
        }
      }
    }

### Java

Before trying this sample, follow the Java setup instructions in the [Agent Platform quickstart using client libraries](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/start/client-libraries) .

To authenticate to Agent Platform, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

    import com.google.api.gax.longrunning.OperationFuture;
    import com.google.cloud.aiplatform.v1.DatasetName;
    import com.google.cloud.aiplatform.v1.DatasetServiceClient;
    import com.google.cloud.aiplatform.v1.DatasetServiceSettings;
    import com.google.cloud.aiplatform.v1.GcsSource;
    import com.google.cloud.aiplatform.v1.ImportDataConfig;
    import com.google.cloud.aiplatform.v1.ImportDataOperationMetadata;
    import com.google.cloud.aiplatform.v1.ImportDataResponse;
    import java.io.IOException;
    import java.util.Collections;
    import java.util.List;
    import java.util.concurrent.ExecutionException;
    import java.util.concurrent.TimeUnit;
    import java.util.concurrent.TimeoutException;
    
    public class ImportDataImageClassificationSample {
    
      public static void main(String[] args)
          throws IOException, InterruptedException, ExecutionException, TimeoutException {
        // TODO(developer): Replace these variables before running the sample.
        String project = "YOUR_PROJECT_ID";
        String datasetId = "YOUR_DATASET_ID";
        String gcsSourceUri =
            "gs://YOUR_GCS_SOURCE_BUCKET/path_to_your_image_source/[file.csv/file.jsonl]";
        importDataImageClassificationSample(project, datasetId, gcsSourceUri);
      }
    
      static void importDataImageClassificationSample(
          String project, String datasetId, String gcsSourceUri)
          throws IOException, InterruptedException, ExecutionException, TimeoutException {
        DatasetServiceSettings datasetServiceSettings =
            DatasetServiceSettings.newBuilder()
                .setEndpoint("us-central1-aiplatform.googleapis.com:443")
                .build();
    
        // Initialize client that will be used to send requests. This client only needs to be created
        // once, and can be reused for multiple requests. After completing all of your requests, call
        // the "close" method on the client to safely clean up any remaining background resources.
        try (DatasetServiceClient datasetServiceClient =
            DatasetServiceClient.create(datasetServiceSettings)) {
          String location = "us-central1";
          String importSchemaUri =
              "gs://google-cloud-aiplatform/schema/dataset/ioformat/"
                  + "image_classification_single_label_io_format_1.0.0.yaml";
    
          GcsSource.Builder gcsSource = GcsSource.newBuilder();
          gcsSource.addUris(gcsSourceUri);
          DatasetName datasetName = DatasetName.of(project, location, datasetId);
    
          List<ImportDataConfig> importDataConfigList =
              Collections.singletonList(
                  ImportDataConfig.newBuilder()
                      .setGcsSource(gcsSource)
                      .setImportSchemaUri(importSchemaUri)
                      .build());
    
          OperationFuture<ImportDataResponse, ImportDataOperationMetadata> importDataResponseFuture =
              datasetServiceClient.importDataAsync(datasetName, importDataConfigList);
          System.out.format(
              "Operation name: %s\n", importDataResponseFuture.getInitialFuture().get().getName());
          System.out.println("Waiting for operation to finish...");
          ImportDataResponse importDataResponse = importDataResponseFuture.get(300, TimeUnit.SECONDS);
    
          System.out.format(
              "Import Data Image Classification Response: %s\n", importDataResponse.toString());
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
    
    // const datasetId = "YOUR_DATASET_ID";
    // const gcsSourceUri = "YOUR_GCS_SOURCE_URI";
    // eg. "gs://<your-gcs-bucket>/<import_source_path>/[file.csv/file.jsonl]"
    // const project = "YOUR_PROJECT_ID";
    // const location = 'YOUR_PROJECT_LOCATION';
    
    // Imports the Google Cloud Dataset Service Client library
    const {DatasetServiceClient} = require('@google-cloud/aiplatform');
    
    // Specifies the location of the api endpoint
    const clientOptions = {
      apiEndpoint: 'us-central1-aiplatform.googleapis.com',
    };
    const datasetServiceClient = new DatasetServiceClient(clientOptions);
    
    async function importDataImageClassification() {
      const name = datasetServiceClient.datasetPath(project, location, datasetId);
      // Here we use only one import config with one source
      const importConfigs = [
        {
          gcsSource: {uris: [gcsSourceUri]},
          importSchemaUri:
            'gs://google-cloud-aiplatform/schema/dataset/ioformat/image_classification_single_label_io_format_1.0.0.yaml',
        },
      ];
      const request = {
        name,
        importConfigs,
      };
    
      // Create Import Data Request
      const [response] = await datasetServiceClient.importData(request);
      console.log(`Long running operation: ${response.name}`);
    
      // Wait for operation to complete
      const [importDataResponse] = await response.promise();
    
      console.log(
        `Import data image classification response : \
          ${JSON.stringify(importDataResponse)}`
      );
    }
    importDataImageClassification();

### Python

To learn how to install or update the Vertex AI SDK for Python, see [Install the Vertex AI SDK for Python](https://docs.cloud.google.com/vertex-ai/docs/start/use-vertex-ai-python-sdk) . For more information, see the [Python API reference documentation](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest) .

    def image_dataset_import_data_sample(
        project: str, location: str, src_uris: list, import_schema_uri: str, dataset_id: str
    ):
        aiplatform.init(project=project, location=location)
    
        ds = aiplatform.ImageDataset(dataset_id)
    
        ds = ds.import_data(
            gcs_source=src_uris, import_schema_uri=import_schema_uri, sync=True
        )
    
        print(ds.display_name)
        print(ds.name)
        print(ds.resource_name)
        return ds

### Multi-label classification

### REST

Before using any of the request data, make the following replacements:

  - LOCATION : Region where the dataset is located. For example, `us-central1` .
  - PROJECT\_ID : .
  - DATASET\_ID : ID of the dataset.
  - IMPORT\_FILE\_URI : Path to the CSV or [JSON Lines](https://jsonlines.org/) file in Cloud Storage that lists data items stored in Cloud Storage to use for model training; for import file formats and limitations, see [Preparing image data](https://docs.cloud.google.com/vertex-ai/docs/datasets/prepare-image) .

HTTP method and URL:

    POST https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/datasets/DATASET_ID:import

Request JSON body:

    {
      "import_configs": [
        {
          "gcs_source": {
            "uris": "IMPORT_FILE_URI"
          },
         "import_schema_uri" : "gs://google-cloud-aiplatform/schema/dataset/ioformat/image_classification_multi_label_io_format_1.0.0.yaml"
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
         "https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/datasets/DATASET_ID:import"

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
        -Uri "https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/datasets/DATASET_ID:import" | Select-Object -Expand Content

You should see output similar to the following. You can use the OPERATION\_ID in the response to [get the status](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/image-data/classification/create-dataset#get-operation) of the operation.

    {
      "name": "projects/PROJECT_NUMBER/locations/LOCATION/datasets/DATASET_ID/operations/OPERATION_ID",
      "metadata": {
        "@type": "type.googleapis.com/google.cloud.aiplatform.v1.ImportDataOperationMetadata",
        "genericMetadata": {
          "createTime": "2020-07-08T20:32:02.543801Z",
          "updateTime": "2020-07-08T20:32:02.543801Z"
        }
      }
    }

### Python

To learn how to install or update the Vertex AI SDK for Python, see [Install the Vertex AI SDK for Python](https://docs.cloud.google.com/vertex-ai/docs/start/use-vertex-ai-python-sdk) . For more information, see the [Python API reference documentation](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest) .

    def image_dataset_import_data_sample(
        project: str, location: str, src_uris: list, import_schema_uri: str, dataset_id: str
    ):
        aiplatform.init(project=project, location=location)
    
        ds = aiplatform.ImageDataset(dataset_id)
    
        ds = ds.import_data(
            gcs_source=src_uris, import_schema_uri=import_schema_uri, sync=True
        )
    
        print(ds.display_name)
        print(ds.name)
        print(ds.resource_name)
        return ds

## Get operation status

Some requests start long-running operations that require time to complete. These requests return an operation name, which you can use to view the operation's status or cancel the operation. Vertex AI provides helper methods to make calls against long-running operations. For more information, see [Working with long-running operations](https://docs.cloud.google.com/vertex-ai/docs/general/long-running-operations) .
