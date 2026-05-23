---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/notebook_execution_get_job
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/notebook_execution_get_job
title: 'MCP Tools Reference: aiplatform.googleapis.com'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

## Tool: `notebook_execution_get_job`

Describes a Colab Enterprise notebook execution job. Use this to retrieve details and status for a specific execution. Format: 'projects/{project\_id}/locations/{region}/notebookExecutionJobs/{notebook\_execution\_job\_id}'. CRITICAL: For {region}, use the region specified in the current context. If no region is specified, prompt the user for one. Do not use 'global'.

The following sample demonstrate how to use `curl` to invoke the `notebook_execution_get_job` MCP tool.

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
    &quot;name&quot;: &quot;notebook_execution_get_job&quot;,
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

Request message for \[NotebookService.GetNotebookExecutionJob\]

### GetNotebookExecutionJobRequest

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;name&quot;: string,&quot;view&quot;: enum (NotebookExecutionJobView)}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`name`

`string`

Required. The name of the NotebookExecutionJob resource.

`view`

`enum ( NotebookExecutionJobView` )

Optional. The NotebookExecutionJob view. Defaults to BASIC.

## Output Schema

NotebookExecutionJob represents an instance of a notebook execution.

### NotebookExecutionJob

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;name&quot;: string,&quot;displayName&quot;: string,&quot;executionTimeout&quot;: string,&quot;scheduleResourceName&quot;: string,&quot;jobState&quot;: enum (JobState),&quot;status&quot;: {object (Status)},&quot;createTime&quot;: string,&quot;updateTime&quot;: string,&quot;labels&quot;: {string: string,...},&quot;kernelName&quot;: string,&quot;encryptionSpec&quot;: {object (EncryptionSpec)},// Union field notebook_source can be only one of the following:&quot;dataformRepositorySource&quot;: {object (DataformRepositorySource)},&quot;gcsNotebookSource&quot;: {object (GcsNotebookSource)},&quot;directNotebookSource&quot;: {object (DirectNotebookSource)}// End of list of possible types for union field notebook_source.// Union field environment_spec can be only one of the following:&quot;notebookRuntimeTemplateResourceName&quot;: string,&quot;customEnvironmentSpec&quot;: {object (CustomEnvironmentSpec)}// End of list of possible types for union field environment_spec.// Union field execution_sink can be only one of the following:&quot;gcsOutputUri&quot;: string// End of list of possible types for union field execution_sink.// Union field execution_identity can be only one of the following:&quot;executionUser&quot;: string,&quot;serviceAccount&quot;: string// End of list of possible types for union field execution_identity.// Union field runtime_environment can be only one of the following:&quot;workbenchRuntime&quot;: {object (WorkbenchRuntime)}// End of list of possible types for union field runtime_environment.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`name`

`string`

Output only. The resource name of this NotebookExecutionJob. Format: `projects/{project_id}/locations/{location}/notebookExecutionJobs/{job_id}`

`displayName`

`string`

The display name of the NotebookExecutionJob. The name can be up to 128 characters long and can consist of any UTF-8 characters.

`executionTimeout`

` string ( Duration  ` format)

Max running time of the execution job in seconds (default 86400s / 24 hrs).

A duration in seconds with up to nine fractional digits, ending with ' `s` '. Example: `"3.5s"` .

`scheduleResourceName`

`string`

The Schedule resource name if this job is triggered by one. Format: `projects/{project_id}/locations/{location}/schedules/{schedule_id}`

`jobState`

`enum ( JobState` )

Output only. The state of the NotebookExecutionJob.

`status`

` object ( Status  ` )

Output only. Populated when the NotebookExecutionJob is completed. When there is an error during notebook execution, the error details are populated.

`createTime`

` string ( Timestamp  ` format)

Output only. Timestamp when this NotebookExecutionJob was created.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`updateTime`

` string ( Timestamp  ` format)

Output only. Timestamp when this NotebookExecutionJob was most recently updated.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`labels`

`map (key: string, value: string)`

The labels with user-defined metadata to organize NotebookExecutionJobs.

Label keys and values can be no longer than 64 characters (Unicode codepoints), can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed.

See <https://goo.gl/xmQnxf> for more information and examples of labels. System reserved label keys are prefixed with "aiplatform.googleapis.com/" and are immutable.

An object containing a list of `"key": value` pairs. Example: `{ "name": "wrench", "mass": "1.3kg", "count": "3" }` .

`kernelName`

`string`

The name of the kernel to use during notebook execution. If unset, the default kernel is used.

`encryptionSpec`

` object ( EncryptionSpec  ` )

Customer-managed encryption key spec for the notebook execution job. This field is auto-populated if the `  NotebookRuntimeTemplate  ` has an encryption spec.

Union field `notebook_source` . The input notebook. `notebook_source` can be only one of the following:

`dataformRepositorySource`

` object ( DataformRepositorySource  ` )

The Dataform Repository pointing to a single file notebook repository.

`gcsNotebookSource`

` object ( GcsNotebookSource  ` )

The Cloud Storage url pointing to the ipynb file. Format: `gs://bucket/notebook_file.ipynb`

`directNotebookSource`

` object ( DirectNotebookSource  ` )

The contents of an input notebook file.

Union field `environment_spec` . The compute config to use for an execution job. `environment_spec` can be only one of the following:

`notebookRuntimeTemplateResourceName`

`string`

The NotebookRuntimeTemplate to source compute configuration from.

`customEnvironmentSpec`

` object ( CustomEnvironmentSpec  ` )

The custom compute configuration for an execution job.

Union field `execution_sink` . The location to store the notebook execution result. `execution_sink` can be only one of the following:

`gcsOutputUri`

`string`

The Cloud Storage location to upload the result to. Format: `gs://bucket-name`

Union field `execution_identity` . The identity to run the execution as. `execution_identity` can be only one of the following:

`executionUser`

`string`

The user email to run the execution as. Only supported by Colab runtimes.

`serviceAccount`

`string`

The service account to run the execution as.

Union field `runtime_environment` . Runtime environment for the notebook execution job. If unspecified, the default runtime of Colab is used. `runtime_environment` can be only one of the following:

`workbenchRuntime`

`object ( WorkbenchRuntime` )

The Workbench runtime configuration to use for the notebook execution.

### DataformRepositorySource

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
  &quot;dataformRepositoryResourceName&quot;: string,
  &quot;commitSha&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`dataformRepositoryResourceName`

`string`

The resource name of the Dataform Repository. Format: `projects/{project_id}/locations/{location}/repositories/{repository_id}`

`commitSha`

`string`

The commit SHA to read repository with. If unset, the file will be read at HEAD.

### GcsNotebookSource

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
  &quot;uri&quot;: string,
  &quot;generation&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`uri`

`string`

The Cloud Storage uri pointing to the ipynb file. Format: `gs://bucket/notebook_file.ipynb`

`generation`

`string`

The version of the Cloud Storage object to read. If unset, the current version of the object is read. See <https://cloud.google.com/storage/docs/metadata#generation-number> .

### DirectNotebookSource

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
  &quot;content&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`content`

`string ( bytes format)`

The base64-encoded contents of the input notebook file.

A base64-encoded string.

### CustomEnvironmentSpec

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;machineSpec&quot;: {object (MachineSpec)},&quot;persistentDiskSpec&quot;: {object (PersistentDiskSpec)},&quot;networkSpec&quot;: {object (NetworkSpec)}}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`machineSpec`

` object ( MachineSpec  ` )

The specification of a single machine for the execution job.

`persistentDiskSpec`

` object ( PersistentDiskSpec  ` )

The specification of a persistent disk to attach for the execution job.

`networkSpec`

` object ( NetworkSpec  ` )

The network configuration to use for the execution job.

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

### Tool Annotations

Destructive Hint: ❌ | Idempotent Hint: ✅ | Read Only Hint: ✅ | Open World Hint: ❌
