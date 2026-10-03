---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v1/projects.locations.schedules/list
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v1/projects.locations.schedules/list
title: 'Method: projects.locations.schedules.list'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Lists schedules in a given project and location.

### HTTP request

`GET https://notebooks.googleapis.com/v1/{parent}/schedules`

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
<li><code>notebooks.schedules.list</code></li>
</ul></td>
</tr>
</tbody>
</table>

### Query parameters

| Parameters  |                                                                                                    |
|-------------|----------------------------------------------------------------------------------------------------|
| `pageSize`  | `integer` Maximum return size of the list call.                                                    |
| `pageToken` | `string` A previous returned page token that can be used to continue listing from the last result. |
| `filter`    | `string` Filter applied to resulting schedules.                                                    |
| `orderBy`   | `string` Field to order results by.                                                                |

### Request body

The request body must be empty.

### Response body

Response for listing scheduled notebook job.

If successful, the response body contains data with the following structure:

**JSON representation**

```
{
  "schedules": [
    {
      object (Schedule)
    }
  ],
  "nextPageToken": string,
  "unreachable": [
    string
  ]
}
```

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Fields</th>
<th></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code>schedules[]</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v1/projects.locations.schedules#Schedule"><code>Schedule</code></a><code> )</code></p>
<p>A list of returned instances.</p></td>
</tr>
<tr class="even">
<td><code>nextPageToken</code></td>
<td><p><code>string</code></p>
<p>Page token that can be used to continue listing from the last result in the next list call.</p></td>
</tr>
<tr class="odd">
<td><code>unreachable[]</code></td>
<td><p><code>string</code></p>
<p>Schedules that could not be reached. For example:</p>
<pre data-fenced=""><code>[&#39;projects/{projectId}/location/{location}/schedules/monthly_digest&#39;,
 &#39;projects/{projectId}/location/{location}/schedules/weekly_sentiment&#39;]</code></pre></td>
</tr>
</tbody>
</table>

### Authorization scopes

Requires the following OAuth scope:

- `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .
