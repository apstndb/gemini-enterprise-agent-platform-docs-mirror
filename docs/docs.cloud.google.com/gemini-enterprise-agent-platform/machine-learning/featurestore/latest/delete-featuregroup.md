---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/featurestore/latest/delete-featuregroup
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/featurestore/latest/delete-featuregroup
title: Delete a feature group
description: Learn how to delete a feature group resource in Vertex AI Feature Store.
data_source: docs.cloud.google.com
---

When you delete a feature group, you automatically unregister any BigQuery data sources that were registered for that feature group. If the feature group contains existing features, you can use the `force` query parameter to delete the feature group. Deleting a feature group unregisters the BigQuery table or view from the Feature Registry and doesn't affect the feature data contained in those data sources.

## Before you begin

Authenticate to Gemini Enterprise Agent Platform, unless you've done so already.

Select the tab for how you plan to use the samples on this page:

### Console

When you use the Google Cloud console to access Google Cloud services and APIs, you don't need to set up authentication.

### REST

To use the REST API samples on this page in a local development environment, you use the credentials you provide to the gcloud CLI.

For more information, see [Authenticate for using REST](https://docs.cloud.google.com/docs/authentication/rest) in the Google Cloud authentication documentation.

## Delete a feature group

Use the following samples to delete a feature group along with its features.

### Console

Use the following instructions to delete a feature group and all its features using the Google Cloud console.

1.  In the Agent Platform section of the Google Cloud console, go to the **Feature Store** page.

2.  In the **Feature groups** section, select checkbox next to the feature group that you want to delete.

3.  Click **Delete** and then click **Confirm** .

### REST

To delete a [`FeatureGroup`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.featureGroups#resource:-featuregroup) resource, send a `DELETE` request by using the [featureGroups.delete](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.featureGroups/delete) method.

Before using any of the request data, make the following replacements:

  - LOCATION\_ID : Region where the feature group is located, such as `us-central1` .
  - PROJECT\_ID : Your project ID.
  - FEATURE\_GROUP\_NAME : The name of the feature group that you want to delete.
  - BOOLEAN : Optional: To delete the feature group even if it contains features, enter `true` . The default value is `false` .

HTTP method and URL:

    DELETE https://LOCATION_ID-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION_ID/featureGroups/FEATURE_GROUP_NAME?force=BOOLEAN

To send your request, choose one of these options:

#### curl

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) , or by using [Cloud Shell](https://docs.cloud.google.com/shell/docs) , which automatically logs you into the `gcloud` CLI . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Execute the following command:

    curl -X DELETE \
         -H "Authorization: Bearer $(gcloud auth print-access-token)" \
         "https://LOCATION_ID-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION_ID/featureGroups/FEATURE_GROUP_NAME?force=BOOLEAN"

#### PowerShell

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Execute the following command:

    $cred = gcloud auth print-access-token
    $headers = @{ "Authorization" = "Bearer $cred" }
    
    Invoke-WebRequest `
        -Method DELETE `
        -Headers $headers `
        -Uri "https://LOCATION_ID-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION_ID/featureGroups/FEATURE_GROUP_NAME?force=BOOLEAN" | Select-Object -Expand Content

You should receive a JSON response similar to the following:

    {
      "name": "projects/PROJECT_NUMBER/locations/LOCATION_ID/operations/OPERATION_ID",
      "metadata": {
        "@type": "type.googleapis.com/google.cloud.aiplatform.v1.DeleteOperationMetadata",
        "genericMetadata": {
          "createTime": "2023-09-15T04:54:03.632646Z",
          "updateTime": "2023-09-15T04:54:03.632646Z"
        }
      },
      "done": true,
      "response": {
        "@type": "type.googleapis.com/google.protobuf.Empty"
      }
    }

## What's next

  - Learn how to [create a feature group](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/featurestore/latest/create-featuregroup) .

  - Learn how to [update a feature group](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/featurestore/latest/update-featuregroup) .

  - Learn how to [delete a feature from a feature group](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/featurestore/latest/delete-feature) .
