---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/long-running-operations
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/long-running-operations
title: Long-running operations
description: Learn about long-running operations and how to use helper methods along with operation names to get the status of or cancel a long-running operation.
data_source: docs.cloud.google.com
---

For some API calls, Gemini Enterprise Agent Platform returns operation names. These API calls start operations that require time to complete and are known as *long-running operations* . For example, creating a dataset, deleting an endpoint, or exporting a model are all long-running operations. You can use helper methods along with operation names to get the status of or cancel a long-running operation, as described in the following sections.

> **Note:** If you are using the Google Cloud console, the console shows the status of the operation and automatically updates the status when an operation is complete.

## Getting the status of an operation

To get the operation status, use the operation name that was in the response when you requested a long-running operation. For example, when you create a dataset, Agent Platform returns an operation name such as:  
` projects/ PROJECT_NUMBER /locations/ LOCATION /datasets/ DATASET_ID /operations/ OPERATION_ID  `

You can poll the operation at regular intervals so that you know when an operation completes.

### REST

Before using any of the request data, make the following replacements:

  - OPERATION\_NAME : The operation name that is returned when you start a long-running operation, such as ` projects/ PROJECT_NUMBER /locations/ LOCATION /datasets/ DATASET_ID /operations/ OPERATION_ID  `

HTTP method and URL:

    GET https://LOCATION-aiplatform.googleapis.com/v1/OPERATION_NAME

To send your request, choose one of these options:

#### curl

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) , or by using [Cloud Shell](https://docs.cloud.google.com/shell/docs) , which automatically logs you into the `gcloud` CLI . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Execute the following command:

    curl -X GET \
         -H "Authorization: Bearer $(gcloud auth print-access-token)" \
         "https://LOCATION-aiplatform.googleapis.com/v1/OPERATION_NAME"

#### PowerShell

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Execute the following command:

    $cred = gcloud auth print-access-token
    $headers = @{ "Authorization" = "Bearer $cred" }
    
    Invoke-WebRequest `
        -Method GET `
        -Headers $headers `
        -Uri "https://LOCATION-aiplatform.googleapis.com/v1/OPERATION_NAME" | Select-Object -Expand Content

In the output, the `metadata` object contains information that is specific to the request type. The `done` field indicates whether the operation is complete. If the operation is complete, the `response` object contains results from the operation.

    {
      "name": "projects/123456789012/locations/us-central1/datasets/1234567890123456789/operations/1223344556677889900",
      "metadata": {
        "@type": "type.googleapis.com/google.cloud.aiplatform.v1.CreateDatasetOperationMetadata",
        "genericMetadata": {
          "createTime": "2020-10-12T16:00:44.686500Z",
          "updateTime": "2020-10-12T16:01:06.115081Z"
        }
      },
      "done": true,
      "response": {
        "@type": "type.googleapis.com/google.cloud.aiplatform.v1.Dataset",
        "name": "projects/123456789012/locations/us-central1/datasets/1234567890123456789",
        "displayName": "image_dataset",
        "metadataSchemaUri": "gs://google-cloud-aiplatform/schema/dataset/metadata/image_1.0.0.yaml",
        "labels": {
          "aiplatform.googleapis.com/dataset_metadata_schema": "IMAGE"
        },
        "metadata": {
          "dataItemSchemaUri": "gs://google-cloud-aiplatform/schema/dataset/dataitem/image_1.0.0.yaml"
        }
      }
    }

## Canceling an Operation

You can cancel a long-running operation so that you can stop it before the operation completes. When you successfully cancel an operation, the operation isn't deleted; instead, the operation stops with an error code of `1` and with a `CANCELLED` message. Note that the cancellation is not guaranteed to succeed.

### REST

Before using any of the request data, make the following replacements:

  - OPERATION\_NAME : The operation name that is returned when you start a long-running operation, such as ` projects/ PROJECT_NUMBER /locations/ LOCATION /datasets/ DATASET_ID /operations/ OPERATION_ID  `

HTTP method and URL:

    POST https://LOCATION-aiplatform.googleapis.com/v1/OPERATION_NAME:cancel

To send your request, choose one of these options:

#### curl

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) , or by using [Cloud Shell](https://docs.cloud.google.com/shell/docs) , which automatically logs you into the `gcloud` CLI . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Execute the following command:

    curl -X POST \
         -H "Authorization: Bearer $(gcloud auth print-access-token)" \
         -H "Content-Type: application/json; charset=utf-8" \
         -d "" \
         "https://LOCATION-aiplatform.googleapis.com/v1/OPERATION_NAME:cancel"

#### PowerShell

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Execute the following command:

    $cred = gcloud auth print-access-token
    $headers = @{ "Authorization" = "Bearer $cred" }
    
    Invoke-WebRequest `
        -Method POST `
        -Headers $headers `
        -Uri "https://LOCATION-aiplatform.googleapis.com/v1/OPERATION_NAME:cancel" | Select-Object -Expand Content

You should receive a successful status code (2xx) and an empty response.
