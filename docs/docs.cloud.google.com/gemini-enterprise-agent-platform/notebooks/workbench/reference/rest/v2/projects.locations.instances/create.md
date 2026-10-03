---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v2/projects.locations.instances/create
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v2/projects.locations.instances/create
title: 'Method: projects.locations.instances.create'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Creates a new Instance in a given project and location.

### HTTP request

`POST https://notebooks.googleapis.com/v2/{parent}/instances`

### Path parameters

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Parameters</th>
<th></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code>parent</code></td>
<td><p><code>string</code></p>
<p>Required. Format: <code>parent=projects/{projectId}/locations/{location}</code></p>
<p>Authorization requires the following <a href="https://cloud.google.com/iam/docs/">IAM</a> permission on the specified resource <code>parent</code> :</p>
<ul>
<li><code>notebooks.instances.create</code></li>
</ul></td>
</tr>
</tbody>
</table>

### Query parameters

| Parameters   |                                                             |
|--------------|-------------------------------------------------------------|
| `instanceId` | `string` Required. User-defined unique ID of this instance. |
| `requestId`  | `string` Optional. Idempotent request UUID.                 |

### Request body

The request body contains an instance of [`Instance`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v2/projects.locations.instances#Instance) .

### Response body

If successful, the response body contains a newly created instance of [`Operation`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/Shared.Types/ListOperationsResponse#Operation) .

### Authorization scopes

Requires the following OAuth scope:

- `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .
