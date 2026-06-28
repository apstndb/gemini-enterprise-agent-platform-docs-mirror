---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/model-monitoring/using-model-monitoring
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/model-monitoring/using-model-monitoring
title: Monitor feature skew and drift
description: Use Gemini Enterprise Agent Platform Model Monitoring to detect drift and training-prediction skew.
data_source: docs.cloud.google.com
---

> To learn more, run the "Use Model Monitoring to detect drift and training-prediction skew." notebook in one of the following environments:
> 
> [![](https://docs.cloud.google.com/static/vertex-ai/images/colab-logo-32px.png) Open in Colab](https://colab.research.google.com/github/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/model_monitoring/model_monitoring.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/colab-enterprise-logo-32px.png) Open in Colab Enterprise](https://console.cloud.google.com/agent-platform/colab/import/https%3A%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Fmodel_monitoring%2Fmodel_monitoring.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/vertex-ai-workbench-logo-32px.png) Open in Agent Platform Workbench](https://console.cloud.google.com/agent-platform/workbench/deploy-notebook?download_url=https%3A%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Fmodel_monitoring%2Fmodel_monitoring.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/github-logo-32px.png) View on GitHub](https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/model_monitoring/model_monitoring.ipynb)

This page describes how to create, manage, and interpret the results of Model Monitoring jobs for models deployed to online prediction endpoints. Gemini Enterprise Agent Platform Model Monitoring supports feature skew and drift detection for categorical and numerical input features.

When a model is deployed in production with Model Monitoring enabled, incoming prediction requests are logged in a BigQuery table in your Google Cloud project. The input feature values contained in the logged requests are then analyzed for skew or drift.

You can enable skew detection if you provide the original training dataset for your model; otherwise, you should enable drift detection. For more information, see [Introduction to Gemini Enterprise Agent Platform Model Monitoring](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/model-monitoring/overview) .

## Prerequisites

To use Model Monitoring, complete the following:

1.  Have an available model in Agent Platform that is either a [tabular AutoML](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/start/automl-model-types#tabular) or imported tabular [custom training](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/overview) type.
    
      - If you are using an existing endpoint, make sure all the models deployed under the endpoint are tabular AutoML or imported custom training types.

2.  If you are enabling skew detection, upload your training data to [Cloud Storage](https://docs.cloud.google.com/storage/docs/uploading-objects) or [BigQuery](https://docs.cloud.google.com/bigquery/docs/loading-data) and obtain the URI link to the data. For drift detection, training data is not required.

3.  Optional: For custom-trained models, upload the [analysis instance schema](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/model-monitoring/schemas) for your model to Cloud Storage. Model Monitoring requires the schema to begin the monitoring process and calculate the baseline distribution for skew detection. If you don't provide the schema during job creation, the job remains in a pending state until Model Monitoring can automatically parse the schema from the first 1000 prediction requests the model receives.

## Create a Model Monitoring job

To set up either skew detection or drift detection, create a model deployment monitoring job:

### Console

To create a model deployment monitoring job using the Google Cloud console, create an endpoint:

> **Note:** To enable model monitoring for an existing endpoint, [edit the endpoint's settings](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/model-monitoring/using-model-monitoring#update-model-monitoring-job) .

1.  In the Google Cloud console, go to the **Agent Platform Endpoints** page.

2.  Click **Create Endpoint** .

3.  In the **New endpoint** pane, name your endpoint and set a region.

4.  Click **Continue** .

5.  In the **Model name** field, select an imported custom training or tabular AutoML model.

6.  In the **Version** field, select a version for your model.

7.  Click **Continue** .

8.  In the **Model monitoring** pane, make sure **Enable model monitoring for this endpoint** is toggled on. Any monitoring settings you configure apply to all models deployed to the endpoint.

9.  Enter a **Monitoring job display name** .

10. Enter a **Monitoring window length** .

11. For **Notification emails** , enter one or more comma-separated email addresses to receive alerts when a model exceeds an alerting threshold.

12. (Optional) For **Notification channels** , add [Cloud Monitoring](https://docs.cloud.google.com/monitoring/support/notification-options) channels to receive alerts when a model exceeds an alerting threshold. You can select existing Cloud Monitoring channels or create a new one by clicking **Manage notification channels** . The Console supports PagerDuty, Slack, and Pub/Sub notification channels.

13. Enter a **Sampling rate** .

14. Optional: Enter the **Prediction input schema** and **Analysis input schema** .

15. Click **Continue** . The **Monitoring objective** pane opens, with options for skew or drift detection:
    
    ### Skew detection
    
    1.  Select **Training-serving skew detection** .
    2.  Under **Training data source** , provide a training data source.
    3.  Under **Target column** , enter the column name from the training data that the model is trained to predict. This field is excluded from the monitoring analysis.
    4.  Optional: Under **Alert thresholds** , specify thresholds at which to trigger alerts. For information about how to format the thresholds, hold the pointer over the help Help icon.
    5.  Click **Create** .
    
    ### Drift detection
    
    1.  Select **Prediction drift detection** .
    2.  Optional: Under **Alert thresholds** , specify thresholds at which to trigger alerts. For information about how to format the thresholds, hold the pointer over the help Help icon.
    3.  Click **Create** .

### gcloud

To create a model deployment monitoring job using the gcloud CLI, first deploy your model to an endpoint:

  - [Deploy an AutoML tabular classification/regression model](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tabular-data/classification-regression/get-online-predictions#deploy-model) .

  - [Deploy a custom tabular model](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/deployment) .

A monitoring job configuration applies to all deployed models under an endpoint.

Run the [`gcloud ai model-monitoring-jobs create`](https://docs.cloud.google.com/sdk/gcloud/reference/ai/model-monitoring-jobs/create) command.

    gcloud ai model-monitoring-jobs create \
      --project=PROJECT_ID \
      --region=REGION \
      --display-name=MONITORING_JOB_NAME \
      --emails=EMAIL_ADDRESS_1,EMAIL_ADDRESS_2 \
      --endpoint=ENDPOINT_ID \
      [--feature-thresholds=FEATURE_1=THRESHOLD_1, FEATURE_2=THRESHOLD_2] \
      [--prediction-sampling-rate=SAMPLING_RATE] \
      [--monitoring-frequency=MONITORING_FREQUENCY] \
      [--analysis-instance-schema=ANALYSIS_INSTANCE_SCHEMA] \
      --target-field=TARGET_FIELD \
      --bigquery-uri=BIGQUERY_URI

where:

  - PROJECT\_ID is the ID of your Google Cloud project. For example, `my-project` .

  - REGION is the location for your monitoring job. For example, `us-central1` .

  - MONITORING\_JOB\_NAME is the name of your monitoring job. For example, `my-job` .

  - EMAIL\_ADDRESS is the email address where you want to receive alerts from Model Monitoring. For example, `example@example.com` .

  - ENDPOINT\_ID is the ID of the endpoint under which your model is deployed. For example, `1234567890987654321` .

  - Optional: FEATURE\_1=THRESHOLD\_1 is the alerting threshold for each feature you want to monitor. For example, if you specify `Age=0.4` , Model Monitoring logs an alert when the [statistical distance](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/model-monitoring/overview#stat-distance) between the input and baseline distributions for the `Age` feature exceeds 0.4. By default, every categorical and numerical feature is monitored with threshold values of 0.3.

  - Optional: SAMPLING\_RATE is the fraction of the incoming prediction requests you want to log. For example, `0.5` . If not specified, Model Monitoring logs all prediction requests.

  - Optional: MONITORING\_FREQUENCY is the frequency at which you want the monitoring job to run on recently logged inputs. The minimum granularity is 1 hour. The default is 24 hours. For example, `2` .

  - Optional: ANALYSIS\_INSTANCE\_SCHEMA is the Cloud Storage URI for the schema file that describes the format of your input data. For example, `gs://test-bucket/schema.yaml` .

  - (required only for skew detection) TARGET\_FIELD is the field that is being predicted by the model. This field is excluded from the monitoring analysis. For example, `housing-price` .

  - (required only for skew detection) BIGQUERY\_URI is the link to the training dataset stored in BigQuery, using the following format:
    
        bq://\PROJECT.\DATASET.\TABLE
    
    For example, `bq://\my-project.\housing-data.\san-francisco` .
    
    You can replace the `bigquery-uri` flag with alternative links to your training dataset:
    
      - For a CSV file stored in a Cloud Storage bucket, use ` --data-format=csv --gcs-uris=gs:// BUCKET_NAME / OBJECT_NAME  ` .
    
      - For a TFRecord file stored in a Cloud Storage bucket, use ` --data-format=tf-record --gcs-uris=gs:// BUCKET_NAME / OBJECT_NAME  ` .
    
      - For a [tabular AutoML managed dataset](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/datasets/export-metadata-annotations#exporting_a_dataset_using_the_or_the_api) , use ` --dataset= DATASET_ID  ` .

### Python SDK

For information about the full end-to-end Model Monitoring API workflow, see the [example notebook](https://colab.research.google.com/github/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/model_monitoring/model_monitoring.ipynb) .

### REST API

1.  If you haven't done so already, deploy your model to an endpoint. During the **Get the endpoint ID** step in the model deployment instructions, note the `deployedModels.id` value in the JSON response for later use:
    
      - [Deploy an AutoML tabular classification/regression model](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tabular-data/classification-regression/get-online-predictions#deploy-model) .
    
      - [Deploy a custom tabular model](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/deployment) .

2.  Create a model monitoring job request. The instructions below show how to create a basic monitoring job for drift detection. To customize the JSON request, see the [Monitoring job reference](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.modelDeploymentMonitoringJobs) .
    
    Before using any of the request data, make the following replacements:
    
      - PROJECT\_ID : is the ID of your Google Cloud project. For example, `my-project` .
      - LOCATION : is the location for your monitoring job. For example, `us-central1` .
      - MONITORING\_JOB\_NAME : is the name of your monitoring job. For example, `my-job` .
      - PROJECT\_NUMBER : is the number for your Google Cloud project. For example, `1234567890` .
      - ENDPOINT\_ID is the ID for the endpoint to which your model is deployed. For example, `1234567890` .
      - DEPLOYED\_MODEL\_ID : is the ID for the deployed model.
      - FEATURE : VALUE is the alerting threshold for each feature you want to monitor. For example, if you specify `"Age": {"value": 0.4}` , Model Monitoring logs an alert when the [statistical distance](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/model-monitoring/overview#stat-distance) between the input and baseline distributions for the `Age` feature exceeds 0.4. By default, every categorical and numerical feature is monitored with threshold values of 0.3.
      - EMAIL\_ADDRESS : is the email address where you want to receive alerts from Model Monitoring. For example, `example@example.com` .
      - NOTIFICATION\_CHANNELS : a list of [Cloud Monitoring notification channels](https://docs.cloud.google.com/monitoring/support/notification-options) where you want to receive alerts from Model Monitoring. Use the resource names for the notification channels, which you can retrieve by [listing the notification channels in your project](https://docs.cloud.google.com/monitoring/alerts/using-channels-api#api-list-channels) . For example, `"projects/my-project/notificationChannels/1355376463305411567", "projects/my-project/notificationChannels/1355376463305411568"` .
      - Optional: ANALYSIS\_INSTANCE\_SCHEMA is the Cloud Storage URI for the schema file that describes the format of your input data. For example, `gs://test-bucket/schema.yaml` .
    
    Request JSON body:
    
        {
          "displayName":"MONITORING_JOB_NAME",
          "endpoint":"projects/PROJECT_NUMBER/locations/LOCATION/endpoints/ENDPOINT_ID",
          "modelDeploymentMonitoringObjectiveConfigs": {
             "deployedModelId": "DEPLOYED_MODEL_ID",
             "objectiveConfig":  {
                "predictionDriftDetectionConfig": {
                    "driftThresholds": {
                      "FEATURE_1": {
                        "value": VALUE_1
                       },
                      "FEATURE_2": {
                        "value": VALUE_2
                       }
                    }
                 },
              },
          },
          "loggingSamplingStrategy": {
             "randomSampleConfig":  {
                "sampleRate":  0.5,
             },
          },
          "modelDeploymentMonitoringScheduleConfig": {
             "monitorInterval": {
                "seconds": 3600,
             },
          },
          "modelMonitoringAlertConfig": {
             "emailAlertConfig": {
                "userEmails": ["EMAIL_ADDRESS"],
             },
             "notificationChannels": [NOTIFICATION_CHANNELS]
          },
          "analysisInstanceSchemaUri": ANALYSIS_INSTANCE_SCHEMA
        }
    
    To send your request, expand one of these options:
    
    #### curl (Linux, macOS, or Cloud Shell)
    
    > **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) , or by using [Cloud Shell](https://docs.cloud.google.com/shell/docs) , which automatically logs you into the `gcloud` CLI . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .
    
    Save the request body in a file named `request.json` . Run the following command in the terminal to create or overwrite this file in the current directory:
    
        cat > request.json << 'EOF'
        {
          "displayName":"MONITORING_JOB_NAME",
          "endpoint":"projects/PROJECT_NUMBER/locations/LOCATION/endpoints/ENDPOINT_ID",
          "modelDeploymentMonitoringObjectiveConfigs": {
             "deployedModelId": "DEPLOYED_MODEL_ID",
             "objectiveConfig":  {
                "predictionDriftDetectionConfig": {
                    "driftThresholds": {
                      "FEATURE_1": {
                        "value": VALUE_1
                       },
                      "FEATURE_2": {
                        "value": VALUE_2
                       }
                    }
                 },
              },
          },
          "loggingSamplingStrategy": {
             "randomSampleConfig":  {
                "sampleRate":  0.5,
             },
          },
          "modelDeploymentMonitoringScheduleConfig": {
             "monitorInterval": {
                "seconds": 3600,
             },
          },
          "modelMonitoringAlertConfig": {
             "emailAlertConfig": {
                "userEmails": ["EMAIL_ADDRESS"],
             },
             "notificationChannels": [NOTIFICATION_CHANNELS]
          },
          "analysisInstanceSchemaUri": ANALYSIS_INSTANCE_SCHEMA
        }
        EOF
    
    Then execute the following command to send your REST request:
    
        curl -X POST \
             -H "Authorization: Bearer $(gcloud auth print-access-token)" \
             -H "Content-Type: application/json; charset=utf-8" \
             -d @request.json \
             "https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/modelDeploymentMonitoringJobs"
    
    #### PowerShell (Windows)
    
    > **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .
    
    Save the request body in a file named `request.json` . Run the following command in the terminal to create or overwrite this file in the current directory:
    
        @'
        {
          "displayName":"MONITORING_JOB_NAME",
          "endpoint":"projects/PROJECT_NUMBER/locations/LOCATION/endpoints/ENDPOINT_ID",
          "modelDeploymentMonitoringObjectiveConfigs": {
             "deployedModelId": "DEPLOYED_MODEL_ID",
             "objectiveConfig":  {
                "predictionDriftDetectionConfig": {
                    "driftThresholds": {
                      "FEATURE_1": {
                        "value": VALUE_1
                       },
                      "FEATURE_2": {
                        "value": VALUE_2
                       }
                    }
                 },
              },
          },
          "loggingSamplingStrategy": {
             "randomSampleConfig":  {
                "sampleRate":  0.5,
             },
          },
          "modelDeploymentMonitoringScheduleConfig": {
             "monitorInterval": {
                "seconds": 3600,
             },
          },
          "modelMonitoringAlertConfig": {
             "emailAlertConfig": {
                "userEmails": ["EMAIL_ADDRESS"],
             },
             "notificationChannels": [NOTIFICATION_CHANNELS]
          },
          "analysisInstanceSchemaUri": ANALYSIS_INSTANCE_SCHEMA
        }
        '@  | Out-File -FilePath request.json -Encoding utf8
    
    Then execute the following command to send your REST request:
    
        $cred = gcloud auth print-access-token
        $headers = @{ "Authorization" = "Bearer $cred" }
        
        Invoke-WebRequest `
            -Method POST `
            -Headers $headers `
            -ContentType: "application/json; charset=utf-8" `
            -InFile request.json `
            -Uri "https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/modelDeploymentMonitoringJobs" | Select-Object -Expand Content
    
    You should receive a JSON response similar to the following:
    
        {
          "name": "projects/PROJECT_NUMBER/locations/LOCATION/modelDeploymentMonitoringJobs/MONITORING_JOB_NUMBER",
          ...
          "state": "JOB_STATE_PENDING",
          "scheduleState": "OFFLINE",
          ...
          "bigqueryTables": [
            {
              "logSource": "SERVING",
              "logType": "PREDICT",
              "bigqueryTablePath": "bq://PROJECT_ID.model_deployment_monitoring_8451189418714202112.serving_predict"
            }
          ],
          ...
        }

After the monitoring job is created, Model Monitoring logs incoming prediction requests in a generated BigQuery table named `  PROJECT_ID .model_deployment_monitoring_ ENDPOINT_ID .serving_predict ` . If [request-response logging](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/online-prediction-logging#model-monitoring) is enabled, Model Monitoring logs incoming requests in the same BigQuery table that is used for request-response logging.

### (Optional) Configure alerts for the Model Monitoring job

You can monitor and debug your Model Monitoring job through alerts. Model Monitoring automatically notifies you of job updates through email, but you can also set up alerts through Cloud Logging and Cloud Monitoring notification channels.

### Email

For the following events, Model Monitoring sends an email notification to each email address you specified when creating the Model Monitoring job:

  - Each time skew or drift detection is set up.
  - Each time an existing Model Monitoring job configuration is updated.
  - Each time a scheduled monitoring pipeline run fails.

### Cloud Logging

To enable logs for scheduled monitoring pipeline runs, set the `enableMonitoringPipelineLogs` field in your [`modelDeploymentMonitoringJobs`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.modelDeploymentMonitoringJobs) configuration to `true` . Debugging logs are written to Cloud Logging when the monitoring job is set up and at each monitoring interval.

The debugging logs are written to Cloud Logging with the log name: `model_monitoring` . For example:

    logName="projects/model-monitoring-demo/logs/aiplatform.googleapis.com%2Fmodel_monitoring" resource.labels.model_deployment_monitoring_job=6680511704087920640

Here is an example of a job progress log entry:

    {
    "insertId": "e2032791-acb9-4d0f-ac73-89a38788ccf3@a1",
    "jsonPayload": {
      "@type": "type.googleapis.com/google.cloud.aiplatform.logging.ModelMonitoringPipelineLogEntry",
      "statusCode": {
        "message": "Scheduled model monitoring pipeline finished successfully for job projects/677687165274/locations/us-central1/modelDeploymentMonitoringJobs/6680511704087920640"
      },
      "modelDeploymentMonitoringJob": "projects/677687165274/locations/us-central1/modelDeploymentMonitoringJobs/6680511704087920640"
    },
    "resource": {
      "type": "aiplatform.googleapis.com/ModelDeploymentMonitoringJob",
      "labels": {
        "model_deployment_monitoring_job": "6680511704087920640",
        "location": "us-central1",
        "resource_container": "projects/677687165274"
      }
    },
    "timestamp": "2022-02-04T15:33:54.778883Z",
    "severity": "INFO",
    "logName": "projects/model-monitoring-demo/logs/staging-aiplatform.sandbox.googleapis.com%2Fmodel_monitoring",
    "receiveTimestamp": "2022-02-04T15:33:56.343298321Z"
    }

### Notification channels

Each time a scheduled monitoring pipeline run fails, Model Monitoring sends a notification to the Cloud Monitoring notification channels you specified when creating the Model Monitoring job.

## Configure alerts for feature anomalies

Model Monitoring detects an anomaly when the threshold set for a feature is exceeded. Model Monitoring automatically notifies you of detected anomalies through email, but you can also set up alerts through Cloud Logging and Cloud Monitoring notification channels.

### Email

At each monitoring interval, if the threshold of at least one feature exceeds the threshold, Model Monitoring sends an email alert to each email address you specified when creating the Model Monitoring job. The email message includes the following:

  - The time at which the monitoring job ran.
  - The name of the feature that has skew or drift.
  - The alerting threshold as well as the recorded statistical distance measure.

### Cloud Logging

To enable Cloud Logging alerts, set the `enableLogging` field of your [`ModelMonitoringAlertConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.modelDeploymentMonitoringJobs#ModelMonitoringAlertConfig) configuration to `true` .

At each monitoring interval, an anomaly log is written to Cloud Logging if the distribution of at least one feature exceeds the threshold for that feature. You can forward logs to any service that Cloud Logging supports, such as Pub/Sub.

Anomalies are written to Cloud Logging with the log name: `model_monitoring_anomaly` . For example:

    logName="projects/model-monitoring-demo/logs/aiplatform.googleapis.com%2Fmodel_monitoring_anomaly" resource.labels.model_deployment_monitoring_job=6680511704087920640

Here is an example of an anomaly log entry:

    {
    "insertId": "b0e9c0e9-0979-4aff-a5d3-4c0912469f9a@a1",
    "jsonPayload": {
      "anomalyObjective": "RAW_FEATURE_SKEW",
      "endTime": "2022-02-03T19:00:00Z",
      "featureAnomalies": [
        {
          "featureDisplayName": "age",
          "deviation": 0.9,
          "threshold": 0.7
        },
        {
          "featureDisplayName": "education",
          "deviation": 0.6,
          "threshold": 0.3
        }
      ],
      "totalAnomaliesCount": 2,
      "@type": "type.googleapis.com/google.cloud.aiplatform.logging.ModelMonitoringAnomaliesLogEntry",
      "startTime": "2022-02-03T18:00:00Z",
      "modelDeploymentMonitoringJob": "projects/677687165274/locations/us-central1/modelDeploymentMonitoringJobs/6680511704087920640",
      "deployedModelId": "1645828169292316672"
    },
    "resource": {
      "type": "aiplatform.googleapis.com/ModelDeploymentMonitoringJob",
      "labels": {
        "model_deployment_monitoring_job": "6680511704087920640",
        "location": "us-central1",
        "resource_container": "projects/677687165274"
      }
    },
    "timestamp": "2022-02-03T19:00:00Z",
    "severity": "WARNING",
    "logName": "projects/model-monitoring-demo/logs/staging-aiplatform.sandbox.googleapis.com%2Fmodel_monitoring_anomaly",
    "receiveTimestamp": "2022-02-03T19:59:52.121398388Z"
    }

### Notification channels

At each monitoring interval, if the threshold of at least one feature exceeds the threshold, Model Monitoring sends an alert to the Cloud Monitoring notification channels you specified when creating the Model Monitoring job. The alert includes information about the Model Monitoring job that triggered the alert.

## Update a Model Monitoring job

You can view, update, pause, and delete a Model Monitoring job. You must pause a job before you can delete it.

### Console

Pausing and deleting are not supported in the Google Cloud console; use the gcloud CLI instead.

To update parameters for a Model Monitoring job:

1.  In the Google Cloud console, go to the **Agent Platform Endpoints** page.

2.  Click the name of the endpoint you want to edit.

3.  Click **Edit settings** .

4.  In the **Edit endpoint** pane, select **Model monitoring** or **Monitoring objectives** .
    
    > **Note:** To enable Model Monitoring for an existing endpoint, make sure **Enable model monitoring for this endpoint** is toggled on under **Model monitoring** .

5.  Update the fields you want to change.

6.  Click **Update** .

To view metrics, alerts, and monitoring properties for a model:

1.  In the Google Cloud console, go to the **Agent Platform Endpoints** page.

2.  Click the name of the endpoint.

3.  In the **Monitoring** column for the model you want to view, click **Enabled** .

### gcloud

Run the following command:

    gcloud ai model-monitoring-jobs COMMAND MONITORING_JOB_ID \
      --PARAMETER=VALUE --project=PROJECT_ID --region=LOCATION

where:

  - COMMAND is the command you want to perform on the monitoring job. For example, `update` , `pause` , `resume` , or `delete` . For more information, see the [gcloud CLI reference](https://docs.cloud.google.com/sdk/gcloud/reference/ai/model-monitoring-jobs) .

  - MONITORING\_JOB\_ID is the ID of your monitoring job. For example, `123456789` . You can find the ID by \[retrieving the endpoint information\]\[retrieve-id\] or viewing **Monitoring properties** for a model in the Google Cloud console. The ID is included in the monitoring job resource name in the format ` projects/ PROJECT_NUMBER /locations/ LOCATION /modelDeploymentMonitoringJobs/ MONITORING_JOB_ID  ` .

  - (optional) PARAMETER=VALUE is the parameter you want to update. This flag is required only when using the `update` command. For example, `monitoring-frequency=2` . For a list of parameters you can update, see the [gcloud CLI reference](https://docs.cloud.google.com/sdk/gcloud/reference/ai/model-monitoring-jobs/update) .

  - PROJECT\_ID is the ID for your Google Cloud project. For example, `my-project` .

  - LOCATION is the location for your monitoring job. For example, `us-central1` .

### REST API

### Pause a job

Before using any of the request data, make the following replacements:

  - PROJECT\_NUMBER : The number of your Google Cloud project. For example, `1234567890` .
  - LOCATION : Location for your monitoring job. For example, `us-central1` .
  - MONITORING\_JOB\_ID : ID of your monitoring job. For example, `0987654321` .

To send your request, expand one of these options:

#### curl (Linux, macOS, or Cloud Shell)

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) , or by using [Cloud Shell](https://docs.cloud.google.com/shell/docs) , which automatically logs you into the `gcloud` CLI . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Execute the following command:

    curl -X POST \
         -H "Authorization: Bearer $(gcloud auth print-access-token)" \
         -H "Content-Type: application/json; charset=utf-8" \
         -d "" \
         "https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT_NUMBER/locations/LOCATION/modelDeploymentMonitoringJobs/MONITORING_JOB_ID:pause"

#### PowerShell (Windows)

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Execute the following command:

    $cred = gcloud auth print-access-token
    $headers = @{ "Authorization" = "Bearer $cred" }
    
    Invoke-WebRequest `
        -Method POST `
        -Headers $headers `
        -Uri "https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT_NUMBER/locations/LOCATION/modelDeploymentMonitoringJobs/MONITORING_JOB_ID:pause" | Select-Object -Expand Content

You should receive a JSON response similar to the following:

``` 
{}
```

### Delete a job

Before using any of the request data, make the following replacements:

  - PROJECT\_NUMBER : The number of your Google Cloud project. For example, `my-project` .
  - LOCATION : Location for your monitoring job. For example, `us-central1` .
  - MONITORING\_JOB\_ID : ID of your monitoring job. For example, `0987654321` .

To send your request, expand one of these options:

#### curl (Linux, macOS, or Cloud Shell)

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) , or by using [Cloud Shell](https://docs.cloud.google.com/shell/docs) , which automatically logs you into the `gcloud` CLI . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Execute the following command:

    curl -X DELETE \
         -H "Authorization: Bearer $(gcloud auth print-access-token)" \
         "https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT_NUMBER/locations/LOCATION/modelDeploymentMonitoringJobs/MONITORING_JOB_ID"

#### PowerShell (Windows)

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Execute the following command:

    $cred = gcloud auth print-access-token
    $headers = @{ "Authorization" = "Bearer $cred" }
    
    Invoke-WebRequest `
        -Method DELETE `
        -Headers $headers `
        -Uri "https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT_NUMBER/locations/LOCATION/modelDeploymentMonitoringJobs/MONITORING_JOB_ID" | Select-Object -Expand Content

You should receive a JSON response similar to the following:

    {
      "name": "projects/PROJECT_NUMBER/locations/LOCATION/operations/MONITORING_JOB_ID",
      ...
      "done": true,
      ...
    }

## Analyze skew and drift data

You can use the Google Cloud console to visualize the distributions of each monitored feature and learn which changes led to skew or drift over time. You can view the feature value distributions as a histogram.

### Console

1.  To navigate to the feature distribution histograms in the Google Cloud console, go to the **Endpoints** page.

2.  On the **Endpoints** page, click the endpoint you want to analyze.

3.  On the detail page for the endpoint you selected, there is a list of all the models deployed on that endpoint. Click the name of a model to analyze.

4.  The details page for the model lists the model's input features, along with pertinent information, such as the alert threshold for each feature and the number of prior alerts for the feature.

5.  To analyze a feature, click the name of the feature. A page shows the feature distribution histograms for that feature.
    
    For each monitored feature, you can view the distributions of the 50 most recent monitoring jobs in the Google Cloud console. For skew detection, the training data distribution is displayed right next to the input data distribution:
    
    ![Histograms showing example input data distribution and training data distribution for skew detection.](https://docs.cloud.google.com/static/gemini-enterprise-agent-platform/machine-learning/model-monitoring/images/skew_detection_distribution.png)
    
    Visualizing data distribution as histograms lets you quickly focus on the changes that occurred in the data. Afterward, you might decide to adjust your feature generation pipeline or retrain the model.

## What's next

  - Work with Model Monitoring following the [API docs](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.modelDeploymentMonitoringJobs) .
  - Work with Model Monitoring following the [gcloud CLI docs](https://docs.cloud.google.com/sdk/gcloud/reference/ai/model-monitoring-jobs) .
  - Try the example notebook [in Colab](https://colab.research.google.com/github/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/model_monitoring/model_monitoring.ipynb) or [view it on GitHub](https://www.github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/model_monitoring/model_monitoring.ipynb) .
  - Learn how Model Monitoring [calculates training-serving skew and prediction drift](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/model-monitoring/overview) .
