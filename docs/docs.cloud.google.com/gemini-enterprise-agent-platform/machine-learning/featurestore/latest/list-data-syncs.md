---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/featurestore/latest/list-data-syncs
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/featurestore/latest/list-data-syncs
title: List sync operations
description: Learn how to view a list of sync operations executed for a feature view in Vertex AI Feature Store.
data_source: docs.cloud.google.com
---

You can view the list of data sync operations executed for a specific feature view. This can be useful if you want to verify whether the data sync is being successfully synced from the BigQuery data source, or whether data sync is in progress for the feature view.

## Before you begin

Authenticate to Gemini Enterprise Agent Platform, unless you've done so already.

To use the REST API samples on this page in a local development environment, you use the credentials you provide to the gcloud CLI.

For more information, see [Authenticate for using REST](https://docs.cloud.google.com/docs/authentication/rest) in the Google Cloud authentication documentation.

## List sync operations in a feature view

Use the following sample to view a list of all sync operations executed for a feature view.

### REST

To view the list of data sync operations in a [`FeatureView`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.featureOnlineStores.featureViews#resource:-featureView) instance, send a `GET` request by using the [featureViewSyncs.list](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.featureOnlineStores.featureViews.featureViewSyncs/list) method.

Before using any of the request data, make the following replacements:

  - LOCATION\_ID : Region where the online store is located, such as `us-central1` .
  - PROJECT\_ID : Your project ID.
  - FEATUREONLINESTORE\_NAME : The name of the online store containing the feature view.
  - FEATUREVIEW\_NAME : The name of the feature view for which you want to view the list of data sync operations.

HTTP method and URL:

    GET https://LOCATION_ID-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION_ID/featureOnlineStores/FEATUREONLINESTORE_NAME/featureViews/FEATUREVIEW_NAME/featureViewSyncs

To send your request, choose one of these options:

#### curl

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) , or by using [Cloud Shell](https://docs.cloud.google.com/shell/docs) , which automatically logs you into the `gcloud` CLI . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Execute the following command:

    curl -X GET \
         -H "Authorization: Bearer $(gcloud auth print-access-token)" \
         "https://LOCATION_ID-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION_ID/featureOnlineStores/FEATUREONLINESTORE_NAME/featureViews/FEATUREVIEW_NAME/featureViewSyncs"

#### PowerShell

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Execute the following command:

    $cred = gcloud auth print-access-token
    $headers = @{ "Authorization" = "Bearer $cred" }
    
    Invoke-WebRequest `
        -Method GET `
        -Headers $headers `
        -Uri "https://LOCATION_ID-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION_ID/featureOnlineStores/FEATUREONLINESTORE_NAME/featureViews/FEATUREVIEW_NAME/featureViewSyncs" | Select-Object -Expand Content

You should receive a JSON response similar to the following:

    {
      "featureViewSyncs": [
        {
          "name": "PROJECT_ID/locations/LOCATION_ID/featureOnlineStores/FEATUREONLINESTORE_NAME/featureViews/FEATUREVIEW_NAME/featureViewSyncs/OPERATION_ID_1",
          "createTime": "2023-09-11T15:33:24.906716Z",
          "dataTransfer": {
            "endTime": "2023-09-11T15:33:43.615598Z"
          },
          "finalStatus": {
            "code": 13
          },
          "runTime": {
            "endTime": "2023-09-11T15:33:43.615598Z"
          }
        },
        {
          "name": "PROJECT_ID/locations/LOCATION_ID/featureOnlineStores/FEATUREONLINESTORE_NAME/featureViews/FEATUREVIEW_NAME/featureViewSyncs/OPERATION_ID_2",
          "createTime": "2023-09-06T23:48:00.670844Z",
          "dataTransfer": {
            "endTime": "2023-09-06T23:48:19.086848Z"
          },
          "finalStatus": {
            "code": 13
          },
          "runTime": {
            "endTime": "2023-09-06T23:48:19.086848Z"
          }
        }
      ]
    }

## What's next

  - Learn how to [manually start a data sync](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/featurestore/latest/sync-data) .

  - Learn how to [update a feature view](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/featurestore/latest/update-featureview) .
