---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/pipelines/schedule-pipeline-run
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/pipelines/schedule-pipeline-run
title: Schedule a pipeline run with scheduler API
description: Learn how to use the scheduler API to schedule recurring pipeline runs to automate continuous model training.
data_source: docs.cloud.google.com
---

You can schedule one-time or recurring pipeline runs in Vertex AI using the scheduler API. This lets you implement continuous training in your project.

After you create a schedule, it can have one of the following states:

  - `ACTIVE` : An active schedule continuously creates pipeline runs according to the frequency configured using the cron schedule expression. A schedule becomes active on its start time and remains in that state until the specified end time, or until you pause it.

  - `PAUSED` : A paused schedule doesn't create pipeline runs. You can resume a paused schedule to make it active again. When you resume a paused schedule, you can use the `catch_up` parameter to specify whether skipped runs (runs that would have been scheduled if the schedule had been active) need to be rescheduled and submitted at the earliest possible schedule.

  - `COMPLETED` : A completed schedule no longer creates new pipeline runs. A schedule is completed according to its specified end time.

You can use the scheduler API to do the following:

  - [Create a schedule](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/pipelines/schedule-pipeline-run#create-a-schedule)

  - [List schedules](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/pipelines/schedule-pipeline-run#list-schedules)

  - [Retrieve a schedule](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/pipelines/schedule-pipeline-run#retrieve-schedule)

  - [Pause a schedule](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/pipelines/schedule-pipeline-run#pause-schedule)

  - [Update a schedule](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/pipelines/schedule-pipeline-run#update-schedule)

  - [Resume a schedule](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/pipelines/schedule-pipeline-run#resume-schedule)

  - [Delete a schedule](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/pipelines/schedule-pipeline-run#delete-schedule)

## Before you begin

Before you schedule a pipeline run using the scheduler API, use the following instructions to set up your Google Cloud project and development environment in the Google Cloud console.

1.  Grant the at least one of the following IAM permissions to the user or service account for using the scheduler API:
    
      - `roles/aiplatform.admin`
      - `roles/aiplatform.user`

2.  Build and compile a pipeline. For more information, see [Build a Pipeline](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/pipelines/build-pipeline) .

## Create a schedule

You can create a one-time or recurring schedule.

### Console

Use the following instructions to create a schedule using the Google Cloud console. If a schedule already exists for the project and region, use the instructions in [Create a pipeline run](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/pipelines/run-pipeline#create_a_pipeline_run) .

Use the following instructions to create a pipeline schedule:

1.  In the Google Cloud console, in the Agent Platform section, go to the **Schedules** tab on the **Pipelines** page.

2.  Click **Create scheduled run** to open the **Create pipeline run** pane.

3.  Specify the following **Run details** by selecting one of the following options:
    
      - To create a pipeline run based on an existing pipeline template, click **Select from existing pipelines** and enter the following details:
        
        1.  Select the **Repository** containing the pipeline or component definition file.
        
        2.  Select the **Pipeline or component** and **Version** .
    
      - To upload a compiled pipeline definition, click **Upload file** and enter the following details:
        
        1.  Click **Browse** to open the file selector. Navigate to the compiled pipeline YAML file that you want to run, select the pipeline, and click **Open** .
        
        2.  The **Pipeline or component name** shows the name specified in the pipeline definition, by default. Optionally, specify a different Pipeline name.
    
      - To import a pipeline definition file from Cloud Storage, click **Import from Cloud Storage** and enter the following details:
        
        1.  Click **Browse** to navigate to the Cloud Storage bucket containing the pipeline definition object, select the file, and then click **Select** .
        
        2.  Specify the **Pipeline or component name** .

4.  Specify a **Run name** to uniquely identify the pipeline run.

5.  Specify the **Run schedule** , as follows:
    
    1.  Select **Recurring** .
    
    2.  Under **Start time** , specify the when the schedule becomes active.
        
          - To schedule the first run to occur immediately upon schedule creation, select **Immediately** .
        
          - To schedule the first run to occur at a specific time and date, select **On** .
    
    3.  In the **Frequency** field, specify the frequency to schedule and execute the pipeline runs, using a cron schedule expression based on [unix-cron](https://man7.org/linux/man-pages/man5/crontab.5.html) .
    
    4.  Under **Ends** , specify when the schedule ends.
        
          - To indicate that the schedule creates pipeline runs indefinitely, select **Never** .
        
          - To indicate that the schedule ends on a specific date and time, select **On** , and specify the end date and time for the schedule.

6.  Optional: To specify a custom service account, a customer-managed encryption key (CMEK), or a peered VPC network, click **Advanced options** and specify a service account, CMEK, or peered VPC network name.

7.  Click **Continue** and specify the **Runtime configuration** for the pipeline.

8.  Click **Submit** to create your pipeline run schedule.

### REST

To create a pipeline run schedule, send a POST request by using the [projects.locations.schedules.create](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.schedules/create) method.

Before using any of the request data, make the following replacements:

  - LOCATION : The region where you want to run the pipeline. For more information about the regions where Agent Platform Pipelines is available, see the [Gemini Enterprise Agent Platform locations guide](https://docs.cloud.google.com/vertex-ai/docs/general/locations#feature-availability) .

  - PROJECT\_ID : The Google Cloud project where you want to run the pipeline.

  - DISPLAY\_NAME : The name of the pipeline schedule. You can specify a name having a maximum length of 128 UTF-8 characters.

  - START\_TIME : Timestamp after which the first run can be scheduled, for example, `2045-07-26T00:00:00Z` . If you don't specify this parameter, the timestamp corresponding to the date and time when you create the schedule is used as the default value.

  - END\_TIME : Timestamp after which pipeline runs are no longer scheduled scheduled. After the END\_TIME is reached, the state of the schedule changes to `COMPLETED` . If you don't specify this parameter, then the schedule continues to run new pipeline jobs indefinitely until you pause or delete the schedule.

  - CRON\_EXPRESSION : Cron schedule expression representing the frequency to schedule and execute pipeline runs. For more information, see [cron](https://en.wikipedia.org/wiki/Cron) .

  - MAX\_CONCURRENT\_RUN\_COUNT : The maximum number of concurrent runs for the schedule.

  - API\_REQUEST\_TEMPLATE : `PipelineService.CreatePipelineJob` API request template used to execute the scheduled pipeline runs. For more information about the parameters in the API request template, see the documentation for [`pipelineJobs.create`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.pipelineJobs/create) . Note that you can't specify the `pipelineJobId` parameter in this template, as the scheduler API doesn't support this parameter.
    
    Click here to view a sample API request template, where `gs://gcs_directory` is the Cloud Storage bucket for pipeline output artifacts.
    
    ``` 
    {
      "parent":"projects//locations/us-central1",
      "pipelineJob": {
        "displayName": "hello-world",
        "pipelineSpec": {
          "deploymentConfig": {
            "@type": "type.googleapis.com/ml_pipelines.PipelineDeploymentConfig",
            "executors": {
              "HelloWorld_executor": {
                "container": {
                  "command": ["sleep", "1"],
                  "image": "google/cloud-sdk:latest"
                }
              }
            }
          },
          "pipelineInfo": {
            "name": "hello-world"
          },
          "root": {
            "dag": {
              "tasks": {
                "task-test-hello-world": {
                  "taskInfo": {"name": "HelloWorld"},
                  "componentRef": {"name": "HelloWorld"},
                  "cachingOptions": {}
                }
              }
            }
          },
          "components": {
            "HelloWorld": {
              "executorLabel": "HelloWorld_executor"
            }
          },
          "schemaVersion": "2.0.0"
        },
        "runtimeConfig": {
          "gcsOutputDirectory": "gs://gcs_directory"
        }
      }
    }
          
    ```

HTTP method and URL:

    POST https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/schedules

Request JSON body:

    {
      "display_name":"DISPLAY_NAME",
      "start_time": "START_TIME",
      "end_time": "END_TIME",
      "cron": "CRON_EXPRESSION",
      "max_concurrent_run_count": "MAX_CONCURRENT_RUN_COUNT",
      "create_pipeline_job_request": API_REQUEST_TEMPLATE
    }

To send your request, choose one of these options:

#### curl

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) , or by using [Cloud Shell](https://docs.cloud.google.com/shell/docs) , which automatically logs you into the `gcloud` CLI . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Save the request body in a file named `request.json` , and execute the following command:

    curl -X POST \
         -H "Authorization: Bearer $(gcloud auth print-access-token)" \
         -H "Content-Type: application/json; charset=utf-8" \
         -d @request.json \
         "https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/schedules"

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
        -Uri "https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/schedules" | Select-Object -Expand Content

You should see output similar to the following. You can use the SCHEDULE\_ID from the response to retrieve, pause, resume, or delete the schedule. PIPELINE\_JOB\_CREATION\_REQUEST represents the API request to create the pipeline job.

    {
      "name": "projects/PROJECT_ID/locations/LOCATION/schedules/SCHEDULE_ID",
      "displayName": "DISPLAY_NAME",
      "startTime": "START_TIME",
      "state": "ACTIVE",
      "createTime": "2025-01-01T00:00:00.000000Z",
      "nextRunTime": "2045-08-01T00:00:00Z",
      "cron": "CRON_EXPRESSION",
      "maxConcurrentRunCount": "MAX_CONCURRENT_RUN_COUNT",
      "createPipelineJobRequest": PIPELINE_JOB_CREATION_REQUEST
    }

### Python

You can create a pipeline run schedule in the following ways:

  - Create a schedule based on a `PipelineJob` using the `PipelineJob.create_schedule` method.

  - Creating a schedule using the `PipelineJobSchedule.create` method.

While creating a pipeline run schedule, you can also pass the following placeholders supported by the KFP SDK as inputs:

  - `{{$.pipeline_job_name_placeholder}}`

  - `{{$.pipeline_job_resource_name_placeholder}}`

  - `{{$.pipeline_job_id_placeholder}}`

  - `{{$.pipeline_task_name_placeholder}}`

  - `{{$.pipeline_task_id_placeholder}}`

  - `{{$.pipeline_job_create_time_utc_placeholder}}`

  - `{{$.pipeline_job_schedule_time_utc_placeholder}}`

  - `{{$.pipeline_root_placeholder}}`

For more information, see [Special input types](https://www.kubeflow.org/docs/components/pipelines/v2/pipelines/pipeline-basics/#special-input-types) in the [Kubeflow Pipelines v2 documentation](https://www.kubeflow.org/docs/components/pipelines/v2/introduction/) .

### Create a schedule from a `PipelineJob`

Use the following sample to schedule pipeline runs using the `PipelineJob.create_schedule` method:

    from google.cloud import aiplatform
    
    pipeline_job = aiplatform.PipelineJob(
      template_path="COMPILED_PIPELINE_PATH",
      pipeline_root="PIPELINE_ROOT_PATH",
      display_name="DISPLAY_NAME",
    )
    
    pipeline_job_schedule = pipeline_job.create_schedule(
      display_name="SCHEDULE_NAME",
      cron="TZ=CRON",
      max_concurrent_run_count=MAX_CONCURRENT_RUN_COUNT,
      max_run_count=MAX_RUN_COUNT,
    )

  - COMPILED\_PIPELINE\_PATH : The path to your compiled pipeline YAML file. It can be a local path or a Cloud Storage URI.
    
    Optional: To specify a particular version of a template, include the version tag along with the path in any one of the following formats:
    
      - `  COMPILED_PIPELINE_PATH : TAG  ` , where TAG is the version tag.
    
      - `  COMPILED_PIPELINE_PATH @ SHA256_TAG  ` , where SHA256\_TAG is the `sha256` hash value of the pipeline version.

  - PIPELINE\_ROOT\_PATH : ( *optional* ) To override the pipeline root path specified in the pipeline definition, specify a path that your pipeline job can access, such as a Cloud Storage bucket URI.

  - DISPLAY\_NAME : The name of the pipeline. This will show up in the Google Cloud console.

  - SCHEDULE\_NAME : The name of the pipeline schedule. You can specify a name having a maximum length of 128 UTF-8 characters.

  - CRON : Cron schedule expression representing the frequency to schedule and execute pipeline runs. For more information, see [Cron](https://en.wikipedia.org/wiki/Cron) .

  - MAX\_CONCURRENT\_RUN\_COUNT : The maximum number of concurrent runs for the schedule.

  - MAX\_RUN\_COUNT : The maximum number of pipeline runs that the schedule creates after which it's completed.

### Create a schedule using `PipelineJobSchedule.create`

Use the following sample to schedule pipeline runs using the `PipelineJobSchedule.create` method:

    from google.cloud import aiplatform
    
    pipeline_job = aiplatform.PipelineJob(
      template_path="COMPILED_PIPELINE_PATH",
      pipeline_root="PIPELINE_ROOT_PATH",
      display_name="DISPLAY_NAME",
    )
    
    pipeline_job_schedule = aiplatform.PipelineJobSchedule(
      pipeline_job=pipeline_job,
      display_name="SCHEDULE_NAME"
    )
    
    pipeline_job_schedule.create(
      cron="TZ=CRON",
      max_concurrent_run_count=MAX_CONCURRENT_RUN_COUNT,
      max_run_count=MAX_RUN_COUNT,
    )

  - COMPILED\_PIPELINE\_PATH : The path to your compiled pipeline YAML file. It can be a local path or a Cloud Storage URI.
    
    Optional: To specify a particular version of a template, include the version tag along with the path in any one of the following formats:
    
      - COMPILED\_PIPELINE\_PATH : TAG , where TAG is the version tag.
    
      - COMPILED\_PIPELINE\_PATH @ SHA256\_TAG , where SHA256\_TAG is the sha256 hash value of the pipeline version.

  - PIPELINE\_ROOT\_PATH : ( *optional* ) To override the pipeline root path specified in the pipeline definition, specify a path that your pipeline job can access, such as a Cloud Storage bucket URI.

  - DISPLAY\_NAME : The name of the pipeline. This will show up in the Google Cloud console.

  - SCHEDULE\_NAME : The name of the pipeline schedule. You can specify a name having a maximum length of 128 UTF-8 characters.

  - CRON : Cron schedule expression representing the frequency to schedule and execute pipeline runs. For more information, see [Cron](https://en.wikipedia.org/wiki/Cron) .

  - MAX\_CONCURRENT\_RUN\_COUNT : The maximum number of concurrent runs for the schedule.

  - MAX\_RUN\_COUNT : The maximum number of pipeline runs that the schedule creates after which it's completed.

## List schedules

You can view the list of pipeline schedules created for your Google Cloud project.

### Console

You can view the list of pipeline schedules on the **Schedules** tab of the Google Cloud console for the selected region.

To view the list of pipeline schedules, in the Google Cloud console, in the Agent Platform section, go to the **Schedules** tab on the **Pipelines** page.

### REST

To list pipeline run schedules in your project, send a GET request by using the [projects.locations.schedules.list](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.schedules/list) method.

Before using any of the request data, make the following replacements:

  - LOCATION : The region where you want to run the pipeline. For more information about the regions where Agent Platform Pipelines is available, see the [Gemini Enterprise Agent Platform locations guide](https://docs.cloud.google.com/vertex-ai/docs/general/locations#feature-availability) .
  - PROJECT\_ID : The Google Cloud project where you want to run the pipeline.
  - FILTER : ( *optional* ) Expression to filter the list of schedules. For more information, see ...
  - PAGE\_SIZE : ( *optional* ) The number of schedules to be listed per page.
  - PAGE\_TOKEN : ( *optional* ) The standard list page token, typically obtained via `ListSchedulesResponse.next_page_token[]` from a previous `ScheduleService.ListSchedules[]` call.
  - ORDER\_BY : ( *optional* ) Comma-separated list of fields, indicating the sort order of the schedules in the response.

HTTP method and URL:

    GET https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/schedules?FILTER&PAGE_SIZE&PAGE_TOKEN&ORDER_BY

To send your request, choose one of these options:

#### curl

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) , or by using [Cloud Shell](https://docs.cloud.google.com/shell/docs) , which automatically logs you into the `gcloud` CLI . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Execute the following command:

    curl -X GET \
         -H "Authorization: Bearer $(gcloud auth print-access-token)" \
         "https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/schedules?FILTER&PAGE_SIZE&PAGE_TOKEN&ORDER_BY"

#### PowerShell

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Execute the following command:

    $cred = gcloud auth print-access-token
    $headers = @{ "Authorization" = "Bearer $cred" }
    
    Invoke-WebRequest `
        -Method GET `
        -Headers $headers `
        -Uri "https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/schedules?FILTER&PAGE_SIZE&PAGE_TOKEN&ORDER_BY" | Select-Object -Expand Content

You should see output similar to the following:

    {
      "schedules": [
        SCHEDULE_ENTITY_OBJECT_1,
        SCHEDULE_ENTITY_OBJECT_2,
        ...
      ],
    }

### Python

Use the following sample to list all the schedules in your project in the descending order of their creation times:

    from google.cloud import aiplatform
    
    aiplatform.PipelineJobSchedule.list(
      filter='display_name="DISPLAY_NAME"',
      order_by='create_time desc'
    )

DISPLAY\_NAME : The name of the pipeline schedule. You can specify a name having a maximum length of 128 UTF-8 characters.

## Retrieve a schedule

You can retrieve a pipeline run schedule using the schedule ID.

### REST

To retrieve a pipeline run schedule, send a GET request by using the [projects.locations.schedules.get](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.schedules/get) method and the schedule ID.

Before using any of the request data, make the following replacements:

  - LOCATION : The region where you want to run the pipeline. For more information about the regions where Agent Platform Pipelines is available, see the [Gemini Enterprise Agent Platform locations guide](https://docs.cloud.google.com/vertex-ai/docs/general/locations#feature-availability) .
  - PROJECT\_ID : The Google Cloud project where you want to run the pipeline.
  - SCHEDULE\_ID : Unique schedule ID generated while creating the schedule.

HTTP method and URL:

    GET https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/schedules/SCHEDULE_ID

To send your request, choose one of these options:

#### curl

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) , or by using [Cloud Shell](https://docs.cloud.google.com/shell/docs) , which automatically logs you into the `gcloud` CLI . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Execute the following command:

    curl -X GET \
         -H "Authorization: Bearer $(gcloud auth print-access-token)" \
         "https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/schedules/SCHEDULE_ID"

#### PowerShell

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Execute the following command:

    $cred = gcloud auth print-access-token
    $headers = @{ "Authorization" = "Bearer $cred" }
    
    Invoke-WebRequest `
        -Method GET `
        -Headers $headers `
        -Uri "https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/schedules/SCHEDULE_ID" | Select-Object -Expand Content

You should see output similar to the following. PIPELINE\_JOB\_CREATION\_REQUEST represents the API request to create the pipeline job.

    {
      "name": "projects/PROJECT_ID/locations/LOCATION/schedules/SCHEDULE_ID",
      "displayName": "schedule_display_name",
      "startTime": "2045-07-26T06:59:59Z",
      "state": "ACTIVE",
      "createTime": "20xx-01-01T00:00:00.000000Z",
      "nextRunTime": "2045-08-01T00:00:00Z",
      "cron": "TZ=America/New_York 0 0 1 * *",
      "maxConcurrentRunCount": "10",
      "createPipelineJobRequest": PIPELINE_JOB_CREATION_REQUEST
    }

### Python

Use the following sample to retrieve a pipeline run schedule using the schedule ID:

    from google.cloud import aiplatform
    
    pipeline_job_schedule = aiplatform.PipelineJobSchedule.get(schedule_id=SCHEDULE_ID)

SCHEDULE\_ID : Unique schedule ID generated while creating the schedule.

## Pause a schedule

You can pause an active pipeline schedule by specifying the schedule ID. When you pause a schedule, its state changes from `ACTIVE` to `PAUSED` .

### Console

You can pause a pipeline run schedule that's currently active.

Use the following instructions to pause a schedule:

1.  In the Google Cloud console, in the Agent Platform section, go to the **Schedules** tab on the **Pipelines** page.

2.  Go to the more\_vert options menu that's in the same row as the schedule you want to pause, and then click **Pause** . You can pause any schedule where the **Status** column shows **Active** .  

### REST

To pause a pipeline run schedule in your project, send a POST request by using the [projects.locations.schedules.pause](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.schedules/pause) method.

Before using any of the request data, make the following replacements:

  - LOCATION : The region where the pipeline run schedule is currently active. For more information about the regions where Agent Platform Pipelines is available, see the [Gemini Enterprise Agent Platform locations guide](https://docs.cloud.google.com/vertex-ai/docs/general/locations#feature-availability) .
  - PROJECT\_ID : The Google Cloud project where the pipeline run schedule is currently active.
  - SCHEDULE\_ID : Unique schedule ID generated while creating the schedule.

HTTP method and URL:

    POST https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/schedules/SCHEDULE_ID:pause

To send your request, choose one of these options:

#### curl

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) , or by using [Cloud Shell](https://docs.cloud.google.com/shell/docs) , which automatically logs you into the `gcloud` CLI . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Execute the following command:

    curl -X POST \
         -H "Authorization: Bearer $(gcloud auth print-access-token)" \
         -H "Content-Type: application/json; charset=utf-8" \
         -d "" \
         "https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/schedules/SCHEDULE_ID:pause"

#### PowerShell

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Execute the following command:

    $cred = gcloud auth print-access-token
    $headers = @{ "Authorization" = "Bearer $cred" }
    
    Invoke-WebRequest `
        -Method POST `
        -Headers $headers `
        -Uri "https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/schedules/SCHEDULE_ID:pause" | Select-Object -Expand Content

You should receive a successful status code (2xx) and an empty response.

### Python

Use the following sample to pause a pipeline run schedule:

    from google.cloud import aiplatform
    
    pipeline_job_schedule = aiplatform.PipelineJobSchedule.get(schedule_id=SCHEDULE_ID)
    
    pipeline_job_schedule.pause()

SCHEDULE\_ID : Unique schedule ID generated while creating the schedule.

## Update a schedule

You can update an existing pipeline schedule that was created for your Google Cloud project.

Updating a schedule is similar to deleting and recreating a schedule. When you update a schedule, new runs are scheduled based on the frequency of the updated schedule. New runs are no longer created based on the old schedule and any queued runs are dropped. Pipeline runs that are already created by the old schedule aren't paused or canceled.

### REST

To update a pipeline run schedule in your project, send a PATCH request by using the [projects.locations.schedules.patch](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.schedules/patch) method.

Before using any of the request data, make the following replacements:

  - LOCATION : The region where you want to run the pipeline. For more information about the regions where Agent Platform Pipelines is available, see the [Gemini Enterprise Agent Platform locations guide](https://docs.cloud.google.com/vertex-ai/docs/general/locations#feature-availability) .
  - PROJECT\_ID : The Google Cloud project where you want to run the pipeline.
  - DISPLAY\_NAME : The name of the pipeline schedule. You can specify a name having a maximum length of 128 UTF-8 characters.
  - MAX\_CONCURRENT\_RUN\_COUNT : The maximum number of concurrent runs for the schedule.

HTTP method and URL:

    POST https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/schedules/SCHEDULE_ID?updateMask=display_name,max_run_count -d '{"display_name":"DISPLAY_NAME", "max_concurrent_run_count": MAX_CONCURRENT_RUN_COUNT}'

To send your request, choose one of these options:

#### curl

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) , or by using [Cloud Shell](https://docs.cloud.google.com/shell/docs) , which automatically logs you into the `gcloud` CLI . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Execute the following command:

    curl -X POST \
         -H "Authorization: Bearer $(gcloud auth print-access-token)" \
         -H "Content-Type: application/json; charset=utf-8" \
         -d "" \
         "https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/schedules/SCHEDULE_ID?updateMask=display_name,max_run_count -d '{"display_name":"DISPLAY_NAME", "max_concurrent_run_count": MAX_CONCURRENT_RUN_COUNT}'"

#### PowerShell

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Execute the following command:

    $cred = gcloud auth print-access-token
    $headers = @{ "Authorization" = "Bearer $cred" }
    
    Invoke-WebRequest `
        -Method POST `
        -Headers $headers `
        -Uri "https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/schedules/SCHEDULE_ID?updateMask=display_name,max_run_count -d '{"display_name":"DISPLAY_NAME", "max_concurrent_run_count": MAX_CONCURRENT_RUN_COUNT}'" | Select-Object -Expand Content

You should see output similar to the following. Based on the update, the NEXT\_RUN\_TIME is recalculated. When you update the schedule, the START\_TIME remains unchanged.

    {
      "name": "projects/PROJECT_ID/locations/LOCATION/schedules/SCHEDULE_ID",
      "displayName": "DISPLAY_NAME",
      "startTime": "START_TIME",
      "state": "ACTIVE",
      "createTime": "2025-01-01T00:00:00.000000Z",
      "nextRunTime": NEXT_RUN_TIME,
      "maxConcurrentRunCount": "MAX_CONCURRENT_RUN_COUNT",
    }

### Python

Use the following sample to schedule pipeline runs using the `PipelineJobSchedule.update` method:

    from google.cloud import aiplatform
    
    pipeline_job_schedule = aiplatform.PipelineJobSchedule.get(schedule_id=SCHEDULE_ID)
    
    pipeline_job_schedule.update(
      display_name='DISPLAY_NAME',
      max_concurrent_run_count=MAX_CONCURRENT_RUN_COUNT,
    )

  - SCHEDULE\_ID : Unique schedule ID generated while creating the schedule.
  - DISPLAY\_NAME : The name of the pipeline schedule. You can specify a name having a maximum length of 128 UTF-8 characters.
  - MAX\_CONCURRENT\_RUN\_COUNT : The maximum number of concurrent runs for the schedule.

## Resume a schedule

You can resume a paused pipeline schedule by specifying the schedule ID. When you resume a schedule, its state changes from `PAUSED` to `ACTIVE` .

### Console

You can resume a pipeline run schedule that's currently paused.

Use the following instructions to resume a schedule:

1.  In the Google Cloud console, in the Agent Platform section, go to the **Schedules** tab on the **Pipelines** page.

2.  Go to the more\_vert options menu that's in the same row as the schedule you want to resume, and then click **Resume** . You can resume any schedule where the **Status** column shows **Paused** .  

### REST

To resume a pipeline run schedule in your project, send a POST request by using the [projects.locations.schedules.resume](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.schedules/resume) method.

Before using any of the request data, make the following replacements:

  - LOCATION : The region where the pipeline run schedule is currently paused. For more information about the regions where Agent Platform Pipelines is available, see the [Gemini Enterprise Agent Platform locations guide](https://docs.cloud.google.com/vertex-ai/docs/general/locations#feature-availability) .
  - PROJECT\_ID : The Google Cloud project where the pipeline run schedule is currently paused.
  - SCHEDULE\_ID : Unique schedule ID generated while creating the schedule.
  - CATCH\_UP : ( *Optional* ) Indicate whether the paused schedule should backfill the skipped pipeline runs. To backfill and reschedule the skipped pipeline runs, enter the following:  
    `{ "catch_up":true }` This parameter is set to \`false\`, by default.

HTTP method and URL:

    POST https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/schedules/SCHEDULE_ID:resume -d 'CATCH_UP'

To send your request, choose one of these options:

#### curl

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) , or by using [Cloud Shell](https://docs.cloud.google.com/shell/docs) , which automatically logs you into the `gcloud` CLI . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Execute the following command:

    curl -X POST \
         -H "Authorization: Bearer $(gcloud auth print-access-token)" \
         -H "Content-Type: application/json; charset=utf-8" \
         -d "" \
         "https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/schedules/SCHEDULE_ID:resume -d 'CATCH_UP'"

#### PowerShell

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Execute the following command:

    $cred = gcloud auth print-access-token
    $headers = @{ "Authorization" = "Bearer $cred" }
    
    Invoke-WebRequest `
        -Method POST `
        -Headers $headers `
        -Uri "https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/schedules/SCHEDULE_ID:resume -d 'CATCH_UP'" | Select-Object -Expand Content

You should receive a successful status code (2xx) and an empty response.

### Python

Use the following sample to resume a paused pipeline run schedule:

    from google.cloud import aiplatform
    
    pipeline_job_schedule = aiplatform.PipelineJobSchedule.get(schedule_id=SCHEDULE_ID)
    
    pipeline_job_schedule.resume(catch_up=CATCH_UP)

  - SCHEDULE\_ID : Unique schedule ID generated while creating the schedule.
  - CATCH\_UP : ( *Optional* ) Indicate whether the paused schedule should backfill the skipped pipeline runs. To backfill and reschedule the skipped pipeline runs, enter the following:  
    `{ "catch_up":true }`

## Delete a schedule

You can delete a pipeline schedule by specifying the schedule ID.

### Console

You can delete a pipeline run schedule regardless of its status.

Use the following instructions to delete a schedule:

1.  In the Google Cloud console, in the Agent Platform section, go to the **Schedules** tab on the **Pipelines** page.

2.  Go to the more\_vert options menu that's in the same row as the schedule you want to delete, and then click **Delete** .

3.  To confirm deletion, click **Delete** .

### REST

To delete a pipeline run schedule in your project, send a DELETE request by using the [projects.locations.schedules.delete](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.schedules/delete) method.

Before using any of the request data, make the following replacements:

  - LOCATION : The region where you want to delete the pipeline schedule. For more information about the regions where Agent Platform Pipelines is available, see the [Gemini Enterprise Agent Platform locations guide](https://docs.cloud.google.com/vertex-ai/docs/general/locations#feature-availability) .
  - PROJECT\_ID : The Google Cloud project where you want to delete the schedule.
  - SCHEDULE\_ID : The unique schedule ID generated while creating the schedule.

HTTP method and URL:

    DELETE https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/schedules/SCHEDULE_ID

To send your request, choose one of these options:

#### curl

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) , or by using [Cloud Shell](https://docs.cloud.google.com/shell/docs) , which automatically logs you into the `gcloud` CLI . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Execute the following command:

    curl -X DELETE \
         -H "Authorization: Bearer $(gcloud auth print-access-token)" \
         "https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/schedules/SCHEDULE_ID"

#### PowerShell

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Execute the following command:

    $cred = gcloud auth print-access-token
    $headers = @{ "Authorization" = "Bearer $cred" }
    
    Invoke-WebRequest `
        -Method DELETE `
        -Headers $headers `
        -Uri "https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/schedules/SCHEDULE_ID" | Select-Object -Expand Content

You should see output similar to the following. OPERATION\_ID represents the delete operation.

    {
      "name": "projects/PROJECT_ID/locations/LOCATION/operations/OPERATION_ID",
      "metadata": {
        "@type": "type.googleapis.com/google.cloud.aiplatform.v1.DeleteOperationMetadata",
        "genericMetadata": {
          "createTime": "20xx-01-01T00:00:00.000000Z",
          "updateTime": "20xx-01-01T00:00:00.000000Z"
        }
      },
      "done": true,
      "response": {
        "@type": "type.googleapis.com/google.protobuf.Empty"
      }
    }

### Python

Use the following sample to delete a pipeline run schedule:

    from google.cloud import aiplatform
    
    pipeline_job_schedule = aiplatform.PipelineJobSchedule.get(schedule_id=SCHEDULE_ID)
    
    pipeline_job_schedule.delete()

SCHEDULE\_ID : Unique schedule ID generated while creating the schedule.

## List all pipeline jobs created by a schedule

You can view a list of all the pipeline jobs created by a schedule by specifying the schedule ID.

### REST

To list all the pipeline runs that have been created by a pipeline schedule, send a GET request by using the [projects.locations.pipelineJobs](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.pipelineJobs) method.

Before using any of the request data, make the following replacements:

  - LOCATION : The region where you want to run the pipeline. For more information about the regions where Agent Platform Pipelines is available, see the [Gemini Enterprise Agent Platform locations guide](https://docs.cloud.google.com/vertex-ai/docs/general/locations#feature-availability) .
  - PROJECT\_ID : The Google Cloud project where you want to run the pipeline.
  - SCHEDULE\_ID : Unique schedule ID generated while creating the schedule.

HTTP method and URL:

    GET https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/pipelineJobs?filter=schedule_name=projects/PROJECT/locations/LOCATION/schedules/SCHEDULE_ID

To send your request, choose one of these options:

#### curl

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) , or by using [Cloud Shell](https://docs.cloud.google.com/shell/docs) , which automatically logs you into the `gcloud` CLI . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Execute the following command:

    curl -X GET \
         -H "Authorization: Bearer $(gcloud auth print-access-token)" \
         "https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/pipelineJobs?filter=schedule_name=projects/PROJECT/locations/LOCATION/schedules/SCHEDULE_ID"

#### PowerShell

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Execute the following command:

    $cred = gcloud auth print-access-token
    $headers = @{ "Authorization" = "Bearer $cred" }
    
    Invoke-WebRequest `
        -Method GET `
        -Headers $headers `
        -Uri "https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/pipelineJobs?filter=schedule_name=projects/PROJECT/locations/LOCATION/schedules/SCHEDULE_ID" | Select-Object -Expand Content

You should see output similar to the following.

    {
      "pipelineJobs": [
        PIPELINE_JOB_ENTITY_1,
        PIPELINE_JOB_ENTITY_2,
        ...
      ],
    }

### Python

Use the following sample to list all the pipeline jobs created by a schedule in the descending order of their creation times:

    from google.cloud import aiplatform
    
    pipeline_job_schedule = aiplatform.PipelineJobSchedule.get(schedule_id=SCHEDULE_ID)
    
    pipeline_job_schedule.list_jobs(order_by='create_time_desc')

SCHEDULE\_ID : Unique schedule ID generated while creating the schedule.
