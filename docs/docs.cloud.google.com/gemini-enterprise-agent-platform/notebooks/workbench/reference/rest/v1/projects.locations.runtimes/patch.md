---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v1/projects.locations.runtimes/patch
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v1/projects.locations.runtimes/patch
title: 'Method: projects.locations.runtimes.patch'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Update Notebook Runtime configuration.

### HTTP request

`PATCH https://notebooks.googleapis.com/v1/{runtime.name}`

### Path parameters

| Parameters     |                                                                                                                                |
|----------------|--------------------------------------------------------------------------------------------------------------------------------|
| `runtime.name` | `string` Output only. The resource name of the runtime. Format: `projects/{project}/locations/{location}/runtimes/{runtimeId}` |

### Query parameters

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
<td><code>updateMask</code></td>
<td><p><code>string ( </code><a href="https://protobuf.dev/reference/protobuf/google.protobuf/#field-mask"><code>FieldMask</code></a><code> format)</code></p>
<p>Required. Specifies the path, relative to <code>Runtime</code> , of the field to update. For example, to change the software configuration kernels, the <code>updateMask</code> parameter would be specified as <code>softwareConfig.kernels</code> , and the <code>PATCH</code> request body would specify the new value, as follows:</p>
<pre data-fenced=""><code>{
  &quot;softwareConfig&quot;:{
    &quot;kernels&quot;: [{
       &#39;repository&#39;:
       &#39;gcr.io/deeplearning-platform-release/pytorch-gpu&#39;, &#39;tag&#39;:
       &#39;latest&#39; }],
    }
}</code></pre>
<p>Currently, only the following fields can be updated:</p>
<ul>
<li><code>softwareConfig.kernels</code></li>
<li><code>softwareConfig.post_startup_script</code></li>
<li><code>softwareConfig.custom_gpu_driver_path</code></li>
<li><code>softwareConfig.idle_shutdown</code></li>
<li><code>softwareConfig.idle_shutdown_timeout</code></li>
<li><code>softwareConfig.disable_terminal</code></li>
<li><code>labels</code></li>
</ul>
<p>This is a comma-separated list of fully qualified names of fields. Example: <code>"user.displayName,photo"</code> .</p></td>
</tr>
<tr class="even">
<td><code>requestId</code></td>
<td><p><code>string</code></p>
<p>Idempotent request UUID.</p></td>
</tr>
</tbody>
</table>

### Request body

The request body contains an instance of [`Runtime`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v1/projects.locations.runtimes#Runtime) .

### Response body

If successful, the response body contains an instance of [`Operation`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/Shared.Types/ListOperationsResponse#Operation) .

### Authorization scopes

Requires the following OAuth scope:

- `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .
