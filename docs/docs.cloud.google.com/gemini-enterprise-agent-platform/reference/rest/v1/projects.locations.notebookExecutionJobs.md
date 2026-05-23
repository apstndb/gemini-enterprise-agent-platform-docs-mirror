---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.notebookExecutionJobs
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.notebookExecutionJobs
title: 'REST Resource: projects.locations.notebookExecutionJobs'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

## Resource: NotebookExecutionJob

NotebookExecutionJob represents an instance of a notebook execution.

Fields

`name` `string`

Output only. The resource name of this NotebookExecutionJob. Format: `projects/{projectId}/locations/{location}/notebookExecutionJobs/{job_id}`

`displayName` `string`

The display name of the NotebookExecutionJob. The name can be up to 128 characters long and can consist of any UTF-8 characters.

`executionTimeout` ` string ( Duration  ` format)

Max running time of the execution job in seconds (default 86400s / 24 hrs).

A duration in seconds with up to nine fractional digits, ending with ' `s` '. Example: `"3.5s"` .

`scheduleResourceName` `string`

The Schedule resource name if this job is triggered by one. Format: `projects/{projectId}/locations/{location}/schedules/{schedule_id}`

`jobState` ` enum ( JobState  ` )

Output only. The state of the NotebookExecutionJob.

`status` ` object ( Status  ` )

Output only. Populated when the NotebookExecutionJob is completed. When there is an error during notebook execution, the error details are populated.

`createTime` ` string ( Timestamp  ` format)

Output only. timestamp when this NotebookExecutionJob was created.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`updateTime` ` string ( Timestamp  ` format)

Output only. timestamp when this NotebookExecutionJob was most recently updated.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`labels` `map (key: string, value: string)`

The labels with user-defined metadata to organize NotebookExecutionJobs.

label keys and values can be no longer than 64 characters (Unicode codepoints), can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed.

See <https://goo.gl/xmQnxf> for more information and examples of labels. System reserved label keys are prefixed with "aiplatform.googleapis.com/" and are immutable.

`kernelName` `string`

The name of the kernel to use during notebook execution. If unset, the default kernel is used.

`encryptionSpec` ` object ( EncryptionSpec  ` )

Customer-managed encryption key spec for the notebook execution job. This field is auto-populated if the `  NotebookRuntimeTemplate  ` has an encryption spec.

`notebook_source` `Union type`

The input notebook. `notebook_source` can be only one of the following:

`dataformRepositorySource` ` object ( DataformRepositorySource  ` )

The Dataform Repository pointing to a single file notebook repository.

`gcsNotebookSource` ` object ( GcsNotebookSource  ` )

The Cloud Storage url pointing to the ipynb file. Format: `gs://bucket/notebookFile.ipynb`

`directNotebookSource` ` object ( DirectNotebookSource  ` )

The contents of an input notebook file.

`environment_spec` `Union type`

The compute config to use for an execution job. `environment_spec` can be only one of the following:

`notebookRuntimeTemplateResourceName` `string`

The NotebookRuntimeTemplate to source compute configuration from.

`customEnvironmentSpec` ` object ( CustomEnvironmentSpec  ` )

The custom compute configuration for an execution job.

`execution_sink` `Union type`

The location to store the notebook execution result. `execution_sink` can be only one of the following:

`gcsOutputUri` `string`

The Cloud Storage location to upload the result to. Format: `gs://bucket-name`

`execution_identity` `Union type`

The identity to run the execution as. `execution_identity` can be only one of the following:

`executionUser` `string`

The user email to run the execution as. Only supported by Colab runtimes.

`serviceAccount` `string`

The service account to run the execution as.

`runtime_environment` `Union type`

Runtime environment for the notebook execution job. If unspecified, the default runtime of Colab is used. `runtime_environment` can be only one of the following:

`workbenchRuntime` ` object ( WorkbenchRuntime  ` )

The Workbench runtime configuration to use for the notebook execution.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;name&quot;: string,&quot;displayName&quot;: string,&quot;executionTimeout&quot;: string,&quot;scheduleResourceName&quot;: string,&quot;jobState&quot;: enum (JobState),&quot;status&quot;: {object (Status)},&quot;createTime&quot;: string,&quot;updateTime&quot;: string,&quot;labels&quot;: {string: string,...},&quot;kernelName&quot;: string,&quot;encryptionSpec&quot;: {object (EncryptionSpec)},// notebook_source&quot;dataformRepositorySource&quot;: {object (DataformRepositorySource)},&quot;gcsNotebookSource&quot;: {object (GcsNotebookSource)},&quot;directNotebookSource&quot;: {object (DirectNotebookSource)}// Union type// environment_spec&quot;notebookRuntimeTemplateResourceName&quot;: string,&quot;customEnvironmentSpec&quot;: {object (CustomEnvironmentSpec)}// Union type// execution_sink&quot;gcsOutputUri&quot;: string// Union type// execution_identity&quot;executionUser&quot;: string,&quot;serviceAccount&quot;: string// Union type// runtime_environment&quot;workbenchRuntime&quot;: {object (WorkbenchRuntime)}// Union type}</code></pre></td>
</tr>
</tbody>
</table>

### DataformRepositorySource

The Dataform Repository containing the input notebook.

Fields

`dataformRepositoryResourceName` `string`

The resource name of the Dataform Repository. Format: `projects/{projectId}/locations/{location}/repositories/{repository_id}`

`commitSha` `string`

The commit SHA to read repository with. If unset, the file will be read at HEAD.

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

### GcsNotebookSource

The Cloud Storage uri for the input notebook.

Fields

`uri` `string`

The Cloud Storage uri pointing to the ipynb file. Format: `gs://bucket/notebookFile.ipynb`

`generation` `string`

The version of the Cloud Storage object to read. If unset, the current version of the object is read. See <https://cloud.google.com/storage/docs/metadata#generation-number> .

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

### DirectNotebookSource

The content of the input notebook in ipynb format.

Fields

`content` `string ( bytes format)`

The base64-encoded contents of the input notebook file.

A base64-encoded string.

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

### CustomEnvironmentSpec

Compute configuration to use for an execution job.

Fields

`machineSpec` ` object ( MachineSpec  ` )

The specification of a single machine for the execution job.

`persistentDiskSpec` ` object ( PersistentDiskSpec  ` )

The specification of a persistent disk to attach for the execution job.

`networkSpec` ` object ( NetworkSpec  ` )

The network configuration to use for the execution job.

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

### WorkbenchRuntime

This type has no fields.

Configuration for a Workbench Instances-based environment.

## Methods

### `            create           `

Creates a NotebookExecutionJob.

### `            delete           `

Deletes a NotebookExecutionJob.

### `            get           `

Gets a NotebookExecutionJob.

### `            list           `

Lists NotebookExecutionJobs in a Location.
