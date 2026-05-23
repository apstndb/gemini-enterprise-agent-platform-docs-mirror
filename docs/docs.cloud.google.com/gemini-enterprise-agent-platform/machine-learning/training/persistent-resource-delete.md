---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/persistent-resource-delete
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/persistent-resource-delete
title: Delete a persistent resource
description: Delete a persistent resource using the {{dynamic_data.site_values.cloud_name_short}} console, Google Cloud CLI, Agent Platform SDK for Python, or the REST API.
data_source: docs.cloud.google.com
---

Persistent resources are available until they are deleted. Once deleted, there is no guarantee that you can create the persistent resource of the same resource type again if there's a stockout. This page shows you how to delete a persistent resource by using the Google Cloud console, Google Cloud CLI, Agent Platform SDK for Python, and the REST API.

## Required roles

To get the permission that you need to delete a persistent resource, ask your administrator to grant you the [Agent Platform Administrator](https://docs.cloud.google.com/iam/docs/roles-permissions/aiplatform#aiplatform.admin) ( `roles/aiplatform.admin` ) IAM role on your project. For more information about granting roles, see [Manage access to projects, folders, and organizations](https://docs.cloud.google.com/iam/docs/granting-changing-revoking-access) .

This predefined role contains the `aiplatform.persistentResources.delete` permission, which is required to delete a persistent resource.

You might also be able to get this permission with [custom roles](https://docs.cloud.google.com/iam/docs/creating-custom-roles) or other [predefined roles](https://docs.cloud.google.com/iam/docs/roles-overview#predefined) .

## Delete a persistent resource

For instructions on how to delete a persistent resource when you no longer needed it, select one of the following tabs. Note that if there are custom jobs running on the persistent resource when you delete it, those custom jobs are automatically cancelled before the persistent resource is deleted.

### Console

To delete a persistent resource in the Google Cloud console, do the following:

1.  In the Google Cloud console, go to the **Persistent resources** page.

2.  Click the name of the persistent resource that you want to delete.

3.  Click delete **Delete** .

4.  Click **Confirm** .

### gcloud

Before using any of the command data below, make the following replacements:

  - PROJECT\_ID : The Project ID of the persistent resource that you want to delete.
  - LOCATION : The region of the persistent resource that you want to delete.
  - PERSISTENT\_RESOURCE\_ID : The ID of the persistent resource that you want to delete.

Execute the following command:

#### Linux, macOS, or Cloud Shell

> **Note:** Ensure you have initialized the Google Cloud CLI with authentication and a project by running either [gcloud init](https://docs.cloud.google.com/sdk/gcloud/reference/init) ; or [gcloud auth login](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) and [gcloud config set project](https://docs.cloud.google.com/sdk/gcloud/reference/config/set) .

    gcloud ai persistent-resources delete PERSISTENT_RESOURCE_ID \
        --project=PROJECT_ID \
        --region=LOCATION

#### Windows (PowerShell)

> **Note:** Ensure you have initialized the Google Cloud CLI with authentication and a project by running either [gcloud init](https://docs.cloud.google.com/sdk/gcloud/reference/init) ; or [gcloud auth login](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) and [gcloud config set project](https://docs.cloud.google.com/sdk/gcloud/reference/config/set) .

    gcloud ai persistent-resources delete PERSISTENT_RESOURCE_ID `
        --project=PROJECT_ID `
        --region=LOCATION

#### Windows (cmd.exe)

> **Note:** Ensure you have initialized the Google Cloud CLI with authentication and a project by running either [gcloud init](https://docs.cloud.google.com/sdk/gcloud/reference/init) ; or [gcloud auth login](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) and [gcloud config set project](https://docs.cloud.google.com/sdk/gcloud/reference/config/set) .

    gcloud ai persistent-resources delete PERSISTENT_RESOURCE_ID ^
        --project=PROJECT_ID ^
        --region=LOCATION

You should receive a response similar to the following:

    Using endpoint [https://us-central1-aiplatform.googleapis.com/]
    Request to delete the PersistentResource [projects/sample-project/locations/us-central1/persistentResources/test-persistent-resource] has been sent.
    
    You may view the status of your persistent resource with the command
    
      $ gcloud ai persistent-resources describe projects/sample-project/locations/us-central1/persistentResources/test-persistent-resource

### Python

Before trying this sample, follow the Python setup instructions in the [Agent Platform quickstart using client libraries](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/start/client-libraries) .

To authenticate to Agent Platform, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

    from google.cloud.aiplatform.preview import persistent_resource
    
    resource_to_delete = persistent_resource.PersistentResource(
        PERSISTENT_RESOURCE_ID
    )
    
    # Delete the persistent resource.
    resource_to_delete.delete(sync=True)

### REST

Before using any of the request data, make the following replacements:

  - PROJECT\_ID : The Project ID of the persistent resource that you want to delete.
  - LOCATION : The region of the persistent resource that you want to delete.
  - PERSISTENT\_RESOURCE\_ID : The ID of the persistent resource that you want to delete.

HTTP method and URL:

    DELETE https://us-central1-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/persistentResources/PERSISTENT_RESOURCE_ID

To send your request, expand one of these options:

#### curl (Linux, macOS, or Cloud Shell)

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) , or by using [Cloud Shell](https://docs.cloud.google.com/shell/docs) , which automatically logs you into the `gcloud` CLI . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Execute the following command:

    curl -X DELETE \
         -H "Authorization: Bearer $(gcloud auth print-access-token)" \
         "https://us-central1-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/persistentResources/PERSISTENT_RESOURCE_ID"

#### PowerShell (Windows)

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Execute the following command:

    $cred = gcloud auth print-access-token
    $headers = @{ "Authorization" = "Bearer $cred" }
    
    Invoke-WebRequest `
        -Method DELETE `
        -Headers $headers `
        -Uri "https://us-central1-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/persistentResources/PERSISTENT_RESOURCE_ID" | Select-Object -Expand Content

You should receive a JSON response similar to the following:

    {
      "name": "projects/123456789012/locations/us-central1/operations/1234567890123456789",
      "metadata": {
        "@type": "type.googleapis.com/google.cloud.aiplatform.v1.DeleteOperationMetadata",
        "genericMetadata": {
          "createTime": "2023-07-28T17:22:08.316883Z",
          "updateTime": "2023-07-28T17:22:08.316883Z"
        }
      },
      "done": true,
      "response": {
        "@type": "type.googleapis.com/google.protobuf.Empty"
      }
    }

## What's next

  - [Learn about persistent resource](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/persistent-resource-overview) .
  - [Run training jobs on a persistent resource](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/persistent-resource-train) .
  - [Create and use a persistent resource](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/persistent-resource-create) .
  - [Get information about a persistent resource](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/persistent-resource-get) .
  - [Reboot a persistent resource](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/persistent-resource-reboot) .
