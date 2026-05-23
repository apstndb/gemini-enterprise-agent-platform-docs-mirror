---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/rest/v1/TextSearch
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/rest/v1/TextSearch
title: TextSearch
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Defines a text search operation.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;searchText&quot;: string,&quot;dataFieldNames&quot;: [string],&quot;outputFields&quot;: {object (OutputFields)},&quot;filter&quot;: {object},&quot;topK&quot;: integer}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`searchText`

`string`

Required. The query text.

`dataFieldNames[]`

`string`

Required. The data field names to search.

`outputFields`

` object ( OutputFields  ` )

Optional. The fields to return in the search results.

`filter`

` object ( Struct  ` format)

Optional. A JSON filter expression, e.g. `{"genre": {"$eq": "sci-fi"}}` , represented as a `google.protobuf.Struct` .

`topK`

`integer`

Optional. The number of results to return.
