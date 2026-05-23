---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/pipelines/gcpc-label-propagation
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/pipelines/gcpc-label-propagation
title: Resource labeling by Gemini Enterprise Agent Platform Pipelines
description: Understand resourcelabel and metadata propagation through resources generated from {{dynamic_data.site_values.cloud_name}} Pipeline Components.
data_source: docs.cloud.google.com
---

Depending on the type of component, resource, and the Google Cloud Pipeline Components SDK version, Agent Platform Pipelines either automatically propagates the labels from your pipeline run to the resources generated from Google Cloud Pipeline Components or requires you to label the generated resources. For user-defined components, you need to author your component code to attach the labels from an environment variable. For more information, see [Resources generated from user-defined components](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/pipelines/gcpc-label-propagation#user_defined_components) .

## Resources with automatic labeling

Agent Platform Pipelines automatically labels the following resources, regardless of the Google Cloud Pipeline Components SDK version:

### `CustomJob` resources

Agent Platform Pipelines automatically propagates the labels from your pipeline run to [`CustomJob`](https://docs.cloud.google.com/vertex-ai/docs/pipelines/customjob-component) resources. This is supported by the following components in all versions of the Google Cloud Pipeline Components SDK:

  - [`CustomTrainingJobOp`](https://google-cloud-pipeline-components.readthedocs.io/en/google-cloud-pipeline-components-2.22.0/api/v1/custom_job.html#v1.custom_job.CustomTrainingJobOp)

  - [`create_custom_training_job_from_component`](https://google-cloud-pipeline-components.readthedocs.io/en/google-cloud-pipeline-components-2.22.0/api/v1/custom_job.html#v1.custom_job.create_custom_training_job_from_component)

  - [`ForecastingValidationOp`](https://google-cloud-pipeline-components.readthedocs.io/en/google-cloud-pipeline-components-2.22.0/api/v1/forecasting.html#v1.forecasting.ForecastingValidationOp)

  - [`ForecastingPrepareDataForTrainOp`](https://google-cloud-pipeline-components.readthedocs.io/en/google-cloud-pipeline-components-2.22.0/api/v1/forecasting.html#v1.forecasting.ForecastingPrepareDataForTrainOp)

## Resources with automatic labeling in Google Cloud Pipeline Components SDK v1.0.31 or later

Agent Platform Pipelines automatically labels the following resources if you use Google Cloud Pipeline Components SDK v1.0.31 or later:

### `BatchPredictionJob` resources

Agent Platform Pipelines automatically propagates labels from your pipeline run to `BatchPredictionJob` resources generated from the [`ModelBatchPredictOp`](https://google-cloud-pipeline-components.readthedocs.io/en/google-cloud-pipeline-components-2.22.0/api/v1/batch_predict_job.html#v1.batch_predict_job.ModelBatchPredictOp) component if you use v1.0.31 or later of the Google Cloud Pipeline Components SDK.

### Gemini Enterprise `endpoint` resources

Agent Platform Pipelines automatically propagates labels from your pipeline run to Gemini Enterprise API `endpoint` resources generated from the [`EndpointCreateOp`](https://google-cloud-pipeline-components.readthedocs.io/en/google-cloud-pipeline-components-2.22.0/api/v1/endpoint.html#v1.endpoint.EndpointCreateOp) component if you use v1.0.31 or later of the Google Cloud Pipeline Components SDK.

### `HyperparameterTuningJob` resources

Agent Platform Pipelines automatically propagates labels from your pipeline run to `HyperparameterTuningJob` resources generated from the [`HyperparameterTuningJobRunOp`](https://google-cloud-pipeline-components.readthedocs.io/en/google-cloud-pipeline-components-2.22.0/api/v1/hyperparameter_tuning_job.html#v1.hyperparameter_tuning_job.HyperparameterTuningJobRunOp) component if you use v1.0.31 or later of the Google Cloud Pipeline Components SDK.

### Gemini Enterprise API dataset resources

Agent Platform Pipelines automatically propagates labels from your pipeline run to Gemini Enterprise API dataset resources generated from the following [Gemini Enterprise API components](https://docs.cloud.google.com/vertex-ai/docs/pipelines/vertex-automl-component#dataset_operators) if you use v1.0.31 or later of the Google Cloud Pipeline Components SDK:

  - [`ImageDatasetCreateOp`](https://google-cloud-pipeline-components.readthedocs.io/en/google-cloud-pipeline-components-2.22.0/api/v1/dataset.html#v1.dataset.ImageDatasetCreateOp)

  - [`TabularDatasetCreateOp`](https://google-cloud-pipeline-components.readthedocs.io/en/google-cloud-pipeline-components-2.22.0/api/v1/dataset.html#v1.dataset.TabularDatasetCreateOp)

  - [`TextDatasetCreateOp`](https://google-cloud-pipeline-components.readthedocs.io/en/google-cloud-pipeline-components-2.22.0/api/v1/dataset.html#v1.dataset.TextDatasetCreateOp)

  - [`TimeSeriesDatasetCreateOp`](https://google-cloud-pipeline-components.readthedocs.io/en/google-cloud-pipeline-components-2.22.0/api/v1/dataset.html#v1.dataset.TimeSeriesDatasetCreateOp)

  - [`VideoDatasetCreateOp`](https://google-cloud-pipeline-components.readthedocs.io/en/google-cloud-pipeline-components-2.22.0/api/v1/dataset.html#v1.dataset.VideoDatasetCreateOp)

### Google Cloud BigQuery Job resources

Agent Platform Pipelines automatically propagates labels from your pipeline run to Google Cloud BigQuery Job resources resources generated from any of the [BigQuery ML components](https://docs.cloud.google.com/vertex-ai/docs/pipelines/gcpc-list#bqml_components) if you use v1.0.31 or later of the Google Cloud Pipeline Components SDK.

### Google Cloud Managed Service for Apache Spark Job resources

Agent Platform Pipelines automatically propagates labels from your pipeline run to Google Cloud Managed Service for Apache Spark Job resources resources generated from any of the [Managed Service for Apache Spark components](https://docs.cloud.google.com/vertex-ai/docs/pipelines/gcpc-list#dataproc_sl_components) if you use v1.0.31 or later of the Google Cloud Pipeline Components SDK.

### `TrainingPipeline` and `Model` resources

Agent Platform Pipelines automatically propagates labels from your pipeline run to `TrainingPipeline` and `Model` resources resources generated from the following [AutoML components](https://docs.cloud.google.com/vertex-ai/docs/pipelines/gcpc-list#experimental_automl_components) if you use v1.0.31 or later of the Google Cloud Pipeline Components SDK:

  - [`AutoMLImageTrainingJobRunOp`](https://google-cloud-pipeline-components.readthedocs.io/en/google-cloud-pipeline-components-2.22.0/api/v1/automl/training_job.html#v1.automl.training_job.AutoMLImageTrainingJobRunOp)

  - [`AutoMLTextTrainingJobRunOp`](https://google-cloud-pipeline-components.readthedocs.io/en/google-cloud-pipeline-components-2.22.0/api/v1/automl/training_job.html#v1.automl.training_job.AutoMLTextTrainingJobRunOp)

  - [`AutoMLVideoTrainingJobRunOp`](https://google-cloud-pipeline-components.readthedocs.io/en/google-cloud-pipeline-components-2.22.0/api/v1/automl/training_job.html#v1.automl.training_job.AutoMLVideoTrainingJobRunOp)

  - [`AutoMLForecastingTrainingJobRunOp`](https://google-cloud-pipeline-components.readthedocs.io/en/google-cloud-pipeline-components-2.22.0/api/v1/automl/training_job.html#v1.automl.training_job.AutoMLForecastingTrainingJobRunOp)

### Google Cloud BigQuery table resources

Agent Platform Pipelines automatically propagates labels from your pipeline run Google Cloud BigQuery table resources resources generated from the [`ForecastingPreprocessingOp`](https://google-cloud-pipeline-components.readthedocs.io/en/google-cloud-pipeline-components-2.22.0/api/v1/forecasting.html#v1.forecasting.ForecastingPreprocessingOp) component if you use v1.0.31 or later of the Google Cloud Pipeline Components SDK.

## Resources without automatic labeling

Agent Platform Pipelines doesn't label the following resources automatically, regardless of the Google Cloud Pipeline Components SDK version:

### Google Cloud Dataflow resources

Agent Platform Pipelines doesn't automatically label Dataflow resources generated by the [`DataflowPythonJobOp`](https://google-cloud-pipeline-components.readthedocs.io/en/google-cloud-pipeline-components-2.22.0/api/v1/dataflow.html#v1.dataflow.DataflowPythonJobOp) component. You can include instructions in your code to label the resources.

Use the following code sample to propagate billing labels from your pipeline run to any Google Cloud Dataflow resource generated using the [`DataflowPythonJobOp`](https://google-cloud-pipeline-components.readthedocs.io/en/google-cloud-pipeline-components-2.22.0/api/v1/dataflow.html#v1.dataflow.DataflowPythonJobOp) component:

``` 
  import argparse
  import apache_beam as beam
  ...
  def run(argv=None):
    parser = argparse.ArgumentParser()
    # Don't add `--labels` to the argument list, so that they will be passed to the pipeline_options 
    parser.add_argument('--input', …)
    parser.add_argument('--output', …)
  ...
    known_args, pipeline_args = parser.parse_known_args(argv)
    pipeline_options = PipelineOptions(pipeline_args)
    with beam.Pipeline(options=pipeline_options) as p:
```

### Resources generated from user-defined components

Agent Platform Pipelines doesn't automatically label Google Cloud resources generated from user-defined components. You can include instructions in your code to retrieve the labels from the environment variable `VERTEX_AI_PIPELINES_RUN_LABELS` and attach those labels to the Google Cloud resources generated using the component at runtime.

The environment variable `VERTEX_AI_PIPELINE_RUN_LABELS` contains the labels in JSON format as key-value pairs.

For example: `{ "label1_key": "label1_value", "label2_key": "label2_value", ...}`

If you're using the Agent Platform SDK for Python, use the following code sample in your component code to propagate labels from the environment variable to a new resource generated from the component:

    import os
    import json
    from google.cloud import aiplatform
    
    aiplatform.init(
      project='PROJECT_ID',
      location='LOCATION'
    )
    
    aiplatform.RESOURCE.create(
      ...ß
      json.loads(os.getenv("VERTEX_AI_PIPELINES_RUN_LABELS"))
    )

Replace the following:

  - PROJECT\_ID : The Google Cloud project containing the pipeline run.

  - LOCATION : The location of the pipeline run.

  - RESOURCE : Google Cloud resource generated from the component, for example, `CustomJob` or `Model` .

You can also use the `gcp_labels_util.attach_system_labels` utility if you want to use Python to parse the environment variable. You can use this utility only if you have access to the Google Cloud Pipeline Components library and are using Python. For more information, see the [source code of the utility function in GitHub](https://github.com/kubeflow/pipelines/blob/master/components/google-cloud/google_cloud_pipeline_components/container/v1/gcp_launcher/utils/gcp_labels_util.py) .

## Resources without labeling support

Agent Platform Pipelines doesn't support billing label propagation to the following resources:

### ML Metadata resources

ML Metadata resources are billed at the store level. You can't use billing labels to understand the resource-level cost.

### Cloud Storage resources

Agent Platform Pipelines doesn't propagate billing labels to Cloud Storage resources, such as Cloud Storage buckets.

## What's next

  - [Understand pipeline run costs](https://docs.cloud.google.com/vertex-ai/docs/pipelines/understand-pipeline-cost-labels)
