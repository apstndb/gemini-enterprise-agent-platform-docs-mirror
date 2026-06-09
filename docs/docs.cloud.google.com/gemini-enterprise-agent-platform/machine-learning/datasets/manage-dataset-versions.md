---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/datasets/manage-dataset-versions
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/datasets/manage-dataset-versions
title: Manage image dataset versions (API-only)
description: Manage dataset versions.
data_source: docs.cloud.google.com
---

> **Preview**
> 
> This feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](https://docs.cloud.google.com/terms/service-terms#1) . Pre-GA features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

> **Note:** This feature is for image datasets only and is accessible exclusively through the Gemini Enterprise Agent Platform REST API. It's intended for advanced users who require programmatic versioning for lineage and reproducibility.

Gemini Enterprise Agent Platform lets you create versions for a dataset. This capability can be useful for reproducibility, traceability, and dataset lineage management.

You can create versions for image datasets. When you create a dataset version, Agent Platform creates a [BigQuery](https://docs.cloud.google.com/bigquery/docs/introduction) dataset if none exists. The BigQuery dataset stores all versions for the associated Gemini Enterprise Agent Platform dataset.

When you restore a version, you override the associated dataset. The dataset is temporarily unavailable for other requests until the restore operation ends.

## Create a dataset version

You can use the Agent Platform API to create a dataset version. Follow the steps in the corresponding tab:

### REST

### Get the dataset's ID

To create a version, you must know the numerical ID of the dataset. If you know the display name of the dataset but not the ID, expand the following section to learn how to get the ID using the API:

#### Get a `Dataset` 's ID from its display name

Before using any of the request data, make the following replacements:

  - LOCATION : The location where the `Dataset` is stored. For example, `us-central1` .

  - PROJECT\_ID : Your [project ID](https://docs.cloud.google.com/resource-manager/docs/creating-managing-projects#identifiers) .

  - DATASET\_DISPLAY\_NAME : The display name of the `Dataset` .

HTTP method and URL:

    GET https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/datasets?filter=displayName=DATASET_DISPLAY_NAME

To send your request, choose one of these options:

#### curl

> **Note:** Ensure you have set the [`GOOGLE_APPLICATION_CREDENTIALS`](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment#local-key) environment variable to the path for your service account private key file.

Execute the following command:

    curl -X GET \
         -H "Authorization: Bearer $(gcloud auth application-default print-access-token)" \
         "https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/datasets?filter=displayName=DATASET_DISPLAY_NAME"

#### PowerShell

> **Note:** Ensure you have set the [`GOOGLE_APPLICATION_CREDENTIALS`](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment#local-key) environment variable to the path for your service account private key file.

Execute the following command:

    $cred = gcloud auth application-default print-access-token
    $headers = @{ "Authorization" = "Bearer $cred" }
    
    Invoke-WebRequest `
        -Method GET `
        -Headers $headers `
        -Uri "https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/datasets?filter=displayName=DATASET_DISPLAY_NAME" | Select-Object -Expand Content

The following example response has been truncated with `...` to emphasize where you can find your `Dataset` 's ID: it is the number that takes the place of DATASET\_ID .

    {
      "datasets": [
        {
          "name": "projects/PROJECT_NUMBER/locations/LOCATION/datasets/DATASET_ID",
          "displayName": "DATASET_DISPLAY_NAME",
          ...
        }
      ]
    }

Alternatively, you can get the dataset's ID from the Google Cloud console: Go to the Agent Platform **Datasets** page and find the number in the **ID** column.

Before using any of the request data, make the following replacements:

  - LOCATION : The region where the dataset version is stored. For example, `us-central` .

  - PROJECT\_ID : Your [project ID](https://docs.cloud.google.com/resource-manager/docs/creating-managing-projects#identifiers) .

  - DATASET\_ID : The numerical ID of the dataset.

HTTP method and URL:

    POST https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/datasets/DATASET_ID/datasetVersions

To send your request, choose one of these options:

#### curl

> **Note:** Ensure you have set the [`GOOGLE_APPLICATION_CREDENTIALS`](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment#local-key) environment variable to the path for your service account private key file.

Execute the following command:

    curl -X POST \
         -H "Authorization: Bearer $(gcloud auth application-default print-access-token)" \
         -H "Content-Type: application/json; charset=utf-8" \
         -d "" \
         "https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/datasets/DATASET_ID/datasetVersions"

#### PowerShell

> **Note:** Ensure you have set the [`GOOGLE_APPLICATION_CREDENTIALS`](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment#local-key) environment variable to the path for your service account private key file.

Execute the following command:

    $cred = gcloud auth application-default print-access-token
    $headers = @{ "Authorization" = "Bearer $cred" }
    
    Invoke-WebRequest `
        -Method POST `
        -Headers $headers `
        -Uri "https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/datasets/DATASET_ID/datasetVersions" | Select-Object -Expand Content

You should receive a JSON response similar to the following:

    {
      "name": "projects/PROJECT_NUMBER/locations/LOCATION/datasets/DATASET_ID/operations/OPERATION_ID",
      "metadata": {
        "@type": "type.googleapis.com/google.cloud.aiplatform.v1.CreateDatasetVersionOperationMetadata",
        "genericMetadata": {
          "createTime": "2021-02-17T00:54:58.827429Z",
          "updateTime": "2021-02-17T00:54:58.827429Z"
        },
      }
    }

Some requests start long-running operations that require time to complete. These requests return an operation name, which you can use to view the operation's status or cancel the operation. Agent Platform provides helper methods to make calls against long-running operations. For more information, see [Working with long-running operations](https://docs.cloud.google.com/vertex-ai/docs/general/long-running-operations) .

## Restore a dataset version

You can use the Agent Platform API to restore a dataset version. Follow the steps in the corresponding tab:

### REST

### Get the dataset version's ID

To restore a version, you must know the version's numerical ID. You can list all the dataset versions using the API:

#### List a `Dataset` 's `DatasetVersion` s

Before using any of the request data, make the following replacements:

  - LOCATION : The region where the dataset version is stored. For example, `us-central` .

  - PROJECT\_ID : Your [project ID](https://docs.cloud.google.com/resource-manager/docs/creating-managing-projects#identifiers) .

  - DATASET\_ID : The numerical ID of the dataset.

HTTP method and URL:

    GET https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/datasets/DATASET_ID/datasetVersions

To send your request, choose one of these options:

#### curl

> **Note:** Ensure you have set the [`GOOGLE_APPLICATION_CREDENTIALS`](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment#local-key) environment variable to the path for your service account private key file.

Execute the following command:

    curl -X GET \
         -H "Authorization: Bearer $(gcloud auth application-default print-access-token)" \
         "https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/datasets/DATASET_ID/datasetVersions"

#### PowerShell

> **Note:** Ensure you have set the [`GOOGLE_APPLICATION_CREDENTIALS`](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment#local-key) environment variable to the path for your service account private key file.

Execute the following command:

    $cred = gcloud auth application-default print-access-token
    $headers = @{ "Authorization" = "Bearer $cred" }
    
    Invoke-WebRequest `
        -Method GET `
        -Headers $headers `
        -Uri "https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/datasets/DATASET_ID/datasetVersions" | Select-Object -Expand Content

The following example response has been truncated with `...` to emphasize where you can find your dataset version's ID: it is the number that takes the place of DATASET\_VERSION\_ID .

    {
      "datasetVersions": [
        {
          "name": "projects/PROJECT_NUMBER/locations/LOCATION/datasets/DATASET_ID/datasetVersions/DATASET_VERSION_ID",
          ...
        }
      ]
    }

Before using any of the request data, make the following replacements:

  - LOCATION : The region where the dataset version is stored. For example, `us-central` .

  - PROJECT\_ID : Your [project ID](https://docs.cloud.google.com/resource-manager/docs/creating-managing-projects#identifiers) .

  - DATASET\_ID : The numerical ID of the dataset.

  - DATASET\_VERSION\_ID : The numerical ID of the dataset version.

HTTP method and URL:

    GET https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/datasets/DATASET_ID/datasetVersions/DATASET_VERSION_ID:restore

To send your request, choose one of these options:

#### curl

> **Note:** Ensure you have set the [`GOOGLE_APPLICATION_CREDENTIALS`](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment#local-key) environment variable to the path for your service account private key file.

Execute the following command:

    curl -X GET \
         -H "Authorization: Bearer $(gcloud auth application-default print-access-token)" \
         "https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/datasets/DATASET_ID/datasetVersions/DATASET_VERSION_ID:restore"

#### PowerShell

> **Note:** Ensure you have set the [`GOOGLE_APPLICATION_CREDENTIALS`](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment#local-key) environment variable to the path for your service account private key file.

Execute the following command:

    $cred = gcloud auth application-default print-access-token
    $headers = @{ "Authorization" = "Bearer $cred" }
    
    Invoke-WebRequest `
        -Method GET `
        -Headers $headers `
        -Uri "https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/datasets/DATASET_ID/datasetVersions/DATASET_VERSION_ID:restore" | Select-Object -Expand Content

You should receive a JSON response similar to the following:

    {
      "name": "projects/PROJECT_NUMBER/locations/LOCATION/datasets/DATASET_ID/operations/OPERATION_ID",
      "metadata": {
        "@type": "type.googleapis.com/google.cloud.aiplatform.v1.RestoreDatasetVersionOperationMetadata",
        "genericMetadata": {
          "createTime": "2021-02-17T00:54:58.827429Z",
          "updateTime": "2021-02-17T00:54:58.827429Z"
        },
      }
    }

Some requests start long-running operations that require time to complete. These requests return an operation name, which you can use to view the operation's status or cancel the operation. Agent Platform provides helper methods to make calls against long-running operations. For more information, see [Working with long-running operations](https://docs.cloud.google.com/vertex-ai/docs/general/long-running-operations) .

## What's next

Read more about [working with datasets in Agent Platform](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/using-managed-datasets) .
