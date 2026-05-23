---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/RagQuery
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/RagQuery
title: RagQuery
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

A query to retrieve relevant contexts.

Fields

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;ragRetrievalConfig&quot;: {object (RagRetrievalConfig)},// query&quot;text&quot;: string// Union type}</code></pre></td>
</tr>
</tbody>
</table>
