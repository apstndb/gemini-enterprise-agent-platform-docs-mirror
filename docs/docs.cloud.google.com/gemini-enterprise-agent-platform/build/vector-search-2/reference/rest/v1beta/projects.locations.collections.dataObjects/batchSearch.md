---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/rest/v1beta/projects.locations.collections.dataObjects/batchSearch
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/rest/v1beta/projects.locations.collections.dataObjects/batchSearch
title: 'Method: projects.locations.collections.dataObjects.batchSearch'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Batch searches data objects.

### HTTP request

`POST https://vectorsearch.googleapis.com/v1beta/{parent}/dataObjects:batchSearch`

### Path parameters

Parameters

`parent`

`string`

Required. The resource name of the Collection for which to search. Format: `projects/{project}/locations/{location}/collections/{collection}`

### Request body

The request body contains data with the following structure:

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;searches&quot;: [{object (Search)}],&quot;combine&quot;: {object (CombineResultsOptions)}}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`searches[]`

` object ( Search  ` )

Required. A list of search requests to execute in parallel.

`combine`

` object ( CombineResultsOptions  ` )

Optional. Options for combining the results of the batch search operations.

### Response body

A response from a batch search operation.

If successful, the response body contains data with the following structure:

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;results&quot;: [{object (SearchDataObjectsResponse)}]}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`results[]`

` object ( SearchDataObjectsResponse  ` )

Output only. A list of search responses, one for each request in the batch. If a ranker is used, a single ranked list of results is returned.

### Authorization scopes

Requires the following OAuth scope:

  - `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .

### IAM Permissions

Requires the following [IAM](https://cloud.google.com/iam/docs) permission on the `parent` resource:

  - `vectorsearch.dataObjects.search`

For more information, see the [IAM documentation](https://cloud.google.com/iam/docs) .

## Search

A single search request within a batch operation.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{// Union field search_type can be only one of the following:&quot;vectorSearch&quot;: {object (VectorSearch)},&quot;semanticSearch&quot;: {object (SemanticSearch)},&quot;textSearch&quot;: {object (TextSearch)}// End of list of possible types for union field search_type.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

Union field `search_type` . The type of search to perform. `search_type` can be only one of the following:

`vectorSearch`

` object ( VectorSearch  ` )

A vector-based search.

`semanticSearch`

` object ( SemanticSearch  ` )

A semantic search.

`textSearch`

` object ( TextSearch  ` )

A text search operation.

## CombineResultsOptions

Options for combining the results of the batch search operations.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;ranker&quot;: {object (Ranker)},&quot;outputFields&quot;: {object (OutputFields)},&quot;topK&quot;: integer}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`ranker`

` object ( Ranker  ` )

Required. The ranker to use for combining the results.

`outputFields`

` object ( OutputFields  ` )

Optional. Mask specifying which fields to return.

`topK`

`integer`

Optional. The number of results to return. If not set, a default value will be used.

## Ranker

Defines a ranker to combine results from multiple searches.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{// Union field ranker can be only one of the following:&quot;rrf&quot;: {object (ReciprocalRankFusion)}// End of list of possible types for union field ranker.// Union field reranker can be only one of the following:&quot;vertexRanker&quot;: {object (VertexRanker)}// End of list of possible types for union field reranker.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

Union field `ranker` . The ranking method to use. `ranker` can be only one of the following:

`rrf`

` object ( ReciprocalRankFusion  ` )

Reciprocal Rank Fusion ranking.

Union field `reranker` . The reranker to use for final ranking of the results combined by the ranker. `reranker` can be only one of the following:

`vertexRanker`

` object ( VertexRanker  ` )

Optional. Vertex AI ranking.

## ReciprocalRankFusion

Defines the Reciprocal Rank Fusion (RRF) algorithm for result ranking.

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
  &quot;weights&quot;: [
    number
  ]
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`weights[]`

`number`

Required. The weights to apply to each search result set during fusion.

## VertexRanker

Defines a ranker using the Vertex AI ranking service. See <https://cloud.google.com/generative-ai-app-builder/docs/ranking> for details.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;model&quot;: string,&quot;topN&quot;: integer,// Union field record_spec can be only one of the following:&quot;textRecordSpec&quot;: {object (TextRecordSpec)}// End of list of possible types for union field record_spec.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`model`

`string`

Required. The model used for ranking documents. The list of available models is described in <https://docs.cloud.google.com/generative-ai-app-builder/docs/ranking#models> . Currently, only `semantic-ranker-fast@latest` is supported.

`topN`

`integer`

Required. The number of documents to be processed for ranking.

Union field `record_spec` . The record specification for ranking. At least one record spec must be set. `record_spec` can be only one of the following:

`textRecordSpec`

` object ( TextRecordSpec  ` )

The record spec for text search.

## TextRecordSpec

The record spec for text search.

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
  &quot;query&quot;: string,
  &quot;titleTemplate&quot;: string,
  &quot;contentTemplate&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`query`

`string`

Required. The query against which the records are ranked and scored.

`titleTemplate`

`string`

Optional. The template used to generate the record's title.

`contentTemplate`

`string`

Optional. The template used to generate the record's content.
