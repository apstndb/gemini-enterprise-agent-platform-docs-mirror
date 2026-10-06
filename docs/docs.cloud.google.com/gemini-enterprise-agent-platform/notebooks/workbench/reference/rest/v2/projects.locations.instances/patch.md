---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v2/projects.locations.instances/patch
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v2/projects.locations.instances/patch
title: 'Method: projects.locations.instances.patch'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

instances.patch updates an Instance.

### HTTP request

`PATCH https://notebooks.googleapis.com/v2/{instance.name}`

### Path parameters

| Parameters      |                                                                                                                                                  |
|-----------------|--------------------------------------------------------------------------------------------------------------------------------------------------|
| `instance.name` | `string` Output only. Identifier. The name of this notebook instance. Format: `projects/{projectId}/locations/{location}/instances/{instanceId}` |

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
<p>Required. Mask used to update an instance. Updatable fields:</p>
<ul>
<li><code>labels</code></li>
<li><code>gceSetup.min_cpu_platform</code></li>
<li><code>gceSetup.metadata</code></li>
<li><code>gceSetup.machine_type</code></li>
<li><code>gceSetup.accelerator_configs</code></li>
<li><code>gceSetup.accelerator_configs.type</code></li>
<li><code>gceSetup.accelerator_configs.core_count</code></li>
<li><code>gceSetup.gpu_driver_config</code></li>
<li><code>gceSetup.gpu_driver_config.enable_gpu_driver</code></li>
<li><code>gceSetup.gpu_driver_config.custom_gpu_driver_path</code></li>
<li><code>gceSetup.shielded_instance_config</code></li>
<li><code>gceSetup.shielded_instance_config.enable_secure_boot</code></li>
<li><code>gceSetup.shielded_instance_config.enable_vtpm</code></li>
<li><code>gceSetup.shielded_instance_config.enable_integrity_monitoring</code></li>
<li><code>gceSetup.reservation_affinity</code></li>
<li><code>gceSetup.reservation_affinity.consume_reservation_type</code></li>
<li><code>gceSetup.reservation_affinity.key</code></li>
<li><code>gceSetup.reservation_affinity.values</code></li>
<li><code>gceSetup.tags</code></li>
<li><code>gceSetup.container_image</code></li>
<li><code>gceSetup.container_image.repository</code></li>
<li><code>gceSetup.container_image.tag</code></li>
<li><code>gceSetup.disable_public_ip</code></li>
<li><code>disableProxyAccess</code></li>
</ul>
<p>Note: <code>gceSetup.disable_public_ip</code> and <code>disableProxyAccess</code> are one-way on update -- they can only be used to <em>disable</em> the feature (set the field to <code>true</code> ). Requests that set either field back to <code>false</code> (re-enabling the external IP or proxy access) are rejected with <code>INVALID_ARGUMENT</code> .</p>
<p>This is a comma-separated list of fully qualified names of fields. Example: <code>"user.displayName,photo"</code> .</p></td>
</tr>
<tr class="even">
<td><code>requestId</code></td>
<td><p><code>string</code></p>
<p>Optional. Idempotent request UUID.</p></td>
</tr>
</tbody>
</table>

### Request body

The request body contains an instance of [`Instance`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v2/projects.locations.instances#Instance) .

### Response body

If successful, the response body contains an instance of [`Operation`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/Shared.Types/ListOperationsResponse#Operation) .

### Authorization scopes

Requires one of the following OAuth scopes:

- `https://www.googleapis.com/auth/cloud-platform`
- `https://www.googleapis.com/auth/notebooks`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .
