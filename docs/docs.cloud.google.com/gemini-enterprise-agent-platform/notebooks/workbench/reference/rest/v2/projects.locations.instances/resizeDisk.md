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
<td><code>notebookInstance</code></td>
<td><p><code>string</code></p>
<p>Required. Format: <code>projects/{projectId}/locations/{location}/instances/{instanceId}</code></p>
<p>Authorization requires the following <a href="https://cloud.google.com/iam/docs/">IAM</a> permission on the specified resource <code>notebookInstance</code> :</p>
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

  // Union field Disk can be only one of the following:
  "bootDisk": {
    object (BootDisk)
  },
  "dataDisk": {
    object (DataDisk)
  }
  // End of list of possible types for union field Disk.
}
```

| Fields                                                                                                                |                                                                                                                                                                                                                                              |
|-----------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Union field `Disk` . Type of the disk that can be resized: boot or data disk `Disk` can be only one of the following: |                                                                                                                                                                                                                                              |
| `bootDisk`                                                                                                            | `object ( `[`BootDisk`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v2/projects.locations.instances#BootDisk)` )` Required. The boot disk to be resized. Only diskSizeGb will be used. |
| `dataDisk`                                                                                                            | `object ( `[`DataDisk`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v2/projects.locations.instances#DataDisk)` )` Required. The data disk to be resized. Only diskSizeGb will be used. |

### Response body

If successful, the response body contains an instance of [`Operation`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/Shared.Types/ListOperationsResponse#Operation) .

### Authorization scopes

Requires the following OAuth scope:

- `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .
