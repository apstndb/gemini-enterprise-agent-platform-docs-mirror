---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/featurestore/latest/serve-feature-values
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/featurestore/latest/serve-feature-values
title: Serve features from online store
description: Learn how to fetch feature values from a feature view for real-time predictions using Bigtable online serving or Optimized online serving in Vertex AI Feature Store.
data_source: docs.cloud.google.com
---

Vertex AI Feature Store lets you online serve feature values in real-time from a feature view within an online store. For example, you can serve feature values from a feature view for online predictions. A feature view must be synced at least once before you can online serve features from that feature.

If the feature view is defined based on feature groups and features, Vertex AI Feature Store fetches the latest feature values corresponding to a specific entity ID. If there are multiple records with the same value in the ID column, Vertex AI Feature Store fetches the most recent non-null feature values, based on the `feature_timestamp` column.

If the feature view is directly associated with a BigQuery data source without associating feature groups and features, then Vertex AI Feature Store fetches all the feature values from the data source. In this case, every row in the data source must contain a unique ID.

Depending on the type of online serving configured for your online store, you can serve feature values in one of the following ways:

  - [Fetch feature values using Bigtable online serving](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/featurestore/latest/serve-feature-values#bigtable_serving) : Choose this option only if the online store is configured for Bigtable online serving.

  - [Fetch feature values using Optimized online serving (Deprecated) with a public endpoint](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/featurestore/latest/serve-feature-values#optimized_serving_public) : Choose this option only if the online store is configured for Optimized online serving ( [Deprecated](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/deprecations) ) from a public endpoint.

  - [Fetch feature values using Optimized online serving (Deprecated) with a Private Service Connect endpoint](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/featurestore/latest/serve-feature-values#optimized_serving_private) : Choose this option only if the online store is configured for Optimized online serving ( [Deprecated](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/deprecations) ) from a dedicated serving endpoint over Private Service Connect.

## Before you begin

Authenticate to Gemini Enterprise Agent Platform, unless you've done so already.

Select the tab for how you plan to use the samples on this page:

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

## Fetch feature values using Bigtable online serving

You can use Bigtable online serving to do the following:

  - [Fetch feature values by specifying a single entity ID](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/featurestore/latest/serve-feature-values#bigtable_single_entity)

  - [Fetch feature values for a set of entities](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/featurestore/latest/serve-feature-values#bigtable_multiple_entities) (preview)

### Fetch feature values for a single entity

If your feature view has only one entity ID column, then you can serve features by specifying the value contained in that column. However, if the feature view has multiple entity ID columns, then you can locate a feature record by specifying the values in those columns to constitute the entity ID that's unique to the feature record.

#### Fetch feature values from a feature view with only one entity ID column

Use the following samples to fetch feature values for a specific entity ID, where the feature view has only one entity ID column.

### REST

To fetch all the latest feature values for a specific entity ID from a [`FeatureView`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.featureOnlineStores.featureViews#resource:-featureView) instance, send a `POST` request by using the [featureViews.fetchFeatureValues](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.featureOnlineStores.featureViews/fetchFeatureValues) method.

Before using any of the request data, make the following replacements:

  - LOCATION\_ID : Region where the online store is located, such as `us-central1` .
  - PROJECT\_ID : Your project ID.
  - FEATUREONLINESTORE\_NAME : The name of the online store containing the feature view.
  - FEATUREVIEW\_NAME : The name of the feature view from which you want to serve feature values.
  - ENTITY\_ID : The value of the ID column in the feature record from which you want to serve the latest feature values.
  - FORMAT : Optional: The format in which you want to fetch the feature values. The following formats are supported:
      - `KEY_VALUE`
      - `PROTO_STRUCT`

HTTP method and URL:

    POST https://LOCATION_ID-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION_ID/featureOnlineStores/FEATUREONLINESTORE_NAME/featureViews/FEATUREVIEW_NAME:fetchFeatureValues

Request JSON body:

    {
      data_key: { key: "ENTITY_ID" },
      data_format: "FORMAT"
    }

To send your request, choose one of these options:

#### curl

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) , or by using [Cloud Shell](https://docs.cloud.google.com/shell/docs) , which automatically logs you into the `gcloud` CLI . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Save the request body in a file named `request.json` , and execute the following command:

    curl -X POST \
         -H "Authorization: Bearer $(gcloud auth print-access-token)" \
         -H "Content-Type: application/json; charset=utf-8" \
         -d @request.json \
         "https://LOCATION_ID-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION_ID/featureOnlineStores/FEATUREONLINESTORE_NAME/featureViews/FEATUREVIEW_NAME:fetchFeatureValues"

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
        -Uri "https://LOCATION_ID-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION_ID/featureOnlineStores/FEATUREONLINESTORE_NAME/featureViews/FEATUREVIEW_NAME:fetchFeatureValues" | Select-Object -Expand Content

You should receive a JSON response similar to the following:

    key_values {
      features {
        value {
          int64_value: 258348
        }
        name: "feature_0"
      }
      features {
        value {
          double_value: 0.96300036744534068
        }
        name: "feature_1"
      }
      features {
        value {
          double_value: 0.42787383695351083
        }
        name: "feature_2"
      }
      features {
        value {
          double_value: 0.12219888824743128
        }
        name: "feature_3"
      }
      features {
        value {
          double_value: 0.037523154697944622
        }
        name: "feature_4"
      }
      features {
        value {
          double_value: 0.1766952509448767
        }
        name: "feature_5"
      }
    }

### Python

> **Note:** You'll need to install or upgrade to the latest version of the Python SDK to complete this step. To do this, run the following command:  
> `pip3 install --upgrade --quiet google-cloud-aiplatform` .  
> To learn more about online serving using the Python SDK, see the [Online feature serving and fetching of BigQuery data with Bigtable online serving notebook tutorial](https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/feature_store/online_feature_serving_and_fetching_bigquery_data_with_feature_store_bigtable.ipynb)

Use the following sample to fetch feature values based on a specific entity ID using Bigtable online serving.

    from google.cloud import aiplatform
    from vertexai.resources.preview.feature_store import FeatureOnlineStore, FeatureView
    
    aiplatform.init(project="PROJECT_ID", location="LOCATION_ID")
    fos = FeatureOnlineStore("FEATUREONLINESTORE_NAME")
    fv = FeatureView("FEATUREVIEW_NAME", feature_online_store_id=fos.name)
    fv.read("ENTITY_ID")

Replace the following:

  - LOCATION\_ID : Region where the online store is located, such as `us-central1` .

  - PROJECT\_ID : Your project ID.

  - FEATUREONLINESTORE\_NAME : The name of the online store containing the feature view.

  - FEATUREVIEW\_NAME : The name of the feature view from which you want to serve feature values.

  - ENTITY\_ID : The value of the ID column for which you want to serve the latest feature values.

  - FORMAT : Optional: The format in which you want to fetch the feature values. Supported formats include JSON `KEY_VALUE` pair and proto `PROTO_STRUCT` formats.

#### Fetch feature values from a feature view with multiple entity ID columns

Use the following samples to fetch feature values for a specific entity ID, where the feature view has multiple entity ID columns.

### REST

To fetch all the latest feature values for a specific entity ID from a [`FeatureView`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.featureOnlineStores.featureViews#resource:-featureView) instance, send a `POST` request by using the [featureViews.fetchFeatureValues](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.featureOnlineStores.featureViews/fetchFeatureValues) method.

Before using any of the request data, make the following replacements:

  - LOCATION\_ID : Region where the online store is located, such as `us-central1` .
  - PROJECT\_ID : Your project ID.
  - FEATUREONLINESTORE\_NAME : The name of the online store containing the feature view.
  - FEATUREVIEW\_NAME : The name of the feature view from which you want to serve feature values.
  - ENTITY\_ID\_PART\_1 , ENTITY\_ID\_PART\_2 , and ENTITY\_ID\_PART\_3 : The parts of the entity ID in the entity ID columns configured for the feature view. These parts constitute the unique entity ID for the feature record.
  - FORMAT : Optional: The format in which you want to fetch the feature values. The following formats are supported:
      - `KEY_VALUE`
      - `PROTO_STRUCT`

HTTP method and URL:

    POST https://LOCATION_ID-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION_ID/featureOnlineStores/FEATUREONLINESTORE_NAME/featureViews/FEATUREVIEW_NAME:fetchFeatureValues

Request JSON body:

    {
      data_key: { composite_key: { parts: ["ENTITY_ID_PART_1", "ENTITY_ID_PART_2", "ENTITY_ID_PART_3"] } },
      data_format: "FORMAT"
    }

To send your request, choose one of these options:

#### curl

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) , or by using [Cloud Shell](https://docs.cloud.google.com/shell/docs) , which automatically logs you into the `gcloud` CLI . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Save the request body in a file named `request.json` , and execute the following command:

    curl -X POST \
         -H "Authorization: Bearer $(gcloud auth print-access-token)" \
         -H "Content-Type: application/json; charset=utf-8" \
         -d @request.json \
         "https://LOCATION_ID-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION_ID/featureOnlineStores/FEATUREONLINESTORE_NAME/featureViews/FEATUREVIEW_NAME:fetchFeatureValues"

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
        -Uri "https://LOCATION_ID-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION_ID/featureOnlineStores/FEATUREONLINESTORE_NAME/featureViews/FEATUREVIEW_NAME:fetchFeatureValues" | Select-Object -Expand Content

You should receive a JSON response similar to the following:

    key_values {
      features {
        value {
          int64_value: 258348
        }
        name: "feature_0"
      }
      features {
        value {
          double_value: 0.96300036744534068
        }
        name: "feature_1"
      }
      features {
        value {
          double_value: 0.42787383695351083
        }
        name: "feature_2"
      }
      features {
        value {
          double_value: 0.12219888824743128
        }
        name: "feature_3"
      }
      features {
        value {
          double_value: 0.037523154697944622
        }
        name: "feature_4"
      }
      features {
        value {
          double_value: 0.1766952509448767
        }
        name: "feature_5"
      }
    }

### Python

> **Note:** You'll need to install or upgrade to the latest version of the Python SDK to complete this step. To do this, run the following command:  
> `pip3 install --upgrade --quiet google-cloud-aiplatform` .  
> To learn more about online serving using the Python SDK, see the [Online feature serving and fetching of BigQuery data with Bigtable online serving notebook tutorial](https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/feature_store/online_feature_serving_and_fetching_bigquery_data_with_feature_store_bigtable.ipynb)

Use the following sample to fetch feature values based on a specific entity ID using Bigtable online serving.

    from google.cloud import aiplatform
    from vertexai.resources.preview.feature_store import FeatureOnlineStore, FeatureView
    
    aiplatform.init(project="PROJECT_ID", location="LOCATION_ID")
    fos = FeatureOnlineStore("FEATUREONLINESTORE_NAME")
    fv = FeatureView("FEATUREVIEW_NAME", feature_online_store_id=fos.name)
    fv.read(["ENTITY_ID_PART_1", "ENTITY_ID_PART_2", "ENTITY_ID_PART_3"])

Replace the following:

  - LOCATION\_ID : Region where the online store is located, such as `us-central1` .

  - PROJECT\_ID : Your project ID.

  - FEATUREONLINESTORE\_NAME : The name of the online store containing the feature view.

  - FEATUREVIEW\_NAME : The name of the feature view from which you want to serve feature values.

  - ENTITY\_ID\_PART\_1 , ENTITY\_ID\_PART\_2 , and ENTITY\_ID\_PART\_3 : The parts of the entity ID in the entity ID columns configured for the feature view. These parts constitute the unique entity ID for the feature record.

  - FORMAT : Optional: The format in which you want to fetch the feature values. Supported formats include JSON `KEY_VALUE` pair and proto `PROTO_STRUCT` formats.

### Fetch feature values for a set of entities

> **Preview**
> 
> This feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](https://docs.cloud.google.com/terms/service-terms#1) . Pre-GA features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

Use the following sample to fetch feature values by specifying a set of IDs from multiple entity ID columns using Bigtable online serving.

### REST

To fetch all the latest feature values for a specific entity ID from a [`FeatureView`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.featureOnlineStores.featureViews#resource:-featureView) instance, send a `POST` request by using the [featureViews.streamingFetchFeatureValues](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.featureOnlineStores.featureViews/streamingFetchFeatureValues) method.

Before using any of the request data, make the following replacements:

  - LOCATION\_ID : Region where the online store is located, such as `us-central1` .
  - PROJECT\_ID : Your project ID.
  - FEATUREONLINESTORE\_NAME : The name of the online store containing the feature view.
  - FEATUREVIEW\_NAME : The name of the feature view from which you want to serve feature values.
  - ENTITY\_ID\_1 , ENTITY\_ID\_2 , ENTITY\_ID\_3 , and ENTITY\_ID\_4 : The set of values from the ID columns in the feature records from which you want to serve the latest feature values. Note that grouping the entity IDs as multiple nested lists in a request can help reduce latency, as Vertex AI Feature Store performs a separate read operation for each nested list of IDs.

HTTP method and URL:

    POST https://LOCATION_ID-aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/LOCATION_ID/featureOnlineStores/FEATUREONLINESTORE_NAME/featureViews/FEATUREVIEW_NAME:streamingFetchFeatureValues

Request JSON body:

    [
      {
        data_keys: [{key: "ENTITY_ID_1"}, {key: "ENTITY_ID_2"}],
        feature_view: "projects/PROJECT_ID/locations/LOCATION_ID/featureOnlineStores/FEATUREONLINESTORE_NAME/featureViews/FEATUREVIEW_NAME"
      },
      {
        data_keys: [{key: "ENTITY_ID_3"}, {key: "ENTITY_ID_4"}],
        feature_view: "projects/PROJECT_ID/locations/LOCATION_ID/featureOnlineStores/FEATUREONLINESTORE_NAME/featureViews/FEATUREVIEW_NAME"
      }
    ]

To send your request, choose one of these options:

#### curl

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) , or by using [Cloud Shell](https://docs.cloud.google.com/shell/docs) , which automatically logs you into the `gcloud` CLI . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Save the request body in a file named `request.json` , and execute the following command:

    curl -X POST \
         -H "Authorization: Bearer $(gcloud auth print-access-token)" \
         -H "Content-Type: application/json; charset=utf-8" \
         -d @request.json \
         "https://LOCATION_ID-aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/LOCATION_ID/featureOnlineStores/FEATUREONLINESTORE_NAME/featureViews/FEATUREVIEW_NAME:streamingFetchFeatureValues"

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
        -Uri "https://LOCATION_ID-aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/LOCATION_ID/featureOnlineStores/FEATUREONLINESTORE_NAME/featureViews/FEATUREVIEW_NAME:streamingFetchFeatureValues" | Select-Object -Expand Content

You should receive a JSON response similar to the following:

    [data {
      key_values {
        features {
          name: "movies"
          value {
            string_value: "movie_04"
          }
        }
        features {
          name: "feature_timestamp"
          value {
            int64_value: 1631694494000000
          }
        }
      }
      data_key {
        key: "eve"
      }
    }
    , data {
      key_values {
        features {
          name: "movies"
          value {
            string_value: "movie_03"
          }
        }
        features {
          name: "feature_timestamp"
          value {
            int64_value: 1631612115000000
          }
        }
      }
      data_key {
        key: "alice"
      }
    }
    data {
      key_values {
        features {
          name: "movies"
          value {
            string_value: "movie_02"
          }
        }
        features {
          name: "feature_timestamp"
          value {
            int64_value: 1631694494000000
          }
        }
      }
      data_key {
        key: "bob"
      }
    }
    ]

### Python

> **Note:** You'll need to install or upgrade to the latest version of the Python SDK to complete this step. To do this, run the following command:  
> `pip3 install --upgrade --quiet google-cloud-aiplatform` .  
> To learn more about online serving features from multiple entities using the Python SDK, see the [Fetch multiple entities notebook tutorial](https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/feature_store/online_feature_serving_fetching_multiple_entities.ipynb)

Use the following sample to fetch feature values from multiple entity ID columns using Bigtable online serving.

    from google.cloud.aiplatform_v1beta1 import FeatureOnlineStoreServiceClient
    from google.cloud.aiplatform_v1beta1.types import feature_online_store_service as feature_online_store_service_pb2
    
    data_client = FeatureOnlineStoreServiceClient(
      client_options={"api_endpoint": f"LOCATION_ID-aiplatform.googleapis.com"}
    )
    
    feature_view = "projects/PROJECT_ID/locations/LOCATION_ID/featureOnlineStores/FEATUREONLINESTORE_NAME/featureViews/FEATUREVIEW_NAME"
    
    keys_list=[
        ["ENTITY_ID_1","ENTITY_ID_2"],
        ["ENTITY_ID_3","ENTITY_ID_4"]
      ]
    
    requests = []
    
    for keys in keys_list:
      requests.append(
        feature_online_store_service_pb2.StreamingFetchFeatureValuesRequest(
          feature_view=feature_view,
          data_keys=[
              feature_online_store_service_pb2.FeatureViewDataKey(key=key)
              for key in keys
          ]
        )
      )
    
    responses = data_client.streaming_fetch_feature_values(
        requests=iter(requests)
    )
    responses = [response for response in responses]

Replace the following:

  - LOCATION\_ID : Region where the online store is located, such as `us-central1` .

  - PROJECT\_ID : Your project ID.

  - FEATUREONLINESTORE\_NAME : The name of the online store containing the feature view.

  - FEATUREVIEW\_NAME : The name of the feature view from which you want to serve feature values.

  - ENTITY\_ID\_1 , ENTITY\_ID\_2 , ENTITY\_ID\_3 , and ENTITY\_ID\_4 : The entity IDs from which you want to serve the latest feature values. Note that grouping the entity IDs as multiple nested lists in a request can help reduce latency, as Vertex AI Feature Store performs a separate read operation for each nested list of IDs.

## Fetch feature values using Optimized online serving from a public endpoint

> Gemini Enterprise Agent Platform Feature Store Optimized online serving is deprecated. Beginning on May 17, 2026, no new features will be added and only critical patches will be provided. On February 17, 2027, the capability will be fully sunset and APIs will no longer be available.
> 
> To improve latency and cost optimizations, migrate to [Bigtable online serving](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/featurestore/latest/online-serving-types#bigtable_serving) . To efficiently store and serve embeddings, use the purpose-built [Vector Search](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search/overview) .

If you've configured your online store instance to serve feature values using Optimized online serving from a public endpoint, then you need to perform the following steps to fetch feature values from a feature view within the online store:

1.  [Retrieve the public endpoint domain name for the `FeatureOnlineStore` instance.](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/featurestore/latest/serve-feature-values#lowlatency_public_step1)

2.  [Fetch feature values from an entity ID using the public endpoint domain name.](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/featurestore/latest/serve-feature-values#lowlatency_public_step2)

### Retrieve the public endpoint domain name for the online store

When you create and configure an online store instance for Optimized online serving with a public endpoint, Vertex AI Feature Store generates the public endpoint domain name for the online store. Before you can start serving feature values from a feature view in the online store, you need to retrieve the public endpoint domain name from the online store details.

Use the following sample to retrieve the details of an online store instance.

### REST

To retrieve the details of a [`FeatureOnlineStore`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.featureOnlineStores#resource:-featureOnlineStore) resource in your project, send a `GET` request by using the [`featureOnlineStores.get`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.featureOnlineStores/get) method.

Before using any of the request data, make the following replacements:

  - LOCATION\_ID : Region where the online store is located, such as `us-central1` .
  - PROJECT\_ID : Your project ID.
  - FEATUREONLINESTORE\_NAME : The name of the online store instance.

HTTP method and URL:

    GET https://LOCATION_ID-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION_ID/featureOnlineStores/FEATUREONLINESTORE_NAME

To send your request, choose one of these options:

#### curl

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) , or by using [Cloud Shell](https://docs.cloud.google.com/shell/docs) , which automatically logs you into the `gcloud` CLI . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Execute the following command:

    curl -X GET \
         -H "Authorization: Bearer $(gcloud auth print-access-token)" \
         "https://LOCATION_ID-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION_ID/featureOnlineStores/FEATUREONLINESTORE_NAME"

#### PowerShell

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Execute the following command:

    $cred = gcloud auth print-access-token
    $headers = @{ "Authorization" = "Bearer $cred" }
    
    Invoke-WebRequest `
        -Method GET `
        -Headers $headers `
        -Uri "https://LOCATION_ID-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION_ID/featureOnlineStores/FEATUREONLINESTORE_NAME" | Select-Object -Expand Content

You should receive a JSON response similar to the following:

    {
      "name": "projects/PROJECT_NUMBER/locations/LOCATION_ID/featureOnlineStores/FEATUREONLINESTORE_NAME_1",
      "createTime": "2023-09-06T23:25:04.256314Z",
      "updateTime": "2023-09-06T23:25:04.256314Z",
      "etag": "AMEw9yMgoV0bAsYuKwVxz4Y7lOmxV7riNVHg217KaQAKORqvdqGCrQ1DIt8yHgoGXf8=",
      "state": "STABLE",
      "dedicatedServingEndpoint": {
        "publicEndpointDomainName": "PUBLIC_ENDPOINT_DOMAIN_NAME"
      },
      "optimized": {}
    }

You'll need the PUBLIC\_ENDPOINT\_DOMAIN\_NAME from the response to fetch feature values in the following step.

### Fetch feature values from an entity ID

After you retrieve the public endpoint domain name for the online store instance, use the following sample to fetch feature values for a specific entity ID using Optimized online serving.

### REST

To fetch all the latest feature values for a specific entity ID from a [`FeatureView`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.featureOnlineStores.featureViews#resource:-featureView) instance, send a `POST` request by using the [`featureViews.fetchFeatureValues`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.featureOnlineStores.featureViews/fetchFeatureValues) method.

Before using any of the request data, make the following replacements:

  - PUBLIC\_ENDPOINT\_DOMAIN\_NAME : The public endpoint domain name for the online store instance that you retrieved using the [`featureOnlineStores.get`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.featureOnlineStores/get) method.
  - LOCATION\_ID : Region where the online store is located, such as `us-central1` .
  - PROJECT\_ID : Your project ID.
  - FEATUREONLINESTORE\_NAME : The name of the online store containing the feature view.
  - FEATUREVIEW\_NAME : The name of the feature view from which you want to serve feature values.
  - ENTITY\_ID : The value of the ID column in the feature record from which you want to serve the latest feature values.
  - FORMAT : Optional: The format used to fetch the feature values. The following formats are supported:
      - `KEY_VALUE`
      - `PROTO_STRUCT`

HTTP method and URL:

    POST https://PUBLIC_ENDPOINT_DOMAIN_NAME/v1/projects/PROJECT_ID/locations/LOCATION_ID/featureOnlineStores/FEATUREONLINESTORE_NAME/featureViews/FEATUREVIEW_NAME:fetchFeatureValues

Request JSON body:

    {
      data_key: { key: "ENTITY_ID" },
      data_format: "FORMAT"
    }

To send your request, choose one of these options:

#### curl

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) , or by using [Cloud Shell](https://docs.cloud.google.com/shell/docs) , which automatically logs you into the `gcloud` CLI . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Save the request body in a file named `request.json` , and execute the following command:

    curl -X POST \
         -H "Authorization: Bearer $(gcloud auth print-access-token)" \
         -H "Content-Type: application/json; charset=utf-8" \
         -d @request.json \
         "https://PUBLIC_ENDPOINT_DOMAIN_NAME/v1/projects/PROJECT_ID/locations/LOCATION_ID/featureOnlineStores/FEATUREONLINESTORE_NAME/featureViews/FEATUREVIEW_NAME:fetchFeatureValues"

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
        -Uri "https://PUBLIC_ENDPOINT_DOMAIN_NAME/v1/projects/PROJECT_ID/locations/LOCATION_ID/featureOnlineStores/FEATUREONLINESTORE_NAME/featureViews/FEATUREVIEW_NAME:fetchFeatureValues" | Select-Object -Expand Content

You should receive a JSON response similar to the following:

    key_values {
      features {
        value {
          int64_value: 258348
        }
        name: "feature_0"
      }
      features {
        value {
          double_value: 0.96300036744534068
        }
        name: "feature_1"
      }
      features {
        value {
          double_value: 0.42787383695351083
        }
        name: "feature_2"
      }
      features {
        value {
          double_value: 0.12219888824743128
        }
        name: "feature_3"
      }
      features {
        value {
          double_value: 0.037523154697944622
        }
        name: "feature_4"
      }
      features {
        value {
          double_value: 0.1766952509448767
        }
        name: "feature_5"
      }
    }

### Python

> **Note:** You'll need to install or upgrade to the latest version of the Python SDK to complete this step. To do this, run the following command:  
> `pip3 install --upgrade --quiet google-cloud-aiplatform` .  
> To learn more about online serving using the Python SDK, see the [Online feature serving and fetching of BigQuery data with Optimized online serving notebook tutorial](https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/feature_store/online_feature_serving_and_fetching_bigquery_data_with_feature_store_optimized.ipynb) .

Use the following sample to fetch feature values based on a specific entity ID using Optimized online serving.

    from google.cloud.aiplatform_v1 import FeatureOnlineStoreServiceClient
    from google.cloud.aiplatform_v1.types import feature_online_store_service as feature_online_store_service_pb2
    
    data_client = FeatureOnlineStoreServiceClient(
      client_options={"api_endpoint": f"PUBLIC_ENDPOINT_DOMAIN_NAME"}
    )
    data_client.fetch_feature_values(
      request=feature_online_store_service_pb2.FetchFeatureValuesRequest(
        feature_view=f"projects/PROJECT_ID/locations/LOCATION_ID/featureOnlineStores/FEATUREONLINESTORE_NAME/featureViews/FEATUREVIEW_NAME",
        data_key=feature_online_store_service_pb2.FeatureViewDataKey(key=f"ENTITY_ID"),
        data_format=feature_online_store_service_pb2.FeatureViewDataFormat.FORMAT,
      )
    )

Replace the following:

  - PUBLIC\_ENDPOINT\_DOMAIN\_NAME : The public endpoint domain name for the online store instance that you retrieved using the [`featureOnlineStores.get`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.featureOnlineStores/get) method.

  - LOCATION\_ID : Region where the online store is located, such as `us-central1` .

  - PROJECT\_ID : Your project ID.

  - FEATUREONLINESTORE\_NAME : The name of the online store containing the feature view.

  - FEATUREVIEW\_NAME : The name of the feature view from which you want to serve feature values.

  - ENTITY\_ID : The value of the ID column in the feature record from which you want to serve the latest feature values.

  - FORMAT : Optional: The format in which you want to fetch the feature values. Supported formats include JSON `KEY_VALUE` pair and proto `PROTO_STRUCT` formats.

> **Note:** If you encounter a serving error following a failed sync, contact [Support](https://cloud.google.com/support-hub) .

## Fetch feature values using Optimized online serving from a Private Service Connect endpoint

> Gemini Enterprise Agent Platform Feature Store Optimized online serving is deprecated. Beginning on May 17, 2026, no new features will be added and only critical patches will be provided. On February 17, 2027, the capability will be fully sunset and APIs will no longer be available.
> 
> To improve latency and cost optimizations, migrate to [Bigtable online serving](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/featurestore/latest/online-serving-types#bigtable_serving) . To efficiently store and serve embeddings, use the purpose-built [Vector Search](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search/overview) .

If you've configured your online store instance to serve feature values using Optimized online serving from a Private Service Connect endpoint, then you need to perform the following steps to fetch feature values from a feature view within the online store:

1.  [Retrieve the Private Service Connect configuration for the `FeatureOnlineStore` instance.](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/featurestore/latest/serve-feature-values#lowlatency_private_step1)

2.  [Add an endpoint for Private Service Connect to your network configuration.](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/featurestore/latest/serve-feature-values#lowlatency_private_step2)

3.  [Connect to the Private Service Connect endpoint over gRPC.](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/featurestore/latest/serve-feature-values#lowlatency_private_step3)

4.  [Fetch feature values from an entity ID.](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/featurestore/latest/serve-feature-values#lowlatency_private_step4)

### Retrieve the service attachment string for the online store

When you create and configure an online store instance for Optimized online serving with a Private Service Connect endpoint, Vertex AI Feature Store generates a service attachment string that you can use to set up the Private Service Connect endpoint. You can retrieve the service attachment string from the online store details.

Use the following sample to retrieve the details of an online store instance.

### REST

To retrieve the details of a [`FeatureOnlineStore`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.featureOnlineStores#resource:-featureOnlineStore) resource in your project, send a `GET` request by using the [`featureOnlineStores.get`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.featureOnlineStores/get) method.

Before using any of the request data, make the following replacements:

  - LOCATION\_ID : Region where the online store is located, such as `us-central1` .
  - PROJECT\_ID : Your project ID.
  - FEATUREONLINESTORE\_NAME : The name of the online store instance.

HTTP method and URL:

    GET https://LOCATION_ID-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION_ID/featureOnlineStores/FEATUREONLINESTORE_NAME

To send your request, choose one of these options:

#### curl

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) , or by using [Cloud Shell](https://docs.cloud.google.com/shell/docs) , which automatically logs you into the `gcloud` CLI . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Execute the following command:

    curl -X GET \
         -H "Authorization: Bearer $(gcloud auth print-access-token)" \
         "https://LOCATION_ID-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION_ID/featureOnlineStores/FEATUREONLINESTORE_NAME"

#### PowerShell

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Execute the following command:

    $cred = gcloud auth print-access-token
    $headers = @{ "Authorization" = "Bearer $cred" }
    
    Invoke-WebRequest `
        -Method GET `
        -Headers $headers `
        -Uri "https://LOCATION_ID-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION_ID/featureOnlineStores/FEATUREONLINESTORE_NAME" | Select-Object -Expand Content

You should receive a JSON response similar to the following:

    {
      "name": "projects/PROJECT_NUMBER/locations/LOCATION_ID/featureOnlineStores/FEATUREONLINESTORE_NAME_1",
      "createTime": "2023-09-06T23:25:04.256314Z",
      "updateTime": "2023-09-06T23:25:04.256314Z",
      "etag": "AMEw9yMgoV0bAsYuKwVxz4Y7lOmxV7riNVHg217KaQAKORqvdqGCrQ1DIt8yHgoGXf8=",
      "state": "STABLE",
      "dedicatedServingEndpoint": {
        "privateServiceConnectConfig": {
          "enablePrivateServiceConnect": "true",
          "projectAllowlist": [
            "PROJECT_NAME"
          ]
        },
        serviceAttachment: "SERVICE_ATTACHMENT_STRING"
      },
      "optimized": {}
    }

You'll need the SERVICE\_ATTACHMENT\_STRING from the response to fetch feature values in the following step.

### Add an endpoint for Private Service Connect

To add a Private Service Connect endpoint for Optimized online serving to your network configuration, perform the following steps:

1.  On the Google Cloud console, select the project containing the online store instance.

2.  Create an endpoint for Private Service Connect by specifying the SERVICE\_ATTACHMENT\_STRING as the **Target service** . For information about how to create an endpoint for Private Service Connect, see [Create an endpoint](https://docs.cloud.google.com/vpc/docs/configure-private-service-connect-services#create-endpoint) .

After you create the endpoint, it appears in the **Connected endpoints** tab on the **Private Service Connect** page. The IP address of the endpoint appears in the **IP addresses** column.

You'll need to use this IP address to connect to the endpoint for your online store instance to the Private Service Connect endpoint over gRPC in the following step.

### Connect to the Private Service Connect endpoint over gRPC

> **Note:** You'll need to install or upgrade to the latest version of the Python SDK to complete this step. To do this, run the following command:  
> `pip3 install --upgrade --quiet google-cloud-aiplatform`

Use the following code sample to connect to the Private Service Connect endpoint created for your online store over gRPC.

### Python

    from google.cloud.aiplatform_v1 import FeatureOnlineStoreServiceClient
    from google.cloud.aiplatform_v1.services.feature_online_store_service.transports.grpc import FeatureOnlineStoreServiceGrpcTransport
    import grpc
    
    data_client = FeatureOnlineStoreServiceClient(
      transport = FeatureOnlineStoreServiceGrpcTransport(
        # Add the IP address of the Endpoint you just created.
        channel = grpc.insecure_channel("ENDPOINT_IP:10002")
      )
    )

Replace the following:

  - ENDPOINT\_IP : The IP address of the endpoint in the **IP addresses** column on the **Private Service Connect** page.

### Fetch feature values from an entity ID

After you've connected to the Private Service Connect endpoint over gRPC, use the following sample to fetch feature values for a specific entity ID using Optimized online serving.

### Python

    data_client.fetch_feature_values(
      request=feature_online_store_service_pb2.FetchFeatureValuesRequest(
      feature_view=f"projects/PROJECT_ID/locations/LOCATION_ID/featureOnlineStores/FEATUREONLINESTORE_NAME/featureViews/FEATUREVIEW_NAME",
      data_key=feature_online_store_service_pb2.FeatureViewDataKey(ENTITY_ID),
      data_format=feature_online_store_service_pb2.FeatureViewDataFormat.PROTO_STRUCT,
      )
    )

Replace the following:

  - LOCATION\_ID : Region where the online store is located, such as `us-central1` .

  - PROJECT\_ID : Your project ID.

  - FEATUREONLINESTORE\_NAME : The name of the online store containing the feature view.

  - FEATUREVIEW\_NAME : The name of the feature view from which you want to serve feature values.

  - ENTITY\_ID : The value of the ID column in the feature record from which you want to serve the latest feature values.

  - FORMAT : Optional: The format in which you want to fetch the feature values. Supported formats include JSON key-value pair and proto `Struct` formats. Note that the proto `Struct` format doesn't support the bytes feature value type. If you want to fetch feature values that are formatted as bytes, use JSON as the response format.

> **Note:** If you encounter a serving error following a failed sync, contact [Support](https://cloud.google.com/support-hub) .

## What's next

  - Learn how to [sync data for a feature view](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/featurestore/latest/sync-data) .

  - Learn how to [update an online store](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/featurestore/latest/update-onlinestore) .
