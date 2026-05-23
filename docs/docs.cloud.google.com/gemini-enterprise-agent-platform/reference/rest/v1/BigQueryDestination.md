---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/BigQueryDestination
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/BigQueryDestination
title: BigQueryDestination
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

The BigQuery location for the output content.

Fields

`outputUri` `string`

Required. BigQuery URI to a project or table, up to 2000 characters long.

When only the project is specified, the Dataset and Table is created. When the full table reference is specified, the Dataset must exist and table must not exist.

Accepted forms:

  - BigQuery path. For example: `bq://projectId` or `bq://projectId.bqDatasetId` or `bq://projectId.bqDatasetId.bqTableId` .

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
  &quot;outputUri&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>
