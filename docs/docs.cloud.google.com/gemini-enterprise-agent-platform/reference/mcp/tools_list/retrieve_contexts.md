---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/retrieve_contexts
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/retrieve_contexts
title: 'MCP Tools Reference: aiplatform.googleapis.com'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

## Tool: `retrieve_contexts`

Retrieves relevant contexts from the specified RAG Engine Corpus via similarity search for the given query. Format: 'projects/{project\_id}/locations/{region}'. CRITICAL: For {region}, use the region specified in the current context window. If no region is specified, prompt the user to provide one. Do not use 'global'. IMPORTANT: The caller must have the `roles/aiplatform.user` IAM role (or `roles/aiplatform.admin` ) on the project that owns the RAG corpus. This grants the required `aiplatform.ragCorpora.query` permission. If the call fails with `403 PERMISSION_DENIED` , the most likely causes are: (1) the caller lacks one of these roles on the corpus's project, or (2) the corpus belongs to a different project than the `parent` argument and no cross-project IAM grant exists. Instruct the user to grant `roles/aiplatform.user` to their principal on the corpus's project before retrying.

**Parameters** \* `parent` : The parent resource, of the form `projects/{project}/locations/{location}` . \* `query` : The query to search for. \* `query.text` : The query text to search for. \* `query.rag_retrieval_config` : The RAG retrieval config to use for the query. \* `query.rag_retrieval_config.top_k` : The number of contexts to retrieve. \* `query.rag_retrieval_config.filter` : The filter config to use for the query. \* `query.rag_retrieval_config.filter.vector_distance_threshold` : The vector distance threshold to use for the query. \* `vertex_rag_store` : The RAG store to use for the query. \* `vertex_rag_store.rag_resources` : a list of RAG resources to use for the query. \* `vertex_rag_store.rag_resources.rag_corpus` : A RAG corpus to use for the query.

The following sample demonstrate how to use `curl` to invoke the `retrieve_contexts` MCP tool.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>Curl Request</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" data-syntax="Bash" translate="no"><code>                  
curl --location &#39;https://aiplatform.googleapis.com/mcp/generate&#39; \
--header &#39;content-type: application/json&#39; \
--header &#39;accept: application/json, text/event-stream&#39; \
--data &#39;{
  &quot;method&quot;: &quot;tools/call&quot;,
  &quot;params&quot;: {
    &quot;name&quot;: &quot;retrieve_contexts&quot;,
    &quot;arguments&quot;: {
      // provide these details according to the tool&#39;s MCP specification
    }
  },
  &quot;jsonrpc&quot;: &quot;2.0&quot;,
  &quot;id&quot;: 1
}&#39;
                </code></pre></td>
</tr>
</tbody>
</table>

## Input Schema

Request message for `VertexRagService.RetrieveContexts` .

### RetrieveContextsRequest

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;parent&quot;: string,&quot;query&quot;: {object (RagQuery)},// Union field data_source can be only one of the following:&quot;vertexRagStore&quot;: {object (VertexRagStore)}// End of list of possible types for union field data_source.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`parent`

`string`

Required. The resource name of the Location from which to retrieve RagContexts. The users must have permission to make a call in the project. Format: `projects/{project}/locations/{location}` .

`query`

` object ( RagQuery  ` )

Required. Single RAG retrieve query.

Union field `data_source` . Data Source to retrieve contexts. `data_source` can be only one of the following:

`vertexRagStore`

` object ( VertexRagStore  ` )

The data source for Vertex RagStore.

### VertexRagStore

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;ragResources&quot;: [{object (RagResource)}],// Union field _vector_distance_threshold can be only one of the following:&quot;vectorDistanceThreshold&quot;: number// End of list of possible types for union field _vector_distance_threshold.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`ragResources[]`

` object ( RagResource  ` )

Optional. The representation of the rag source. It can be used to specify corpus only or ragfiles. Currently only support one corpus or multiple files from one corpus. In the future we may open up multiple corpora support.

Union field `_vector_distance_threshold` .

`_vector_distance_threshold` can be only one of the following:

` vectorDistanceThreshold (deprecated)  `

`number`

> This item is deprecated\!

Optional. Only return contexts with vector distance smaller than the threshold.

### RagResource

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;ragCorpus&quot;: string,
  &quot;ragFileIds&quot;: [
    string
  ]
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`ragCorpus`

`string`

Optional. RagCorpora resource name. Format: `projects/{project}/locations/{location}/ragCorpora/{rag_corpus}`

`ragFileIds[]`

`string`

Optional. rag\_file\_id. The files should be in the same rag\_corpus set in rag\_corpus field.

### RagQuery

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;ragRetrievalConfig&quot;: {object (RagRetrievalConfig)},// Union field query can be only one of the following:&quot;text&quot;: string// End of list of possible types for union field query.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`ragRetrievalConfig`

` object ( RagRetrievalConfig  ` )

Optional. The retrieval config for the query.

Union field `query` . The query to retrieve contexts. Currently only text query is supported. `query` can be only one of the following:

`text`

`string`

Optional. The query in text format to get relevant contexts.

### RagRetrievalConfig

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;topK&quot;: integer,&quot;filter&quot;: {object (Filter)},&quot;ranking&quot;: {object (Ranking)}}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`topK`

`integer`

Optional. The number of contexts to retrieve.

`filter`

` object ( Filter  ` )

Optional. Config for filters.

`ranking`

` object ( Ranking  ` )

Optional. Config for ranking and reranking.

### Filter

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;metadataFilter&quot;: string,// Union field vector_db_threshold can be only one of the following:&quot;vectorDistanceThreshold&quot;: number,&quot;vectorSimilarityThreshold&quot;: number// End of list of possible types for union field vector_db_threshold.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`metadataFilter`

`string`

Optional. String for metadata filtering.

Union field `vector_db_threshold` . Filter contexts retrieved from the vector DB based on either vector distance or vector similarity. `vector_db_threshold` can be only one of the following:

`vectorDistanceThreshold`

`number`

Optional. Only returns contexts with vector distance smaller than the threshold.

`vectorSimilarityThreshold`

`number`

Optional. Only returns contexts with vector similarity larger than the threshold.

### Ranking

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{// Union field ranking_config can be only one of the following:&quot;rankService&quot;: {object (RankService)},&quot;llmRanker&quot;: {object (LlmRanker)}// End of list of possible types for union field ranking_config.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

Union field `ranking_config` . Config options for ranking. Currently only Rank Service is supported. `ranking_config` can be only one of the following:

`rankService`

` object ( RankService  ` )

Optional. Config for Rank Service.

`llmRanker`

` object ( LlmRanker  ` )

Optional. Config for LlmRanker.

### RankService

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{// Union field _model_name can be only one of the following:&quot;modelName&quot;: string// End of list of possible types for union field _model_name.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

Union field `_model_name` .

`_model_name` can be only one of the following:

`modelName`

`string`

Optional. The model name of the rank service. Format: `semantic-ranker-512@latest`

### LlmRanker

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{// Union field _model_name can be only one of the following:&quot;modelName&quot;: string// End of list of possible types for union field _model_name.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

Union field `_model_name` .

`_model_name` can be only one of the following:

`modelName`

`string`

Optional. The model name used for ranking. See [Supported models](https://cloud.google.com/vertex-ai/generative-ai/docs/model-reference/inference#supported-models) .

## Output Schema

Response message for `VertexRagService.RetrieveContexts` .

### RetrieveContextsResponse

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;contexts&quot;: {object (RagContexts)}}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`contexts`

` object ( RagContexts  ` )

The contexts of the query.

### RagContexts

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;contexts&quot;: [{object (Context)}]}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`contexts[]`

` object ( Context  ` )

All its contexts.

### Context

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;sourceUri&quot;: string,&quot;sourceDisplayName&quot;: string,&quot;text&quot;: string,&quot;chunk&quot;: {object (RagChunk)},// Union field _score can be only one of the following:&quot;score&quot;: number// End of list of possible types for union field _score.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`sourceUri`

`string`

If the file is imported from Cloud Storage or Google Drive, source\_uri will be original file URI in Cloud Storage or Google Drive; if file is uploaded, source\_uri will be file display name.

`sourceDisplayName`

`string`

The file display name.

`text`

`string`

The text chunk.

`chunk`

` object ( RagChunk  ` )

Context of the retrieved chunk.

Union field `_score` .

`_score` can be only one of the following:

`score`

`number`

According to the underlying Vector DB and the selected metric type, the score can be either the distance or the similarity between the query and the context and its range depends on the metric type.

For example, if the metric type is COSINE\_DISTANCE, it represents the distance between the query and the context. The larger the distance, the less relevant the context is to the query. The range is \[0, 2\], while 0 means the most relevant and 2 means the least relevant.

### RagChunk

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;text&quot;: string,// Union field _page_span can be only one of the following:&quot;pageSpan&quot;: {object (PageSpan)}// End of list of possible types for union field _page_span.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`text`

`string`

The content of the chunk.

Union field `_page_span` .

`_page_span` can be only one of the following:

`pageSpan`

` object ( PageSpan  ` )

If populated, represents where the chunk starts and ends in the document.

### PageSpan

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;firstPage&quot;: integer,
  &quot;lastPage&quot;: integer
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`firstPage`

`integer`

Page where chunk starts in the document. Inclusive. 1-indexed.

`lastPage`

`integer`

Page where chunk ends in the document. Inclusive. 1-indexed.

### Tool Annotations

Destructive Hint: ❌ | Idempotent Hint: ✅ | Read Only Hint: ✅ | Open World Hint: ❌
