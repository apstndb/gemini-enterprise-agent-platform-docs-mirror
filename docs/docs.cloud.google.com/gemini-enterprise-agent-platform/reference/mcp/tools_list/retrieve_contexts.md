---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/retrieve_contexts
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/retrieve_contexts
title: 'MCP Tools Reference: aiplatform.googleapis.com'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

## Tool: `retrieve_contexts`

Retrieves relevant contexts from the specified RAG Engine Corpus via similarity search for the given query. Format: 'projects/{project_id}/locations/{region}'. CRITICAL: For {region}, use the region specified in the current context window. If no region is specified, prompt the user to provide one. Do not use 'global'. IMPORTANT: The caller must have the `roles/aiplatform.user` IAM role (or `roles/aiplatform.admin` ) on the project that owns the RAG corpus. This grants the required `aiplatform.ragCorpora.query` permission. If the call fails with `403 PERMISSION_DENIED` , the most likely causes are: (1) the caller lacks one of these roles on the corpus's project, or (2) the corpus belongs to a different project than the `parent` argument and no cross-project IAM grant exists. Instruct the user to grant `roles/aiplatform.user` to their principal on the corpus's project before retrying.

**Parameters** \* `parent` : The parent resource, of the form `projects/{project}/locations/{location}` . \* `query` : The query to search for. \* `query.text` : The query text to search for. \* `query.rag_retrieval_config` : The RAG retrieval config to use for the query. \* `query.rag_retrieval_config.top_k` : The number of contexts to retrieve. \* `query.rag_retrieval_config.filter` : The filter config to use for the query. \* `query.rag_retrieval_config.filter.vector_distance_threshold` : The vector distance threshold to use for the query. \* `vertex_rag_store` : The RAG store to use for the query. \* `vertex_rag_store.rag_resources` : a list of RAG resources to use for the query. \* `vertex_rag_store.rag_resources.rag_corpus` : A RAG corpus to use for the query.

The following sample demonstrate how to use `curl` to invoke the `retrieve_contexts` MCP tool.

**Curl Request**

```
curl --location 'https://aiplatform.googleapis.com/mcp/generate' \
--header 'content-type: application/json' \
--header 'accept: application/json, text/event-stream' \
--data '{
  "method": "tools/call",
  "params": {
    "name": "retrieve_contexts",
    "arguments": {
      // provide these details according to the tool's MCP specification
    }
  },
  "jsonrpc": "2.0",
  "id": 1
}'
```

## Input Schema

Request message for `VertexRagService.RetrieveContexts` .

### RetrieveContextsRequest

**JSON representation**

```
{
  "parent": string,
  "query": {
    object (RagQuery)
  },

  // Union field data_source can be only one of the following:
  "vertexRagStore": {
    object (VertexRagStore)
  }
  // End of list of possible types for union field data_source.
}
```

| Fields                                                                                                        |                                                                                                                                                                                                               |
|---------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `parent`                                                                                                      | `string` Required. The resource name of the Location from which to retrieve RagContexts. The users must have permission to make a call in the project. Format: `projects/{project}/locations/{location}` .    |
| `query`                                                                                                       | `object ( `[`RagQuery`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/retrieve_contexts#Input.Schema.RagQuery)` )` Required. Single RAG retrieve query.             |
| Union field `data_source` . Data Source to retrieve contexts. `data_source` can be only one of the following: |                                                                                                                                                                                                               |
| `vertexRagStore`                                                                                              | `object ( `[`VertexRagStore`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/retrieve_contexts#Input.Schema.VertexRagStore)` )` The data source for Vertex RagStore. |

### VertexRagStore

**JSON representation**

```
{
  "ragResources": [
    {
      object (RagResource)
    }
  ],

  // Union field _vector_distance_threshold can be only one of the following:
  "vectorDistanceThreshold": number
  // End of list of possible types for union field _vector_distance_threshold.
}
```

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Fields</th>
<th></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code>ragResources[]</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/retrieve_contexts#Input.Schema.RagResource"><code>RagResource</code></a><code> )</code></p>
<p>Optional. The representation of the rag source. It can be used to specify corpus only or ragfiles. Currently only support one corpus or multiple files from one corpus. In the future we may open up multiple corpora support.</p></td>
</tr>
<tr class="even">
<td><p>Union field <code>_vector_distance_threshold</code> .</p>
<p><code>_vector_distance_threshold</code> can be only one of the following:</p></td>
<td></td>
</tr>
<tr class="odd">
<td><code>vectorDistanceThreshold </code><strong><code>(deprecated)</code></strong></td>
<td><p><code>number</code></p>
<blockquote>
<p>This item is deprecated!</p>
</blockquote>
<p>Optional. Only return contexts with vector distance smaller than the threshold.</p></td>
</tr>
</tbody>
</table>

### RagResource

**JSON representation**

```
{
  "ragCorpus": string,
  "ragFileIds": [
    string
  ]
}
```

| Fields         |                                                                                                                        |
|----------------|------------------------------------------------------------------------------------------------------------------------|
| `ragCorpus`    | `string` Optional. RagCorpora resource name. Format: `projects/{project}/locations/{location}/ragCorpora/{rag_corpus}` |
| `ragFileIds[]` | `string` Optional. rag_file_id. The files should be in the same rag_corpus set in rag_corpus field.                    |

### RagQuery

**JSON representation**

```
{
  "ragRetrievalConfig": {
    object (RagRetrievalConfig)
  },

  // Union field query can be only one of the following:
  "text": string
  // End of list of possible types for union field query.
}
```

| Fields                                                                                                                                  |                                                                                                                                                                                                                                |
|-----------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `ragRetrievalConfig`                                                                                                                    | `object ( `[`RagRetrievalConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/retrieve_contexts#Input.Schema.RagRetrievalConfig)` )` Optional. The retrieval config for the query. |
| Union field `query` . The query to retrieve contexts. Currently only text query is supported. `query` can be only one of the following: |                                                                                                                                                                                                                                |
| `text`                                                                                                                                  | `string` Optional. The query in text format to get relevant contexts.                                                                                                                                                          |

### RagRetrievalConfig

**JSON representation**

```
{
  "topK": integer,
  "filter": {
    object (Filter)
  },
  "ranking": {
    object (Ranking)
  }
}
```

| Fields    |                                                                                                                                                                                                        |
|-----------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `topK`    | `integer` Optional. The number of contexts to retrieve.                                                                                                                                                |
| `filter`  | `object ( `[`Filter`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/retrieve_contexts#Input.Schema.Filter)` )` Optional. Config for filters.                 |
| `ranking` | `object ( `[`Ranking`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/retrieve_contexts#Input.Schema.Ranking)` )` Optional. Config for ranking and reranking. |

### Filter

**JSON representation**

```
{
  "metadataFilter": string,

  // Union field vector_db_threshold can be only one of the following:
  "vectorDistanceThreshold": number,
  "vectorSimilarityThreshold": number
  // End of list of possible types for union field vector_db_threshold.
}
```

| Fields                                                                                                                                                                                         |                                                                                            |
|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------|
| `metadataFilter`                                                                                                                                                                               | `string` Optional. String for metadata filtering.                                          |
| Union field `vector_db_threshold` . Filter contexts retrieved from the vector DB based on either vector distance or vector similarity. `vector_db_threshold` can be only one of the following: |                                                                                            |
| `vectorDistanceThreshold`                                                                                                                                                                      | `number` Optional. Only returns contexts with vector distance smaller than the threshold.  |
| `vectorSimilarityThreshold`                                                                                                                                                                    | `number` Optional. Only returns contexts with vector similarity larger than the threshold. |

### Ranking

**JSON representation**

```
{

  // Union field ranking_config can be only one of the following:
  "rankService": {
    object (RankService)
  },
  "llmRanker": {
    object (LlmRanker)
  }
  // End of list of possible types for union field ranking_config.
}
```

| Fields                                                                                                                                                  |                                                                                                                                                                                                       |
|---------------------------------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Union field `ranking_config` . Config options for ranking. Currently only Rank Service is supported. `ranking_config` can be only one of the following: |                                                                                                                                                                                                       |
| `rankService`                                                                                                                                           | `object ( `[`RankService`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/retrieve_contexts#Input.Schema.RankService)` )` Optional. Config for Rank Service. |
| `llmRanker`                                                                                                                                             | `object ( `[`LlmRanker`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/retrieve_contexts#Input.Schema.LlmRanker)` )` Optional. Config for LlmRanker.        |

### RankService

**JSON representation**

```
{

  // Union field _model_name can be only one of the following:
  "modelName": string
  // End of list of possible types for union field _model_name.
}
```

| Fields                                                                      |                                                                                             |
|-----------------------------------------------------------------------------|---------------------------------------------------------------------------------------------|
| Union field `_model_name` . `_model_name` can be only one of the following: |                                                                                             |
| `modelName`                                                                 | `string` Optional. The model name of the rank service. Format: `semantic-ranker-512@latest` |

### LlmRanker

**JSON representation**

```
{

  // Union field _model_name can be only one of the following:
  "modelName": string
  // End of list of possible types for union field _model_name.
}
```

| Fields                                                                      |                                                                                                                                                                                |
|-----------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Union field `_model_name` . `_model_name` can be only one of the following: |                                                                                                                                                                                |
| `modelName`                                                                 | `string` Optional. The model name used for ranking. See [Supported models](https://cloud.google.com/vertex-ai/generative-ai/docs/model-reference/inference#supported-models) . |

## Output Schema

Response message for `VertexRagService.RetrieveContexts` .

### RetrieveContextsResponse

**JSON representation**

```
{
  "contexts": {
    object (RagContexts)
  }
}
```

| Fields     |                                                                                                                                                                                                |
|------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `contexts` | `object ( `[`RagContexts`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/retrieve_contexts#Output.Schema.RagContexts)` )` The contexts of the query. |

### RagContexts

**JSON representation**

```
{
  "contexts": [
    {
      object (Context)
    }
  ]
}
```

| Fields       |                                                                                                                                                                               |
|--------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `contexts[]` | `object ( `[`Context`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/retrieve_contexts#Output.Schema.Context)` )` All its contexts. |

### Context

**JSON representation**

```
{
  "sourceUri": string,
  "sourceDisplayName": string,
  "text": string,
  "chunk": {
    object (RagChunk)
  },

  // Union field _score can be only one of the following:
  "score": number
  // End of list of possible types for union field _score.
}
```

| Fields                                                            |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
|-------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `sourceUri`                                                       | `string` If the file is imported from Cloud Storage or Google Drive, source_uri will be original file URI in Cloud Storage or Google Drive; if file is uploaded, source_uri will be file display name.                                                                                                                                                                                                                                                                                           |
| `sourceDisplayName`                                               | `string` The file display name.                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| `text`                                                            | `string` The text chunk.                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
| `chunk`                                                           | `object ( `[`RagChunk`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/retrieve_contexts#Output.Schema.RagChunk)` )` Context of the retrieved chunk.                                                                                                                                                                                                                                                                                                    |
| Union field `_score` . `_score` can be only one of the following: |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| `score`                                                           | `number` According to the underlying Vector DB and the selected metric type, the score can be either the distance or the similarity between the query and the context and its range depends on the metric type. For example, if the metric type is COSINE_DISTANCE, it represents the distance between the query and the context. The larger the distance, the less relevant the context is to the query. The range is \[0, 2\], while 0 means the most relevant and 2 means the least relevant. |

### RagChunk

**JSON representation**

```
{
  "text": string,

  // Union field _page_span can be only one of the following:
  "pageSpan": {
    object (PageSpan)
  }
  // End of list of possible types for union field _page_span.
}
```

| Fields                                                                    |                                                                                                                                                                                                                                         |
|---------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `text`                                                                    | `string` The content of the chunk.                                                                                                                                                                                                      |
| Union field `_page_span` . `_page_span` can be only one of the following: |                                                                                                                                                                                                                                         |
| `pageSpan`                                                                | `object ( `[`PageSpan`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/retrieve_contexts#Output.Schema.PageSpan)` )` If populated, represents where the chunk starts and ends in the document. |

### PageSpan

**JSON representation**

```
{
  "firstPage": integer,
  "lastPage": integer
}
```

| Fields      |                                                                          |
|-------------|--------------------------------------------------------------------------|
| `firstPage` | `integer` Page where chunk starts in the document. Inclusive. 1-indexed. |
| `lastPage`  | `integer` Page where chunk ends in the document. Inclusive. 1-indexed.   |

### Tool Annotations

Destructive Hint: ❌ \| Idempotent Hint: ✅ \| Read Only Hint: ✅ \| Open World Hint: ❌
