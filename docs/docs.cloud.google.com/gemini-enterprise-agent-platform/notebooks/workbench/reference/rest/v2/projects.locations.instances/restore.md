---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v2/projects.locations.instances/restore
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v2/projects.locations.instances/restore
title: 'Method: projects.locations.instances.restore'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

instances.restore restores an Instance from a BackupSource.

### HTTP request

`POST https://notebooks.googleapis.com/v2/{name}:restore`

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
<td><code>name</code></td>
<td><p><code>string</code></p>
<p>Required. Format: <code>projects/{projectId}/locations/{location}/instances/{instanceId}</code></p>
<p>Authorization requires the following <a href="https://cloud.google.com/iam/docs/">IAM</a> permission on the specified resource <code>name</code> :</p>
<ul>
<li><code>notebooks.instances.update</code></li>
</ul></td>
</tr>
</tbody>
</table>

### Request body

The request body contains data with the following structure:

**JSON representation**

```
{

  // The following is a list of mutually exclusive fields. At most one of the
  // fields will be set in a response:
  "snapshot": {
    object (Snapshot)
  }
  // End of mutually exclusive fields.
}
```

| Fields                                                                                                                                 |                                                                                                                                                                                                                  |
|----------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Source to be restored from. The following is a list of mutually exclusive fields. At most one of the fields will be set in a response: |                                                                                                                                                                                                                  |
| `snapshot`                                                                                                                             | `object ( `[`Snapshot`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v2/projects.locations.instances/restore#Snapshot)` )` Snapshot to be used for restore. |
| End of mutually exclusive fields.                                                                                                      |                                                                                                                                                                                                                  |

### Response body

If successful, the response body contains an instance of [`Operation`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/Shared.Types/ListOperationsResponse#Operation) .

### Authorization scopes

Requires one of the following OAuth scopes:

- `https://www.googleapis.com/auth/cloud-platform`
- `https://www.googleapis.com/auth/notebooks`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .

## Snapshot

Snapshot represents the snapshot of the data disk used to restore the Workbench Instance from. Refers to: compute/v1/projects/{projectId}/global/snapshots/{snapshotId}

**JSON representation**

```
{
  "snapshotId": string,
  "projectId": string
}
```

| Fields       |                                                    |
|--------------|----------------------------------------------------|
| `snapshotId` | `string` Required. The ID of the snapshot.         |
| `projectId`  | `string` Required. The project ID of the snapshot. |
