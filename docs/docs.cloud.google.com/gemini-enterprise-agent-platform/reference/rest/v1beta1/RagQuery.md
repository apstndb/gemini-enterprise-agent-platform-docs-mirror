---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/RagQuery
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/RagQuery
title: RagQuery
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

A query to retrieve relevant contexts.

Fields

` similarityTopK (deprecated)  ` `integer`

> This item is deprecated\!

Optional. The number of contexts to retrieve.

` ranking (deprecated)  ` ` object ( Ranking  ` )

> This item is deprecated\!

Optional. Configurations for hybrid search results ranking.

`ragRetrievalConfig` ` object ( RagRetrievalConfig  ` )

Optional. The retrieval config for the query.

`query` `Union type`

The query to retrieve contexts. Currently only text query is supported. `query` can be only one of the following:

`text` `string`

Optional. The query in text format to get relevant contexts.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;similarityTopK&quot;: integer,&quot;ranking&quot;: {object (Ranking)},&quot;ragRetrievalConfig&quot;: {object (RagRetrievalConfig)},// query&quot;text&quot;: string// Union type}</code></pre></td>
</tr>
</tbody>
</table>

## Ranking

Configurations for hybrid search results ranking.

Fields

`alpha` `number`

Optional. Alpha value controls the weight between dense and sparse vector search results. The range is \[0, 1\], while 0 means sparse vector search only and 1 means dense vector search only. The default value is 0.5 which balances sparse and dense vector search equally.

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
  &quot;alpha&quot;: number
}</code></pre></td>
</tr>
</tbody>
</table>
