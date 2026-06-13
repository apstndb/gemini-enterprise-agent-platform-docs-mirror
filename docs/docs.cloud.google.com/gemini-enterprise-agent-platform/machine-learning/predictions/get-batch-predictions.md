---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/get-batch-predictions
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/get-batch-predictions
title: Get batch inferences from a custom trained model
description: Get batch inferences from a custom trained model in Gemini Enterprise Agent Platform.
data_source: docs.cloud.google.com
---

This page shows you how to get batch inferences from your custom trained models using the Google Cloud console or the Agent Platform API.

To make a batch inference request, you specify an [input source](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/get-batch-predictions#input_data_requirements) and an output location, either [Cloud Storage](https://docs.cloud.google.com/storage/docs/introduction) or [BigQuery](https://docs.cloud.google.com/bigquery/docs/introduction) , where Gemini Enterprise Agent Platform stores the batch inference results.

## Limitations and requirements

Consider the following limitations and requirements when getting batch inferences:

  - To minimize processing time, your input and output locations must be in the same region or multi-region. For example, if your input is in `us-central1` , your output can be in `us-central1` or `US` , but not `europe-west4` . To learn more, see [Cloud Storage locations](https://docs.cloud.google.com/storage/docs/locations) and [BigQuery locations](https://docs.cloud.google.com/bigquery/docs/locations) .
  - Your input and output must also be in the same region or multi-region as your model.
  - Unlike online inference, batch inference jobs don't [autoscale](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/deployment#scaling) . Because all of the input data is known up front, the system partitions the data to each replica when the job starts. The system uses the `starting_replica_count` parameter. The `max_replica_count` parameter is ignored.
  - BigQuery ML models aren't custom trained models. However, the information in this page can be used to get batch inferences from a BigQuery ML model under the following conditions:
      - The BigQuery ML model must be registered with Gemini Enterprise Agent Platform Model Registry.
      - To use a BigQuery table as input, you must set [`InstanceConfig.instanceType`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.batchPredictionJobs#instanceconfig) to `"object"` using the Agent Platform API.
  - Loading a batch inference model times out after approximately 40 minutes. If you see the following error message, use a smaller model for batch inferences: `Error: model server never became ready. Please validate that your model file or container configuration are valid.`
  - Custom service accounts are only supported for the model server, not for the batch inference client that performs data read and write operations to and from Cloud Storage and BigQuery.

## Input data requirements

The input for batch requests specifies the items to send to your model for inference. We support the following input formats:

> **Note:** Gemini Enterprise Agent Platform transforms your input to JSON instances before sending it to the inference container. Make sure your container accepts instances as described in [Custom container requirements](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/custom-container-requirements#prediction) .

> **Note:** For [PyTorch prebuilt containers](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/pre-built-containers#pytorch) , Gemini Enterprise Agent Platform wraps each instance in a `data` field before sending it to the container. This is because TorchServe's default handlers expect each instance to be wrapped in a `data` field.

### JSON Lines

Use a [JSON Lines](https://jsonlines.org/) file to specify a list of input instances to make inferences about. Store the file in a Cloud Storage bucket.

**Example 1**

The following example shows a JSON Lines file where each line contains an array:

    [1, 2, 3, 4]
    [5, 6, 7, 8]

Here is what is sent to the container in the HTTP request body:

### All other containers

    {"instances": [ [1, 2, 3, 4], [5, 6, 7, 8] ]}

### PyTorch containers

    {"instances": [
    { "data": [1, 2, 3, 4] },
    { "data": [5, 6, 7, 8] } ]}

**Example 2**

The following example shows a JSON Lines file where each line contains an object.

    { "values": [1, 2, 3, 4], "key": 1 }
    { "values": [5, 6, 7, 8], "key": 2 }

Here is what is sent to the container in the HTTP request body. Note that the same request body is sent to all containers.

    {"instances": [
      { "values": [1, 2, 3, 4], "key": 1 },
      { "values": [5, 6, 7, 8], "key": 2 }
    ]}

**Example 3**

For PyTorch prebuilt containers, make sure that you wrap each instance in a `data` field as required by TorchServe's default handler; Gemini Enterprise Agent Platform doesn't wrap your instances for you. For example:

    { "data": { "values": [1, 2, 3, 4], "key": 1 } }
    { "data": { "values": [5, 6, 7, 8], "key": 2 } }

Here is what is sent to the inference container in the HTTP request body:

    {"instances": [
      { "data": { "values": [1, 2, 3, 4], "key": 1 } },
      { "data": { "values": [5, 6, 7, 8], "key": 2 } }
    ]}

### TFRecord

Save input instances in the [TFRecord format](https://www.tensorflow.org/guide/data#consuming_tfrecord_data) . You can optionally compress the TFRecord files with Gzip. Store the TFRecord files in a Cloud Storage bucket.

Agent Platform reads each instance in your TFRecord files as binary and then base64-encodes the instance as JSON object with a single key named `b64` .

Here is what is sent to the container in the HTTP request body:

### All other containers

    {"instances": [
    { "b64": "b64EncodedASCIIString" },
    { "b64": "b64EncodedASCIIString" } ]}

### PyTorch containers

    {"instances": [ { "data": {"b64": "b64EncodedASCIIString" } }, { "data": {"b64": "b64EncodedASCIIString" } }
    ]}

Make sure your container knows how to decode the instance.

### CSV

Specify one input instance per row in a CSV file. The first row must be a header row. You must enclose all strings in double quotation marks ("). Agent Platform doesn't accept cell values that contain newlines. Non-quoted values are read as floating point numbers.

The following example shows a CSV file with two input instances:

    "input1","input2","input3"
    0.1,1.2,"cat1"
    4.0,5.0,"cat2"

Here is what is sent to the container in the HTTP request body:

### All other containers

    {"instances": [ [0.1,1.2,"cat1"], [4.0,5.0,"cat2"] ]}

### PyTorch containers

    {"instances": [
    { "data": [0.1,1.2,"cat1"] },
    { "data": [4.0,5.0,"cat2"] } ]}

### File list

Create a text file where each row is the Cloud Storage URI to a file. Agent Platform reads the contents of each file as binary and then base64-encodes the instance as JSON object with a single key named `b64` .

If you plan to use the Google Cloud console to get batch inferences, paste your file list directly into the Google Cloud console. Otherwise, save the list in a Cloud Storage bucket.

The following example shows a file list with two input instances:

    gs://path/to/image/image1.jpg
    gs://path/to/image/image2.jpg

Here is what is sent to the container in the HTTP request body:

### All other containers

    { "instances": [
    { "b64": "b64EncodedASCIIString" },
    { "b64": "b64EncodedASCIIString" } ]}

### PyTorch containers

    { "instances": [ { "data": { "b64": "b64EncodedASCIIString" } }, { "data": { "b64": "b64EncodedASCIIString" } }
    ]}

Make sure your container knows how to decode the instance.

### BigQuery

Specify a BigQuery table as `projectId.datasetId.tableId` . Agent Platform transforms each row from the table to a JSON instance.

For example, if your table contains the following:

| Column 1 | Column 2 | Column 3 |
| -------- | -------- | -------- |
| 1.0      | 3.0      | "Cat1"   |
| 2.0      | 4.0      | "Cat2"   |

Here is what is sent to the container in the HTTP request body:

### All other containers

    {"instances": [ [1.0,3.0,"cat1"], [2.0,4.0,"cat2"] ]}

### PyTorch containers

    {"instances": [
    { "data": [1.0,3.0,"cat1"] },
    { "data": [2.0,4.0,"cat2"] } ]}

Here is how BigQuery data types are converted to JSON:

| BigQuery Type | JSON Type     | Example value                      |
| ------------- | ------------- | ---------------------------------- |
| String        | String        | "abc"                              |
| Integer       | Integer       | 1                                  |
| Float         | Float         | 1.2                                |
| Numeric       | Float         | 4925.000000000                     |
| Boolean       | Boolean       | true                               |
| TimeStamp     | String        | "2019-01-01 23:59:59.999999+00:00" |
| Date          | String        | "2018-12-31"                       |
| Time          | String        | "23:59:59.999999"                  |
| DateTime      | String        | "2019-01-01T00:00:00"              |
| Record        | Object        | { "A": 1,"B": 2}                   |
| Repeated Type | Array\[Type\] | \[1, 2\]                           |
| Nested Record | Object        | {"A": {"a": 0}, "B": 1}            |

## Partition data

Batch inference uses MapReduce to shard the input to each replica. To make use of the MapReduce features, the input should be partitionable.

Gemini Enterprise Agent Platform automatically partitions **BigQuery** , **file list** , and **JSON lines** input.

Gemini Enterprise Agent Platform does not automatically partition **CSV** files because they are not naturally partition-friendly. Rows in CSV files are not self-descriptive, typed, and may contain newlines. We recommend against using CSV input for throughput-sensitive applications.

For **TFRecord** input, make sure you manually partition the data by splitting the instances into smaller files and passing the files to the job with a wildcard (for example, `gs://my-bucket/*.tfrecord` ). The number of files should be at least the number of replicas specified.

## Filter and transform input data

You can filter and transform your batch input by specifying [`instanceConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.batchPredictionJobs#instanceconfig) in your [`BatchPredictionJob`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.batchPredictionJobs) request.

**Filtering** lets you either exclude certain fields that are in the input data from your inference request, or include only a subset of fields from the input data in your inference request, without having to do any custom pre-processing or post-processing in the inference container. This is useful when your input data file has extra columns that the model doesn't need, such as keys or additional data.

**Transforming** lets you send the instances to your container in either a JSON `array` or `object` format. See [`instanceType`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.batchPredictionJobs#instanceconfig) for more information.

For example, if your input table contains the following:

| customerId | col1 | col2 |
| ---------- | ---- | ---- |
| 1001       | 1    | 2    |
| 1002       | 5    | 6    |

and you specify the following `instanceConfig` :

    {
      "name": "batchJob1",
      ...
      "instanceConfig": {
        "excludedFields":["customerId"]
        "instanceType":"object"
      }
    }

Next, the instances in your inference request are sent as JSON objects, and the `customerId` column is excluded:

    {"col1":1,"col2":2}
    {"col1":5,"col2":6}

Note that specifying the following `instanceConfig` would yield the same result:

    {
      "name": "batchJob1",
      ...
      "instanceConfig": {
        "includedFields": ["col1","col2"]
        "instanceType":"object"
      }
    }

For a demonstration on how to use feature filters, see the [Custom model batch inference with feature filtering](https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/prediction/custom_batch_prediction_feature_filter.ipynb) notebook.

## Request a batch inference

For batch inference requests, you can use the Google Cloud console or the Agent Platform API. Depending on the number of input items that you've submitted, a batch inference task can take some time to complete.

When you request a batch inference, the inference container runs as the user-provided [custom service account](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/custom-service-account) . The read-write operations, such as reading the inference instances from the data source or writing the inference results, are done using the [Gemini Enterprise Agent Platform service agent](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/access-control#service-agents) , which by default has access to BigQuery and Cloud Storage.

### Google Cloud console

Use the Google Cloud console to request a batch inference.

1.  In the Google Cloud console, in the Agent Platform section, go to the **Batch predictions** page.

<!-- end list -->

1.  Click **Create** to open the **New batch prediction** window.

2.  For **Define your batch prediction** , complete the following steps:
    
    1.  Enter a name for the batch inference.
    
    2.  For **Model name** , select the name of the model to use for this batch inference.
    
    3.  For **Select source** , select the source that applies to your [input data](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/get-batch-predictions#input_data_requirements) :
        
          - If you have formatted your input as JSON Lines, CSV, or TFRecord, select **File on Cloud Storage (JSON Lines, CSV, TFRecord, TFRecord Gzip)** . Then specify your input file in the **Source path** field.
          - If you are using a file list as input, select **Files on Cloud Storage (other)** and paste your file list into the following field.
          - For BigQuery input, select **BigQuery path** . If you select BigQuery as input, you must also select BigQuery as output and Google-managed encryption key. Customer-managed encryption key (CMEK) isn't supported with BigQuery as input/output.
    
    4.  In the **Destination path** field, specify the Cloud Storage directory where you want Agent Platform to store batch inference output.
    
    5.  Optionally, you can check **Enable feature attributions for this model** to get [feature attributions](https://docs.cloud.google.com/vertex-ai/docs/explainable-ai/overview) as part of the batch inference response. Then click **Edit** to [configure explanation settings](https://docs.cloud.google.com/vertex-ai/docs/explainable-ai/configuring-explanations) . (Editing the explanation settings is optional if you previously configured explanation settings for the model, and required otherwise.)
    
    6.  Specify compute options for the batch inference job: **Number of compute nodes** , [**Machine type**](https://docs.cloud.google.com/vertex-ai/docs/predictions/configure-compute) , and (optionally) [**Accelerator type**](https://docs.cloud.google.com/vertex-ai/docs/predictions/configure-compute#gpus) and **Accelerator count** .

3.  Optional: [**Model Monitoring**](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/model-monitoring/overview) analysis for batch inferences is available in [Preview](https://cloud.google.com/products/#product-launch-stages) . See the [Prerequisites](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/model-monitoring/model-monitoring-batch-predictions#prerequisites) for adding skew detection configuration to your batch inference job.
    
    1.  Click to toggle on **Enable model monitoring for this batch prediction** .
    
    2.  Select a **Training data source** . Enter the data path or location for the training data source that you selected.
    
    3.  Optional: Under **Alert thresholds** , specify thresholds at which to trigger alerts.
    
    4.  For **Notification emails** , enter one or more comma-separated email addresses to receive alerts when a model exceeds an alerting threshold.
    
    5.  Optional: For **Notification channels** , add [Cloud Monitoring](https://docs.cloud.google.com/monitoring/support/notification-options) channels to receive alerts when a model exceeds an alerting threshold. You can select existing Cloud Monitoring channels or create a new one by clicking **Manage notification channels** . The Google Cloud console supports PagerDuty, Slack, and Pub/Sub notification channels.

4.  Click **Create** .

### API

Use the Agent Platform API to send batch inference requests. Select a tab depending on which tool you are using to get batch inferences.

### REST

Before using any of the request data, make the following replacements:

  - LOCATION\_ID : Region where Model is stored and batch prediction job is executed. For example, `us-central1` .

  - PROJECT\_ID : Your [project ID](https://docs.cloud.google.com/resource-manager/docs/creating-managing-projects#identifiers) .

  - BATCH\_JOB\_NAME : Display name for the batch prediction job.

  - MODEL\_ID : The ID for the model to use for making predictions.

  - INPUT\_FORMAT : The [format of your input data](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/get-batch-predictions#input_data_requirements) : `jsonl` , `csv` , `tf-record` , `tf-record-gzip` , or `file-list` .

  - INPUT\_URI : Cloud Storage URI of your input data. May contain wildcards.

  - OUTPUT\_DIRECTORY : Cloud Storage URI of a directory where you want Agent Platform to save output.

  - MACHINE\_TYPE : The [machine resources](https://docs.cloud.google.com/vertex-ai/docs/predictions/configure-compute) to be used for this batch prediction job.
    
    You can optionally [configure the `machineSpec` field](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/MachineSpec) to [use accelerators](https://docs.cloud.google.com/vertex-ai/docs/predictions/configure-compute#gpus) , but the following example does not demonstrate this.

  - BATCH\_SIZE : The number of instances to send in each prediction request; the default is 64. Increasing the batch size can lead to higher throughput, but it can also cause request timeouts.

  - STARTING\_REPLICA\_COUNT : The number of nodes for this batch prediction job.

HTTP method and URL:

    POST https://LOCATION_ID-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION_ID/batchPredictionJobs

Request JSON body:

    {
      "displayName": "BATCH_JOB_NAME",
      "model": "projects/PROJECT_ID/locations/LOCATION_ID/models/MODEL_ID",
      "inputConfig": {
        "instancesFormat": "INPUT_FORMAT",
        "gcsSource": {
          "uris": ["INPUT_URI"],
        },
      },
      "outputConfig": {
        "predictionsFormat": "jsonl",
        "gcsDestination": {
          "outputUriPrefix": "OUTPUT_DIRECTORY",
        },
      },
      "dedicatedResources" : {
        "machineSpec" : {
          "machineType": MACHINE_TYPE
        },
        "startingReplicaCount": STARTING_REPLICA_COUNT
      },
      "manualBatchTuningParameters": {
        "batch_size": BATCH_SIZE,
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
         "https://LOCATION_ID-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION_ID/batchPredictionJobs"

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
        -Uri "https://LOCATION_ID-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION_ID/batchPredictionJobs" | Select-Object -Expand Content

You should receive a JSON response similar to the following:

    {
      "name": "projects/PROJECT_NUMBER/locations/LOCATION_ID/batchPredictionJobs/BATCH_JOB_ID",
      "displayName": "BATCH_JOB_NAME 202005291958",
      "model": "projects/PROJECT_ID/locations/LOCATION_ID/models/MODEL_ID",
      "inputConfig": {
        "instancesFormat": "jsonl",
        "gcsSource": {
          "uris": [
            "INPUT_URI"
          ]
        }
      },
      "outputConfig": {
        "predictionsFormat": "jsonl",
        "gcsDestination": {
          "outputUriPrefix": "OUTPUT_DIRECTORY"
        }
      },
      "state": "JOB_STATE_PENDING",
      "createTime": "2020-05-30T02:58:44.341643Z",
      "updateTime": "2020-05-30T02:58:44.341643Z",
    }

### Java

Before trying this sample, follow the Java setup instructions in the [Agent Platform quickstart using client libraries](https://docs.cloud.google.com/vertex-ai/docs/start/client-libraries) . For more information, see the [Agent Platform Java API reference documentation](https://docs.cloud.google.com/java/docs/reference/google-cloud-aiplatform/latest/com.google.cloud.aiplatform.v1) .

To authenticate to Agent Platform, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

In the following sample, replace PREDICTIONS\_FORMAT with `jsonl` . To learn how to replace the other placeholders, see the `REST & CMD LINE` tab of this section.

    import com.google.cloud.aiplatform.util.ValueConverter;
    import com.google.cloud.aiplatform.v1.AcceleratorType;
    import com.google.cloud.aiplatform.v1.BatchDedicatedResources;
    import com.google.cloud.aiplatform.v1.BatchPredictionJob;
    import com.google.cloud.aiplatform.v1.GcsDestination;
    import com.google.cloud.aiplatform.v1.GcsSource;
    import com.google.cloud.aiplatform.v1.JobServiceClient;
    import com.google.cloud.aiplatform.v1.JobServiceSettings;
    import com.google.cloud.aiplatform.v1.LocationName;
    import com.google.cloud.aiplatform.v1.MachineSpec;
    import com.google.cloud.aiplatform.v1.ModelName;
    import com.google.protobuf.Value;
    import java.io.IOException;
    
    public class CreateBatchPredictionJobSample {
    
      public static void main(String[] args) throws IOException {
        // TODO(developer): Replace these variables before running the sample.
        String project = "PROJECT";
        String displayName = "DISPLAY_NAME";
        String modelName = "MODEL_NAME";
        String instancesFormat = "INSTANCES_FORMAT";
        String gcsSourceUri = "GCS_SOURCE_URI";
        String predictionsFormat = "PREDICTIONS_FORMAT";
        String gcsDestinationOutputUriPrefix = "GCS_DESTINATION_OUTPUT_URI_PREFIX";
        createBatchPredictionJobSample(
            project,
            displayName,
            modelName,
            instancesFormat,
            gcsSourceUri,
            predictionsFormat,
            gcsDestinationOutputUriPrefix);
      }
    
      static void createBatchPredictionJobSample(
          String project,
          String displayName,
          String model,
          String instancesFormat,
          String gcsSourceUri,
          String predictionsFormat,
          String gcsDestinationOutputUriPrefix)
          throws IOException {
        JobServiceSettings settings =
            JobServiceSettings.newBuilder()
                .setEndpoint("us-central1-aiplatform.googleapis.com:443")
                .build();
        String location = "us-central1";
    
        // Initialize client that will be used to send requests. This client only needs to be created
        // once, and can be reused for multiple requests. After completing all of your requests, call
        // the "close" method on the client to safely clean up any remaining background resources.
        try (JobServiceClient client = JobServiceClient.create(settings)) {
    
          // Passing in an empty Value object for model parameters
          Value modelParameters = ValueConverter.EMPTY_VALUE;
    
          GcsSource gcsSource = GcsSource.newBuilder().addUris(gcsSourceUri).build();
          BatchPredictionJob.InputConfig inputConfig =
              BatchPredictionJob.InputConfig.newBuilder()
                  .setInstancesFormat(instancesFormat)
                  .setGcsSource(gcsSource)
                  .build();
          GcsDestination gcsDestination =
              GcsDestination.newBuilder().setOutputUriPrefix(gcsDestinationOutputUriPrefix).build();
          BatchPredictionJob.OutputConfig outputConfig =
              BatchPredictionJob.OutputConfig.newBuilder()
                  .setPredictionsFormat(predictionsFormat)
                  .setGcsDestination(gcsDestination)
                  .build();
          MachineSpec machineSpec =
              MachineSpec.newBuilder()
                  .setMachineType("n1-standard-2")
                  .setAcceleratorType(AcceleratorType.NVIDIA_TESLA_T4)
                  .setAcceleratorCount(1)
                  .build();
          BatchDedicatedResources dedicatedResources =
              BatchDedicatedResources.newBuilder()
                  .setMachineSpec(machineSpec)
                  .setStartingReplicaCount(1)
                  .setMaxReplicaCount(1)
                  .build();
          String modelName = ModelName.of(project, location, model).toString();
          BatchPredictionJob batchPredictionJob =
              BatchPredictionJob.newBuilder()
                  .setDisplayName(displayName)
                  .setModel(modelName)
                  .setModelParameters(modelParameters)
                  .setInputConfig(inputConfig)
                  .setOutputConfig(outputConfig)
                  .setDedicatedResources(dedicatedResources)
                  .build();
          LocationName parent = LocationName.of(project, location);
          BatchPredictionJob response = client.createBatchPredictionJob(parent, batchPredictionJob);
          System.out.format("response: %s\n", response);
          System.out.format("\tName: %s\n", response.getName());
        }
      }
    }

### Python

To learn how to install or update the Vertex AI SDK for Python, see [Install the Vertex AI SDK for Python](https://docs.cloud.google.com/vertex-ai/docs/start/use-vertex-ai-python-sdk) . For more information, see the [Python API reference documentation](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest) .

    def create_batch_prediction_job_dedicated_resources_sample(
        project: str,
        location: str,
        model_resource_name: str,
        job_display_name: str,
        gcs_source: Union[str, Sequence[str]],
        gcs_destination: str,
        instances_format: str = "jsonl",
        machine_type: str = "n1-standard-2",
        accelerator_count: int = 1,
        accelerator_type: Union[str, aiplatform_v1.AcceleratorType] = "NVIDIA_TESLA_K80",
        starting_replica_count: int = 1,
        sync: bool = True,
    ):
        aiplatform.init(project=project, location=location)
    
        my_model = aiplatform.Model(model_resource_name)
    
        batch_prediction_job = my_model.batch_predict(
            job_display_name=job_display_name,
            gcs_source=gcs_source,
            gcs_destination_prefix=gcs_destination,
            instances_format=instances_format,
            machine_type=machine_type,
            accelerator_count=accelerator_count,
            accelerator_type=accelerator_type,
            starting_replica_count=starting_replica_count,
            sync=sync,
        )
    
        batch_prediction_job.wait()
    
        print(batch_prediction_job.display_name)
        print(batch_prediction_job.resource_name)
        print(batch_prediction_job.state)
        return batch_prediction_job

#### BigQuery

The preceding REST example uses Cloud Storage for the source and destination. To use BigQuery instead, make the following changes:

  - Change the `inputConfig` field to the following:
    
        "inputConfig": {
           "instancesFormat": "bigquery",
           "bigquerySource": {
              "inputUri": "bq://SOURCE_PROJECT_ID.SOURCE_DATASET_NAME.SOURCE_TABLE_NAME"
           }
        }

  - Change the `outputConfig` field to the following:
    
        "outputConfig": {
           "predictionsFormat":"bigquery",
           "bigqueryDestination":{
              "outputUri": "bq://DESTINATION_PROJECT_ID.DESTINATION_DATASET_NAME.DESTINATION_TABLE_NAME"
           }
         }

  - Replace the following:
    
      - `SOURCE_PROJECT_ID` : ID of the source Google Cloud project
      - `SOURCE_DATASET_NAME` : name of the source BigQuery dataset
      - `SOURCE_TABLE_NAME` : name of the BigQuery source table
      - `DESTINATION_PROJECT_ID` : ID of the destination Google Cloud project
      - `DESTINATION_DATASET_NAME` : name of the destination BigQuery dataset
      - `DESTINATION_TABLE_NAME` : name of the BigQuery destination table

#### Feature importance

If you want feature importance values returned for your inferences, set the `generateExplanation` property to `true` . Note that *forecasting* models don't support feature importance, so you can't include it in your batch inference requests.

Feature importance, sometimes called *feature attributions* , is part of [Vertex Explainable AI](https://docs.cloud.google.com/vertex-ai/docs/explainable-ai/overview) .

You can only set `generateExplanation` to `true` if you have [configured your `Model` for explanations](https://docs.cloud.google.com/vertex-ai/docs/explainable-ai/configuring-explanations) or if you specify the `BatchPredictionJob` 's [`explanationSpec` field](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.batchPredictionJobs#BatchPredictionJob.FIELDS.explanation_spec) .

### Choose machine type and replica count

Scaling horizontally by increasing the number of replicas improves throughput more linearly and predictably than by using larger machine types.

In general, we recommend that you specify the smallest machine type possible for your job and increase the number of replicas.

For cost-effectiveness, we recommend that you choose the replica count such that your batch inference job runs for at least 10 minutes. This is because you are billed per replica node hour, which includes the approximately 5 minutes it takes for each replica to start up. It isn't cost-effective to process for only a few seconds and then shut down.

As general guidance, for thousands of instances, we recommend a `starting_replica_count` in the tens. For millions of instances, we recommend a `starting_replica_count` in the hundreds. You can also use the following formula to estimate the number of replicas:

`N / (T * (60 / Tb))`

Where:

  - **N:** The number of batches in the job. For example, 1 million instances / 100 batch size = 10,000 batches.
  - **T** : The expected time for the batch inference job. For example, 10 minutes.
  - **Tb** : The time in seconds it takes for a replica to process a single batch. For example, 1 second per batch on a 2-core machine type.

In our example, 10,000 batches / (10 minutes \* (60 / 1s)) rounds up to 17 replicas.

These recommendations are all approximate guidelines. They don't necessarily give optimal throughput for every model. They don't provide exact estimates of processing time and cost. And they don't necessarily capture the best cost-versus-throughput tradeoffs for each scenario. Use them as a reasonable starting point and adjust them as necessary. To measure characteristics such as throughput for your model, run the [Finding ideal machine type](https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/community/vertex_endpoints/find_ideal_machine_type/find_ideal_machine_type.ipynb) notebook.

#### For GPU- or TPU-accelerated machines

Follow the preceding guidelines (which also apply to CPU-only models), with the following additional considerations:

  - You might need more CPUs and GPUs (for example, for data preprocessing).
  - GPU machine types take more time to startup (10 minutes), so you may want to target longer times (for example, at least 20 minutes instead of 10 minutes) for the batch inference job so that a reasonable proportion of the time and cost is spent on generating inferences.

### Retrieve batch inference results

When a batch inference task is complete, the output of the inference is stored in the Cloud Storage bucket or BigQuery location that you specified in your request.

### Example batch inference result

The output folder contains a set of JSON Lines files.

The files are named `{gcs_path}/prediction.results-{file_number}-of-{number_of_files_generated}` . The number of files is nondeterministic, due to the distributed nature of batch inference.

Each line in the file corresponds to an instance from the input and has the following key-value pairs:

  - `prediction` : contains the value returned by the container.
  - `instance` : For a file list, contains the Cloud Storage URI. For all other input formats, contains the value that was sent to the container in the HTTP request body.

#### Example 1

If the HTTP request contains:

    {
      "instances": [
        [1, 2, 3, 4],
        [5, 6, 7, 8]
    ]}

And the container returns:

    {
      "predictions": [
        [0.1,0.9],
        [0.7,0.3]
      ],
    }

Then the JSON Lines output file is:

    { "instance": [1, 2, 3, 4], "prediction": [0.1,0.9]}
    { "instance": [5, 6, 7, 8], "prediction": [0.7,0.3]}

#### Example 2

If the HTTP request contains:

    {
      "instances": [
        {"values": [1, 2, 3, 4], "key": 1},
        {"values": [5, 6, 7, 8], "key": 2}
    ]}

And the container returns:

    {
      "predictions": [
        {"result":1},
        {"result":0}
      ],
    }

Then the JSON Lines output file is:

    { "instance": {"values": [1, 2, 3, 4], "key": 1}, "prediction": {"result":1}}
    { "instance": {"values": [5, 6, 7, 8], "key": 2}, "prediction": {"result":0}}

### User-facing endpoint

> **Preview — User-facing endpoints for batch inference**
> 
> This feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](https://docs.cloud.google.com/terms/service-terms#1) . Pre-GA features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

To improve observability and reduce the number of quotas to manage, the model server is available as a user-facing Agent Platform endpoint. Configuring any of the following features will result in the model being deployed to a user-facing endpoint:

  - Shared reservations
  - Spot VMs
  - Flex-start VMs

## Use Explainable AI

We don't recommend running [feature-based explanations](https://docs.cloud.google.com/vertex-ai/docs/explainable-ai/overview#feature-based) on a large amount of data. This is because each input can potentially fan out to thousands of requests based on the set of possible feature values which may result in massively increased processing time and cost. In general, a small dataset is enough to understand feature importance.

Batch inference does not support [example-based explanations](https://docs.cloud.google.com/vertex-ai/docs/explainable-ai/overview#example-based) .

## Notebooks

> To learn more, run the "Custom model batch prediction with feature filtering" notebook in one of the following environments:
> 
> [![](https://docs.cloud.google.com/static/vertex-ai/images/colab-logo-32px.png) Open in Colab](https://colab.research.google.com/github/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/prediction/custom_batch_prediction_feature_filter.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/colab-enterprise-logo-32px.png) Open in Colab Enterprise](https://console.cloud.google.com/vertex-ai/colab/import/https%3A%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Fprediction%2Fcustom_batch_prediction_feature_filter.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/vertex-ai-workbench-logo-32px.png) Open in Vertex AI Workbench](https://console.cloud.google.com/vertex-ai/workbench/deploy-notebook?download_url=https%3A%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Fprediction%2Fcustom_batch_prediction_feature_filter.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/github-logo-32px.png) View on GitHub](https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/prediction/custom_batch_prediction_feature_filter.ipynb)

## What's next

  - Learn about [Compute resources for inference](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/configure-compute) .
  - Learn how to [use reservations with Agent Platform batch inference](https://docs.cloud.google.com/vertex-ai/docs/predictions/use-reservations-batch) .
