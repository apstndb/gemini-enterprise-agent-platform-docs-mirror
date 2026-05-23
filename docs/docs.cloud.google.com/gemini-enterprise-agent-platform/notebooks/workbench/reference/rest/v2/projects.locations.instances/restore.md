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

Parameters

`name`

`string`

Required. Format: `projects/{projectId}/locations/{location}/instances/{instanceId}`

Authorization requires the following [IAM](https://cloud.google.com/iam/docs/) permission on the specified resource `name` :

  - `notebooks.instances.update`

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{// Union field Source can be only one of the following:&quot;snapshot&quot;: {object (Snapshot)}// End of list of possible types for union field Source.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

Union field `Source` . Source to be restored from. `Source` can be only one of the following:

`snapshot`

` object ( Snapshot  ` )

Snapshot to be used for restore.

### Response body

If successful, the response body contains an instance of `  Operation  ` .

### Authorization scopes

Requires the following OAuth scope:

  - `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .

## Snapshot

Snapshot represents the snapshot of the data disk used to restore the Workbench Instance from. Refers to: compute/v1/projects/{projectId}/global/snapshots/{snapshotId}

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
  &quot;snapshotId&quot;: string,
  &quot;projectId&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`snapshotId`

`string`

Required. The ID of the snapshot.

`projectId`

`string`

Required. The project ID of the snapshot.
