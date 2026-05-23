---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/featurestore/latest/create-onlinestore
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/featurestore/latest/create-onlinestore
title: Create an online store instance
description: Learn how to create an online store instance for Bigtable online serving or Optimized online serving in Vertex AI Feature Store.
data_source: docs.cloud.google.com
---

To set up online serving, you need to first create an online store instance for Bigtable online serving or Optimized online serving ( [Deprecated](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/deprecations) ).

Note that you can't change the type of online serving after you choose Bigtable online serving or Optimized online serving while creating your online store. However, you can change the serving endpoint configuration for an online store instance created for Optimized online serving.

After you create the online store, you can [add feature views](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/featurestore/latest/create-featureview) and associate those feature views with feature data sources in BigQuery.

You can encrypt your online store instance by specifying a [customer-managed encryption key (CMEK)](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/cmek) when you create your online store instance. Only Bigtable online serving supports encryption using a CMEK. To learn more about the benefits of using a CMEK and to understand whether a CMEK is useful for your online store, see [Benefits of CMEK](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/cmek#benefits) .

Using a CMEK can involve additional usage costs, depending on the type of key being used. For more information about pricing, refer to [Cloud Key Management Service pricing](https://cloud.google.com/kms/pricing) .

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

## Create an online store for Bigtable online serving

When you use Bigtable online serving, you have the option to encrypt the online store using a [CMEK](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/cmek) .

### Create an online store for Bigtable online serving without CMEK

To create an online store instance for Bigtable online serving with autoscaling, without specifying a CMEK, use the Google Cloud console or the REST API.

> **Note:** Bigtable online serving doesn't support embeddings. If you want to serve embeddings, use [Vector Search](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search/overview) instead.

### Console

Use the following instructions to create an online store for Bigtable online serving using the Google Cloud console.

1.  In the Agent Platform section of the Google Cloud console, go to the **Feature Store** page.

2.  Click **Online store** to go to the **Online store** section.

3.  Click **Create** to open the **Create Online Store** page.

4.  Specify a name for the online store.

5.  Optional: To add labels, click **Add label** , and specify the label name and value. You can add multiple labels to an online store.

6.  In the **Choose a storage solution for your online store** field, click **Bigtable** .

7.  Modify the **Minimum node count** , **Maximum node count** , and **CPU utilization target** , as needed.

8.  Click **Create** .

### Python

To learn how to install or update the Vertex AI SDK for Python, see [Install the Vertex AI SDK for Python](https://docs.cloud.google.com/vertex-ai/docs/start/use-vertex-ai-python-sdk) . For more information, see the [Python API reference documentation](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest) .

    from google.cloud import aiplatform
    from vertexai.resources.preview import feature_store
    
    
    def create_bigtable_feature_online_store_sample(
        project: str,
        location: str,
        feature_online_store_id: str,
    ):
        aiplatform.init(project=project, location=location)
        fos = feature_store.FeatureOnlineStore.create_bigtable_store(
            feature_online_store_id
        )
        return fos

  - `project` : Your project ID.
  - `location` : Region where the online store is located, such as `us-central1` .
  - `feature_online_store_id` : The name of the new `FeatureOnlineStore` instance.

### REST

To create a [`FeatureOnlineStore`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.featureOnlineStores#resource:-featureOnlineStore) resource, send a `POST` request by using the [featureOnlineStores.create](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.featureOnlineStores/create) method.

Before using any of the request data, make the following replacements:

  - LOCATION\_ID : Region where you want to create the online store, such as `us-central1` .
  - PROJECT\_ID : Your project ID.
  - FEATUREONLINESTORE\_NAME : The name of the new online store instance.
  - BOOLEAN : Optional: To create an online store that supports embedding management, enter `true` . The default value is `false` .

HTTP method and URL:

    POST https://LOCATION_ID-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION_ID/featureOnlineStores?feature_online_store_id=FEATUREONLINESTORE_NAME

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

    curl -X POST \
         -H "Authorization: Bearer $(gcloud auth print-access-token)" \
         -H "Content-Type: application/json; charset=utf-8" \
         -d @request.json \
         "https://LOCATION_ID-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION_ID/featureOnlineStores?feature_online_store_id=FEATUREONLINESTORE_NAME"

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
        -Uri "https://LOCATION_ID-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION_ID/featureOnlineStores?feature_online_store_id=FEATUREONLINESTORE_NAME" | Select-Object -Expand Content

You should receive a JSON response similar to the following:

    {
      "name": "projects/PROJECT_NUMBER/locations/LOCATION_ID/featureOnlineStores/FEATUREONLINESTORE_NAME/operations/OPERATION_ID",
      "metadata": {
        "@type": "type.googleapis.com/google.cloud.aiplatform.v1.CreateFeatureOnlineStoreOperationMetadata",
        "genericMetadata": {
          "createTime": "2023-09-18T17:49:23.847496Z",
          "updateTime": "2023-09-18T17:49:23.847496Z"
        }
      }
    }

### Create an online store that uses a CMEK

Use the following steps to create an online store instance for Bigtable online serving that's encrypted with a CMEK.

Using a CMEK encryption can involve additional usage costs, depending on the type of key being used. For more information about pricing, refer to [Cloud Key Management Service pricing](https://cloud.google.com/kms/pricing) .

> **Note:** Bigtable online serving doesn't support embeddings. If you want to serve embeddings, use [Vector Search](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search/overview) instead.

1.  [Use Cloud Key Management Service to configure a customer-managed encryption key.](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/cmek#configure-cmek)

2.  To create a [`FeatureOnlineStore`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.featureOnlineStores#resource:-featureOnlineStore) resource, send the following `POST` request by using the [featureOnlineStores.create](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.featureOnlineStores/create) method and specifying the CMEK.
    
    Before using any of the request data, make the following replacements:
    
      - LOCATION\_ID : Region where you want to create the online store, such as `us-central1` .
      - PROJECT\_ID : Your project ID.
      - FEATUREONLINESTORE\_NAME : The name of the new online store instance.
      - BOOLEAN : Optional: To create an online store that supports embedding management, enter `true` . The default value is `false` .
      - KEY\_NAME : The name of the encryption key that you want to use for this metadata store.
    
    HTTP method and URL:
    
        POST https://LOCATION_ID-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION_ID/featureOnlineStores?feature_online_store_id=FEATUREONLINESTORE_NAME
    
    Request JSON body:
    
        {
          "bigtable": {
            "auto_scaling": {
              "min_node_count": 1,
              "max_node_count": 3,
              "cpu_utilization_target": 50
            }
          },
          "encryption_spec": {
            "kms_key_name": "KEY_NAME"
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
             "https://LOCATION_ID-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION_ID/featureOnlineStores?feature_online_store_id=FEATUREONLINESTORE_NAME"
    
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
            -Uri "https://LOCATION_ID-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION_ID/featureOnlineStores?feature_online_store_id=FEATUREONLINESTORE_NAME" | Select-Object -Expand Content
    
    You should receive a JSON response similar to the following:
    
        {
          "name": "projects/PROJECT_NUMBER/locations/LOCATION_ID/featureOnlineStores/FEATUREONLINESTORE_NAME/operations/OPERATION_ID",
          "metadata": {
            "@type": "type.googleapis.com/google.cloud.aiplatform.v1.CreateFeatureOnlineStoreOperationMetadata",
            "genericMetadata": {
              "createTime": "2023-09-18T17:49:23.847496Z",
              "updateTime": "2023-09-18T17:49:23.847496Z"
            }
          }
        }

## Create an online store for Optimized online serving

> Gemini Enterprise Agent Platform Feature Store Optimized online serving is [deprecated](https://docs.cloud.google.com/vertex-ai/docs/deprecations) . Beginning on May 17, 2026, no new features will be added and only critical patches will be provided. On February 17, 2027, the capability will be fully sunset and APIs will no longer be available.
> 
> To improve latency and cost optimizations, migrate to [Bigtable online serving](https://docs.cloud.google.com/vertex-ai/docs/featurestore/latest/online-serving-types#bigtable_serving) . To efficiently store and serve embeddings, use the purpose-built [Vector Search](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search/overview) .

When you use Optimized online serving, you can configure the online store to serve features from either a public endpoint or a dedicated Private Service Connect endpoint.

### Create an online store for Optimized online serving with a public endpoint

Use the following samples to create an online store for Optimized online serving with a public endpoint.

### Console

Use the following instructions to create an online store for Optimized online serving using the Google Cloud console.

1.  In the Agent Platform section of the Google Cloud console, go to the **Feature Store** page.

2.  Click **Online store** to go to the **Online store** section.

3.  Click **Create** to open the **Create Online Store** page.

4.  Specify a name for the online store.

5.  Optional: To add labels, click **Add label** , and specify the label name and value. You can add multiple labels to an online store.

6.  In the **Choose a storage solution for your online store** field, click **Optimized** .

7.  Click **Create** .

### Python

To learn how to install or update the Vertex AI SDK for Python, see [Install the Vertex AI SDK for Python](https://docs.cloud.google.com/vertex-ai/docs/start/use-vertex-ai-python-sdk) . For more information, see the [Python API reference documentation](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest) .

    from google.cloud import aiplatform
    from vertexai.resources.preview import feature_store
    
    
    def create_optimized_public_feature_online_store_sample(
        project: str,
        location: str,
        feature_online_store_id: str,
    ):
        aiplatform.init(project=project, location=location)
        fos = feature_store.FeatureOnlineStore.create_optimized_store(
            feature_online_store_id
        )
        return fos

  - `project` : Your project ID.
  - `location` : Region where you want to create the `FeatureOnlineStore` instance, such as `us-central1` .
  - `feature_online_store_id` : The name of the new `FeatureOnlineStore` instance.

### REST

To create an online store instance, send a `POST` request by using the [featureOnlineStores.create](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.featureOnlineStores/create) method.

Before using any of the request data, make the following replacements:

  - LOCATION\_ID : Region where you want to create the `FeatureOnlineStore` instance, such as `us-central1` .
  - PROJECT\_ID : Your project ID.
  - FEATUREONLINESTORE\_NAME : The name of the new `FeatureOnlineStore` instance.

HTTP method and URL:

    POST https://LOCATION_ID-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION_ID/featureOnlineStores?feature_online_store_id=FEATUREONLINESTORE_NAME

Request JSON body:

    {
      "optimized": {}
    }

To send your request, choose one of these options:

#### curl

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) , or by using [Cloud Shell](https://docs.cloud.google.com/shell/docs) , which automatically logs you into the `gcloud` CLI . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Save the request body in a file named `request.json` , and execute the following command:

    curl -X POST \
         -H "Authorization: Bearer $(gcloud auth print-access-token)" \
         -H "Content-Type: application/json; charset=utf-8" \
         -d @request.json \
         "https://LOCATION_ID-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION_ID/featureOnlineStores?feature_online_store_id=FEATUREONLINESTORE_NAME"

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
        -Uri "https://LOCATION_ID-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION_ID/featureOnlineStores?feature_online_store_id=FEATUREONLINESTORE_NAME" | Select-Object -Expand Content

You should receive a JSON response similar to the following:

    {
      "name": "projects/PROJECT_NUMBER/locations/LOCATION_ID/featureOnlineStores/FEATUREONLINESTORE_NAME/operations/OPERATION_ID",
      "metadata": {
        "@type": "type.googleapis.com/google.cloud.aiplatform.v1.CreateFeatureOnlineStoreOperationMetadata",
        "genericMetadata": {
          "createTime": "2023-09-18T17:49:23.847496Z",
          "updateTime": "2023-09-18T17:49:23.847496Z"
        }
      }
    }

### Create an online store for Optimized online serving with a Private Service Connect endpoint

Use the following samples to create an online store for Optimized online serving with [Private Service Connect](https://docs.cloud.google.com/vpc/docs/private-service-connect) .

### Python

To learn how to install or update the Vertex AI SDK for Python, see [Install the Vertex AI SDK for Python](https://docs.cloud.google.com/vertex-ai/docs/start/use-vertex-ai-python-sdk) . For more information, see the [Python API reference documentation](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest) .

    from typing import List
    
    from google.cloud import aiplatform
    from vertexai.resources.preview import feature_store
    
    
    def create_optimized_private_feature_online_store_sample(
        project: str,
        location: str,
        feature_online_store_id: str,
        project_allowlist: List[str],
    ):
        aiplatform.init(project=project, location=location)
        fos = feature_store.FeatureOnlineStore.create_optimized_store(
            name=feature_online_store_id,
            enable_private_service_connect=True,
            project_allowlist=project_allowlist,
        )
        return fos

  - `project` : Your project ID.
  - `location` : Region where you want to create the `FeatureOnlineStore` instance, such as `us-central1` .
  - `feature_online_store_id` : The name of the new `FeatureOnlineStore` instance.
  - `project_allowlist` : The list of project names to be allowlisted for private service connect (PSC).

### REST

To create an online store instance, send a `POST` request by using the [featureOnlineStores.create](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.featureOnlineStores/create) method.

Before using any of the request data, make the following replacements:

  - LOCATION\_ID : Region where you want to create the `FeatureOnlineStore` instance, such as `us-central1` .
  - PROJECT\_ID : Your project ID.
  - FEATUREONLINESTORE\_NAME : The name of the new `FeatureOnlineStore` instance.
  - PROJECT\_NAMES : The list of project names to be allowlisted for private service connect (PSC).

HTTP method and URL:

    POST https://LOCATION_ID-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION_ID/featureOnlineStores?feature_online_store_id=FEATUREONLINESTORE_NAME

Request JSON body:

    {
      "optimized": {},
      "dedicated_serving_endpoint": {
        "private_service_connect_config": {
          "enable_private_service_connect": true,
          "project_allowlist": ["PROJECT_NAMES"]
        }
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
         "https://LOCATION_ID-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION_ID/featureOnlineStores?feature_online_store_id=FEATUREONLINESTORE_NAME"

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
        -Uri "https://LOCATION_ID-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION_ID/featureOnlineStores?feature_online_store_id=FEATUREONLINESTORE_NAME" | Select-Object -Expand Content

You should receive a JSON response similar to the following:

    {
      "name": "projects/PROJECT_NUMBER/locations/LOCATION_ID/featureOnlineStores/FEATUREONLINESTORE_NAME/operations/OPERATION_ID",
      "metadata": {
        "@type": "type.googleapis.com/google.cloud.aiplatform.v1.CreateFeatureOnlineStoreOperationMetadata",
        "genericMetadata": {
          "createTime": "2023-09-18T17:49:23.847496Z",
          "updateTime": "2023-09-18T17:49:23.847496Z"
        }
      }
    }

## What's next

  - Learn how to [create a feature view](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/featurestore/latest/create-featureview) .

  - Learn how to [update an online store](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/featurestore/latest/update-onlinestore) .
