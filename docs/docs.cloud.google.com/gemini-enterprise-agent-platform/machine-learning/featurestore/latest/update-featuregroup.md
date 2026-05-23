---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/featurestore/latest/update-featuregroup
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/featurestore/latest/update-featuregroup
title: Update a feature group
description: Learn how to update an existing feature group resource in Vertex AI Feature Store.
data_source: docs.cloud.google.com
---

> **Preview**
> 
> This feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](https://docs.cloud.google.com/terms/service-terms#1) . Pre-GA features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

You can update a feature group to register a BigQuery table or view as the feature data source for that feature group. If the feature group already has an associated data source, you can associate a different BigQuery table or view as the feature data source.

> **Caution:** You can update a feature group even if there are feature views and features associated with it. If the updated data source excludes a column that's being used for online serving or is associated with a feature view or feature, then you also need to update that [feature view](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/featurestore/latest/update-featureview) or [feature](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/featurestore/latest/update-feature) .

While creating or updating a feature group, you have the option to add user-defined metadata in the form of labels to the feature group. For more information about how to update user-defined labels for a feature group, see [Update labels for a feature group](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/featurestore/latest/feature-labels#feature_group) .

## Before you begin

Authenticate to Gemini Enterprise Agent Platform, unless you've done so already.

To use the REST API samples on this page in a local development environment, you use the credentials you provide to the gcloud CLI.

For more information, see [Authenticate for using REST](https://docs.cloud.google.com/docs/authentication/rest) in the Google Cloud authentication documentation.

## Update a feature group

Use the following sample to update a feature group.

### REST

To update a [`FeatureGroup`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.featureGroups#resource:-featuregroup) resource, send a `PATCH` request by using the [featureGroups.patch](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.featureGroups/patch) method.

Before using any of the request data, make the following replacements:

  - LOCATION\_ID : Region where the feature group is located, such as `us-central1` .
  - PROJECT\_ID : Your project ID.
  - FEATURE\_GROUP\_NAME : The name of the feature group that you want to update.
  - ENTITY\_ID\_COLUMNS : The names of the column(s) containing the entity IDs. You can specify either one column or multiple columns.
      - To specify only one entity ID column, specify the column name in the following format:  
        `"entity_id_column_name"` .
      - To specify multiple entity ID columns, specify the column names in the following format:  
        `["entity_id_column_1_name", "entity_id_column_2_name", ...]` .
  - BIGQUERY\_SOURCE\_URI : URI of the BigQuery source table or view that you want to associate with the feature group.

HTTP method and URL:

    PATCH https://LOCATION_ID-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION_ID/featureGroups?feature_group_id=FEATURE_GROUP_NAME

Request JSON body:

    {
      "big_query": {
        "entity_id_columns": "ENTITY_ID_COLUMNS",
        "big_query_source": {
          "input_uri": "BIGQUERY_SOURCE_URI"
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
         "https://LOCATION_ID-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION_ID/featureGroups?feature_group_id=FEATURE_GROUP_NAME"

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
        -Uri "https://LOCATION_ID-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION_ID/featureGroups?feature_group_id=FEATURE_GROUP_NAME" | Select-Object -Expand Content

You should receive a JSON response similar to the following:

    {
      "name": "projects/PROJECT_NUMBER/locations/LOCATION_ID/featureGroups/FEATURE_GROUP_NAME/operations/OPERATION_ID",
      "metadata": {
        "@type": "type.googleapis.com/google.cloud.aiplatform.v1.UpdateFeatureGroupOperationMetadata",
        "genericMetadata": {
          "createTime": "2023-09-18T03:00:13.060636Z",
          "updateTime": "2023-09-18T03:00:13.060636Z"
        }
      },
      "done": true,
      "response": {
        "@type": "type.googleapis.com/google.cloud.aiplatform.v1.FeatureGroup",
        "name": "projects/PROJECT_NUMBER/locations/LOCATION_ID/featureGroups/FEATURE_GROUP_NAME"
      }
    }

## What's next

  - Learn how to [update a feature view](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/featurestore/latest/update-featureview) .

  - Learn how to [update a feature](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/featurestore/latest/update-feature) .

  - Learn how to [delete a feature group](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/featurestore/latest/update-featureview) .
