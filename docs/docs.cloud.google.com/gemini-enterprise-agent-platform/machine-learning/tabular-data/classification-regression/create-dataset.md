---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tabular-data/classification-regression/create-dataset
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tabular-data/classification-regression/create-dataset
title: Create a dataset for training classification and regression models
description: Create a dataset for training classification and regression models in Agent Platform.
data_source: docs.cloud.google.com
---

This page shows you how to create a Gemini Enterprise Agent Platform dataset from your tabular data so you can start training classification and regression models. You can create a dataset using either the Google Cloud console or the Agent Platform API.

## Before you begin

Before you create an Agent Platform dataset from your tabular data, first prepare your data. For details, see:

  - [Prepare tabular training data for classification and regression models](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tabular-data/classification-regression/prepare-data)
  - [Best practices for creating tabular training data](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tabular-data/bp-tabular) .

## Create an empty dataset and associate your prepared data

To create a machine learning model for classification or regression, you must first have a representative collection of data to train with. Use the Google Cloud console or the API to associate your prepared data into the dataset. Associating your data lets you make modifications and start model training.

### Google Cloud console

1.  In the Google Cloud console, in the Agent Platform section, go to the **Datasets** page.

2.  Click **Create** to open the create dataset details page.

3.  Modify the **Dataset name** field to create a descriptive dataset display name.

4.  Select the **Tabular** tab.

5.  Select the **Regression/classification** objective.

6.  Select a region from the **Region** drop-down list.

7.  If you want to use [customer-managed encryption keys (CMEK)](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/cmek) with your dataset, open **Advanced options** and provide your key. ( [Preview](https://cloud.google.com/products/#product-launch-stages) )

8.  Click **Create** to create your empty dataset, and advance to the **Source** tab.

9.  Choose one of the following options, based on your data source.
    
    > Tabular training data in Cloud Storage or BigQuery is not imported into Agent Platform. (When you import from local files, they are imported into Cloud Storage.) When you create a dataset with tabular data, the data is associated with the dataset. Changes you make to your data source in Cloud Storage or BigQuery after dataset creation are incorporated into models subsequently trained with that dataset. A snapshot of the dataset is taken when model training begins.
    
    ### CSV files on your computer
    
    1.  Click radio\_button\_checked **Upload CSV files from your computer** .
    2.  Click **Select files** and choose all the local files to upload to a Cloud Storage bucket.
    3.  In the **Select a Cloud Storage path** section enter the path to the Cloud Storage bucket or click **Browse** to choose a bucket location.
    
    ### CSV files in Cloud Storage
    
    1.  Click radio\_button\_checked **Select CSV files from Cloud Storage** .
    2.  In the **Select CSV files from Cloud Storage** section enter the path to the Cloud Storage bucket or click **Browse** to choose the location of your CSV files.
    
    ### A table or view in BigQuery
    
    1.  Click radio\_button\_checked **Select a table or view from BigQuery** .
    2.  Enter the project, dataset, and table IDs for your input file.

10. Click **Continue** .
    
    Your data source is associated with your dataset.

### API

When you create a dataset, you also associate it with its data source. The code needed to create a dataset depends on whether the training data resides in [Cloud Storage](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tabular-data/classification-regression/create-dataset#gcs) or [BigQuery](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tabular-data/classification-regression/create-dataset#bq) . If the data source resides in a different project, make sure you [set up the required permissions](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/access-control#foreign-project) .

> Tabular training data in Cloud Storage or BigQuery is not imported into Agent Platform. (When you import from local files, they are imported into Cloud Storage.) When you create a dataset with tabular data, the data is associated with the dataset. Changes you make to your data source in Cloud Storage or BigQuery after dataset creation are incorporated into models subsequently trained with that dataset. A snapshot of the dataset is taken when model training begins.

### Creating a dataset with data in Cloud Storage

### REST

You use the [datasets.create](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.datasets/create) method to create a dataset.

Before using any of the request data, make the following replacements:

  - LOCATION : Region where the dataset will be stored. This must be a [region that supports dataset resources](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/locations#feature-availability) . For example, `us-central1` .

  - PROJECT : Your [project ID](https://docs.cloud.google.com/resource-manager/docs/creating-managing-projects#identifiers) .

  - DATASET\_NAME : Display name for the dataset.

  - METADATA\_SCHEMA\_URI : The URI to the schema file for your objective. `gs://google-cloud-aiplatform/schema/dataset/metadata/tabular_1.0.0.yaml`

  - URI : Paths (URIs) to the Cloud Storage buckets containing the training data. There can be more than one. Each URI has the form:
    
        gs://GCSprojectId/bucketName/fileName

  - PROJECT\_NUMBER : Your project's automatically generated [project number](https://docs.cloud.google.com/resource-manager/docs/creating-managing-projects#identifiers) .

HTTP method and URL:

    POST https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT/locations/LOCATION/datasets

Request JSON body:

    {
      "display_name": "DATASET_NAME",
      "metadata_schema_uri": "METADATA_SCHEMA_URI",
      "metadata": {
        "input_config": {
          "gcs_source": {
            "uri": [URI1, URI2, ...]
          }
        }
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
         "https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT/locations/LOCATION/datasets"

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
        -Uri "https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT/locations/LOCATION/datasets" | Select-Object -Expand Content

You should receive a JSON response similar to the following:

    {
      "name": "projects/PROJECT_NUMBER/locations/LOCATION/datasets/DATASET_ID/operations/OPERATION_ID",
      "metadata": {
        "@type": "type.googleapis.com/google.cloud.aiplatform.v1.CreateDatasetOperationMetadata",
        "genericMetadata": {
          "createTime": "2020-07-07T21:27:35.964882Z",
          "updateTime": "2020-07-07T21:27:35.964882Z"
        }
    }

### Java

Before trying this sample, follow the Java setup instructions in the [Agent Platform quickstart using client libraries](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/start/client-libraries) . For more information, see the [Agent Platform Java API reference documentation](https://docs.cloud.google.com/java/docs/reference/google-cloud-aiplatform/latest/com.google.cloud.aiplatform.v1) .

To authenticate to Agent Platform, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

    import com.google.api.gax.longrunning.OperationFuture;
    import com.google.cloud.aiplatform.v1.CreateDatasetOperationMetadata;
    import com.google.cloud.aiplatform.v1.Dataset;
    import com.google.cloud.aiplatform.v1.DatasetServiceClient;
    import com.google.cloud.aiplatform.v1.DatasetServiceSettings;
    import com.google.cloud.aiplatform.v1.LocationName;
    import com.google.protobuf.Value;
    import com.google.protobuf.util.JsonFormat;
    import java.io.IOException;
    import java.util.concurrent.ExecutionException;
    import java.util.concurrent.TimeUnit;
    import java.util.concurrent.TimeoutException;
    
    public class CreateDatasetTabularGcsSample {
    
      public static void main(String[] args)
          throws InterruptedException, ExecutionException, TimeoutException, IOException {
        // TODO(developer): Replace these variables before running the sample.
        String project = "YOUR_PROJECT_ID";
        String datasetDisplayName = "YOUR_DATASET_DISPLAY_NAME";
        String gcsSourceUri = "gs://YOUR_GCS_SOURCE_BUCKET/path_to_your_gcs_table/file.csv";
        ;
        createDatasetTableGcs(project, datasetDisplayName, gcsSourceUri);
      }
    
      static void createDatasetTableGcs(String project, String datasetDisplayName, String gcsSourceUri)
          throws IOException, ExecutionException, InterruptedException, TimeoutException {
        DatasetServiceSettings settings =
            DatasetServiceSettings.newBuilder()
                .setEndpoint("us-central1-aiplatform.googleapis.com:443")
                .build();
    
        // Initialize client that will be used to send requests. This client only needs to be created
        // once, and can be reused for multiple requests. After completing all of your requests, call
        // the "close" method on the client to safely clean up any remaining background resources.
        try (DatasetServiceClient datasetServiceClient = DatasetServiceClient.create(settings)) {
          String location = "us-central1";
          String metadataSchemaUri =
              "gs://google-cloud-aiplatform/schema/dataset/metadata/tables_1.0.0.yaml";
          LocationName locationName = LocationName.of(project, location);
    
          String jsonString =
              "{\"input_config\": {\"gcs_source\": {\"uri\": [\"" + gcsSourceUri + "\"]}}}";
          Value.Builder metaData = Value.newBuilder();
          JsonFormat.parser().merge(jsonString, metaData);
    
          Dataset dataset =
              Dataset.newBuilder()
                  .setDisplayName(datasetDisplayName)
                  .setMetadataSchemaUri(metadataSchemaUri)
                  .setMetadata(metaData)
                  .build();
    
          OperationFuture<Dataset, CreateDatasetOperationMetadata> datasetFuture =
              datasetServiceClient.createDatasetAsync(locationName, dataset);
          System.out.format("Operation name: %s\n", datasetFuture.getInitialFuture().get().getName());
          System.out.println("Waiting for operation to finish...");
          Dataset datasetResponse = datasetFuture.get(300, TimeUnit.SECONDS);
    
          System.out.println("Create Dataset Table GCS sample");
          System.out.format("Name: %s\n", datasetResponse.getName());
          System.out.format("Display Name: %s\n", datasetResponse.getDisplayName());
          System.out.format("Metadata Schema Uri: %s\n", datasetResponse.getMetadataSchemaUri());
          System.out.format("Metadata: %s\n", datasetResponse.getMetadata());
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
    
    // const datasetDisplayName = 'YOUR_DATASET_DISPLAY_NAME';
    // const gcsSourceUri = 'YOUR_GCS_SOURCE_URI';
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
    
    async function createDatasetTabularGcs() {
      // Configure the parent resource
      const parent = `projects/${project}/locations/${location}`;
      const metadata = {
        structValue: {
          fields: {
            inputConfig: {
              structValue: {
                fields: {
                  gcsSource: {
                    structValue: {
                      fields: {
                        uri: {
                          listValue: {
                            values: [{stringValue: gcsSourceUri}],
                          },
                        },
                      },
                    },
                  },
                },
              },
            },
          },
        },
      };
      // Configure the dataset resource
      const dataset = {
        displayName: datasetDisplayName,
        metadataSchemaUri:
          'gs://google-cloud-aiplatform/schema/dataset/metadata/tabular_1.0.0.yaml',
        metadata: metadata,
      };
      const request = {
        parent,
        dataset,
      };
    
      // Create dataset request
      const [response] = await datasetServiceClient.createDataset(request);
      console.log(`Long running operation : ${response.name}`);
    
      // Wait for operation to complete
      await response.promise();
      const result = response.result;
    
      console.log('Create dataset tabular gcs response');
      console.log(`\tName : ${result.name}`);
      console.log(`\tDisplay name : ${result.displayName}`);
      console.log(`\tMetadata schema uri : ${result.metadataSchemaUri}`);
      console.log(`\tMetadata : ${JSON.stringify(result.metadata)}`);
    }
    createDatasetTabularGcs();

### Python

To learn how to install or update the Vertex AI SDK for Python, see [Install the Vertex AI SDK for Python](https://docs.cloud.google.com/vertex-ai/docs/start/use-vertex-ai-python-sdk) . For more information, see the [Python API reference documentation](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest) .

    def create_and_import_dataset_tabular_gcs_sample(
        display_name: str,
        project: str,
        location: str,
        gcs_source: Union[str, List[str]],
    ):
    
        aiplatform.init(project=project, location=location)
    
        dataset = aiplatform.TabularDataset.create(
            display_name=display_name,
            gcs_source=gcs_source,
        )
    
        dataset.wait()
    
        print(f'\tDataset: "{dataset.display_name}"')
        print(f'\tname: "{dataset.resource_name}"')

### Creating a dataset with data in BigQuery

### REST

You use the [datasets.create](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.datasets/create) method to create a dataset.

Before using any of the request data, make the following replacements:

  - LOCATION : Region where the dataset will be stored. This must be a [region that supports dataset resources](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/locations#feature-availability) . For example, `us-central1` .

  - PROJECT : .

  - DATASET\_NAME : Display name for the dataset.

  - METADATA\_SCHEMA\_URI : The URI to the schema file for your objective. `gs://google-cloud-aiplatform/schema/dataset/metadata/tabular_1.0.0.yaml`

  - URI : Path to the BigQuery table containing the training data. In the form:
    
        bq://bqprojectId.bqDatasetId.bqTableId

  - PROJECT\_NUMBER : Your project's automatically generated [project number](https://docs.cloud.google.com/resource-manager/docs/creating-managing-projects#identifiers) .

HTTP method and URL:

    POST https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT/locations/LOCATION/datasets

Request JSON body:

    {
      "display_name": "DATASET_NAME",
      "metadata_schema_uri": "METADATA_SCHEMA_URI",
      "metadata": {
        "input_config": {
          "bigquery_source" :{
            "uri": "URI
          }
        }
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
         "https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT/locations/LOCATION/datasets"

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
        -Uri "https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT/locations/LOCATION/datasets" | Select-Object -Expand Content

You should receive a JSON response similar to the following:

    {
      "name": "projects/PROJECT_NUMBER/locations/LOCATION/datasets/DATASET_ID/operations/OPERATION_ID",
      "metadata": {
        "@type": "type.googleapis.com/google.cloud.aiplatform.v1.CreateDatasetOperationMetadata",
        "genericMetadata": {
          "createTime": "2020-07-07T21:27:35.964882Z",
          "updateTime": "2020-07-07T21:27:35.964882Z"
        }
    }

### Java

Before trying this sample, follow the Java setup instructions in the [Agent Platform quickstart using client libraries](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/start/client-libraries) . For more information, see the [Agent Platform Java API reference documentation](https://docs.cloud.google.com/java/docs/reference/google-cloud-aiplatform/latest/com.google.cloud.aiplatform.v1) .

To authenticate to Agent Platform, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

    import com.google.api.gax.longrunning.OperationFuture;
    import com.google.cloud.aiplatform.v1.CreateDatasetOperationMetadata;
    import com.google.cloud.aiplatform.v1.Dataset;
    import com.google.cloud.aiplatform.v1.DatasetServiceClient;
    import com.google.cloud.aiplatform.v1.DatasetServiceSettings;
    import com.google.cloud.aiplatform.v1.LocationName;
    import com.google.protobuf.Value;
    import com.google.protobuf.util.JsonFormat;
    import java.io.IOException;
    import java.util.concurrent.ExecutionException;
    import java.util.concurrent.TimeUnit;
    import java.util.concurrent.TimeoutException;
    
    public class CreateDatasetTabularBigquerySample {
    
      public static void main(String[] args)
          throws InterruptedException, ExecutionException, TimeoutException, IOException {
        // TODO(developer): Replace these variables before running the sample.
        String project = "YOUR_PROJECT_ID";
        String bigqueryDisplayName = "YOUR_DATASET_DISPLAY_NAME";
        String bigqueryUri =
            "bq://YOUR_GOOGLE_CLOUD_PROJECT_ID.BIGQUERY_DATASET_ID.BIGQUERY_TABLE_OR_VIEW_ID";
        createDatasetTableBigquery(project, bigqueryDisplayName, bigqueryUri);
      }
    
      static void createDatasetTableBigquery(
          String project, String bigqueryDisplayName, String bigqueryUri)
          throws IOException, ExecutionException, InterruptedException, TimeoutException {
        DatasetServiceSettings settings =
            DatasetServiceSettings.newBuilder()
                .setEndpoint("us-central1-aiplatform.googleapis.com:443")
                .build();
    
        // Initialize client that will be used to send requests. This client only needs to be created
        // once, and can be reused for multiple requests. After completing all of your requests, call
        // the "close" method on the client to safely clean up any remaining background resources.
        try (DatasetServiceClient datasetServiceClient = DatasetServiceClient.create(settings)) {
          String location = "us-central1";
          String metadataSchemaUri =
              "gs://google-cloud-aiplatform/schema/dataset/metadata/tables_1.0.0.yaml";
          LocationName locationName = LocationName.of(project, location);
    
          String jsonString =
              "{\"input_config\": {\"bigquery_source\": {\"uri\": \"" + bigqueryUri + "\"}}}";
          Value.Builder metaData = Value.newBuilder();
          JsonFormat.parser().merge(jsonString, metaData);
    
          Dataset dataset =
              Dataset.newBuilder()
                  .setDisplayName(bigqueryDisplayName)
                  .setMetadataSchemaUri(metadataSchemaUri)
                  .setMetadata(metaData)
                  .build();
    
          OperationFuture<Dataset, CreateDatasetOperationMetadata> datasetFuture =
              datasetServiceClient.createDatasetAsync(locationName, dataset);
          System.out.format("Operation name: %s\n", datasetFuture.getInitialFuture().get().getName());
          System.out.println("Waiting for operation to finish...");
          Dataset datasetResponse = datasetFuture.get(300, TimeUnit.SECONDS);
    
          System.out.println("Create Dataset Table Bigquery sample");
          System.out.format("Name: %s\n", datasetResponse.getName());
          System.out.format("Display Name: %s\n", datasetResponse.getDisplayName());
          System.out.format("Metadata Schema Uri: %s\n", datasetResponse.getMetadataSchemaUri());
          System.out.format("Metadata: %s\n", datasetResponse.getMetadata());
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
    
    // const datasetDisplayName = 'YOUR_DATASET_DISPLAY_NAME';
    // const bigquerySourceUri = 'YOUR_BIGQUERY_SOURCE_URI';
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
    
    async function createDatasetTabularBigquery() {
      // Configure the parent resource
      const parent = `projects/${project}/locations/${location}`;
      const metadata = {
        structValue: {
          fields: {
            inputConfig: {
              structValue: {
                fields: {
                  bigquerySource: {
                    structValue: {
                      fields: {
                        uri: {
                          listValue: {
                            values: [{stringValue: bigquerySourceUri}],
                          },
                        },
                      },
                    },
                  },
                },
              },
            },
          },
        },
      };
      // Configure the dataset resource
      const dataset = {
        displayName: datasetDisplayName,
        metadataSchemaUri:
          'gs://google-cloud-aiplatform/schema/dataset/metadata/tabular_1.0.0.yaml',
        metadata: metadata,
      };
      const request = {
        parent,
        dataset,
      };
    
      // Create dataset request
      const [response] = await datasetServiceClient.createDataset(request);
      console.log(`Long running operation : ${response.name}`);
    
      // Wait for operation to complete
      await response.promise();
      const result = response.result;
    
      console.log('Create dataset tabular bigquery response');
      console.log(`\tName : ${result.name}`);
      console.log(`\tDisplay name : ${result.displayName}`);
      console.log(`\tMetadata schema uri : ${result.metadataSchemaUri}`);
      console.log(`\tMetadata : ${JSON.stringify(result.metadata)}`);
    }
    createDatasetTabularBigquery();

### Python

To learn how to install or update the Vertex AI SDK for Python, see [Install the Vertex AI SDK for Python](https://docs.cloud.google.com/vertex-ai/docs/start/use-vertex-ai-python-sdk) . For more information, see the [Python API reference documentation](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest) .

    def create_and_import_dataset_tabular_bigquery_sample(
        display_name: str,
        project: str,
        location: str,
        bq_source: str,
    ):
    
        aiplatform.init(project=project, location=location)
    
        dataset = aiplatform.TabularDataset.create(
            display_name=display_name,
            bq_source=bq_source,
        )
    
        dataset.wait()
    
        print(f'\tDataset: "{dataset.display_name}"')
        print(f'\tname: "{dataset.resource_name}"')

### Get operation status

Some requests start long-running operations that require time to complete. These requests return an operation name, which you can use to view the operation's status or cancel the operation. Agent Platform provides helper methods to make calls against long-running operations. For more information, see [Working with long-running operations](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/long-running-operations) .

## What's next

  - [Train a classification or regression model with your dataset](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tabular-data/classification-regression/train-model) .
