---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/ExportDataResponse
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/ExportDataResponse
title: ExportDataResponse
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Response message for `  DatasetService.ExportData  ` .

Fields

`exportedFiles[]` `string`

All of the files that are exported in this export operation. For custom code training export, only three (training, validation and test) Cloud Storage paths in wildcard format are populated (for example, gs://.../training-\*).

`dataStats` ` object ( DataStats  ` )

Only present for custom code training export use case. Records data stats, i.e., train/validation/test item/annotation counts calculated during the export operation.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;exportedFiles&quot;: [string],&quot;dataStats&quot;: {object (DataStats)}}</code></pre></td>
</tr>
</tbody>
</table>
