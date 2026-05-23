---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/featurestore/latest/update-feature
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/featurestore/latest/update-feature
title: Update a feature
description: Learn how to update an existing feature resource in Vertex AI Feature Store.
data_source: docs.cloud.google.com
---

Within a feature group, you can update a feature to associate it with a specific column in the BigQuery data source that's associated with the feature group.

While creating or updating a feature, you have the option to add user-defined metadata in the form of labels to the feature. For more information about how to update user-defined labels for a feature, see [Update labels for a feature](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/featurestore/latest/feature-labels#feature) .

## Before you begin

Authenticate to Gemini Enterprise Agent Platform, unless you've done so already.

To use the REST API samples on this page in a local development environment, you use the credentials you provide to the gcloud CLI.

For more information, see [Authenticate for using REST](https://docs.cloud.google.com/docs/authentication/rest) in the Google Cloud authentication documentation.

## Update a feature

Use the following sample to update a feature within a feature group.

### REST

To update a [`Feature`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.featureGroups.features#resource:-feature) resource, send a `PATCH` request by using the [features.patch](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.featureGroups.features/patch) method.

Before using any of the request data, make the following replacements:

  - LOCATION\_ID : Region where the feature group containing the feature is located, such as `us-central1` .
  - PROJECT\_ID : Your project ID.
  - FEATURE\_GROUP\_NAME : The name of the feature group containing the feature.
  - FEATURE\_NAME : The name of the feature you want to update.
  - VERSION\_COLUMN\_NAME : The column from the BigQuery source table or view that you want to associate while updating the feature.

HTTP method and URL:

    PATCH https://LOCATION_ID-aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/LOCATION_ID/featureGroups/FEATURE_GROUP_NAME/features?feature_id=FEATURE_NAME

Request JSON body:

    {
      "version_column_name": "VERSION_COLUMN_NAME"
    }

To send your request, choose one of these options:

#### curl

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) , or by using [Cloud Shell](https://docs.cloud.google.com/shell/docs) , which automatically logs you into the `gcloud` CLI . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Save the request body in a file named `request.json` , and execute the following command:

    curl -X PATCH \
         -H "Authorization: Bearer $(gcloud auth print-access-token)" \
         -H "Content-Type: application/json; charset=utf-8" \
         -d @request.json \
         "https://LOCATION_ID-aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/LOCATION_ID/featureGroups/FEATURE_GROUP_NAME/features?feature_id=FEATURE_NAME"

#### PowerShell

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Save the request body in a file named `request.json` , and execute the following command:

    $cred = gcloud auth print-access-token
    $headers = @{ "Authorization" = "Bearer $cred" }
    
    Invoke-WebRequest `
        -Method PATCH `
        -Headers $headers `
        -ContentType: "application/json; charset=utf-8" `
        -InFile request.json `
        -Uri "https://LOCATION_ID-aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/LOCATION_ID/featureGroups/FEATURE_GROUP_NAME/features?feature_id=FEATURE_NAME" | Select-Object -Expand Content

You should receive a JSON response similar to the following:

    {
      "name": "projects/PROJECT_NUMBER/locations/LOCATION_ID/featureGroups/FEATURE_GROUP_NAME/features/FEATURE_NAME/operations/OPERATION_ID",
      "metadata": {
        "@type": "type.googleapis.com/google.cloud.aiplatform.v1beta1.UpdateFeatureOperationMetadata",
        "genericMetadata": {
          "createTime": "2023-09-18T02:36:22.870679Z",
          "updateTime": "2023-09-18T02:36:22.870679Z"
        }
      },
      "done": true,
      "response": {
        "@type": "type.googleapis.com/google.cloud.aiplatform.v1beta1.Feature",
        "name": "projects/PROJECT_NUMBER/locations/LOCATION_ID/featureGroups/FEATURE_GROUP_NAME/features/FEATURE_NAME"
      }
    }

## What's next

  - Learn how to [create a feature](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/featurestore/latest/create-feature) .

  - Learn how to [delete a feature view](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/featurestore/latest/delete-featureview) .
