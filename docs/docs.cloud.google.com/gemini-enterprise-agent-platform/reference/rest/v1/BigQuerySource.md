---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/BigQuerySource
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/BigQuerySource
title: BigQuerySource
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

The BigQuery location for the input content.

Fields

`inputUri` `string`

Required. BigQuery URI to a table, up to 2000 characters long. Accepted forms:

  - BigQuery path. For example: `bq://projectId.bqDatasetId.bqTableId` .

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
  &quot;inputUri&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>
