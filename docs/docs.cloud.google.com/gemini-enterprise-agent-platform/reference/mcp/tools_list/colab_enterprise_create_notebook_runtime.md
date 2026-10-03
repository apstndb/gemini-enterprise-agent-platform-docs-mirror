---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/colab_enterprise_create_notebook_runtime
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/colab_enterprise_create_notebook_runtime
title: 'MCP Tools Reference: aiplatform.googleapis.com'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

## Tool: `colab_enterprise_create_notebook_runtime`

Creates a Colab Enterprise runtime that can be used to run code from your notebook (IPYNB file). Use this tool to provision a notebook runtime for a specific user that can be used to run code from on notebooks. Format: 'projects/{project_id}/locations/{region}'. CRITICAL: For {region}, use the region specified in the current context. If no region is specified, prompt the user for one. Do not use 'global'.

The following sample demonstrate how to use `curl` to invoke the `colab_enterprise_create_notebook_runtime` MCP tool.

**Curl Request**

```
curl --location 'https://aiplatform.googleapis.com/mcp/generate' \
--header 'content-type: application/json' \
--header 'accept: application/json, text/event-stream' \
--data '{
  "method": "tools/call",
  "params": {
    "name": "colab_enterprise_create_notebook_runtime",
    "arguments": {
      // provide these details according to the tool's MCP specification
    }
  },
  "jsonrpc": "2.0",
  "id": 1
}'
```

## Input Schema

Request message for `NotebookService.AssignNotebookRuntime` .

### AssignNotebookRuntimeRequest

**JSON representation**

```
{
  "parent": string,
  "notebookRuntimeTemplate": string,
  "notebookRuntime": {
    object (NotebookRuntime)
  },
  "notebookRuntimeId": string
}
```

| Fields                    |                                                                                                                                                                                                                                                                                                                         |
|---------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `parent`                  | `string` Required. The resource name of the Location to get the NotebookRuntime assignment. Format: `projects/{project}/locations/{location}`                                                                                                                                                                           |
| `notebookRuntimeTemplate` | `string` Required. The resource name of the NotebookRuntimeTemplate based on which a NotebookRuntime will be assigned (reuse or create a new one).                                                                                                                                                                      |
| `notebookRuntime`         | `object ( `[`NotebookRuntime`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/colab_enterprise_create_notebook_runtime#Input.Schema.NotebookRuntime)` )` Required. Provide runtime specific information (e.g. runtime owner, notebook id) used for NotebookRuntime assignment. |
| `notebookRuntimeId`       | `string` Optional. User specified ID for the notebook runtime.                                                                                                                                                                                                                                                          |

### NotebookRuntime

**JSON representation**

```
{
  "name": string,
  "runtimeUser": string,
  "notebookRuntimeTemplateRef": {
    object (NotebookRuntimeTemplateRef)
  },
  "proxyUri": string,
  "createTime": string,
  "updateTime": string,
  "healthState": enum (HealthState),
  "displayName": string,
  "description": string,
  "serviceAccount": string,
  "runtimeState": enum (RuntimeState),
  "isUpgradable": boolean,
  "labels": {
    string: string,
    ...
  },
  "expirationTime": string,
  "version": string,
  "notebookRuntimeType": enum (NotebookRuntimeType),
  "machineSpec": {
    object (MachineSpec)
  },
  "dataPersistentDiskSpec": {
    object (PersistentDiskSpec)
  },
  "networkSpec": {
    object (NetworkSpec)
  },
  "idleShutdownConfig": {
    object (NotebookIdleShutdownConfig)
  },
  "eucConfig": {
    object (NotebookEucConfig)
  },
  "shieldedVmConfig": {
    object (ShieldedVmConfig)
  },
  "networkTags": [
    string
  ],
  "softwareConfig": {
    object (NotebookSoftwareConfig)
  },
  "encryptionSpec": {
    object (EncryptionSpec)
  },
  "satisfiesPzs": boolean,
  "satisfiesPzi": boolean
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
<p>Output only. The resource name of the NotebookRuntime.</p></td>
</tr>
<tr class="even">
<td><code>runtimeUser</code></td>
<td><p><code>string</code></p>
<p>Required. The user email of the NotebookRuntime.</p></td>
</tr>
<tr class="odd">
<td><code>notebookRuntimeTemplateRef</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/colab_enterprise_create_notebook_runtime#Input.Schema.NotebookRuntimeTemplateRef"><code>NotebookRuntimeTemplateRef</code></a><code> )</code></p>
<p>Output only. The pointer to NotebookRuntimeTemplate this NotebookRuntime is created from.</p></td>
</tr>
<tr class="even">
<td><code>proxyUri</code></td>
<td><p><code>string</code></p>
<p>Output only. The proxy endpoint used to access the NotebookRuntime.</p></td>
</tr>
<tr class="odd">
<td><code>createTime</code></td>
<td><p><code>string ( </code><a href="https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp"><code>Timestamp</code></a><code> format)</code></p>
<p>Output only. Timestamp when this NotebookRuntime was created.</p>
<p>Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: <code>"2014-10-02T15:01:23Z"</code> , <code>"2014-10-02T15:01:23.045123456Z"</code> or <code>"2014-10-02T15:01:23+05:30"</code> .</p></td>
</tr>
<tr class="even">
<td><code>updateTime</code></td>
<td><p><code>string ( </code><a href="https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp"><code>Timestamp</code></a><code> format)</code></p>
<p>Output only. Timestamp when this NotebookRuntime was most recently updated.</p>
<p>Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: <code>"2014-10-02T15:01:23Z"</code> , <code>"2014-10-02T15:01:23.045123456Z"</code> or <code>"2014-10-02T15:01:23+05:30"</code> .</p></td>
</tr>
<tr class="odd">
<td><code>healthState</code></td>
<td><p><code>enum ( </code><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/colab_enterprise_create_notebook_runtime#Input.Schema.HealthState"><code>HealthState</code></a><code> )</code></p>
<p>Output only. The health state of the NotebookRuntime.</p></td>
</tr>
<tr class="even">
<td><code>displayName</code></td>
<td><p><code>string</code></p>
<p>Required. The display name of the NotebookRuntime. The name can be up to 128 characters long and can consist of any UTF-8 characters.</p></td>
</tr>
<tr class="odd">
<td><code>description</code></td>
<td><p><code>string</code></p>
<p>The description of the NotebookRuntime.</p></td>
</tr>
<tr class="even">
<td><code>serviceAccount</code></td>
<td><p><code>string</code></p>
<p>Output only. Deprecated: This field is no longer used and the "Agent Platform Notebook Service Account" ( <a href="mailto:service-PROJECT_NUMBER@gcp-sa-aiplatform-vm.iam.gserviceaccount.com">service-PROJECT_NUMBER@gcp-sa-aiplatform-vm.iam.gserviceaccount.com</a> ) is used for the runtime workload identity. See <a href="https://cloud.google.com/iam/docs/service-agents#vertex-ai-notebook-service-account">https://cloud.google.com/iam/docs/service-agents#vertex-ai-notebook-service-account</a> for more details.</p>
<p>The service account that the NotebookRuntime workload runs as.</p></td>
</tr>
<tr class="odd">
<td><code>runtimeState</code></td>
<td><p><code>enum ( </code><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/colab_enterprise_create_notebook_runtime#Input.Schema.RuntimeState"><code>RuntimeState</code></a><code> )</code></p>
<p>Output only. The runtime (instance) state of the NotebookRuntime.</p></td>
</tr>
<tr class="even">
<td><code>isUpgradable</code></td>
<td><p><code>boolean</code></p>
<p>Output only. Whether NotebookRuntime is upgradable.</p></td>
</tr>
<tr class="odd">
<td><code>labels</code></td>
<td><p><code>map (key: string, value: string)</code></p>
<p>The labels with user-defined metadata to organize your NotebookRuntime.</p>
<p>Label keys and values can be no longer than 64 characters (Unicode codepoints), can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed. No more than 64 user labels can be associated with one NotebookRuntime (System labels are excluded).</p>
<p>See <a href="https://goo.gl/xmQnxf">https://goo.gl/xmQnxf</a> for more information and examples of labels. System reserved label keys are prefixed with "aiplatform.googleapis.com/" and are immutable. Following system labels exist for NotebookRuntime:</p>
<ul>
<li>"aiplatform.googleapis.com/notebook_runtime_gce_instance_id": output only, its value is the Compute Engine instance id.</li>
<li>"aiplatform.googleapis.com/colab_enterprise_entry_service": its value is either "bigquery" or "vertex"; if absent, it should be "vertex". This is to describe the entry service, either BigQuery or Vertex.</li>
</ul>
<p>An object containing a list of <code>"key": value</code> pairs. Example: <code>{ "name": "wrench", "mass": "1.3kg", "count": "3" }</code> .</p></td>
</tr>
<tr class="even">
<td><code>expirationTime</code></td>
<td><p><code>string ( </code><a href="https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp"><code>Timestamp</code></a><code> format)</code></p>
<p>Output only. Timestamp when this NotebookRuntime will be expired: 1. System Predefined NotebookRuntime: 24 hours after creation. After expiration, system predifined runtime will be deleted. 2. User created NotebookRuntime: 6 months after last upgrade. After expiration, user created runtime will be stopped and allowed for upgrade.</p>
<p>Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: <code>"2014-10-02T15:01:23Z"</code> , <code>"2014-10-02T15:01:23.045123456Z"</code> or <code>"2014-10-02T15:01:23+05:30"</code> .</p></td>
</tr>
<tr class="odd">
<td><code>version</code></td>
<td><p><code>string</code></p>
<p>Output only. The VM os image version of NotebookRuntime.</p></td>
</tr>
<tr class="even">
<td><code>notebookRuntimeType</code></td>
<td><p><code>enum ( </code><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/colab_enterprise_create_notebook_runtime_template#Input.Schema.NotebookRuntimeType"><code>NotebookRuntimeType</code></a><code> )</code></p>
<p>Output only. The type of the notebook runtime.</p></td>
</tr>
<tr class="odd">
<td><code>machineSpec</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/colab_enterprise_create_notebook_runtime_template#Input.Schema.MachineSpec"><code>MachineSpec</code></a><code> )</code></p>
<p>Output only. The specification of a single machine used by the notebook runtime.</p></td>
</tr>
<tr class="even">
<td><code>dataPersistentDiskSpec</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/colab_enterprise_create_notebook_runtime_template#Input.Schema.PersistentDiskSpec"><code>PersistentDiskSpec</code></a><code> )</code></p>
<p>Output only. The specification of [persistent disk][https://cloud.google.com/compute/docs/disks/persistent-disks] attached to the notebook runtime as data disk storage.</p></td>
</tr>
<tr class="odd">
<td><code>networkSpec</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/colab_enterprise_create_notebook_runtime_template#Input.Schema.NetworkSpec"><code>NetworkSpec</code></a><code> )</code></p>
<p>Output only. Network spec of the notebook runtime.</p></td>
</tr>
<tr class="even">
<td><code>idleShutdownConfig</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/colab_enterprise_create_notebook_runtime_template#Input.Schema.NotebookIdleShutdownConfig"><code>NotebookIdleShutdownConfig</code></a><code> )</code></p>
<p>Output only. The idle shutdown configuration of the notebook runtime.</p></td>
</tr>
<tr class="odd">
<td><code>eucConfig</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/colab_enterprise_create_notebook_runtime_template#Input.Schema.NotebookEucConfig"><code>NotebookEucConfig</code></a><code> )</code></p>
<p>Output only. EUC configuration of the notebook runtime.</p></td>
</tr>
<tr class="even">
<td><code>shieldedVmConfig</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/colab_enterprise_create_notebook_runtime_template#Input.Schema.ShieldedVmConfig"><code>ShieldedVmConfig</code></a><code> )</code></p>
<p>Output only. Runtime Shielded VM spec.</p></td>
</tr>
<tr class="odd">
<td><code>networkTags[]</code></td>
<td><p><code>string</code></p>
<p>Optional. The Compute Engine tags to add to runtime (see <a href="https://cloud.google.com/vpc/docs/add-remove-network-tags">Tagging instances</a> ).</p></td>
</tr>
<tr class="even">
<td><code>softwareConfig</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/colab_enterprise_create_notebook_runtime_template#Input.Schema.NotebookSoftwareConfig"><code>NotebookSoftwareConfig</code></a><code> )</code></p>
<p>Output only. Software config of the notebook runtime.</p></td>
</tr>
<tr class="odd">
<td><code>encryptionSpec</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/upload_model#Input.Schema.EncryptionSpec"><code>EncryptionSpec</code></a><code> )</code></p>
<p>Output only. Customer-managed encryption key spec for the notebook runtime.</p></td>
</tr>
<tr class="even">
<td><code>satisfiesPzs</code></td>
<td><p><code>boolean</code></p>
<p>Output only. Reserved for future use.</p></td>
</tr>
<tr class="odd">
<td><code>satisfiesPzi</code></td>
<td><p><code>boolean</code></p>
<p>Output only. Reserved for future use.</p></td>
</tr>
</tbody>
</table>

### NotebookRuntimeTemplateRef

**JSON representation**

```
{
  "notebookRuntimeTemplate": string
}
```

| Fields                    |                                                                     |
|---------------------------|---------------------------------------------------------------------|
| `notebookRuntimeTemplate` | `string` Immutable. A resource name of the NotebookRuntimeTemplate. |

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

### HealthState

The substate of the NotebookRuntime to display health information.

| Enums                      |                                                                 |
|----------------------------|-----------------------------------------------------------------|
| `HEALTH_STATE_UNSPECIFIED` | Unspecified health state.                                       |
| `HEALTHY`                  | NotebookRuntime is in healthy state. Applies to ACTIVE state.   |
| `UNHEALTHY`                | NotebookRuntime is in unhealthy state. Applies to ACTIVE state. |

### RuntimeState

The substate of the NotebookRuntime to display state of runtime. The resource of NotebookRuntime is in ACTIVE state for these sub state.

| Enums                       |                                                                                                       |
|-----------------------------|-------------------------------------------------------------------------------------------------------|
| `RUNTIME_STATE_UNSPECIFIED` | Unspecified runtime state.                                                                            |
| `RUNNING`                   | NotebookRuntime is in running state.                                                                  |
| `BEING_STARTED`             | NotebookRuntime is in starting state. This is when the runtime is being started from a stopped state. |
| `BEING_STOPPED`             | NotebookRuntime is in stopping state.                                                                 |
| `STOPPED`                   | NotebookRuntime is in stopped state.                                                                  |
| `BEING_UPGRADED`            | NotebookRuntime is in upgrading state. It is in the middle of upgrading process.                      |
| `ERROR`                     | NotebookRuntime was unable to start/stop properly.                                                    |
| `INVALID`                   | NotebookRuntime is in invalid state. Cannot be recovered.                                             |

### NotebookRuntimeType

Represents a notebook runtime type.

| Enums                               |                                                                                      |
|-------------------------------------|--------------------------------------------------------------------------------------|
| `NOTEBOOK_RUNTIME_TYPE_UNSPECIFIED` | Unspecified notebook runtime type, NotebookRuntimeType will default to USER_DEFINED. |
| `USER_DEFINED`                      | runtime or template with coustomized configurations from user.                       |
| `ONE_CLICK`                         | runtime or template with system defined configurations.                              |

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

### PostStartupScriptBehavior

Represents a notebook runtime post startup script behavior.

| Enums                                      |                                                                     |
|--------------------------------------------|---------------------------------------------------------------------|
| `POST_STARTUP_SCRIPT_BEHAVIOR_UNSPECIFIED` | Unspecified post startup script behavior.                           |
| `RUN_ONCE`                                 | Run post startup script after runtime is started.                   |
| `RUN_EVERY_START`                          | Run post startup script after runtime is stopped.                   |
| `DOWNLOAD_AND_RUN_EVERY_START`             | Download and run post startup script every time runtime is started. |

## Output Schema

This resource represents a long-running operation that is the result of a network API call.

### Operation

**JSON representation**

```
{
  "name": string,
  "metadata": {
    "@type": string,
    field1: ...,
    ...
  },
  "done": boolean,

  // Union field result can be only one of the following:
  "error": {
    object (Status)
  },
  "response": {
    "@type": string,
    field1: ...,
    ...
  }
  // End of list of possible types for union field result.
}
```

| Fields                                                                                                                                                                                                                                                                                                                          |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `name`                                                                                                                                                                                                                                                                                                                          | `string` The server-assigned name, which is only unique within the same service that originally returns it. If you use the default HTTP mapping, the `name` should be a resource name ending with `operations/{unique_id}` .                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| `metadata`                                                                                                                                                                                                                                                                                                                      | `object` Service-specific metadata associated with the operation. It typically contains progress information and common metadata such as create time. Some services might not provide such metadata. Any method that returns a long-running operation should document the metadata type, if any. An object containing fields of an arbitrary type. An additional field `"@type"` contains a URI identifying the type. Example: `{ "id": 1234, "@type": "types.example.com/standard/id" }` .                                                                                                                                                                                                                     |
| `done`                                                                                                                                                                                                                                                                                                                          | `boolean` If the value is `false` , it means the operation is still in progress. If `true` , the operation is completed, and either `error` or `response` is available.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
| Union field `result` . The operation result, which can be either an `error` or a valid `response` . If `done` == `false` , neither `error` nor `response` is set. If `done` == `true` , exactly one of `error` or `response` can be set. Some services might not provide the result. `result` can be only one of the following: |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| `error`                                                                                                                                                                                                                                                                                                                         | `object ( `[`Status`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/create_endpoint#Output.Schema.Status)` )` The error result of the operation in case of failure or cancellation.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| `response`                                                                                                                                                                                                                                                                                                                      | `object` The normal, successful response of the operation. If the original method returns no data on success, such as `Delete` , the response is `google.protobuf.Empty` . If the original method is standard `Get` / `Create` / `Update` , the response should be the resource. For other methods, the response should have the type `XxxResponse` , where `Xxx` is the original method name. For example, if the original method name is `TakeSnapshot()` , the inferred response type is `TakeSnapshotResponse` . An object containing fields of an arbitrary type. An additional field `"@type"` contains a URI identifying the type. Example: `{ "id": 1234, "@type": "types.example.com/standard/id" }` . |

### Any

**JSON representation**

```
{
  "typeUrl": string,
  "value": string
}
```

| Fields    |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
|-----------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `typeUrl` | `string` Identifies the type of the serialized Protobuf message with a URI reference consisting of a prefix ending in a slash and the fully-qualified type name. Example: type.googleapis.com/google.protobuf.StringValue This string must contain at least one `/` character, and the content after the last `/` must be the fully-qualified name of the type in canonical form, without a leading dot. Do not write a scheme on these URI references so that clients do not attempt to contact them. The prefix is arbitrary and Protobuf implementations are expected to simply strip off everything up to and including the last `/` to identify the type. `type.googleapis.com/` is a common default prefix that some legacy implementations require. This prefix does not indicate the origin of the type, and URIs containing it are not expected to respond to any requests. All type URL strings must be legal URI references with the additional restriction (for the text format) that the content of the reference must consist only of alphanumeric characters, percent-encoded escapes, and characters in the following set (not including the outer backticks): `/-.~_!$&()*+,;=` . Despite our allowing percent encodings, implementations should not unescape them to prevent confusion with existing parsers. For example, `type.googleapis.com%2FFoo` should be rejected. In the original design of `Any` , the possibility of launching a type resolution service at these type URLs was considered but Protobuf never implemented one and considers contacting these URLs to be problematic and a potential security issue. Do not attempt to contact type URLs. |
| `value`   | `string ( `[`bytes`](https://developers.google.com/discovery/v1/type-format)` format)` Holds a Protobuf serialization of the type described by type_url. A base64-encoded string.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |

### Status

**JSON representation**

```
{
  "code": integer,
  "message": string,
  "details": [
    {
      "@type": string,
      field1: ...,
      ...
    }
  ]
}
```

| Fields      |                                                                                                                                                                                                                                                                                                              |
|-------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `code`      | `integer` The status code, which should be an enum value of `google.rpc.Code` .                                                                                                                                                                                                                              |
| `message`   | `string` A developer-facing error message, which should be in English. Any user-facing error message should be localized and sent in the `google.rpc.Status.details` field, or localized by the client.                                                                                                      |
| `details[]` | `object` A list of messages that carry the error details. There is a common set of message types for APIs to use. An object containing fields of an arbitrary type. An additional field `"@type"` contains a URI identifying the type. Example: `{ "id": 1234, "@type": "types.example.com/standard/id" }` . |

### Tool Annotations

Destructive Hint: ❌ \| Idempotent Hint: ❌ \| Read Only Hint: ❌ \| Open World Hint: ❌
