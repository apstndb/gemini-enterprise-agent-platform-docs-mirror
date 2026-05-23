---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search/using-metadata
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search/using-metadata
title: Vector Search embeddings with metadata
description: Learn how to use Vector Search embeddings with metadata.
data_source: docs.cloud.google.com
---

> **Preview**
> 
> This feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](https://docs.cloud.google.com/terms/service-terms#1) . Pre-GA features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

This guide provides information about optional metadata for vector embeddings. Vector Search lets you define metadata for each embedding.

Metadata is non-filterable, arbitrary information that Vector Search can store for each embedding. This can provide embeddings with useful context such as:

  - Product details, such as name, price, and an image URL.

  - Descriptions, snippets, dates, and authorship for text embeddings.

  - User information for user embeddings.

  - Coordinates for place embeddings.

## Key features and benefits

Features and benefits of using metadata include:

  - **Context with results** : Information can be provided directly in your search results, which eliminates the need for separate lookups and reduces latency.

  - **Flexible structure** : Metadata is provided as a **JSON object** , which allows the metadata to be defined as complex, nested data.

  - **Non-Filterable** : Vector embedding metadata is for storing and retrieving non-filterable information that's distinct from `restricts` and `numeric_restricts` .

  - **Efficient updates** : The `update_mask` field lets you specify that APIs *only* update metadata to avoid resubmitting embedding vectors.

  - **Decoupled Information** : Non-filterable information can be separated from filterable attributes like `restricts` .

  - **Streamlined development** : Search responses include metadata associated with a vector embedding, while reducing the complexity needed for features such as displaying rich search results and performing context-based post-processing.

## Data format

An optional `embedding_metadata` field holds a JSON object that flexibly associates rich, non-filterable information with embeddings in Vector Search. This can streamline applications by returning context with results and allows efficient metadata-only updates using `update_mask` for the `upsertDatapoints` API.

> **Note:** Use `restricts` and `numeric_restricts` for filtering data.

Example data point structure:

``` 
    {
        "id": "movie_001",
        "embedding": [0.1, 0.2, ..., 0.3],
        "sparse_embedding": {
            "values": [-0.4, 0.2, -1.3],
            "dimensions": [10, 20, 30]
        },
        "numeric_restricts": [{'namespace': 'year', 'value_int': 2022}],
        "restricts": [{'namespace': 'genre', 'allow': ['action', 'comedy']}],

        # --- New embedding_metadata field ---
        "embedding_metadata": {
            "title": "Ballet Train",
            "runtime": {
                "hours": 2,
                "minutes": 6
            },
            "review_info": {
                "review": "This movie is fun and...",
                "rotten_potatoes_rating": 76
            }
        }
        # ------------------------------------
    },
    # ... other data points
```

## Ingesting data with `embedding_metadata`

When adding data points, you can include `embedding_metadata` when one of the following actions occurs:

  - Uploading a file (Cloud Storage):
      - Use **JSON** or **AVRO** [formats](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search/format-structure) . **CSV isn't supported** for `embedding_metadata` .
  - Using the `upsertDatapoints` API:
      - Pass data point objects (including `embedding_metadata` ) in the API request payload.

> **Note:** `embedding_metadata` has a size limit of 2 KB for each datapoint.

## Retrieving `embedding_metadata` during queries

When performing a standard nearest-neighbor search using the `findNeighbors` API, the `embedding_metadata` field for each neighbor is **automatically included** in the response if `returnFullDatapoint` is set to `True` .

### curl

    curl -X POST -H "Authorization: Bearer $(gcloud auth print-access-token)" \
    "https://${PUBLIC_ENDPOINT_DOMAIN}/v1/projects/${PROJECT_ID}/locations/${LOCATION}/indexEndpoints/${INDEX_ENDPOINT_ID}:findNeighbors" \
    -d '{deployedIndexId:"${DEPLOYED_INDEX_ID}", "queries":[{datapoint:{"featureVector":"<FEATURE_VECTOR>"}}], returnFullDatapoint:true}'

## Updating `embedding_metadata`

Update metadata using the `upsertDatapoints` API and an `update_mask` using the value `embedding_metadata` . The `update_mask` field might also include additional mask values. For uses of a field mask, see [Update embedding metadata](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search/update-rebuild-index#upsert-metadata) .

The `update_mask` field helps to ensure that only `embedding_metadata` is updated, avoiding resubmission of restrict and embedding fields.

> **Note:** This can also include existing `FieldMask` values, such as [all\_restricts](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search/update-rebuild-index#upsert-metadata) , along with `embedding_metadata` in the request.

The following example demonstrates how to define and update metadata to create a targeted `IndexDatapoint` , specifying `update_mask` , and calling `upsertDatapoints` .

### curl

    curl -H "Content-Type: application/json" -H "Authorization: Bearer `gcloud auth print-access-token`" https://${LOCATION}-aiplatform.googleapis.com/v1/projects/${PROJECT_ID}/locations/${LOCATION}/indexes/${INDEX_ID}:upsertDatapoints \
    -d '{
    datapoints:[
        {
            datapoint_id: "'${DATAPOINT_ID_1}'",
            feature_vector: [...],
            embedding_metadata:{"title": "updated title", "rating": 4.5, "tags": ["updated", "reviewed"]
        }, update_mask: "embedding_metadata"}'
