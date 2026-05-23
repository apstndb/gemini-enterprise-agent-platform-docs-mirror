---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/DeployOperationMetadata
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/DeployOperationMetadata
title: DeployOperationMetadata
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Runtime operation information for `  ModelGardenService.Deploy  ` .

Fields

`genericMetadata` ` object ( GenericOperationMetadata  ` )

The operation generic information.

`publisherModel` `string`

Output only. The name of the model resource.

`destination` `string`

Output only. The resource name of the Location to deploy the model in. Format: `projects/{project}/locations/{location}`

`projectNumber` `string ( int64 format)`

Output only. The project number where the deploy model request is sent.

`modelId` `string`

Output only. The model id to be used at query time.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;genericMetadata&quot;: {object (GenericOperationMetadata)},&quot;publisherModel&quot;: string,&quot;destination&quot;: string,&quot;projectNumber&quot;: string,&quot;modelId&quot;: string}</code></pre></td>
</tr>
</tbody>
</table>
