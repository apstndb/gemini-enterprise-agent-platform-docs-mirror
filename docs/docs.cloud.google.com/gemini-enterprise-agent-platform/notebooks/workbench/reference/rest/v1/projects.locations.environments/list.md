---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v1/projects.locations.environments/list
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v1/projects.locations.environments/list
title: 'Method: projects.locations.environments.list'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Lists environments in a project.

### HTTP request

`GET https://notebooks.googleapis.com/v1/{parent}/environments`

### Path parameters

Parameters

`parent`

`string`

Required. Format: `projects/{projectId}/locations/{location}`

Authorization requires the following [IAM](https://cloud.google.com/iam/docs/) permission on the specified resource `parent` :

  - `notebooks.environments.list`

### Query parameters

Parameters

`pageSize`

`integer`

Maximum return size of the list call.

`pageToken`

`string`

A previous returned page token that can be used to continue listing from the last result.

### Request body

The request body must be empty.

### Response body

Response for listing environments.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;environments&quot;: [{object (Environment)}],&quot;nextPageToken&quot;: string,&quot;unreachable&quot;: [string]}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`environments[]`

` object ( Environment  ` )

A list of returned environments.

`nextPageToken`

`string`

A page token that can be used to continue listing from the last result in the next list call.

`unreachable[]`

`string`

Locations that could not be reached.

### Authorization scopes

Requires the following OAuth scope:

  - `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .
