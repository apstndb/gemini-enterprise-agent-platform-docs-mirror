---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/TensorboardBlob
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/TensorboardBlob
title: TensorboardBlob
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

One blob (e.g, image, graph) viewable on a blob metric plot.

Fields

`id` `string`

Output only. A URI safe key uniquely identifying a blob. Can be used to locate the blob stored in the Cloud Storage bucket of the consumer project.

`data` `string ( bytes format)`

Optional. The bytes of the blob is not present unless it's returned by the ReadTensorboardBlobData endpoint.

A base64-encoded string.

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
  &quot;id&quot;: string,
  &quot;data&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>
