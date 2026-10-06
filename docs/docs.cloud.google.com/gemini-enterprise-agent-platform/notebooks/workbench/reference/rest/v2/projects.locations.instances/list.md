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
<p>Required. The parent of the instance. Formats: - <code>projects/{projectId}/locations/{location}</code> to list instances in a specific zone. - <code>projects/{projectId}/locations/-</code> to list instances in all locations.</p>
<p>Authorization requires the following <a href="https://cloud.google.com/iam/docs/">IAM</a> permission on the specified resource <code>parent</code> :</p>
<ul>
<li><code>notebooks.instances.list</code></li>
</ul></td>
</tr>
</tbody>
</table>

### Query parameters

| Parameters  |                                                                                                              |
|-------------|--------------------------------------------------------------------------------------------------------------|
| `pageSize`  | `integer` Optional. Maximum return size of the list call.                                                    |
| `pageToken` | `string` Optional. A previous returned page token that can be used to continue listing from the last result. |
| `orderBy`   | `string` Optional. Sort results. Supported values are "name", "name desc" or "" (unsorted).                  |
| `filter`    | `string` Optional. List filter.                                                                              |

### Request body

The request body must be empty.

### Response body

Response for listing notebook instances.

If successful, the response body contains data with the following structure:

**JSON representation**

```
{
  "instances": [
    {
      object (Instance)
    }
  ],
  "nextPageToken": string,
  "unreachable": [
    string
  ]
}
```

| Fields          |                                                                                                                                                                                                                                                         |
|-----------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `instances[]`   | `object ( `[`Instance`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v2/projects.locations.instances#Instance)` )` A list of returned instances.                                                   |
| `nextPageToken` | `string` Page token that can be used to continue listing from the last result in the next list call.                                                                                                                                                    |
| `unreachable[]` | `string` Unordered list. Locations that could not be reached. For example, \['projects/{projectId}/locations/us-west1-a', 'projects/{projectId}/locations/us-central1-b'\]. A ListInstancesResponse will only contain either instances or unreachables, |

### Authorization scopes

Requires one of the following OAuth scopes:

- `https://www.googleapis.com/auth/cloud-platform`
- `https://www.googleapis.com/auth/notebooks`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .
