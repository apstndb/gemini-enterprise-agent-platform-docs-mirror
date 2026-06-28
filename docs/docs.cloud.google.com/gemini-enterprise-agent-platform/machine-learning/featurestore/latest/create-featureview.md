---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/featurestore/latest/create-featureview
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/featurestore/latest/create-featureview
title: Create a feature view instance
description: Learn how to create a feature view instance in Vertex AI Feature Store.
data_source: docs.cloud.google.com
---

You can create a feature view within an existing online store instance. While creating a feature view, you can associate features with it in the following ways:

  - **Add feature groups and features from Feature Registry :** Associate with existing feature groups and features from the Feature Registry. A feature group specifies the location of the BigQuery data source. A feature within the feature group points to a specific feature column within that data source. You can associate a feature view with multiple feature groups.

  - **Add features from a BigQuery source:** Directly associate a BigQuery data source, such as a BigQuery table or view, and specify at least one entity ID column.

After you create a feature view, Vertex AI Feature Store syncs the latest feature values from the BigQuery data source. If you set the query parameter `run_sync_immediately=true` , then Vertex AI Feature Store syncs the feature values when you create the feature view. Otherwise, Vertex AI Feature Store syncs the feature values according to the [sync](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/featurestore/latest/sync-data) schedule specified for the feature view.

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

## Sync feature data in a feature view

Vertex AI Feature Store can refresh or sync the feature values from the BigQuery data source to the feature view. You can specify the type of data sync for a feature view by using the [`FeatureView.sync_config`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.featureOnlineStores.featureViews#FeatureView.FIELDS.sync_config) parameter.

> **Note:** If your online store instance uses Bigtable online serving, the feature records that you delete from the BigQuery source table are retained in the corresponding feature views, even when you sync the data. To delete those feature records, you must [delete the feature view](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/featurestore/latest/delete-featureview) .

Vertex AI Feature Store supports the following types of data sync:

  - **Scheduled data sync** : You can specify the schedule or frequency for the data sync. You can choose this scheduled data sync for a feature view, regardless of the online serving type specified for the online store instance.
    
    If your feature view is configured to use scheduled data sync, you can optionally skip the wait until the next scheduled sync operation, by manually initiating the data sync. For more information about manually triggering a data sync, see [Sync feature data to online store](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/featurestore/latest/sync-data) .
    
    During online serving, if you want to serve only the latest feature values, including null values, you must use the following setup:
    
    1.  [Register your feature data source by creating a feature group](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/featurestore/latest/create-featuregroup) with the `dense` parameter set to `true` .
    
    2.  Choose Bigtable online serving when you [create the online store instance](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/featurestore/latest/create-onlinestore) .
    
    3.  Choose scheduled data sync when you create your feature views.

  - **Continuous data sync** : The feature data is refreshed whenever the feature data in the BigQuery data source is updated. You can choose this type of data sync for a feature view only if all of the following conditions are fulfilled:
    
      - The online store instance is configured for Bigtable online serving.
    
      - The feature view is associated with feature groups and feature resources.
    
      - The BigQuery data source is located in any of the following regions:
        
          - `eu`
        
          - `us`
        
          - `us-central1`
    
    Continuous data sync has the following limitations:
    
      - You can't update a feature view if you select continuous data sync for it.
    
      - Only new feature records are synced from the BigQuery data source. Continuous data sync doesn't sync feature records that you update or delete in BigQuery.
    
      - The feature group in the Feature Registry source must have a BigQuery table as its source.

### Optimize costs during scheduled data sync

A data sync operation might involve costs for BigQuery resource usage. Follow these guidelines to optimize these costs and improve performance during a data sync:

  - Don't configure the sync schedule to run more frequently than the frequency at which the data is expected to change in the BigQuery source.

  - Optimize the size of the feature data source in BigQuery. While creating the feature view, only include the data that you need for online serving.

  - Avoid running complex aggregations in BigQuery. Run a `SELECT *` query on the table or view to estimate the volume and duration of data processing.

  - While setting the scaling options for the online store, set `max_node_count` to a value that's high enough to cover high loads during a data sync.

  - Schedule the sync for different feature views at different times within the same online store.

  - If your BigQuery table contains extensive historical data, consider partitioning the table using timestamps and specify a time range for retrieving the feature data. This minimizes the retrieval of obsolete feature data during sync.

  - Bigtable utilization increases during data syncs. For feature views created within online stores for Bigtable online serving, schedule sync jobs during off-peak times for best performance.

## Configure the service account for a feature view

Each feature view uses a service account to access the source data in BigQuery during sync. Vertex AI Feature Store assigns the [BigQuery Data Viewer](https://docs.cloud.google.com/bigquery/docs/access-control#bigquery.dataViewer) Identity and Access Management (IAM) role to this service account.

By default, a feature view uses the service account configured for your project. With this configuration, any user with permission to create a feature view in your project can access the feature data in BigQuery.

Alternatively, you can configure the feature view to use its own service account. Vertex AI Feature Store then sets up a dedicated service account for the feature view. With this configuration, you can restrict access to feature data in BigQuery or grant access to additional users. You can specify the service account configuration by using the [`FeatureView.service_agent_type`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.featureOnlineStores.featureViews#FeatureView.FIELDS.service_agent_type) parameter. Note that Vertex AI Feature Store generates a unique service account email address for each feature view configured to have a dedicated service account.

If a feature view is configured to have a dedicated service account, you can view the service account email address in either of the following ways:

  - [Retrieve a list of all feature views within the online store instance](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/featurestore/latest/list-featureviews) by using the [featureViews.list](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.featureOnlineStores.featureViews/list) method.

  - Retrieve the details of the feature view by using the [featureViews.get](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.featureOnlineStores.featureViews/get) method.

## Configure vector retrieval for a feature view

> Gemini Enterprise Agent Platform Feature Store Optimized online serving is deprecated. Beginning on May 17, 2026, no new features will be added and only critical patches will be provided. On February 17, 2027, the capability will be fully sunset and APIs will no longer be available.
> 
> To improve latency and cost optimizations, migrate to [Bigtable online serving](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/featurestore/latest/online-serving-types#bigtable_serving) . To efficiently store and serve embeddings, use the purpose-built [Vector Search](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search/overview) .

You can configure vector retrieval for a feature view within an online store created for Optimized online serving by using the [`FeatureView.index_config`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.featureOnlineStores.featureViews#IndexConfig) parameter. For information about how to prepare or update the BigQuery data source to support embeddings by including the `embedding` column, see [Data source preparation guidelines](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/featurestore/latest/prepare-data-source#guidelines) .

Note that you can configure vector retrieval and manage embeddings only if the feature view is created by specifying a BigQuery source URI and not from feature groups and features from Feature Registry.

For more information about how to search for approximate nearest neighbors using embeddings in Vertex AI Feature Store, see [Search using embeddings](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/featurestore/latest/embeddings-search) .

## Create a feature view from feature groups

You can create a feature view based on feature data registered using feature groups and features. To associate multiple BigQuery data sources with the same feature view, you can specify multiple feature groups.

If you create a feature view by specifying feature groups and features:

  - Your data source must have a `feature_timestamp` column and can contain historical data.

  - Vertex AI Feature Store serves only the latest feature values based on the feature timestamp.

  - You can't configure embedding management for the feature view.

### Create a feature view with the default service account configuration

Use the following sample to create a feature view by associating multiple feature groups without specifying a service account configuration.

### REST

To create a [`FeatureView`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.featureOnlineStores.featureViews#resource:-featureView) resource, send a `POST` request by using the [featureViews.create](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.featureOnlineStores.featureViews/create) method.

Before using any of the request data, make the following replacements:

  - LOCATION\_ID : Region where you want to create the feature view, such as `us-central1` .
  - PROJECT\_ID : Your project ID.
  - FEATUREONLINESTORE\_NAME : The name of the online store instance where you want to create the feature view.
  - FEATUREVIEW\_NAME : The name of the new feature view instance that you want to create.
  - FEATUREGROUP\_NAME\_A and FEATUREGROUP\_NAME\_B : The names of the feature groups from which you want to add features to the feature view.
  - FEATURE\_ID\_A1 and FEATURE\_ID\_A2 : Feature IDs from the feature group FEATUREGROUP\_NAME\_A that you want to add to the feature view.
  - FEATURE\_ID\_B1 and FEATURE\_ID\_B2 : Feature IDs from the feature group FEATUREGROUP\_NAME\_B that you want to add to the feature view.
  - SYNC\_CONFIG : Enter one of the following sync configurations for the feature view:
      - To use scheduled data sync, provide the sync schedule in the following format:  
        `"cron": "cron_schedule_expression"`  
        Replace \`cron\_schedule\_expression\` with the cron schedule expression representing the frequency for syncing data to the feature view. For more information, see [cron](https://en.wikipedia.org/wiki/Cron) .
      - To use continuous data sync, enter the following:  
        `"continuous": true` You can use continuous data sync only if the online store instance containing the feature view is configured for Bigtable online serving.

HTTP method and URL:

    POST https://LOCATION_ID-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION_ID/featureOnlineStores/FEATUREONLINESTORE_NAME/featureViews?feature_view_id=FEATUREVIEW_NAME

Request JSON body:

    {
      "feature_registry_source": {
        "feature_groups": [
          {
            "feature_group_id": "FEATUREGROUP_NAME_A",
            "feature_ids": [ "FEATURE_ID_A1", "FEATURE_ID_A2" ]
          },
          {
            "feature_group_id": "FEATUREGROUP_NAME_B",
            "feature_ids": [ "FEATURE_ID_B1", "FEATURE_ID_B2" ]
          }
        ]
      },
      "sync_config": {
        SYNC_CONFIG
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
         "https://LOCATION_ID-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION_ID/featureOnlineStores/FEATUREONLINESTORE_NAME/featureViews?feature_view_id=FEATUREVIEW_NAME"

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
        -Uri "https://LOCATION_ID-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION_ID/featureOnlineStores/FEATUREONLINESTORE_NAME/featureViews?feature_view_id=FEATUREVIEW_NAME" | Select-Object -Expand Content

You should receive a JSON response similar to the following:

    {
      "name": "projects/PROJECT_NUMBER/locations/LOCATION_ID/featureOnlineStores/FEATUREONLINESTORE_NAME/featureViews/FEATUREVIEW_NAME/operations/OPERATION_ID",
      "metadata": {
        "@type": "type.googleapis.com/google.cloud.aiplatform.v1.CreateFeatureViewOperationMetadata",
        "genericMetadata": {
          "createTime": "2023-09-15T02:11:29.458820Z",
          "updateTime": "2023-09-15T02:11:29.458820Z"
        }
      }
    }

### Create a feature view that uses a dedicated service account

Use the following sample to create a feature view from feature groups by configuring a dedicated service account.

### REST

To create a [`FeatureView`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.featureOnlineStores.featureViews#resource:-featureView) resource, send a `POST` request by using the [featureViews.create](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.featureOnlineStores.featureViews/create) method.

Before using any of the request data, make the following replacements:

  - LOCATION\_ID : Region where you want to create the feature view, such as `us-central1` .
  - PROJECT\_ID : Your project ID.
  - FEATUREONLINESTORE\_NAME : The name of the online store instance where you want to create the feature view.
  - FEATUREVIEW\_NAME : The name of the new feature view instance that you want to create.
  - FEATUREGROUP\_NAME\_A and FEATUREGROUP\_NAME\_B : The names of the feature groups from which you want to add features to the feature view.
  - FEATURE\_ID\_A1 and FEATURE\_ID\_A2 : Feature IDs from the feature group FEATUREGROUP\_NAME\_A that you want to add to the feature view.
  - FEATURE\_ID\_B1 and FEATURE\_ID\_B2 : Feature IDs from the feature group FEATUREGROUP\_NAME\_B that you want to add to the feature view.
  - SYNC\_CONFIG : Enter one of the following sync configurations for the feature view:
      - To use scheduled data sync, provide the sync schedule in the following format:  
        `"cron": "cron_schedule_expression"`  
        Replace \`cron\_schedule\_expression\` with the cron schedule expression representing the frequency for syncing data to the feature view. For more information, see [cron](https://en.wikipedia.org/wiki/Cron) .
      - To use continuous data sync, enter the following:  
        `"continuous": true` You can use continuous data sync only if the online store instance containing the feature view is configured for Bigtable online serving.
  - SERVICE\_AGENT\_TYPE : Service account configuration for the feature view. To use a dedicated service account for the feature view, enter `SERVICE_AGENT_TYPE_FEATURE_VIEW` .

HTTP method and URL:

    POST https://LOCATION_ID-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION_ID/featureOnlineStores/FEATUREONLINESTORE_NAME/featureViews?feature_view_id=FEATUREVIEW_NAME

Request JSON body:

    {
      "feature_registry_source": {
        "feature_groups": [
          {
            "feature_group_id": "FEATUREGROUP_NAME_A",
            "feature_ids": [ "FEATURE_ID_A1", "FEATURE_ID_A2" ]
          },
          {
            "feature_group_id": "FEATUREGROUP_NAME_B",
            "feature_ids": [ "FEATURE_ID_B1", "FEATURE_ID_B2" ]
          }
        ]
      },
      "sync_config": {
        SYNC_CONFIG
      },
      "service_agent_type": "SERVICE_AGENT_TYPE",
    }

To send your request, choose one of these options:

#### curl

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) , or by using [Cloud Shell](https://docs.cloud.google.com/shell/docs) , which automatically logs you into the `gcloud` CLI . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Save the request body in a file named `request.json` , and execute the following command:

    curl -X POST \
         -H "Authorization: Bearer $(gcloud auth print-access-token)" \
         -H "Content-Type: application/json; charset=utf-8" \
         -d @request.json \
         "https://LOCATION_ID-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION_ID/featureOnlineStores/FEATUREONLINESTORE_NAME/featureViews?feature_view_id=FEATUREVIEW_NAME"

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
        -Uri "https://LOCATION_ID-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION_ID/featureOnlineStores/FEATUREONLINESTORE_NAME/featureViews?feature_view_id=FEATUREVIEW_NAME" | Select-Object -Expand Content

You should receive a JSON response similar to the following:

    {
      "name": "projects/PROJECT_NUMBER/locations/LOCATION_ID/featureOnlineStores/FEATUREONLINESTORE_NAME/featureViews/FEATUREVIEW_NAME/operations/OPERATION_ID",
      "metadata": {
        "@type": "type.googleapis.com/google.cloud.aiplatform.v1.CreateFeatureViewOperationMetadata",
        "genericMetadata": {
          "createTime": "2023-09-15T02:11:29.458820Z",
          "updateTime": "2023-09-15T02:11:29.458820Z"
        }
      }
    }

## Create a feature view from a BigQuery source

If you want to serve features online without registering your BigQuery data source using feature groups and features, you can create a feature view by specifying the URI of the BigQuery data source.

If you create a feature view by specifying the data source:

  - You can't include a `feature_timestamp` column in the BigQuery table or view.

  - You can't include historical feature values in the data source. Every row must contain a unique entity ID.

### Create a feature view that uses the default service account and doesn't support embeddings

Use the following samples to create a feature view that doesn't support embeddings, by directly associating a BigQuery data source and without specifying a service account configuration.

### Python

To learn how to install or update the Vertex AI SDK for Python, see [Install the Vertex AI SDK for Python](https://docs.cloud.google.com/vertex-ai/docs/start/use-vertex-ai-python-sdk) . For more information, see the [Python API reference documentation](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest) .

    from google.cloud import aiplatform
    from vertexai.resources.preview import feature_store
    from typing import List
    
    
    def create_feature_view_from_bq_source(
        project: str,
        location: str,
        existing_feature_online_store_id: str,
        feature_view_id: str,
        bq_table_uri: str,
        entity_id_columns: List[str],
    ):
        aiplatform.init(project=project, location=location)
        fos = feature_store.FeatureOnlineStore(existing_feature_online_store_id)
        fv = fos.create_feature_view(
            name=feature_view_id,
            source=feature_store.utils.FeatureViewBigQuerySource(
                uri=bq_table_uri, entity_id_columns=entity_id_columns
            ),
        )
        return fv

  - `project` : Your project ID.
  - `location` : Region where you want to create the feature view, such as `us-central1` .
  - `existing_feature_online_store_id` : The name of the online store instance where you want to create the feature view.
  - `feature_view_id` : The name of the new feature view instance that you want to create.
  - `bq_table_uri` : URI of the BigQuery source table or view.
  - `entity_id_columns` : The names of the columns containing the entity IDs. You can specify either one column or multiple columns.
      - To specify only one entity ID column, specify the column name in the following format:  
        `"entity_id_column_name"` .
      - To specify multiple entity ID columns, specify the column names in the following format:  
        `["entity_id_column_1_name", "entity_id_column_2_name", ...]` .

### REST

To create a [`FeatureView`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.featureOnlineStores.featureViews#resource:-featureView) resource, send a `POST` request by using the [featureViews.create](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.featureOnlineStores.featureViews/create) method.

Before using any of the request data, make the following replacements:

  - LOCATION\_ID : Region where you want to create the feature view, such as `us-central1` .
  - PROJECT\_ID : Your project ID.
  - FEATUREONLINESTORE\_NAME : The name of the online store instance where you want to create the feature view.
  - FEATUREVIEW\_NAME : The name of the new feature view that you want to create.
  - PROJECT\_NAME : Your project name.
  - DATASET\_NAME : Your BigQuery dataset name.
  - TABLE\_NAME : The name of the table from your BigQuery dataset.
  - ENTITY\_ID\_COLUMNS : The names of the column(s) containing the entity IDs. You can specify either one column or multiple columns.
      - To specify only one entity ID column, specify the column name in the following format:  
        `"entity_id_column_name"`
      - To specify multiple entity ID columns, specify the column names in the following format:  
        `["entity_id_column_1_name", "entity_id_column_2_name", ...]`
  - CRON : Cron schedule expression representing the frequency for syncing data to the feature view. For more information, see [cron](https://en.wikipedia.org/wiki/Cron) .

HTTP method and URL:

    POST https://LOCATION_ID-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION_ID/featureOnlineStores/FEATUREONLINESTORE_NAME/featureViews?feature_view_id=FEATUREVIEW_NAME

Request JSON body:

    {
      "big_query_source": {
        "uri": "bq://PROJECT_NAME.DATASET_NAME.TABLE_NAME",
        "entity_id_columns": "ENTITY_ID_COLUMNS"
      },
      "sync_config": {
        "cron": "CRON"
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
         "https://LOCATION_ID-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION_ID/featureOnlineStores/FEATUREONLINESTORE_NAME/featureViews?feature_view_id=FEATUREVIEW_NAME"

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
        -Uri "https://LOCATION_ID-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION_ID/featureOnlineStores/FEATUREONLINESTORE_NAME/featureViews?feature_view_id=FEATUREVIEW_NAME" | Select-Object -Expand Content

You should receive a JSON response similar to the following:

    {
      "name": "projects/PROJECT_NUMBER/locations/LOCATION_ID/featureOnlineStores/FEATUREONLINESTORE_NAME/featureViews/FEATUREVIEW_NAME/operations/OPERATION_ID",
      "metadata": {
        "@type": "type.googleapis.com/google.cloud.aiplatform.v1.CreateFeatureViewOperationMetadata",
        "genericMetadata": {
          "createTime": "2023-09-15T02:11:29.458820Z",
          "updateTime": "2023-09-15T02:11:29.458820Z"
        }
      }
    }

### Create a feature view that uses the default service account and supports embeddings

Use the following samples to create a feature view with embedding support by directly associating a BigQuery data source and with the default service account configuration.

### Python

To learn how to install or update the Vertex AI SDK for Python, see [Install the Vertex AI SDK for Python](https://docs.cloud.google.com/vertex-ai/docs/start/use-vertex-ai-python-sdk) . For more information, see the [Python API reference documentation](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest) .

    from google.cloud import aiplatform
    from vertexai.resources.preview import feature_store
    from typing import List
    
    
    def create_feature_view_from_bq_source_with_embedding_management(
        project: str,
        location: str,
        existing_feature_online_store_id: str,
        feature_view_id: str,
        bq_table_uri: str,
        entity_id_columns: List[str],
        embedding_column: str,
        embedding_dimensions: int,
    ):
        aiplatform.init(project=project, location=location)
    
        fos = feature_store.FeatureOnlineStore(existing_feature_online_store_id)
    
        bigquery_source = feature_store.utils.FeatureViewBigQuerySource(
            uri=bq_table_uri,
            entity_id_columns=entity_id_columns,
        )
        index_config = feature_store.utils.IndexConfig(
            embedding_column=embedding_column,
            dimensions=embedding_dimensions,
            algorithm_config=feature_store.utils.TreeAhConfig(),
        )
        fv = fos.create_feature_view(
            name=feature_view_id,
            source=bigquery_source,
            index_config=index_config,
        )
        return fv

  - `project` : Your project ID.
  - `location` : Region where you want to create the feature view, such as `us-central1` .
  - `existing_feature_online_store_id` : The name of the online store instance where you want to create the feature view.
  - `feature_view_id` : The name of the new feature view instance that you want to create.
  - `bq_table_uri` : URI of the BigQuery source table or view.
  - `entity_id_columns` : The names of the columns containing the entity IDs. You can specify either one column or multiple columns.
      - To specify only one entity ID column, specify the column name in the following format:  
        `"entity_id_column_name"` .
      - To specify multiple entity ID columns, specify the column names in the following format:  
        `["entity_id_column_1_name", "entity_id_column_2_name", ...]` .
  - `embedding_column` : The name of the column containing the source data to create the index for vector search. This is required only if you want to manage embeddings with the feature view.
  - `embedding_dimensions` : Optional. The size, expressed as number of dimensions, of an embedding in the embedding column.

### REST

To create a [`FeatureView`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.featureOnlineStores.featureViews#resource:-featureView) resource, send a `POST` request by using the [featureViews.create](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.featureOnlineStores.featureViews/create) method.

Before using any of the request data, make the following replacements:

  - LOCATION\_ID : Region where you want to create the feature view, such as `us-central1` .
  - PROJECT\_ID : Your project ID.
  - FEATUREONLINESTORE\_NAME : The name of the online store instance where you want to create the feature view.
  - FEATUREVIEW\_NAME : The name of the new feature view that you want to create.
  - PROJECT\_NAME : Your project name.
  - DATASET\_NAME : Your BigQuery dataset name.
  - TABLE\_NAME : The name of the table from your BigQuery dataset.
  - ENTITY\_ID\_COLUMNS : The names of the column(s) containing the entity IDs. You can specify either one column or multiple columns.
      - To specify only one entity ID column, specify the column name in the following format:  
        `"entity_id_column_name"`
      - To specify multiple entity ID columns, specify the column names in the following format:  
        `["entity_id_column_1_name", "entity_id_column_2_name", ...]`
  - CRON : Cron schedule expression representing the frequency for syncing data to the feature view. For more information, see [cron](https://en.wikipedia.org/wiki/Cron) .
  - EMBEDDING\_COLUMN : The name of the column containing the source data to create the index for vector search. This is required only if you want to manage embeddings with the feature view.
  - FILTER\_COLUMN\_1 and FILTER\_COLUMN\_2 : Optional: The names of the columns used to filter the vector search results.
  - CROWDING\_COLUMN : Optional: The name of the column containing the crowding attributes.
  - EMBEDDING\_DIMENSION : Optional: The size, expressed as number of dimensions, of an embedding in the embedding column.

HTTP method and URL:

    POST https://LOCATION_ID-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION_ID/featureOnlineStores/FEATUREONLINESTORE_NAME/featureViews?feature_view_id=FEATUREVIEW_NAME

Request JSON body:

    {
      "big_query_source": {
        "uri": "bq://PROJECT_NAME.DATASET_NAME.TABLE_NAME",
        "entity_id_columns": "ENTITY_ID_COLUMNS"
      },
      "sync_config": {
        "cron": "CRON"
      },
      "index_config": {
        "embedding_column": "EMBEDDING_COLUMN",
        "filter_columns": ["FILTER_COLUMN_1", "FILTER_COLUMN_2"],
        "crowding_column": "CROWDING_COLUMN",
        "embedding_dimension": EMBEDDING_DIMENSION
        "tree_ah_config": {}
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
         "https://LOCATION_ID-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION_ID/featureOnlineStores/FEATUREONLINESTORE_NAME/featureViews?feature_view_id=FEATUREVIEW_NAME"

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
        -Uri "https://LOCATION_ID-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION_ID/featureOnlineStores/FEATUREONLINESTORE_NAME/featureViews?feature_view_id=FEATUREVIEW_NAME" | Select-Object -Expand Content

You should receive a JSON response similar to the following:

    {
      "name": "projects/PROJECT_NUMBER/locations/LOCATION_ID/featureOnlineStores/FEATUREONLINESTORE_NAME/featureViews/FEATUREVIEW_NAME/operations/OPERATION_ID",
      "metadata": {
        "@type": "type.googleapis.com/google.cloud.aiplatform.v1.CreateFeatureViewOperationMetadata",
        "genericMetadata": {
          "createTime": "2023-09-15T02:11:29.458820Z",
          "updateTime": "2023-09-15T02:11:29.458820Z"
        }
      }
    }

### Create a feature view with a dedicated service account and without embedding management

Use the following sample to create a feature view without embedding support by directly associating a BigQuery data source and specifying a service account configuration.

### REST

To create a [`FeatureView`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.featureOnlineStores.featureViews#resource:-featureView) resource with embeddings support, send a `POST` request by using the [featureViews.create](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.featureOnlineStores.featureViews/create) method and specifying the [`FeatureView.index_config`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.featureOnlineStores.featureViews#IndexConfig) parameter. Note that you can use embedding management only if the online store is configured for Optimized online serving.

Before using any of the request data, make the following replacements:

  - LOCATION\_ID : Region where you want to create the feature view, such as `us-central1` .
  - PROJECT\_ID : Your project ID.
  - FEATUREONLINESTORE\_NAME : The name of the online store instance where you want to create the feature view.
  - FEATUREVIEW\_NAME : The name of the new feature view that you want to create.
  - PROJECT\_NAME : Your project name.
  - DATASET\_NAME : Your BigQuery dataset name.
  - TABLE\_NAME : The name of the table from your BigQuery dataset.
  - ENTITY\_ID\_COLUMNS : The names of the column(s) containing the entity IDs. You can specify either one column or multiple columns.
      - To specify only one entity ID column, specify the column name in the following format:  
        `"entity_id_column_name"`
      - To specify multiple entity ID columns, specify the column names in the following format:  
        `["entity_id_column_1_name", "entity_id_column_2_name", ...]`
  - CRON : Cron schedule expression representing the frequency for syncing data to the feature view. For more information, see [cron](https://en.wikipedia.org/wiki/Cron) .
  - SERVICE\_AGENT\_TYPE : Service account configuration for the feature view. To use a dedicated service account for the feature view, enter `SERVICE_AGENT_TYPE_FEATURE_VIEW` .

HTTP method and URL:

    POST https://LOCATION_ID-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION_ID/featureOnlineStores/FEATUREONLINESTORE_NAME/featureViews?feature_view_id=FEATUREVIEW_NAME

Request JSON body:

    {
      "big_query_source": {
        "uri": "bq://PROJECT_NAME.DATASET_NAME.TABLE_NAME",
        "entity_id_columns": "ENTITY_ID_COLUMNS"
      },
      "sync_config": {
        "cron": "CRON"
      },
      "service_agent_type": "SERVICE_AGENT_TYPE",
    }

To send your request, choose one of these options:

#### curl

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) , or by using [Cloud Shell](https://docs.cloud.google.com/shell/docs) , which automatically logs you into the `gcloud` CLI . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Save the request body in a file named `request.json` , and execute the following command:

    curl -X POST \
         -H "Authorization: Bearer $(gcloud auth print-access-token)" \
         -H "Content-Type: application/json; charset=utf-8" \
         -d @request.json \
         "https://LOCATION_ID-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION_ID/featureOnlineStores/FEATUREONLINESTORE_NAME/featureViews?feature_view_id=FEATUREVIEW_NAME"

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
        -Uri "https://LOCATION_ID-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION_ID/featureOnlineStores/FEATUREONLINESTORE_NAME/featureViews?feature_view_id=FEATUREVIEW_NAME" | Select-Object -Expand Content

You should receive a JSON response similar to the following:

    {
      "name": "projects/PROJECT_NUMBER/locations/LOCATION_ID/featureOnlineStores/FEATUREONLINESTORE_NAME/featureViews/FEATUREVIEW_NAME/operations/OPERATION_ID",
      "metadata": {
        "@type": "type.googleapis.com/google.cloud.aiplatform.v1.CreateFeatureViewOperationMetadata",
        "genericMetadata": {
          "createTime": "2023-09-15T02:11:29.458820Z",
          "updateTime": "2023-09-15T02:11:29.458820Z"
        }
      }
    }

### Create a feature view with embedding management and a dedicated service account

Use the following sample to create a feature view with embedding support by directly associating a BigQuery data source and specifying a service account configuration.

### REST

To create a [`FeatureView`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.featureOnlineStores.featureViews#resource:-featureView) resource with embeddings support, send a `POST` request by using the [featureViews.create](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.featureOnlineStores.featureViews/create) method and specifying the [`FeatureView.index_config`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.featureOnlineStores.featureViews#IndexConfig) parameter. Note that you can use embedding management only if the online store is configured for Optimized online serving.

Before using any of the request data, make the following replacements:

  - LOCATION\_ID : Region where you want to create the feature view, such as `us-central1` .
  - PROJECT\_ID : Your project ID.
  - FEATUREONLINESTORE\_NAME : The name of the online store instance where you want to create the feature view.
  - FEATUREVIEW\_NAME : The name of the new feature view that you want to create.
  - PROJECT\_NAME : Your project name.
  - DATASET\_NAME : Your BigQuery dataset name.
  - TABLE\_NAME : The name of the table from your BigQuery dataset.
  - ENTITY\_ID\_COLUMNS : The names of the column(s) containing the entity IDs. You can specify either one column or multiple columns.
      - To specify only one entity ID column, specify the column name in the following format:  
        `"entity_id_column_name"`
      - To specify multiple entity ID columns, specify the column names in the following format:  
        `["entity_id_column_1_name", "entity_id_column_2_name", ...]`
  - CRON : Cron schedule expression representing the frequency for syncing data to the feature view. For more information, see [cron](https://en.wikipedia.org/wiki/Cron) .
  - SERVICE\_AGENT\_TYPE : Service account configuration for the feature view. To use a dedicated service account for the feature view, enter `SERVICE_AGENT_TYPE_FEATURE_VIEW` .
  - EMBEDDING\_COLUMN : The name of the column containing the source data to create the index for vector search. This is required only if you want to manage embeddings with the feature view.
  - FILTER\_COLUMN\_1 and FILTER\_COLUMN\_2 : Optional: The names of the columns used to filter the vector search results.
  - CROWDING\_COLUMN : Optional: The name of the column containing the crowding attributes.
  - EMBEDDING\_DIMENSION : Optional: The size, expressed as number of dimensions, of an embedding in the embedding column.

HTTP method and URL:

    POST https://LOCATION_ID-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION_ID/featureOnlineStores/FEATUREONLINESTORE_NAME/featureViews?feature_view_id=FEATUREVIEW_NAME

Request JSON body:

    {
      "big_query_source": {
        "uri": "bq://PROJECT_NAME.DATASET_NAME.TABLE_NAME",
        "entity_id_columns": "ENTITY_ID_COLUMNS"
      },
      "sync_config": {
        "cron": "CRON"
      },
      "service_agent_type": "SERVICE_AGENT_TYPE",
      "index_config": {
        "embedding_column": "EMBEDDING_COLUMN",
        "filter_columns": ["FILTER_COLUMN_1", "FILTER_COLUMN_2"],
        "crowding_column": "CROWDING_COLUMN",
        "embedding_dimension": EMBEDDING_DIMENSION
        "tree_ah_config": {}
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
         "https://LOCATION_ID-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION_ID/featureOnlineStores/FEATUREONLINESTORE_NAME/featureViews?feature_view_id=FEATUREVIEW_NAME"

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
        -Uri "https://LOCATION_ID-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION_ID/featureOnlineStores/FEATUREONLINESTORE_NAME/featureViews?feature_view_id=FEATUREVIEW_NAME" | Select-Object -Expand Content

You should receive a JSON response similar to the following:

    {
      "name": "projects/PROJECT_NUMBER/locations/LOCATION_ID/featureOnlineStores/FEATUREONLINESTORE_NAME/featureViews/FEATUREVIEW_NAME/operations/OPERATION_ID",
      "metadata": {
        "@type": "type.googleapis.com/google.cloud.aiplatform.v1.CreateFeatureViewOperationMetadata",
        "genericMetadata": {
          "createTime": "2023-09-15T02:11:29.458820Z",
          "updateTime": "2023-09-15T02:11:29.458820Z"
        }
      }
    }

## What's next

  - Learn how to [serve features online](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/featurestore/latest/serve-feature-values) .

  - Learn how to [update a feature view](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/featurestore/latest/update-featureview) .

  - Learn how to [delete a feature view](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/featurestore/latest/delete-featureview) .
