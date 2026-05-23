---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/DeployResponse
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/DeployResponse
title: DeployResponse
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Response message for `  ModelGardenService.Deploy  ` .

Fields

`publisherModel` `string`

Output only. The name of the PublisherModel resource. Format: `publishers/{publisher}/models/{publisherModel}@{versionId}` , or `publishers/hf-{hugging-face-author}/models/{hugging-face-model-name}@001`

`endpoint` `string`

Output only. The name of the Endpoint created. Format: `projects/{project}/locations/{location}/endpoints/{endpoint}`

`model` `string`

Output only. The name of the Model created. Format: `projects/{project}/locations/{location}/models/{model}`

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
  &quot;endpoint&quot;: string,
  &quot;model&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>
