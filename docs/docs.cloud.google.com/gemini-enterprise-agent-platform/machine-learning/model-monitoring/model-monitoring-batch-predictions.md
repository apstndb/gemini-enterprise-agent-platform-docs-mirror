---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/model-monitoring/model-monitoring-batch-predictions
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/model-monitoring/model-monitoring-batch-predictions
title: Gemini Enterprise Agent Platform Model Monitoring for batch inferences
description: Explains how to set up batch inference job requests to include one-time Gemini Enterprise Agent Platform Model Monitoring analysis, which supports feature skew detection for both categorical and numerical input features.
data_source: docs.cloud.google.com
---

> **Preview**
> 
> This feature is covered by the [Pre-GA Offerings Terms](https://cloud.google.com/terms/service-terms#1) of the Google Cloud Terms of Service. For this feature, you can process personal data as outlined in the [Data Processing Security Terms](https://cloud.google.com/terms/data-processing-terms) , subject to the restrictions described in the [Google Cloud Terms of Service](https://cloud.google.com/terms/) . Pre-GA products and features might have limited support, and changes to pre-GA products and features might not be compatible with other pre-GA versions. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

This page describes how to configure [batch inference job requests](https://docs.cloud.google.com/vertex-ai/docs/predictions/get-batch-predictions) to include one-time Model Monitoring analysis. For batch inferences, Model Monitoring supports feature skew detection for categorical and numerical input features.

To create a batch inference job with Model Monitoring skew analysis, you must include both your batch inference input data and original training data for your model in the request. You can only add Model Monitoring analysis when creating new batch inference jobs.

For more information about skew, see [Introduction to Model Monitoring](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/model-monitoring/overview) .

For instructions on how to set up Model Monitoring for online (real-time) inferences, see [Using Model Monitoring](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/model-monitoring/using-model-monitoring) .

## Prerequisites

To use Model Monitoring with batch inferences, complete the following:

1.  Have an available model in Gemini Enterprise Agent Platform Model Registry that is either a [tabular AutoML](https://docs.cloud.google.com/vertex-ai/docs/start/automl-model-types#tabular) or tabular [custom training](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/overview) type.

2.  Upload your training data to [Cloud Storage](https://docs.cloud.google.com/storage/docs/uploading-objects) or [BigQuery](https://docs.cloud.google.com/bigquery/docs/loading-data) and obtain the URI link to the data.
    
      - For models trained with AutoML, you can use the [dataset id](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/datasets/export-metadata-annotations#export_a_dataset_using_the_or_the_api) for your training dataset instead.

3.  Model Monitoring compares the training data to the batch inference output. Make sure you use supported file formats for the training data and batch inference output:
    
    | Model type     | Training data                                    | Batch inference output                         |
    | -------------- | ------------------------------------------------ | ---------------------------------------------- |
    | Custom-trained | CSV, JSONL, BigQuery, TfRecord(tf.train.Example) | JSONL                                          |
    | AutoML tabular | CSV, JSONL, BigQuery, TfRecord(tf.train.Example) | CSV, JSONL, BigQuery, TfRecord(Protobuf.Value) |
    

4.  Optional: For custom-trained models, upload the [schema](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/model-monitoring/schemas#parse-batch-schemas) for your model to Cloud Storage. Model Monitoring requires the schema to calculate the baseline distribution for skew detection.

## Request a batch inference

You can use the following methods to add Model Monitoring configurations to batch inference jobs:

### Console

Follow the instructions to make a batch inference request with Model Monitoring enabled:

  - [Tabular AutoML classification and regression](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tabular-data/classification-regression/get-batch-predictions#make-batch-request)

  - [Tabular AutoML forecasting](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tabular-data/forecasting/get-predictions#make_a_batch_prediction_request_to_your_model)

  - [Tabular custom training](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/get-batch-predictions)

### REST API

Follow the instructions to make a batch inference request using the REST API:

  - [Tabular AutoML classification and regression](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tabular-data/classification-regression/get-batch-predictions#make-batch-request)

  - [Tabular AutoML forecasting](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tabular-data/forecasting/get-predictions#make_a_batch_prediction_request_to_your_model)

  - [Tabular custom training](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/get-batch-predictions)

When you create the batch inference request, add the following Model Monitoring configuration to the request JSON body:

    "modelMonitoringConfig": {
     "alertConfig": {
       "emailAlertConfig": {
         "userEmails": "EMAIL_ADDRESS"
       },
      "notificationChannels": [NOTIFICATION_CHANNELS]
     },
     "objectiveConfigs": [
       {
         "trainingDataset": {
           "dataFormat": "csv",
           "gcsSource": {
             "uris": [
               "TRAINING_DATASET"
             ]
           }
         },
         "trainingPredictionSkewDetectionConfig": {
           "skewThresholds": {
             "FEATURE_1": {
               "value": VALUE_1
             },
             "FEATURE_2": {
               "value": VALUE_2
             }
           }
         }
       }
     ]
    }

where:

  - EMAIL\_ADDRESS is the email address where you want to receive alerts from Model Monitoring. For example, `example@example.com` .

  - NOTIFICATION\_CHANNELS : a list of [Cloud Monitoring notification channels](https://docs.cloud.google.com/monitoring/support/notification-options) where you want to receive alerts from Model Monitoring. Use the resource names for the notification channels, which you can retrieve by [listing the notification channels in your project](https://docs.cloud.google.com/monitoring/alerts/using-channels-api#api-list-channels) . For example, `"projects/my-project/notificationChannels/1355376463305411567", "projects/my-project/notificationChannels/1355376463305411568"` .

  - TRAINING\_DATASET is the link to the training dataset stored in Cloud Storage.
    
      - To use a link to a BigQuery training dataset, replace the the `gcsSource` field with the following:
    
    <!-- end list -->
    
        "bigquerySource": {
            {
              "inputUri": "TRAINING_DATASET"
            }
         }
    
      - To use a link to an AutoML model, replace the `gcsSource` field with the following:
    
    <!-- end list -->
    
        "dataset": "TRAINING_DATASET"

  - FEATURE\_1 : VALUE\_1 and FEATURE\_2 : VALUE\_2 is the alerting threshold for each feature you want to monitor. For example, if you specify `Age=0.4` , Model Monitoring logs an alert when the [statistical distance](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/model-monitoring/overview#stat-distance) between the input and baseline distributions for the `Age` feature exceeds 0.4. By default, every categorical and numerical feature is monitored with threshold values of 0.3.

For more information about Model Monitoring configurations, see the [Monitoring job reference](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.modelDeploymentMonitoringJobs) .

### Python

See the [example notebook](https://colab.sandbox.google.com/github/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/model_monitoring/batch_prediction_model_monitoring.ipynb) to run a batch inference job with Model Monitoring for a custom tabular model.

Model Monitoring automatically notifies you of job updates and alerts through email.

## Access skew metrics

You can use the following methods to access skew metrics for batch inference jobs:

### Console (Histogram)

Use the Google Cloud console to view the feature distribution histograms for each monitored feature and learn which changes led to skew over time:

1.  Go to the **Batch predictions** page:

2.  On the **Batch predictions** page, click the batch inference job you want to analyze.

3.  Click the **Model Monitoring Alerts** tab to view a list of the model's input features, along with pertinent information, such as the alert threshold for each feature.

4.  To analyze a feature, click the name of the feature. A page shows the feature distribution histograms for that feature.
    
    Visualizing data distribution as histograms lets you quickly focus on the changes that occurred in the data. Afterward, you might decide to adjust your feature generation pipeline or retrain the model.
    
    ![Histograms showing example input data distribution and training data distribution for skew detection.](https://docs.cloud.google.com/static/gemini-enterprise-agent-platform/machine-learning/model-monitoring/images/skew_detection_distribution_bp.png)

### Console (JSON file)

Use the Google Cloud console to access the metrics in JSON format:

1.  Go to the **Batch predictions** page:

2.  Click the name of the batch inference monitoring job.

3.  Click the **Monitoring properties** tab.

4.  Click the **Monitoring output directory** link, which directs you to a Cloud Storage bucket.

5.  Click the **`metrics/`** folder.

6.  Click the **`skew/`** folder.

7.  Click the `feature_skew.json` file, which directs you to the **Object details** page.

8.  Open the JSON file using either option:

<!-- end list -->

  - Click **Download** and open the file in your local text editor.

  - Use the **gsutil URI** path to run ` gcloud storage cat gsutil_URI  ` in the Cloud Shell or your local terminal.

The `feature_skew.json` file includes a dictionary where the key is the feature name and the value is the feature skew. For example:

    {
      "cnt_ad_reward": 0.670936,
      "cnt_challenge_a_friend": 0.737924,
      "cnt_completed_5_levels": 0.549467,
      "month": 0.293332,
      "operating_system": 0.05758,
      "user_pseudo_id": 0.1
    }

### Python

See the [example notebook](https://colab.sandbox.google.com/github/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/model_monitoring/batch_prediction_model_monitoring.ipynb) to access skew metrics for a custom tabular model after running a batch inference job with Model Monitoring.

## Debug batch inference monitoring failures

If your batch inference monitoring job fails, you can find debugging logs in the Google Cloud console:

1.  Go to the **Batch predictions** page.

2.  Click the name of the failed batch inference monitoring job.

3.  Click the **Monitoring properties** tab.

4.  Click the **Monitoring output directory** link, which directs you to a Cloud Storage bucket.

5.  Click the **`logs/`** folder.

6.  Click either of the `.INFO` files, which directs you to the **Object details** page.

7.  Open the logs file using either option:
    
      - Click **Download** and open the file in your local text editor.
    
      - Use the **gsutil URI** path to run ` gcloud storage cat gsutil_URI  ` in the Cloud Shell or your local terminal.

## Notebook tutorials

Learn more about how to use Model Monitoring to get visualizations and statistics for models with these end-to-end tutorials.

### AutoML

  - [Model Monitoring for AutoML tabular models](https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/model_monitoring/get_started_with_model_monitoring_automl.ipynb)
  - [Model Monitoring for batch prediction in AutoML image models](https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/model_monitoring/get_started_with_model_monitoring_automl_image_batch.ipynb)
  - [Model Monitoring for online prediction in AutoML image models](https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/model_monitoring/get_started_with_model_monitoring_automl_image_online.ipynb)

### Custom

  - [Model Monitoring for custom tabular models](https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/model_monitoring/get_started_with_model_monitoring_custom.ipynb)
  - [Model Monitoring for custom tabular models with TensorFlow Serving container](https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/model_monitoring/get_started_with_model_monitoring_custom_tf_serving.ipynb)

### XGBoost models

  - [Gemini Enterprise Agent Platform Model Monitoring for XGBoost models](https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/model_monitoring/get_started_with_model_monitoring_xgboost.ipynb)

### Vertex Explainable AI feature attributions

  - [Gemini Enterprise Agent Platform Model Monitoring with Explainable AI Feature Attributions](https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/model_monitoring/model_monitoring.ipynb)

### Batch inference

  - [Gemini Enterprise Agent Platform batch prediction with Model Monitoring](https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/model_monitoring/batch_prediction_model_monitoring.ipynb)

### Setup for tabular models

  - [Gemini Enterprise Agent Platform Model Monitoring for setup for tabular models](https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/model_monitoring/get_started_with_model_monitoring_setup.ipynb)

## What's next

  - Learn how to use [Model Monitoring](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/model-monitoring/using-model-monitoring) .
  - Learn how Model Monitoring [calculates training-serving skew and inference drift](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/model-monitoring/overview) .
