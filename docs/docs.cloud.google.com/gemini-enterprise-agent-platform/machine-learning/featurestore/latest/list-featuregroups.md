---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/featurestore/latest/list-featuregroups
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/featurestore/latest/list-featuregroups
title: List feature groups
description: Learn how to retrieve a list of feature groups created for a specific location in Vertex AI Feature Store.
data_source: docs.cloud.google.com
---

You can retrieve a list of all the feature groups created for a specific location in your Google Cloud project, along with the URI of the BigQuery source table or view associated with each feature group.

If a feature group is configured to use a dedicated service account, then the details for that feature group also include the associated service account email address. For more information about creating feature groups with dedicated service account configurations, see [Configure the service account for a feature group](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/featurestore/latest/create-featuregroup#serviceaccount) .

## Before you begin

Authenticate to Gemini Enterprise Agent Platform, unless you've done so already.

Select the tab for how you plan to use the samples on this page:

### Console

When you use the Google Cloud console to access Google Cloud services and APIs, you don't need to set up authentication.

### REST

To use the REST API samples on this page in a local development environment, you use the credentials you provide to the gcloud CLI.

For more information, see [Authenticate for using REST](https://docs.cloud.google.com/docs/authentication/rest) in the Google Cloud authentication documentation.

## List feature groups

Use the following samples to retrieve a list of all feature groups for a specific location in your project.

### Console

Use the following instructions to view the list of feature groups for a specific location using the Google Cloud console.

1.  In the Agent Platform section of the Google Cloud console, go to the **Feature Store** page.

2.  In the **Feature groups** section, you can view the list of all the feature groups for the selected location.

### REST

To retrieve a list of all the [`FeatureGroup`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.featureGroups#resource:-featuregroup) resources for a specific location in your project, send a `GET` request by using the [featureGroups.list](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.featureGroups/list) method.

Before using any of the request data, make the following replacements:

  - LOCATION\_ID : Region for which you want to view the list of feature groups, such as `us-central1` .
  - PROJECT\_ID : Your project ID.

HTTP method and URL:

    GET https://LOCATION_ID-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION_ID/featureGroups

To send your request, choose one of these options:

#### curl

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) , or by using [Cloud Shell](https://docs.cloud.google.com/shell/docs) , which automatically logs you into the `gcloud` CLI . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Execute the following command:

    curl -X GET \
         -H "Authorization: Bearer $(gcloud auth print-access-token)" \
         "https://LOCATION_ID-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION_ID/featureGroups"

#### PowerShell

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Execute the following command:

    $cred = gcloud auth print-access-token
    $headers = @{ "Authorization" = "Bearer $cred" }
    
    Invoke-WebRequest `
        -Method GET `
        -Headers $headers `
        -Uri "https://LOCATION_ID-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION_ID/featureGroups" | Select-Object -Expand Content

You should receive a JSON response similar to the following. BIGQUERY\_URI\_1 is the BigQuery source table or view registered via FEATURE\_GROUP\_NAME\_1 and BIGQUERY\_URI\_2 is the BigQuery source table or view registered with FEATURE\_GROUP\_NAME\_2 .  
If any of the feature groups listed in the response has a dedicated service account configuration, then the service account email address is also listed in its details. In this example, SERVICE\_ACCOUNT\_EMAIL is the service account email address associated with the feature group FEATURE\_GROUP\_NAME\_1 .

    {
      "featureGroups": [
        {
          "name": "projects/PROJECT_NUMBER/locations/LOCATION_ID/featureGroups/FEATURE_GROUP_NAME_1",
          "createTime": "2023-09-07T00:57:00.142639Z",
          "updateTime": "2023-09-07T00:57:00.142639Z",
          "etag": "AMEw9yOY0byP8qKsDY0DoZyouAtX23zDru2l422C0affZZPYNFOGgIrONELNrM49uH4=",
          "bigQuery": {
            "bigQuerySource": {
              "inputUri": "BIGQUERY_URI_1"
            }
          }
          "serviceAccountEmail": "SERVICE_ACCOUNT_EMAIL"
        },
        {
          "name": "projects/PROJECT_NUMBER/locations/LOCATION_ID/featureGroups/FEATURE_GROUP_NAME_2",
          "createTime": "2023-09-06T23:14:30.795502Z",
          "updateTime": "2023-09-06T23:14:30.795502Z",
          "etag": "AMEw9yO5UfrPWobGR2Ry-PnbJUQoklW5lX0uW4JmKqj6OgQui6p-rMdUHfuENpQjbJ3t",
          "bigQuery": {
            "bigQuerySource": {
              "inputUri": "BIGQUERY_URI_2"
            }
          }
        }
      ]
    }

## What's next

  - Learn how to [create a feature](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/featurestore/latest/create-feature) .

  - Learn how to [update a feature group](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/featurestore/latest/update-featuregroup) .

  - Learn how to [delete a feature group](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/featurestore/latest/delete-featuregroup) .
