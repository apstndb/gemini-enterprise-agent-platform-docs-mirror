---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/featurestore/latest/create-featuregroup
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/featurestore/latest/create-featuregroup
title: Create a feature group
description: Learn how to create a feature group resource in Vertex AI Feature Store.
data_source: docs.cloud.google.com
---

A feature group is a Feature Registry resource that's associated with a BigQuery table or view containing your feature data. A feature group can contain multiple features , where each feature is associated with a column in the feature data source. If you want to register your feature data source in the Feature Registry, create a feature group and then [add features](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/featurestore/latest/create-feature) to it.

After you create a feature group and associate the BigQuery data source, you can [create features](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/featurestore/latest/create-feature) associated with the columns in the data source. Note that although it's optional to associate a data source while creating a feature group, you must associate a BigQuery table or view before you create features within that feature group. Each feature corresponds to a column in the data source associated with the feature group.

## Why use feature groups and features?

Registering your feature data source is optional. However, you must register your feature data by creating feature groups and features in the following scenarios:

  - **Use historical data in time series format to train a model** : If the feature data source contains latest as well as historical feature data with multiple feature records for the same entity ID, then format this data as a time series by adding the `feature_timestamp` column. In this scenario, you must register the data source using feature groups and features. You can then serve features, as follows:
    
      - Use [online serving](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/featurestore/latest/serve-feature-values) to serve the latest feature values based on the timestamp to make real-time predictions.
    
      - Use [offline serving](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/featurestore/latest/serve-historical-features) to serve latest as well as historical feature values to train a model.

  - **Aggregate features from multiple sources** : Use feature groups to aggregate specific columns from multiple BigQuery data sources when you [create a feature view instance](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/featurestore/latest/create-featureview) .

  - **Serve null feature values** : During online serving, if you want to serve only the latest feature values, including null values, then register your featured data source by creating feature groups with the `dense` parameter set to `true` .
    
    > **Note:** To serve null feature values, you must also use an online store instance configured for Bigtable online serving and use scheduled data sync in your feature views.

  - **Use continuous data sync in your feature views** : Registering your features is a prerequisite for using continuous data sync in your feature views.
    
    > **Note:** To use continuous data sync, you must also meet the following requirements:
    > 
    >   - The online store instance must be configured for Bigtable online serving.
    >   - The associated BigQuery data source must be located in `eu` , `us` , or `us-central1` .

  - **Monitor features for anomalies** : You must register your features if you want to set up [feature monitoring](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/featurestore/latest/monitor-features) to retrieve feature statistics and detect feature drift.

## When not to use feature groups and features

If you want to [serve embeddings](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/featurestore/latest/embeddings-search) from your feature data source, then don't register the data source by creating feature groups and features. In this scenario, you must set up online serving by directly associating the BigQuery table or view with your feature views.

For more information about setting up online serving without registering your feature data source, see [Create a feature view from a BigQuery source](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/featurestore/latest/create-featureview#create_from_bq) .

## Control access

You can control access for a feature group at the following levels:

  - **Control access to the `FeatureGroup` resource** : To control access to a feature group for a specific individual, Google group, domain, or service account, [set up an IAM policy for the feature group](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/featurestore/latest#set_iam_fg) .

  - **Control access to the BigQuery data source** : By default, a feature group uses the default service account configured for the project. Vertex AI Feature Store assigns the [BigQuery Data Viewer](https://docs.cloud.google.com/bigquery/docs/access-control#bigquery.dataViewer) Identity and Access Management (IAM) role to this service account. This lets any user with permission to create a feature group in the project access the feature data source in BigQuery. To restrict access to the BigQuery data source or to grant access to additional users, you can set up your feature group to use its own dedicated service account. Vertex AI Feature Store generates a unique service account email address for each feature group configured to have a dedicated service account.
    
    > **Note:** You can view the dedicated service account email address for a feature group in one of the following ways:
    > 
    >   - [Retrieve a list of all feature groups](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/featurestore/latest/list-featuregroups) by using the [`featureGroups.list`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.featureGroups/list) method.
    >   - Retrieve the details of the feature group by using the [`featureGroups.get`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.featureGroups/get) method.

## Before you begin

Before you create a feature group, complete the following prerequisites:

  - Ensure that there's at least one online store instance created in your project, even if you want to create a new online store instance. If you're using a new project, then [create an online store instance](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/featurestore/latest/create-onlinestore) before you create the feature group.

  - Format your feature data in the BigQuery table or view to conform to the [Data source preparation guidelines](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/featurestore/latest/prepare-data-source#guidelines) .

  - Verify that your BigQuery data source contains at least one entity ID column with `string` or `int` values.

  - Authenticate to Gemini Enterprise Agent Platform, unless you've done so already.
    
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

## Create a feature group to register a feature data source

Use the following samples to create a feature group and associate a feature data source, such as a BigQuery table or view.

### Console

> **Important:** You can't create a feature group with a dedicated service account from the Google Cloud console. To create a feature group with a dedicated service account, use the REST API or the Agent Platform SDK for Python.

Use the following instructions to create a feature group using the Google Cloud console:

1.  In the Agent Platform section of the Google Cloud console, go to the **Feature Store** page.

2.  In the **Feature groups** section, click **Create** to open the **Basic info** pane on the **Create Feature Group** page.

3.  Specify the **Feature group name** .

4.  Optional: To add labels, click **Add label** , and specify the label name and value. You can add multiple labels to a feature group.

5.  In the **BigQuery path** field, click **Browse** to select BigQuery source table or view to associate with the feature group.

6.  In the **Entity ID column** list, select the entity ID columns from the BigQuery source table or view.
    
    Note that this is optional if the BigQuery source table or view has a column named `entity_id` . In that case, if you don't select an entity ID column, the feature group uses the `entity_id` column as the default entity ID column.

7.  Click **Continue** .

8.  In the **Register** pane, click one of the following options to indicate whether you want to add features to the new feature group:
    
      - **Include all columns from the BigQuery table** —Create features within the feature group for all the columns in the BigQuery source table or view.
    
      - **Manually enter your features** —Create features based on specific columns in the BigQuery source. For each feature, enter a **Feature name** and click the corresponding BigQuery source column name in the list.
        
        To add more features, click **Add another feature** .
    
      - **Create an empty feature group** —Create the feature group without adding features to it.

9.  Click **Create** .

### Python

To learn how to install or update the Vertex AI SDK for Python, see [Install the Vertex AI SDK for Python](https://docs.cloud.google.com/vertex-ai/docs/start/use-vertex-ai-python-sdk) . For more information, see the [Python API reference documentation](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest) .

> **Note:** This sample creates a feature group with the default service account configuration.

    from google.cloud import aiplatform
    from vertexai.resources.preview import feature_store
    from typing import List
    
    
    def create_feature_group_sample(
        project: str,
        location: str,
        feature_group_id: str,
        bq_table_uri: str,
        entity_id_columns: List[str],
    ):
        aiplatform.init(project=project, location=location)
        fg = feature_store.FeatureGroup.create(
            name=feature_group_id,
            source=feature_store.utils.FeatureGroupBigQuerySource(
                uri=bq_table_uri, entity_id_columns=entity_id_columns
            ),
        )
        return fg

  - `project` : Your project ID.
  - `location` : Region where you want to create the feature group, such as `us-central1` .
  - `feature_group_id` : The name of the new feature group that you want to create.
  - `bq_table_uri` : URI of the BigQuery source table or view that you want to register for the feature group.
  - `entity_id_columns` : The names of the columns containing the entity IDs. You can specify either one column or multiple columns.
      - To specify only one entity ID column, specify the column name in the following format:  
        `"entity_id_column_name"` .
      - To specify multiple entity ID columns, specify the column names in the following format:  
        `["entity_id_column_1_name", "entity_id_column_2_name", ...]` .

### REST

To create a [`FeatureGroup`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.featureGroups#resource:-featuregroup) resource, send a `POST` request by using the [featureGroups.create](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.featureGroups/create) method.

Before using any of the request data, make the following replacements:

  - LOCATION\_ID : Region where you want to create the feature group, such as `us-central1` .

  - SERVICE\_AGENT\_TYPE : Optional. Service account configuration for the feature group. To use a dedicated service account for the feature group, enter `SERVICE_AGENT_TYPE_FEATURE_GROUP` .

  - PROJECT\_ID : Your project ID.

  - ENTITY\_ID\_COLUMNS : The names of the column(s) containing the entity IDs. You can specify either one column or multiple columns.
    
      - To specify only one entity ID column, specify the column name in the following format:  
        `"entity_id_column_name"` .
      - To specify multiple entity ID columns, specify the column names in the following format:  
        `["entity_id_column_1_name", "entity_id_column_2_name", ...]` .

  - FEATUREGROUP\_NAME : The name of the new feature group that you want to create.

  - BIGQUERY\_SOURCE\_URI : URI of the BigQuery source table or view that you want to register for the feature group.

  - TIMESTAMP\_COLUMN : Optional. Specify the name of the column containing the feature timestamps in the BigQuery source table or view.  
    You need to specify the timestamp column name only if the data is formatted as a time series and the column containing the feature timestamps isn't named `feature_timestamp` .  
    
    > **Caution** : Don't include the `time_series` parameter if you set the `static_data_source` parameter to `true` .

  - STATIC\_DATA\_SOURCE : Optional. Enter `true` if the data isn't formatted as a time series. The default setting is `false` .  
    
    > **Caution** : Don't include `static_data_source` parameter if you use the `time_series` parameter.

  - DENSE : Optional. Indicate how Vertex AI Feature Store handles null values while serving data from feature views associated with the feature group:
    
      - `false` —This is the default setting. Vertex AI Feature Store serves only the latest non-null feature values. If the latest value for a feature is null, Vertex AI Feature Store serves the most recent non-null historical value. However, if the current as well as historical values for that feature are null, then Vertex AI Feature Store serves null as the feature value.
      - `true` —For feature views with scheduled data sync, Vertex AI Feature Store serves only the latest feature values, including null values. For feature views with continuous data sync, Vertex AI Feature Store serves only the latest non-null feature values. However, if the current as well as historical values for the feature are null, then Vertex AI Feature Store serves null as the feature value. For more information about data sync types and how to configure the type of data sync in a feature view, see [Sync the data in a feature view](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/featurestore/latest/create-featureview#sync_featuredata) .

HTTP method and URL:

    POST https://LOCATION_ID-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION_ID/featureGroups?feature_group_id=FEATUREGROUP_NAME

Request JSON body:

    {
      "service_agent_type": "SERVICE_AGENT_TYPE",
      "big_query": {
        "entity_id_columns": "ENTITY_ID_COLUMNS",
        "big_query_source": {
          "input_uri": "BIGQUERY_SOURCE_URI",
        }
        "time_series": {
          "timestamp_column": ""TIMESTAMP_COLUMN"",
        },
        "static_data_source": STATIC_DATA_SOURCE,
        "dense": DENSE
      }
    }

To send your request, choose one of these options:

#### curl

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) , or by using [Cloud Shell](https://docs.cloud.google.com/shell/docs) , which automatically logs you into the `gcloud` CLI . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Save the request body in a file named `request.json` , and execute the following command:

    curl -X POST \
         -H "Authorization: Bearer $(gcloud auth print-access-token)" \
         -H "Content-Type: application/json; charset=utf-8" \
         -d @request.json \
         "https://LOCATION_ID-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION_ID/featureGroups?feature_group_id=FEATUREGROUP_NAME"

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
        -Uri "https://LOCATION_ID-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION_ID/featureGroups?feature_group_id=FEATUREGROUP_NAME" | Select-Object -Expand Content

You should receive a JSON response similar to the following:

    {
      "name": "projects/PROJECT_NUMBER/locations/LOCATION_ID/featureGroups/FEATUREGROUP_NAME/operations/OPERATION_ID",
      "metadata": {
        "@type": "type.googleapis.com/google.cloud.aiplatform.v1.UpdateFeatureGroupOperationMetadata",
        "genericMetadata": {
          "createTime": "2023-09-18T03:00:13.060636Z",
          "updateTime": "2023-09-18T03:00:13.060636Z"
        }
      }
    }

## What's next

  - Learn how to [create a feature](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/featurestore/latest/create-feature) .

  - Learn how to [update a feature group](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/featurestore/latest/update-featuregroup) .

  - Learn how to [delete a feature group](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/featurestore/latest/delete-featuregroup) .
