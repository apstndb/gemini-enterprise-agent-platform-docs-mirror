---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.tensorboards/readSize
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.tensorboards/readSize
title: 'Method: tensorboards.readSize'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.tensorboards.readSize

Returns the storage size for a given TensorBoard instance.

### Endpoint

get `https: / /{service-endpoint} /v1 /{tensorboard}:readSize`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`tensorboard` `string`

Required. The name of the Tensorboard resource. Format: `projects/{project}/locations/{location}/tensorboards/{tensorboard}`

### Request body

The request body must be empty.

### Response body

Response message for `  TensorboardService.ReadTensorboardSize  ` .

If successful, the response body contains data with the following structure:

Fields

`storageSizeByte` `string ( int64 format)`

Payload storage size for the TensorBoard

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
  &quot;storageSizeByte&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>
