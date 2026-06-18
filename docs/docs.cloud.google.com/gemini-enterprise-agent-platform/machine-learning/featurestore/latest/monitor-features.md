---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/featurestore/latest/monitor-features
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/featurestore/latest/monitor-features
title: Monitor features
description: Learn how to monitor feature data by scheduling and running monitoring jobs to retrieve feature statistics in Vertex AI Feature Store.
data_source: docs.cloud.google.com
---

> **Preview**
> 
> This feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](https://docs.cloud.google.com/terms/service-terms#1) . Pre-GA features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

Vertex AI Feature Store lets you schedule and run feature monitoring jobs to monitor feature data, retrieve feature statistics, and [detect feature drift](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/featurestore/latest/monitor-features#detect-drift) . You can monitor feature data only if you've registered your feature data source in the Feature Registry.

To monitor feature data, you can create the `FeatureMonitor` resource under a `FeatureGroup` resource. While creating the `FeatureMonitor` resource, you can configure the monitoring schedule to periodically run monitoring jobs on the feature data. Alternatively, you can run a feature monitoring job manually to monitor your feature data outside of the monitoring schedule.

For each monitoring job that's executed, Vertex AI Feature Store generates a `FeatureMonitorJob` resource, which you can retrieve to view the feature statistics and information about drift detected in the feature data.

## Before you begin

Before you monitor features using Vertex AI Feature Store, complete the prerequisites listed in this section.

### Register feature data source

Register your feature data source from BigQuery in the Feature Registry by creating [feature groups](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/featurestore/latest/create-featuregroup) and and [features](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/featurestore/latest/create-feature) . The `FeatureMonitor` resources used to retrieve and monitor feature statistics are associated with feature groups.

### Authenticate to Agent Platform

Authenticate to Gemini Enterprise Agent Platform, unless you've done so already.

Select the tab for how you plan to use the samples on this page:

### Python

To use the Python samples on this page in a local development environment, install and initialize the gcloud CLI, and then set up Application Default Credentials with your user credentials.

1.  [Install](https://docs.cloud.google.com/sdk/docs/install) the Google Cloud CLI.

2.  If you're using an external identity provider (IdP), you must first [sign in to the gcloud CLI with your federated identity](https://docs.cloud.google.com/iam/docs/workforce-log-in-gcloud) .

3.  If you're using a local shell, then create local authentication credentials for your user account:
    
        gcloud auth application-default login
    
    You don't need to do this if you're using Cloud Shell.
    
    If an authentication error is returned, and you are using an external identity provider (IdP), confirm that you have [signed in to the gcloud CLI with your federated identity](https://docs.cloud.google.com/iam/docs/workforce-log-in-gcloud) .

For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/authentication#local-development) .

### REST

To use the REST API samples on this page in a local development environment, you use the credentials you provide to the gcloud CLI.

For more information, see [Authenticate for using REST](https://docs.cloud.google.com/docs/authentication/rest) in the Google Cloud authentication documentation.

## Create a feature monitor with a monitoring schedule

To retrieve and monitor feature statistics, create a `FeatureMonitor` resource specifying the schedule to periodically execute feature monitoring jobs and retrieve feature statistics for the features registered in the feature group.

Use the following samples to create a `FeatureMonitor` resource. To set up multiple schedules for the same feature group, you must create multiple `FeatureMonitor` resources.

### REST

To create a [`FeatureMonitor`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.featureGroups.featureMonitors#FeatureMonitor) resource and schedule feature monitoring jobs, send a `POST` request by using the [featureMonitors.create](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.featureGroups.featureMonitors/create) method.

Before using any of the request data, make the following replacements:

  - LOCATION\_ID : Region where you want to create the feature monitor, such as `us-central1` .
  - PROJECT\_ID : Your project ID.
  - FEATUREGROUP\_NAME : The name of the feature group where you set up feature monitoring.
  - FEATURE\_MONITOR\_NAME : A name for the new feature monitor that you want to create.
  - FEATURE\_ID\_1 and FEATURE\_ID\_2 : The IDs of the features that you want to monitor.
  - DRIFT\_THRESHOLD\_1 and DRIFT\_THRESHOLD\_2 : Drift thresholds for each feature included in the feature monitor. The drift threshold is used to detect anomalies, such as feature drift. Enter a value in the range `[0, 1)` . If you don't enter a value, the threshold is set to `0.3` , by default.  
    Vertex AI Feature Store compares the snapshots from consecutive feature monitor job executions and calculates drifts using [the ML.TFDV\_VALIDATE function in BigQuery](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-tfdv-validate) . To classify anomalies, [L-infinity distance](https://en.wikipedia.org/wiki/Chebyshev_distance) is used for categorical features and [Jensen-Shannon divergence](https://en.wikipedia.org/wiki/Jensen%E2%80%93Shannon_divergence) is used for numerical features.
  - CRON : Cron schedule expression representing the frquency for running the feature monitoring job. For more information, see [cron](https://en.wikipedia.org/wiki/Cron) .

HTTP method and URL:

    POST https://LOCATION_ID-aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/LOCATION_ID/featureGroups/FEATUREGROUP_NAME/featureMonitors?feature_monitor_id=FEATURE_MONITOR_NAME

Request JSON body:

    {
      "feature_selection_config": {
        "feature_configs": [
          {"feature_id":"FEATURE_ID_1", "drift_threshold": "DRIFT_THRESHOLD_1" },
          {"feature_id":"FEATURE_ID_2", "drift_threshold": "DRIFT_THRESHOLD_2" }
        ],
      },
      "schedule_config": {
        "cron": "CRON"
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
         "https://LOCATION_ID-aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/LOCATION_ID/featureGroups/FEATUREGROUP_NAME/featureMonitors?feature_monitor_id=FEATURE_MONITOR_NAME"

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
        -Uri "https://LOCATION_ID-aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/LOCATION_ID/featureGroups/FEATUREGROUP_NAME/featureMonitors?feature_monitor_id=FEATURE_MONITOR_NAME" | Select-Object -Expand Content

You should receive a JSON response similar to the following:

    {
      "name": "projects/PROJECT_NUMBER/locations/LOCATION_ID/featureGroups/FEATUREGROUP_NAME/featureMonitors/FEATURE_MONITOR_NAME/operations/OPERATION_ID",
      "metadata": {
        "@type": "type.googleapis.com/google.cloud.aiplatform.v1beta1.CreateFeatureMonitorOperationMetadata",
        "genericMetadata": {
          "createTime": "2024-12-15T19:35:03.975958Z",
          "updateTime": "2024-12-15T19:35:03.975958Z"
        }
      }
    }

### Python

Before trying this sample, follow the Python setup instructions in the [Agent Platform quickstart using client libraries](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/start/client-libraries) . For more information, see the [Agent Platform Python API reference documentation](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest) .

To authenticate to Agent Platform, set up Application Default Credentials. For more information, see [Set up authentication for client libraries](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/authentication#client-libs) .

    from google.cloud import aiplatform
    from vertexai.resources.preview import feature_store
    
    def create_feature_monitor_sample(
        project: str,
        location: str,
        existing_feature_group_id: str,
        feature_monitor_id: str,
        feature_selection_configs: List[Tuple[str, float]]
        schedule_config: str # Cron string. For example, "0 * * * *" indicates hourly execution.
    ):
        aiplatform.init(project="PROJECT_ID", location="LOCATION_ID")
        feature_group = feature_store.FeatureGroup("FEATUREGROUP_NAME")
        feature_monitor = feature_group.create_feature_monitor(
            name= "FEATURE_MONITOR_NAME",
            feature_selection_configs=[("FEATURE_ID_1", DRIFT_THRESHOLD_1),("FEATURE_ID_2", DRIFT_THRESHOLD_2)],
            schedule_config="CRON"
            )

Replace the following:

  - LOCATION\_ID : Region where you want to create the feature monitor, such as `us-central1` .
  - PROJECT\_ID : Your project ID.
  - FEATUREGROUP\_NAME : The name of the feature group where you set up feature monitoring.
  - FEATURE\_MONITOR\_NAME : A name for the new feature monitor that you want to create.
  - FEATURE\_ID\_1 and FEATURE\_ID\_2 : The IDs of the features that you want to monitor.
  - DRIFT\_THRESHOLD\_1 and DRIFT\_THRESHOLD\_2 : Drift thresholds for each Feature included in the feature monitor. The drift threshold is used to detect feature drift. Enter a value between `0` and `1` . If you don't enter a value, the threshold is set to `0.3` , by default.  
    Vertex AI Feature Store compares the data snapshot from the current feature monitor job with the data snapshot during the previous feature monitor job. Note that to calculate the distribution deviation, Vertex AI Feature Store uses [the ML.TFDV\_VALIDATE function in BigQuery](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-tfdv-validate) .  
    For the metric used to compare statistics, [L-infinity distance](https://en.wikipedia.org/wiki/Chebyshev_distance) is used for categorical features and [Jensen-Shannon divergence](https://en.wikipedia.org/wiki/Jensen%E2%80%93Shannon_divergence) is used for numerical features.
  - CRON : Cron schedule expression representing the frequency for running the feature monitoring job. For more information, see [cron](https://en.wikipedia.org/wiki/Cron) .

## Run a feature monitoring job manually

You can skip the wait between consecutive scheduled feature monitoring jobs and manually run a feature monitor job. This is useful if you want to retrieve monitoring information and detect anomalies in the feature data immediately instead of waiting for the next scheduled monitoring job to run.

### REST

To run a feature monitoring job manually by creating a [`FeatureMonitorJob`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.featureGroups.featureMonitors.featureMonitorJobs#FeatureMonitorJob) resource , send a `POST` request by using the [featureMonitorJobs.create](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.featureGroups.featureMonitors.featureMonitorJobs/create) method.

Before using any of the request data, make the following replacements:

  - LOCATION\_ID : Region where you want to run the feature monitoring job, such as `us-central1` .
  - FEATUREGROUP\_NAME : The name of the feature group containing the `FeatureMonitor` resource.
  - PROJECT\_ID : Your project ID.
  - FEATURE\_MONITOR\_NAME : The name of the `FeatureMonitor` resource for which you want to run the feature monitoring job.

HTTP method and URL:

    POST https://LOCATION_ID-aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/LOCATION_ID/featureGroups/FEATUREGROUP_NAME/featureMonitors/FEATURE_MONITOR_ID/featureMonitorJobs

To send your request, choose one of these options:

#### curl

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) , or by using [Cloud Shell](https://docs.cloud.google.com/shell/docs) , which automatically logs you into the `gcloud` CLI . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Execute the following command:

    curl -X POST \
         -H "Authorization: Bearer $(gcloud auth print-access-token)" \
         -H "Content-Type: application/json; charset=utf-8" \
         -d "" \
         "https://LOCATION_ID-aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/LOCATION_ID/featureGroups/FEATUREGROUP_NAME/featureMonitors/FEATURE_MONITOR_ID/featureMonitorJobs"

#### PowerShell

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Execute the following command:

    $cred = gcloud auth print-access-token
    $headers = @{ "Authorization" = "Bearer $cred" }
    
    Invoke-WebRequest `
        -Method POST `
        -Headers $headers `
        -Uri "https://LOCATION_ID-aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/LOCATION_ID/featureGroups/FEATUREGROUP_NAME/featureMonitors/FEATURE_MONITOR_ID/featureMonitorJobs" | Select-Object -Expand Content

You should receive a JSON response similar to the following:

    {
      "name": "projects/PROJECT_NUMBER/locations/LOCATION_ID/featureGroups/FEATUREGROUP_NAME/featureMonitors/FEATURE_MONITOR_NAME/featureMonitorJobs/FEATURE_MONITOR_JOB_ID"
    }

### Python

Before trying this sample, follow the Python setup instructions in the [Agent Platform quickstart using client libraries](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/start/client-libraries) . For more information, see the [Agent Platform Python API reference documentation](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest) .

To authenticate to Agent Platform, set up Application Default Credentials. For more information, see [Set up authentication for client libraries](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/authentication#client-libs) .

    from google.cloud import aiplatform
    from vertexai.resources.preview import feature_store
    
    aiplatofrm.init(project="PROJECT_ID", location="LOCATION_ID")
    
    feature_group = FeatureGroup.get("FEATUREGROUP_NAME}")
    feature_monitor = feature_group.get_feature_monitor(FEATURE_MONITOR_NAME)
    feature_monitor_job = feature_monitor.create_feature_monitor_job()

Replace the following:

  - LOCATION\_ID : Region where you want to run the feature monitoring job, such as `us-central1` .
  - PROJECT\_ID : Your project ID.
  - FEATUREGROUP\_NAME : The name of the feature group containing the `FeatureMonitor` resource.
  - FEATURE\_MONITOR\_NAME : The name of the `FeatureMonitor` resource for which you want to run the feature monitoring job.

## Retrieve feature statistics from a monitoring job

You can retrieve feature statistics for all the features in a feature monitoring job by retrieving the `FeatureMonitorJob` resource using the feature monitor job ID generated during the feature monitoring job execution. You can also retrieve feature statistics for a specific resource for the latest monitoring job.

### List feature monitor jobs

The following samples show how to retrieve a list of all the `FeatureMonitorJob` resources created for a given `FeatureMonitor` resource.

### REST

To retrieve a list of [`FeatureMonitorJob`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.featureGroups.featureMonitors.featureMonitorJobs#FeatureMonitorJob) resources for a specified `FeatureMonitor` resource, send a `GET` request by using the [featureMonitorJobs.list](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.featureGroups.featureMonitors.featureMonitorJobs/list) method.

Before using any of the request data, make the following replacements:

  - LOCATION\_ID : Region where the `Feature` resource is located, such as `us-central1` .
  - PROJECT\_ID : Your project ID.
  - FEATUREGROUP\_NAME : The name of the feature group containing the `FeatureMonitor` resource.
  - FEATURE\_MONITOR\_NAME : The name of the `FeatureMonitor` resource for which you want to list the feature monitoring jobs.

HTTP method and URL:

    GET https://LOCATION_ID-aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/LOCATION_ID/featureGroups/FEATUREGROUP_NAME/featureMonitors/FEATURE_MONITOR_NAME/featureMonitorJobs

To send your request, choose one of these options:

#### curl

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) , or by using [Cloud Shell](https://docs.cloud.google.com/shell/docs) , which automatically logs you into the `gcloud` CLI . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Execute the following command:

    curl -X GET \
         -H "Authorization: Bearer $(gcloud auth print-access-token)" \
         "https://LOCATION_ID-aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/LOCATION_ID/featureGroups/FEATUREGROUP_NAME/featureMonitors/FEATURE_MONITOR_NAME/featureMonitorJobs"

#### PowerShell

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Execute the following command:

    $cred = gcloud auth print-access-token
    $headers = @{ "Authorization" = "Bearer $cred" }
    
    Invoke-WebRequest `
        -Method GET `
        -Headers $headers `
        -Uri "https://LOCATION_ID-aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/LOCATION_ID/featureGroups/FEATUREGROUP_NAME/featureMonitors/FEATURE_MONITOR_NAME/featureMonitorJobs" | Select-Object -Expand Content

You should receive a JSON response similar to the following:

    {
      "featureMonitorJobs": [
        {
          "name": "projects/PROJECT_NUMBER/locations/LOCATION_ID/featureGroups/FEATUREGROUP_NAME/featureMonitors/FEATURE_MONITOR_NAME/featureMonitorJobs/FEATURE_MONITOR_JOB_ID_1",
          "createTime": "2024-12-18T19:18:18.077161Z",
          "finalStatus": {},
          "featureSelectionConfig": {
            "featureConfigs": [
              {
                "featureId": "feature_name_1",
                "driftThreshold": 0.2
              },
              {
                "featureId": "feature_name_2",
                "driftThreshold": 0.2
              }
            ]
          }
        },
        {
          "name": "projects/PROJECT_NUMBER/locations/LOCATION_ID/featureGroups/FEATUREGROUP_NAME/featureMonitors/FEATURE_MONITOR_NAME/featureMonitorJobs/FEATURE_MONITOR_JOB_ID_2",
          "createTime": "2024-12-19T19:18:30.859921Z",
          "finalStatus": {},
          "featureSelectionConfig": {
            "featureConfigs": [
              {
                "featureId": "feature_name_1",
                "driftThreshold": 0.2
              },
              {
                "featureId": "feature_name_2",
                "driftThreshold": 0.2
              }
            ]
          }
        }
      ]
    }

### Python

Before trying this sample, follow the Python setup instructions in the [Agent Platform quickstart using client libraries](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/start/client-libraries) . For more information, see the [Agent Platform Python API reference documentation](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest) .

To authenticate to Agent Platform, set up Application Default Credentials. For more information, see [Set up authentication for client libraries](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/authentication#client-libs) .

    from google.cloud import aiplatform
    from vertexai.resources.preview import feature_store
    
    aiplatofrm.init(project="PROJECT_ID", location="LOCATION_ID")
    
    feature_group = FeatureGroup.get("FEATUREGROUP_NAME")
    feature_monitor = feature_group.get_feature_monitor(FEATURE_MONITOR_NAME)
    feature_monitor_jobs = feature_monitor.list_feature_monitor_jobs()

Replace the following:

  - LOCATION\_ID : Region where the `Feature` resource is located, such as `us-central1` .
  - PROJECT\_ID : Your project ID.
  - FEATUREGROUP\_NAME : The name of the feature group containing the `FeatureMonitor` resource.
  - FEATURE\_MONITOR\_NAME : The name of the `FeatureMonitor` resource for which you want to list the feature monitoring jobs.

### View feature statistics from a monitoring job

The following samples show how to view the feature statistics for all the features in a feature monitoring job. For each feature, the statistics and anomalies are displayed in the [`FeatureNameStatistics`](https://www.tensorflow.org/tfx/tf_metadata/api_docs/python/tfmd/proto/statistics_pb2/FeatureNameStatistics) format.

### REST

To view the feature statistics from a monitoring job by retrieving a [`FeatureMonitorJob`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.featureGroups.featureMonitors.featureMonitorJobs#FeatureMonitorJob) resource, send a `GET` request by using the [featureMonitorJobs.get](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.featureGroups.featureMonitors.featureMonitorJobs/get) method.

Before using any of the request data, make the following replacements:

  - LOCATION\_ID : Region where where the feature monitoring job was run, such as `us-central1` .
  - PROJECT\_ID : Your project ID.
  - FEATUREGROUP\_NAME : The name of the feature group containing the `FeatureMonitor` resource.
  - FEATURE\_MONITOR\_NAME : The name of the `FeatureMonitor` resource for which the feature monitoring job was run.
  - FEATURE\_MONITOR\_JOB\_ID : The ID of the FeatureMonitorJob resource that you want to retrieve.

HTTP method and URL:

    GET https://LOCATION_ID-aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/LOCATION_ID/featureGroups/FEATUREGROUP_NAME/featureMonitors/FEATURE_MONITOR_NAME/featureMonitorJobs/FEATURE_MONITOR_JOB_ID

To send your request, choose one of these options:

#### curl

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) , or by using [Cloud Shell](https://docs.cloud.google.com/shell/docs) , which automatically logs you into the `gcloud` CLI . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Execute the following command:

    curl -X GET \
         -H "Authorization: Bearer $(gcloud auth print-access-token)" \
         "https://LOCATION_ID-aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/LOCATION_ID/featureGroups/FEATUREGROUP_NAME/featureMonitors/FEATURE_MONITOR_NAME/featureMonitorJobs/FEATURE_MONITOR_JOB_ID"

#### PowerShell

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Execute the following command:

    $cred = gcloud auth print-access-token
    $headers = @{ "Authorization" = "Bearer $cred" }
    
    Invoke-WebRequest `
        -Method GET `
        -Headers $headers `
        -Uri "https://LOCATION_ID-aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/LOCATION_ID/featureGroups/FEATUREGROUP_NAME/featureMonitors/FEATURE_MONITOR_NAME/featureMonitorJobs/FEATURE_MONITOR_JOB_ID" | Select-Object -Expand Content

You should receive a JSON response similar to the following:

    {
      "name": "projects/PROJECT_NUMBER/locations/LOCATION_ID/featureGroups/FEATUREGROUP_NAME/featureMonitors/FEATURE_MONITOR_NAME/featureMonitorJobs/FEATURE_MONITOR_JOB_ID",
      "createTime": "2024-12-19T19:18:18.077161Z",
      "finalStatus": {},
      "jobSummary": {
        "featureStatsAndAnomalies": [
          {
            "featureId": "feature_id_1",
            "featureStats": {
              "name": "feature_name_1",
              "type": "STRING",
              "stringStats": {
                "commonStats": {
                  "numNonMissing": "6",
                  "minNumValues": "1",
                  "maxNumValues": "1",
                  "avgNumValues": 1,
                  "numValuesHistogram": {
                    "buckets": [
                      {
                        "lowValue": 1,
                        "highValue": 1,
                        "sampleCount": 0.6
                      },
                      {
                        "lowValue": 1,
                        "highValue": 1,
                        "sampleCount": 0.6
                      }
                    ],
                    "type": "QUANTILES"
                  },
                  "totNumValues": "6"
                },
                "unique": "2",
                "topValues": [
                  {
                    "value": "59",
                    "frequency": 2
                  },
                  {
                    "value": "19",
                    "frequency": 1
                  }
                ],
                "avgLength": 2,
                "rankHistogram": {
                  "buckets": [
                    {
                      "label": "59",
                      "sampleCount": 2
                    },
                    {
                      "lowRank": "1",
                      "highRank": "1",
                      "label": "19",
                      "sampleCount": 1
                    }
                  ]
                }
              }
            },
            "statsTime": "2024-12-19T19:18:18.077161Z",
            "featureMonitorJobId": "FEATURE_MONITOR_JOB_ID",
            "featureMonitorId": "FEATURE_MONITOR_NAME"
          },
          {
            "featureId": "feature_id_2",
            "featureStats": {
              "name": "feature_name_1",
              "type": "STRING",
              "stringStats": {
                "commonStats": {
                  "numNonMissing": "6",
                  "minNumValues": "1",
                  "maxNumValues": "1",
                  "avgNumValues": 1,
                  "numValuesHistogram": {
                    "buckets": [
                      {
                        "lowValue": 1,
                        "highValue": 1,
                        "sampleCount": 0.6
                      },
                      {
                        "lowValue": 1,
                        "highValue": 1,
                        "sampleCount": 0.6
                      }
                    ],
                    "type": "QUANTILES"
                  },
                  "totNumValues": "6"
                },
                "unique": "2",
                "topValues": [
                  {
                    "value": "59",
                    "frequency": 2
                  },
                  {
                    "value": "19",
                    "frequency": 1
                  }
                ],
                "avgLength": 2,
                "rankHistogram": {
                  "buckets": [
                    {
                      "label": "59",
                      "sampleCount": 2
                    },
                    {
                      "lowRank": "1",
                      "highRank": "1",
                      "label": "19",
                      "sampleCount": 1
                    }
                  ]
                }
              }
            },
            "statsTime": "2024-12-19T19:18:18.077161Z",
            "featureMonitorJobId": "FEATURE_MONITOR_JOB_ID",
            "featureMonitorId": "FEATURE_MONITOR_NAME"
          }
        ]
      },
      "driftBaseFeatureMonitorJobId": "2250003330000300000",
      "driftBaseSnapshotTime": "2024-12-12T16:00:01.211686Z",
      "featureSelectionConfig": {
        "featureConfigs": [
          {
            "featureId": "feature_id_1",
            "driftThreshold": 0.2
          },
          {
            "featureId": "feature_id_2",
            "driftThreshold": 0.2
          }
        ]
      },
      "triggerType": "FEATURE_MONITOR_JOB_TRIGGER_ON_DEMAND"
    }

### Python

Before trying this sample, follow the Python setup instructions in the [Agent Platform quickstart using client libraries](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/start/client-libraries) . For more information, see the [Agent Platform Python API reference documentation](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest) .

To authenticate to Agent Platform, set up Application Default Credentials. For more information, see [Set up authentication for client libraries](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/authentication#client-libs) .

    from google.cloud import aiplatform
    from vertexai.resources.preview import feature_store
    
    aiplatofrm.init(project="PROJECT_ID", location="LOCATION_ID")
    feature_group = FeatureGroup.get("FEATUREGROUP_NAME"})
    
    feature_monitor = feature_group.get_feature_monitor("FEATURE_MONITOR_NAME")
    feature_monitor_job = feature_monitor.get_feature_monitor_job("FEATURE_MONITOR_JOB_ID)")
    
    # Retrieve feature stats and anomalies
    feature_stats_and_anomalies = feature_monitor_job.feature_stats_and_anomalies
    print(feature_stats_and_anomalies)

Replace the following:

  - LOCATION\_ID : Region where where the feature monitoring job was run, such as `us-central1` .
  - PROJECT\_ID : Your project ID.
  - FEATUREGROUP\_NAME : The name of the feature group containing the `FeatureMonitor` resource.
  - FEATURE\_MONITOR\_NAME : The name of the `FeatureMonitor` resource for which the feature monitoring job was run.
  - FEATURE\_MONITOR\_JOB\_ID : The ID of the `FeatureMonitorJob` resource that you want to retrieve.

### View feature statistics for a feature

You can retrieve the feature statistics for a specific feature from the most recent feature monitoring jobs executed, by retrieving the feature details and specifying the number of monitoring jobs that you want to retrieve the statistics from. The statistics and anomalies are displayed in the [`FeatureNameStatistics`](https://www.tensorflow.org/tfx/tf_metadata/api_docs/python/tfmd/proto/statistics_pb2/FeatureNameStatistics) format.

The following samples show how to view the feature statistics for a specific feature from a specified number of recent feature monitoring jobs.

### REST

To view the feature statistics for a specific feature in a [`Feature`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.featureGroups.features#resource:-feature) resource, send a `GET` request using the [features.get](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.featureGroups.features/get) method and specifying the number of monitoring jobs to retrieve the statistics from.

Before using any of the request data, make the following replacements:

  - LOCATION\_ID : Region where where the feature monitoring job was run, such as `us-central1` .
  - PROJECT\_ID : Your project ID.
  - FEATUREGROUP\_NAME : The name of the feature group containing the feature.
  - FEATURE\_NAME : The name of the `Feature` resource for which you want to retrieve the feature statistics.
  - LATEST\_STATS\_COUNT : The number of the latest monitoring jobs to retrieve the feature statistics from.

HTTP method and URL:

    GET https://LOCATION_ID-aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/LOCATION_ID/featureGroups/FEATUREGROUP_NAME/features/FEATURE_NAME?feature_stats_and_anomaly_spec.latest_stats_count=LATEST_STATS_COUNT

To send your request, choose one of these options:

#### curl

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) , or by using [Cloud Shell](https://docs.cloud.google.com/shell/docs) , which automatically logs you into the `gcloud` CLI . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Execute the following command:

    curl -X GET \
         -H "Authorization: Bearer $(gcloud auth print-access-token)" \
         "https://LOCATION_ID-aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/LOCATION_ID/featureGroups/FEATUREGROUP_NAME/features/FEATURE_NAME?feature_stats_and_anomaly_spec.latest_stats_count=LATEST_STATS_COUNT"

#### PowerShell

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Execute the following command:

    $cred = gcloud auth print-access-token
    $headers = @{ "Authorization" = "Bearer $cred" }
    
    Invoke-WebRequest `
        -Method GET `
        -Headers $headers `
        -Uri "https://LOCATION_ID-aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/LOCATION_ID/featureGroups/FEATUREGROUP_NAME/features/FEATURE_NAME?feature_stats_and_anomaly_spec.latest_stats_count=LATEST_STATS_COUNT" | Select-Object -Expand Content

You should receive a JSON response similar to the following:

    {
      "name": "projects/PROJECT_NUMBER/locations/LOCATION_ID/featureGroups/FEATUREGROUP_NAME/features/FEATURE_NAME",
      "createTime": "2024-12-19T21:17:23.373559Z",
      "updateTime": "2024-12-19T21:17:23.373559Z",
      "etag": "sample_etag",
      "featureStatsAndAnomaly": [
        {
          "featureStats": {
            "name": "FEATURE_NAME",
            "type": "STRING",
            "stringStats": {
              "commonStats": {
                "numNonMissing": "4",
                "minNumValues": "1",
                "maxNumValues": "1",
                "avgNumValues": 1,
                "numValuesHistogram": {
                  "buckets": [
                    {
                      "lowValue": 1,
                      "highValue": 1,
                      "sampleCount": 0.4
                    },
                    {
                      "lowValue": 1,
                      "highValue": 1,
                      "sampleCount": 0.4
                    },
                    {
                      "lowValue": 1,
                      "highValue": 1,
                      "sampleCount": 0.4
                    },
                    {
                      "lowValue": 1,
                      "highValue": 1,
                      "sampleCount": 0.4
                    }
                  ],
                  "type": "QUANTILES"
                },
                "totNumValues": "4"
              },
              "unique": "4",
              "topValues": [
                {
                  "value": "feature_value_1",
                  "frequency": 1
                },
                {
                  "value": "feature_value_2",
                  "frequency": 1
                },
                {
                  "value": "feature_value_3",
                  "frequency": 1
                },
                {
                  "value": "feature_value_4",
                  "frequency": 1
                }
              ],
              "avgLength": 4,
              "rankHistogram": {
                "buckets": [
                  {
                    "label": "label_1",
                    "sampleCount": 1
                  },
                  {
                    "lowRank": "1",
                    "highRank": "1",
                    "label": "label_2",
                    "sampleCount": 1
                  },
                  {
                    "lowRank": "2",
                    "highRank": "2",
                    "label": "label_3",
                    "sampleCount": 1
                  },
                  {
                    "lowRank": "3",
                    "highRank": "3",
                    "label": "label_4",
                    "sampleCount": 1
                  }
                ]
              }
            }
          },
          "driftDetectionThreshold": 0.1,
          "statsTime": "2024-12-19T22:00:02.734796Z",
          "featureMonitorJobId": "feature_monitor_job_id_1",
          "featureMonitorId": "feature_monitor_name_1"
        }
      ],
      "versionColumnName": "version_column_name"
    }

### Python

Before trying this sample, follow the Python setup instructions in the [Agent Platform quickstart using client libraries](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/start/client-libraries) . For more information, see the [Agent Platform Python API reference documentation](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest) .

To authenticate to Agent Platform, set up Application Default Credentials. For more information, see [Set up authentication for client libraries](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/authentication#client-libs) .

    from google.cloud import aiplatform
    from vertexai.resources.preview import feature_store
    
    aiplatofrm.init(project="PROJECT_ID", location="LOCATION_ID")
    
    feature_group = FeatureGroup.get("FEATUREGROUP_NAME"})
    feature_stats_and_anomalies = feature_group.get_feature("FEATURE_NAME", latest_stats_count=LATEST_STATS_COUNT)
    print(feature_stats_and_anomalies)

Replace the following:

  - LOCATION\_ID : Region where where the feature monitoring job was run, such as `us-central1` .
  - PROJECT\_ID : Your project ID.
  - FEATUREGROUP\_NAME : The name of the feature group containing the `FeatureMonitor` resource.
  - FEATURE\_NAME : The name of the feature for which you want to retrieve the feature statistics.
  - LATEST\_STATS\_COUNT : The number of latest monitoring jobs to retrieve the feature statistics from.

## Example use case: Use feature monitoring to detect feature drift

You can use feature monitoring to detect an anomaly in feature data called feature drift. A drift is a significant and unforeseen change to feature data in BigQuery over time. Vertex AI Feature Store helps you identify feature drift by comparing the snapshot at the time when the monitoring job is run, with the data snapshot during the previous monitoring job execution.

For any feature included in the feature monitor, if the difference between the two snapshots exceeds the threshold specified in the [`drift_threshold`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/FeatureSelectionConfig#FeatureConfig) parameter, Vertex AI Feature Store identifies a feature drift and returns the following information in the `FeatureMonitorJob` resource:

  - The `driftDetected` parameter is set to `true` .

  - The distribution deviation between the two snapshots. For numerical features, Vertex AI Feature Store calculates this value using [Jensen-Shannon divergence](https://en.wikipedia.org/wiki/Jensen-Shannon_Divergence) . For categorical features, Vertex AI Feature Store calculates this value using [L-infinity distance](https://en.wikipedia.org/wiki/Chebyshev_distance) .

  - The threshold that was exceeded by the distribution deviation.

The following samples show how to retrieve a `FeatureMonitorJob` resource and verify whether a drift was detected.

### REST

To retrieve a [`FeatureMonitorJob`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.featureGroups.featureMonitors.featureMonitorJobs#FeatureMonitorJob) resource , send a `GET` request by using the [featureMonitorJobs.get](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.featureGroups.featureMonitors.featureMonitorJobs/get) method.

Before using any of the request data, make the following replacements:

  - LOCATION\_ID : Region where where the feature monitoring job was run, such as `us-central1` .
  - PROJECT\_ID : Your project ID.
  - FEATUREGROUP\_NAME : The name of the feature group containing the `FeatureMonitor` resource.
  - FEATURE\_MONITOR\_NAME : The name of the `FeatureMonitor` resource for which the feature monitoring job was run.
  - FEATURE\_MONITOR\_JOB\_ID : The ID of the `FeatureMonitorJob` resource that you want to retrieve.

HTTP method and URL:

    GET https://LOCATION_ID-aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/LOCATION_ID/featureGroups/FEATUREGROUP_NAME/featureMonitors/FEATURE_MONITOR_NAME/featureMonitorJobs/FEATURE_MONITOR_JOB_ID

To send your request, choose one of these options:

#### curl

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) , or by using [Cloud Shell](https://docs.cloud.google.com/shell/docs) , which automatically logs you into the `gcloud` CLI . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Execute the following command:

    curl -X GET \
         -H "Authorization: Bearer $(gcloud auth print-access-token)" \
         "https://LOCATION_ID-aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/LOCATION_ID/featureGroups/FEATUREGROUP_NAME/featureMonitors/FEATURE_MONITOR_NAME/featureMonitorJobs/FEATURE_MONITOR_JOB_ID"

#### PowerShell

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Execute the following command:

    $cred = gcloud auth print-access-token
    $headers = @{ "Authorization" = "Bearer $cred" }
    
    Invoke-WebRequest `
        -Method GET `
        -Headers $headers `
        -Uri "https://LOCATION_ID-aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/LOCATION_ID/featureGroups/FEATUREGROUP_NAME/featureMonitors/FEATURE_MONITOR_NAME/featureMonitorJobs/FEATURE_MONITOR_JOB_ID" | Select-Object -Expand Content

You should receive a JSON response similar to the following:

    {
      "name": "projects/PROJECT_NUMBER/locations/LOCATION_ID/featureGroups/FEATUREGROUP_NAME/featureMonitors/FEATURE_MONITOR_NAME/featureMonitorJobs/FEATURE_MONITOR_JOB_ID",
      "createTime": "2024-12-14T19:45:30.026522Z",
      "finalStatus": {},
      "jobSummary": {
        "featureStatsAndAnomalies": [
          {
            "featureId": "feature_id_1",
            "featureStats": {
              "name": "feature_name_1",
              "type": "STRING",
              "stringStats": {
                "commonStats": {
                  "numNonMissing": "3",
                  "minNumValues": "1",
                  "maxNumValues": "1",
                  "avgNumValues": 1,
                  "numValuesHistogram": {
                    "buckets": [
                      {
                        "lowValue": 1,
                        "highValue": 1,
                        "sampleCount": 0.9
                      },
                      {
                        "lowValue": 1,
                        "highValue": 1,
                        "sampleCount": 0.9
                      },
                      {
                        "lowValue": 1,
                        "highValue": 1,
                        "sampleCount": 0.9
                      }
                    ],
                    "type": "QUANTILES"
                  },
                  "totNumValues": "3"
                },
                "unique": "3",
                "topValues": [
                  {
                    "value": "sample_value_1",
                    "frequency": 1
                  },
                  {
                    "value": "sample_value_2",
                    "frequency": 1
                  },
                  {
                    "value": "sample_value_3",
                    "frequency": 1
                  }
                ],
                "avgLength": 3,
                "rankHistogram": {
                  "buckets": [
                    {
                      "label": "sample_label_1",
                      "sampleCount": 1
                    },
                    {
                      "lowRank": "1",
                      "highRank": "1",
                      "label": "sample_label_2",
                      "sampleCount": 1
                    },
                    {
                      "lowRank": "2",
                      "highRank": "3",
                      "label": "sample_label_3",
                      "sampleCount": 1
                    }
                  ]
                }
              }
            },
            "distributionDeviation": 0.1388880008888000,
            "driftDetectionThreshold": 0.1,
            "driftDetected": true,
            "statsTime": "2024-12-15T19:45:37.026522Z",
            "featureMonitorJobId": "FEATURE_MONITOR_JOB_ID",
            "featureMonitorId": "FEATURE_MONITOR_NAME"
          }
        ]
      },
      "driftBaseFeatureMonitorJobId": "2250003330000300000",
      "driftBaseSnapshotTime": "2024-12-12T18:18:18.077161Z",
      "description": "sample_feature_monitor_job_description",
      "featureSelectionConfig": {
        "featureConfigs": [
          {
            "featureId": "feature_name",
            "driftThreshold": 0.1
          }
        ]
      },
      "triggerType": "FEATURE_MONITOR_JOB_TRIGGER_ON_DEMAND"
    }

### Python

Before trying this sample, follow the Python setup instructions in the [Agent Platform quickstart using client libraries](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/start/client-libraries) . For more information, see the [Agent Platform Python API reference documentation](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest) .

To authenticate to Agent Platform, set up Application Default Credentials. For more information, see [Set up authentication for client libraries](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/authentication#client-libs) .

    from google.cloud import aiplatform
    from vertexai.resources.preview import feature_store
    
    aiplatofrm.init(project="PROJECT_ID", location="LOCATION_ID")
    feature_group = FeatureGroup.get("FEATUREGROUP_NAME"})
    feature_monitor = feature_group.get_feature_monitor("FEATURE_MONITOR_NAME")
    feature_monitor_job = feature_monitor.get_feature_monitor_job("FEATURE_MONITOR_JOB_ID)")
    
    # Retrieve feature stats and anomalies
    feature_stats_and_anomalies = feature_monitor_job.feature_stats_and_anomalies
    print(feature_stats_and_anomalies)
    
    # Check whether drifts are detected
    for feature_stats_and_anomalies in feature_monitor_job.feature_stats_and_anomalies:
        print("feature: ", feature_stats_and_anomalies.feature_id)
        print("distribution deviation: ", feature_stats_and_anomalies.distribution_deviation)
        print("drift detected: ", feature_stats_and_anomalies.drift_detected)

Replace the following:

  - LOCATION\_ID : Region where where the feature monitoring job was run, such as `us-central1` .
  - PROJECT\_ID : Your project ID.
  - FEATUREGROUP\_NAME : The name of the feature group containing the `FeatureMonitor` resource.
  - FEATURE\_MONITOR\_NAME : The name of the `FeatureMonitor` resource for which the feature monitoring job was run.
  - FEATURE\_MONITOR\_JOB\_ID : The ID of the `FeatureMonitorJob` resource that you want to retrieve.
