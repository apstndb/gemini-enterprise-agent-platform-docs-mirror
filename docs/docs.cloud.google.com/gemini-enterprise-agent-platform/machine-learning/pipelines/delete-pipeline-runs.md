---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/pipelines/delete-pipeline-runs
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/pipelines/delete-pipeline-runs
title: Delete pipeline runs
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

If your project contains failed or canceled pipeline runs, you can delete them. You can delete a maximum of 32 pipeline runs in a batch deletion operation.

When you initiate a pipeline run deletion, the status of the pipeline run changes to **Being deleted** . After the pipeline run remains in this status for an hour, Gemini Enterprise Agent Platform Pipelines queues it for permanent deletion. Subsequently, a daily scheduled operation permanently removes all pipeline runs queued for permanent deletion.

## Delete a pipeline run

To delete a pipeline run, use the Google Cloud console, the REST API, or the Agent Platform SDK for Python.

### Console

Use the following instructions to delete an ongoing pipeline run from the Google Cloud console:

1.  In the Agent Platform section, go to the **Runs** tab on the **Pipelines** page.
2.  Select the checkbox next to a canceled or failed pipeline run that you want to delete.
3.  Click **Delete** . This option is available only if the pipeline run is in the **Failed** or **Canceled** status.

After you click **Delete** , the status of the pipeline run changes to **Being deleted** , before it's permanently deleted.

### REST

To delete an ongoing or scheduled pipeline run, send a `DELETE` request by using the [pipelineJobs.delete](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.pipelineJobs/delete) method.

Before using any of the request data, make the following replacements:

  - LOCATION : The region where the pipeline run is located. For more information about the regions where Agent Platform Pipelines is available, see the [Gemini Enterprise Agent Platform locations guide](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/locations#feature-availability) .
  - PROJECT\_ID : The Google Cloud project containing the pipeline run.
  - PIPELINE\_RUN\_ID : The unique ID of the pipeline run that you want to delete. The pipeline run ID is displayed in the **Runs** tab on the **Pipelines** page in the Google Cloud console.

HTTP method and URL:

    DELETE https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/pipelineJobs/PIPELINE_RUN_ID

To send your request, choose one of these options:

#### curl

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) , or by using [Cloud Shell](https://docs.cloud.google.com/shell/docs) , which automatically logs you into the `gcloud` CLI . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Execute the following command:

    curl -X DELETE \
         -H "Authorization: Bearer $(gcloud auth print-access-token)" \
         "https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/pipelineJobs/PIPELINE_RUN_ID"

#### PowerShell

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Execute the following command:

    $cred = gcloud auth print-access-token
    $headers = @{ "Authorization" = "Bearer $cred" }
    
    Invoke-WebRequest `
        -Method DELETE `
        -Headers $headers `
        -Uri "https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/pipelineJobs/PIPELINE_RUN_ID" | Select-Object -Expand Content

You should receive a JSON response similar to the following:

    {
      "name": "projects/PROJECT_NUMBER/locations/us-central1/operations/OPERATION_ID",
      "metadata": {
        "@type": "type.googleapis.com/google.cloud.aiplatform.v1.DeleteOperationMetadata",
        "genericMetadata": {
          "createTime": "2025-07-25T16:23:47.201943Z",
          "updateTime": "2025-07-25T16:23:47.201943Z"
        }
      },
      "done": true,
      "response": {
        "@type": "type.googleapis.com/google.protobuf.Empty"
      }
    }

### Python

Use the following sample to delete a failed or cancelled pipeline run by using the [`PipelineJob.delete`](https://docs.cloud.google.com/google.cloud.aiplatform.PipelineJob#google_cloud_aiplatform_PipelineJob_delete) method:

    from google.cloud import aiplatform
    aiplatform.init(project="PROJECT_ID", location="LOCATION")
    pipeline_job = aiplatform.PipelineJob.get(resource_name="PIPELINE_RUN_ID")
    pipeline_job.delete()

Replace the following:

  - PROJECT\_ID : The Google Cloud project containing the pipeline run.
  - LOCATION : The region where the pipeline run is located. For more information about the regions where Agent Platform Pipelines is available, see the [Gemini Enterprise Agent Platform locations guide](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/locations#feature-availability) .
  - PIPELINE\_RUN\_ID with the unique ID of the pipeline run that you want to delete. The ID is displayed in the **Runs** tab on the **Pipelines** page in the Google Cloud console.

## Delete multiple pipeline runs

To delete multiple failed or cancelled pipeline runs simultaneously, use the Google Cloud console, the REST API, or the Agent Platform SDK for Python. You can batch delete pipeline runs that are in the same project and region.

### Console

Use the following instructions to delete multiple ongoing pipeline run from the Google Cloud console:

1.  In the Agent Platform section, go to the **Runs** tab on the **Pipelines** page.
2.  Select the checkboxes next to the canceled or failed pipeline runs that you want to delete.
3.  Click **Delete** . This option is available only if all of the selected pipeline runs are in the **Failed** or **Canceled** status.

After you click **Delete** , the status of the selected pipeline runs changes to **Being deleted** , before the runs are permanently deleted.

### REST

To batch delete multiple ongoing or scheduled pipeline runs, send a `POST` request by using the [pipelineJobs.batchDelete](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.pipelineJobs/batchDelete) method.

Before using any of the request data, make the following replacements:

  - LOCATION : The region where the pipeline runs are located. For more information about the regions where Agent Platform Pipelines is available, see the [Gemini Enterprise Agent Platform locations guide](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/locations#feature-availability) .
  - PROJECT\_ID : The Google Cloud project containing the pipeline runs.
  - PIPELINE\_RUN\_ID\_1 , PIPELINE\_RUN\_ID\_2 : The IDs of the pipeline jobs that you want to delete. You can find the job ID in the **Runs** tab on the **Pipelines** page in the Google Cloud console.

HTTP method and URL:

    POST https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/pipelineJobs:batchDelete

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
         "https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/pipelineJobs:batchDelete"

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
        -Uri "https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/pipelineJobs:batchDelete" | Select-Object -Expand Content

You should receive a JSON response similar to the following:

    {
      "name": "projects/PROJECT_NUMBER/locations/LOCATION/operations/OPERATION_ID",
      "metadata": {
        "@type": "type.googleapis.com/google.cloud.aiplatform.v1.DeleteOperationMetadata",
        "genericMetadata": {
          "createTime": "2025-05-31T16:07:12.233655Z",
          "updateTime": "2025-05-31T16:07:12.233655Z"
        }
      },
      "done": true,
      "response": {
        "@type": "type.googleapis.com/google.cloud.aiplatform.v1.BatchDeletePipelineJobsResponse",
        "pipelineJobs": [
          {
            "name": "projects/PROJECT_ID/locations/LOCATION/pipelineJobs/PIPELINE_RUN_ID_1"
          },
          {
            "name": "projects/PROJECT_ID/locations/LOCATION/pipelineJobs/PIPELINE_RUN_ID_2"
          }
        ]
      }
    }

### Python

Use the following sample to delete multiple ongoing or scheduled pipeline runs by using the [`PipelineJob.batch_delete`](https://docs.cloud.google.com/google.cloud.aiplatform.PipelineJob#google_cloud_aiplatform_PipelineJob_batch_delete) method:

    from google.cloud import aiplatform_v1
    from google.api_core.client_options import ClientOptions
    pipeline_run_ids_to_delete = ["PIPELINE_RUN_ID_1",
      "PIPELINE_RUN_ID_2",
    ]
    client_options = ClientOptions(api_endpoint=f"LOCATION-aiplatform.googleapis.com")
    
    pipeline_job_client = aiplatform_v1.PipelineServiceClient(client_options=client_options)
    pipeline_resource_names_to_delete = []
    for run_id in pipeline_run_ids_to_delete:
      full_resource_name = f"projects/PROJECT_NUMBER/locations/LOCATION/pipelineJobs/{run_id}"
      pipeline_resource_names_to_delete.append(full_resource_name)
    parent = f"projects/PROJECT_ID/locations/LOCATION"
    
    pipeline_job_client.batch_delete_pipeline_jobs(
      parent=parent,
      names=pipeline_resource_names_to_delete
    )

Replace the following:

  - PROJECT\_ID : Your project ID.
  - PROJECT\_ID : The Google Cloud project containing the pipeline runs.
  - PROJECT\_NUMBER : The project number for your project. You can locate this project number in the Google Cloud console. For more information, see [Find the project name, number, and ID](https://docs.cloud.google.com/resource-manager/docs/creating-managing-projects#identifying_projects) .
  - PIPELINE\_RUN\_ID\_1 , PIPELINE\_RUN\_ID\_2 : The IDs of the pipeline jobs that you want to delete. The pipeline run IDs are displayed in the **Runs** tab on the **Pipelines** page in the Google Cloud console.
