---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/featurestore/latest/create-feature
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/featurestore/latest/create-feature
title: Create a feature
description: Learn how to create a feature within an existing feature group in Vertex AI Feature Store.
data_source: docs.cloud.google.com
---

You can create a feature after you [create a feature group and associate a BigQuery table or BigQuery view with it](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/featurestore/latest/create-featuregroup) . You can create multiple features for a feature group and associate each feature with a specific column in the BigQuery data source. For information about how to use BigQuery, refer to the [BigQuery documentation](https://docs.cloud.google.com/bigquery/docs) .

For example, if the feature group `featuregroup1` is associated with the BigQuery table `datasource_1` containing feature values in columns `fval1` and `fval2` , then you can create feature `feature_1` under `featuregroup1` and associate it with the feature values in column `fval1` . Similarly, you can create another feature named `feature_2` and associate it with the feature values in column `fval2` .

A feature group must have a feature data source associated with it before you can create features. If the feature group doesn't have an associated data source, you must associate a BigQuery data source by [updating the feature group](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/featurestore/latest/update-featuregroup) , before you can create features within it.

To understand whether it's mandatory, optional, or inadvisable for you to register your feature data using feature groups and features, see the following:

  - [Why use feature groups and features?](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/featurestore/latest/create-featuregroup#why_use_feature_groups_and_features)

  - [When not to use feature groups and features.](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/featurestore/latest/create-featuregroup#when_not_to_use_feature_groups_and_features)

## Before you begin

Authenticate to Gemini Enterprise Agent Platform, unless you've done so already.

Select the tab for how you plan to use the samples on this page:

### Console

When you use the Google Cloud console to access Google Cloud services and APIs, you don't need to set up authentication.

### Python

To use the Python samples on this page in a local development environment, install and initialize the gcloud CLI, and then set up Application Default Credentials with your user credentials.

1.  [Install](https://docs.cloud.google.com/sdk/docs/install) the Google Cloud CLI.

2.  If you're using an external identity provider (IdP), you must first [sign in to the gcloud CLI with your federated identity](https://docs.cloud.google.com/iam/docs/workforce-log-in-gcloud) .

3.  If you're using a local shell, then create local authentication credentials for your user account:
    
        gcloud auth application-default login
    
    You don't need to do this if you're using Cloud Shell.
    
    If an authentication error is returned, and you are using an external identity provider (IdP), confirm that you have [signed in to the gcloud CLI with your federated identity](https://docs.cloud.google.com/iam/docs/workforce-log-in-gcloud) .

For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/authentication#local-development) .

### REST

To use the REST API samples on this page in a local development environment, you use the credentials you provide to the gcloud CLI.

For more information, see [Authenticate for using REST](https://docs.cloud.google.com/docs/authentication/rest) in the Google Cloud authentication documentation.

## Create a feature within a feature group

Use the following samples to create a feature within a feature group and associate a column containing feature values from the BigQuery data source registered for the feature group.

### Console

Use the following instructions to add features to an existing feature group using the Google Cloud console.

1.  In the Agent Platform section of the Google Cloud console, go to the **Feature Store** page.

2.  In the **Feature groups** section, click more\_vert in the row corresponding to the feature group where you want to add a feature, and then click **Add features** .

3.  For each feature, enter a **Feature name** and click the corresponding BigQuery source column name in the list. To add more features, click **Add another feature** .

4.  Click **Create** .

### Python

To learn how to install or update the Vertex AI SDK for Python, see [Install the Vertex AI SDK for Python](https://docs.cloud.google.com/vertex-ai/docs/start/use-vertex-ai-python-sdk) . For more information, see the [Python API reference documentation](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest) .

    from google.cloud import aiplatform
    from vertexai.resources.preview import feature_store
    
    
    def create_feature_sample(
        project: str,
        location: str,
        existing_feature_group_id: str,
        feature_id: str,
        version_column_name: str,
    ):
        aiplatform.init(project=project, location=location)
        feature_group = feature_store.FeatureGroup(existing_feature_group_id)
        feature = feature_group.create_feature(
            name=feature_id, version_column_name=version_column_name
        )
        return feature

  - `project` : Your project ID.
  - `location` : Region where the feature group is located, such as `us-central1` .
  - `existing_feature_group_id` : The name of the existing feature group where you want to create the feature.
  - `version_column_name` : Optional: The column from the BigQuery table or view that you want to associate with the feature. If you don't specify this parameter, it's set to FEATURE\_NAME , by default.
  - `feature_id` : The name of the new feature you want to create

### REST

To create a [`Feature`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.featureGroups.features#resource:-feature) resource, send a `POST` request by using the [features.create](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.featureGroups.features/create) method.

Before using any of the request data, make the following replacements:

  - LOCATION\_ID : Region where the feature group is located, such as `us-central1` .
  - PROJECT\_ID : Your project ID.
  - FEATUREGROUP\_NAME : The name of the feature group where you want to create the feature.
  - FEATURE\_NAME : The name of the new feature you want to create.
  - VERSION\_COLUMN\_NAME : Optional: The column from the BigQuery table or view that you want to associate with the feature. If you don't specify this parameter, it's set to FEATURE\_NAME , by default.

HTTP method and URL:

    POST https://LOCATION_ID-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION_ID/featureGroups/FEATUREGROUP_NAME/features?feature_id=FEATURE_NAME

Request JSON body:

    {
      "version_column_name": "VERSION_COLUMN_NAME"
    }

To send your request, choose one of these options:

#### curl

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) , or by using [Cloud Shell](https://docs.cloud.google.com/shell/docs) , which automatically logs you into the `gcloud` CLI . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Save the request body in a file named `request.json` , and execute the following command:

    curl -X POST \
         -H "Authorization: Bearer $(gcloud auth print-access-token)" \
         -H "Content-Type: application/json; charset=utf-8" \
         -d @request.json \
         "https://LOCATION_ID-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION_ID/featureGroups/FEATUREGROUP_NAME/features?feature_id=FEATURE_NAME"

#### PowerShell

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Save the request body in a file named `request.json` , and execute the following command:

    $cred = gcloud auth print-access-token
    $headers = @{ "Authorization" = "Bearer $cred" }
    
    Invoke-WebRequest `
        -Method POST `
        -Headers $headers `
        -ContentType: "application/json; charset=utf-8" `
        -InFile request.json `
        -Uri "https://LOCATION_ID-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION_ID/featureGroups/FEATUREGROUP_NAME/features?feature_id=FEATURE_NAME" | Select-Object -Expand Content

You should receive a JSON response similar to the following:

    {
      "name": "projects/PROJECT_NUMBER/locations/LOCATION_ID/featureGroups/FEATUREGROUP_NAME/features/FEATURE_NAME/operations/OPERATION_ID",
      "metadata": {
        "@type": "type.googleapis.com/google.cloud.aiplatform.v1.UpdateFeatureOperationMetadata",
        "genericMetadata": {
          "createTime": "2023-09-18T02:36:22.870679Z",
          "updateTime": "2023-09-18T02:36:22.870679Z"
        }
      }
    }

## What's next

  - Learn how to [list all features in a feature group](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/featurestore/latest/list-features) .

  - Learn how to [update a feature](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/featurestore/latest/update-feature) .

  - Learn how to [delete a feature](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/featurestore/latest/delete-feature) .

  - Learn how to [update a feature group](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/featurestore/latest/update-featuregroup) .

  - Set up [feature monitoring](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/featurestore/latest/monitor-features) for features in a feature group.

  - [Online serving types](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/featurestore/latest/online-serving-types) in Vertex AI Feature Store.
