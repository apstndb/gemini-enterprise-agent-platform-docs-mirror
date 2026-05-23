---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v1/projects.locations.runtimes/list
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v1/projects.locations.runtimes/list
title: 'Method: projects.locations.runtimes.list'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Lists Runtimes in a given project and location.

### HTTP request

`GET https://notebooks.googleapis.com/v1/{parent}/runtimes`

### Path parameters

Parameters

`parent`

`string`

Required. Format: `parent=projects/{projectId}/locations/{location}`

Authorization requires the following [IAM](https://cloud.google.com/iam/docs/) permission on the specified resource `parent` :

  - `notebooks.runtimes.list`

### Query parameters

Parameters

`pageSize`

`integer`

Maximum return size of the list call.

`pageToken`

`string`

A previous returned page token that can be used to continue listing from the last result.

`orderBy`

`string`

Optional. Sort results. Supported values are "name", "name desc" or "" (unsorted).

`filter`

`string`

Optional. List filter.

### Request body

The request body must be empty.

### Response body

Response for listing Managed Notebook Runtimes.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;runtimes&quot;: [{object (Runtime)}],&quot;nextPageToken&quot;: string,&quot;unreachable&quot;: [string]}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`runtimes[]`

` object ( Runtime  ` )

A list of returned Runtimes.

`nextPageToken`

`string`

Page token that can be used to continue listing from the last result in the next list call.

`unreachable[]`

`string`

Locations that could not be reached. For example, `['us-west1', 'us-central1']` . A ListRuntimesResponse will only contain either runtimes or unreachables,

### Authorization scopes

Requires the following OAuth scope:

  - `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .
