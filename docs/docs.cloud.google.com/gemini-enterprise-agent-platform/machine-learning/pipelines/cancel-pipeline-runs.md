---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/pipelines/cancel-pipeline-runs
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/pipelines/cancel-pipeline-runs
title: Cancel pipeline runs
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

If you no longer need a scheduled or running pipeline run, you can cancel it. If there are multiple pipeline runs to cancel, you can batch cancel those pipeline runs.

When you initiate a pipeline run cancellation, the status of the pipeline run changes to **Canceling** . During this status, Gemini Enterprise Agent Platform Pipelines cancels all the remaining tasks in the pipeline and all the Google Cloud services and resources invoked by the pipeline run. After all of these tasks, services, and resources are canceled, the pipeline status changes to **Canceled** .

Note that a canceled pipeline run isn't deleted. You have the option to [delete the pipeline run](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/pipelines/delete-pipeline-runs) after you cancel it.

## Cancel a pipeline run

To cancel a pipeline run, use the Google Cloud console, the REST API, or the Agent Platform SDK for Python.

### Console

Use the following instructions to cancel an ongoing pipeline run from the Google Cloud console:

1.  In the Agent Platform section, go to the **Runs** tab on the **Pipelines** page.
2.  In the **Run** column, click the name of the pipeline run that you want to cancel.
3.  On the page displaying the pipeline run details, click **Stop** . This option is available only if the pipeline run is in the **Running** status.

After you click **Stop** , the status of the pipeline changes to **Canceling** . After all the pipeline tasks, Google Cloud services, and Google Cloud resources invoked by the run are canceled, the status changes to **Canceled** .

### REST

To cancel an ongoing or scheduled pipeline run, send a `POST` request by using the [pipelineJobs.cancel](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.pipelineJobs/cancel) method.

Before using any of the request data, make the following replacements:

  - LOCATION : The region where the pipeline run is located. For more information about the regions where Agent Platform Pipelines is available, see the [Gemini Enterprise Agent Platform locations guide](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/locations#feature-availability) .
  - PROJECT\_ID : The Google Cloud project containing the pipeline run.
  - PIPELINE\_RUN\_ID : The unique ID of the pipeline run that you want to cancel. The pipeline run ID is displayed in the **Runs** tab on the **Pipelines** page in the Google Cloud console.

HTTP method and URL:

    POST https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/pipelineJobs/PIPELINE_RUN_ID:cancel

To send your request, choose one of these options:

#### curl

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) , or by using [Cloud Shell](https://docs.cloud.google.com/shell/docs) , which automatically logs you into the `gcloud` CLI . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Execute the following command:

    curl -X POST \
         -H "Authorization: Bearer $(gcloud auth print-access-token)" \
         -H "Content-Type: application/json; charset=utf-8" \
         -d "" \
         "https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/pipelineJobs/PIPELINE_RUN_ID:cancel"

#### PowerShell

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Execute the following command:

    $cred = gcloud auth print-access-token
    $headers = @{ "Authorization" = "Bearer $cred" }
    
    Invoke-WebRequest `
        -Method POST `
        -Headers $headers `
        -Uri "https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/pipelineJobs/PIPELINE_RUN_ID:cancel" | Select-Object -Expand Content

You should receive a successful status code (2xx) and an empty response.

### Python

Use the following sample to cancel an ongoing or scheduled pipeline run by using the [`PipelineJob.cancel`](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.PipelineJob#google_cloud_aiplatform_PipelineJob_cancel) method:

    from google.cloud import aiplatform
    aiplatform.init(project=PROJECT_ID, location=LOCATION)
    pipeline_job = aiplatform.PipelineJob.get(resource_name="PIPELINE_RUN_ID")
    pipeline_job.cancel()

Replace the following:

  - PROJECT\_ID : The Google Cloud project containing the pipeline run.
  - LOCATION : The region where the pipeline run is located. For more information about the regions where Agent Platform Pipelines is available, see the [Gemini Enterprise Agent Platform locations guide](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/locations#feature-availability) .
  - PIPELINE\_RUN\_ID with the unique ID of the pipeline run that you want to cancel. The ID is displayed in the **Runs** tab on the **Pipelines** page in the Google Cloud console.

## Cancel multiple pipeline runs

To cancel multiple pipeline runs simultaneously, use the REST API, or the Agent Platform SDK for Python. You can batch cancel pipeline runs that are in the same project and region.

### REST

To batch cancel multiple ongoing or scheduled pipeline runs, send a `POST` request by using the [pipelineJobs.batchCancel](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.pipelineJobs/batchCancel) method.

Before using any of the request data, make the following replacements:

  - LOCATION : The region where the pipeline runs are located. For more information about the regions where Agent Platform Pipelines is available, see the [Gemini Enterprise Agent Platform locations guide](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/locations#feature-availability) .
  - PROJECT\_ID : The Google Cloud project containing the pipeline runs.
  - PIPELINE\_RUN\_ID\_1 , PIPELINE\_RUN\_ID\_2 : The IDs of the pipeline jobs that you want to cancel. You can find the job ID in the **Runs** tab on the **Pipelines** page in the Google Cloud console.

HTTP method and URL:

    POST https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/pipelineJobs:batchCancel

Request JSON body:

    {
      "names": [
        "projects/PROJECT_ID/locations/LOCATION/pipelineJobs/PIPELINE_RUN_ID_1",
        "projects/PROJECT_ID/locations/LOCATION/pipelineJobs/PIPELINE_RUN_ID_2"
      ]
    }

To send your request, choose one of these options:

#### curl

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) , or by using [Cloud Shell](https://docs.cloud.google.com/shell/docs) , which automatically logs you into the `gcloud` CLI . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Save the request body in a file named `request.json` , and execute the following command:

    curl -X POST \
         -H "Authorization: Bearer $(gcloud auth print-access-token)" \
         -H "Content-Type: application/json; charset=utf-8" \
         -d @request.json \
         "https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/pipelineJobs:batchCancel"

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
        -Uri "https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/pipelineJobs:batchCancel" | Select-Object -Expand Content

You should receive a JSON response similar to the following:

    {
      "name": "projects/PROJECT_NUMBER/locations/LOCATION/operations/OPERATION_ID",
      "metadata": {
        "@type": "type.googleapis.com/google.cloud.aiplatform.v1.BatchCancelPipelineJobsOperationMetadata",
        "genericMetadata": {
          "createTime": "2025-05-25T16:11:21.011113Z",
          "updateTime": "2025-05-25T16:11:21.011113Z"
        }
      }
    }

### Python

Use the following sample to cancel multiple ongoing or scheduled pipeline runs by using the [`PipelineJob.batch_cancel`](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.PipelineJob#google_cloud_aiplatform_PipelineJob_batch_cancel) method:

    from google.cloud import aiplatform_v1
    from google.api_core.client_options import ClientOptions
    pipeline_run_ids_to_cancel = [
      "PIPELINE_RUN_ID_1",
      "PIPELINE_RUN_ID_2",
    ]
    client_options = ClientOptions(api_endpoint=f"LOCATION-aiplatform.googleapis.com")
    pipeline_job_client = aiplatform_v1.PipelineServiceClient(client_options=client_options)
    pipeline_resource_names_to_cancel = []
    for run_id in pipeline_run_ids_to_cancel:
      full_resource_name = f"projects/PROJECT_NUMBER/locations/LOCATION/pipelineJobs/{run_id.strip()}"
      pipeline_resource_names_to_cancel.append(full_resource_name)
    parent = f"projects/PROJECT_ID/locations/LOCATION"
    pipeline_job_client.batch_cancel_pipeline_jobs(parent=parent, names=pipeline_resource_names_to_cancel)

Replace the following:

  - PROJECT\_ID : Your project ID.
  - LOCATION : The region where the pipeline runs were created.
  - PROJECT\_NUMBER : The project number for your project. You can locate this project number in the Google Cloud console.For more information, see [Find the project name, number, and ID](https://docs.cloud.google.com/resource-manager/docs/creating-managing-projects#identifying_projects) .
  - PIPELINE\_RUN\_ID\_1 and PIPELINE\_JOB\_ID\_2 : The unique IDs of the pipeline runs that you want to cancel. The pipeline run IDs are displayed in the **Runs** tab on the **Pipelines** page in the Google Cloud console.
