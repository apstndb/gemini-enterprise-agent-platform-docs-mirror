---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v1/projects.locations.runtimes/switch
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v1/projects.locations.runtimes/switch
title: 'Method: projects.locations.runtimes.switch'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Switch a Managed Notebook Runtime.

### HTTP request

`POST https://notebooks.googleapis.com/v1/{name}:switch`

### Path parameters

Parameters

`name`

`string`

Required. Format: `projects/{projectId}/locations/{location}/runtimes/{runtimeId}`

Authorization requires the following [IAM](https://cloud.google.com/iam/docs/) permission on the specified resource `name` :

  - `notebooks.runtimes.switch`

### Request body

The request body contains data with the following structure:

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;machineType&quot;: string,&quot;acceleratorConfig&quot;: {object (RuntimeAcceleratorConfig)},&quot;requestId&quot;: string}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`machineType`

`string`

machine type.

`acceleratorConfig`

` object ( RuntimeAcceleratorConfig  ` )

accelerator config.

`requestId`

`string`

Idempotent request UUID.

### Response body

If successful, the response body contains an instance of `  Operation  ` .

### Authorization scopes

Requires the following OAuth scope:

  - `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .
