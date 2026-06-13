---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tabular-data/classification-regression/get-batch-predictions
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tabular-data/classification-regression/get-batch-predictions
title: Get batch inferences for AutoML models
description: Make a batch inference request to a AutoML classification or regression model in Agent Platform.
data_source: docs.cloud.google.com
---

This page shows you how to make a batch inference request to your trained AutoML classification or regression model using the Google Cloud console or the Agent Platform API.

A batch inference request is an asynchronous request (as opposed to [online inference](https://docs.cloud.google.com/vertex-ai/docs/tabular-data/classification-regression/get-online-predictions) , which is a synchronous request). Request batch inferences directly from the model resource without deploying the model to an endpoint. For tabular data, use batch inferences when you don't require an immediate response and want to process accumulated data by using a single request.

To make a batch inference request, specify an input source and an output format where Gemini Enterprise Agent Platform stores inference results.

> **Note:** To minimize processing time when you use the Google Cloud console to create batch inferences, select input and output locations that are in the same region as your model. If you use the API to create batch inferences, send requests to a service endpoint (such as `https://us-central1-aiplatform.googleapis.com` ) that is in the same region or geographically close to your input and output locations.

## Before you begin

Before you make a batch inference request, you must first [train](https://docs.cloud.google.com/vertex-ai/docs/tabular-data/classification-regression/train-model) an AutoML model.

## Input data

The input data for batch inference requests is the data that your model uses to make inferences. For classification or regression models, you can provide input data in one of the following formats:

  - BigQuery tables
  - CSV objects in Cloud Storage

We recommend that you use the same format for your input data as you used for training the model. For example, if you trained your model using data in BigQuery, it is best to use a BigQuery table as the input for your batch inference. Because Gemini Enterprise Agent Platform treats all CSV input fields as strings, mixing training and input data formats may cause errors.

Your data source must contain tabular data that includes all of the columns, in any order, that were used to train the model. You can include columns that were not in the training data, or that were in the training data but excluded from use for training. These extra columns are included in the output but don't affect the inference results.

### Input data requirements

### BigQuery table

If you choose a BigQuery table as the input, you must ensure the following:

  - BigQuery data source tables must be no larger than 100 GB.
  - If the table is in a different project, you must grant the `BigQuery Data Editor` role to the Agent Platform service account in that project.

### CSV file

If you choose a CSV object in Cloud Storage as the input, you must ensure the following:

  - The data source must begin with a header row with the column names.
  - Each data source object must not be larger than 10 GB. You can include multiple files, up to a maximum amount of 100 GB.
  - If the Cloud Storage bucket is in a different project, you must grant the `Storage Object Creator` role to the Agent Platform service account in that project.
  - You must enclose all strings in double quotation marks (").

## Output format

The output format of your batch inference request doesn't need to be the same as the input format. For example, if you used BigQuery table as the input, you can output the results to a CSV object in Cloud Storage.

## Make a batch inference request to your model

To make batch inference requests to an AutoML model, you can use the Google Cloud console or the Agent Platform API. The input data source can be CSV objects stored in a Cloud Storage bucket or BigQuery tables. Depending on the amount of data that you submit as input, a batch inference task can take some time to complete.

### Google Cloud console

Use the Google Cloud console to request a batch inference.

1.  In the Google Cloud console, in the Agent Platform section, go to the **Batch inference** page.
2.  Click **Create** to open the **New batch inference** window.
3.  For **Define your batch inference** , complete the following steps:
    1.  Enter a name for the batch inference.
    2.  For **Model name** , select the name of the model to use for this batch inference.
    3.  For **Version** , select the model version to use for this batch inference.
    4.  For **Select source** , select whether your source input data is a CSV file on Cloud Storage or a table in BigQuery.
          - For CSV files, specify the Cloud Storage location where your CSV input file is located.
          - For BigQuery tables, specify the project ID where the table is located, the BigQuery dataset ID, and the BigQuery table or view ID.
    5.  For the **Output** , select **CSV** or **BigQuery** .
          - For CSV, specify the Cloud Storage bucket where Gemini Enterprise Agent Platform stores your output.
        
          - For BigQuery, you can specify a project ID or an existing dataset:
            
              - To specify the project ID, enter the project ID in the **Google Cloud project ID** field. Gemini Enterprise Agent Platform creates a new output dataset for you.
              - To specify an existing dataset, enter its BigQuery path in the **Google Cloud project ID** field, such as `bq://projectid.datasetid` .
        
          - **Optional** . You can request an inference with explanations (also called feature attributions) to see how your model arrived at an inference. The local feature importance values tell you how much each feature contributed to the inference result. Feature attributions are included in Agent Platform inferences through [Vertex Explainable AI](https://docs.cloud.google.com/vertex-ai/docs/tabular-data/classification-explanations) .  
            
            To enable feature attributions, select **Enable feature attributions for this model** . This option is available if your output destination is BigQuery or JSONL on Cloud Storage. Feature attributions are not supported for CSV on Cloud Storage.
4.  Optional: [**Model Monitoring**](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/model-monitoring/overview) analysis for batch inferences is available in [Preview](https://cloud.google.com/products/#product-launch-stages) . See the [Prerequisites](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/model-monitoring/model-monitoring-batch-predictions#prerequisites) for adding skew detection configuration to your batch inference job.
    1.  Click to toggle on **Enable model monitoring for this batch inference** .
    2.  Select a **Training data source** . Enter the data path or location for the training data source that you selected.
    3.  Optional: Under **Alert thresholds** , specify thresholds at which to trigger alerts.
    4.  For **Notification emails** , enter one or more comma-separated email addresses to receive alerts when a model exceeds an alerting threshold.
    5.  Optional: For **Notification channels** , add [Cloud Monitoring](https://docs.cloud.google.com/monitoring/support/notification-options) channels to receive alerts when a model exceeds an alerting threshold. You can select existing Cloud Monitoring channels or create a new one by clicking **Manage notification channels** . The Console supports PagerDuty, Slack, and Pub/Sub notification channels.
5.  Click **Create** .

### API: BigQuery

### REST

You use the [batchPredictionJobs.create](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.batchPredictionJobs/create) method to request a batch prediction.

Before using any of the request data, make the following replacements:

  - LOCATION\_ID : Region where Model is stored and batch inference job is executed. For example, `us-central1` .

  - PROJECT\_ID : Your \[project ID\](/resource-manager/docs/creating-managing-projects\#identifiers).

  - BATCH\_JOB\_NAME : Display name for the batch job

  - MODEL\_ID : The ID for the model to use for making inferences

  - INPUT\_URI : Reference to the BigQuery data source. In the form:
    
        bq://bqprojectId.bqDatasetId.bqTableId

  - OUTPUT\_URI : Reference to the BigQuery destination (where the inferences are written). Specify the project ID and, **optionally** , an existing dataset ID. If you specify just the project ID, Agent Platform creates a new output dataset for you. Use the following form:
    
        bq://bqprojectId.bqDatasetId

  - MACHINE\_TYPE : The machine resources to be used for this batch inference job. [Learn more](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/configure-compute) .

  - STARTING\_REPLICA\_COUNT : The starting number of nodes for this batch inference job. The node count can be increased or decreased as required by load, up to the maximum number of nodes, but will never fall below this number.

  - MAX\_REPLICA\_COUNT : The maximum number of nodes for this batch inference job. The node count can be increased or decreased as required by load, but will never exceed the maximum. Optional, defaults to 10.

  - GENERATE\_EXPLANATION : You can request an inference with explanations (also called feature attributions) to see how your model arrived at an inference. The local feature importance values tell you how much each feature contributed to the inference result. Feature attributions are included in Agent Platform inferences through [Vertex Explainable AI](https://docs.cloud.google.com/vertex-ai/docs/tabular-data/classification-explanations) .  
    
    Default value is *false* . Set to *true* to enable feature attributions.

HTTP method and URL:

    POST https://LOCATION_ID-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION_ID/batchPredictionJobs

Request JSON body:

    {
      "displayName": "BATCH_JOB_NAME",
      "model": "MODEL_ID",
      "inputConfig": {
        "instancesFormat": "bigquery",
        "bigquerySource": {
          "inputUri": "INPUT_URI"
        }
      },
      "outputConfig": {
        "predictionsFormat": "bigquery",
        "bigqueryDestination": {
          "outputUri": "OUTPUT_URI"
        }
      },
      "dedicatedResources": {
        "machineSpec": {
          "machineType": "MACHINE_TYPE",
          "acceleratorCount": "0"
        },
        "startingReplicaCount": STARTING_REPLICA_COUNT,
        "maxReplicaCount": MAX_REPLICA_COUNT
      },
    
      "generateExplanation": GENERATE_EXPLANATION
    
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
      "name": "projects/PROJECT_ID/locations/LOCATION_ID/batchPredictionJobs/67890",
      "displayName": "batch_job_1 202005291958",
      "model": "projects/12345/locations/us-central1/models/5678",
      "state": "JOB_STATE_PENDING",
      "inputConfig": {
        "instancesFormat": "bigquery",
        "bigquerySource": {
          "inputUri": "INPUT_URI"
        }
      },
      "outputConfig": {
        "predictionsFormat": "bigquery",
        "bigqueryDestination": {
            "outputUri": bq://12345
        }
      },
      "dedicatedResources": {
        "machineSpec": {
          "machineType": "n1-standard-32",
          "acceleratorCount": "0"
        },
        "startingReplicaCount": 2,
        "maxReplicaCount": 6
      },
      "manualBatchTuningParameters": {
        "batchSize": 4
      },
      "generateExplanation": false,
      "outputInfo": {
        "bigqueryOutputDataset": "bq://12345.reg_model_2020_10_02_06_04
      }
      "state": "JOB_STATE_PENDING",
      "createTime": "2020-09-30T02:58:44.341643Z",
      "updateTime": "2020-09-30T02:58:44.341643Z",
    }

### Java

Before trying this sample, follow the Java setup instructions in the [Agent Platform quickstart using client libraries](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/start/client-libraries) .

To authenticate to Agent Platform, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

In the following sample, replace INSTANCES\_FORMAT and PREDICTIONS\_FORMAT with \`bigquery\`. To learn how to replace the other placeholders, see the \`REST & CMD LINE\` tab of this section.

    import com.google.cloud.aiplatform.v1.BatchPredictionJob;
    import com.google.cloud.aiplatform.v1.BigQueryDestination;
    import com.google.cloud.aiplatform.v1.BigQuerySource;
    import com.google.cloud.aiplatform.v1.JobServiceClient;
    import com.google.cloud.aiplatform.v1.JobServiceSettings;
    import com.google.cloud.aiplatform.v1.LocationName;
    import com.google.cloud.aiplatform.v1.ModelName;
    import com.google.gson.JsonObject;
    import com.google.protobuf.Value;
    import com.google.protobuf.util.JsonFormat;
    import java.io.IOException;
    
    public class CreateBatchPredictionJobBigquerySample {
    
      public static void main(String[] args) throws IOException {
        // TODO(developer): Replace these variables before running the sample.
        String project = "PROJECT";
        String displayName = "DISPLAY_NAME";
        String modelName = "MODEL_NAME";
        String instancesFormat = "INSTANCES_FORMAT";
        String bigquerySourceInputUri = "BIGQUERY_SOURCE_INPUT_URI";
        String predictionsFormat = "PREDICTIONS_FORMAT";
        String bigqueryDestinationOutputUri = "BIGQUERY_DESTINATION_OUTPUT_URI";
        createBatchPredictionJobBigquerySample(
            project,
            displayName,
            modelName,
            instancesFormat,
            bigquerySourceInputUri,
            predictionsFormat,
            bigqueryDestinationOutputUri);
      }
    
      static void createBatchPredictionJobBigquerySample(
          String project,
          String displayName,
          String model,
          String instancesFormat,
          String bigquerySourceInputUri,
          String predictionsFormat,
          String bigqueryDestinationOutputUri)
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
          JsonObject jsonModelParameters = new JsonObject();
          Value.Builder modelParametersBuilder = Value.newBuilder();
          JsonFormat.parser().merge(jsonModelParameters.toString(), modelParametersBuilder);
          Value modelParameters = modelParametersBuilder.build();
          BigQuerySource bigquerySource =
              BigQuerySource.newBuilder().setInputUri(bigquerySourceInputUri).build();
          BatchPredictionJob.InputConfig inputConfig =
              BatchPredictionJob.InputConfig.newBuilder()
                  .setInstancesFormat(instancesFormat)
                  .setBigquerySource(bigquerySource)
                  .build();
          BigQueryDestination bigqueryDestination =
              BigQueryDestination.newBuilder().setOutputUri(bigqueryDestinationOutputUri).build();
          BatchPredictionJob.OutputConfig outputConfig =
              BatchPredictionJob.OutputConfig.newBuilder()
                  .setPredictionsFormat(predictionsFormat)
                  .setBigqueryDestination(bigqueryDestination)
                  .build();
          String modelName = ModelName.of(project, location, model).toString();
          BatchPredictionJob batchPredictionJob =
              BatchPredictionJob.newBuilder()
                  .setDisplayName(displayName)
                  .setModel(modelName)
                  .setModelParameters(modelParameters)
                  .setInputConfig(inputConfig)
                  .setOutputConfig(outputConfig)
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

In the following sample, set the \`instances\_format\` and \`predictions\_format\` parameters to \`"bigquery"\`. To learn how to set the other parameters, see the \`REST & CMD LINE\` tab of this section.

    from google.cloud import aiplatform_v1beta1
    from google.protobuf import json_format
    from google.protobuf.struct_pb2 import Value
    
    
    def create_batch_prediction_job_bigquery_sample(
        project: str,
        display_name: str,
        model_name: str,
        instances_format: str,
        bigquery_source_input_uri: str,
        predictions_format: str,
        bigquery_destination_output_uri: str,
        location: str = "us-central1",
        api_endpoint: str = "us-central1-aiplatform.googleapis.com",
    ):
        # The AI Platform services require regional API endpoints.
        client_options = {"api_endpoint": api_endpoint}
        # Initialize client that will be used to create and send requests.
        # This client only needs to be created once, and can be reused for multiple requests.
        client = aiplatform_v1beta1.JobServiceClient(client_options=client_options)
        model_parameters_dict = {}
        model_parameters = json_format.ParseDict(model_parameters_dict, Value())
    
        batch_prediction_job = {
            "display_name": display_name,
            # Format: 'projects/{project}/locations/{location}/models/{model_id}'
            "model": model_name,
            "model_parameters": model_parameters,
            "input_config": {
                "instances_format": instances_format,
                "bigquery_source": {"input_uri": bigquery_source_input_uri},
            },
            "output_config": {
                "predictions_format": predictions_format,
                "bigquery_destination": {"output_uri": bigquery_destination_output_uri},
            },
            # optional
            "generate_explanation": True,
        }
        parent = f"projects/{project}/locations/{location}"
        response = client.create_batch_prediction_job(
            parent=parent, batch_prediction_job=batch_prediction_job
        )
        print("response:", response)

### API: Cloud Storage

### REST

You use the [batchPredictionJobs.create](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.batchPredictionJobs/create) method to request a batch inference.

Before using any of the request data, make the following replacements:

  - LOCATION\_ID : Region where Model is stored and batch inference job is executed. For example, `us-central1` .

  - PROJECT\_ID :

  - BATCH\_JOB\_NAME : Display name for the batch job

  - MODEL\_ID : The ID for the model to use for making inferences

  - URI : Paths (URIs) to the Cloud Storage buckets containing the training data. There can be more than one. Each URI has the form:
    
        gs://bucketName/pathToFileName

  - OUTPUT\_URI\_PREFIX : Path to a Cloud Storage destination where the inferences are written. Agent Platform writes batch inferences to a timestamped subdirectory of this path. Set this value to a string with the following format:
    
        gs://bucketName/pathToOutputDirectory

  - MACHINE\_TYPE : The machine resources to be used for this batch inference job. [Learn more](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/configure-compute) .

  - STARTING\_REPLICA\_COUNT : The starting number of nodes for this batch inference job. The node count can be increased or decreased as required by load, up to the maximum number of nodes, but will never fall below this number.

  - MAX\_REPLICA\_COUNT : The maximum number of nodes for this batch inference job. The node count can be increased or decreased as required by load, but will never exceed the maximum. Optional, defaults to 10.

  - GENERATE\_EXPLANATION : You can request an inference with explanations (also called feature attributions) to see how your model arrived at an inference. The local feature importance values tell you how much each feature contributed to the inference result. Feature attributions are included in Agent Platform inferences through [Vertex Explainable AI](https://docs.cloud.google.com/vertex-ai/docs/tabular-data/classification-explanations) .  
    
    Default value is *false* . Set to *true* to enable feature attributions. This option is available only if your output destination is JSONL. Feature attributions are not supported for CSV on Cloud Storage.

HTTP method and URL:

    POST https://LOCATION_ID-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION_ID/batchPredictionJobs

Request JSON body:

    {
      "displayName": "BATCH_JOB_NAME",
      "model": "MODEL_ID",
      "inputConfig": {
        "instancesFormat": "csv",
        "gcsSource": {
          "uris": [
            URI1,...
          ]
        },
      },
      "outputConfig": {
        "predictionsFormat": "csv",
        "gcsDestination": {
          "outputUriPrefix": "OUTPUT_URI_PREFIX"
        }
      },
      "dedicatedResources": {
        "machineSpec": {
          "machineType": "MACHINE_TYPE",
          "acceleratorCount": "0"
        },
        "startingReplicaCount": STARTING_REPLICA_COUNT,
        "maxReplicaCount": MAX_REPLICA_COUNT
      },
    
      "generateExplanation": GENERATE_EXPLANATION
    
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
      "name": "projects/PROJECT__ID/locations/LOCATION_ID/batchPredictionJobs/67890",
      "displayName": "batch_job_1 202005291958",
      "model": "projects/12345/locations/us-central1/models/5678",
      "state": "JOB_STATE_PENDING",
      "inputConfig": {
        "instancesFormat": "csv",
        "gcsSource": {
          "uris": [
            "gs://bp_bucket/reg_mode_test"
          ]
        }
      },
      "outputConfig": {
        "predictionsFormat": "csv",
        "gcsDestination": {
          "outputUriPrefix": "OUTPUT_URI_PREFIX"
        }
      },
      "dedicatedResources": {
        "machineSpec": {
          "machineType": "n1-standard-32",
          "acceleratorCount": "0"
        },
        "startingReplicaCount": 2,
        "maxReplicaCount": 6
      },
      "manualBatchTuningParameters": {
        "batchSize": 4
      }
      "outputInfo": {
        "gcsOutputDataset": "OUTPUT_URI_PREFIX/prediction-batch_job_1 202005291958-2020-09-30T02:58:44.341643Z"
      }
      "state": "JOB_STATE_PENDING",
      "createTime": "2020-09-30T02:58:44.341643Z",
      "updateTime": "2020-09-30T02:58:44.341643Z",
    }

## Retrieve batch inference results

Gemini Enterprise Agent Platform sends the output of batch inferences to the destination that you specified, which can be either BigQuery or Cloud Storage.

### BigQuery

*Output dataset*

If you are using BigQuery, the output of batch inference is stored in an output dataset. If you had provided a dataset to Gemini Enterprise Agent Platform, the name of the dataset ( BQ\_DATASET\_NAME ) is the name you had provided earlier. If you didn't provide an output dataset, Gemini Enterprise Agent Platform created one for you. You can find its name ( BQ\_DATASET\_NAME ) with the following steps:

1.  In the Google Cloud console, go to the Gemini Enterprise Agent Platform **Batch inference** page.  
2.  Select the inference you created.
3.  The output dataset is given in **Export location** . The dataset name is formatted as follows: ` prediction_ MODEL_NAME _ TIMESTAMP  `

*Output tables*

The output dataset contains one or more of the following three output tables:

  - Predictions table  
    
    This table contains a row for every row in your input data where an inference was requested (that is, where TARGET\_COLUMN\_NAME = null).

  - Errors table  
    
    This table contains a row for each non-critical error encountered during batch inference. Each non-critical error corresponds with a row in the input data that Agent Platform could not return a forecast for.

*Predictions table*

The name of the table ( BQ\_PREDICTIONS\_TABLE\_NAME ) is formed by appending \`predictions\_\` with the timestamp of when the batch inference job started: ` predictions_ TIMESTAMP  `

To retrieve inferences, go to the BigQuery page.

The format of the query depends on your model type:

**Classification:**

```sql
SELECT predicted_TARGET_COLUMN_NAME.classes AS classes,
predicted_TARGET_COLUMN_NAME.scores AS scores
FROM BQ_DATASET_NAME.BQ_PREDICTIONS_TABLE_NAME
```

`classes` is the list of potential classes, and `scores` are the corresponding confidence scores.

**Regression:**

    SELECT predicted_TARGET_COLUMN_NAME.value,
    predicted_TARGET_COLUMN_NAME.lower_bound,
    predicted_TARGET_COLUMN_NAME.upper_bound
    FROM BQ_DATASET_NAME.BQ_PREDICTIONS_TABLE_NAME

If you enabled feature attributions, you can find them in the predictions table as well. To access attributions for a feature BQ\_FEATURE\_NAME , run the following query:

```sql
SELECT explanation.attributions[OFFSET(0)].featureAttributions.BQ_FEATURE_NAME FROM BQ_DATASET_NAME.BQ_PREDICTIONS_TABLE_NAME
  
```

*Errors table*

The name of the table ( BQ\_ERRORS\_TABLE\_NAME ) is formed by appending `errors_` with the timestamp of when the batch inference job started: ` errors_ TIMESTAMP  ` To retrieve the errors validation table:

1.  In the console, go to the BigQuery page.

2.  Run the following query:
    
    ```sql
    SELECT * FROM BQ_DATASET_NAME.BQ_ERRORS_TABLE_NAME
          
    ```

The errors are stored in the following columns:

  - errors\_ TARGET\_COLUMN\_NAME .code
  - errors\_ TARGET\_COLUMN\_NAME .message

### Cloud Storage

If you specified Cloud Storage as your output destination, the results of your batch inference request are returned as CSV objects in a new folder in the bucket you specified. The name of the folder is the name of your model, prepended with "prediction-" and appended with the timestamp of when the batch inference job started. You can find the Cloud Storage folder name in the **Batch predictions** tab for your model.

The Cloud Storage folder contains two kinds of objects:

  - **Prediction objects**
    
    The inference objects are named \`predictions\_1.csv\`, \`predictions\_2.csv\`, and so on. They contain a header row with the column names, and a row for every inference returned. In the inference objects, Agent Platform returns your inference data and creates one or more new columns for the inference results based on your model type:
    
      - **Classification** : For each potential value of your target column, a column named `  TARGET_COLUMN_NAME _ VALUE _score ` is added to the results. This column contains the score, or confidence estimate, for that value.
      - **Regression** : The predicted value for that row is returned in a column named ` predicted_ TARGET_COLUMN_NAME  ` . The prediction interval is not returned for CSV output.

  - **Error objects**
    
    The error objects are named \`errors\_1.csv\`, \`errors\_2.csv\`, and so on. They contain a header row, and a row for every row in your input data that Agent Platform could not return an inference (for example, if a non-nullable feature was null) for.

Note: If the results are large, it is split into multiple objects.

Feature attributions are not available for batch inference results returned in Cloud Storage.

## Interpret inference results

### Classification

Classification models return a confidence score.

The confidence score communicates how strongly your model associates each class or label with a test item. The higher the number, the higher the model's confidence that the label should be applied to that item. You decide how high the confidence score must be for you to accept the model's results.

### Regression

Regression models return an inference value. For BigQuery destinations, they also return a inference interval. The inference interval provides a range of values that the model has 95% confidence contain the actual result.

## Interpret explanation results

If your batch inference results are stored in BigQuery and you chose to enable feature attributions, you can find the feature attribution values in the inferences table.

To calculate local feature importance, first the *baseline inference score* is calculated. Baseline values are computed from the training data, using the median value for numeric features and the mode for categorical features. The inference generated from the baseline values is the *baseline inference score* . Baseline values are calculated once for a model and do not change.

For a specific inference, the local feature importance for each feature tells you how much that feature added to or subtracted from the result as compared with the baseline inference score. The sum of all of the feature importance values equals the difference between the baseline inference score and the inference result.

For classification models, the score is always between 0.0 and 1.0, inclusive. Therefore, local feature importance values for classification models are always between -1.0 and 1.0 (inclusive).

For examples of feature attribution queries and to learn more, see [Feature Attributions for Classification and Regression](https://docs.cloud.google.com/vertex-ai/docs/tabular-data/classification-explanations) .

## What's next

  - Learn how to [export your model](https://docs.cloud.google.com/vertex-ai/docs/export/export-model-tabular) .
