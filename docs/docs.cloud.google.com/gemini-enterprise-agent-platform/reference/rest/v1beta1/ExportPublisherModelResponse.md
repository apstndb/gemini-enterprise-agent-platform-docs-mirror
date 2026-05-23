---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/ExportPublisherModelResponse
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/ExportPublisherModelResponse
title: ExportPublisherModelResponse
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Response message for `  ModelGardenService.ExportPublisherModel  ` .

Fields

`publisherModel` `string`

The name of the PublisherModel resource. Format: `publishers/{publisher}/models/{publisherModel}@{versionId}`

`destinationUri` `string`

The destination uri of the model weights.

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
  &quot;publisherModel&quot;: string,
  &quot;destinationUri&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>
