---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/get-batch-model-garden
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/get-batch-model-garden
title: Get batch predictions from a self-deployed Model Garden model
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

> **Preview**
> 
> This feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](https://docs.cloud.google.com/terms/service-terms#1) . Pre-GA features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

Some of the models that are available in [Model Garden](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/model-garden/explore-models) can be self-deployed in your own Google Cloud project and used to provide batch predictions. Batch predictions let you efficiently use a model to process multiple text-only prompts that aren't latency sensitive.

## Prepare input

Before you begin, prepare your inputs in a BigQuery table or as a JSONL file in Cloud Storage. The input for both sources must follow the [OpenAI API schema](https://platform.openai.com/docs/api-reference/fine-tuning/chat-input) JSON format, as shown in the following example:

    {"body": {"messages": [{"role": "user", "content": "Give me a recipe for banana bread"}], "max_tokens": 1000}}

> **Note:** Gemini Enterprise Agent Platform doesn't use the `custom_id` , `method` , `url` , and `model` fields. You can include them, but they are ignored by the batch prediction job.

### BigQuery

Your BigQuery input table must adhere to the following schema:

| Column name | Description                                                |
| ----------- | ---------------------------------------------------------- |
| custom\_id  | An ID for each request to match the input with the output. |
| method      | The request method.                                        |
| url         | The request endpoint.                                      |
| body(JSON)  | Your input prompt.                                         |

  - Your input table can have other columns, which are ignored by the batch job and passed directly to the output table.
  - Batch prediction jobs reserve two column names for the batch prediction output: **response(JSON)** and **id** . Don't use these columns in the input table.
  - The **method** and **url** columns are dropped and not included in the output table.

### Cloud Storage

For Cloud Storage, the input file must be a JSONL file that is located in a Cloud Storage bucket.

## Get the required resources for a model

Choose a model and query its resource requirements. The required resources appear in the response, in the `dedicatedResources` field, which you specify in the configuration of your batch prediction job.

### REST

After you set up your environment, you can use REST to test a text prompt. The following sample sends a request to the publisher model endpoint.

Before using any of the request data, make the following replacements:

  - PUBLISHER : The model publisher, for example, `meta` , `google` , `mistral-ai` , or `deepseek-ai` .
  - PUBLISHER\_MODEL\_ID : The publisher's model ID for the model, for example, `llama3_1` .
  - VERSION\_ID : The publisher's version ID for the model, for example, `llama-3.1-8b-instruct` .

HTTP method and URL:

    GET "https://us-central1-aiplatform.googleapis.com/ui/publishers/PUBLISHER/models/PUBLISHER_MODEL_ID@VERSION_ID" | jq '.supportedActions.multiDeployVertex'

To send your request, choose one of these options:

#### curl

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) , or by using [Cloud Shell](https://docs.cloud.google.com/shell/docs) , which automatically logs you into the `gcloud` CLI . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Execute the following command:

    curl -X GET \
         -H "Authorization: Bearer $(gcloud auth print-access-token)" \
         -H "x-goog-user-project: PROJECT_ID" \
         ""https://us-central1-aiplatform.googleapis.com/ui/publishers/PUBLISHER/models/PUBLISHER_MODEL_ID@VERSION_ID" | jq '.supportedActions.multiDeployVertex'"

#### PowerShell

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Execute the following command:

    $cred = gcloud auth print-access-token
    $headers = @{ "Authorization" = "Bearer $cred"; "x-goog-user-project" = "PROJECT_ID" }
    
    Invoke-WebRequest `
        -Method GET `
        -Headers $headers `
        -Uri ""https://us-central1-aiplatform.googleapis.com/ui/publishers/PUBLISHER/models/PUBLISHER_MODEL_ID@VERSION_ID" | jq '.supportedActions.multiDeployVertex'" | Select-Object -Expand Content

You should receive a successful status code (2xx) and an empty response.

## Request a batch prediction

Make a batch prediction against a self-deployed Model Garden model by using input from BigQuery or Cloud Storage. You can independently choose to output predictions to either a BigQuery table or a JSONL file in a Cloud Storage bucket.

### BigQuery

Specify your BigQuery input table, model, and output location. The batch prediction job and your table must be in the same region.

### REST

After you set up your environment, you can use REST to test a text prompt. The following sample sends a request to the publisher model endpoint.

Before using any of the request data, make the following replacements:

  - LOCATION : A region that supports Model Garden self-deployed models.
  - PROJECT\_ID : Your \[project ID\](/resource-manager/docs/creating-managing-projects\#identifiers). .
  - MODEL : The name of the [model](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/get-batch-model-garden#models) to tune, for example, `llama-3.1-8b-instruct` .
  - PUBLISHER : The model publisher, for example, `meta` , `google` , `mistral-ai` , or `deepseek-ai` .
  - INPUT\_URI : The BigQuery table where your batch prediction input is located such as `myproject.mydataset.input_table` .
  - OUTPUT\_FORMAT : To output to a BigQuery table, specify `bigquery` . To output to a Cloud Storage bucket, specify `jsonl` .
  - DESTINATION : For BigQuery, specify `bigqueryDestination` . For Cloud Storage, specify `gcsDestination` .
  - OUTPUT\_URI\_FIELD\_NAME : For BigQuery, specify `outputUri` . For Cloud Storage, specify `outputUriPrefix` .
  - OUTPUT\_URI : For BigQuery, specify the table location such as `myproject.mydataset.output_result` . For Cloud Storage, specify the bucket and folder location such as `gs://mybucket/path/to/outputfile` .
  - MACHINE\_TYPE : Defines the set of resources to deploy for your model, for example, `g2-standard-4` .
  - ACC\_TYPE : Specifies accelerators to add to your batch prediction job to help improve performance when working with intensive workloads, for example, `NVIDIA_L4` .
  - ACC\_COUNT : The number of accelerators to use in your batch prediction job.

HTTP method and URL:

    POST https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/batchPredictionJobs

Request JSON body:

    '{
      "displayName": "JOB_NAME",
      "model": "publishers/PUBLISHER/models/MODEL",
      "inputConfig": {
        "instancesFormat":"bigquery",
        "bigquerySource":{
          "inputUri" : "INPUT_URI"
        }
      },
      "outputConfig": {
        "predictionsFormat":"OUTPUT_FORMAT",
        "DESTINATION":{
          "OUTPUT_URI_FIELD_NAME": "OUTPUT_URI"
        }
      },
      "dedicated_resources": {
        "machine_spec": {
          "machine_type": "MACHINE_TYPE",
          "accelerator_type": "ACC_TYPE",
          "accelerator_count": ACC_COUNT,
        },
        "starting_replica_count": 1,
      },
    }'

To send your request, choose one of these options:

#### curl

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) , or by using [Cloud Shell](https://docs.cloud.google.com/shell/docs) , which automatically logs you into the `gcloud` CLI . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Save the request body in a file named `request.json` , and execute the following command:

    curl -X POST \
         -H "Authorization: Bearer $(gcloud auth print-access-token)" \
         -H "Content-Type: application/json; charset=utf-8" \
         -d @request.json \
         "https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/batchPredictionJobs"

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
        -Uri "https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/batchPredictionJobs" | Select-Object -Expand Content

You should receive a JSON response similar to the following.

#### Response

    {
    "name":
      "projects/PROJECT_ID/locations/LOCATION/batchPredictionJobs/BATCH_JOB_ID",
      "displayName": "JOB_NAME",
      "model": "publishers/PUBLISHER/models/MODEL",
      "inputConfig": {
        "instancesFormat":"bigquery",
        "bigquerySource":{
          "inputUri" : "INPUT_URI"
        }
      },
      "outputConfig": {
        "predictionsFormat":"OUTPUT_FORMAT",
        "DESTINATION":{
          "OUTPUT_URI_FIELD_NAME": "OUTPUT_URI"
        }
      },
      "state": "JOB_STATE_PENDING",
      "createTime": "2024-10-16T19:33:59.153782Z",
      "updateTime": "2024-10-16T19:33:59.153782Z",
      "labels": {
        "purpose": "testing"
      },
      "modelVersionId": "1"
    }

### Cloud Storage

Specify your JSONL file's Cloud Storage location, model, and output location.

### REST

After you set up your environment, you can use REST to test a text prompt. The following sample sends a request to the publisher model endpoint.

Before using any of the request data, make the following replacements:

  - LOCATION : A region that supports Model Garden self-deployed models.
  - PROJECT\_ID : Your \[project ID\](/resource-manager/docs/creating-managing-projects\#identifiers). .
  - MODEL : The name of the [model](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/get-batch-model-garden#models) to tune, for example, `llama-3.1-8b-instruct` .
  - PUBLISHER : The model publisher, for example, `meta` , `google` , `mistral-ai` , or `deepseek-ai` .
  - INPUT\_URI : The Cloud Storage location of your JSONL batch prediction input such as `gs://bucketname/path/to/jsonl` .
  - OUTPUT\_FORMAT : To output to a BigQuery table, specify `bigquery` . To output to a Cloud Storage bucket, specify `jsonl` .
  - DESTINATION : For BigQuery, specify `bigqueryDestination` . For Cloud Storage, specify `gcsDestination` .
  - OUTPUT\_URI\_FIELD\_NAME : For BigQuery, specify `outputUri` . For Cloud Storage, specify `outputUriPrefix` .
  - OUTPUT\_URI : For BigQuery, specify the table location such as `myproject.mydataset.output_result` . For Cloud Storage, specify the bucket and folder location such as `gs://mybucket/path/to/outputfile` .
  - MACHINE\_TYPE : Defines the set of resources to deploy for your model, for example, `g2-standard-4` .
  - ACC\_TYPE : Specifies accelerators to add to your batch prediction job to help improve performance when working with intensive workloads, for example, `NVIDIA_L4` .
  - ACC\_COUNT : The number of accelerators to use in your batch prediction job.

HTTP method and URL:

    POST https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/batchPredictionJobs

Request JSON body:

    '{
      "displayName": "JOB_NAME",
      "model": "publishers/PUBLISHER/models/MODEL",
      "inputConfig": {
        "instancesFormat":"jsonl",
        "gcsDestination":{
          "uris" : "INPUT_URI"
        }
      },
      "outputConfig": {
        "predictionsFormat":"OUTPUT_FORMAT",
        "DESTINATION":{
          "OUTPUT_URI_FIELD_NAME": "OUTPUT_URI"
        }
      },
      "dedicated_resources": {
        "machine_spec": {
            "machine_type": "MACHINE_TYPE",
            "accelerator_type": "ACC_TYPE",
            "accelerator_count": ACC_COUNT,
        },
        "starting_replica_count": 1,
      },
    }'

To send your request, choose one of these options:

#### curl

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) , or by using [Cloud Shell](https://docs.cloud.google.com/shell/docs) , which automatically logs you into the `gcloud` CLI . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Save the request body in a file named `request.json` , and execute the following command:

    curl -X POST \
         -H "Authorization: Bearer $(gcloud auth print-access-token)" \
         -H "Content-Type: application/json; charset=utf-8" \
         -d @request.json \
         "https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/batchPredictionJobs"

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
        -Uri "https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/batchPredictionJobs" | Select-Object -Expand Content

You should receive a JSON response similar to the following.

#### Response

    {
    "name":
      "projects/PROJECT_ID/locations/LOCATION/batchPredictionJobs/BATCH_JOB_ID",
      "displayName": "JOB_NAME",
      "model": "publishers/PUBLISHER/models/MODEL",
      "inputConfig": {
        "instancesFormat": "jsonl",
        "gcsSource": {
          "uris": [
            "INPUT_URI"
          ]
        }
      },
      "outputConfig": {
        "predictionsFormat":"OUTPUT_FORMAT",
        "DESTINATION":{
          "OUTPUT_URI_FIELD_NAME": "OUTPUT_URI"
        }
      },
      "state": "JOB_STATE_PENDING",
      "createTime": "2024-10-16T19:33:59.153782Z",
      "updateTime": "2024-10-16T19:33:59.153782Z",
      "labels": {
        "purpose": "testing"
      },
      "modelVersionId": "1"
    }

## Get the status of a batch prediction job

Get the state of your batch prediction job to check whether it has completed successfully. The job length depends on the number of input items that you submitted.

### REST

After you set up your environment, you can use REST to test a text prompt. The following sample sends a request to the publisher model endpoint.

Before using any of the request data, make the following replacements:

  - PROJECT\_ID : Your \[project ID\](/resource-manager/docs/creating-managing-projects\#identifiers). .
  - LOCATION : The region where your batch job is located.
  - JOB\_ID : The batch job ID that was returned when you created the job.

HTTP method and URL:

    GET https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/batchPredictionJobs/JOB_ID

To send your request, choose one of these options:

#### curl

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) , or by using [Cloud Shell](https://docs.cloud.google.com/shell/docs) , which automatically logs you into the `gcloud` CLI . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Execute the following command:

    curl -X GET \
         -H "Authorization: Bearer $(gcloud auth print-access-token)" \
         "https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/batchPredictionJobs/JOB_ID"

#### PowerShell

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Execute the following command:

    $cred = gcloud auth print-access-token
    $headers = @{ "Authorization" = "Bearer $cred" }
    
    Invoke-WebRequest `
        -Method GET `
        -Headers $headers `
        -Uri "https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/batchPredictionJobs/JOB_ID" | Select-Object -Expand Content

You should receive a JSON response similar to the following.

#### Response

    {
    "name":
      "projects/PROJECT_ID/locations/LOCATION/batchPredictionJobs/BATCH_JOB_ID",
      "displayName": "JOB_NAME",
      "model": "publishers/PUBLISHER/models/MODEL",
      "inputConfig": {
        "instancesFormat":"bigquery",
        "bigquerySource":{
          "inputUri" : "INPUT_URI"
        }
      },
      "outputConfig": {
        "predictionsFormat":"OUTPUT_FORMAT",
        "DESTINATION":{
          "OUTPUT_URI_FIELD_NAME": "OUTPUT_URI"
        }
      },
      "state": "JOB_STATE_SUCCEEDED",
      "createTime": "2024-10-16T19:33:59.153782Z",
      "updateTime": "2024-10-16T19:33:59.153782Z",
      "labels": {
        "purpose": "testing"
      },
      "modelVersionId": "1"
    }

## Retrieve output

When a batch prediction job completes, retrieve the output from the location that you specified:

  - For BigQuery, the output is in the **response(JSON)** column of your destination BigQuery table.
  - For Cloud Storage, the output is saved as a JSONL file in the output Cloud Storage location.

## Supported models

Gemini Enterprise Agent Platform supports batch predictions for the following self-deployed models:

  - Llama
      - `publishers/meta/models/llama3_1@llama-3.1-8b-instruct`
      - `publishers/meta/models/llama3_1@llama-3.1-70b-instruct`
      - `publishers/meta/models/llama3_1@llama-3.1-405b-instruct-fp8`
      - `publishers/meta/models/llama3-2@llama-3.2-1b-instruct`
      - `publishers/meta/models/llama3-2@llama-3.2-3b-instruct`
      - `publishers/meta/models/llama3-2@llama-3.2-90b-vision-instruct`
  - Gemma
      - `publishers/google/models/gemma@gemma-1.1-2b-it`
      - `publishers/google/models/gemma@gemma-7b-it`
      - `publishers/google/models/gemma@gemma-1.1-7b-it`
      - `publishers/google/models/gemma@gemma-2b-it`
      - `publishers/google/models/gemma2@gemma-2-2b-it`
      - `publishers/google/models/gemma2@gemma-2-9b-it`
      - `publishers/google/models/gemma2@gemma-2-27b-it`
  - Mistral
      - `publishers/mistral-ai/models/mistral@mistral-7b-instruct-v0.2`
      - `publishers/mistral-ai/models/mistral@mistral-7b-instruct-v0.3`
      - `publishers/mistral-ai/models/mistral@mistral-7b-instruct-v0.1`
      - `publishers/mistral-ai/models/mistral@mistral-nemo-instruct-2407`
  - Deepseek
      - `publishers/deepseek-ai/models/deepseek-r1@deepseek-r1-distill-llama-8b`
