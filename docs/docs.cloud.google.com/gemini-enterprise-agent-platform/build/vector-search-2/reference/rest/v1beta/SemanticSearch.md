---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/rest/v1beta/SemanticSearch
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/rest/v1beta/SemanticSearch
title: SemanticSearch
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Defines a semantic search operation.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;searchText&quot;: string,&quot;searchField&quot;: string,&quot;taskType&quot;: enum (EmbeddingTaskType),&quot;outputFields&quot;: {object (OutputFields)},&quot;filter&quot;: {object},&quot;searchHint&quot;: {object (SearchHint)},&quot;topK&quot;: integer}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`searchText`

`string`

Required. The query text, which is used to generate an embedding according to the embedding model specified in the collection config.

`searchField`

`string`

Required. The vector field to search.

`taskType`

` enum ( EmbeddingTaskType  ` )

Required. The task type of the query embedding.

`outputFields`

` object ( OutputFields  ` )

Optional. The fields to return in the search results.

`filter`

` object ( Struct  ` format)

Optional. A JSON filter expression, e.g. {"genre": {"$eq": "sci-fi"}}, represented as a google.protobuf.Struct.

`searchHint`

` object ( SearchHint  ` )

Optional. Sets the search hint. If no strategy is specified, the service will use an index if one is available, and fall back to KNN search otherwise.

`topK`

`integer`

Optional. The number of data objects to return.
