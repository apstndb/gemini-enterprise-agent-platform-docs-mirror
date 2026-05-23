---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/featurestore/latest/delete-featureview
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/featurestore/latest/delete-featureview
title: Delete a feature view
description: Learn how to delete a feature view instance in Vertex AI Feature Store.
data_source: docs.cloud.google.com
---

Deleting a feature view doesn't cancel ongoing online serving operations. You need to stop any active online serving operation that's currently active from the feature view you want to delete. Otherwise, the online serving operation fails after you delete the feature view.

If your online store instance uses Bigtable online serving, the feature records that you delete from the BigQuery source table are retained in the corresponding feature views until you delete those feature views.

## Before you begin

Authenticate to Gemini Enterprise Agent Platform, unless you've done so already.

Select the tab for how you plan to use the samples on this page:

### Console

When you use the Google Cloud console to access Google Cloud services and APIs, you don't need to set up authentication.

### REST

To use the REST API samples on this page in a local development environment, you use the credentials you provide to the gcloud CLI.

For more information, see [Authenticate for using REST](https://docs.cloud.google.com/docs/authentication/rest) in the Google Cloud authentication documentation.

## Delete a feature view instance

Use the following samples to delete a feature view from an online store in your project.

### Console

Use the following instructions to delete a feature view using the Google Cloud console.

1.  In the Agent Platform section of the Google Cloud console, go to the **Feature Store** page.

2.  Click **Online store** .

3.  Click the name of the online store to view its details on the **Online store details** page.

4.  In the **Feature views** section, XZselect checkbox next to the feature view that you want to delete.

5.  Click **Delete** and then click **Confirm** .

### REST

To delete a [`FeatureView`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.featureOnlineStores.featureViews#resource:-featureView) instance, send a `DELETE` request by using the [featureViews.delete](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.featureOnlineStores.featureViews/delete) method.

Before using any of the request data, make the following replacements:

  - LOCATION\_ID : Region where the online store is located, such as `us-central1` .
  - PROJECT\_ID : Your project ID.
  - FEATUREONLINESTORE\_NAME : The name of the online store containing the feature view.
  - FEATUREVIEW\_NAME : The name of the feature view you want to delete.

HTTP method and URL:

    DELETE https://LOCATION_ID-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION_ID/featureOnlineStores/FEATUREONLINESTORE_NAME/featureViews/FEATUREVIEW_NAME

To send your request, choose one of these options:

#### curl

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) , or by using [Cloud Shell](https://docs.cloud.google.com/shell/docs) , which automatically logs you into the `gcloud` CLI . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Execute the following command:

    curl -X DELETE \
         -H "Authorization: Bearer $(gcloud auth print-access-token)" \
         "https://LOCATION_ID-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION_ID/featureOnlineStores/FEATUREONLINESTORE_NAME/featureViews/FEATUREVIEW_NAME"

#### PowerShell

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Execute the following command:

    $cred = gcloud auth print-access-token
    $headers = @{ "Authorization" = "Bearer $cred" }
    
    Invoke-WebRequest `
        -Method DELETE `
        -Headers $headers `
        -Uri "https://LOCATION_ID-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION_ID/featureOnlineStores/FEATUREONLINESTORE_NAME/featureViews/FEATUREVIEW_NAME" | Select-Object -Expand Content

You should receive a JSON response similar to the following:

    {
      "name": "projects/PROJECT_NUMBER/locations/LOCATION_ID/featureOnlineStores/FEATUREONLINESTORE_NAME/operations/OPERATION_ID",
      "metadata": {
        "@type": "type.googleapis.com/google.cloud.aiplatform.v1.DeleteOperationMetadata",
        "genericMetadata": {
          "createTime": "2023-09-15T17:30:31.741064Z",
          "updateTime": "2023-09-15T17:30:31.741064Z"
        }
      }
    }

## What's next

  - Learn how to [update a feature view](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/featurestore/latest/update-featureview) .
