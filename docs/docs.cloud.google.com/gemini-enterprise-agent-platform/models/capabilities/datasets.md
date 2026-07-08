---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/models/capabilities/datasets
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/capabilities/datasets
title: Multimodal datasets
description: Manage and use multimodal datasets for Agent Platform. Load data from BigQuery, DataFrames, or Cloud Storage, prevent duplication, and ensure data quality with built-in validation. Use with Agent Platform SDK or REST API.
data_source: docs.cloud.google.com
---

> To see an example of Multimodal datasets, run the " Multimodal Dataset Preview" notebook in one of the following environments:
> 
> [![](https://docs.cloud.google.com/static/vertex-ai/images/colab-logo-32px.png) Open in Colab](https://colab.research.google.com/github/GoogleCloudPlatform/generative-ai/blob/main/gemini/multimodal-dataset/intro_vertex_ai_multimodal_dataset.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/colab-enterprise-logo-32px.png) Open in Colab Enterprise](https://console.cloud.google.com/agent-platform/colab/import/https%3A%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fgenerative-ai%2Fmain%2Fgemini%2Fmultimodal-dataset%2Fintro_vertex_ai_multimodal_dataset.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/vertex-ai-workbench-logo-32px.png) Open in Agent Platform Workbench](https://console.cloud.google.com/agent-platform/workbench/deploy-notebook?download_url=https%3A%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fgenerative-ai%2Fmain%2Fgemini%2Fmultimodal-dataset%2Fintro_vertex_ai_multimodal_dataset.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/github-logo-32px.png) View on GitHub](https://github.com/GoogleCloudPlatform/generative-ai/blob/main/gemini/multimodal-dataset/intro_vertex_ai_multimodal_dataset.ipynb)

> **Preview**
> 
> This feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](https://docs.cloud.google.com/terms/service-terms#1) . Pre-GA features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

Multimodal datasets on Agent Platform let you create, manage, share, and use multimodal datasets for Generative AI. Multimodal datasets provide the following key features:

  - You can load datasets from BigQuery, DataFrames, or JSONL files in Cloud Storage.

  - Create your dataset once and use it across different job types, such as [supervised fine-tuning](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini-supervised-tuning) and batch prediction, which prevents data duplication and formatting issues.

  - Keep all your generative AI datasets in a single, managed location.

  - Validate your schema and structure and quantify the resources needed for downstream tasks, helping you catch errors and estimate the cost before you start a task.

You can use multimodal datasets through the [Agent Platform SDK](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/python-sdk/use-vertex-ai-sdk) or [REST API](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.datasets) .

Multimodal datasets are a type of [managed datasets on Agent Platform](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/datasets/overview) . They are different from other types of managed datasets in the following ways:

  - Multimodal datasets can include data of any modality (text, image, audio, video). Other types of managed datasets are for only a single modality.
  - Multimodal datasets can only be used for Generative AI services on Agent Platform, such as tuning and batch prediction with generative models. Other managed dataset types can only be used for Agent Platform predictive models.
  - Multimodal datasets support additional methods, such as `assemble` and `assess` , which are used for previewing data, validating requests, and estimating costs.
  - Multimodal datasets are stored in BigQuery, which is optimized for large datasets.

## Before you begin

1.  [Install and initialize the Agent Platform SDK for Python](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/start/install-sdk)

2.  Import the following libraries and create a client:
    
    ```python
    import agentplatform
    from agentplatform.types import (
        GeminiExample,
        GeminiRequestReadConfig,
        GeminiTemplateConfig,
    )
    
    # To use related features, such as tuning and batch prediction, you may also
    # need to import the Google Gen AI SDK:
    from google import genai
    from google.genai.types import Content, Part
    
    # Create a client for multimodal dataset operations.
    client = agentplatform.Client(project="PROJECT_ID", location="LOCATION")
    ```

## Create a dataset

You can create a multimodal [`dataset`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.datasets) from different sources:

  - from a Pandas DataFrame
    
        my_dataset = client.datasets.create_from_pandas(
            dataframe=my_dataframe,
            target_table_id=table_id    # optional
        )

  - from a [BigQuery DataFrame](https://docs.cloud.google.com/bigquery/docs/bigquery-dataframes-introduction) :
    
        my_dataset = client.datasets.create_from_bigframes(
            dataframe=my_dataframe,
            target_table_id=table_id    # optional
        )

  - from a BigQuery table
    
        my_dataset_from_bigquery = client.datasets.create_from_bigquery(
            bigquery_uri="bq://projectId.datasetId.tableId"
        )

  - from a BigQuery table, using the REST API
    
        curl -X POST \
        -H "Authorization: Bearer $(gcloud auth print-access-token)" \
        -H "Content-Type: application/json" \
        "https://LOCATION-aiplatform.googleapis.com/v1beta1/projects/PROJECT/locations/LOCATION/datasets" \
        -d '{
          "display_name": "TestDataset",
          "metadataSchemaUri": "gs://google-cloud-aiplatform/schema/dataset/metadata/multimodal_1.0.0.yaml",
          "metadata": {
            "inputConfig": {
              "bigquery_source": {
                "uri": "bq://projectId.datasetId.tableId"
              }
            }
          }
        }'

  - from a JSONL file in Cloud Storage. In the following example, the JSONL file contains requests that are already formatted for Gemini, so no assembly is required.
    
        my_dataset = client.datasets.create_from_gemini_request_jsonl(
          gcs_uri = gcs_uri_of_jsonl_file,
        )

  - from an existing multimodal dataset
    
        # Load dataset based on its name. This accepts a full resource name or a
        # dataset ID.
        same_dataset = client.datasets.get_multimodal_dataset(name=dataset_name)

## Construct and attach a read configuration

A read configuration ( `GeminiRequestReadConfig` ) defines how to transform the multimodal dataset to a format that can be passed to the model. It contains a template with placeholders that are replaced with the values of the corresponding dataset columns during assembly. This is required for running a tuning or batch prediction job.

### Agent Platform SDK

1.  Construct a read configuration. There are two ways to construct one:
    
      - Use the `GeminiRequestReadConfig.single_turn_template` helper method:
    
    <!-- end list -->
    
        read_config = GeminiRequestReadConfig.single_turn_template(
                prompt="This is the image: {image_uris}",
                response="{labels}",
                system_instruction='You are a botanical image classifier. Analyze the provided image '
                        'and determine the most accurate classification of the flower.'
                        'These are the only flower categories: [\'daisy\', \'dandelion\', \'roses\', \'sunflowers\', \'tulips\'].'
                        'Return only one category per image.'
        )
    
      - Manually construct a read configuration from a `GeminiExample` , which allows finer granularity, such as multi-turn conversations. The following code sample also includes optional commented code for specifying a `field_mapping` , which lets you use a placeholder name that is different from the column name of the dataset. For example:
    
    <!-- end list -->
    
        # Define a GeminiExample
        gemini_example = GeminiExample(
          contents=[
              Content(role="user", parts=[Part.from_text(text="This is the image: {image_uris}")]),
              Content(role="model", parts=[Part.from_text(text="This is the flower class: {label}.")]),
              Content(role="user", parts=[Part.from_text(text="Your response should only contain the class label.")]),
              Content(role="model", parts=[Part.from_text(text="{label}")]),
        
              # Optional: If you specify a field_mapping, you can use different placeholder values. For example:
              # Content(role="user", parts=[Part.from_text(text="This is the image: {uri_placeholder}")]),
              # Content(role="model", parts=[Part.from_text(text="This is the flower class: {flower_placeholder}.")]),
              # Content(role="user", parts=[Part.from_text(text="Your response should only contain the class label.")]),
              # Content(role="model", parts=[Part.from_text(text="{flower_placeholder}")]),
          ],
          system_instruction=Content(
              parts=[
                  Part.from_text(
                      text='You are a botanical image classifier. Analyze the provided image '
                      'and determine the most accurate classification of the flower.'
                      'These are the only flower categories: [\'daisy\', \'dandelion\', \'roses\', \'sunflowers\', \'tulips\'].'
                      'Return only one category per image.'
                  )
              ]
          ),
        )
        
        # Construct the read config, specifying a map for the placeholders.
        read_config = GeminiRequestReadConfig(
            template_config=GeminiTemplateConfig(
                gemini_example=gemini_example,
        
                # Optional: Map the template placeholders to the column names of your dataset.
                # Not required if the template placeholders are column names of the dataset.
                # field_mapping={"uri_placeholder": "image_uris", "flower_placeholder": "labels"},
            ),
        )

2.  Attach it to the dataset and persist the change:
    
        my_dataset.set_read_config(read_config=read_config)
        my_dataset = client.datasets.update_multimodal_dataset(multimodal_dataset=my_dataset)

### REST

Call the [`patch`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.datasets/patch) method and update the `metadata` field with the following:

  - The URI of the BigQuery table. For datasets created from a BigQuery table, this is your source `bigquery_uri` . For datasets created from other sources, such as JSONL or DataFrame, this is the BigQuery table where your data was copied.
  - A [`gemini_template_config`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/GeminiRequestReadConfig#GeminiTemplateConfig) .

<!-- end list -->

    curl -X PATCH \
    -H "Authorization: Bearer $(gcloud auth print-access-token)" \
    -H "Content-Type: application/json" \
    -d $'{
      "metadata": {
        "input_config": {
          "bigquery_source": {
            "uri": "bq://projectId.datasetId.tableId"
          }
        },
        "gemini_template_config_source": {
          "gemini_template_config": {
            "gemini_example": {
              "contents": [
                {
                  "role": "user",
                  "parts": [
                    {
                      "text": "This is the image: {image_uris}"
    
                    }
                  ]
                },
                {
                  "role": "model",
                  "parts": [
                    {
                      "text": "response"
                    }
                  ]
                }
              ]
            "systemInstruction": {
                "parts": [
                    {
                        "text": "You are a botanical image classifier."
                    }
                ]
              }
            }
          }
        }
      }
    }' \
    "https://LOCATION-aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/LOCATION/datasets/DATASET_ID?updateMask=metadata"

## (Optional) Assemble the dataset

The [`assemble`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.datasets/assemble) method applies the read configuration to transform your dataset and stores the output in a new BigQuery table. This lets you preview the data before it is passed to the model.

By default, the dataset's attached read configuration is used, but you can pass a `gemini_request_read_config` to override the default behavior.

### Agent Platform SDK

The `assemble` method returns a `(table_id, dataframe)` tuple. Pass `load_dataframe=True` to also load the assembled table as a DataFrame for inspection.

    table_id, assembly = client.datasets.assemble(
        name=my_dataset.name,
        gemini_request_read_config=read_config,    # optional if attached to the dataset
        load_dataframe=True,
    )
    
    # Inspect the results
    assembly.head()

### REST

    curl -X POST \
    -H "Authorization: Bearer $(gcloud auth print-access-token)" \
    -H "Content-Type: application/json" \
    "https://LOCATION-aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/LOCATION/datasets/DATASET_ID:assemble" \
    -d '{}'

For example, assume that your multimodal dataset contains the following data:

| Row | image\_uris                                                                     | labels |
| --- | ------------------------------------------------------------------------------- | ------ |
| 1   | gs://cloud-samples-data/ai-platform/flowers/daisy/1396526833\_fb867165be\_n.jpg | daisy  |

Then, the `assemble` method creates a new BigQuery table with the name `table_id` where each row contains the [request body](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.publishers.models/streamGenerateContent#request-body) . For example:

    {
      "contents": [
        {
          "parts": [
            {
              "text": "This is the image: "
            },
            {
              "fileData": {
                "fileUri": "gs://cloud-samples-data/ai-platform/flowers/daisy/1396526833_fb867165be_n.jpg",
                "mimeType": "image/jpeg"
              }
            }
          ],
          "role": "user"
        },
        {
          "parts": [
            {
              "text": "daisy"
            }
          ],
          "role": "model"
        }
      ],
      "systemInstruction": {
        "parts": [
          {
            "text": "You are a botanical image classifier. Analyze the provided image and determine the most accurate classification of the flower.These are the only flower categories: ['daisy', 'dandelion', 'roses', 'sunflowers', 'tulips'].Return only one category per image."
          }
        ]
      }
    }

## Tune your model

You can [tune Gemini models](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini-use-supervised-tuning) using a multimodal dataset.

### (Optional) Validate the dataset

Assess the dataset to check whether it contains errors, such as dataset formatting errors or model errors.

### Agent Platform SDK

Call `assess_tuning_validity()` . By default, the dataset's attached read configuration is used, but you can pass a `gemini_request_read_config` to override the default behavior.

    # Attach the read configuration to the dataset.
    my_dataset.set_read_config(read_config=read_config)
    my_dataset = client.datasets.update_multimodal_dataset(multimodal_dataset=my_dataset)
    
    # Validation for tuning
    validation = client.datasets.assess_tuning_validity(
        dataset_name=my_dataset.name,
        model_name="gemini-2.5-flash",
        dataset_usage="SFT_TRAINING"
    )
    
    # Inspect validation result
    validation.errors

### REST

Call the `assess` method and provide a [`TuningValidationAssessmentConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.datasets/assess#TuningValidationAssessmentConfig) .

    curl -X POST \
    -H "Authorization: Bearer $(gcloud auth print-access-token)" \
    -H "Content-Type: application/json" \
    "https://LOCATION-aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/LOCATION/datasets/DATASET_ID:assess" \
    -d '{
      "tuningValidationAssessmentConfig": {
        "modelName": "projects/PROJECT_ID/locations/LOCATION/models/gemini-2.5-flash",
        "datasetUsage": "SFT_TRAINING"
      }
    }'

### (Optional) Estimate resource usage

Assess the dataset to get the token and billable character count for your tuning job.

### Agent Platform SDK

Call `assess_tuning_resources()` .

    # Resource estimation for tuning.
    tuning_resources = client.datasets.assess_tuning_resources(
        dataset_name=my_dataset.name,
        model_name="gemini-2.5-flash"
    )
    
    print(tuning_resources)
    # For example, TuningResourceUsageAssessmentResult(token_count=362688, billable_character_count=122000)

### REST

Call the `assess` method and provide a [`TuningResourceUsageAssessmentConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.datasets/assess#TuningResourceUsageAssessmentConfig) .

    curl -X POST \
    -H "Authorization: Bearer $(gcloud auth print-access-token)" \
    -H "Content-Type: application/json" \
    "https://LOCATION-aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/LOCATION/datasets/DATASET_ID:assess" \
    -d '{
      "tuningResourceUsageAssessmentConfig": {
        "modelName": "projects/PROJECT_ID/locations/LOCATION/models/gemini-2.5-flash"
      }
    }'

### Run the tuning job

Use the Google Gen AI SDK to start a tuning job, passing the resource name of the multimodal dataset. The dataset must have an attached read configuration.

### Google Gen AI SDK

    from google import genai
    from google.genai.types import HttpOptions, CreateTuningJobConfig
    
    genai_client = genai.Client(http_options=HttpOptions(api_version="v1"))
    
    tuning_job = genai_client.tunings.tune(
      base_model="gemini-2.5-flash",
      # Pass the resource name of the Multimodal Dataset, not the dataset object
      training_dataset={
          "vertex_dataset_resource": my_multimodal_dataset.name
      },
      # Optional
      config=CreateTuningJobConfig(
          validation_dataset={
              "vertex_dataset_resource": my_multimodal_validation_dataset.name
          },
          tuned_model_display_name="Example tuning job"),
    )

For more information, see [Create a tuning job](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini-use-supervised-tuning#create_a_text_model_supervised_tuning_job) .

## Batch prediction

You can get [batch predictions](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/capabilities/batch-prediction-gemini) using a multimodal dataset.

### (Optional) Validate the dataset

Assess the dataset to check whether it contains errors, such as dataset formatting errors or model errors.

### Agent Platform SDK

Call `assess_batch_prediction_validity()` . By default, the dataset's attached read configuration is used, but you can pass a `gemini_request_read_config` to override the default behavior.

    # Attach the read configuration to the dataset.
    my_dataset.set_read_config(read_config=read_config)
    my_dataset = client.datasets.update_multimodal_dataset(multimodal_dataset=my_dataset)
    
    # Validation for batch prediction
    validation = client.datasets.assess_batch_prediction_validity(
        dataset_name=my_dataset.name,
        model_name="gemini-2.5-flash"
    )
    
    # Inspect validation result
    validation.errors

### REST

Call the `assess` method and provide a [`batchPredictionValidationAssessmentConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.datasets/assess#BatchPredictionValidationAssessmentConfig) .

    curl -X POST \
    -H "Authorization: Bearer $(gcloud auth print-access-token)" \
    -H "Content-Type: application/json" \
    "https://LOCATION-aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/LOCATION/datasets/DATASET_ID:assess" \
    -d '{
      "batchPredictionValidationAssessmentConfig": {
        "modelName": "projects/PROJECT_ID/locations/LOCATION/models/gemini-2.5-flash",
      }
    }'

### (Optional) Estimate resource usage

Assess the dataset to get the token count for your job.

### Agent Platform SDK

Call `assess_batch_prediction_resources()` .

    batch_prediction_resources = client.datasets.assess_batch_prediction_resources(
        dataset_name=my_dataset.name,
        model_name="gemini-2.5-flash"
    )
    
    print(batch_prediction_resources)
    # For example, BatchPredictionResourceUsageAssessmentResult(token_count=362688, audio_token_count=122000)

### REST

Call the `assess` method and provide a [`batchPredictionResourceUsageAssessmentConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.datasets/assess#BatchPredictionResourceUsageAssessmentConfig) .

    curl -X POST \
    -H "Authorization: Bearer $(gcloud auth print-access-token)" \
    -H "Content-Type: application/json" \
    "https://LOCATION-aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/LOCATION/datasets/DATASET_ID:assess" \
    -d '{
      "batchPredictionResourceUsageAssessmentConfig": {
        "modelName": "projects/PROJECT_ID/locations/LOCATION/models/gemini-2.5-flash"
      }
    }'

### Run the batch prediction job

You can use your multimodal dataset to do batch prediction by passing the BigQuery `table_id` of the assembled output:

### Google Gen AI SDK

    from google import genai
    from google.genai.types import HttpOptions
    
    # Attach the read configuration to the dataset.
    my_dataset.set_read_config(read_config=read_config)
    my_dataset = client.datasets.update_multimodal_dataset(multimodal_dataset=my_dataset)
    
    # Assemble the dataset to get the assembled BigQuery table.
    table_id, _ = client.datasets.assemble(name=my_dataset.name)
    
    genai_client = genai.Client(http_options=HttpOptions(api_version="v1"))
    
    job = genai_client.batches.create(
        model="gemini-2.5-flash",
        src=f"bq://{table_id}",
    )

For more information, see [Request a batch prediction job](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/capabilities/batch-prediction-gemini#request_a_batch_prediction_job) .

## Limitations

  - Multimodal datasets can be used with only generative AI features. They cannot be used with non-generative AI features such as [AutoML training](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/automl-training-overview) and [custom training](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/overview) .

  - Multimodal datasets can be used with only Google models such as Gemini. They cannot be used with third-party models.

## Pricing

When you tune a model or run a batch prediction job, you are billed for [Generative AI usage](https://cloud.google.com/gemini-enterprise-agent-platform/generative-ai/pricing) and querying the dataset in [BigQuery](https://cloud.google.com/bigquery/pricing) .

When you create, assemble, or assess your multimodal dataset, you are billed for storing and querying multimodal datasets in [BigQuery](https://cloud.google.com/bigquery/pricing) . Specifically, the following operations use those underlying services:

  - `Create` dataset
    
      - Datasets created from either an existing BigQuery table or DataFrame incur no additional storage costs. This is because we use a [logical view](https://docs.cloud.google.com/bigquery/docs/views-intro) instead of storing another copy of the data.
      - Datasets created from other sources copy the data to a new BigQuery table, which incurs storage costs in BigQuery. For example, active logical storage for $0.02 per GiB per month.

  - `Assemble` dataset
    
      - This method creates a new BigQuery table that contains the full dataset in model request format, which incurs storage costs in BigQuery. For example, active logical storage for $0.02 per GiB per month.
    
      - This method also reads the dataset once, which incurs query costs in BigQuery. For example, on-demand compute in pricing, $6.25 per TiB.

  - `Assess` reads the dataset once, which incurs query costs in BigQuery. For example, on-demand compute in pricing, $6.25 per TiB.

Use the [Pricing Calculator](https://cloud.google.com/products/calculator) to generate a cost estimate based on your projected usage.
