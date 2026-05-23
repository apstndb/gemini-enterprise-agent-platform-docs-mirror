---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/ExportEvaluatedDataItemsConfig
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/ExportEvaluatedDataItemsConfig
title: ExportEvaluatedDataItemsConfig
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Configuration for exporting test set predictions to a BigQuery table.

Fields

`destinationBigqueryUri` `string`

URI of desired destination BigQuery table. Expected format: `bq://{projectId}:{datasetId}:{table}`

If not specified, then results are exported to the following auto-created BigQuery table: `{projectId}:export_evaluated_examples_{modelName}_{yyyy_MM_dd'T'HH_mm_ss_SSS'Z'}.evaluated_examples`

`overrideExistingTable` `boolean`

If true and an export destination is specified, then the contents of the destination are overwritten. Otherwise, if the export destination already exists, then the export operation fails.

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
  &quot;destinationBigqueryUri&quot;: string,
  &quot;overrideExistingTable&quot;: boolean
}</code></pre></td>
</tr>
</tbody>
</table>
