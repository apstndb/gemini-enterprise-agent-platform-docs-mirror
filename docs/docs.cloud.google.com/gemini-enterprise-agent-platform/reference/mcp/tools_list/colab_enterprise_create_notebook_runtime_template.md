---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/colab_enterprise_create_notebook_runtime_template
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/colab_enterprise_create_notebook_runtime_template
title: 'MCP Tools Reference: aiplatform.googleapis.com'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

## Tool: `colab_enterprise_create_notebook_runtime_template`

Creates a new Colab Enterprise runtime template. Use this tool to define configurations for notebook runtimes, such as machine type and software setup. Format: 'projects/{project\_id}/locations/{region}'. CRITICAL: For {region}, use the region specified in the current context. If no region is specified, prompt the user for one. Do not use 'global'.

The following sample demonstrate how to use `curl` to invoke the `colab_enterprise_create_notebook_runtime_template` MCP tool.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>Curl Request</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" data-syntax="Bash" translate="no"><code>                  
curl --location &#39;https://aiplatform.googleapis.com/mcp/generate&#39; \
--header &#39;content-type: application/json&#39; \
--header &#39;accept: application/json, text/event-stream&#39; \
--data &#39;{
  &quot;method&quot;: &quot;tools/call&quot;,
  &quot;params&quot;: {
    &quot;name&quot;: &quot;colab_enterprise_create_notebook_runtime_template&quot;,
    &quot;arguments&quot;: {
      // provide these details according to the tool&#39;s MCP specification
    }
  },
  &quot;jsonrpc&quot;: &quot;2.0&quot;,
  &quot;id&quot;: 1
}&#39;
                </code></pre></td>
</tr>
</tbody>
</table>

## Input Schema

Request message for `NotebookService.CreateNotebookRuntimeTemplate` .

### CreateNotebookRuntimeTemplateRequest

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;parent&quot;: string,&quot;notebookRuntimeTemplate&quot;: {object (NotebookRuntimeTemplate)},&quot;notebookRuntimeTemplateId&quot;: string}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`parent`

`string`

Required. The resource name of the Location to create the NotebookRuntimeTemplate. Format: `projects/{project}/locations/{location}`

`notebookRuntimeTemplate`

` object ( NotebookRuntimeTemplate  ` )

Required. The NotebookRuntimeTemplate to create.

`notebookRuntimeTemplateId`

`string`

Optional. User specified ID for the notebook runtime template.

### NotebookRuntimeTemplate

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;name&quot;: string,&quot;displayName&quot;: string,&quot;description&quot;: string,&quot;isDefault&quot;: boolean,&quot;machineSpec&quot;: {object (MachineSpec)},&quot;dataPersistentDiskSpec&quot;: {object (PersistentDiskSpec)},&quot;networkSpec&quot;: {object (NetworkSpec)},&quot;serviceAccount&quot;: string,&quot;etag&quot;: string,&quot;labels&quot;: {string: string,...},&quot;idleShutdownConfig&quot;: {object (NotebookIdleShutdownConfig)},&quot;eucConfig&quot;: {object (NotebookEucConfig)},&quot;createTime&quot;: string,&quot;updateTime&quot;: string,&quot;notebookRuntimeType&quot;: enum (NotebookRuntimeType),&quot;shieldedVmConfig&quot;: {object (ShieldedVmConfig)},&quot;networkTags&quot;: [string],&quot;encryptionSpec&quot;: {object (EncryptionSpec)},&quot;softwareConfig&quot;: {object (NotebookSoftwareConfig)}}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`name`

`string`

The resource name of the NotebookRuntimeTemplate.

`displayName`

`string`

Required. The display name of the NotebookRuntimeTemplate. The name can be up to 128 characters long and can consist of any UTF-8 characters.

`description`

`string`

The description of the NotebookRuntimeTemplate.

` isDefault (deprecated)  `

`boolean`

> This item is deprecated\!

Output only. Deprecated: This field has no behavior. Use notebook\_runtime\_type = 'ONE\_CLICK' instead.

The default template to use if not specified.

`machineSpec`

` object ( MachineSpec  ` )

Optional. Immutable. The specification of a single machine for the template.

`dataPersistentDiskSpec`

` object ( PersistentDiskSpec  ` )

Optional. The specification of \[persistent disk\]\[https://cloud.google.com/compute/docs/disks/persistent-disks\] attached to the runtime as data disk storage.

`networkSpec`

` object ( NetworkSpec  ` )

Optional. Network spec.

` serviceAccount (deprecated)  `

`string`

> This item is deprecated\!

Deprecated: This field is ignored and the "Agent Platform Notebook Service Account" ( <service-PROJECT_NUMBER@gcp-sa-aiplatform-vm.iam.gserviceaccount.com> ) is used for the runtime workload identity. See <https://cloud.google.com/iam/docs/service-agents#vertex-ai-notebook-service-account> for more details. For NotebookExecutionJob, use NotebookExecutionJob.service\_account instead.

The service account that the runtime workload runs as. You can use any service account within the same project, but you must have the service account user permission to use the instance.

If not specified, the [Compute Engine default service account](https://cloud.google.com/compute/docs/access/service-accounts#default_service_account) is used.

`etag`

`string`

Used to perform consistent read-modify-write updates. If not set, a blind "overwrite" update happens.

`labels`

`map (key: string, value: string)`

The labels with user-defined metadata to organize the NotebookRuntimeTemplates.

Label keys and values can be no longer than 64 characters (Unicode codepoints), can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed.

See <https://goo.gl/xmQnxf> for more information and examples of labels.

An object containing a list of `"key": value` pairs. Example: `{ "name": "wrench", "mass": "1.3kg", "count": "3" }` .

`idleShutdownConfig`

` object ( NotebookIdleShutdownConfig  ` )

The idle shutdown configuration of NotebookRuntimeTemplate. This config will only be set when idle shutdown is enabled.

`eucConfig`

` object ( NotebookEucConfig  ` )

EUC configuration of the NotebookRuntimeTemplate.

`createTime`

` string ( Timestamp  ` format)

Output only. Timestamp when this NotebookRuntimeTemplate was created.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`updateTime`

` string ( Timestamp  ` format)

Output only. Timestamp when this NotebookRuntimeTemplate was most recently updated.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`notebookRuntimeType`

`enum ( NotebookRuntimeType` )

Optional. Immutable. The type of the notebook runtime template.

`shieldedVmConfig`

` object ( ShieldedVmConfig  ` )

Optional. Immutable. Runtime Shielded VM spec.

`networkTags[]`

`string`

Optional. The Compute Engine tags to add to runtime (see [Tagging instances](https://cloud.google.com/vpc/docs/add-remove-network-tags) ).

`encryptionSpec`

` object ( EncryptionSpec  ` )

Customer-managed encryption key spec for the notebook runtime.

`softwareConfig`

` object ( NotebookSoftwareConfig  ` )

Optional. The notebook software configuration of the notebook runtime.

### MachineSpec

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;machineType&quot;: string,&quot;acceleratorType&quot;: enum (AcceleratorType),&quot;acceleratorCount&quot;: integer,&quot;gpuPartitionSize&quot;: string,&quot;tpuTopology&quot;: string,&quot;reservationAffinity&quot;: {object (ReservationAffinity)}}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`machineType`

`string`

Immutable. The type of the machine.

See the [list of machine types supported for prediction](https://cloud.google.com/vertex-ai/docs/predictions/configure-compute#machine-types)

See the [list of machine types supported for custom training](https://cloud.google.com/vertex-ai/docs/training/configure-compute#machine-types) .

For `DeployedModel` this field is optional, and the default value is `n1-standard-2` . For `BatchPredictionJob` or as part of `WorkerPoolSpec` this field is required.

`acceleratorType`

`enum ( AcceleratorType` )

Immutable. The type of accelerator(s) that may be attached to the machine as per `accelerator_count` .

`acceleratorCount`

`integer`

The number of accelerators to attach to the machine.

For accelerator optimized machine types ( <https://cloud.google.com/compute/docs/accelerator-optimized-machines> , One may set the accelerator\_count from 1 to N for machine with N GPUs. If accelerator\_count is less than or equal to N / 2, Vertex will co-schedule the replicas of the model into the same VM to save cost.

For example, if the machine type is a3-highgpu-8g, which has 8 H100 GPUs, one can set accelerator\_count to 1 to 8. If accelerator\_count is 1, 2, 3, or 4, Vertex will co-schedule 8, 4, 2, or 2 replicas of the model into the same VM to save cost.

When co-scheduling, CPU, memory and storage on the VM will be distributed to replicas on the VM. For example, one can expect a co-scheduled replica requesting 2 GPUs out of a 8-GPU VM will receive 25% of the CPU, memory and storage of the VM.

Note that the feature is not compatible with \[multihost\_gpu\_node\_count\]\[\]. When multihost\_gpu\_node\_count is set, the co-scheduling will not be enabled.

`gpuPartitionSize`

`string`

Optional. Immutable. The Nvidia GPU partition size.

When specified, the requested accelerators will be partitioned into smaller GPU partitions. For example, if the request is for 8 units of NVIDIA A100 GPUs, and gpu\_partition\_size="1g.10gb", the service will create 8 \* 7 = 56 partitioned MIG instances.

The partition size must be a value supported by the requested accelerator. Refer to [Nvidia GPU Partitioning](https://cloud.google.com/kubernetes-engine/docs/how-to/gpus-multi#multi-instance_gpu_partitions) for the available partition sizes.

If set, the accelerator\_count should be set to 1.

`tpuTopology`

`string`

Immutable. The topology of the TPUs. Corresponds to the TPU topologies available from GKE. (Example: tpu\_topology: "2x2x1").

`reservationAffinity`

` object ( ReservationAffinity  ` )

Optional. Immutable. Configuration controlling how this resource pool consumes reservation.

### ReservationAffinity

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;reservationAffinityType&quot;: enum (Type),&quot;key&quot;: string,&quot;values&quot;: [string]}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`reservationAffinityType`

`enum ( Type` )

Required. Specifies the reservation affinity type.

`key`

`string`

Optional. Corresponds to the label key of a reservation resource. To target a SPECIFIC\_RESERVATION by name, use `compute.googleapis.com/reservation-name` as the key and specify the name of your reservation as its value.

`values[]`

`string`

Optional. Corresponds to the label values of a reservation resource. This must be the full resource name of the reservation or reservation block.

### PersistentDiskSpec

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
  &quot;diskType&quot;: string,
  &quot;diskSizeGb&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`diskType`

`string`

Type of the disk (default is "pd-standard"). Valid values: "pd-ssd" (Persistent Disk Solid State Drive) "pd-standard" (Persistent Disk Hard Disk Drive) "pd-balanced" (Balanced Persistent Disk) "pd-extreme" (Extreme Persistent Disk)

`diskSizeGb`

`string ( int64 format)`

Size in GB of the disk (default is 100GB).

### NetworkSpec

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
  &quot;enableInternetAccess&quot;: boolean,
  &quot;network&quot;: string,
  &quot;subnetwork&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`enableInternetAccess`

`boolean`

Whether to enable public internet access. Default false.

`network`

`string`

The full name of the Google Compute Engine [network](https://cloud.google.com//compute/docs/networks-and-firewalls#networks)

`subnetwork`

`string`

The name of the subnet that this instance is in. Format: `projects/{project_id_or_number}/regions/{region}/subnetworks/{subnetwork_id}`

### LabelsEntry

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
  &quot;key&quot;: string,
  &quot;value&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`key`

`string`

`value`

`string`

### NotebookIdleShutdownConfig

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
  &quot;idleTimeout&quot;: string,
  &quot;idleShutdownDisabled&quot;: boolean
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`idleTimeout`

` string ( Duration  ` format)

Required. Duration is accurate to the second. In Notebook, Idle Timeout is accurate to minute so the range of idle\_timeout (second) is: 10 \* 60 \~ 1440 \* 60.

A duration in seconds with up to nine fractional digits, ending with ' `s` '. Example: `"3.5s"` .

`idleShutdownDisabled`

`boolean`

Whether Idle Shutdown is disabled in this NotebookRuntimeTemplate.

### Duration

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
  &quot;seconds&quot;: string,
  &quot;nanos&quot;: integer
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`seconds`

`string ( int64 format)`

Signed seconds of the span of time. Must be from -315,576,000,000 to +315,576,000,000 inclusive. Note: these bounds are computed from: 60 sec/min \* 60 min/hr \* 24 hr/day \* 365.25 days/year \* 10000 years

`nanos`

`integer`

Signed fractions of a second at nanosecond resolution of the span of time. Durations less than one second are represented with a 0 `seconds` field and a positive or negative `nanos` field. For durations of one second or more, a non-zero value for the `nanos` field must be of the same sign as the `seconds` field. Must be from -999,999,999 to +999,999,999 inclusive.

### NotebookEucConfig

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
  &quot;eucDisabled&quot;: boolean,
  &quot;bypassActasCheck&quot;: boolean
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`eucDisabled`

`boolean`

Input only. Whether EUC is disabled in this NotebookRuntimeTemplate. In proto3, the default value of a boolean is false. In this way, by default EUC will be enabled for NotebookRuntimeTemplate.

`bypassActasCheck`

`boolean`

Output only. Whether ActAs check is bypassed for service account attached to the VM. If false, we need ActAs check for the default Compute Engine Service account. When a Runtime is created, a VM is allocated using Default Compute Engine Service Account. Any user requesting to use this Runtime requires Service Account User (ActAs) permission over this SA. If true, Runtime owner is using EUC and does not require the above permission as VM no longer use default Compute Engine SA, but a P4SA.

### Timestamp

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
  &quot;seconds&quot;: string,
  &quot;nanos&quot;: integer
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`seconds`

`string ( int64 format)`

Represents seconds of UTC time since Unix epoch 1970-01-01T00:00:00Z. Must be between -62135596800 and 253402300799 inclusive (which corresponds to 0001-01-01T00:00:00Z to 9999-12-31T23:59:59Z).

`nanos`

`integer`

Non-negative fractions of a second at nanosecond resolution. This field is the nanosecond portion of the duration, not an alternative to seconds. Negative second values with fractions must still have non-negative nanos values that count forward in time. Must be between 0 and 999,999,999 inclusive.

### ShieldedVmConfig

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
  &quot;enableSecureBoot&quot;: boolean
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`enableSecureBoot`

`boolean`

Defines whether the instance has [Secure Boot](https://cloud.google.com/compute/shielded-vm/docs/shielded-vm#secure-boot) enabled.

Secure Boot helps ensure that the system only runs authentic software by verifying the digital signature of all boot components, and halting the boot process if signature verification fails.

### EncryptionSpec

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
  &quot;kmsKeyName&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`kmsKeyName`

`string`

Required. Resource name of the Cloud KMS key used to protect the resource.

The Cloud KMS key must be in the same region as the resource. It must have the format `projects/{project}/locations/{location}/keyRings/{key_ring}/cryptoKeys/{crypto_key}` .

### NotebookSoftwareConfig

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;env&quot;: [{object (EnvVar)}],&quot;postStartupScriptConfig&quot;: {object (PostStartupScriptConfig)},// Union field runtime_image can be only one of the following:&quot;colabImage&quot;: {object (ColabImage)}// End of list of possible types for union field runtime_image.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`env[]`

` object ( EnvVar  ` )

Optional. Environment variables to be passed to the container. Maximum limit is 100.

`postStartupScriptConfig`

` object ( PostStartupScriptConfig  ` )

Optional. Post startup script config.

Union field `runtime_image` .

`runtime_image` can be only one of the following:

`colabImage`

` object ( ColabImage  ` )

Optional. Google-managed NotebookRuntime colab image.

### ColabImage

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
  &quot;releaseName&quot;: string,
  &quot;description&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`releaseName`

`string`

Optional. The release name of the NotebookRuntime Colab image, e.g. "py310". If not specified, detault to the latest release.

`description`

`string`

Output only. A human-readable description of the specified colab image release, populated by the system. Example: "Python 3.10", "Latest - current Python 3.11"

### EnvVar

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
  &quot;name&quot;: string,
  &quot;value&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`name`

`string`

Required. Name of the environment variable. Must be a valid C identifier.

`value`

`string`

Required. Variables that reference a $(VAR\_NAME) are expanded using the previous defined environment variables in the container and any service environment variables. If a variable cannot be resolved, the reference in the input string will be unchanged. The $(VAR\_NAME) syntax can be escaped with a double $$, ie: $$(VAR\_NAME). Escaped references will never be expanded, regardless of whether the variable exists or not.

### PostStartupScriptConfig

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;postStartupScript&quot;: string,&quot;postStartupScriptUrl&quot;: string,&quot;postStartupScriptBehavior&quot;: enum (PostStartupScriptBehavior)}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`postStartupScript`

`string`

Optional. Post startup script to run after runtime is started.

`postStartupScriptUrl`

`string`

Optional. Post startup script url to download. Example: `gs://bucket/script.sh`

`postStartupScriptBehavior`

`enum ( PostStartupScriptBehavior` )

Optional. Post startup script behavior that defines download and execution behavior.

## Output Schema

This resource represents a long-running operation that is the result of a network API call.

### Operation

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;name&quot;: string,&quot;metadata&quot;: {&quot;@type&quot;: string,field1: ...,...},&quot;done&quot;: boolean,// Union field result can be only one of the following:&quot;error&quot;: {object (Status)},&quot;response&quot;: {&quot;@type&quot;: string,field1: ...,...}// End of list of possible types for union field result.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`name`

`string`

The server-assigned name, which is only unique within the same service that originally returns it. If you use the default HTTP mapping, the `name` should be a resource name ending with `operations/{unique_id}` .

`metadata`

`object`

Service-specific metadata associated with the operation. It typically contains progress information and common metadata such as create time. Some services might not provide such metadata. Any method that returns a long-running operation should document the metadata type, if any.

An object containing fields of an arbitrary type. An additional field `"@type"` contains a URI identifying the type. Example: `{ "id": 1234, "@type": "types.example.com/standard/id" }` .

`done`

`boolean`

If the value is `false` , it means the operation is still in progress. If `true` , the operation is completed, and either `error` or `response` is available.

Union field `result` . The operation result, which can be either an `error` or a valid `response` . If `done` == `false` , neither `error` nor `response` is set. If `done` == `true` , exactly one of `error` or `response` can be set. Some services might not provide the result. `result` can be only one of the following:

`error`

` object ( Status  ` )

The error result of the operation in case of failure or cancellation.

`response`

`object`

The normal, successful response of the operation. If the original method returns no data on success, such as `Delete` , the response is `google.protobuf.Empty` . If the original method is standard `Get` / `Create` / `Update` , the response should be the resource. For other methods, the response should have the type `XxxResponse` , where `Xxx` is the original method name. For example, if the original method name is `TakeSnapshot()` , the inferred response type is `TakeSnapshotResponse` .

An object containing fields of an arbitrary type. An additional field `"@type"` contains a URI identifying the type. Example: `{ "id": 1234, "@type": "types.example.com/standard/id" }` .

### Any

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
  &quot;typeUrl&quot;: string,
  &quot;value&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`typeUrl`

`string`

Identifies the type of the serialized Protobuf message with a URI reference consisting of a prefix ending in a slash and the fully-qualified type name.

Example: type.googleapis.com/google.protobuf.StringValue

This string must contain at least one `/` character, and the content after the last `/` must be the fully-qualified name of the type in canonical form, without a leading dot. Do not write a scheme on these URI references so that clients do not attempt to contact them.

The prefix is arbitrary and Protobuf implementations are expected to simply strip off everything up to and including the last `/` to identify the type. `type.googleapis.com/` is a common default prefix that some legacy implementations require. This prefix does not indicate the origin of the type, and URIs containing it are not expected to respond to any requests.

All type URL strings must be legal URI references with the additional restriction (for the text format) that the content of the reference must consist only of alphanumeric characters, percent-encoded escapes, and characters in the following set (not including the outer backticks): `/-.~_!$&()*+,;=` . Despite our allowing percent encodings, implementations should not unescape them to prevent confusion with existing parsers. For example, `type.googleapis.com%2FFoo` should be rejected.

In the original design of `Any` , the possibility of launching a type resolution service at these type URLs was considered but Protobuf never implemented one and considers contacting these URLs to be problematic and a potential security issue. Do not attempt to contact type URLs.

`value`

`string ( bytes format)`

Holds a Protobuf serialization of the type described by type\_url.

A base64-encoded string.

### Status

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
  &quot;code&quot;: integer,
  &quot;message&quot;: string,
  &quot;details&quot;: [
    {
      &quot;@type&quot;: string,
      field1: ...,
      ...
    }
  ]
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`code`

`integer`

The status code, which should be an enum value of `google.rpc.Code` .

`message`

`string`

A developer-facing error message, which should be in English. Any user-facing error message should be localized and sent in the `google.rpc.Status.details` field, or localized by the client.

`details[]`

`object`

A list of messages that carry the error details. There is a common set of message types for APIs to use.

An object containing fields of an arbitrary type. An additional field `"@type"` contains a URI identifying the type. Example: `{ "id": 1234, "@type": "types.example.com/standard/id" }` .

### Tool Annotations

Destructive Hint: ❌ | Idempotent Hint: ❌ | Read Only Hint: ❌ | Open World Hint: ❌
