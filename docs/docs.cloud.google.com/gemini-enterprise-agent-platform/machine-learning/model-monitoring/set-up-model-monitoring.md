---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/model-monitoring/set-up-model-monitoring
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/model-monitoring/set-up-model-monitoring
title: Set up model monitoring
description: Set up model monitoring for Gemini Enterprise Agent Platform Model Monitoring v2.
data_source: docs.cloud.google.com
---

> **Preview**
> 
> This feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](https://docs.cloud.google.com/terms/service-terms#1) . Pre-GA features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

Before you can start monitoring a model, you must register the model with Gemini Enterprise Agent Platform Model Registry and then configure monitoring details by creating a model monitor. This page describes how to register a model and explains all the specifications that you can define in a monitoring configuration.

Model Monitoring v2 supports tabular models only. These models can be served on Agent Platform or on other serving infrastructure.

## Register model

You can monitor models that are deployed on any serving infrastructure, such as on Agent Platform endpoints, GKE, or BigQuery. To register a model that you serve in Agent Platform, see [Import models](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/model-registry/import-model) .

For models that you serve outside of Agent Platform, you can register a *reference* model, which is a placeholder for models that are being served on other resources. When you register a reference model, you register the model's name, as shown in the following example:

### Python SDK

    model = aiplatform.Model.upload(
     display_name="MODEL_NAME"
    )

For reference models, Model Monitoring can support datasets from Cloud Storage or BigQuery. You cannot monitor feature attributions for reference models.

## Data sources

You can monitor metrics in data that is stored in the following sources. Nested features are not supported. To analyze nested data, flatten it first. If your data is in, for example, BigQuery, you can use SQL to transform nested features.

  - BigQuery  
    You can provide a BigQuery table URI or a SQL query. To specify a time window or to set up continuous monitoring, your table must include a timestamp column, which you specify in your dataset as `timestamp_field` .

  - Cloud Storage  
    Data must be stored in either the CSV or JSONL format. For CSV files, include a header of your column names as the first row in your file.

  - Agent Platform batch prediction jobs  
    Provide the fully qualified batch prediction job resource name to monitor a batch prediction job. You can run a monitoring job as soon as you create the batch prediction job; you don't have to wait for the batch job to complete. Model Monitoring v2 runs your monitoring job soon after the batch prediction job has completed.

  - Agent Platform endpoint logging  
    You must enable request-response logging on the endpoint before you can start monitoring it. Private endpoints aren't supported because they don't support request-response logging.
    
    Model Monitoring v2 expects the JSON format of Agent Platform endpoint requests and responses to follow the format used by the [`predict` method](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.endpoints/predict) . The `instances` objects are inserted to the logging table in the `request_payload` column as an array: `[INSTANCE_1, INSTANCE_2]` . Similarly, the `predictions` objects are inserted to the logging table in the `response_payload` column as an array: `[PREDICTION_1, PREDICTION_2]` .
    
    Other methods are supported (such as raw predict), but your data must follow the request and response JSON format as documented in the API reference for the [`predict` method](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.endpoints/predict) .

  - Agent Platform managed dataset  
    Datasets that are managed in Agent Platform. For more information, see the [tabular dataset format](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/using-managed-datasets#tabular_datasets) .

### Continuous monitoring

Continuous monitoring (also known as scheduled runs) lets you run monitoring jobs on a schedule that you set. Continuous model monitoring with [time specifications](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/model-monitoring/set-up-model-monitoring#time-spec) only supports BigQuery and Agent Platform endpoint logging as data sources.

To use BigQuery as a source for continuous monitoring with time specifications, your table must have a timestamp column. For BigQuery tables that were generated by Agent Platform endpoint logging, the tables already include a `logging_time` timestamp column.

As a general BigQuery optimization technique, we recommend that you [partition your table](https://docs.cloud.google.com/bigquery/docs/partitioned-tables) by timestamp to improve query performance and control costs by reducing the number of bytes read by a query.

### Supported data types

Both numerical and categorical features are supported. You can include columns with arrays, such as an array of boolean, categorical, string, or integer values. Model Monitoring v2 flattens the array so that each element in the array is a distinct value.

Numerical features maps to the following data types:

  - Float
  - Integer

Categorical features maps to the following data types:

  - Boolean
  - String
  - Categorical

## Model schema

Model Monitoring v2 uses the model schema to parse your data. This schema is required when you create a model monitor. For AutoML Tables, you don't need to specify the model schema; Gemini Enterprise Agent Platform Model Monitoring automatically fetches it.

The following example shows the general structure of the expected schema:

### Python SDK

    ml_monitoring.spec.ModelMonitoringSchema(
      feature_fields=[
          ml_monitoring.spec.FieldSchema(
              name="FEATURE_NAME",
              data_type="DATA_TYPE",
              repeated=BOOLEAN
          )
      ],
        prediction_fields = [
          model_monitor.spec.FieldSchema(
              name="PREDICTION_NAME",
              data_type="DATA_TYPE",
              repeated=BOOLEAN
          )
      ],
      ground_truth_fields = [
          model_monitor.spec.FieldSchema(
              feature="GROUND_TRUTH_NAME",
              data_type="DATA_TYPE",
              repeated=BOOLEAN
          )
      ]
    )

If a column includes an array of values, set `repeated` to `true` .

For AutoML Tables, when Model Monitoring v2 fetches the model schema, it uses the features that are in the training dataset as the input features, excluding the target column. The prediction output is set to the `predicted_{target_column}` column. Also, the Model Monitoring v2 extraction method for the prediction output value depends on the model type. For AutoML Tables classification models, Gemini Enterprise Agent Platform Model Monitoring monitors the argmax label distribution. For AutoML Tables regression models, Gemini Enterprise Agent Platform Model Monitoring monitors the value distribution.

## Baseline and target datasets

The baseline dataset represents a point of reference that you use to measure metrics over time. The target dataset includes more recent data that you use to compare against the baseline dataset. Model Monitoring v2 calculates the metrics between the two datasets to help you track the quality of your models. The baseline and target datasets can be from any supported data source.

As examples of targets and baselines, you can compare your serving dataset (target) with your model's training dataset (baseline), or you can compare your serving dataset (target) with a serving dataset from an earlier time period (baseline).

### Target dataset

When you select your target dataset, Model Monitoring v2 can process the entire dataset or you can set a *window* , which specifies the quantity of data for Model Monitoring v2 to examine. For example, if you specify a 24 hour window, Model Monitoring v2 compares only the latest 24 hours data against the baseline dataset.

For data drift analysis, the drift can be volatile if an inadequate volume data gets processed. A larger time window can help avoid alerts that were triggered as a result of low sample counts.

### Baseline dataset

You can set your baseline dataset to any supported data source, such as an Agent Platform managed dataset that contains your model's training data. Similar to target datasets, you can choose to have Model Monitoring v2 process the entire dataset or a particular window.

### Time specification

You can set monitoring time specifications through two methods:

  - Time range, which includes a start time and end time pair.
  - Time window and offset, which specifies the quantity of data to include and the time period between comparison datasets.

For example, in cases where you want to compare recent data with data that was collected previously, you can set an *offset* . The offset specifies the time period between the target and baseline datasets. As an example, imagine you set your target dataset with a one day window, and your baseline is set with an offset of one week also with a one day window.

In this case, the target dataset includes data from the 24 hours preceding the monitoring job's start time. The baseline dataset includes data from the same 24-hour period but exactly one week prior.

## Create a model monitor

Create a model monitor to associate monitoring details with a model version that has been registered in Gemini Enterprise Agent Platform Model Registry. The resulting resource is called a *model monitor* . You can create only one model monitor per model version.

When creating a model monitor, specify the model name, its version, and its schema. For some models, such as AutoML models, the schema is provided for you.

You can optionally set [monitoring objectives](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/model-monitoring/overview#v2-objectives) , a training dataset, monitoring output location, and notification settings in the model monitor. When you run a monitoring job, Model Monitoring v2 uses these settings as the defaults.

> **Note:** If you specify an output location, the monitoring service agent ( `service-PROJECT_NUMBER@gcp-sa-vertex-mm.iam.gserviceaccount.com` ) must have write access to that location. If you don't specify a location, Model Monitoring creates a default Cloud Storage bucket in your project to store monitoring results; you don't need to modify service agent permissions.

### Console

1.  In the Google Cloud console, go to the **Monitoring** page.

2.  Click **Configure monitoring** .

3.  Select a model and its version to monitor.

4.  If applicable, define the schema of your input features your prediction outputs and, if available, the ground truth.

5.  Optional: To monitor drift from your training dataset, specify the location of your dataset.

6.  Optional: To specify an existing Cloud Storage bucket for exporting monitoring results, expand **Advanced options** and then select a bucket.

7.  To configure monitoring objectives, click **Continue** or click **Set up** to create the model monitor.
    
    This configuration is used as the defaults when running a job.

8.  Select the objectives to monitor. For each objective, you can set the metric to monitor and a threshold for alerts.

9.  Specify the email addresses and, optionally, notification channels in Cloud Monitoring for monitoring alerts and notifications.

### Python SDK

    from vertexai.resources.preview import ml_monitoring
    from google.cloud.aiplatform_v1beta1.types import ExplanationSpec, ExplanationParameters, ExplanationMetadata
    
    # Define Monitoring Schema. For AutoML models, this is optional if the schema information is available.
    MONITORING_SCHEMA=ml_monitoring.spec.ModelMonitoringSchema(
      feature_fields=[
          ml_monitoring.spec.FieldSchema(
              name="sepal_length_cm",
              data_type="float"
          ),
          ml_monitoring.spec.FieldSchema(
              name="sepal_width_cm",
              data_type="float"
          ),
          ml_monitoring.spec.FieldSchema(
              name="petal_length_cm",
              data_type="float"
          ),
          ml_monitoring.spec.FieldSchema(
              name="petal_width_cm",
              data_type="float"
          )
      ],
      prediction_fields = [
          ml_monitoring.spec.FieldSchema(
              name="predicted_species",
              data_type="categorical"
          )
      ]
    )
    
    TRAINING_DATASET = ml_monitoring.spec.MonitoringInput(
      gcs_uri=GCS_INPUT_URI,
      data_format=DATA_FORMAT,
    )
    
    DEFAULT_FEATURE_DRIFT_SPEC=ml_monitoring.spec.DataDriftSpec(
      categorical_metric_type="l_infinity",
      numeric_metric_type="jensen_shannon_divergence",
      default_categorical_alert_threshold=0.1,
      default_numeric_alert_threshold=0.1,
    )
    
    DEFAULT_PREDICTION_OUTPUT_DRIFT_SPEC=ml_monitoring.spec.DataDriftSpec(
      categorical_metric_type="l_infinity",
      numeric_metric_type="jensen_shannon_divergence",
      default_categorical_alert_threshold=0.1,
      default_numeric_alert_threshold=0.1,
    )
    
    DEFAULT_FEATURE_ATTRIBUTION_SPEC=ml_monitoring.spec.FeatureAttributionSpec(
      default_alert_threshold=0.0003,
      feature_alert_thresholds={"sepal_length_cm":0.0001},
    )
    
    EXPLANATION_SPEC=ExplanationSpec(
      parameters=ExplanationParameters(
          {"sampled_shapley_attribution": {"path_count": 2}}
      ),
      metadata=ExplanationMetadata(
          inputs={
              "sepal_length_cm": ExplanationMetadata.InputMetadata({
                  "input_tensor_name": "sepal_length_cm",
                  "encoding": "IDENTITY",
                  "modality": "numeric",
              }),
              ...
          },
          ...
      )
    )
    
    DEFAULT_OUTPUT_SPEC = ml_monitoring.spec.output.OutputSpec(
      gcs_base_dir=GCS_OUTPUT_BASE_DIR
    )
    
    DEFAULT_NOTIFICATION_SPEC = ml_monitoring.spec.NotificationSpec(
      user_emails=['email@example.com']
    )
    
    my_model_monitor = ml_monitoring.ModelMonitor.create(
      display_name=MONITORING_JOB_DISPLAY_NAME,
      model_name=MODEL_RESOURCE_NAME,
      model_version_id=MODEL_VERSION_ID,
      model_monitoring_schema=MONITORING_SCHEMA,
      # The following fields are optional for creating the model monitor.
      training_dataset=TRAINING_DATASET,
      tabular_objective_spec=ml_monitoring.spec.TabularObjective(
          feature_drift_spec=DEFAULT_FEATURE_DRIFT_SPEC,
          prediction_output_drift_spec=DEFAULT_PREDICTION_OUTPUT_DRIFT_SPEC,
          feature_attribution_spec=DEFAULT_FEATURE_ATTRIBUTION_SPEC,
      ),
      explanation_spec=DEFAULT_FEATURE_ATTRIBUTION_SPEC,
      output_spec=DEFAULT_OUTPUT_SPEC,
      notification_spec=DEFAULT_NOTIFICATION_SPEC
    )
