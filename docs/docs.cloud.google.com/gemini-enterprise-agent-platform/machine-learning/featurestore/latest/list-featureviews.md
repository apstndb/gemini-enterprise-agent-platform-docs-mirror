---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/featurestore/latest/list-featureviews
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/featurestore/latest/list-featureviews
title: List feature views
description: Learn how to retrieve a list of feature views within an online store instance in Vertex AI Feature Store.
data_source: docs.cloud.google.com
---

You can retrieve a list of all the feature view instances created within an online store in your Google Cloud project. For each feature view, you can also view the feature data source, which can be either of the following:

  - One or more feature groups and their constituent features. Each feature group is associated with a feature data source, such as a BigQuery table or view. Each feature designates a column in the BigQuery data source.

  - A BigQuery table or view directly associated with the feature view.

If a feature view is configured to use a dedicated service account, then the details for that feature view also include the associated service account email address. For more information about creating feature views with dedicated service account configurations, see [Configure the service account for a feature view](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/featurestore/latest/create-featureview#serviceaccount) .

## Before you begin

Authenticate to Gemini Enterprise Agent Platform, unless you've done so already.

Select the tab for how you plan to use the samples on this page:

### Console

When you use the Google Cloud console to access Google Cloud services and APIs, you don't need to set up authentication.

### REST

To use the REST API samples on this page in a local development environment, you use the credentials you provide to the gcloud CLI.

For more information, see [Authenticate for using REST](https://docs.cloud.google.com/docs/authentication/rest) in the Google Cloud authentication documentation.

## List feature views in an online store

Use the following samples to retrieve a list of feature views created for an online store in your project for a specific location.

### Console

Use the following instructions to view the list of feature views in an online store using the Google Cloud console.

1.  In the Agent Platform section of the Google Cloud console, go to the **Feature Store** page.

2.  Click **Online store** .

3.  Click the name of the online store to view its details on the **Online store details** page.

4.  In the **Feature views** section, you can view the list of all the online stores for the selected location.

### REST

To retrieve a list of all the [`FeatureView`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.featureOnlineStores.featureViews#resource:-featureView) instances created within a specific online store in your project, send a `GET` request by using the [featureViews.list](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.featureOnlineStores.featureViews/list) method.

Before using any of the request data, make the following replacements:

  - LOCATION\_ID : Region where the online store is located, such as `us-central1` .
  - PROJECT\_ID : Your project ID.
  - FEATUREONLINESTORE\_NAME : The name of the online store for which you want to view the list of feature views.

HTTP method and URL:

    GET https://LOCATION_ID-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION_ID/featureOnlineStores/FEATUREONLINESTORE_NAME/featureViews

To send your request, choose one of these options:

#### curl

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) , or by using [Cloud Shell](https://docs.cloud.google.com/shell/docs) , which automatically logs you into the `gcloud` CLI . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Execute the following command:

    curl -X GET \
         -H "Authorization: Bearer $(gcloud auth print-access-token)" \
         "https://LOCATION_ID-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION_ID/featureOnlineStores/FEATUREONLINESTORE_NAME/featureViews"

#### PowerShell

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Execute the following command:

    $cred = gcloud auth print-access-token
    $headers = @{ "Authorization" = "Bearer $cred" }
    
    Invoke-WebRequest `
        -Method GET `
        -Headers $headers `
        -Uri "https://LOCATION_ID-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION_ID/featureOnlineStores/FEATUREONLINESTORE_NAME/featureViews" | Select-Object -Expand Content

You should receive a JSON response similar to the following. If any of the feature views listed in the response has a dedicated service account configuration, then the service account email address is also listed in its details. In this example, SERVICE\_ACCOUNT\_EMAIL is the service account email address associated with the feature view FEATUREVIEW\_NAME\_1 .

    {
      "featureViews": [
        {
          "name": "projects/PROJECT_NUMBER/locations/LOCATION_ID/featureOnlineStores/FEATUREONLINESTORE_NAME/featureViews/FEATUREVIEW_NAME_1",
          "createTime": "2023-09-06T23:46:49.936284Z",
          "updateTime": "2023-09-06T23:46:49.936284Z",
          "etag": "sample_etag",
          "featureRegistrySource": {
            "featureGroups": [
              {
                "featureGroupId": "FEATUREGROUP_ID",
                "featureIds": [
                  "FEATURE_ID_1",
                  "FEATURE_ID_2",
                ]
              }
            ]
          }
          "serviceAccountEmail": "SERVICE_ACCOUNT_EMAIL"
        },
        {
          "name": "projects/PROJECT_NUMBER/locations/LOCATION_ID/featureOnlineStores/FEATUREONLINESTORE_NAME/featureViews/FEATUREVIEW_NAME_2",
          "createTime": "2024-02-05T23:48:49.936284Z",
          "updateTime": "2024-02-05T23:48:49.936284Z",
          "etag": "sample_etag",
          "featureRegistrySource": {
            "featureGroups": [
              {
                "featureGroupId": "FEATUREGROUP_ID",
                "featureIds": [
                  "FEATURE_ID_3",
                  "FEATURE_ID_4",
                ]
              }
            ]
          }
        }
      ]
    }

## What's next

  - Learn how to [update a feature view](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/featurestore/latest/update-featureview) .

  - Learn how to [delete a feature view](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/featurestore/latest/delete-featureview) .

  - [Add more feature views](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/featurestore/latest/create-featureview) .
