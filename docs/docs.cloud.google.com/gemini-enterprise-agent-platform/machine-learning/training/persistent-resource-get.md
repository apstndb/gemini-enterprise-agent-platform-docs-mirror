---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/persistent-resource-get
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/persistent-resource-get
title: Get persistent resource information
description: Get a list of persistent resources and information about a specific resource using the {{dynamic_data.site_values.cloud_name_short}} console, Google Cloud CLI, Agent Platform SDK for Python, or the REST API.
data_source: docs.cloud.google.com
---

This page shows you how to get a list of persistent resources and how to get information about a specific persistent resource by Google Cloud console, Google Cloud CLI, Agent Platform SDK for Python, and the REST API.

## Required roles

To get the permissions that you need to get persistent resource information, ask your administrator to grant you the [Agent Platform Viewer](https://docs.cloud.google.com/iam/docs/roles-permissions/aiplatform#aiplatform.viewer) ( `roles/aiplatform.viewer` ) IAM role on your project. For more information about granting roles, see [Manage access to projects, folders, and organizations](https://docs.cloud.google.com/iam/docs/granting-changing-revoking-access) .

This predefined role contains the permissions required to get persistent resource information. To see the exact permissions that are required, expand the **Required permissions** section:

#### Required permissions

The following permissions are required to get persistent resource information:

  - `aiplatform.persistentResources.get`
  - `aiplatform.persistentResources.list`

You might also be able to get these permissions with [custom roles](https://docs.cloud.google.com/iam/docs/creating-custom-roles) or other [predefined roles](https://docs.cloud.google.com/iam/docs/roles-overview#predefined) .

## Get a list of persistent resources

Select one of the following tabs for instructions on how to get a list of existing persistent resources.

### Console

To view a list of persistent resources in the Google Cloud console, go to the **Persistent resources** page.

### gcloud

Before using any of the command data below, make the following replacements:

  - PROJECT\_ID : The Project ID of the Google Cloud project that you want to get a list persistent resources for.
  - LOCATION : The region where you want to create the persistent resource. For a list of supported regions, see [Feature availability](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/locations#feature-availability) .

Execute the following command:

#### Linux, macOS, or Cloud Shell

> **Note:** Ensure you have initialized the Google Cloud CLI with authentication and a project by running either [gcloud init](https://docs.cloud.google.com/sdk/gcloud/reference/init) ; or [gcloud auth login](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) and [gcloud config set project](https://docs.cloud.google.com/sdk/gcloud/reference/config/set) .

    gcloud ai persistent-resources list \
        --project=PROJECT_ID \
        --region=LOCATION

#### Windows (PowerShell)

> **Note:** Ensure you have initialized the Google Cloud CLI with authentication and a project by running either [gcloud init](https://docs.cloud.google.com/sdk/gcloud/reference/init) ; or [gcloud auth login](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) and [gcloud config set project](https://docs.cloud.google.com/sdk/gcloud/reference/config/set) .

    gcloud ai persistent-resources list `
        --project=PROJECT_ID `
        --region=LOCATION

#### Windows (cmd.exe)

> **Note:** Ensure you have initialized the Google Cloud CLI with authentication and a project by running either [gcloud init](https://docs.cloud.google.com/sdk/gcloud/reference/init) ; or [gcloud auth login](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) and [gcloud config set project](https://docs.cloud.google.com/sdk/gcloud/reference/config/set) .

    gcloud ai persistent-resources list ^
        --project=PROJECT_ID ^
        --region=LOCATION

You should receive a response similar to the following:

#### Response

    Using endpoint [https://us-central1-aiplatform.googleapis.com/]
    ---
    createTime: '2023-09-12T20:45:33.220989Z'
    displayName: test
    name: projects/123456789012/locations/us-central1/persistentResources/test-persistent-resource
    resourcePools:
    - autoscalingSpec:
        maxReplicaCount: '4'
        minReplicaCount: '1'
      diskSpec:
        bootDiskSizeGb: 100
        bootDiskType: pd-standard
      id: n1-highmem-2-nvidia-tesla-t4-1
      machineSpec:
        acceleratorCount: 1
        acceleratorType: NVIDIA_TESLA_T4
        machineType: n1-highmem-2
      replicaCount: '1'
    startTime: '2023-09-12T20:50:36.992739253Z'
    state: RUNNING
    updateTime: '2023-09-12T20:50:42.813723Z'
    ---
    createTime: '2023-09-12T20:37:21.691977Z'
    displayName: my-persistent-resource
    name: projects/123456789012/locations/us-central1/persistentResources/my-persistent-resource
    resourcePools:
    - autoscalingSpec:
        maxReplicaCount: '12'
        minReplicaCount: '4'
      diskSpec:
        bootDiskSizeGb: 200
        bootDiskType: pd-standard
      id: n1-highmem-2-nvidia-tesla-t4-1
      machineSpec:
        acceleratorCount: 1
        acceleratorType: NVIDIA_TESLA_T4
        machineType: n1-highmem-2
      replicaCount: '4'
    - diskSpec:
        bootDiskSizeGb: 100
        bootDiskType: pd-ssd
      id: n1-standard-4
      machineSpec:
        machineType: n1-standard-4
      replicaCount: '4'
    startTime: '2023-09-12T20:42:46.495575169Z'
    state: RUNNING
    updateTime: '2023-09-12T20:42:51.519271Z'

### Python

Before trying this sample, follow the Python setup instructions in the [Agent Platform quickstart using client libraries](https://docs.cloud.google.com/vertex-ai/docs/start/client-libraries) . For more information, see the [Agent Platform Python API reference documentation](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest) .

To authenticate to Agent Platform, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

The status of each persistent resource in the list is represented by a numerical value. For more information, see the [state definitions in the Agent Platform SDK](https://github.com/googleapis/python-aiplatform/blob/c76ac624a4b708dc5980ec64eb52661eb7c8061d/google/cloud/aiplatform/preview/persistent_resource.py#L95-L113) .

    from google.cloud.aiplatform.preview import persistent_resource
    
    # Optional arguments:
    # filter (str): An expression for filtering the results of the request. For
    #   field names both snake_case and camelCase are supported.
    # order_by (str): A comma-separated list of fields to order by, sorted in
    #   ascending order. Use "desc" after a field name for descending. Supported
    #   fields: `display_name`, `create_time`, `update_time`
    
    # List the persistent resource on the project.
    
    resource_list = persistent_resource.PersistentResource.list()
    
    for i in range(len(resource_list)):
        print(resource_list[i].name)
        print(resource_list[i].state)

### REST

Before using any of the request data, make the following replacements:

  - PROJECT\_ID : The Project ID of the Google Cloud project that you want to get a list persistent resources for.
  - LOCATION : The region where you want to create the persistent resource. For a list of supported regions, see [Feature availability](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/locations#feature-availability) .

HTTP method and URL:

    GET https://us-central1-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/persistentResources

To send your request, expand one of these options:

#### curl (Linux, macOS, or Cloud Shell)

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) , or by using [Cloud Shell](https://docs.cloud.google.com/shell/docs) , which automatically logs you into the `gcloud` CLI . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Execute the following command:

    curl -X GET \
         -H "Authorization: Bearer $(gcloud auth print-access-token)" \
         "https://us-central1-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/persistentResources"

#### PowerShell (Windows)

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Execute the following command:

    $cred = gcloud auth print-access-token
    $headers = @{ "Authorization" = "Bearer $cred" }
    
    Invoke-WebRequest `
        -Method GET `
        -Headers $headers `
        -Uri "https://us-central1-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/persistentResources" | Select-Object -Expand Content

You should receive a JSON response similar to the following:

#### Response

    {
      "persistentResources": [
        {
          "name": "projects/123456789012/locations/us-central1/persistentResources/test-persistent-resource",
          "displayName": "test",
          "resourcePools": [
            {
              "id": "n1-highmem-2-nvidia-tesla-t4-1",
              "machineSpec": {
                "machineType": "n1-highmem-2",
                "acceleratorType": "NVIDIA_TESLA_T4",
                "acceleratorCount": 1
              },
              "replicaCount": "1",
              "diskSpec": {
                "bootDiskType": "pd-standard",
                "bootDiskSizeGb": 100
              },
              "autoscalingSpec": {
                "minReplicaCount": "1",
                "maxReplicaCount": "4"
              }
            }
          ],
          "state": "RUNNING",
          "createTime": "2023-09-12T20:45:33.220989Z",
          "startTime": "2023-09-12T20:50:36.992739253Z",
          "updateTime": "2023-09-12T20:50:42.813723Z"
        },
        {
          "name": "projects/123456789012/locations/us-central1/persistentResources/my-persistent-resource",
          "displayName": "my-persistent-resource",
          "resourcePools": [
            {
              "id": "n1-highmem-2-nvidia-tesla-t4-1",
              "machineSpec": {
                "machineType": "n1-highmem-2",
                "acceleratorType": "NVIDIA_TESLA_T4",
                "acceleratorCount": 1
              },
              "replicaCount": "4",
              "diskSpec": {
                "bootDiskType": "pd-standard",
                "bootDiskSizeGb": 200
              },
              "autoscalingSpec": {
                "minReplicaCount": "4",
                "maxReplicaCount": "12"
              }
            },
            {
              "id": "n1-standard-4",
              "machineSpec": {
                "machineType": "n1-standard-4"
              },
              "replicaCount": "4",
              "diskSpec": {
                "bootDiskType": "pd-ssd",
                "bootDiskSizeGb": 100
              }
            }
          ],
          "state": "RUNNING",
          "createTime": "2023-09-12T20:37:21.691977Z",
          "startTime": "2023-09-12T20:42:46.495575169Z",
          "updateTime": "2023-09-12T20:42:51.519271Z"
        },
      ]
    }

## Get information about a persistent resource

Select one of the following tabs for instructions on how to get information about a persistent resource, including its status, hardware configuration, and available replicas.

### Console

To view information about a persistent resource in the Google Cloud console, do the following:

1.  In the Google Cloud console, go to the **Persistent resources** page.

2.  Click the name of the persistent resource that you want to view.

### gcloud

Before using any of the command data below, make the following replacements:

  - PROJECT\_ID : The Project ID of the persistent resource that you want to get information about.
  - LOCATION : The region of the persistent resource that you want to get information about.
  - PERSISTENT\_RESOURCE\_ID : The ID of the persistent resource that you want to get information about.

Execute the following command:

#### Linux, macOS, or Cloud Shell

> **Note:** Ensure you have initialized the Google Cloud CLI with authentication and a project by running either [gcloud init](https://docs.cloud.google.com/sdk/gcloud/reference/init) ; or [gcloud auth login](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) and [gcloud config set project](https://docs.cloud.google.com/sdk/gcloud/reference/config/set) .

    gcloud ai persistent-resources describe PERSISTENT_RESOURCE_ID \
        --project=PROJECT_ID \
        --region=LOCATION

#### Windows (PowerShell)

> **Note:** Ensure you have initialized the Google Cloud CLI with authentication and a project by running either [gcloud init](https://docs.cloud.google.com/sdk/gcloud/reference/init) ; or [gcloud auth login](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) and [gcloud config set project](https://docs.cloud.google.com/sdk/gcloud/reference/config/set) .

    gcloud ai persistent-resources describe PERSISTENT_RESOURCE_ID `
        --project=PROJECT_ID `
        --region=LOCATION

#### Windows (cmd.exe)

> **Note:** Ensure you have initialized the Google Cloud CLI with authentication and a project by running either [gcloud init](https://docs.cloud.google.com/sdk/gcloud/reference/init) ; or [gcloud auth login](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) and [gcloud config set project](https://docs.cloud.google.com/sdk/gcloud/reference/config/set) .

    gcloud ai persistent-resources describe PERSISTENT_RESOURCE_ID ^
        --project=PROJECT_ID ^
        --region=LOCATION

You should receive a response similar to the following:

#### Response

    Using endpoint [https://us-central1-aiplatform.googleapis.com/]
    createTime: '2023-07-06T18:47:42.098296Z'
    displayName: Test-Persistent-Resource
    name: projects/123456789012/locations/us-central1/persistentResources/my-persistent-resource
    resourcePools:
    - diskSpec:
        bootDiskSizeGb: 100
        bootDiskType: pd-ssd
      machineSpec:
        machineType: n1-highmem-4
      replicaCount: '4'
    - diskSpec:
        bootDiskSizeGb: 100
        bootDiskType: pd-ssd
      machineSpec:
        acceleratorCount: 1
        acceleratorType: NVIDIA_TESLA_P4
        machineType: n1-standard-4
      replicaCount: '4'
      usedReplicaCOunt: '2'
    startTime: '2023-07-06T18:51:53.209127117Z'
    state: RUNNING
    updateTime: '2023-07-06T18:52:01.545109Z'

### Python

Before trying this sample, follow the Python setup instructions in the [Agent Platform quickstart using client libraries](https://docs.cloud.google.com/vertex-ai/docs/start/client-libraries) . For more information, see the [Agent Platform Python API reference documentation](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest) .

To authenticate to Agent Platform, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

    from google.cloud.aiplatform.preview import persistent_resource
    
    resource_to_get = persistent_resource.PersistentResource(
        PERSISTENT_RESOURCE_ID
    )
    
    print(resource_to_get.display_name)
    print(resource_to_get.state)
    print(resource_to_get.start_time)

### REST

Before using any of the request data, make the following replacements:

  - PROJECT\_ID : The Project ID of the persistent resource that you want to get information about.
  - LOCATION : The region of the persistent resource that you want to get information about.
  - PERSISTENT\_RESOURCE\_ID : The ID of the persistent resource that you want to get information about.

HTTP method and URL:

    GET https://us-central1-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/persistentResources/PERSISTENT_RESOURCE_ID

To send your request, expand one of these options:

#### curl (Linux, macOS, or Cloud Shell)

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) , or by using [Cloud Shell](https://docs.cloud.google.com/shell/docs) , which automatically logs you into the `gcloud` CLI . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Execute the following command:

    curl -X GET \
         -H "Authorization: Bearer $(gcloud auth print-access-token)" \
         "https://us-central1-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/persistentResources/PERSISTENT_RESOURCE_ID"

#### PowerShell (Windows)

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Execute the following command:

    $cred = gcloud auth print-access-token
    $headers = @{ "Authorization" = "Bearer $cred" }
    
    Invoke-WebRequest `
        -Method GET `
        -Headers $headers `
        -Uri "https://us-central1-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/persistentResources/PERSISTENT_RESOURCE_ID" | Select-Object -Expand Content

You should receive a JSON response similar to the following:

    {
      "name": "projects/123456789012/locations/us-central1/persistentResources/test-persistent-resource",
      "displayName": "test",
      "resourcePools": [
        {
          "id": "n1-highmem-2-nvidia-tesla-t4-1",
          "machineSpec": {
            "machineType": "n1-highmem-2",
            "acceleratorType": "NVIDIA_TESLA_T4",
            "acceleratorCount": 1
          },
          "replicaCount": "1",
          "diskSpec": {
            "bootDiskType": "pd-standard",
            "bootDiskSizeGb": 100
          },
          "autoscalingSpec": {
            "minReplicaCount": "1",
            "maxReplicaCount": "4"
          }
        }
      ],
      "state": "RUNNING",
      "createTime": "2023-09-12T20:45:33.220989Z",
      "startTime": "2023-09-12T20:50:36.992739253Z",
      "updateTime": "2023-09-12T20:50:42.813723Z"
    }

## What's next

  - [Learn about persistent resource](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/persistent-resource-overview) .
  - [Run training jobs on a persistent resource](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/persistent-resource-train) .
  - [Get information about a persistent resource](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/persistent-resource-get) .
  - [Reboot a persistent resource](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/persistent-resource-reboot) .
  - [Delete a persistent resource](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/persistent-resource-delete) .
