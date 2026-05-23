---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v1/projects.locations.instances/updateMetadataItems
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v1/projects.locations.instances/updateMetadataItems
title: 'Method: projects.locations.instances.updateMetadataItems'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Add/update metadata items for an instance.

### HTTP request

`PATCH https://notebooks.googleapis.com/v1/{name}:updateMetadataItems`

### Path parameters

Parameters

`name`

`string`

Required. Format: `projects/{projectId}/locations/{location}/instances/{instanceId}`

Authorization requires the following [IAM](https://cloud.google.com/iam/docs/) permission on the specified resource `name` :

  - `notebooks.instances.updateConfig`

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
  &quot;items&quot;: {
    string: string,
    ...
  }
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`items`

`map (key: string, value: string)`

Metadata items to add/update for the instance.

An object containing a list of `"key": value` pairs. Example: `{ "name": "wrench", "mass": "1.3kg", "count": "3" }` .

### Response body

Response for adding/changing metadata items for an instance.

If successful, the response body contains data with the following structure:

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
  &quot;items&quot;: {
    string: string,
    ...
  }
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`items`

`map (key: string, value: string)`

Map of items that were added/updated to/in the metadata.

An object containing a list of `"key": value` pairs. Example: `{ "name": "wrench", "mass": "1.3kg", "count": "3" }` .

### Authorization scopes

Requires the following OAuth scope:

  - `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .
