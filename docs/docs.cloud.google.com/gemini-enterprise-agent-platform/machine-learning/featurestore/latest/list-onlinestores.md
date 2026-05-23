---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/featurestore/latest/list-onlinestores
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/featurestore/latest/list-onlinestores
title: List online stores
description: Learn how to retrieve a list of online store instances for a specific location in Vertex AI Feature Store.
data_source: docs.cloud.google.com
---

You can retrieve a list of all the online store instances created for a specific location in your Google Cloud project, along with the online serving configuration for each online store.

## Before you begin

Authenticate to Gemini Enterprise Agent Platform, unless you've done so already.

Select the tab for how you plan to use the samples on this page:

### Console

When you use the Google Cloud console to access Google Cloud services and APIs, you don't need to set up authentication.

### REST

To use the REST API samples on this page in a local development environment, you use the credentials you provide to the gcloud CLI.

For more information, see [Authenticate for using REST](https://docs.cloud.google.com/docs/authentication/rest) in the Google Cloud authentication documentation.

## List online store instances

Use the following samples to retrieve a list of all the online store instances in your project for a specific location.

### Console

Use the following instructions to view the list of online stores for a specific location using the Google Cloud console.

1.  In the Agent Platform section of the Google Cloud console, go to the **Feature Store** page.

2.  Click **Online store** .

3.  In the **Online stores** section, you can view the list of all the online stores for the selected location.

### REST

To retrieve a list of all the [`FeatureOnlineStore`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.featureOnlineStores#resource:-featureOnlineStore) resources in your project, send a `GET` request by using the [featureOnlineStores.list](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.featureOnlineStores/list) method.

Before using any of the request data, make the following replacements:

  - LOCATION\_ID : Region for which you want to view the list of online stores, such as `us-central1` .
  - PROJECT\_ID : Your project ID.

HTTP method and URL:

    GET https://LOCATION_ID-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION_ID/featureOnlineStores

To send your request, choose one of these options:

#### curl

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) , or by using [Cloud Shell](https://docs.cloud.google.com/shell/docs) , which automatically logs you into the `gcloud` CLI . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Execute the following command:

    curl -X GET \
         -H "Authorization: Bearer $(gcloud auth print-access-token)" \
         "https://LOCATION_ID-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION_ID/featureOnlineStores"

#### PowerShell

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Execute the following command:

    $cred = gcloud auth print-access-token
    $headers = @{ "Authorization" = "Bearer $cred" }
    
    Invoke-WebRequest `
        -Method GET `
        -Headers $headers `
        -Uri "https://LOCATION_ID-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION_ID/featureOnlineStores" | Select-Object -Expand Content

You should see output similar to the following. You can use the OPERATION\_ID in the response to [get the status](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/long-running-operations) of the operation.

    {
      "featureOnlineStores": [
        {
          "name": "projects/PROJECT_NUMBER/locations/LOCATION_ID/featureOnlineStores/FEATUREONLINESTORE_NAME_1",
          "createTime": "2023-09-06T23:25:04.256314Z",
          "updateTime": "2023-09-06T23:25:04.256314Z",
          "etag": "AMEw9yMgoV0bAsYuKwVxz4Y7lOmxV7riNVHg217KaQAKORqvdqGCrQ1DIt8yHgoGXf8=",
          "bigtable": {
            "autoScaling": {
              "minNodeCount": 1,
              "maxNodeCount": 4,
              "cpuUtilizationTarget": 70
            }
          }
        },
        {
          "name": "projects/PROJECT_NUMBER/locations/LOCATION_ID/featureOnlineStores/FEATUREONLINESTORE_NAME_2",
          "createTime": "2023-07-21T14:24:20.206446Z",
          "updateTime": "2023-07-21T14:24:20.206446Z",
          "etag": "AMEw9yPTfvIHvpFD-mbtMVKG4Sp_y08aDFZiZl4m_97VvC0YiyEVj-sbDo_NkVueeBo=",
          "bigtable": {
            "autoScaling": {
              "minNodeCount": 1,
              "maxNodeCount": 4,
              "cpuUtilizationTarget": 70
            }
          }
        }
      ]
    }

## What's next

  - Learn how to [create a feature view within an online store](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/featurestore/latest/create-featureview) .

  - Learn how to [update an online store](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/featurestore/latest/update-onlinestore) .

  - Learn how to [delete an online store](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/featurestore/latest/delete-onlinestore) .
