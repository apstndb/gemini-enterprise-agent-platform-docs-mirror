---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v2/projects.locations.instances/list
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v2/projects.locations.instances/list
title: 'Method: projects.locations.instances.list'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Lists instances in a given project and location.

### HTTP request

`GET https://notebooks.googleapis.com/v2/{parent}/instances`

### Path parameters

Parameters

`parent`

`string`

Required. The parent of the instance. Formats: - `projects/{projectId}/locations/{location}` to list instances in a specific zone. - `projects/{projectId}/locations/-` to list instances in all locations.

Authorization requires the following [IAM](https://cloud.google.com/iam/docs/) permission on the specified resource `parent` :

  - `notebooks.instances.list`

### Query parameters

Parameters

`pageSize`

`integer`

Optional. Maximum return size of the list call.

`pageToken`

`string`

Optional. A previous returned page token that can be used to continue listing from the last result.

`orderBy`

`string`

Optional. Sort results. Supported values are "name", "name desc" or "" (unsorted).

`filter`

`string`

Optional. List filter.

### Request body

The request body must be empty.

### Response body

Response for listing notebook instances.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;instances&quot;: [{object (Instance)}],&quot;nextPageToken&quot;: string,&quot;unreachable&quot;: [string]}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`instances[]`

` object ( Instance  ` )

A list of returned instances.

`nextPageToken`

`string`

Page token that can be used to continue listing from the last result in the next list call.

`unreachable[]`

`string`

Unordered list. Locations that could not be reached. For example, \['projects/{projectId}/locations/us-west1-a', 'projects/{projectId}/locations/us-central1-b'\]. A ListInstancesResponse will only contain either instances or unreachables,

### Authorization scopes

Requires the following OAuth scope:

  - `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .
