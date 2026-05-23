---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/featurestore/latest/update-onlinestore
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/featurestore/latest/update-onlinestore
title: Update an online store
description: Learn how to update an existing online store instance in Vertex AI Feature Store.
data_source: docs.cloud.google.com
---

You can update the online serving configuration for an online store created for Bigtable online serving. For example, you can update the maximum and minimum numbers of serving nodes.

While creating or updating an online store, you have the option to add user-defined metadata in the form of labels to the online store. For more information about how to update user-defined labels for an online store, see [Update labels for an online store](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/featurestore/latest/feature-labels#online_store) .

## Before you begin

Authenticate to Gemini Enterprise Agent Platform, unless you've done so already.

To use the REST API samples on this page in a local development environment, you use the credentials you provide to the gcloud CLI.

For more information, see [Authenticate for using REST](https://docs.cloud.google.com/docs/authentication/rest) in the Google Cloud authentication documentation.

## Update an online store instance

Use the following sample to update the scaling options in an online store instance created for Bigtable online serving.

### REST

To update a [`FeatureOnlineStore`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.featureOnlineStores#resource:-featureOnlineStore) resource, send a `PATCH` request by using the [featureOnlineStores.patch](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.featureOnlineStores/patch) method.

Before using any of the request data, make the following replacements:

  - LOCATION\_ID : Region where the online store is located, such as `us-central1` .
  - PROJECT\_ID : Your project ID.
  - FEATUREONLINESTORE\_NAME : The name of the online store that you want to update.

HTTP method and URL:

    PATCH https://LOCATION_ID-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION_ID/featureOnlineStores/FEATUREONLINESTORE_NAME

Request JSON body:

    {
      "bigtable": {
        "auto_scaling": {
          "min_node_count": 1,
          "max_node_count": 3,
          "cpu_utilization_target": 50
        }
      }
    }

To send your request, choose one of these options:

#### curl

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) , or by using [Cloud Shell](https://docs.cloud.google.com/shell/docs) , which automatically logs you into the `gcloud` CLI . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Save the request body in a file named `request.json` , and execute the following command:

    curl -X PATCH \
         -H "Authorization: Bearer $(gcloud auth print-access-token)" \
         -H "Content-Type: application/json; charset=utf-8" \
         -d @request.json \
         "https://LOCATION_ID-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION_ID/featureOnlineStores/FEATUREONLINESTORE_NAME"

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
        -Uri "https://LOCATION_ID-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION_ID/featureOnlineStores/FEATUREONLINESTORE_NAME" | Select-Object -Expand Content

You should receive a JSON response similar to the following:

    {
      "name": "projects/PROJECT_NUMBER/locations/LOCATION_ID/featureOnlineStores/FEATUREONLINESTORE_NAME/operations/OPERATION_ID",
      "metadata": {
        "@type": "type.googleapis.com/google.cloud.aiplatform.v1.UpdateFeatureOnlineStoreOperationMetadata",
        "genericMetadata": {
          "createTime": "2023-09-18T17:49:23.847496Z",
          "updateTime": "2023-09-18T17:49:23.847496Z"
        }
      },
      "done": true,
      "response": {
        "@type": "type.googleapis.com/google.cloud.aiplatform.v1.FeatureView",
        "name": "projects/PROJECT_NUMBER/locations/LOCATION_ID/featureOnlineStores/FEATUREONLINESTORE_NAME"
      }
    }

## What's next

  - Learn how to [delete an online store](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/featurestore/latest/delete-onlinestore) .

  - Learn how to [create a feature view](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/featurestore/latest/create-featureview) .

  - [Start online serving](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/featurestore/latest/serve-feature-values) feature data.
