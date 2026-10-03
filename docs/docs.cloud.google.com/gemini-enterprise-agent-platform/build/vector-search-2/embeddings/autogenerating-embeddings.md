---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/embeddings/autogenerating-embeddings
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/embeddings/autogenerating-embeddings
title: Autogenerating embeddings for Agent Retrieval
description: Autogenerate embeddings for Agent Retrieval (formerly Vector Search 2.0)
data_source: docs.cloud.google.com
---

You can use Agent Retrieval (formerly Vector Search 2.0) to autogenerate embeddings for your [Collections](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/collections/collections) . This lets you build new embeddings and deploy them instantly, which streamlines the path from raw data to a live production-scale search engine.

## Supported Gemini Enterprise embedding models

> **Note:** Support for embedding models is subject to Gemini Enterprise versioning and lifecycle guidelines. For more information, including retirement dates, see [Model versions and lifecycle](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/model-versions) .

Agent Retrieval (formerly Vector Search 2.0) supports the following embedding models:

- Gemini — Provides state-of-the-art performance for embedding text (English-only and multilingual).

- Text — Specializes in (English-only and multilingual) and source code data.

> **Note:** Support for multimodal embedding ( `multimodalembedding@001` ) is coming soon.

The following table provides details on each supported model.

| Model                             | Description                                                                                                                                                                                                                                         | Max output dimensions | Max sequence length (tokens) | Supported modalities and text languages                                                                                                                  | Additional limits                                                                                                                   |
|-----------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------------|------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------|
| `gemini-embedding-001`            | State-of-the-art performance across English, multilingual and code tasks. It unifies the previously specialized models like `text-embedding-005` and `text-multilingual-embedding-002` and achieves better performance in their respective domains. | 3072                  | 2048                         | [Supported text languages](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/models/text-embeddings-api#supported_text_languages) | [Embedding limits](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/quotas#text-embedding-limits)    |
| `gemini-embedding-2-preview`      | This is a next-generation multimodal embedding model from Google. Built on on the latest Gemini model architecture, this "omni embedding model" maps text, image, video, and PDF data into a single, unified embedding space.                       | 3072                  | 8192                         | Interleaved text, image, video, and PDF                                                                                                                  | [API limits](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/embeddings/get-multimodal-embeddings#api-limits) |
| `gemini-embedding-2`              | This is a next-generation multimodal embedding model from Google. Built on on the latest Gemini model architecture, this "omni embedding model" maps text, image, video, and PDF data into a single, unified embedding space.                       | 3072                  | 8192                         | Interleaved text, image, video, and PDF                                                                                                                  | [API limits](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/embeddings/get-multimodal-embeddings#api-limits) |
| `text-embedding-004`              | Specialized in English and code tasks.                                                                                                                                                                                                              | 768                   | 2048                         | English                                                                                                                                                  | [API limits](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/embeddings/get-text-embeddings#api_limits)       |
| `text-embedding-005`              | Specialized in English and code tasks.                                                                                                                                                                                                              | 768                   | 2048                         | English                                                                                                                                                  | [API limits](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/embeddings/get-text-embeddings#api_limits)       |
| `text-multilingual-embedding-002` | Specialized in multilingual tasks.                                                                                                                                                                                                                  | 768                   | 2048                         | [Supported text languages](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/models/text-embeddings-api#supported_text_languages) | [API limits](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/embeddings/get-text-embeddings#api_limits)       |

> **Note:** For `gemini-embedding-001` technical details, go to [Gemini Embedding: Generalizable Embeddings from Gemini](https://deepmind.google/research/publications/157741/) .

## Creating Collections with autogenerated embeddings

When creating a Collection, specify the embedding model in the `model_id` field of `vertex_embedding_config` . This model is used whenever a [Data Object](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/data-objects/data-objects) is created without `genre_embedding` data defined.

The following code demonstrates how to specify the embedding model to use when autogenerating embeddings.

```
request = vectorsearch.CreateCollectionRequest(
   parent=f"projects/{PROJECT_ID}/locations/{LOCATION}",
   collection_id=collection_id,
   collection={
       "data_schema": {
           "type": "object",
           "properties": {
               "year": {"type": "number"},
               "genre": {"type": "string"},
               "director": {"type": "string"},
               "title": {"type": "string"},
           },
       },
       "vector_schema": {
           "plot_embedding": {"dense_vector": {"dimensions": 3} },
           "soundtrack_embedding": {"dense_vector": {"dimensions": 5} },
           "genre_embedding": {
               "dense_vector": {
                   "dimensions": 4,
                   "vertex_embedding_config": {
                       # If a data object is created without a supplied value for genre_embedding, it will be
                       # auto-generated based on this config.
                       "model_id": "text-embedding-004",
                       "text_template": ("Movie: {title} Genre: {genre} Year: {year}"),
                       "task_type": "RETRIEVAL_DOCUMENT",
                   },
               }
           },
           "sparse_embedding": {"sparse_vector": { } },
       },
   },
)
operation = vector_search_service_client.create_collection(request=request)
operation.result()
```

In the example code, a new Collection is created with the `model_id` field set to `text-embedding-004` . See [Supported Gemini Enterprise embedding models](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/embeddings/autogenerating-embeddings#supported-models) for which embedding models can be specified for `model_id` .

## Quotas

Autogenerated embeddings rely on on customer quotas for the underlying Gemini Enterprise embedding models. This is primarily constrained by two main quotas:

- Embed content input tokens per minute per region per base_model.

- Online prediction requests per base model per minute per region per base_model.

Make sure you have enough quota before creating Data Objects or running an import job.

See [Manage your quota using the console](https://docs.cloud.google.com/docs/quotas/view-manage#viewing_your_quota_console) for information on how to request larger quotas.

## See also

- [Collections](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/collections/collections)
- [Indexes](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/indexes/indexes)
- [Data Objects](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/data-objects/data-objects)
