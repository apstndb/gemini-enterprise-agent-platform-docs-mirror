---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/colab_enterprise_update_notebook_runtime_template
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/colab_enterprise_update_notebook_runtime_template
title: 'MCP Tools Reference: aiplatform.googleapis.com'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

## Tool: `colab_enterprise_update_notebook_runtime_template`

Updates a Colab Enterprise runtime template. Use this tool to modify an existing runtime template's configuration. Format: 'projects/{project_id}/locations/{region}/notebookRuntimeTemplates/{notebook_runtime_template_id}'. CRITICAL: For {region}, use the region specified in the current context. If no region is specified, prompt the user for one. Do not use 'global'.

The following sample demonstrate how to use `curl` to invoke the `colab_enterprise_update_notebook_runtime_template` MCP tool.

**Curl Request**

```
curl --location 'https://aiplatform.googleapis.com/mcp/generate' \
--header 'content-type: application/json' \
--header 'accept: application/json, text/event-stream' \
--data '{
  "method": "tools/call",
  "params": {
    "name": "colab_enterprise_update_notebook_runtime_template",
    "arguments": {
      // provide these details according to the tool's MCP specification
    }
  },
  "jsonrpc": "2.0",
  "id": 1
}'
```

## Input Schema

Request message for `NotebookService.UpdateNotebookRuntimeTemplate` .

### UpdateNotebookRuntimeTemplateRequest

**JSON representation**

```
{
  "notebookRuntimeTemplate": {
    object (NotebookRuntimeTemplate)
  },
  "updateMask": string
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
<td><code>notebookRuntimeTemplate</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/colab_enterprise_create_notebook_runtime_template#Input.Schema.NotebookRuntimeTemplate"><code>NotebookRuntimeTemplate</code></a><code> )</code></p>
<p>Required. The NotebookRuntimeTemplate to update.</p></td>
</tr>
<tr class="even">
<td><code>updateMask</code></td>
<td><p><code>string ( </code><a href="https://protobuf.dev/reference/protobuf/google.protobuf/#field-mask"><code>FieldMask</code></a><code> format)</code></p>
<p>Required. The update mask applies to the resource. For the <code>FieldMask</code> definition, see <a href="https://protobuf.dev/reference/protobuf/google.protobuf/#field-mask"><code>google.protobuf.FieldMask</code></a> . Input format: <code>{paths: "${updated_field}"}</code> Updatable fields:</p>
<ul>
<li><code>encryption_spec.kms_key_name</code></li>
<li><code>display_name</code></li>
<li><code>software_config.post_startup_script_config.post_startup_script</code></li>
<li><code>software_config.post_startup_script_config.post_startup_script_url</code></li>
<li><code>software_config.post_startup_script_config.post_startup_script_behavior</code></li>
<li><code>software_config.env</code></li>
<li><code>software_config.colab_image.release_name</code></li>
<li><code>software_config.custom_container_config.image_uri</code></li>
</ul>
<p>This is a comma-separated list of fully qualified names of fields. Example: <code>"user.displayName,photo"</code> .</p></td>
</tr>
</tbody>
</table>

### NotebookRuntimeTemplate

**JSON representation**

```
{
  "name": string,
  "displayName": string,
  "description": string,
  "isDefault": boolean,
  "machineSpec": {
    object (MachineSpec)
  },
  "dataPersistentDiskSpec": {
    object (PersistentDiskSpec)
  },
  "networkSpec": {
    object (NetworkSpec)
  },
  "serviceAccount": string,
  "etag": string,
  "labels": {
    string: string,
    ...
  },
  "idleShutdownConfig": {
    object (NotebookIdleShutdownConfig)
  },
  "eucConfig": {
    object (NotebookEucConfig)
  },
  "createTime": string,
  "updateTime": string,
  "notebookRuntimeType": enum (NotebookRuntimeType),
  "shieldedVmConfig": {
    object (ShieldedVmConfig)
  },
  "networkTags": [
    string
  ],
  "encryptionSpec": {
    object (EncryptionSpec)
  },
  "softwareConfig": {
    object (NotebookSoftwareConfig)
  }
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
<td><code>name</code></td>
<td><p><code>string</code></p>
<p>The resource name of the NotebookRuntimeTemplate.</p></td>
</tr>
<tr class="even">
<td><code>displayName</code></td>
<td><p><code>string</code></p>
<p>Required. The display name of the NotebookRuntimeTemplate. The name can be up to 128 characters long and can consist of any UTF-8 characters.</p></td>
</tr>
<tr class="odd">
<td><code>description</code></td>
<td><p><code>string</code></p>
<p>The description of the NotebookRuntimeTemplate.</p></td>
</tr>
<tr class="even">
<td><code>isDefault </code><strong><code>(deprecated)</code></strong></td>
<td><p><code>boolean</code></p>
<blockquote>
<p>This item is deprecated!</p>
</blockquote>
<p>Output only. Deprecated: This field has no behavior. Use notebook_runtime_type = 'ONE_CLICK' instead.</p>
<p>The default template to use if not specified.</p></td>
</tr>
<tr class="odd">
<td><code>machineSpec</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/colab_enterprise_create_notebook_runtime_template#Input.Schema.MachineSpec"><code>MachineSpec</code></a><code> )</code></p>
<p>Optional. Immutable. The specification of a single machine for the template.</p></td>
</tr>
<tr class="even">
<td><code>dataPersistentDiskSpec</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/colab_enterprise_create_notebook_runtime_template#Input.Schema.PersistentDiskSpec"><code>PersistentDiskSpec</code></a><code> )</code></p>
<p>Optional. The specification of [persistent disk][https://cloud.google.com/compute/docs/disks/persistent-disks] attached to the runtime as data disk storage.</p></td>
</tr>
<tr class="odd">
<td><code>networkSpec</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/colab_enterprise_create_notebook_runtime_template#Input.Schema.NetworkSpec"><code>NetworkSpec</code></a><code> )</code></p>
<p>Optional. Network spec.</p></td>
</tr>
<tr class="even">
<td><code>serviceAccount </code><strong><code>(deprecated)</code></strong></td>
<td><p><code>string</code></p>
<blockquote>
<p>This item is deprecated!</p>
</blockquote>
<p>Deprecated: This field is ignored and the "Agent Platform Notebook Service Account" ( <a href="mailto:service-PROJECT_NUMBER@gcp-sa-aiplatform-vm.iam.gserviceaccount.com">service-PROJECT_NUMBER@gcp-sa-aiplatform-vm.iam.gserviceaccount.com</a> ) is used for the runtime workload identity. See <a href="https://cloud.google.com/iam/docs/service-agents#vertex-ai-notebook-service-account">https://cloud.google.com/iam/docs/service-agents#vertex-ai-notebook-service-account</a> for more details. For NotebookExecutionJob, use NotebookExecutionJob.service_account instead.</p>
<p>The service account that the runtime workload runs as. You can use any service account within the same project, but you must have the service account user permission to use the instance.</p>
<p>If not specified, the <a href="https://cloud.google.com/compute/docs/access/service-accounts#default_service_account">Compute Engine default service account</a> is used.</p></td>
</tr>
<tr class="odd">
<td><code>etag</code></td>
<td><p><code>string</code></p>
<p>Used to perform consistent read-modify-write updates. If not set, a blind "overwrite" update happens.</p></td>
</tr>
<tr class="even">
<td><code>labels</code></td>
<td><p><code>map (key: string, value: string)</code></p>
<p>The labels with user-defined metadata to organize the NotebookRuntimeTemplates.</p>
<p>Label keys and values can be no longer than 64 characters (Unicode codepoints), can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed.</p>
<p>See <a href="https://goo.gl/xmQnxf">https://goo.gl/xmQnxf</a> for more information and examples of labels.</p>
<p>An object containing a list of <code>"key": value</code> pairs. Example: <code>{ "name": "wrench", "mass": "1.3kg", "count": "3" }</code> .</p></td>
</tr>
<tr class="odd">
<td><code>idleShutdownConfig</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/colab_enterprise_create_notebook_runtime_template#Input.Schema.NotebookIdleShutdownConfig"><code>NotebookIdleShutdownConfig</code></a><code> )</code></p>
<p>The idle shutdown configuration of NotebookRuntimeTemplate. This config will only be set when idle shutdown is enabled.</p></td>
</tr>
<tr class="even">
<td><code>eucConfig</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/colab_enterprise_create_notebook_runtime_template#Input.Schema.NotebookEucConfig"><code>NotebookEucConfig</code></a><code> )</code></p>
<p>EUC configuration of the NotebookRuntimeTemplate.</p></td>
</tr>
<tr class="odd">
<td><code>createTime</code></td>
<td><p><code>string ( </code><a href="https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp"><code>Timestamp</code></a><code> format)</code></p>
<p>Output only. Timestamp when this NotebookRuntimeTemplate was created.</p>
<p>Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: <code>"2014-10-02T15:01:23Z"</code> , <code>"2014-10-02T15:01:23.045123456Z"</code> or <code>"2014-10-02T15:01:23+05:30"</code> .</p></td>
</tr>
<tr class="even">
<td><code>updateTime</code></td>
<td><p><code>string ( </code><a href="https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp"><code>Timestamp</code></a><code> format)</code></p>
<p>Output only. Timestamp when this NotebookRuntimeTemplate was most recently updated.</p>
<p>Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: <code>"2014-10-02T15:01:23Z"</code> , <code>"2014-10-02T15:01:23.045123456Z"</code> or <code>"2014-10-02T15:01:23+05:30"</code> .</p></td>
</tr>
<tr class="odd">
<td><code>notebookRuntimeType</code></td>
<td><p><code>enum ( </code><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/colab_enterprise_create_notebook_runtime_template#Input.Schema.NotebookRuntimeType"><code>NotebookRuntimeType</code></a><code> )</code></p>
<p>Optional. Immutable. The type of the notebook runtime template.</p></td>
</tr>
<tr class="even">
<td><code>shieldedVmConfig</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/colab_enterprise_create_notebook_runtime_template#Input.Schema.ShieldedVmConfig"><code>ShieldedVmConfig</code></a><code> )</code></p>
<p>Optional. Immutable. Runtime Shielded VM spec.</p></td>
</tr>
<tr class="odd">
<td><code>networkTags[]</code></td>
<td><p><code>string</code></p>
<p>Optional. The Compute Engine tags to add to runtime (see <a href="https://cloud.google.com/vpc/docs/add-remove-network-tags">Tagging instances</a> ).</p></td>
</tr>
<tr class="even">
<td><code>encryptionSpec</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/upload_model#Input.Schema.EncryptionSpec"><code>EncryptionSpec</code></a><code> )</code></p>
<p>Customer-managed encryption key spec for the notebook runtime.</p></td>
</tr>
<tr class="odd">
<td><code>softwareConfig</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/colab_enterprise_create_notebook_runtime_template#Input.Schema.NotebookSoftwareConfig"><code>NotebookSoftwareConfig</code></a><code> )</code></p>
<p>Optional. The notebook software configuration of the notebook runtime.</p></td>
</tr>
</tbody>
</table>

### MachineSpec

**JSON representation**

```
{
  "machineType": string,
  "acceleratorType": enum (AcceleratorType),
  "acceleratorCount": integer,
  "gpuPartitionSize": string,
  "tpuTopology": string,
  "reservationAffinity": {
    object (ReservationAffinity)
  }
}
```

| Fields                |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
|-----------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `machineType`         | `string` Immutable. The type of the machine. See the [list of machine types supported for prediction](https://cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/configure-compute#machine-types) See the [list of machine types supported for custom training](https://cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/configure-compute#machine-types) . For `DeployedModel` this field is optional, and the default value is `n1-standard-2` . For `BatchPredictionJob` or as part of `WorkerPoolSpec` this field is required.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| `acceleratorType`     | `enum ( `[`AcceleratorType`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/colab_enterprise_create_notebook_runtime_template#Input.Schema.AcceleratorType)` )` Immutable. The type of accelerator(s) that may be attached to the machine as per `accelerator_count` .                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| `acceleratorCount`    | `integer` The number of accelerators to attach to the machine. For [accelerator optimized machine types](https://cloud.google.com/compute/docs/accelerator-optimized-machines) , One may set the accelerator_count from 1 to N for machine with N GPUs. If accelerator_count is less than or equal to N / 2, Agent Platform co-schedules the replicas of the model into the same VM to save cost. For example, if the machine type is a3-highgpu-8g, which has 8 H100 GPUs, one can set accelerator_count to 1 to 8. If accelerator_count is 1, 2, 3, or 4, Agent Platform co-schedules 8, 4, 2, or 2 replicas of the model into the same VM to save cost. When co-scheduling, CPU, memory and storage on the VM will be distributed to replicas on the VM. For example, one can expect a co-scheduled replica requesting 2 GPUs out of a 8-GPU VM will receive 25% of the CPU, memory and storage of the VM. Note that the feature is not compatible with \[multihost_gpu_node_count\]\[\]. When multihost_gpu_node_count is set, the co-scheduling will not be enabled. |
| `gpuPartitionSize`    | `string` Optional. Immutable. The Nvidia GPU partition size. When specified, the requested accelerators will be partitioned into smaller GPU partitions. For example, if the request is for 8 units of NVIDIA A100 GPUs, and gpu_partition_size="1g.10gb", the service will create 8 \* 7 = 56 partitioned MIG instances. The partition size must be a value supported by the requested accelerator. Refer to [Nvidia GPU Partitioning](https://cloud.google.com/kubernetes-engine/docs/how-to/gpus-multi#multi-instance_gpu_partitions) for the available partition sizes. If set, the accelerator_count should be set to 1.                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| `tpuTopology`         | `string` Immutable. The topology of the TPUs. Corresponds to the TPU topologies available from GKE. (Example: tpu_topology: "2x2x1").                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| `reservationAffinity` | `object ( `[`ReservationAffinity`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/colab_enterprise_create_notebook_runtime_template#Input.Schema.ReservationAffinity)` )` Optional. Immutable. Configuration controlling how this resource pool consumes reservation.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |

### ReservationAffinity

**JSON representation**

```
{
  "reservationAffinityType": enum (Type),
  "key": string,
  "values": [
    string
  ]
}
```

| Fields                    |                                                                                                                                                                                                                                       |
|---------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `reservationAffinityType` | `enum ( `[`Type`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/colab_enterprise_create_notebook_runtime_template#Input.Schema.Type)` )` Required. Specifies the reservation affinity type. |
| `key`                     | `string` Optional. Corresponds to the label key of a reservation resource. To target a SPECIFIC_RESERVATION by name, use `compute.googleapis.com/reservation-name` as the key and specify the name of your reservation as its value.  |
| `values[]`                | `string` Optional. Corresponds to the label values of a reservation resource. This must be the full resource name of the reservation or reservation block.                                                                            |

### PersistentDiskSpec

**JSON representation**

```
{
  "diskType": string,
  "diskSizeGb": string
}
```

| Fields       |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
|--------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `diskType`   | `string` Type of the disk (default is "pd-standard"). Valid values: "pd-ssd" (Persistent Disk Solid State Drive) "pd-standard" (Persistent Disk Hard Disk Drive) "pd-balanced" (Balanced Persistent Disk) "pd-extreme" (Extreme Persistent Disk) "hyperdisk-balanced" (Hyperdisk Balanced) "hyperdisk-extreme" (Hyperdisk Extreme) "hyperdisk-balanced-high-availability" (Hyperdisk Balanced High Availability) "hyperdisk-ml" (Hyperdisk ML) "hyperdisk-throughput" (Hyperdisk Throughput) |
| `diskSizeGb` | `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)` Size in GB of the disk (default is 100GB).                                                                                                                                                                                                                                                                                                                                                            |

### NetworkSpec

**JSON representation**

```
{
  "enableInternetAccess": boolean,
  "network": string,
  "subnetwork": string
}
```

| Fields                 |                                                                                                                                                  |
|------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------|
| `enableInternetAccess` | `boolean` Whether to enable public internet access. Default false.                                                                               |
| `network`              | `string` The full name of the Google Compute Engine [network](https://cloud.google.com//compute/docs/networks-and-firewalls#networks)            |
| `subnetwork`           | `string` The name of the subnet that this instance is in. Format: `projects/{project_id_or_number}/regions/{region}/subnetworks/{subnetwork_id}` |

### LabelsEntry

**JSON representation**

```
{
  "key": string,
  "value": string
}
```

| Fields  |          |
|---------|----------|
| `key`   | `string` |
| `value` | `string` |

### NotebookIdleShutdownConfig

**JSON representation**

```
{
  "idleTimeout": string,
  "idleShutdownDisabled": boolean
}
```

| Fields                 |                                                                                                                                                                                                                                                                                                                                                                        |
|------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `idleTimeout`          | `string ( `[`Duration`](https://protobuf.dev/reference/protobuf/google.protobuf/#duration)` format)` Required. Duration is accurate to the second. In Notebook, Idle Timeout is accurate to minute so the range of idle_timeout (second) is: 10 \* 60 \~ 1440 \* 60. A duration in seconds with up to nine fractional digits, ending with ' `s` '. Example: `"3.5s"` . |
| `idleShutdownDisabled` | `boolean` Whether Idle Shutdown is disabled in this NotebookRuntimeTemplate.                                                                                                                                                                                                                                                                                           |

### Duration

**JSON representation**

```
{
  "seconds": string,
  "nanos": integer
}
```

| Fields    |                                                                                                                                                                                                                                                                                                                                                                                          |
|-----------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `seconds` | `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)` Signed seconds of the span of time. Must be from -315,576,000,000 to +315,576,000,000 inclusive. Note: these bounds are computed from: 60 sec/min \* 60 min/hr \* 24 hr/day \* 365.25 days/year \* 10000 years                                                                                    |
| `nanos`   | `integer` Signed fractions of a second at nanosecond resolution of the span of time. Durations less than one second are represented with a 0 `seconds` field and a positive or negative `nanos` field. For durations of one second or more, a non-zero value for the `nanos` field must be of the same sign as the `seconds` field. Must be from -999,999,999 to +999,999,999 inclusive. |

### NotebookEucConfig

**JSON representation**

```
{
  "eucDisabled": boolean,
  "bypassActasCheck": boolean
}
```

| Fields             |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
|--------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `eucDisabled`      | `boolean` Input only. Whether EUC is disabled in this NotebookRuntimeTemplate. In proto3, the default value of a boolean is false. In this way, by default EUC will be enabled for NotebookRuntimeTemplate.                                                                                                                                                                                                                                                                                                             |
| `bypassActasCheck` | `boolean` Output only. Whether ActAs check is bypassed for service account attached to the VM. If false, we need ActAs check for the default Compute Engine Service account. When a Runtime is created, a VM is allocated using Default Compute Engine Service Account. Any user requesting to use this Runtime requires Service Account User (ActAs) permission over this SA. If true, Runtime owner is using EUC and does not require the above permission as VM no longer use default Compute Engine SA, but a P4SA. |

### Timestamp

**JSON representation**

```
{
  "seconds": string,
  "nanos": integer
}
```

| Fields    |                                                                                                                                                                                                                                                                                                                      |
|-----------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `seconds` | `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)` Represents seconds of UTC time since Unix epoch 1970-01-01T00:00:00Z. Must be between -62135596800 and 253402300799 inclusive (which corresponds to 0001-01-01T00:00:00Z to 9999-12-31T23:59:59Z).                            |
| `nanos`   | `integer` Non-negative fractions of a second at nanosecond resolution. This field is the nanosecond portion of the duration, not an alternative to seconds. Negative second values with fractions must still have non-negative nanos values that count forward in time. Must be between 0 and 999,999,999 inclusive. |

### ShieldedVmConfig

**JSON representation**

```
{
  "enableSecureBoot": boolean
}
```

| Fields             |                                                                                                                                                                                                                                                                                                                                             |
|--------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `enableSecureBoot` | `boolean` Defines whether the instance has [Secure Boot](https://cloud.google.com/compute/shielded-vm/docs/shielded-vm#secure-boot) enabled. Secure Boot helps ensure that the system only runs authentic software by verifying the digital signature of all boot components, and halting the boot process if signature verification fails. |

### EncryptionSpec

**JSON representation**

```
{
  "kmsKeyName": string
}
```

| Fields       |                                                                                                                                                                                                                                                                   |
|--------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `kmsKeyName` | `string` Required. Resource name of the Cloud KMS key used to protect the resource. The Cloud KMS key must be in the same region as the resource. It must have the format `projects/{project}/locations/{location}/keyRings/{key_ring}/cryptoKeys/{crypto_key}` . |

### NotebookSoftwareConfig

**JSON representation**

```
{
  "env": [
    {
      object (EnvVar)
    }
  ],
  "postStartupScriptConfig": {
    object (PostStartupScriptConfig)
  },

  // Union field runtime_image can be only one of the following:
  "colabImage": {
    object (ColabImage)
  }
  // End of list of possible types for union field runtime_image.
}
```

| Fields                                                                          |                                                                                                                                                                                                                                                                  |
|---------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `env[]`                                                                         | `object ( `[`EnvVar`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/upload_model#Input.Schema.EnvVar)` )` Optional. Environment variables to be passed to the container. Maximum limit is 100.                         |
| `postStartupScriptConfig`                                                       | `object ( `[`PostStartupScriptConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/colab_enterprise_create_notebook_runtime_template#Input.Schema.PostStartupScriptConfig)` )` Optional. Post startup script config. |
| Union field `runtime_image` . `runtime_image` can be only one of the following: |                                                                                                                                                                                                                                                                  |
| `colabImage`                                                                    | `object ( `[`ColabImage`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/colab_enterprise_create_notebook_runtime_template#Input.Schema.ColabImage)` )` Optional. Google-managed NotebookRuntime colab image.           |

### ColabImage

**JSON representation**

```
{
  "releaseName": string,
  "description": string
}
```

| Fields        |                                                                                                                                                                          |
|---------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `releaseName` | `string` Optional. The release name of the NotebookRuntime Colab image, e.g. "py310". If not specified, detault to the latest release.                                   |
| `description` | `string` Output only. A human-readable description of the specified colab image release, populated by the system. Example: "Python 3.10", "Latest - current Python 3.11" |

### EnvVar

**JSON representation**

```
{
  "name": string,
  "value": string
}
```

| Fields  |                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
|---------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `name`  | `string` Required. Name of the environment variable. Must be a valid C identifier.                                                                                                                                                                                                                                                                                                                                                                  |
| `value` | `string` Required. Variables that reference a \$(VAR_NAME) are expanded using the previous defined environment variables in the container and any service environment variables. If a variable cannot be resolved, the reference in the input string will be unchanged. The \$(VAR_NAME) syntax can be escaped with a double \$\$, ie: \$\$(VAR_NAME). Escaped references will never be expanded, regardless of whether the variable exists or not. |

### PostStartupScriptConfig

**JSON representation**

```
{
  "postStartupScript": string,
  "postStartupScriptUrl": string,
  "postStartupScriptBehavior": enum (PostStartupScriptBehavior)
}
```

| Fields                      |                                                                                                                                                                                                                                                                                                                   |
|-----------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `postStartupScript`         | `string` Optional. Post startup script to run after runtime is started.                                                                                                                                                                                                                                           |
| `postStartupScriptUrl`      | `string` Optional. Post startup script url to download. Example: `gs://bucket/script.sh`                                                                                                                                                                                                                          |
| `postStartupScriptBehavior` | `enum ( `[`PostStartupScriptBehavior`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/colab_enterprise_create_notebook_runtime_template#Input.Schema.PostStartupScriptBehavior)` )` Optional. Post startup script behavior that defines download and execution behavior. |

### FieldMask

**JSON representation**

```
{
  "paths": [
    string
  ]
}
```

| Fields    |                                       |
|-----------|---------------------------------------|
| `paths[]` | `string` The set of field mask paths. |

### AcceleratorType

Represents a hardware accelerator type.

| Enums                          |                                                                                                                        |
|--------------------------------|------------------------------------------------------------------------------------------------------------------------|
| `ACCELERATOR_TYPE_UNSPECIFIED` | Unspecified accelerator type, which means no accelerator.                                                              |
| `NVIDIA_TESLA_K80`             | Deprecated: Nvidia Tesla K80 GPU has reached end of support, see <https://cloud.google.com/compute/docs/eol/k80-eol> . |
| `NVIDIA_TESLA_P100`            | Nvidia Tesla P100 GPU.                                                                                                 |
| `NVIDIA_TESLA_V100`            | Nvidia Tesla V100 GPU.                                                                                                 |
| `NVIDIA_TESLA_P4`              | Nvidia Tesla P4 GPU.                                                                                                   |
| `NVIDIA_TESLA_T4`              | Nvidia Tesla T4 GPU.                                                                                                   |
| `NVIDIA_TESLA_A100`            | Nvidia Tesla A100 GPU.                                                                                                 |
| `NVIDIA_A100_80GB`             | Nvidia A100 80GB GPU.                                                                                                  |
| `NVIDIA_L4`                    | Nvidia L4 GPU.                                                                                                         |
| `NVIDIA_H100_80GB`             | Nvidia H100 80Gb GPU.                                                                                                  |
| `NVIDIA_H100_MEGA_80GB`        | Nvidia H100 Mega 80Gb GPU.                                                                                             |
| `NVIDIA_H200_141GB`            | Nvidia H200 141Gb GPU.                                                                                                 |
| `NVIDIA_B200`                  | Nvidia B200 GPU.                                                                                                       |
| `NVIDIA_GB200`                 | Nvidia GB200 GPU.                                                                                                      |
| `NVIDIA_RTX_PRO_6000`          | Nvidia RTX Pro 6000 GPU.                                                                                               |
| `TPU_V2`                       | TPU v2.                                                                                                                |
| `TPU_V3`                       | TPU v3.                                                                                                                |
| `TPU_V4_POD`                   | TPU v4.                                                                                                                |
| `TPU_V5_LITEPOD`               | TPU v5.                                                                                                                |

### Type

Identifies a type of reservation affinity.

| Enums                  |                                                                                                                         |
|------------------------|-------------------------------------------------------------------------------------------------------------------------|
| `TYPE_UNSPECIFIED`     | Default value. This should not be used.                                                                                 |
| `NO_RESERVATION`       | Do not consume from any reserved capacity, only use on-demand.                                                          |
| `ANY_RESERVATION`      | Consume any reservation available, falling back to on-demand.                                                           |
| `SPECIFIC_RESERVATION` | Consume from a specific reservation. When chosen, the reservation must be identified via the `key` and `values` fields. |

### NotebookRuntimeType

Represents a notebook runtime type.

| Enums                               |                                                                                      |
|-------------------------------------|--------------------------------------------------------------------------------------|
| `NOTEBOOK_RUNTIME_TYPE_UNSPECIFIED` | Unspecified notebook runtime type, NotebookRuntimeType will default to USER_DEFINED. |
| `USER_DEFINED`                      | runtime or template with coustomized configurations from user.                       |
| `ONE_CLICK`                         | runtime or template with system defined configurations.                              |

### PostStartupScriptBehavior

Represents a notebook runtime post startup script behavior.

| Enums                                      |                                                                     |
|--------------------------------------------|---------------------------------------------------------------------|
| `POST_STARTUP_SCRIPT_BEHAVIOR_UNSPECIFIED` | Unspecified post startup script behavior.                           |
| `RUN_ONCE`                                 | Run post startup script after runtime is started.                   |
| `RUN_EVERY_START`                          | Run post startup script after runtime is stopped.                   |
| `DOWNLOAD_AND_RUN_EVERY_START`             | Download and run post startup script every time runtime is started. |

## Output Schema

A template that specifies runtime configurations such as machine type, runtime version, network configurations, etc. Multiple runtimes can be created from a runtime template.

### NotebookRuntimeTemplate

**JSON representation**

```
{
  "name": string,
  "displayName": string,
  "description": string,
  "isDefault": boolean,
  "machineSpec": {
    object (MachineSpec)
  },
  "dataPersistentDiskSpec": {
    object (PersistentDiskSpec)
  },
  "networkSpec": {
    object (NetworkSpec)
  },
  "serviceAccount": string,
  "etag": string,
  "labels": {
    string: string,
    ...
  },
  "idleShutdownConfig": {
    object (NotebookIdleShutdownConfig)
  },
  "eucConfig": {
    object (NotebookEucConfig)
  },
  "createTime": string,
  "updateTime": string,
  "notebookRuntimeType": enum (NotebookRuntimeType),
  "shieldedVmConfig": {
    object (ShieldedVmConfig)
  },
  "networkTags": [
    string
  ],
  "encryptionSpec": {
    object (EncryptionSpec)
  },
  "softwareConfig": {
    object (NotebookSoftwareConfig)
  }
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
<td><code>name</code></td>
<td><p><code>string</code></p>
<p>The resource name of the NotebookRuntimeTemplate.</p></td>
</tr>
<tr class="even">
<td><code>displayName</code></td>
<td><p><code>string</code></p>
<p>Required. The display name of the NotebookRuntimeTemplate. The name can be up to 128 characters long and can consist of any UTF-8 characters.</p></td>
</tr>
<tr class="odd">
<td><code>description</code></td>
<td><p><code>string</code></p>
<p>The description of the NotebookRuntimeTemplate.</p></td>
</tr>
<tr class="even">
<td><code>isDefault </code><strong><code>(deprecated)</code></strong></td>
<td><p><code>boolean</code></p>
<blockquote>
<p>This item is deprecated!</p>
</blockquote>
<p>Output only. Deprecated: This field has no behavior. Use notebook_runtime_type = 'ONE_CLICK' instead.</p>
<p>The default template to use if not specified.</p></td>
</tr>
<tr class="odd">
<td><code>machineSpec</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/colab_enterprise_create_notebook_runtime_template#Input.Schema.MachineSpec"><code>MachineSpec</code></a><code> )</code></p>
<p>Optional. Immutable. The specification of a single machine for the template.</p></td>
</tr>
<tr class="even">
<td><code>dataPersistentDiskSpec</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/colab_enterprise_create_notebook_runtime_template#Input.Schema.PersistentDiskSpec"><code>PersistentDiskSpec</code></a><code> )</code></p>
<p>Optional. The specification of [persistent disk][https://cloud.google.com/compute/docs/disks/persistent-disks] attached to the runtime as data disk storage.</p></td>
</tr>
<tr class="odd">
<td><code>networkSpec</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/colab_enterprise_create_notebook_runtime_template#Input.Schema.NetworkSpec"><code>NetworkSpec</code></a><code> )</code></p>
<p>Optional. Network spec.</p></td>
</tr>
<tr class="even">
<td><code>serviceAccount </code><strong><code>(deprecated)</code></strong></td>
<td><p><code>string</code></p>
<blockquote>
<p>This item is deprecated!</p>
</blockquote>
<p>Deprecated: This field is ignored and the "Agent Platform Notebook Service Account" ( <a href="mailto:service-PROJECT_NUMBER@gcp-sa-aiplatform-vm.iam.gserviceaccount.com">service-PROJECT_NUMBER@gcp-sa-aiplatform-vm.iam.gserviceaccount.com</a> ) is used for the runtime workload identity. See <a href="https://cloud.google.com/iam/docs/service-agents#vertex-ai-notebook-service-account">https://cloud.google.com/iam/docs/service-agents#vertex-ai-notebook-service-account</a> for more details. For NotebookExecutionJob, use NotebookExecutionJob.service_account instead.</p>
<p>The service account that the runtime workload runs as. You can use any service account within the same project, but you must have the service account user permission to use the instance.</p>
<p>If not specified, the <a href="https://cloud.google.com/compute/docs/access/service-accounts#default_service_account">Compute Engine default service account</a> is used.</p></td>
</tr>
<tr class="odd">
<td><code>etag</code></td>
<td><p><code>string</code></p>
<p>Used to perform consistent read-modify-write updates. If not set, a blind "overwrite" update happens.</p></td>
</tr>
<tr class="even">
<td><code>labels</code></td>
<td><p><code>map (key: string, value: string)</code></p>
<p>The labels with user-defined metadata to organize the NotebookRuntimeTemplates.</p>
<p>Label keys and values can be no longer than 64 characters (Unicode codepoints), can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed.</p>
<p>See <a href="https://goo.gl/xmQnxf">https://goo.gl/xmQnxf</a> for more information and examples of labels.</p>
<p>An object containing a list of <code>"key": value</code> pairs. Example: <code>{ "name": "wrench", "mass": "1.3kg", "count": "3" }</code> .</p></td>
</tr>
<tr class="odd">
<td><code>idleShutdownConfig</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/colab_enterprise_create_notebook_runtime_template#Input.Schema.NotebookIdleShutdownConfig"><code>NotebookIdleShutdownConfig</code></a><code> )</code></p>
<p>The idle shutdown configuration of NotebookRuntimeTemplate. This config will only be set when idle shutdown is enabled.</p></td>
</tr>
<tr class="even">
<td><code>eucConfig</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/colab_enterprise_create_notebook_runtime_template#Input.Schema.NotebookEucConfig"><code>NotebookEucConfig</code></a><code> )</code></p>
<p>EUC configuration of the NotebookRuntimeTemplate.</p></td>
</tr>
<tr class="odd">
<td><code>createTime</code></td>
<td><p><code>string ( </code><a href="https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp"><code>Timestamp</code></a><code> format)</code></p>
<p>Output only. Timestamp when this NotebookRuntimeTemplate was created.</p>
<p>Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: <code>"2014-10-02T15:01:23Z"</code> , <code>"2014-10-02T15:01:23.045123456Z"</code> or <code>"2014-10-02T15:01:23+05:30"</code> .</p></td>
</tr>
<tr class="even">
<td><code>updateTime</code></td>
<td><p><code>string ( </code><a href="https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp"><code>Timestamp</code></a><code> format)</code></p>
<p>Output only. Timestamp when this NotebookRuntimeTemplate was most recently updated.</p>
<p>Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: <code>"2014-10-02T15:01:23Z"</code> , <code>"2014-10-02T15:01:23.045123456Z"</code> or <code>"2014-10-02T15:01:23+05:30"</code> .</p></td>
</tr>
<tr class="odd">
<td><code>notebookRuntimeType</code></td>
<td><p><code>enum ( </code><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/colab_enterprise_create_notebook_runtime_template#Input.Schema.NotebookRuntimeType"><code>NotebookRuntimeType</code></a><code> )</code></p>
<p>Optional. Immutable. The type of the notebook runtime template.</p></td>
</tr>
<tr class="even">
<td><code>shieldedVmConfig</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/colab_enterprise_create_notebook_runtime_template#Input.Schema.ShieldedVmConfig"><code>ShieldedVmConfig</code></a><code> )</code></p>
<p>Optional. Immutable. Runtime Shielded VM spec.</p></td>
</tr>
<tr class="odd">
<td><code>networkTags[]</code></td>
<td><p><code>string</code></p>
<p>Optional. The Compute Engine tags to add to runtime (see <a href="https://cloud.google.com/vpc/docs/add-remove-network-tags">Tagging instances</a> ).</p></td>
</tr>
<tr class="even">
<td><code>encryptionSpec</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/upload_model#Input.Schema.EncryptionSpec"><code>EncryptionSpec</code></a><code> )</code></p>
<p>Customer-managed encryption key spec for the notebook runtime.</p></td>
</tr>
<tr class="odd">
<td><code>softwareConfig</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/colab_enterprise_create_notebook_runtime_template#Input.Schema.NotebookSoftwareConfig"><code>NotebookSoftwareConfig</code></a><code> )</code></p>
<p>Optional. The notebook software configuration of the notebook runtime.</p></td>
</tr>
</tbody>
</table>

### MachineSpec

**JSON representation**

```
{
  "machineType": string,
  "acceleratorType": enum (AcceleratorType),
  "acceleratorCount": integer,
  "gpuPartitionSize": string,
  "tpuTopology": string,
  "reservationAffinity": {
    object (ReservationAffinity)
  }
}
```

| Fields                |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
|-----------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `machineType`         | `string` Immutable. The type of the machine. See the [list of machine types supported for prediction](https://cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/configure-compute#machine-types) See the [list of machine types supported for custom training](https://cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/configure-compute#machine-types) . For `DeployedModel` this field is optional, and the default value is `n1-standard-2` . For `BatchPredictionJob` or as part of `WorkerPoolSpec` this field is required.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| `acceleratorType`     | `enum ( `[`AcceleratorType`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/colab_enterprise_create_notebook_runtime_template#Input.Schema.AcceleratorType)` )` Immutable. The type of accelerator(s) that may be attached to the machine as per `accelerator_count` .                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| `acceleratorCount`    | `integer` The number of accelerators to attach to the machine. For [accelerator optimized machine types](https://cloud.google.com/compute/docs/accelerator-optimized-machines) , One may set the accelerator_count from 1 to N for machine with N GPUs. If accelerator_count is less than or equal to N / 2, Agent Platform co-schedules the replicas of the model into the same VM to save cost. For example, if the machine type is a3-highgpu-8g, which has 8 H100 GPUs, one can set accelerator_count to 1 to 8. If accelerator_count is 1, 2, 3, or 4, Agent Platform co-schedules 8, 4, 2, or 2 replicas of the model into the same VM to save cost. When co-scheduling, CPU, memory and storage on the VM will be distributed to replicas on the VM. For example, one can expect a co-scheduled replica requesting 2 GPUs out of a 8-GPU VM will receive 25% of the CPU, memory and storage of the VM. Note that the feature is not compatible with \[multihost_gpu_node_count\]\[\]. When multihost_gpu_node_count is set, the co-scheduling will not be enabled. |
| `gpuPartitionSize`    | `string` Optional. Immutable. The Nvidia GPU partition size. When specified, the requested accelerators will be partitioned into smaller GPU partitions. For example, if the request is for 8 units of NVIDIA A100 GPUs, and gpu_partition_size="1g.10gb", the service will create 8 \* 7 = 56 partitioned MIG instances. The partition size must be a value supported by the requested accelerator. Refer to [Nvidia GPU Partitioning](https://cloud.google.com/kubernetes-engine/docs/how-to/gpus-multi#multi-instance_gpu_partitions) for the available partition sizes. If set, the accelerator_count should be set to 1.                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| `tpuTopology`         | `string` Immutable. The topology of the TPUs. Corresponds to the TPU topologies available from GKE. (Example: tpu_topology: "2x2x1").                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| `reservationAffinity` | `object ( `[`ReservationAffinity`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/colab_enterprise_create_notebook_runtime_template#Input.Schema.ReservationAffinity)` )` Optional. Immutable. Configuration controlling how this resource pool consumes reservation.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |

### ReservationAffinity

**JSON representation**

```
{
  "reservationAffinityType": enum (Type),
  "key": string,
  "values": [
    string
  ]
}
```

| Fields                    |                                                                                                                                                                                                                                       |
|---------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `reservationAffinityType` | `enum ( `[`Type`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/colab_enterprise_create_notebook_runtime_template#Input.Schema.Type)` )` Required. Specifies the reservation affinity type. |
| `key`                     | `string` Optional. Corresponds to the label key of a reservation resource. To target a SPECIFIC_RESERVATION by name, use `compute.googleapis.com/reservation-name` as the key and specify the name of your reservation as its value.  |
| `values[]`                | `string` Optional. Corresponds to the label values of a reservation resource. This must be the full resource name of the reservation or reservation block.                                                                            |

### PersistentDiskSpec

**JSON representation**

```
{
  "diskType": string,
  "diskSizeGb": string
}
```

| Fields       |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
|--------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `diskType`   | `string` Type of the disk (default is "pd-standard"). Valid values: "pd-ssd" (Persistent Disk Solid State Drive) "pd-standard" (Persistent Disk Hard Disk Drive) "pd-balanced" (Balanced Persistent Disk) "pd-extreme" (Extreme Persistent Disk) "hyperdisk-balanced" (Hyperdisk Balanced) "hyperdisk-extreme" (Hyperdisk Extreme) "hyperdisk-balanced-high-availability" (Hyperdisk Balanced High Availability) "hyperdisk-ml" (Hyperdisk ML) "hyperdisk-throughput" (Hyperdisk Throughput) |
| `diskSizeGb` | `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)` Size in GB of the disk (default is 100GB).                                                                                                                                                                                                                                                                                                                                                            |

### NetworkSpec

**JSON representation**

```
{
  "enableInternetAccess": boolean,
  "network": string,
  "subnetwork": string
}
```

| Fields                 |                                                                                                                                                  |
|------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------|
| `enableInternetAccess` | `boolean` Whether to enable public internet access. Default false.                                                                               |
| `network`              | `string` The full name of the Google Compute Engine [network](https://cloud.google.com//compute/docs/networks-and-firewalls#networks)            |
| `subnetwork`           | `string` The name of the subnet that this instance is in. Format: `projects/{project_id_or_number}/regions/{region}/subnetworks/{subnetwork_id}` |

### LabelsEntry

**JSON representation**

```
{
  "key": string,
  "value": string
}
```

| Fields  |          |
|---------|----------|
| `key`   | `string` |
| `value` | `string` |

### NotebookIdleShutdownConfig

**JSON representation**

```
{
  "idleTimeout": string,
  "idleShutdownDisabled": boolean
}
```

| Fields                 |                                                                                                                                                                                                                                                                                                                                                                        |
|------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `idleTimeout`          | `string ( `[`Duration`](https://protobuf.dev/reference/protobuf/google.protobuf/#duration)` format)` Required. Duration is accurate to the second. In Notebook, Idle Timeout is accurate to minute so the range of idle_timeout (second) is: 10 \* 60 \~ 1440 \* 60. A duration in seconds with up to nine fractional digits, ending with ' `s` '. Example: `"3.5s"` . |
| `idleShutdownDisabled` | `boolean` Whether Idle Shutdown is disabled in this NotebookRuntimeTemplate.                                                                                                                                                                                                                                                                                           |

### Duration

**JSON representation**

```
{
  "seconds": string,
  "nanos": integer
}
```

| Fields    |                                                                                                                                                                                                                                                                                                                                                                                          |
|-----------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `seconds` | `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)` Signed seconds of the span of time. Must be from -315,576,000,000 to +315,576,000,000 inclusive. Note: these bounds are computed from: 60 sec/min \* 60 min/hr \* 24 hr/day \* 365.25 days/year \* 10000 years                                                                                    |
| `nanos`   | `integer` Signed fractions of a second at nanosecond resolution of the span of time. Durations less than one second are represented with a 0 `seconds` field and a positive or negative `nanos` field. For durations of one second or more, a non-zero value for the `nanos` field must be of the same sign as the `seconds` field. Must be from -999,999,999 to +999,999,999 inclusive. |

### NotebookEucConfig

**JSON representation**

```
{
  "eucDisabled": boolean,
  "bypassActasCheck": boolean
}
```

| Fields             |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
|--------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `eucDisabled`      | `boolean` Input only. Whether EUC is disabled in this NotebookRuntimeTemplate. In proto3, the default value of a boolean is false. In this way, by default EUC will be enabled for NotebookRuntimeTemplate.                                                                                                                                                                                                                                                                                                             |
| `bypassActasCheck` | `boolean` Output only. Whether ActAs check is bypassed for service account attached to the VM. If false, we need ActAs check for the default Compute Engine Service account. When a Runtime is created, a VM is allocated using Default Compute Engine Service Account. Any user requesting to use this Runtime requires Service Account User (ActAs) permission over this SA. If true, Runtime owner is using EUC and does not require the above permission as VM no longer use default Compute Engine SA, but a P4SA. |

### Timestamp

**JSON representation**

```
{
  "seconds": string,
  "nanos": integer
}
```

| Fields    |                                                                                                                                                                                                                                                                                                                      |
|-----------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `seconds` | `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)` Represents seconds of UTC time since Unix epoch 1970-01-01T00:00:00Z. Must be between -62135596800 and 253402300799 inclusive (which corresponds to 0001-01-01T00:00:00Z to 9999-12-31T23:59:59Z).                            |
| `nanos`   | `integer` Non-negative fractions of a second at nanosecond resolution. This field is the nanosecond portion of the duration, not an alternative to seconds. Negative second values with fractions must still have non-negative nanos values that count forward in time. Must be between 0 and 999,999,999 inclusive. |

### ShieldedVmConfig

**JSON representation**

```
{
  "enableSecureBoot": boolean
}
```

| Fields             |                                                                                                                                                                                                                                                                                                                                             |
|--------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `enableSecureBoot` | `boolean` Defines whether the instance has [Secure Boot](https://cloud.google.com/compute/shielded-vm/docs/shielded-vm#secure-boot) enabled. Secure Boot helps ensure that the system only runs authentic software by verifying the digital signature of all boot components, and halting the boot process if signature verification fails. |

### EncryptionSpec

**JSON representation**

```
{
  "kmsKeyName": string
}
```

| Fields       |                                                                                                                                                                                                                                                                   |
|--------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `kmsKeyName` | `string` Required. Resource name of the Cloud KMS key used to protect the resource. The Cloud KMS key must be in the same region as the resource. It must have the format `projects/{project}/locations/{location}/keyRings/{key_ring}/cryptoKeys/{crypto_key}` . |

### NotebookSoftwareConfig

**JSON representation**

```
{
  "env": [
    {
      object (EnvVar)
    }
  ],
  "postStartupScriptConfig": {
    object (PostStartupScriptConfig)
  },

  // Union field runtime_image can be only one of the following:
  "colabImage": {
    object (ColabImage)
  }
  // End of list of possible types for union field runtime_image.
}
```

| Fields                                                                          |                                                                                                                                                                                                                                                                  |
|---------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `env[]`                                                                         | `object ( `[`EnvVar`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/upload_model#Input.Schema.EnvVar)` )` Optional. Environment variables to be passed to the container. Maximum limit is 100.                         |
| `postStartupScriptConfig`                                                       | `object ( `[`PostStartupScriptConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/colab_enterprise_create_notebook_runtime_template#Input.Schema.PostStartupScriptConfig)` )` Optional. Post startup script config. |
| Union field `runtime_image` . `runtime_image` can be only one of the following: |                                                                                                                                                                                                                                                                  |
| `colabImage`                                                                    | `object ( `[`ColabImage`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/colab_enterprise_create_notebook_runtime_template#Input.Schema.ColabImage)` )` Optional. Google-managed NotebookRuntime colab image.           |

### ColabImage

**JSON representation**

```
{
  "releaseName": string,
  "description": string
}
```

| Fields        |                                                                                                                                                                          |
|---------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `releaseName` | `string` Optional. The release name of the NotebookRuntime Colab image, e.g. "py310". If not specified, detault to the latest release.                                   |
| `description` | `string` Output only. A human-readable description of the specified colab image release, populated by the system. Example: "Python 3.10", "Latest - current Python 3.11" |

### EnvVar

**JSON representation**

```
{
  "name": string,
  "value": string
}
```

| Fields  |                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
|---------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `name`  | `string` Required. Name of the environment variable. Must be a valid C identifier.                                                                                                                                                                                                                                                                                                                                                                  |
| `value` | `string` Required. Variables that reference a \$(VAR_NAME) are expanded using the previous defined environment variables in the container and any service environment variables. If a variable cannot be resolved, the reference in the input string will be unchanged. The \$(VAR_NAME) syntax can be escaped with a double \$\$, ie: \$\$(VAR_NAME). Escaped references will never be expanded, regardless of whether the variable exists or not. |

### PostStartupScriptConfig

**JSON representation**

```
{
  "postStartupScript": string,
  "postStartupScriptUrl": string,
  "postStartupScriptBehavior": enum (PostStartupScriptBehavior)
}
```

| Fields                      |                                                                                                                                                                                                                                                                                                                   |
|-----------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `postStartupScript`         | `string` Optional. Post startup script to run after runtime is started.                                                                                                                                                                                                                                           |
| `postStartupScriptUrl`      | `string` Optional. Post startup script url to download. Example: `gs://bucket/script.sh`                                                                                                                                                                                                                          |
| `postStartupScriptBehavior` | `enum ( `[`PostStartupScriptBehavior`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/colab_enterprise_create_notebook_runtime_template#Input.Schema.PostStartupScriptBehavior)` )` Optional. Post startup script behavior that defines download and execution behavior. |

### AcceleratorType

Represents a hardware accelerator type.

| Enums                          |                                                                                                                        |
|--------------------------------|------------------------------------------------------------------------------------------------------------------------|
| `ACCELERATOR_TYPE_UNSPECIFIED` | Unspecified accelerator type, which means no accelerator.                                                              |
| `NVIDIA_TESLA_K80`             | Deprecated: Nvidia Tesla K80 GPU has reached end of support, see <https://cloud.google.com/compute/docs/eol/k80-eol> . |
| `NVIDIA_TESLA_P100`            | Nvidia Tesla P100 GPU.                                                                                                 |
| `NVIDIA_TESLA_V100`            | Nvidia Tesla V100 GPU.                                                                                                 |
| `NVIDIA_TESLA_P4`              | Nvidia Tesla P4 GPU.                                                                                                   |
| `NVIDIA_TESLA_T4`              | Nvidia Tesla T4 GPU.                                                                                                   |
| `NVIDIA_TESLA_A100`            | Nvidia Tesla A100 GPU.                                                                                                 |
| `NVIDIA_A100_80GB`             | Nvidia A100 80GB GPU.                                                                                                  |
| `NVIDIA_L4`                    | Nvidia L4 GPU.                                                                                                         |
| `NVIDIA_H100_80GB`             | Nvidia H100 80Gb GPU.                                                                                                  |
| `NVIDIA_H100_MEGA_80GB`        | Nvidia H100 Mega 80Gb GPU.                                                                                             |
| `NVIDIA_H200_141GB`            | Nvidia H200 141Gb GPU.                                                                                                 |
| `NVIDIA_B200`                  | Nvidia B200 GPU.                                                                                                       |
| `NVIDIA_GB200`                 | Nvidia GB200 GPU.                                                                                                      |
| `NVIDIA_RTX_PRO_6000`          | Nvidia RTX Pro 6000 GPU.                                                                                               |
| `TPU_V2`                       | TPU v2.                                                                                                                |
| `TPU_V3`                       | TPU v3.                                                                                                                |
| `TPU_V4_POD`                   | TPU v4.                                                                                                                |
| `TPU_V5_LITEPOD`               | TPU v5.                                                                                                                |

### Type

Identifies a type of reservation affinity.

| Enums                  |                                                                                                                         |
|------------------------|-------------------------------------------------------------------------------------------------------------------------|
| `TYPE_UNSPECIFIED`     | Default value. This should not be used.                                                                                 |
| `NO_RESERVATION`       | Do not consume from any reserved capacity, only use on-demand.                                                          |
| `ANY_RESERVATION`      | Consume any reservation available, falling back to on-demand.                                                           |
| `SPECIFIC_RESERVATION` | Consume from a specific reservation. When chosen, the reservation must be identified via the `key` and `values` fields. |

### NotebookRuntimeType

Represents a notebook runtime type.

| Enums                               |                                                                                      |
|-------------------------------------|--------------------------------------------------------------------------------------|
| `NOTEBOOK_RUNTIME_TYPE_UNSPECIFIED` | Unspecified notebook runtime type, NotebookRuntimeType will default to USER_DEFINED. |
| `USER_DEFINED`                      | runtime or template with coustomized configurations from user.                       |
| `ONE_CLICK`                         | runtime or template with system defined configurations.                              |

### PostStartupScriptBehavior

Represents a notebook runtime post startup script behavior.

| Enums                                      |                                                                     |
|--------------------------------------------|---------------------------------------------------------------------|
| `POST_STARTUP_SCRIPT_BEHAVIOR_UNSPECIFIED` | Unspecified post startup script behavior.                           |
| `RUN_ONCE`                                 | Run post startup script after runtime is started.                   |
| `RUN_EVERY_START`                          | Run post startup script after runtime is stopped.                   |
| `DOWNLOAD_AND_RUN_EVERY_START`             | Download and run post startup script every time runtime is started. |

### Tool Annotations

Destructive Hint: ✅ \| Idempotent Hint: ✅ \| Read Only Hint: ❌ \| Open World Hint: ❌
