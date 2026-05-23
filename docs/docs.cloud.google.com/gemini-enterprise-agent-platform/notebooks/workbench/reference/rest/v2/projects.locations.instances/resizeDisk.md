---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v2/projects.locations.instances/resizeDisk
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v2/projects.locations.instances/resizeDisk
title: 'Method: projects.locations.instances.resizeDisk'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Resize a notebook instance disk to a higher capacity.

### HTTP request

`POST https://notebooks.googleapis.com/v2/{notebookInstance}:resizeDisk`

### Path parameters

Parameters

`notebookInstance`

`string`

Required. Format: `projects/{projectId}/locations/{location}/instances/{instanceId}`

Authorization requires the following [IAM](https://cloud.google.com/iam/docs/) permission on the specified resource `notebookInstance` :

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{// Union field Disk can be only one of the following:&quot;bootDisk&quot;: {object (BootDisk)},&quot;dataDisk&quot;: {object (DataDisk)}// End of list of possible types for union field Disk.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

Union field `Disk` . Type of the disk that can be resized: boot or data disk `Disk` can be only one of the following:

`bootDisk`

` object ( BootDisk  ` )

Required. The boot disk to be resized. Only diskSizeGb will be used.

`dataDisk`

` object ( DataDisk  ` )

Required. The data disk to be resized. Only diskSizeGb will be used.

### Response body

If successful, the response body contains an instance of `  Operation  ` .

### Authorization scopes

Requires the following OAuth scope:

  - `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .
