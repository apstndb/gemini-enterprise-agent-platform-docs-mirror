---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/models/tuning
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/models/tuning
title: Tuning API
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Model tuning is a crucial process in adapting Gemini to perform specific tasks with greater precision and accuracy. Model tuning works by providing a model with a training dataset that contains a set of examples of specific downstream tasks.

Use the Gemini tuning API for the following use-cases:

  - [Supervised fine tuning](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini-supervised-tuning)

#### Supported Models:

You can use supervised fine-tuning on the following Gemini models:

#### Click to expand supported models

  - [Gemini 3.5 Flash](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/3-5-flash)
  - [Gemini 3.1 Flash-Lite](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/3-1-flash-lite)
  - [Gemini 2.5 Pro](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/2-5-pro)
  - [Gemini 2.5 Flash-Lite](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/2-5-flash-lite)
  - [Gemini 2.5 Flash](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/2-5-flash)

Translation LLM V2 ( `translation-llm-002` ) is also supported.

## Example syntax

Syntax to tune a model.

### curl

    curl -X POST \
      -H "Authorization: Bearer $(gcloud auth print-access-token)" \
      -H "Content-Type: application/json" \
    
    https://TUNING_JOB_REGION-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/TUNING_JOB_REGION/tuningJobs \
    -d '{
      "baseModel": "...",
      "supervisedTuningSpec" : {
        ...
          "hyper_parameters": {
            ...
          },
      },
      "tunedModelDisplayName": "",
    }'

## Parameters list

See [examples](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/models/tuning#examples) for implementation details.

#### Request body

The request body contains data with the following parameters:

Parameters

`source_model`

Optional: `string`

Name of the foundation model that's being tuned.

`tunedModelDisplayName`

`string`

The display name of the `TunedModel` . The name can be up to 128 characters long and can consist of any UTF-8 characters.

#### `supervisedTuningSpec`

Parameters

`training_dataset`

`string`

Cloud Storage URI of your training dataset. The dataset must be formatted as a JSONL file. For best results, provide at least 100 to 500 examples. For more information, see [About supervised tuning datasets.](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini-supervised-tuning-prepare#about-datasets)

`validation_dataset`

Optional: `string`

Cloud Storage URI of your validation dataset. Your dataset must be formatted as a JSONL file. A dataset can contain up to 256 examples. If you provide this file, the data is used to generate validation metrics periodically during fine-tuning. For more information, see [About supervised tuning datasets](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini-supervised-tuning-prepare#about-datasets) .

`epoch_count`

Optional: `int`

Number of complete passes the model makes over the entire training dataset during training. Gemini Enterprise Agent Platform automatically adjusts the default value to your training dataset size. This value is based on benchmarking results to optimize model output quality.

`learning_rate_multiplier`

Optional: `float`

Multiplier for adjusting the default learning rate.

`adapter_size`

Optional: `AdapterSize`

Adapter size for tuning.

`tuned_model_display_name`

Optional: `string`

Display name of the `TunedModel` . The name can be up to 128 characters long and can consist of any UTF-8 characters.

#### `AdapterSize`

Adapter size for tuning job.

Parameters

`ADAPTER_SIZE_UNSPECIFIED`

Unspecified adapter size.

`ADAPTER_SIZE_ONE`

Adapter size 1.

`ADAPTER_SIZE_FOUR`

Adapter size 4.

`ADAPTER_SIZE_EIGHT`

Adapter size 8.

`ADAPTER_SIZE_SIXTEEN`

Adapter size 16.

## Examples

### Create a supervised tuning Job

You can create a supervised text model tuning job by using the Google Gen AI SDK or by sending a POST request.

#### Basic use case

The basic use case only sets values for `baseModel` and `training_dataset_uri` . All other parameters use the default values.

### REST

To create a model tuning job, send a POST request by using the [`tuningJobs.create`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.tuningJobs/create) method. Note that some of the parameters are not supported by all of the models. Ensure that you only include the applicable parameters for the model that you're tuning.

Before using any of the request data, make the following replacements:

  - PROJECT\_ID : Your \[project ID\](/resource-manager/docs/creating-managing-projects\#identifiers). .
  - TUNING\_JOB\_REGION : The [region](https://docs.cloud.google.com/gemini-enterprise-agent-platform/resources/locations) where the tuning job runs. This is also the default region for where the tuned model is uploaded.
  - BASE\_MODEL : Name of the foundation model to tune.
  - TRAINING\_DATASET\_URI : Cloud Storage URI of your training dataset. The dataset must be formatted as a JSONL file. For best results, provide at least 100 to 500 examples. For more information, see [About supervised tuning datasets](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini-supervised-tuning-prepare) .

HTTP method and URL:

    POST https://TUNING_JOB_REGION-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/TUNING_JOB_REGION/tuningJobs

Request JSON body:

    {
      "baseModel": "BASE_MODEL",
      "supervisedTuningSpec" : {
          "training_dataset_uri": "TRAINING_DATASET_URI"
      },
    }

To send your request, choose one of these options:

#### curl

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) , or by using [Cloud Shell](https://docs.cloud.google.com/shell/docs) , which automatically logs you into the `gcloud` CLI . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Save the request body in a file named `request.json` , and execute the following command:

    curl -X POST \
         -H "Authorization: Bearer $(gcloud auth print-access-token)" \
         -H "Content-Type: application/json; charset=utf-8" \
         -d @request.json \
         "https://TUNING_JOB_REGION-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/TUNING_JOB_REGION/tuningJobs"

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
        -Uri "https://TUNING_JOB_REGION-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/TUNING_JOB_REGION/tuningJobs" | Select-Object -Expand Content

You should receive a JSON response similar to the following.

#### Response

    {
      "name": "projects/PROJECT_ID/locations/TUNING_JOB_REGION/tuningJobs/TUNING_JOB_ID",
      "createTime": CREATE_TIME,
      "updateTime": UPDATE_TIME,
      "status": "STATUS",
      "supervisedTuningSpec": {
            "training_dataset_uri": "TRAINING_DATASET_URI",
            "validation_dataset_uri": "VALIDATION_DATASET_URI",
            "hyper_parameters": {
                "epoch_count": EPOCH_COUNT,
                "learning_rate_multiplier": LEARNING_RATE_MULTIPLIER
            },
        },
      "tunedModelDisplayName": "TUNED_MODEL_DISPLAYNAME"
    }

### Python

    import time
    
    from google import genai
    from google.genai.types import (
        CreateTuningJobConfig,
        EvaluationConfig,
        GcsDestination,
        HttpOptions,
        Metric,
        OutputConfig,
        TuningDataset,
    )
    
    # TODO(developer): Update and un-comment below line
    # output_gcs_uri = "gs://your-bucket/your-prefix"
    
    client = genai.Client(http_options=HttpOptions(api_version="v1beta1"))
    
    training_dataset = TuningDataset(
        gcs_uri="gs://cloud-samples-data/ai-platform/generative_ai/gemini/text/sft_train_data.jsonl",
    )
    validation_dataset = TuningDataset(
        gcs_uri="gs://cloud-samples-data/ai-platform/generative_ai/gemini/text/sft_validation_data.jsonl",
    )
    
    evaluation_config = EvaluationConfig(
        metrics=[
            Metric(
                name="FLUENCY",
                prompt_template="""Evaluate this {prediction}"""
            )
        ],
        output_config=OutputConfig(
            gcs_destination=GcsDestination(
                output_uri_prefix=output_gcs_uri,
            )
        ),
    )
    
    tuning_job = client.tunings.tune(
        base_model="gemini-3.5-flash",
        training_dataset=training_dataset,
        config=CreateTuningJobConfig(
            tuned_model_display_name="Example tuning job",
            validation_dataset=validation_dataset,
            evaluation_config=evaluation_config,
        ),
    )
    
    running_states = set([
        "JOB_STATE_PENDING",
        "JOB_STATE_RUNNING",
    ])
    
    while tuning_job.state in running_states:
        print(tuning_job.state)
        tuning_job = client.tunings.get(name=tuning_job.name)
        time.sleep(60)
    
    print(tuning_job.tuned_model.model)
    print(tuning_job.tuned_model.endpoint)
    print(tuning_job.experiment)
    # Example response:
    # projects/123456789012/locations/us-central1/models/1234567890@1
    # projects/123456789012/locations/us-central1/endpoints/123456789012345
    # projects/123456789012/locations/us-central1/metadataStores/default/contexts/tuning-experiment-2025010112345678
    
    if tuning_job.tuned_model.checkpoints:
        for i, checkpoint in enumerate(tuning_job.tuned_model.checkpoints):
            print(f"Checkpoint {i + 1}: ", checkpoint)
        # Example response:
        # Checkpoint 1:  checkpoint_id='1' epoch=1 step=10 endpoint='projects/123456789012/locations/us-central1/endpoints/123456789000000'
        # Checkpoint 2:  checkpoint_id='2' epoch=2 step=20 endpoint='projects/123456789012/locations/us-central1/endpoints/123456789012345'

#### Advanced use case

The advance use case expands upon the basic use case, but also sets values for optional `hyper_parameters` , such as `epoch_count` , `learning_rate_multiplier` and `adapter_size` .

### REST

To create a model tuning job, send a POST request by using the [`tuningJobs.create`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.tuningJobs/create) method. Note that some of the parameters are not supported by all of the models. Ensure that you only include the applicable parameters for the model that you're tuning.

Before using any of the request data, make the following replacements:

  - PROJECT\_ID : Your [project ID](https://docs.cloud.google.com/resource-manager/docs/creating-managing-projects#identifiers) .
  - TUNING\_JOB\_REGION : The [region](https://docs.cloud.google.com/gemini-enterprise-agent-platform/resources/locations) where the tuning job runs. This is also the default region for where the tuned model is uploaded.
  - BASE\_MODEL : Name of the foundation model to tune.
  - TRAINING\_DATASET\_URI : Cloud Storage URI of your training dataset. The dataset must be formatted as a JSONL file. For best results, provide at least 100 to 500 examples. For more information, see [About supervised tuning datasets](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini-supervised-tuning-prepare) .
  - VALIDATION\_DATASET\_URI Optional: The Cloud Storage URI of your validation dataset file.
  - EPOCH\_COUNT Optional: The number of complete passes the model makes over the entire training dataset during training. Leave it unset to use the [pre-populated recommended value.](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/models/tuning#supervisedtuningspec)
  - ADAPTER\_SIZE Optional: The [Adapter size](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/models/tuning#adaptersize) to use for the tuning job. The adapter size influences the number of trainable parameters for the tuning job. A larger adapter size implies that the model can learn more complex tasks, but it requires a larger training dataset and longer training times.
  - LEARNING\_RATE\_MULTIPLIER : Optional: A multiplier to apply to the recommended learning rate. Leave it unset to use the [recommended value.](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/models/tuning#supervisedtuningspec)
  - EXPORT\_LAST\_CHECKPOINT\_ONLY Optional: Set to `true` to use only the latest checkpoint.
  - METRIC\_SPEC Optional: One or more [metric specs](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/models/evaluation) you are using to run an evaluation using the Gen AI evaluation service. You can use the following metric specs: `"pointwise_metric_spec"` , `"pairwise_metric_spec"` , `"exact_match_spec"` , `"bleu_spec"` , and `"rouge_spec"` .
  - METRIC\_SPEC\_FIELD\_NAME Optional: The required fields for your chosen metric spec. For example, `"metric_prompt_template"`
  - METRIC\_SPEC\_FIELD\_NAME\_CONTENT Optional: The field content for your chosen metric spec. For example, you can use the following field content for a pointwise evaluation: `"Evaluate the fluency of this sentence: {response}. Give score from 0 to 1. 0 - not fluent at all. 1 - very fluent."`
  - CLOUD\_STORAGE\_BUCKET Optional: The Cloud Storage bucket to store the results of an evaluation run by the Gen AI evaluation service.
  - TUNED\_MODEL\_DISPLAYNAME Optional: A display name for the tuned model. If not set, a random name is generated.
  - KMS\_KEY\_NAME Optional: The Cloud KMS resource identifier of the customer-managed encryption key used to protect a resource. The key has the format: `projects/my-project/locations/my-region/keyRings/my-kr/cryptoKeys/my-key` . The key needs to be in the same region as where the compute resource is created. For more information, see [Customer-managed encryption keys (CMEK)](https://cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/cmek) .
  - SERVICE\_ACCOUNT Optional: The service account that the tuningJob workload runs as. If not specified, the Agent Platform Secure Fine-Tuning Service Agent in the project is used. See [Tuning Service Agent](https://cloud.google.com/iam/docs/service-agents#vertex-ai-secure-fine-tuning-service-account) . If you plan to use a customer-managed Service Account, you must grant the `roles/aiplatform.tuningServiceAgent` role to the service account. Also grant the [Tuning Service Agent](https://cloud.google.com/iam/docs/service-agents#vertex-ai-secure-fine-tuning-service-account) `roles/iam.serviceAccountTokenCreator` role to the customer-managed Service Account.

HTTP method and URL:

    POST https://TUNING_JOB_REGION-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/TUNING_JOB_REGION/tuningJobs

Request JSON body:

    {
      "baseModel": "BASE_MODEL",
      "supervisedTuningSpec" : {
          "trainingDatasetUri": "TRAINING_DATASET_URI",
          "validationDatasetUri": "VALIDATION_DATASET_URI",
          "hyperParameters": {
              "epochCount": "EPOCH_COUNT",
              "adapterSize": "ADAPTER_SIZE",
              "learningRateMultiplier": "LEARNING_RATE_MULTIPLIER"
          },
          "exportLastCheckpointOnly": EXPORT_LAST_CHECKPOINT_ONLY,
          "evaluationConfig": {
              "metrics": [
                  {
                      "aggregation_metrics": ["AVERAGE", "STANDARD_DEVIATION"],
                      "METRIC_SPEC": {
                          "METRIC_SPEC_FIELD_NAME":
                              METRIC_SPEC_FIELD_CONTENT
                      }
                  },
              ],
              "outputConfig": {
                  "gcs_destination": {
                      "output_uri_prefix": "CLOUD_STORAGE_BUCKET"
                  }
              },
          },
      },
      "tunedModelDisplayName": "TUNED_MODEL_DISPLAYNAME",
      "encryptionSpec": {
        "kmsKeyName": "KMS_KEY_NAME"
      },
      "serviceAccount": "SERVICE_ACCOUNT"
    }

To send your request, choose one of these options:

#### curl

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) , or by using [Cloud Shell](https://docs.cloud.google.com/shell/docs) , which automatically logs you into the `gcloud` CLI . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Save the request body in a file named `request.json` , and execute the following command:

    curl -X POST \
         -H "Authorization: Bearer $(gcloud auth print-access-token)" \
         -H "Content-Type: application/json; charset=utf-8" \
         -d @request.json \
         "https://TUNING_JOB_REGION-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/TUNING_JOB_REGION/tuningJobs"

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
        -Uri "https://TUNING_JOB_REGION-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/TUNING_JOB_REGION/tuningJobs" | Select-Object -Expand Content

You should receive a JSON response similar to the following.

#### Response

    {
      "name": "projects/PROJECT_ID/locations/TUNING_JOB_REGION/tuningJobs/TUNING_JOB_ID",
      "createTime": CREATE_TIME,
      "updateTime": UPDATE_TIME,
      "status": "STATUS",
      "supervisedTuningSpec": {
            "trainingDatasetUri": "TRAINING_DATASET_URI",
            "validationDatasetUri": "VALIDATION_DATASET_URI",
            "hyperParameters": {
                "epochCount": EPOCH_COUNT,
                "adapterSize": "ADAPTER_SIZE",
                "learningRateMultiplier": LEARNING_RATE_MULTIPLIER
            },
        },
      "tunedModelDisplayName": "TUNED_MODEL_DISPLAYNAME",
      "encryptionSpec": {
        "kmsKeyName": "KMS_KEY_NAME"
      },
      "serviceAccount": "SERVICE_ACCOUNT"
    }

### Python

    import time
    
    from google import genai
    from google.genai.types import (
        CreateTuningJobConfig,
        EvaluationConfig,
        GcsDestination,
        HttpOptions,
        Metric,
        OutputConfig,
        TuningDataset,
    )
    
    # TODO(developer): Update and un-comment below line
    # output_gcs_uri = "gs://your-bucket/your-prefix"
    
    client = genai.Client(http_options=HttpOptions(api_version="v1beta1"))
    
    training_dataset = TuningDataset(
        gcs_uri="gs://cloud-samples-data/ai-platform/generative_ai/gemini/text/sft_train_data.jsonl",
    )
    validation_dataset = TuningDataset(
        gcs_uri="gs://cloud-samples-data/ai-platform/generative_ai/gemini/text/sft_validation_data.jsonl",
    )
    
    evaluation_config = EvaluationConfig(
        metrics=[
            Metric(
                name="FLUENCY",
                prompt_template="""Evaluate this {prediction}"""
            )
        ],
        output_config=OutputConfig(
            gcs_destination=GcsDestination(
                output_uri_prefix=output_gcs_uri,
            )
        ),
    )
    
    tuning_job = client.tunings.tune(
        base_model="gemini-3.5-flash",
        training_dataset=training_dataset,
        config=CreateTuningJobConfig(
            tuned_model_display_name="Example tuning job",
            validation_dataset=validation_dataset,
            evaluation_config=evaluation_config,
        ),
    )
    
    running_states = set([
        "JOB_STATE_PENDING",
        "JOB_STATE_RUNNING",
    ])
    
    while tuning_job.state in running_states:
        print(tuning_job.state)
        tuning_job = client.tunings.get(name=tuning_job.name)
        time.sleep(60)
    
    print(tuning_job.tuned_model.model)
    print(tuning_job.tuned_model.endpoint)
    print(tuning_job.experiment)
    # Example response:
    # projects/123456789012/locations/us-central1/models/1234567890@1
    # projects/123456789012/locations/us-central1/endpoints/123456789012345
    # projects/123456789012/locations/us-central1/metadataStores/default/contexts/tuning-experiment-2025010112345678
    
    if tuning_job.tuned_model.checkpoints:
        for i, checkpoint in enumerate(tuning_job.tuned_model.checkpoints):
            print(f"Checkpoint {i + 1}: ", checkpoint)
        # Example response:
        # Checkpoint 1:  checkpoint_id='1' epoch=1 step=10 endpoint='projects/123456789012/locations/us-central1/endpoints/123456789000000'
        # Checkpoint 2:  checkpoint_id='2' epoch=2 step=20 endpoint='projects/123456789012/locations/us-central1/endpoints/123456789012345'

### List tuning Jobs

You can view a list of tuning jobs in your current project by using the Google Gen AI SDK or by sending a GET request.

### REST

To create a model tuning job, send a POST request by using the [`tuningJobs.create`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.tuningJobs/create) method. Note that some of the parameters are not supported by all of the models. Ensure that you only include the applicable parameters for the model that you're tuning.

Before using any of the request data, make the following replacements:

  - PROJECT\_ID : Your [project ID](https://docs.cloud.google.com/resource-manager/docs/creating-managing-projects#identifiers) .
  - TUNING\_JOB\_REGION : The [region](https://docs.cloud.google.com/gemini-enterprise-agent-platform/resources/locations) where the tuning job runs. This is also the default region for where the tuned model is uploaded.

HTTP method and URL:

    GET https://TUNING_JOB_REGION-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/TUNING_JOB_REGION/tuningJobs

To send your request, choose one of these options:

#### curl

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) , or by using [Cloud Shell](https://docs.cloud.google.com/shell/docs) , which automatically logs you into the `gcloud` CLI . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Execute the following command:

    curl -X GET \
         -H "Authorization: Bearer $(gcloud auth print-access-token)" \
         "https://TUNING_JOB_REGION-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/TUNING_JOB_REGION/tuningJobs"

#### PowerShell

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Execute the following command:

    $cred = gcloud auth print-access-token
    $headers = @{ "Authorization" = "Bearer $cred" }
    
    Invoke-WebRequest `
        -Method GET `
        -Headers $headers `
        -Uri "https://TUNING_JOB_REGION-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/TUNING_JOB_REGION/tuningJobs" | Select-Object -Expand Content

You should receive a JSON response similar to the following.

#### Response

    {
      "tuning_jobs": [
        TUNING_JOB_1, TUNING_JOB_2, ...
      ]
    }

### Python

    from google import genai
    from google.genai.types import HttpOptions
    
    client = genai.Client(http_options=HttpOptions(api_version="v1"))
    
    responses = client.tunings.list()
    for response in responses:
        print(response.name)
        # Example response:
        # projects/123456789012/locations/us-central1/tuningJobs/123456789012345

### Get details of a tuning job

You can get the details of a tuning job by using the Google Gen AI SDK or by sending a GET request.

### REST

To view a list of model tuning jobs, send a GET request by using the [`tuningJobs.get`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.tuningJobs/get) method and specify the `TuningJob_ID` .

Before using any of the request data, make the following replacements:

  - PROJECT\_ID : Your [project ID](https://docs.cloud.google.com/resource-manager/docs/creating-managing-projects#identifiers) .
  - TUNING\_JOB\_REGION : The [region](https://docs.cloud.google.com/gemini-enterprise-agent-platform/resources/locations) where the tuning job runs. This is also the default region for where the tuned model is uploaded.
  - TUNING\_JOB\_ID : The ID of the tuning job.

HTTP method and URL:

    GET https://TUNING_JOB_REGION-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/TUNING_JOB_REGION/tuningJobs/TUNING_JOB_ID

To send your request, choose one of these options:

#### curl

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) , or by using [Cloud Shell](https://docs.cloud.google.com/shell/docs) , which automatically logs you into the `gcloud` CLI . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Execute the following command:

    curl -X GET \
         -H "Authorization: Bearer $(gcloud auth print-access-token)" \
         "https://TUNING_JOB_REGION-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/TUNING_JOB_REGION/tuningJobs/TUNING_JOB_ID"

#### PowerShell

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Execute the following command:

    $cred = gcloud auth print-access-token
    $headers = @{ "Authorization" = "Bearer $cred" }
    
    Invoke-WebRequest `
        -Method GET `
        -Headers $headers `
        -Uri "https://TUNING_JOB_REGION-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/TUNING_JOB_REGION/tuningJobs/TUNING_JOB_ID" | Select-Object -Expand Content

You should receive a JSON response similar to the following.

#### Response

    {
      "name": "projects/PROJECT_ID/locations/TUNING_JOB_REGION/tuningJobs/TUNING_JOB_ID",
      "tunedModelDisplayName": "TUNED_MODEL_DISPLAYNAME",
      "createTime": CREATE_TIME,
      "endTime": END_TIME,
      "tunedModel": {
          "model": "projects/PROJECT_ID/locations/TUNING_JOB_REGION/models/MODEL_ID",
          "endpoint": "projects/PROJECT_ID/locations/TUNING_JOB_REGION/endpoints/ENDPOINT_ID"
      },
      "experiment": "projects/PROJECT_ID/locations/TUNING_JOB_REGION/metadataStores/default/contexts/EXPERIMENT_ID",
      "tuning_data_statistics": {
          "supervisedTuningDataStats": {
              "tuninDatasetExampleCount": "TUNING_DATASET_EXAMPLE_COUNT",
              "totalBillableTokenCount": "TOTAL_BILLABLE_TOKEN_COUNT",
              "tuningStepCount": "TUNING_STEP_COUNT"
          }
      },
      "status": "STATUS",
      "supervisedTuningSpec" : {
            "trainingDatasetUri": "TRAINING_DATASET_URI",
            "validationDataset_uri": "VALIDATION_DATASET_URI",
            "hyperParameters": {
                "epochCount": EPOCH_COUNT,
                "learningRateMultiplier": LEARNING_RATE_MULTIPLIER
            }
        }
    }

### Python

    from google import genai
    from google.genai.types import HttpOptions
    
    client = genai.Client(http_options=HttpOptions(api_version="v1"))
    
    # Get the tuning job and the tuned model.
    # Eg. tuning_job_name = "projects/123456789012/locations/us-central1/tuningJobs/123456789012345"
    tuning_job = client.tunings.get(name=tuning_job_name)
    
    print(tuning_job.tuned_model.model)
    print(tuning_job.tuned_model.endpoint)
    print(tuning_job.experiment)
    # Example response:
    # projects/123456789012/locations/us-central1/models/1234567890@1
    # projects/123456789012/locations/us-central1/endpoints/123456789012345
    # projects/123456789012/locations/us-central1/metadataStores/default/contexts/tuning-experiment-2025010112345678

### Cancel a tuning job

You can cancel a tuning job by using the Google Gen AI SDK or by sending a POST request.

### REST

To view a list of model tuning jobs, send a GET request by using the [`tuningJobs.cancel`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.tuningJobs/cancel) method and specify the `TuningJob_ID` .

Before using any of the request data, make the following replacements:

  - PROJECT\_ID : Your [project ID](https://docs.cloud.google.com/resource-manager/docs/creating-managing-projects#identifiers) .
  - TUNING\_JOB\_REGION : The [region](https://docs.cloud.google.com/gemini-enterprise-agent-platform/resources/locations) where the tuning job runs. This is also the default region for where the tuned model is uploaded.
  - TUNING\_JOB\_ID : The ID of the tuning job.

HTTP method and URL:

    POST https://TUNING_JOB_REGION-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/TUNING_JOB_REGION/tuningJobs/TUNING_JOB_ID:cancel

To send your request, choose one of these options:

#### curl

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) , or by using [Cloud Shell](https://docs.cloud.google.com/shell/docs) , which automatically logs you into the `gcloud` CLI . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Execute the following command:

    curl -X POST \
         -H "Authorization: Bearer $(gcloud auth print-access-token)" \
         -H "Content-Type: application/json; charset=utf-8" \
         -d "" \
         "https://TUNING_JOB_REGION-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/TUNING_JOB_REGION/tuningJobs/TUNING_JOB_ID:cancel"

#### PowerShell

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Execute the following command:

    $cred = gcloud auth print-access-token
    $headers = @{ "Authorization" = "Bearer $cred" }
    
    Invoke-WebRequest `
        -Method POST `
        -Headers $headers `
        -Uri "https://TUNING_JOB_REGION-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/TUNING_JOB_REGION/tuningJobs/TUNING_JOB_ID:cancel" | Select-Object -Expand Content

You should receive a JSON response similar to the following.

#### Response

``` 
{}
```

### Python

    from google import genai
    from google.genai.types import HttpOptions
    
    
    def cancel_tuning_job(tuning_job_name: str) -> None:
        client = genai.Client(http_options=HttpOptions(api_version="v1"))
    
        # Cancel the tuning job.
        # Eg. tuning_job_name = "projects/123456789012/locations/us-central1/tuningJobs/123456789012345"
        client.tunings.cancel(name=tuning_job_name)

## What's next

For detailed documentation, see the following:

  - [Supervised Tuning Job](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini-use-supervised-tuning#create_a_text_model_supervised_tuning_job)
  - [Generate content with the Gemini API](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/models/inference)
