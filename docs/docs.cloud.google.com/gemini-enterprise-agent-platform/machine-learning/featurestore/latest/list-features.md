---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/featurestore/latest/list-features
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/featurestore/latest/list-features
title: List features
description: Learn how to retrieve a list of features within a feature group in Vertex AI Feature Store.
data_source: docs.cloud.google.com
---

You can retrieve a list of the features added to a specific feature group in your Google Cloud project. Each feature corresponds to feature values contained in a specific column in the BigQuery source table or view associated with the feature group.

## Before you begin

Authenticate to Gemini Enterprise Agent Platform, unless you've done so already.

Select the tab for how you plan to use the samples on this page:

### Console

When you use the Google Cloud console to access Google Cloud services and APIs, you don't need to set up authentication.

### REST

To use the REST API samples on this page in a local development environment, you use the credentials you provide to the gcloud CLI.

For more information, see [Authenticate for using REST](https://docs.cloud.google.com/docs/authentication/rest) in the Google Cloud authentication documentation.

## List features in a feature group

Use the following samples to retrieve the list of features within a feature group.

### Console

Use the following instructions to view the list of features within a feature group using the Google Cloud console.

1.  In the Agent Platform section of the Google Cloud console, go to the **Feature Store** page.

2.  In the **Feature groups** section, click the expand icon next to the feature group name to view all the features within it.

### REST

To retrieve a list of all the [`Feature`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.featureGroups.features#resource:-feature) resources within a specific feature group in your project, send a `GET` request by using the [features.list](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.featureGroups.features/list) method.

Before using any of the request data, make the following replacements:

  - LOCATION\_ID : Region where the featuregroup is located, such as `us-central1` .
  - PROJECT\_ID : Your project ID.
  - FEATURE\_GROUP\_NAME : The name of the feature group for which you want to view the list of features.

HTTP method and URL:

    GET https://LOCATION_ID-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION_ID/featureGroups/FEATURE_GROUP_NAME/features

To send your request, choose one of these options:

#### curl

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) , or by using [Cloud Shell](https://docs.cloud.google.com/shell/docs) , which automatically logs you into the `gcloud` CLI . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Execute the following command:

    curl -X GET \
         -H "Authorization: Bearer $(gcloud auth print-access-token)" \
         "https://LOCATION_ID-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION_ID/featureGroups/FEATURE_GROUP_NAME/features"

#### PowerShell

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Execute the following command:

    $cred = gcloud auth print-access-token
    $headers = @{ "Authorization" = "Bearer $cred" }
    
    Invoke-WebRequest `
        -Method GET `
        -Headers $headers `
        -Uri "https://LOCATION_ID-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION_ID/featureGroups/FEATURE_GROUP_NAME/features" | Select-Object -Expand Content

You should receive a JSON response similar to the following:

    {
      "features": [
        {
          "name": "projects/PROJECT_NUMBER/locations/LOCATION_ID/featureGroups/FEATURE_GROUP_NAME/features/FEATURE_NAME_1",
          "createTime": "2023-09-06T23:16:00.429055Z",
          "updateTime": "2023-09-06T23:16:00.429055Z",
          "etag": "AMEw9yP4QWrXwty9C5J9a77O3_yV5LW4DUIIagKpmoHdzctF577OtlBlOyZC7EIQUZ8_",
          "versionColumnName": "double"
        },
        {
          "name": "projects/PROJECT_NUMBER/locations/LOCATION_ID/featureGroups/FEATURE_GROUP_NAME/features/FEATURE_NAME_2",
          "createTime": "2023-09-07T00:59:39.330881Z",
          "updateTime": "2023-09-07T00:59:39.330881Z",
          "etag": "AMEw9yOZhegkDL44AMibnanMoDNJeVx-MHwcOqAQuihGHWFQxJMpvG3ePH3bNDS-tIRX",
          "versionColumnName": "double2"
        }
      ]
    }

## What's next

  - Learn how to [create a feature view](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/featurestore/latest/create-featureview) .

  - Learn how to [update a feature](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/featurestore/latest/update-feature) .

  - Learn how to [delete a feature](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/featurestore/latest/delete-feature) .
