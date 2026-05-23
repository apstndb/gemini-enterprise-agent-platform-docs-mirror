---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/featurestore/latest/delete-feature
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/featurestore/latest/delete-feature
title: Delete a feature
description: Learn how to delete a feature resource in Vertex AI Feature Store.
data_source: docs.cloud.google.com
---

You can delete specific features from a feature group. Deleting a feature unregisters the feature column from the Feature Registry and doesn't affect the data in the column in the registered BigQuery source table or view. You can [create another feature](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/featurestore/latest/create-feature) in any feature group to register the same column again, if necessary.

## Before you begin

Authenticate to Gemini Enterprise Agent Platform, unless you've done so already.

To use the REST API samples on this page in a local development environment, you use the credentials you provide to the gcloud CLI.

For more information, see [Authenticate for using REST](https://docs.cloud.google.com/docs/authentication/rest) in the Google Cloud authentication documentation.

## Delete a feature

Use the following sample to delete a feature from a feature group.

### REST

To delete a [`Feature`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.featureGroups.features#resource:-feature) resource, send a `DELETE` request by using the [features.delete](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.featureGroups.features/delete) method.

Before using any of the request data, make the following replacements:

  - LOCATION\_ID : Region where the feature group is located, such as `us-central1` .
  - PROJECT\_ID : Your project ID.
  - FEATURE\_GROUP\_NAME : The name of the feature group containing the feature.
  - FEATURE\_NAME : The name of the feature that you want to delete.

HTTP method and URL:

    DELETE https://LOCATION_ID-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION_ID/featureGroups/FEATURE_GROUP_NAME/features/FEATURE_NAME

To send your request, choose one of these options:

#### curl

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) , or by using [Cloud Shell](https://docs.cloud.google.com/shell/docs) , which automatically logs you into the `gcloud` CLI . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Execute the following command:

    curl -X DELETE \
         -H "Authorization: Bearer $(gcloud auth print-access-token)" \
         "https://LOCATION_ID-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION_ID/featureGroups/FEATURE_GROUP_NAME/features/FEATURE_NAME"

#### PowerShell

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Execute the following command:

    $cred = gcloud auth print-access-token
    $headers = @{ "Authorization" = "Bearer $cred" }
    
    Invoke-WebRequest `
        -Method DELETE `
        -Headers $headers `
        -Uri "https://LOCATION_ID-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION_ID/featureGroups/FEATURE_GROUP_NAME/features/FEATURE_NAME" | Select-Object -Expand Content

You should receive a JSON response similar to the following:

    "name": "projects/PROJECT_NUMBER/locations/LOCATION_ID/operations/OPERATION_ID",
      "metadata": {
        "@type": "type.googleapis.com/google.cloud.aiplatform.v1.DeleteOperationMetadata",
        "genericMetadata": {
          "createTime": "2023-09-25T18:52:42.092928Z",
          "updateTime": "2023-09-25T18:52:42.092928Z"
        }
      },
      "done": true,
      "response": {
        "@type": "type.googleapis.com/google.protobuf.Empty"
      }
    }

## What's next

  - Learn how to [create a feature](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/featurestore/latest/create-feature) .

  - Learn how to [update a feature](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/featurestore/latest/update-feature) .

  - Learn how to [delete a feature group along with its features](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/featurestore/latest/delete-featuregroup) .
