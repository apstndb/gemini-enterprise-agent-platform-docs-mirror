---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/indexes/indexes
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/indexes/indexes
title: Collection Indexes
description: Learn about Collection Indexes in Agent Retrieval (formerly Vector Search 2.0).
data_source: docs.cloud.google.com
---

To prepare your application for production scale and performance, you need to create Collection Indexes. Without an Index, ANN searches are slow because they perform a brute-force scan. Creating an Index makes searches against the indexed vector fields very fast.

## Index configuration

When you create an Index, you set the vector field to index and optionally the distance metric, dedicated infrastructure, and dense ScaNN configuration.

The following table lists the top-level fields that you can set when creating an Index.

| Field           | Required | Immutable | Description                                                                                                                  |
| :-------------- | :------- | :-------- | :--------------------------------------------------------------------------------------------------------------------------- |
| Index Field     | Yes      | Yes       | The Collection vector-schema field to index. Must reference a dense vector or sparse vector field defined in the Collection. |
| Display name    | No       | No        | A display name for the Index.                                                                                                |
| Description     | No       | No        | A description for the Index.                                                                                                 |
| Labels          | No       | No        | Key-value pairs for labeling the resource.                                                                                   |
| Filter fields   | No       | Yes       | Data fields pushed into the Index to enable fast inline filtering during Approximate Nearest Neighbor (ANN) search.          |
| Store fields    | No       | Yes       | Data fields pushed into the Index to enable inline data retrieval with search results.                                       |
| Distance metric | No       | Yes       | The distance metric used for indexing. Defaults to `DOT_PRODUCT` .                                                           |
| Dense ScaNN     | No       | Yes       | The feature normalization for dense vector fields when using performance-optimized infrastructure.                           |

> **Note:** The service assigns the read-only fields `name` , `create_time` , and `update_time` .

### Dedicated infrastructure

The optional dedicated infrastructure field controls the Index's optimization mode and scaling behavior.

The following table lists lists the fields that are available.

| Field            | Required | Description                                                                                               |
| :--------------- | :------- | :-------------------------------------------------------------------------------------------------------- |
| Autoscaling spec | No       | The autoscaling bounds for the index replicas.                                                            |
| Mode             | No       | The infrastructure performance mode. This can be performance-optimized (the default) or storage-optimized |

### Autoscaling

The optional autoscaling field defines the minimum and maximum replica counts when autoscaling is performed.

The following table lists the fields that are available.

| Field                 | Required | Description                                                                                                                                                                                                                    |
| :-------------------- | :------- | :----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Minimum replica count | No       | The minimum number of replicas. If unspecified or set to 0, defaults to 2. Must be greater than or equal to 1 and less than or equal to 1000.                                                                                  |
| Maximum replica count | No       | The maximum number of replicas. Must be greater than or equal to minimum replica count and less than or equal to 1000. If unspecified or set to 0, set to whichever is greater: the minimum replica count or 2 (5 for v1beta). |

### Infrastructure optimization modes

The optional infrastructure optimization mode field specifies whether the serving hardware is optimized for performance or storage.

The following table lists the modes that are available.

| Mode                               | Value                   | Description                                                                                                                                                                         |
| :--------------------------------- | :---------------------- | :---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Performance optimization (default) | `PERFORMANCE_OPTIMIZED` | The serving hardware is optimized for performance.                                                                                                                                  |
| Storage optimization               | `STORAGE_OPTIMIZED`     | The serving hardware is optimized for storage. This is recommended for large Indexes where storage cost matters more than lowest latency. This is only supported for dense vectors. |

### Distance metric

The optional distance metric field determines how vector similarity is measured.

The following table lists available distance metrics.

| Metric                | Supported optimization modes | Value             | Description                                                                                                                                                 |
| :-------------------- | :--------------------------- | :---------------- | :---------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Dot product (default) | Performance, storage         | `DOT_PRODUCT`     | The dot product distance. This is the default if the distance metric field is unspecified.                                                                  |
| Cosine similarity     | Performance                  | `COSINE_DISTANCE` | Cosine distance. You don't need to set the feature normalization type when using this metric; unit L2 normalization is used as the underlying optimization. |

#### Choosing a distance metric

Choosing the right distance metric for your Index is crucial for achieving accurate and relevant similarity search results. The optimal choice depends primarily on the characteristics of your vector embeddings and the nature of your data.

The most critical rule is to use the distance metric that your embedding model was trained on. Embedding models are optimized to produce vector representations where similarity is best captured by a specific distance calculation. Using a different metric can lead to suboptimal or incorrect search results.

  - **Check your embedding model's documentation:** This is the most reliable way to determine the intended distance metric.

  - **Consider your use case:** For finding semantically similar text or images, Cosine Similarity is often the best choice. If the "strength" or "intensity" represented by the vector's magnitude is important, consider L2 Distance.

  - **Analyze your vectors:** Determine if your vectors are normalized. If they are, you can use either Cosine Similarity or Dot Product and expect similar ranking.

By carefully considering these factors, you can select the most appropriate distance metric for your Index, leading to more accurate and meaningful similarity search results.

### Dense ScaNN and feature normalization

For dense vector fields, the optional dense ScaNN configuration field lets you control how features are normalized before indexing. The dense vector field contains the optional feature normalization type field. Set this only when you need a specific normalization and the infrastructure mode is performance optimized. When unspecified, the service applies a suitable default.

The following table provides the feature normalization values that are available.

| Feature normalization | Value          | Description                         |
| :-------------------- | :------------- | :---------------------------------- |
| None                  | `NONE`         | No feature should be normalized.    |
| Unit L2               | `UNIT_L2_NORM` | Normalizes vectors to unit L2 norm. |

> **Note:** Don't specify feature normalization if the infrastructure mode is storage optimized.

## Creating an ANN Index

Data Object string, numeric, and boolean fields are pushed down to the Index to allow for inline filtering.

To optimize compute costs, you can specify exactly which fields should be filterable ( `filter_fields` ) and which should just be stored as payload only ( `store_fields` ).

> **Note:** An Index always references a single vector field that you declared in the Collection's vector schema. Create the Collection and its vector schema first, before creating Indexes over its vector fields.

The following example demonstrates how to create an Index, `  INDEX_ID  ` , in a Collection with the ID `  COLLECTION_ID  ` .

### REST

Before using any of the request data, make the following replacements:

  - INDEX\_ID : The ID of the index.
  - COLLECTION\_ID : The ID of the collection.
  - LOCATION : The region where you are using Agent Platform.
  - PROJECT\_ID : Your Google Cloud [project ID](https://docs.cloud.google.com/resource-manager/docs/creating-managing-projects#identifying_projects) .

HTTP method and URL:

    POST https://vectorsearch.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/collections/COLLECTION_ID/indexes?indexId=INDEX_ID

Request JSON body:

    {
        "index_field": "plot_embedding",
        "filter_fields": [
          "year",
          "genre"
        ],
        "store_fields": [
          "title"
        ]
    }

To send your request, expand one of these options:

#### curl (Linux, macOS, or Cloud Shell)

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) , or by using [Cloud Shell](https://docs.cloud.google.com/shell/docs) , which automatically logs you into the `gcloud` CLI . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Save the request body in a file named `request.json` , and execute the following command:

    curl -X POST \
         -H "Authorization: Bearer $(gcloud auth print-access-token)" \
         -H "Content-Type: application/json; charset=utf-8" \
         -d @request.json \
         "https://vectorsearch.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/collections/COLLECTION_ID/indexes?indexId=INDEX_ID"

#### PowerShell (Windows)

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Save the request body in a file named `request.json` , and execute the following command:

    $cred = gcloud auth print-access-token
    $headers = @{ "Authorization" = "Bearer $cred" }
    
    Invoke-WebRequest `
        -Method POST `
        -Headers $headers `
        -ContentType: "application/json; charset=utf-8" `
        -InFile request.json `
        -Uri "https://vectorsearch.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/collections/COLLECTION_ID/indexes?indexId=INDEX_ID" | Select-Object -Expand Content

You should receive a JSON response similar to the following:

    {
      "name": "projects/PROJECT_ID/locations/LOCATION/operations/operation-1770302393524-64a14a54fa197-0dea326c-5a90efda",
      "metadata": {
        "@type": "type.googleapis.com/google.cloud.vectorsearch.v1.OperationMetadata",
        "createTime": "2026-02-05T14:39:53.558308609Z",
        "target": "projects/PROJECT_ID/locations/LOCATION/collections/COLLECTION_ID/indexes/INDEX_ID",
        "verb": "create",
        "requestedCancellation": false,
        "apiVersion": "v1"
      },
      "done": false
    }

### gcloud

Before using any of the command data below, make the following replacements:

  - INDEX\_ID : The ID of the index.
  - COLLECTION\_ID : The ID of the collection.
  - LOCATION : The region where you are using Agent Platform.
  - PROJECT\_ID : Your Google Cloud [project ID](https://docs.cloud.google.com/resource-manager/docs/creating-managing-projects#identifying_projects) .

Execute the following command:

#### Linux, macOS, or Cloud Shell

> **Note:** Ensure you have initialized the Google Cloud CLI with authentication and a project by running either [gcloud init](https://docs.cloud.google.com/sdk/gcloud/reference/init) ; or [gcloud auth login](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) and [gcloud config set project](https://docs.cloud.google.com/sdk/gcloud/reference/config/set) .

    gcloud vector-search collections indexes create INDEX_ID \
      --collection=COLLECTION_ID \
      --index-field=plot_embedding \
      --filter-fields=year,genre \
      --store-fields=title \
      --location=LOCATION \
      --project=PROJECT_ID

#### Windows (PowerShell)

> **Note:** Ensure you have initialized the Google Cloud CLI with authentication and a project by running either [gcloud init](https://docs.cloud.google.com/sdk/gcloud/reference/init) ; or [gcloud auth login](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) and [gcloud config set project](https://docs.cloud.google.com/sdk/gcloud/reference/config/set) .

    gcloud vector-search collections indexes create INDEX_ID `
      --collection=COLLECTION_ID `
      --index-field=plot_embedding `
      --filter-fields=year,genre `
      --store-fields=title `
      --location=LOCATION `
      --project=PROJECT_ID

#### Windows (cmd.exe)

> **Note:** Ensure you have initialized the Google Cloud CLI with authentication and a project by running either [gcloud init](https://docs.cloud.google.com/sdk/gcloud/reference/init) ; or [gcloud auth login](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) and [gcloud config set project](https://docs.cloud.google.com/sdk/gcloud/reference/config/set) .

    gcloud vector-search collections indexes create INDEX_ID ^
      --collection=COLLECTION_ID ^
      --index-field=plot_embedding ^
      --filter-fields=year,genre ^
      --store-fields=title ^
      --location=LOCATION ^
      --project=PROJECT_ID

You should receive a response similar to the following:

    Created index [INDEX_ID].

### Python

    from google.cloud import vectorsearch_v1
    
    # Create a client
    client = vectorsearch_v1.VectorSearchServiceClient()
    
    # Initialize request argument(s)
    index = vectorsearch_v1.Index(
        index_field="plot_embedding",
        filter_fields=["year", "genre"],
        store_fields=["title"],
    )
    request = vectorsearch_v1.CreateIndexRequest(
        parent="projects/PROJECT_ID/locations/LOCATION/collections/COLLECTION_ID",
        index_id="INDEX_ID",
        index=index,
    )
    
    # Make the request
    operation = client.create_index(request=request)
    
    # Wait for the result (note this may take up to several minutes)
    operation.result()

In the example, the request specifies that `year` and `genre` are filterable (passed as filter fields to the Index), and the payload field `title` is non-filterable.

## Getting an Index

The following demonstrates how to get an existing Index, `  INDEX_ID  ` , stored in a Collection with the ID `  COLLECTION_ID  ` .

### REST

Before using any of the request data, make the following replacements:

  - INDEX\_ID : The ID of the index.
  - COLLECTION\_ID : The ID of the collection.
  - LOCATION : The region where you are using Agent Platform.
  - PROJECT\_ID : Your Google Cloud [project ID](https://docs.cloud.google.com/resource-manager/docs/creating-managing-projects#identifying_projects) .

HTTP method and URL:

    GET https://vectorsearch.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/collections/COLLECTION_ID/indexes/INDEX_ID

To send your request, expand one of these options:

#### curl (Linux, macOS, or Cloud Shell)

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) , or by using [Cloud Shell](https://docs.cloud.google.com/shell/docs) , which automatically logs you into the `gcloud` CLI . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Execute the following command:

    curl -X GET \
         -H "Authorization: Bearer $(gcloud auth print-access-token)" \
         "https://vectorsearch.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/collections/COLLECTION_ID/indexes/INDEX_ID"

#### PowerShell (Windows)

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Execute the following command:

    $cred = gcloud auth print-access-token
    $headers = @{ "Authorization" = "Bearer $cred" }
    
    Invoke-WebRequest `
        -Method GET `
        -Headers $headers `
        -Uri "https://vectorsearch.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/collections/COLLECTION_ID/indexes/INDEX_ID" | Select-Object -Expand Content

You should receive a JSON response similar to the following:

    {
      "name": "projects/PROJECT_ID/locations/LOCATION/collections/COLLECTION_ID/indexes/INDEX_ID",
      "createTime": "2026-02-05T14:39:53.550302019Z",
      "updateTime": "2026-02-05T14:39:53.550302019Z",
      "distanceMetric": "DOT_PRODUCT",
      "indexField": "plot_embedding",
      "filterFields": [
        "year",
        "genre"
      ],
      "storeFields": [
        "title"
      ]
    }

### gcloud

Before using any of the command data below, make the following replacements:

  - INDEX\_ID : The ID of the index.
  - COLLECTION\_ID : The ID of the collection.
  - LOCATION : The region where you are using Agent Platform.
  - PROJECT\_ID : Your Google Cloud [project ID](https://docs.cloud.google.com/resource-manager/docs/creating-managing-projects#identifying_projects) .

Execute the following command:

#### Linux, macOS, or Cloud Shell

    gcloud vector-search collections indexes describe INDEX_ID \
      --collection=COLLECTION_ID \
      --location=LOCATION \
      --project=PROJECT_ID

#### Windows (PowerShell)

    gcloud vector-search collections indexes describe INDEX_ID `
      --collection=COLLECTION_ID `
      --location=LOCATION `
      --project=PROJECT_ID

#### Windows (cmd.exe)

    gcloud vector-search collections indexes describe INDEX_ID ^
      --collection=COLLECTION_ID ^
      --location=LOCATION ^
      --project=PROJECT_ID

You should receive a response similar to the following:

    createTime: '2026-02-05T1T14:39:53.550302019Z'
    distanceMetric: DOT_PRODUCT
    filterFields:
    - year
    - genre
    indexField: plot_embedding
    name: projects/PROJECT_ID/locations/LOCATION/collections/COLLECTION_ID/indexes/INDEX_ID
    storeFields:
    - title
    updateTime: '2026-02-05T14:39:53.550302019Z'

### Python

    from google.cloud import vectorsearch_v1
    
    # Create the client
    vector_search_service_client = vectorsearch_v1.VectorSearchServiceClient()
    
    # Initialize request
    request = vectorsearch_v1.GetIndexRequest(
        name="projects/PROJECT_ID/locations/LOCATION/collections/COLLECTION_ID/indexes/INDEX_ID",
    )
    
    # Make the request
    response = vector_search_service_client.get_index(request=request)
    
    # Handle the response
    print(response)

## Listing Indexes

The following example demonstrates how to list all Indexes in a Collection with the ID `  COLLECTION_ID  ` .

### REST

Before using any of the request data, make the following replacements:

  - COLLECTION\_ID : The ID of the collection.
  - LOCATION : The region where you are using Agent Platform.
  - PROJECT\_ID : Your Google Cloud [project ID](https://docs.cloud.google.com/resource-manager/docs/creating-managing-projects#identifying_projects) .

HTTP method and URL:

    GET https://vectorsearch.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/collections/COLLECTION_ID/indexes

To send your request, expand one of these options:

#### curl (Linux, macOS, or Cloud Shell)

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) , or by using [Cloud Shell](https://docs.cloud.google.com/shell/docs) , which automatically logs you into the `gcloud` CLI . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Execute the following command:

    curl -X GET \
         -H "Authorization: Bearer $(gcloud auth print-access-token)" \
         "https://vectorsearch.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/collections/COLLECTION_ID/indexes"

#### PowerShell (Windows)

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Execute the following command:

    $cred = gcloud auth print-access-token
    $headers = @{ "Authorization" = "Bearer $cred" }
    
    Invoke-WebRequest `
        -Method GET `
        -Headers $headers `
        -Uri "https://vectorsearch.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/collections/COLLECTION_ID/indexes" | Select-Object -Expand Content

You should receive a JSON response similar to the following:

    {
      "indexes": [
        {
          "name": "projects/PROJECT_ID/locations/LOCATION/collections/COLLECTION_ID/indexes/INDEX_ID",
          "createTime": "2026-02-05T14:39:53.550302019Z",
          "updateTime": "2026-02-05T14:39:53.550302019Z",
          "distanceMetric": "DOT_PRODUCT",
          "indexField": "plot_embedding",
          "filterFields": [
            "year",
            "genre"
          ],
          "storeFields": [
            "title"
          ]
        }
      ]
    }

### gcloud

Before using any of the command data below, make the following replacements:

  - COLLECTION\_ID : The ID of the collection.
  - LOCATION : The region where you are using Agent Platform.
  - PROJECT\_ID : Your Google Cloud [project ID](https://docs.cloud.google.com/resource-manager/docs/creating-managing-projects#identifying_projects) .

Execute the following command:

#### Linux, macOS, or Cloud Shell

    gcloud vector-search collections indexes list \
      --collection=COLLECTION_ID \
      --location=LOCATION \
      --project=PROJECT_ID

#### Windows (PowerShell)

    gcloud vector-search collections indexes list `
      --collection=COLLECTION_ID `
      --location=LOCATION `
      --project=PROJECT_ID

#### Windows (cmd.exe)

    gcloud vector-search collections indexes list ^
      --collection=COLLECTION_ID ^
      --location=LOCATION ^
      --project=PROJECT_ID

You should receive a response similar to the following:

    ---
    createTime: '2026-02-05T14:39:53.550302019Z'
    distanceMetric: DOT_PRODUCT
    filterFields:
    - year
    - genre
    indexField: plot_embedding
    name: projects/PROJECT_ID/locations/LOCATION/collections/COLLECTION_ID/indexes/INDEX_ID
    storeFields:
    - title
    updateTime: '2026-02-05T14:39:53.550302019Z'

### Python

    from google.cloud import vectorsearch_v1
    
    # Create the client
    vector_search_service_client = vectorsearch_v1.VectorSearchServiceClient()
    
    # Initialize request
    request = vectorsearch_v1.ListIndexesRequest(
        parent="projects/PROJECT_ID/locations/LOCATION/collections/COLLECTION_ID",
    )
    
    # Make the request
    page_result = vector_search_service_client.list_indexes(request=request)
    
    # Handle the response
    for response in page_result:
        print(response)

## Deleting an Index

The following example demonstrates how to delete an existing Index, `  INDEX_ID  ` , from a Collection with the ID `  COLLECTION_ID  ` .

### REST

Before using any of the request data, make the following replacements:

  - INDEX\_ID : The ID of the index.
  - COLLECTION\_ID : The ID of the collection.
  - LOCATION : The region where you are using Agent Platform.
  - PROJECT\_ID : Your Google Cloud [project ID](https://docs.cloud.google.com/resource-manager/docs/creating-managing-projects#identifying_projects) .

HTTP method and URL:

    DELETE https://vectorsearch.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/collections/COLLECTION_ID/indexes/INDEX_ID

To send your request, expand one of these options:

#### curl (Linux, macOS, or Cloud Shell)

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) , or by using [Cloud Shell](https://docs.cloud.google.com/shell/docs) , which automatically logs you into the `gcloud` CLI . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Execute the following command:

    curl -X DELETE \
         -H "Authorization: Bearer $(gcloud auth print-access-token)" \
         "https://vectorsearch.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/collections/COLLECTION_ID/indexes/INDEX_ID"

#### PowerShell (Windows)

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Execute the following command:

    $cred = gcloud auth print-access-token
    $headers = @{ "Authorization" = "Bearer $cred" }
    
    Invoke-WebRequest `
        -Method DELETE `
        -Headers $headers `
        -Uri "https://vectorsearch.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/collections/COLLECTION_ID/indexes/INDEX_ID" | Select-Object -Expand Content

You should receive a JSON response similar to the following:

    {
      "name": "projects/PROJECT_ID/locations/LOCATION/operations/operation-1770303323075-64a14dcb7734e-eb6a75d5-6798cef3",
      "metadata": {
        "@type": "type.googleapis.com/google.cloud.vectorsearch.v1.OperationMetadata",
        "createTime": "2026-02-05T14:55:23.086771813Z",
        "target": "projects/PROJECT_ID/locations/LOCATION/collections/COLLECTION_ID/indexes/INDEX_ID",
        "verb": "delete",
        "requestedCancellation": false,
        "apiVersion": "v1"
      },
      "done": false
    }

### gcloud

Before using any of the command data below, make the following replacements:

  - INDEX\_ID : The ID of the index.
  - COLLECTION\_ID : The ID of the collection.
  - LOCATION : The region where you are using Agent Platform.
  - PROJECT\_ID : Your Google Cloud [project ID](https://docs.cloud.google.com/resource-manager/docs/creating-managing-projects#identifying_projects) .

Execute the following command:

#### Linux, macOS, or Cloud Shell

    gcloud vector-search collections indexes delete INDEX_ID \
      --collection=COLLECTION_ID \
      --location=LOCATION \
      --project=PROJECT_ID

#### Windows (PowerShell)

    gcloud vector-search collections indexes delete INDEX_ID `
      --collection=COLLECTION_ID `
      --location=LOCATION `
      --project=PROJECT_ID

#### Windows (cmd.exe)

    gcloud vector-search collections indexes delete INDEX_ID ^
      --collection=COLLECTION_ID ^
      --location=LOCATION ^
      --project=PROJECT_ID

You should receive a response similar to the following:

    Deleted index [INDEX_ID].

### Python

    from google.cloud import vectorsearch_v1
    
    # Create the client
    vector_search_service_client = vectorsearch_v1.VectorSearchServiceClient()
    
    # Initialize request
    request = vectorsearch_v1.DeleteIndexRequest(
        name="projects/PROJECT_ID/locations/LOCATION/collections/COLLECTION_ID/indexes/INDEX_ID",
    )
    
    # Make the request
    operation = vector_search_service_client.delete_index(request=request)
    
    # Wait for the result (note this may take up to several minutes)
    operation.result()

## What's next?

  - Learn how to [query](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/query-search/query) Data Objects.
  - Learn how to [search for Data Objects](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/query-search/search) using semantic search or hybrid search.
