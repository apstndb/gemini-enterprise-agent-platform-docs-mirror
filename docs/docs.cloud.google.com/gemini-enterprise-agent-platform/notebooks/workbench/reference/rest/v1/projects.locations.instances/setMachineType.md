---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v1/projects.locations.instances/setMachineType
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v1/projects.locations.instances/setMachineType
title: 'Method: projects.locations.instances.setMachineType'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Updates the machine type of a single Instance.

### HTTP request

`PATCH https://notebooks.googleapis.com/v1/{name}:setMachineType`

### Path parameters

Parameters

`name`

`string`

Required. Format: `projects/{projectId}/locations/{location}/instances/{instanceId}`

Authorization requires the following [IAM](https://cloud.google.com/iam/docs/) permission on the specified resource `name` :

  - `notebooks.instances.setMachineType`

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;machineType&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`machineType`

`string`

Required. The [Compute Engine machine type](https://cloud.google.com/compute/docs/machine-resource) .

### Response body

If successful, the response body contains an instance of `  Operation  ` .

### Authorization scopes

Requires the following OAuth scope:

  - `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .
