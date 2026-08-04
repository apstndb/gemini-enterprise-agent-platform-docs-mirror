---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/training-clusters/manage-clusters-slurm
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/training-clusters/manage-clusters-slurm
title: Manage training clusters by using the Slurm Job API
description: Use the Slurm Job API to manage Gemini Enterprise Agent Platform training clusters. Submit, check, list, and cancel Slurm jobs on your cluster, from a script, notebook, or a CI/CD pipeline.
data_source: docs.cloud.google.com
---

The Slurm Job API lets you manage your Gemini Enterprise Agent Platform training clusters through the Agent Platform API, a script, a notebook, or a CI/CD pipeline. The Slurm Job API lets you manage the Slurm cluster job without connecting to the cluster with SSH.

## Prerequisites

Before you use the Slurm Job API to manage your cluster, make sure that you meet the following requirements:

  - You have access to the training clusters, typically through the **Vertex AI User** role `roles/aiplatform.user` on the cluster's project, or any role that includes the `aiplatform.googleapis.com/modelDevelopmentClusters.run` permission.

  - Google Cloud CLI is installed and you've configured Application Default Credentials ( `gcloud auth application-default login` ). For automated tools that can't run an interactive login, authenticate as a service account with the `aiplatform.googleapis.com/modelDevelopmentClusters.run` permission.

  - You know your cluster's project ID, region, and cluster ID.

Additionally, we recommend that you set up a convenience alias:

    alias gcurl='curl -H "Authorization: Bearer $(gcloud auth application-default print-access-token)" -H "Content-Type: application/json"'

## Overview

Every call is a POST request to the `callSlurmRestApi` endpoint for your cluster. In the request body you provide the following fields:

  - **`method`** : The Slurm REST HTTP method, such as: `HTTP_METHOD_GET` , `HTTP_METHOD_POST` , or `HTTP_METHOD_DELETE` .

  - **`path`** : The Slurm REST path. For example, `/slurm/v0.0.42/job/submit` . Use the Slurm version that your cluster is running. The examples in this guide use v0.0.42.

> **Note:** The [public Slurm guide](https://slurm.schedmd.com/rest_api.html) defaults to v0.0.45. To view the API reference for v0.0.42, run `slurmrestd --generate-openapi-spec -d v0.0.42` while connected using SSH to your cluster.

  - **`body`** : A JSON object with the request payload. The body is required for `HTTP_METHOD_POST` requests. Omit it for `HTTP_METHOD_GET` and `HTTP_METHOD_DELETE` requests.

The response contains the following fields:

  - **`status`** : the HTTP status returned by the Slurm Job API. For example, `200` .

  - **`body`** : the response from the Slurm Job API as a JSON string. Parse the body fields for fields that you need, such as the job ID or the job list.

You run jobs on your own Linux account on the training clusters automatically. There is no additional configuration, and you can't run the job as another user. SSH isn't required, because everything is done through the Agent Platform API.

Each call returns Slurm's response directly, without an operation to poll. You can follow a job's status over time. For more information, see [Check job status](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/training-clusters/manage-clusters-slurm#check-job-status) .

## Call the API

The following sections show how to use the Slurm Job API.

### Submit a job

    gcurl -X POST \
      "https://REGION-aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/REGION/modelDevelopmentClusters/CLUSTER_ID:callSlurmRestApi" \
      -d '{
        "method": "HTTP_METHOD_POST",
        "path": "/slurm/v0.0.42/job/submit",
        "body": {
          "job": {
            "name": "my-run",
            "partition": "PARTITION",
            "current_working_directory": "/home/USERNAME",
            "minimum_nodes": 1,
            "tasks_per_node": 1,
            "environment": ["PATH=/bin:/usr/bin"],
            "time_limit": {"set": true, "number": 120}
          },
          "script": "#!/bin/bash\necho hello\nsleep 5\necho done\n"
        }
      }'

Replace the following:

  - `  REGION  ` : The region that your cluster is in.

  - `  PROJECT_ID  ` : Your project ID.

  - `  CLUSTER_ID  ` : Your cluster ID.

  - `  PARTITION  ` : The Slurm partition you're connecting to.

  - `  USERNAME  ` : Your username on the Slurm partition.

The `time_limit` value is time in minutes. The `script` field holds the script contents, not a path to a file.

The Slurm Job API returns the new job's ID in the response body. You can use the `jq` command to isolate the job ID:

    gcurl -sS -X POST "https://REGION-aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/REGION/modelDevelopmentClusters/CLUSTER_ID:callSlurmRestApi" \
      -d '{ ... }' | jq -r '.body | fromjson | .job_id'

### Check job status

Use the following to monitor a running job. Poll until the status reaches a stopped state, such as `COMPLETED` , `FAILED` , or `CANCELLED` :

    gcurl -X POST \
      "https://REGION-aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/REGION/modelDevelopmentClusters/CLUSTER_ID:callSlurmRestApi" \
      -d '{
        "method": "HTTP_METHOD_GET",
        "path": "/slurm/v0.0.42/job/JOB_ID"
      }'

Replace the following:

  - `  REGION  ` : The region that your cluster is in.

  - `  PROJECT_ID  ` : Your project ID.

  - `  CLUSTER_ID  ` : Your cluster ID.

  - `  JOB_ID  ` : The job ID of the Slurm job.

### List jobs

Use the following to list running jobs:

    gcurl -X POST \
      "https://REGION-aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/REGION/modelDevelopmentClusters/CLUSTER_ID:callSlurmRestApi" \
      -d '{
        "method": "HTTP_METHOD_GET",
        "path": "/slurm/v0.0.42/jobs/"
      }'

Replace the following:

  - `  REGION  ` : The region that your cluster is in.

  - `  PROJECT_ID  ` : Your project ID.

  - `  CLUSTER_ID  ` : Your cluster ID.

### Cancel a job

Canceling is accepted immediately, but the job takes a moment to stop. [Check its status](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/training-clusters/manage-clusters-slurm#check-job-status) to verify that its status is `CANCELLED` . You can cancel only your own jobs. Canceling a completed job is safe and returns success.

Use the following to cancel a running job:

    gcurl -X POST \
      "https://REGION-aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/REGION/modelDevelopmentClusters/CLUSTER_ID:callSlurmRestApi" \
      -d '{
        "method": "HTTP_METHOD_DELETE",
        "path": "/slurm/v0.0.42/job/JOB_ID"
      }'

Replace the following:

  - `  REGION  ` : The region that your cluster is in.

  - `  PROJECT_ID  ` : Your project ID.

  - `  CLUSTER_ID  ` : Your cluster ID.

  - `  JOB_ID  ` : The job ID of the Slurm job.

### Display a finished job

Checking a job with the `/slurm` path works only while the job is still in the live queue. For completed jobs, use the `slurmdb` path instead:

    gcurl -X POST \
      "https://REGION-aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/REGION/modelDevelopmentClusters/CLUSTER_ID:callSlurmRestApi" \
      -d '{
        "method": "HTTP_METHOD_GET",
        "path": "/slurmdb/v0.0.42/job/JOB_ID"
      }'

Replace the following:

  - `  REGION  ` : The region that your cluster is in.

  - `  PROJECT_ID  ` : Your project ID.

  - `  CLUSTER_ID  ` : Your cluster ID.

  - `  JOB_ID  ` : The job ID of the Slurm job.

### Using the Slurm Job API from Python

If you prefer using Python to curl, you can use the following helper script to submit jobs, check job status, and cancel jobs. The helper script uses the google-auth library for Application Default Credentials.

Do the following to use the Slurm Job API from Python:

1.  Install Application Default Credentials:
    
        pip install google-auth requests

2.  Use the following Python script to use the API:
    
        import json
        import google.auth
        import google.auth.transport.requests
        
        # Fill in your cluster's values.
        PROJECT_ID = "PROJECT_ID"
        REGION = "REGION"
        CLUSTER_ID = "CLUSTER_ID"
        PARTITION = "PARTITION"
        USERNAME = "USERNAME"
        
        # Application Default Credentials: gcloud auth application-default login, or a
        # service account for automated callers.
        credentials, _ = google.auth.default(
            scopes=["https://www.googleapis.com/auth/cloud-platform"])
        session = google.auth.transport.requests.AuthorizedSession(credentials)
        
        url = (
            f"https://{REGION}-aiplatform.googleapis.com/v1beta1/projects/{PROJECT_ID}"
            f"/locations/{REGION}/modelDevelopmentClusters/{CLUSTER_ID}:callSlurmRestApi"
        )
        
        def call_slurm(method, path, body=None):
            request = {"method": method, "path": path}
            if body is not None:
                request["body"] = body
            response = session.post(url, json=request)
            response.raise_for_status()
            envelope = response.json()
            # body is a JSON string; parse it to read Slurm's fields.
            return envelope["status"], json.loads(envelope["body"])
        
        # Submit a job.
        status, result = call_slurm(
            "HTTP_METHOD_POST",
            "/slurm/v0.0.42/job/submit",
            {
                "job": {
                    "name": "my-run",
                    "partition": f"{PARTITION}",
                    "current_working_directory": f"/home/{USERNAME}",
                    "minimum_nodes": 1,
                    "tasks_per_node": 1,
                    "environment": ["PATH=/bin:/usr/bin"],
                    "time_limit": {"set": True, "number": 120},
                },
                "script": "#!/bin/bash\necho hello\nsleep 5\necho done\n",
            },
        )
        job_id = result["job_id"]
        print("submitted job", job_id)
        
        # Check its status.
        _, pending_result = call_slurm("HTTP_METHOD_GET", f"/slurm/v0.0.42/job/{job_id}")
        print("state:", pending_result["jobs"][0]["job_state"])
        
        # Cancel it.
        call_slurm("HTTP_METHOD_DELETE", f"/slurm/v0.0.42/job/{job_id}")
        print("cancelled job", job_id)
        
        # Confirm the job is cancelled.
        _, cancelled_result  = call_slurm("HTTP_METHOD_GET", f"/slurm/v0.0.42/job/{job_id}")
        print("state", cancelled_result["jobs"][0]["job_state"])

The helper script returns the status from Slurm and the parsed body, so that you can read fields like `job_id` or `job_state` directly. For using the script in automated environments, authenticate as a [service account](https://docs.cloud.google.com/iam/docs/service-account-overview) instead of using an interactive login.

## API Response

The following is a typical Slurm Job API response:

    {
      "status": 200,
      "body": "{ ... raw Slurm JSON ... }"
    }

The `status` field is the HTTP status from Slurm, and the `body` field is a JSON string. You can use `jq` to parse the `body` field, for example: `jq -r '.body | fromjson'` .

We recommend that you check the `body` field, regardless of the Slurm status, because the body field includes any errors or warnings that Slurm reports.

If the `CallSlurmRestApi` request itself is malformatted, you may get an `error` result as follows:

    {
      "error": {
        "code": 400,
        "message": "{ ... some error ... }",
        "status": "INVALID_ARGUMENT"
      }
    }

### Common responses

| What you see             | What it means                                                                                                                                  |
| ------------------------ | ---------------------------------------------------------------------------------------------------------------------------------------------- |
| Status 200 with a job id | Job submitted successfully.                                                                                                                    |
| Status 200, no errors    | Request succeeded.                                                                                                                             |
| Status 200 with warnings | Request succeeded, but Slurm ignored or adjusted something. Read the warning.                                                                  |
| Status 404 for a job     | The job isn't in the live queue; it may have finished. Try the history path.                                                                   |
| Status 400 or 500        | Slurm rejected the request. Reasons for the rejection could include a malformed body or a field of the wrong type. Read the error in the body. |
| PERMISSION\_DENIED error | You don't have access to this cluster.                                                                                                         |
| NOT\_FOUND error         | The cluster name is wrong or the cluster doesn't exist.                                                                                        |
| INVALID\_ARGUMENT error  | The path is not a valid Slurm path, or the request is too large.                                                                               |
| UNAVAILABLE error        | The cluster is temporarily unreachable. Retry after a short wait.                                                                              |

## Limits

The entire request must remain under 1 MB in size. To use large scripts, place the script on the cluster's shared storage and then call it from a short wrapper script.
