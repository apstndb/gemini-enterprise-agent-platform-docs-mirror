---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/persistent-resource-reboot
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/persistent-resource-reboot
title: Reboot a persistent resource
description: Reboot a persistent resource using the {{dynamic_data.site_values.cloud_name_short}} console, Google Cloud CLI, Agent Platform SDK for Python, or the REST API.
data_source: docs.cloud.google.com
---

You can reboot any persistent resource that's in the `RUNNING` or `ERROR` state. Rebooting a persistent resource lets you recover from errors that the persistent resource can't recover from on its own. You can also reboot a persistent resource to manually obtain more up-to-date clusters. This page shows you how to reboot a persistent resource by using the Google Cloud console and the REST API.

## Required roles

To get the permission that you need to reboot a persistent resource, ask your administrator to grant you the [Agent Platform Administrator](https://docs.cloud.google.com/iam/docs/roles-permissions/aiplatform#aiplatform.admin) ( `roles/aiplatform.admin` ) IAM role on your project. For more information about granting roles, see [Manage access to projects, folders, and organizations](https://docs.cloud.google.com/iam/docs/granting-changing-revoking-access) .

This predefined role contains the `aiplatform.persistentResources.update` permission, which is required to reboot a persistent resource.

You might also be able to get this permission with [custom roles](https://docs.cloud.google.com/iam/docs/creating-custom-roles) or other [predefined roles](https://docs.cloud.google.com/iam/docs/roles-overview#predefined) .

## Reboot a persistent resource

Select one of the following tabs for instructions on how to reboot a persistent resource. Make sure there's no training jobs running on the persistent resource.

### Console

To reboot a persistent resource in the Google Cloud console, do the following:

1.  In the Google Cloud console, go to the **Persistent resources** page.

2.  Next to the name of the persistent resource that you want to reboot, click the vertical ellipses ( more\_vert ).

3.  Click **Reboot** .

4.  Click **Confirm** .

### gcloud

Before using any of the command data below, make the following replacements:

  - PROJECT\_ID : The Project ID of the persistent resource that you want to reboot.
  - LOCATION : The region of the persistent resource that you want to reboot.
  - PERSISTENT\_RESOURCE\_ID : The ID of the persistent resource that you want to reboot.

Execute the following command:

#### Linux, macOS, or Cloud Shell

> **Note:** Ensure you have initialized the Google Cloud CLI with authentication and a project by running either [gcloud init](https://docs.cloud.google.com/sdk/gcloud/reference/init) ; or [gcloud auth login](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) and [gcloud config set project](https://docs.cloud.google.com/sdk/gcloud/reference/config/set) .

    gcloud ai persistent-resources reboot PERSISTENT_RESOURCE_ID \
        --project=PROJECT_ID \
        --region=LOCATION

#### Windows (PowerShell)

> **Note:** Ensure you have initialized the Google Cloud CLI with authentication and a project by running either [gcloud init](https://docs.cloud.google.com/sdk/gcloud/reference/init) ; or [gcloud auth login](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) and [gcloud config set project](https://docs.cloud.google.com/sdk/gcloud/reference/config/set) .

    gcloud ai persistent-resources reboot PERSISTENT_RESOURCE_ID `
        --project=PROJECT_ID `
        --region=LOCATION

#### Windows (cmd.exe)

> **Note:** Ensure you have initialized the Google Cloud CLI with authentication and a project by running either [gcloud init](https://docs.cloud.google.com/sdk/gcloud/reference/init) ; or [gcloud auth login](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) and [gcloud config set project](https://docs.cloud.google.com/sdk/gcloud/reference/config/set) .

    gcloud ai persistent-resources reboot PERSISTENT_RESOURCE_ID ^
        --project=PROJECT_ID ^
        --region=LOCATION

You should receive a response similar to the following:

    Using endpoint [https://us-central1-aiplatform.googleapis.com/]
    Request to reboot the PersistentResource [projects/sample-project/locations/us-central1/persistentResources/test-persistent-resource] has been sent.
    
    You may view the status of your persistent resource with the command
    
      $ gcloud ai persistent-resources describe projects/sample-project/locations/us-central1/persistentResources/test-persistent-resource

### REST

Before using any of the request data, make the following replacements:

  - PROJECT\_ID : The Project ID of the persistent resource that you want to reboot.
  - LOCATION : The region of the persistent resource that you want to reboot.
  - PERSISTENT\_RESOURCE\_ID : The ID of the persistent resource that you want to reboot.

HTTP method and URL:

    POST https://us-central1-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/persistentResources/PERSISTENT_RESOURCE_ID:reboot

To send your request, expand one of these options:

#### curl (Linux, macOS, or Cloud Shell)

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) , or by using [Cloud Shell](https://docs.cloud.google.com/shell/docs) , which automatically logs you into the `gcloud` CLI . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Execute the following command:

    curl -X POST \
         -H "Authorization: Bearer $(gcloud auth print-access-token)" \
         -H "Content-Type: application/json; charset=utf-8" \
         -d "" \
         "https://us-central1-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/persistentResources/PERSISTENT_RESOURCE_ID:reboot"

#### PowerShell (Windows)

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Execute the following command:

    $cred = gcloud auth print-access-token
    $headers = @{ "Authorization" = "Bearer $cred" }
    
    Invoke-WebRequest `
        -Method POST `
        -Headers $headers `
        -Uri "https://us-central1-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/persistentResources/PERSISTENT_RESOURCE_ID:reboot" | Select-Object -Expand Content

You should receive a JSON response similar to the following:

    response: 
      {
        "name": "projects/123456789012/locations/us-central1/persistentResources/test-persistent-resource/operations/1234567890123456789",
        "metadata": {
          "@type": "type.googleapis.com/google.cloud.aiplatform.v1.RebootPersistentResourceOperationMetadata",
          "genericMetadata": {
            "createTime": "2024-03-18T17:31:54.955004Z",
            "updateTime": "2024-03-18T17:31:55.204817Z",
            "state": "RUNNING",
            "worksOn": [
              "projects/123456789012/locations/us-central1/persistentResources/test-persistent-resource"
            ]
          },
          "progressMessage": "Waiting for persistent resource shut down."
        }
      }

Rebooting a persistent resource is a [long running operation](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/long-running-operations) , during which the persistent resource can't be deleted. The operation contains a `progressMessage` field that populates with an error status if one occurs. After the operation indicates `"done: true"` , [check the status](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/persistent-resource-get#get_information_about_a_persistent_resource) of the persistent resource. If the persistent resource is in the `RUNNING` state, the reboot is successful and it's ready to run training jobs.

## Limitations

The following are limitations for rebooting a persistent resource:

  - In some cases, it's possible to lose capacity of scarce resources when rebooting a persistent resource. Full resource retention is not guaranteed.
  - Reboot is not available on Ray on Agent Platform.
  - Persistent resources containing autoscaled worker pools reboot with the minimum replica count.

## What's next

  - [Learn about persistent resource](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/persistent-resource-overview) .
  - [Create and use a persistent resource](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/persistent-resource-create) .
  - [Run training jobs on a persistent resource](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/persistent-resource-train) .
  - [Get information about a persistent resource](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/persistent-resource-get) .
  - [Delete a persistent resource](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/persistent-resource-delete) .
