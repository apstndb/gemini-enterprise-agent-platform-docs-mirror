---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/featurestore/latest/embeddings-search
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/featurestore/latest/embeddings-search
title: Search using embeddings
description: Learn how to search for approximate nearest neighbors of entities or embeddings in Vertex AI Feature Store.
data_source: docs.cloud.google.com
---

> Gemini Enterprise Agent Platform Feature Store Optimized online serving is deprecated. Beginning on May 17, 2026, no new features will be added and only critical patches will be provided. On February 17, 2027, the capability will be fully sunset and APIs will no longer be available.
> 
> To improve latency and cost optimizations, migrate to [Bigtable online serving](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/featurestore/latest/online-serving-types#bigtable_serving) . To efficiently store and serve embeddings, use the purpose-built [Vector Search](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search/overview) .

For online store instances created for Optimized online serving, you can perform a vector similarity search to retrieve a list of semantically similar or related entities, also called approximate nearest neighbors. You can search based on either an entity ID or an embedding.

Depending on the type of endpoint configured for your online store instance, you can do one of the following:

  - [Search nearest neighbor matches using a public endpoint](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/featurestore/latest/embeddings-search#public-endpoint) : Choose this option only if the online store is configured for Optimized online serving from a public endpoint.

  - [Search nearest neighbor matches using a Private Service Connect endpoint](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/featurestore/latest/embeddings-search#private-endpoint) : Choose this option only if the online store is configured for Optimized online serving from a dedicated serving endpoint over Private Service Connect.

## Before you begin

To search for approximate nearest neighbors, you need to first do the following:

  - Set up the BigQuery data source to support embeddings by including the `embedding` column. Optionally, include filtering and crowding columns. For more information, see [Data source preparation guidelines](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/featurestore/latest/prepare-data-source#guidelines) .

  - [Create an online store instance for Optimized online serving](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/featurestore/latest/create-onlinestore#create_fos_optimized) .

  - Create a feature view that supports embeddings by directly associating the BigQuery data source. While creating the feature view, specify the `embedding` column. For more information about how to create a feature view that supports embeddings, see [Configure vector retrieval for a feature view](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/featurestore/latest/create-featureview#configure-vectorretrieval) .

  - If you want to search nearest neighbor matches using a Private Service Connect endpoint, install or upgrade to the latest version of the Python SDK. Run the following command:  
    `pip3 install --upgrade --quiet google-cloud-aiplatform`

  - Follow these instructions to authenticate to Agent Platform, unless you've done so already.
    
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

## Search nearest neighbor matches using a public endpoint

If you've configured your online store instance to serve feature values using Optimized online serving from a public endpoint, you must do the following to retrieve approximate nearest neighbor matches:

1.  [Retrieve the public endpoint domain name for the online store](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/featurestore/latest/embeddings-search#retrieve-publicendpoint)

2.  [Retrieve nearest neighbor matches of an embedding or entity](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/featurestore/latest/embeddings-search#search-embeddingvalue)

### Retrieve the public endpoint domain name for the online store

When you create an online store instance for Optimized online serving, Vertex AI Feature Store generates a public endpoint domain name for the online store. Before you can start searching for nearest neighbors from a feature view in the online store, you must retrieve the public endpoint domain name from the online store details.

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

You'll need the PUBLIC\_ENDPOINT\_DOMAIN\_NAME from the response to retrieve approximate nearest neighbors in the following step.

### Retrieve approximate nearest neighbors using a public endpoint

After you retrieve the public endpoint domain name for the online store, you can use it to search for approximate nearest neighbors of an embedding or entity.

#### Retrieve approximate nearest neighbors of an embedding

Use the following sample to search for semantically related entities by specifying an embedding while using a public endpoint.

### REST

To search nearest neighbors for an embedding, send a `POST` request by using the [featureViews.searchNearestEntities](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.featureOnlineStores.featureViews/searchNearestEntities) method.

Before using any of the request data, make the following replacements:

  - PUBLIC\_ENDPOINT\_DOMAIN\_NAME : The public endpoint domain name for the online store instance that you retrieved using the [`featureOnlineStores.get`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.featureOnlineStores/get) method.
  - PROJECT\_ID : Your project ID.
  - LOCATION\_ID : Region where the online store instance is located, such as `us-central1` .
  - FEATUREONLINESTORE\_NAME : The name of the online store instance containing the feature view where you want to search for approximate nearest neighbor matches.
  - FEATUREVIEW\_NAME : The name of the feature view where you want to search for approximate nearest neighbor matches.
  - EMBEDDING : Embedding for which you want to retrieve approximate nearest neighbor matches. An embedding is represented by an array of `double` values.
  - RETURN\_FULL\_ENTITY : Optional: Specify whether you want to include or exclude the features for the entities in the response. To include the features along with the entities in the response, enter `true` . The default value is `false` .
  - NEIGHBOR\_COUNT : Number of approximate nearest neighbors you want to retrieve.

HTTP method and URL:

    POST https://PUBLIC_ENDPOINT_DOMAIN_NAME/v1/projects/PROJECT_ID/locations/LOCATION_ID/featureOnlineStores/FEATUREONLINESTORE_NAME/featureViews/FEATUREVIEW_NAME:searchNearestEntities

Request JSON body:

    {
      "query": {
        "embedding": {
          "value": EMBEDDING
        },
        "neighbor_count": NEIGHBOR_COUNT
      },
      "return_full_entity": RETURN_FULL_ENTITY
    }

To send your request, choose one of these options:

#### curl

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) , or by using [Cloud Shell](https://docs.cloud.google.com/shell/docs) , which automatically logs you into the `gcloud` CLI . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Save the request body in a file named `request.json` , and execute the following command:

    curl -X POST \
         -H "Authorization: Bearer $(gcloud auth print-access-token)" \
         -H "Content-Type: application/json; charset=utf-8" \
         -d @request.json \
         "https://PUBLIC_ENDPOINT_DOMAIN_NAME/v1/projects/PROJECT_ID/locations/LOCATION_ID/featureOnlineStores/FEATUREONLINESTORE_NAME/featureViews/FEATUREVIEW_NAME:searchNearestEntities"

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
        -Uri "https://PUBLIC_ENDPOINT_DOMAIN_NAME/v1/projects/PROJECT_ID/locations/LOCATION_ID/featureOnlineStores/FEATUREONLINESTORE_NAME/featureViews/FEATUREVIEW_NAME:searchNearestEntities" | Select-Object -Expand Content

You should receive a JSON response similar to the following:

    {
      "nearestNeighbors": {
        "neighbors": [
        {
          "entityId": "305281",
          "distance": -41.115459442138672
        },
        {
          "entityId": "80280",
          "distance": -38.703567504882812
        },
        {
          "entityId": "80280",
          "distance":-38.703567504882812
        },
        {
          "entityId": "903779",
          "distance": -38.214759826660156
        },
        {
          "entityId": "1008145",
          "distance": -36.271354675292969
        },
        {
          "entityId": "606431",
          "distance": -34.791431427001953
        } ]
      }
    }

#### Retrieve approximate nearest neighbors of an entity

Use the following sample to search for semantically related entities by specifying an entity ID while using a public endpoint.

### REST

To search nearest neighbors for an entity ID, send a `POST` request by using the [featureViews.searchNearestEntities](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.featureOnlineStores.featureViews/searchNearestEntities) method.

Before using any of the request data, make the following replacements:

  - PUBLIC\_ENDPOINT\_DOMAIN\_NAME : The public endpoint domain name for the online store instance that you retrieved using the [`featureOnlineStores.get`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.featureOnlineStores/get) method.
  - PROJECT\_ID : Your project ID.
  - LOCATION\_ID : Region where the online store instance is located, such as `us-central1` .
  - FEATUREONLINESTORE\_NAME : The name of the online store instance containing the feature view where you want to search for approximate nearest neighbor matches.
  - FEATUREVIEW\_NAME : The name of the feature view where you want to search for approximate nearest neighbor matches.
  - ENTITY\_ID : Entity ID of the entity for which you want to retrieve approximate nearest neighbor matches.
  - RETURN\_FULL\_ENTITY : Optional: Specify whether you want to include or exclude the features for the entities in the response. To include the features along with the entities in the response, enter `true` . The default value is `false` .
  - NEIGHBOR\_COUNT : Number of approximate nearest neighbors you want to retrieve.

HTTP method and URL:

    POST https://PUBLIC_ENDPOINT_DOMAIN_NAME/v1/projects/PROJECT_ID/locations/LOCATION_ID/featureOnlineStores/FEATUREONLINESTORE_NAME/featureViews/FEATUREVIEW_NAME:searchNearestEntities

Request JSON body:

    {
      "query": {
        "entity_id": ENTITY_ID,
        "neighbor_count": NEIGHBOR_COUNT
      },
      "return_full_entity": RETURN_FULL_ENTITY
    }

To send your request, choose one of these options:

#### curl

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) , or by using [Cloud Shell](https://docs.cloud.google.com/shell/docs) , which automatically logs you into the `gcloud` CLI . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Save the request body in a file named `request.json` , and execute the following command:

    curl -X POST \
         -H "Authorization: Bearer $(gcloud auth print-access-token)" \
         -H "Content-Type: application/json; charset=utf-8" \
         -d @request.json \
         "https://PUBLIC_ENDPOINT_DOMAIN_NAME/v1/projects/PROJECT_ID/locations/LOCATION_ID/featureOnlineStores/FEATUREONLINESTORE_NAME/featureViews/FEATUREVIEW_NAME:searchNearestEntities"

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
        -Uri "https://PUBLIC_ENDPOINT_DOMAIN_NAME/v1/projects/PROJECT_ID/locations/LOCATION_ID/featureOnlineStores/FEATUREONLINESTORE_NAME/featureViews/FEATUREVIEW_NAME:searchNearestEntities" | Select-Object -Expand Content

You should receive a JSON response similar to the following:

    {
      "nearestNeighbors": {
        "neighbors": [
        {
          "entityId": "305281",
          "distance": -41.115459442138672
        },
        {
          "entityId": "80280",
          "distance": -38.703567504882812
        },
        {
          "entityId": "80280",
          "distance":-38.703567504882812
        },
        {
          "entityId": "903779",
          "distance": -38.214759826660156
        },
        {
          "entityId": "1008145",
          "distance": -36.271354675292969
        },
        {
          "entityId": "606431",
          "distance": -34.791431427001953
        } ]
      }
    }

## Search nearest neighbor matches using a Private Service Connect endpoint

If you've configured your online store instance to serve feature values using Optimized online serving from a Private Service Connect endpoint, then you must do the following to retrieve approximate nearest neighbor matches:

1.  [Retrieve the service attachment string for the online store.](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/featurestore/latest/embeddings-search#private-serviceattachmentstring)

2.  [Add an endpoint for Private Service Connect to your network configuration.](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/featurestore/latest/embeddings-search#private-addendpoint)

3.  [Connect to the Private Service Connect endpoint over gRPC.](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/featurestore/latest/embeddings-search#private-connect)

4.  [Retrieve nearest neighbor matches of an embedding or entity](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/featurestore/latest/embeddings-search#private-search-embeddingvalue)

### Retrieve the service attachment string for the online store

When you create an online store instance for Optimized online serving with a Private Service Connect endpoint, Vertex AI Feature Store generates a service attachment string. You can retrieve the service attachment string from the online store details and use this string to set up the Private Service Connect endpoint.

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

2.  [Create an endpoint for Private Service Connect](https://docs.cloud.google.com/vpc/docs/configure-private-service-connect-services#create-endpoint) by specifying the SERVICE\_ATTACHMENT\_STRING as the **Target service** .

After you create the endpoint, it appears in the **Connected endpoints** tab on the **Private Service Connect** page. The IP address of the endpoint appears in the **IP addresses** column.

You'll need to use this IP address to connect to the endpoint for your online store instance to the Private Service Connect endpoint over gRPC in the following step.

### Connect to the Private Service Connect endpoint over gRPC

> **Note:** To complete this step, you must install or upgrade to the latest version of the Python SDK, as described in [Before you begin](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/featurestore/latest/embeddings-search#before-you-begin) section.

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

### Retrieve approximate nearest neighbors using a Private Service Connect endpoint

After you've connected to the Private Service Connect endpoint over gRPC, you can search for approximate nearest neighbors of an embedding or entity.

#### Retrieve approximate nearest neighbors of an embedding

Use the following sample to search for semantically related entities by specifying an embedding while using a private endpoint.

### Python

    data_client.search_nearest_entities(
      request=feature_online_store_service_pb2.SearchNearestEntitiesRequest(
          feature_view=f"projects/PROJECT_ID/locations/LOCATION_ID/featureOnlineStores/FEATUREONLINESTORE_NAME/featureViews/FEATUREVIEW_NAME",
          query=feature_online_store_service_pb2.NearestNeighborQuery(
              embedding = "EMBEDDING",
              neighbor_count = NEIGHBOR_COUNT,
          ),
          return_full_entity=RETURN_FULL_ENTITY
      ))

Replace the following:

  - LOCATION\_ID : Region where the online store is located, such as `us-central1` .

  - PROJECT\_ID : Your project ID.

  - FEATUREONLINESTORE\_NAME : The name of the online store containing the feature view.

  - FEATUREVIEW\_NAME : The name of the feature view where you want to search for approximate nearest neighbor matches.

  - EMBEDDING : Embedding for which you want to retrieve approximate nearest neighbor matches. An embedding is represented by an array of `double` values.

  - FORMAT : Optional: The format in which you want to fetch the feature values. Supported formats include JSON key-value pair and proto `Struct` formats. Note that the proto `Struct` format doesn't support the bytes feature value type. If you want to fetch feature values that are formatted as bytes, use JSON as the response format.

  - RETURN\_FULL\_ENTITY : Optional: Specify whether you want to include or exclude the features for the entities in the response. To include the features along with the entities in the response, enter `true` . The default value is `false` .

  - NEIGHBOR\_COUNT : Number of approximate nearest neighbors you want to retrieve.

#### Retrieve approximate nearest neighbors of an entity

Use the following sample to search for semantically related entities by specifying an entity ID while using a private endpoint.

### Python

    data_client.search_nearest_entities(
      request=feature_online_store_service_pb2.SearchNearestEntitiesRequest(
          feature_view=f"projects/PROJECT_ID/locations/LOCATION_ID/featureOnlineStores/FEATUREONLINESTORE_NAME/featureViews/FEATUREVIEW_NAME",
          query=feature_online_store_service_pb2.NearestNeighborQuery(
              entity_id = "ENTITY_ID",
              neighbor_count = NEIGHBOR_COUNT,
          ),
          return_full_entity=RETURN_FULL_ENTITY
      ))
     ```

Replace the following:

  - LOCATION\_ID : Region where the online store is located, such as `us-central1` .

  - PROJECT\_ID : Your project ID.

  - FEATUREONLINESTORE\_NAME : The name of the online store containing the feature view.

  - FEATUREVIEW\_NAME : The name of the feature view where you want to search for approximate nearest neighbor matches.

  - ENTITY\_ID : Entity ID of the entity for which you want to retrieve approximate nearest neighbor matches.

  - FORMAT : Optional: The format in which you want to fetch the feature values. Supported formats include JSON key-value pair and proto `Struct` formats. Note that the proto `Struct` format doesn't support the bytes feature value type. If you want to fetch feature values that are formatted as bytes, use JSON as the response format.

  - RETURN\_FULL\_ENTITY : Optional: Specify whether you want to include or exclude the features for the entities in the response. To include the features along with the entities in the response, enter `true` . The default value is `false` .

  - NEIGHBOR\_COUNT : Number of approximate nearest neighbors you want to retrieve.

> **Note:** If you encounter a serving error following a failed sync, contact [Support](https://cloud.google.com/support-hub) .
