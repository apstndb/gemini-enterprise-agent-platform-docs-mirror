---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rpc/google.cloud.notebooks.v1
title: Package google.cloud.notebooks.v1
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

## Index

  - `  ManagedNotebookService  ` (interface)
  - `  NotebookService  ` (interface)
  - `  ContainerImage  ` (message)
  - `  CreateEnvironmentRequest  ` (message)
  - `  CreateExecutionRequest  ` (message)
  - `  CreateInstanceRequest  ` (message)
  - `  CreateRuntimeRequest  ` (message)
  - `  CreateScheduleRequest  ` (message)
  - `  DeleteEnvironmentRequest  ` (message)
  - `  DeleteExecutionRequest  ` (message)
  - `  DeleteInstanceRequest  ` (message)
  - `  DeleteRuntimeRequest  ` (message)
  - `  DeleteScheduleRequest  ` (message)
  - `  DiagnoseInstanceRequest  ` (message)
  - `  DiagnosticConfig  ` (message)
  - `  EncryptionConfig  ` (message)
  - `  Environment  ` (message)
  - `  Event  ` (message)
  - `  Event.EventType  ` (enum)
  - `  Execution  ` (message)
  - `  Execution.State  ` (enum)
  - `  ExecutionTemplate  ` (message)
  - `  ExecutionTemplate.DataprocParameters  ` (message)
  - `  ExecutionTemplate.JobType  ` (enum)
  - `  ExecutionTemplate.ScaleTier  ` (enum)
  - `  ExecutionTemplate.SchedulerAcceleratorConfig  ` (message)
  - `  ExecutionTemplate.SchedulerAcceleratorType  ` (enum)
  - `  ExecutionTemplate.VertexAIParameters  ` (message)
  - `  GetEnvironmentRequest  ` (message)
  - `  GetExecutionRequest  ` (message)
  - `  GetInstanceHealthRequest  ` (message)
  - `  GetInstanceHealthResponse  ` (message)
  - `  GetInstanceHealthResponse.HealthState  ` (enum)
  - `  GetInstanceRequest  ` (message)
  - `  GetRuntimeRequest  ` (message)
  - `  GetScheduleRequest  ` (message)
  - `  Instance  ` (message)
  - `  Instance.AcceleratorConfig  ` (message)
  - `  Instance.AcceleratorType  ` (enum)
  - `  Instance.Disk  ` (message)
  - `  Instance.Disk.GuestOsFeature  ` (message)
  - `  Instance.DiskEncryption  ` (enum)
  - `  Instance.DiskType  ` (enum)
  - `  Instance.NicType  ` (enum)
  - `  Instance.ShieldedInstanceConfig  ` (message)
  - `  Instance.State  ` (enum)
  - `  Instance.UpgradeHistoryEntry  ` (message)
  - `  Instance.UpgradeHistoryEntry.Action  ` (enum)
  - `  Instance.UpgradeHistoryEntry.State  ` (enum)
  - `  InstanceConfig  ` (message)
  - `  InstanceMigrationEligibility  ` (message)
  - `  InstanceMigrationEligibility.Error  ` (enum)
  - `  InstanceMigrationEligibility.Warning  ` (enum)
  - `  IsInstanceUpgradeableRequest  ` (message)
  - `  IsInstanceUpgradeableResponse  ` (message)
  - `  ListEnvironmentsRequest  ` (message)
  - `  ListEnvironmentsResponse  ` (message)
  - `  ListExecutionsRequest  ` (message)
  - `  ListExecutionsResponse  ` (message)
  - `  ListInstancesRequest  ` (message)
  - `  ListInstancesResponse  ` (message)
  - `  ListRuntimesRequest  ` (message)
  - `  ListRuntimesResponse  ` (message)
  - `  ListSchedulesRequest  ` (message)
  - `  ListSchedulesResponse  ` (message)
  - `  LocalDisk  ` (message)
  - `  LocalDisk.RuntimeGuestOsFeature  ` (message)
  - `  LocalDiskInitializeParams  ` (message)
  - `  LocalDiskInitializeParams.DiskType  ` (enum)
  - `  MigrateInstanceRequest  ` (message)
  - `  MigrateInstanceRequest.PostStartupScriptOption  ` (enum)
  - `  MigrateInstanceResponse  ` (message)
  - `  MigrateRuntimeRequest  ` (message)
  - `  MigrateRuntimeRequest.PostStartupScriptOption  ` (enum)
  - `  OperationMetadata  ` (message)
  - `  RegisterInstanceRequest  ` (message)
  - `  ReportInstanceInfoRequest  ` (message)
  - `  ReportRuntimeEventRequest  ` (message)
  - `  ReservationAffinity  ` (message)
  - `  ReservationAffinity.Type  ` (enum)
  - `  ResetInstanceRequest  ` (message)
  - `  ResetRuntimeRequest  ` (message)
  - `  RollbackInstanceRequest  ` (message)
  - `  Runtime  ` (message)
  - `  Runtime.HealthState  ` (enum)
  - `  Runtime.State  ` (enum)
  - `  RuntimeAcceleratorConfig  ` (message)
  - `  RuntimeAcceleratorConfig.AcceleratorType  ` (enum)
  - `  RuntimeAccessConfig  ` (message)
  - `  RuntimeAccessConfig.RuntimeAccessType  ` (enum)
  - `  RuntimeMetrics  ` (message)
  - `  RuntimeMigrationEligibility  ` (message)
  - `  RuntimeMigrationEligibility.Error  ` (enum)
  - `  RuntimeMigrationEligibility.Warning  ` (enum)
  - `  RuntimeShieldedInstanceConfig  ` (message)
  - `  RuntimeSoftwareConfig  ` (message)
  - `  RuntimeSoftwareConfig.PostStartupScriptBehavior  ` (enum)
  - `  Schedule  ` (message)
  - `  Schedule.State  ` (enum)
  - `  SetInstanceAcceleratorRequest  ` (message)
  - `  SetInstanceLabelsRequest  ` (message)
  - `  SetInstanceMachineTypeRequest  ` (message)
  - `  StartInstanceRequest  ` (message)
  - `  StartRuntimeRequest  ` (message)
  - `  StopInstanceRequest  ` (message)
  - `  StopRuntimeRequest  ` (message)
  - `  SwitchRuntimeRequest  ` (message)
  - `  UpdateInstanceConfigRequest  ` (message)
  - `  UpdateInstanceMetadataItemsRequest  ` (message)
  - `  UpdateInstanceMetadataItemsResponse  ` (message)
  - `  UpdateRuntimeRequest  ` (message)
  - `  UpdateShieldedInstanceConfigRequest  ` (message)
  - `  UpgradeInstanceRequest  ` (message)
  - `  UpgradeType  ` (enum)
  - `  VirtualMachine  ` (message)
  - `  VirtualMachineConfig  ` (message)
  - `  VirtualMachineConfig.BootImage  ` (message)
  - `  VirtualMachineConfig.NicType  ` (enum)
  - `  VmImage  ` (message)

## ManagedNotebookService

API v1 service for Managed Notebooks.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>CreateRuntime</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr" translate="no">rpc CreateRuntime(              CreateRuntimeRequest            </code> ) returns ( <code dir="ltr" translate="no">             Operation            </code> )</p>
<p>Creates a new Runtime in a given project and location.</p>
<dl>
<dt>Authorization scopes</dt>
<dd><p>Requires the following OAuth scope:</p>
<ul>
<li><code dir="ltr" translate="no">https://www.googleapis.com/auth/cloud-platform</code></li>
</ul>
<p>For more information, see the <a href="https://docs.cloud.google.com/docs/authentication#authorization-gcp">Authentication Overview</a> .</p>
</dd>
</dl></td>
</tr>
</tbody>
</table>

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>DeleteRuntime</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr" translate="no">rpc DeleteRuntime(              DeleteRuntimeRequest            </code> ) returns ( <code dir="ltr" translate="no">             Operation            </code> )</p>
<p>Deletes a single Runtime.</p>
<dl>
<dt>Authorization scopes</dt>
<dd><p>Requires the following OAuth scope:</p>
<ul>
<li><code dir="ltr" translate="no">https://www.googleapis.com/auth/cloud-platform</code></li>
</ul>
<p>For more information, see the <a href="https://docs.cloud.google.com/docs/authentication#authorization-gcp">Authentication Overview</a> .</p>
</dd>
</dl></td>
</tr>
</tbody>
</table>

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>GetRuntime</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr" translate="no">rpc GetRuntime(              GetRuntimeRequest            </code> ) returns ( <code dir="ltr" translate="no">             Runtime            </code> )</p>
<p>Gets details of a single Runtime. The location must be a regional endpoint rather than zonal.</p>
<dl>
<dt>Authorization scopes</dt>
<dd><p>Requires the following OAuth scope:</p>
<ul>
<li><code dir="ltr" translate="no">https://www.googleapis.com/auth/cloud-platform</code></li>
</ul>
<p>For more information, see the <a href="https://docs.cloud.google.com/docs/authentication#authorization-gcp">Authentication Overview</a> .</p>
</dd>
</dl></td>
</tr>
</tbody>
</table>

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>ListRuntimes</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr" translate="no">rpc ListRuntimes(              ListRuntimesRequest            </code> ) returns ( <code dir="ltr" translate="no">             ListRuntimesResponse            </code> )</p>
<p>Lists Runtimes in a given project and location.</p>
<dl>
<dt>Authorization scopes</dt>
<dd><p>Requires the following OAuth scope:</p>
<ul>
<li><code dir="ltr" translate="no">https://www.googleapis.com/auth/cloud-platform</code></li>
</ul>
<p>For more information, see the <a href="https://docs.cloud.google.com/docs/authentication#authorization-gcp">Authentication Overview</a> .</p>
</dd>
</dl></td>
</tr>
</tbody>
</table>

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>MigrateRuntime</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr" translate="no">rpc MigrateRuntime(              MigrateRuntimeRequest            </code> ) returns ( <code dir="ltr" translate="no">             Operation            </code> )</p>
<p>Migrate an existing Runtime to a new Workbench Instance.</p>
<dl>
<dt>Authorization scopes</dt>
<dd><p>Requires the following OAuth scope:</p>
<ul>
<li><code dir="ltr" translate="no">https://www.googleapis.com/auth/cloud-platform</code></li>
</ul>
<p>For more information, see the <a href="https://docs.cloud.google.com/docs/authentication#authorization-gcp">Authentication Overview</a> .</p>
</dd>
</dl></td>
</tr>
</tbody>
</table>

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>ReportRuntimeEvent</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr" translate="no">rpc ReportRuntimeEvent(              ReportRuntimeEventRequest            </code> ) returns ( <code dir="ltr" translate="no">             Operation            </code> )</p>
<p>Reports and processes a runtime event.</p>
<dl>
<dt>Authorization scopes</dt>
<dd><p>Requires the following OAuth scope:</p>
<ul>
<li><code dir="ltr" translate="no">https://www.googleapis.com/auth/cloud-platform</code></li>
</ul>
<p>For more information, see the <a href="https://docs.cloud.google.com/docs/authentication#authorization-gcp">Authentication Overview</a> .</p>
</dd>
</dl></td>
</tr>
</tbody>
</table>

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>ResetRuntime</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr" translate="no">rpc ResetRuntime(              ResetRuntimeRequest            </code> ) returns ( <code dir="ltr" translate="no">             Operation            </code> )</p>
<p>Resets a Managed Notebook Runtime.</p>
<dl>
<dt>Authorization scopes</dt>
<dd><p>Requires the following OAuth scope:</p>
<ul>
<li><code dir="ltr" translate="no">https://www.googleapis.com/auth/cloud-platform</code></li>
</ul>
<p>For more information, see the <a href="https://docs.cloud.google.com/docs/authentication#authorization-gcp">Authentication Overview</a> .</p>
</dd>
</dl></td>
</tr>
</tbody>
</table>

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>StartRuntime</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr" translate="no">rpc StartRuntime(              StartRuntimeRequest            </code> ) returns ( <code dir="ltr" translate="no">             Operation            </code> )</p>
<p>Starts a Managed Notebook Runtime. Perform "Start" on GPU instances; "Resume" on CPU instances See: <a href="https://cloud.google.com/compute/docs/instances/stop-start-instance">https://cloud.google.com/compute/docs/instances/stop-start-instance</a> <a href="https://cloud.google.com/compute/docs/instances/suspend-resume-instance">https://cloud.google.com/compute/docs/instances/suspend-resume-instance</a></p>
<dl>
<dt>Authorization scopes</dt>
<dd><p>Requires the following OAuth scope:</p>
<ul>
<li><code dir="ltr" translate="no">https://www.googleapis.com/auth/cloud-platform</code></li>
</ul>
<p>For more information, see the <a href="https://docs.cloud.google.com/docs/authentication#authorization-gcp">Authentication Overview</a> .</p>
</dd>
</dl></td>
</tr>
</tbody>
</table>

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>StopRuntime</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr" translate="no">rpc StopRuntime(              StopRuntimeRequest            </code> ) returns ( <code dir="ltr" translate="no">             Operation            </code> )</p>
<p>Stops a Managed Notebook Runtime. Perform "Stop" on GPU instances; "Suspend" on CPU instances See: <a href="https://cloud.google.com/compute/docs/instances/stop-start-instance">https://cloud.google.com/compute/docs/instances/stop-start-instance</a> <a href="https://cloud.google.com/compute/docs/instances/suspend-resume-instance">https://cloud.google.com/compute/docs/instances/suspend-resume-instance</a></p>
<dl>
<dt>Authorization scopes</dt>
<dd><p>Requires the following OAuth scope:</p>
<ul>
<li><code dir="ltr" translate="no">https://www.googleapis.com/auth/cloud-platform</code></li>
</ul>
<p>For more information, see the <a href="https://docs.cloud.google.com/docs/authentication#authorization-gcp">Authentication Overview</a> .</p>
</dd>
</dl></td>
</tr>
</tbody>
</table>

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>SwitchRuntime</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr" translate="no">rpc SwitchRuntime(              SwitchRuntimeRequest            </code> ) returns ( <code dir="ltr" translate="no">             Operation            </code> )</p>
<p>Switch a Managed Notebook Runtime.</p>
<dl>
<dt>Authorization scopes</dt>
<dd><p>Requires the following OAuth scope:</p>
<ul>
<li><code dir="ltr" translate="no">https://www.googleapis.com/auth/cloud-platform</code></li>
</ul>
<p>For more information, see the <a href="https://docs.cloud.google.com/docs/authentication#authorization-gcp">Authentication Overview</a> .</p>
</dd>
</dl></td>
</tr>
</tbody>
</table>

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>UpdateRuntime</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr" translate="no">rpc UpdateRuntime(              UpdateRuntimeRequest            </code> ) returns ( <code dir="ltr" translate="no">             Operation            </code> )</p>
<p>Update Notebook Runtime configuration.</p>
<dl>
<dt>Authorization scopes</dt>
<dd><p>Requires the following OAuth scope:</p>
<ul>
<li><code dir="ltr" translate="no">https://www.googleapis.com/auth/cloud-platform</code></li>
</ul>
<p>For more information, see the <a href="https://docs.cloud.google.com/docs/authentication#authorization-gcp">Authentication Overview</a> .</p>
</dd>
</dl></td>
</tr>
</tbody>
</table>

## NotebookService

API v1 service for Cloud AI Platform Notebooks.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>CreateEnvironment</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr" translate="no">rpc CreateEnvironment(              CreateEnvironmentRequest            </code> ) returns ( <code dir="ltr" translate="no">             Operation            </code> )</p>
<p>Creates a new Environment.</p>
<dl>
<dt>Authorization scopes</dt>
<dd><p>Requires the following OAuth scope:</p>
<ul>
<li><code dir="ltr" translate="no">https://www.googleapis.com/auth/cloud-platform</code></li>
</ul>
<p>For more information, see the <a href="https://docs.cloud.google.com/docs/authentication#authorization-gcp">Authentication Overview</a> .</p>
</dd>
</dl></td>
</tr>
</tbody>
</table>

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>CreateExecution</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr" translate="no">rpc CreateExecution(              CreateExecutionRequest            </code> ) returns ( <code dir="ltr" translate="no">             Operation            </code> )</p>
<p>Creates a new Execution in a given project and location.</p>
<dl>
<dt>Authorization scopes</dt>
<dd><p>Requires the following OAuth scope:</p>
<ul>
<li><code dir="ltr" translate="no">https://www.googleapis.com/auth/cloud-platform</code></li>
</ul>
<p>For more information, see the <a href="https://docs.cloud.google.com/docs/authentication#authorization-gcp">Authentication Overview</a> .</p>
</dd>
</dl></td>
</tr>
</tbody>
</table>

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>CreateInstance</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr" translate="no">rpc CreateInstance(              CreateInstanceRequest            </code> ) returns ( <code dir="ltr" translate="no">             Operation            </code> )</p>
<p>Creates a new Instance in a given project and location.</p>
<dl>
<dt>Authorization scopes</dt>
<dd><p>Requires the following OAuth scope:</p>
<ul>
<li><code dir="ltr" translate="no">https://www.googleapis.com/auth/cloud-platform</code></li>
</ul>
<p>For more information, see the <a href="https://docs.cloud.google.com/docs/authentication#authorization-gcp">Authentication Overview</a> .</p>
</dd>
</dl></td>
</tr>
</tbody>
</table>

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>CreateSchedule</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr" translate="no">rpc CreateSchedule(              CreateScheduleRequest            </code> ) returns ( <code dir="ltr" translate="no">             Operation            </code> )</p>
<p>Creates a new Scheduled Notebook in a given project and location.</p>
<dl>
<dt>Authorization scopes</dt>
<dd><p>Requires the following OAuth scope:</p>
<ul>
<li><code dir="ltr" translate="no">https://www.googleapis.com/auth/cloud-platform</code></li>
</ul>
<p>For more information, see the <a href="https://docs.cloud.google.com/docs/authentication#authorization-gcp">Authentication Overview</a> .</p>
</dd>
</dl></td>
</tr>
</tbody>
</table>

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>DeleteEnvironment</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr" translate="no">rpc DeleteEnvironment(              DeleteEnvironmentRequest            </code> ) returns ( <code dir="ltr" translate="no">             Operation            </code> )</p>
<p>Deletes a single Environment.</p>
<dl>
<dt>Authorization scopes</dt>
<dd><p>Requires the following OAuth scope:</p>
<ul>
<li><code dir="ltr" translate="no">https://www.googleapis.com/auth/cloud-platform</code></li>
</ul>
<p>For more information, see the <a href="https://docs.cloud.google.com/docs/authentication#authorization-gcp">Authentication Overview</a> .</p>
</dd>
</dl></td>
</tr>
</tbody>
</table>

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>DeleteExecution</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr" translate="no">rpc DeleteExecution(              DeleteExecutionRequest            </code> ) returns ( <code dir="ltr" translate="no">             Operation            </code> )</p>
<p>Deletes execution</p>
<dl>
<dt>Authorization scopes</dt>
<dd><p>Requires the following OAuth scope:</p>
<ul>
<li><code dir="ltr" translate="no">https://www.googleapis.com/auth/cloud-platform</code></li>
</ul>
<p>For more information, see the <a href="https://docs.cloud.google.com/docs/authentication#authorization-gcp">Authentication Overview</a> .</p>
</dd>
</dl></td>
</tr>
</tbody>
</table>

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>DeleteInstance</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr" translate="no">rpc DeleteInstance(              DeleteInstanceRequest            </code> ) returns ( <code dir="ltr" translate="no">             Operation            </code> )</p>
<p>Deletes a single Instance.</p>
<dl>
<dt>Authorization scopes</dt>
<dd><p>Requires the following OAuth scope:</p>
<ul>
<li><code dir="ltr" translate="no">https://www.googleapis.com/auth/cloud-platform</code></li>
</ul>
<p>For more information, see the <a href="https://docs.cloud.google.com/docs/authentication#authorization-gcp">Authentication Overview</a> .</p>
</dd>
</dl></td>
</tr>
</tbody>
</table>

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>DeleteSchedule</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr" translate="no">rpc DeleteSchedule(              DeleteScheduleRequest            </code> ) returns ( <code dir="ltr" translate="no">             Operation            </code> )</p>
<p>Deletes schedule and all underlying jobs</p>
<dl>
<dt>Authorization scopes</dt>
<dd><p>Requires the following OAuth scope:</p>
<ul>
<li><code dir="ltr" translate="no">https://www.googleapis.com/auth/cloud-platform</code></li>
</ul>
<p>For more information, see the <a href="https://docs.cloud.google.com/docs/authentication#authorization-gcp">Authentication Overview</a> .</p>
</dd>
</dl></td>
</tr>
</tbody>
</table>

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>DiagnoseInstance</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr" translate="no">rpc DiagnoseInstance(              DiagnoseInstanceRequest            </code> ) returns ( <code dir="ltr" translate="no">             Operation            </code> )</p>
<p>Creates a Diagnostic File and runs Diagnostic Tool given an Instance.</p>
<dl>
<dt>Authorization scopes</dt>
<dd><p>Requires the following OAuth scope:</p>
<ul>
<li><code dir="ltr" translate="no">https://www.googleapis.com/auth/cloud-platform</code></li>
</ul>
<p>For more information, see the <a href="https://docs.cloud.google.com/docs/authentication#authorization-gcp">Authentication Overview</a> .</p>
</dd>
</dl></td>
</tr>
</tbody>
</table>

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>GetEnvironment</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr" translate="no">rpc GetEnvironment(              GetEnvironmentRequest            </code> ) returns ( <code dir="ltr" translate="no">             Environment            </code> )</p>
<p>Gets details of a single Environment.</p>
<dl>
<dt>Authorization scopes</dt>
<dd><p>Requires the following OAuth scope:</p>
<ul>
<li><code dir="ltr" translate="no">https://www.googleapis.com/auth/cloud-platform</code></li>
</ul>
<p>For more information, see the <a href="https://docs.cloud.google.com/docs/authentication#authorization-gcp">Authentication Overview</a> .</p>
</dd>
</dl></td>
</tr>
</tbody>
</table>

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>GetExecution</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr" translate="no">rpc GetExecution(              GetExecutionRequest            </code> ) returns ( <code dir="ltr" translate="no">             Execution            </code> )</p>
<p>Gets details of executions</p>
<dl>
<dt>Authorization scopes</dt>
<dd><p>Requires the following OAuth scope:</p>
<ul>
<li><code dir="ltr" translate="no">https://www.googleapis.com/auth/cloud-platform</code></li>
</ul>
<p>For more information, see the <a href="https://docs.cloud.google.com/docs/authentication#authorization-gcp">Authentication Overview</a> .</p>
</dd>
</dl></td>
</tr>
</tbody>
</table>

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>GetInstance</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr" translate="no">rpc GetInstance(              GetInstanceRequest            </code> ) returns ( <code dir="ltr" translate="no">             Instance            </code> )</p>
<p>Gets details of a single Instance.</p>
<dl>
<dt>Authorization scopes</dt>
<dd><p>Requires the following OAuth scope:</p>
<ul>
<li><code dir="ltr" translate="no">https://www.googleapis.com/auth/cloud-platform</code></li>
</ul>
<p>For more information, see the <a href="https://docs.cloud.google.com/docs/authentication#authorization-gcp">Authentication Overview</a> .</p>
</dd>
</dl></td>
</tr>
</tbody>
</table>

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>GetInstanceHealth</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr" translate="no">rpc GetInstanceHealth(              GetInstanceHealthRequest            </code> ) returns ( <code dir="ltr" translate="no">             GetInstanceHealthResponse            </code> )</p>
<p>Checks whether a notebook instance is healthy.</p>
<dl>
<dt>Authorization scopes</dt>
<dd><p>Requires the following OAuth scope:</p>
<ul>
<li><code dir="ltr" translate="no">https://www.googleapis.com/auth/cloud-platform</code></li>
</ul>
<p>For more information, see the <a href="https://docs.cloud.google.com/docs/authentication#authorization-gcp">Authentication Overview</a> .</p>
</dd>
</dl></td>
</tr>
</tbody>
</table>

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>GetSchedule</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr" translate="no">rpc GetSchedule(              GetScheduleRequest            </code> ) returns ( <code dir="ltr" translate="no">             Schedule            </code> )</p>
<p>Gets details of schedule</p>
<dl>
<dt>Authorization scopes</dt>
<dd><p>Requires the following OAuth scope:</p>
<ul>
<li><code dir="ltr" translate="no">https://www.googleapis.com/auth/cloud-platform</code></li>
</ul>
<p>For more information, see the <a href="https://docs.cloud.google.com/docs/authentication#authorization-gcp">Authentication Overview</a> .</p>
</dd>
</dl></td>
</tr>
</tbody>
</table>

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>IsInstanceUpgradeable</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr" translate="no">rpc IsInstanceUpgradeable(              IsInstanceUpgradeableRequest            </code> ) returns ( <code dir="ltr" translate="no">             IsInstanceUpgradeableResponse            </code> )</p>
<p>Checks whether a notebook instance is upgradable.</p>
<dl>
<dt>Authorization scopes</dt>
<dd><p>Requires the following OAuth scope:</p>
<ul>
<li><code dir="ltr" translate="no">https://www.googleapis.com/auth/cloud-platform</code></li>
</ul>
<p>For more information, see the <a href="https://docs.cloud.google.com/docs/authentication#authorization-gcp">Authentication Overview</a> .</p>
</dd>
</dl></td>
</tr>
</tbody>
</table>

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>ListEnvironments</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr" translate="no">rpc ListEnvironments(              ListEnvironmentsRequest            </code> ) returns ( <code dir="ltr" translate="no">             ListEnvironmentsResponse            </code> )</p>
<p>Lists environments in a project.</p>
<dl>
<dt>Authorization scopes</dt>
<dd><p>Requires the following OAuth scope:</p>
<ul>
<li><code dir="ltr" translate="no">https://www.googleapis.com/auth/cloud-platform</code></li>
</ul>
<p>For more information, see the <a href="https://docs.cloud.google.com/docs/authentication#authorization-gcp">Authentication Overview</a> .</p>
</dd>
</dl></td>
</tr>
</tbody>
</table>

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>ListExecutions</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr" translate="no">rpc ListExecutions(              ListExecutionsRequest            </code> ) returns ( <code dir="ltr" translate="no">             ListExecutionsResponse            </code> )</p>
<p>Lists executions in a given project and location</p>
<dl>
<dt>Authorization scopes</dt>
<dd><p>Requires the following OAuth scope:</p>
<ul>
<li><code dir="ltr" translate="no">https://www.googleapis.com/auth/cloud-platform</code></li>
</ul>
<p>For more information, see the <a href="https://docs.cloud.google.com/docs/authentication#authorization-gcp">Authentication Overview</a> .</p>
</dd>
</dl></td>
</tr>
</tbody>
</table>

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>ListInstances</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr" translate="no">rpc ListInstances(              ListInstancesRequest            </code> ) returns ( <code dir="ltr" translate="no">             ListInstancesResponse            </code> )</p>
<p>Lists instances in a given project and location.</p>
<dl>
<dt>Authorization scopes</dt>
<dd><p>Requires the following OAuth scope:</p>
<ul>
<li><code dir="ltr" translate="no">https://www.googleapis.com/auth/cloud-platform</code></li>
</ul>
<p>For more information, see the <a href="https://docs.cloud.google.com/docs/authentication#authorization-gcp">Authentication Overview</a> .</p>
</dd>
</dl></td>
</tr>
</tbody>
</table>

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>ListSchedules</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr" translate="no">rpc ListSchedules(              ListSchedulesRequest            </code> ) returns ( <code dir="ltr" translate="no">             ListSchedulesResponse            </code> )</p>
<p>Lists schedules in a given project and location.</p>
<dl>
<dt>Authorization scopes</dt>
<dd><p>Requires the following OAuth scope:</p>
<ul>
<li><code dir="ltr" translate="no">https://www.googleapis.com/auth/cloud-platform</code></li>
</ul>
<p>For more information, see the <a href="https://docs.cloud.google.com/docs/authentication#authorization-gcp">Authentication Overview</a> .</p>
</dd>
</dl></td>
</tr>
</tbody>
</table>

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>MigrateInstance</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr" translate="no">rpc MigrateInstance(              MigrateInstanceRequest            </code> ) returns ( <code dir="ltr" translate="no">             Operation            </code> )</p>
<p>Migrates an existing User-Managed Notebook to Workbench Instances.</p>
<dl>
<dt>Authorization scopes</dt>
<dd><p>Requires the following OAuth scope:</p>
<ul>
<li><code dir="ltr" translate="no">https://www.googleapis.com/auth/cloud-platform</code></li>
</ul>
<p>For more information, see the <a href="https://docs.cloud.google.com/docs/authentication#authorization-gcp">Authentication Overview</a> .</p>
</dd>
</dl></td>
</tr>
</tbody>
</table>

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>RegisterInstance</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr" translate="no">rpc RegisterInstance(              RegisterInstanceRequest            </code> ) returns ( <code dir="ltr" translate="no">             Operation            </code> )</p>
<p>Registers an existing legacy notebook instance to the Notebooks API server. Legacy instances are instances created with the legacy Compute Engine calls. They are not manageable by the Notebooks API out of the box. This call makes these instances manageable by the Notebooks API.</p>
<dl>
<dt>Authorization scopes</dt>
<dd><p>Requires the following OAuth scope:</p>
<ul>
<li><code dir="ltr" translate="no">https://www.googleapis.com/auth/cloud-platform</code></li>
</ul>
<p>For more information, see the <a href="https://docs.cloud.google.com/docs/authentication#authorization-gcp">Authentication Overview</a> .</p>
</dd>
</dl></td>
</tr>
</tbody>
</table>

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>ReportInstanceInfo</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr" translate="no">rpc ReportInstanceInfo(              ReportInstanceInfoRequest            </code> ) returns ( <code dir="ltr" translate="no">             Operation            </code> )</p>
<p>Allows notebook instances to report their latest instance information to the Notebooks API server. The server will merge the reported information to the instance metadata store. Do not use this method directly.</p>
<dl>
<dt>Authorization scopes</dt>
<dd><p>Requires the following OAuth scope:</p>
<ul>
<li><code dir="ltr" translate="no">https://www.googleapis.com/auth/cloud-platform</code></li>
</ul>
<p>For more information, see the <a href="https://docs.cloud.google.com/docs/authentication#authorization-gcp">Authentication Overview</a> .</p>
</dd>
</dl></td>
</tr>
</tbody>
</table>

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>ResetInstance</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr" translate="no">rpc ResetInstance(              ResetInstanceRequest            </code> ) returns ( <code dir="ltr" translate="no">             Operation            </code> )</p>
<p>Resets a notebook instance.</p>
<dl>
<dt>Authorization scopes</dt>
<dd><p>Requires the following OAuth scope:</p>
<ul>
<li><code dir="ltr" translate="no">https://www.googleapis.com/auth/cloud-platform</code></li>
</ul>
<p>For more information, see the <a href="https://docs.cloud.google.com/docs/authentication#authorization-gcp">Authentication Overview</a> .</p>
</dd>
</dl></td>
</tr>
</tbody>
</table>

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>RollbackInstance</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr" translate="no">rpc RollbackInstance(              RollbackInstanceRequest            </code> ) returns ( <code dir="ltr" translate="no">             Operation            </code> )</p>
<p>Rollbacks a notebook instance to the previous version.</p>
<dl>
<dt>Authorization scopes</dt>
<dd><p>Requires the following OAuth scope:</p>
<ul>
<li><code dir="ltr" translate="no">https://www.googleapis.com/auth/cloud-platform</code></li>
</ul>
<p>For more information, see the <a href="https://docs.cloud.google.com/docs/authentication#authorization-gcp">Authentication Overview</a> .</p>
</dd>
</dl></td>
</tr>
</tbody>
</table>

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>SetInstanceAccelerator</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr" translate="no">rpc SetInstanceAccelerator(              SetInstanceAcceleratorRequest            </code> ) returns ( <code dir="ltr" translate="no">             Operation            </code> )</p>
<p>Updates the guest accelerators of a single Instance.</p>
<dl>
<dt>Authorization scopes</dt>
<dd><p>Requires the following OAuth scope:</p>
<ul>
<li><code dir="ltr" translate="no">https://www.googleapis.com/auth/cloud-platform</code></li>
</ul>
<p>For more information, see the <a href="https://docs.cloud.google.com/docs/authentication#authorization-gcp">Authentication Overview</a> .</p>
</dd>
</dl></td>
</tr>
</tbody>
</table>

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>SetInstanceLabels</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr" translate="no">rpc SetInstanceLabels(              SetInstanceLabelsRequest            </code> ) returns ( <code dir="ltr" translate="no">             Operation            </code> )</p>
<p>Replaces all the labels of an Instance.</p>
<dl>
<dt>Authorization scopes</dt>
<dd><p>Requires the following OAuth scope:</p>
<ul>
<li><code dir="ltr" translate="no">https://www.googleapis.com/auth/cloud-platform</code></li>
</ul>
<p>For more information, see the <a href="https://docs.cloud.google.com/docs/authentication#authorization-gcp">Authentication Overview</a> .</p>
</dd>
</dl></td>
</tr>
</tbody>
</table>

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>SetInstanceMachineType</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr" translate="no">rpc SetInstanceMachineType(              SetInstanceMachineTypeRequest            </code> ) returns ( <code dir="ltr" translate="no">             Operation            </code> )</p>
<p>Updates the machine type of a single Instance.</p>
<dl>
<dt>Authorization scopes</dt>
<dd><p>Requires the following OAuth scope:</p>
<ul>
<li><code dir="ltr" translate="no">https://www.googleapis.com/auth/cloud-platform</code></li>
</ul>
<p>For more information, see the <a href="https://docs.cloud.google.com/docs/authentication#authorization-gcp">Authentication Overview</a> .</p>
</dd>
</dl></td>
</tr>
</tbody>
</table>

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>StartInstance</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr" translate="no">rpc StartInstance(              StartInstanceRequest            </code> ) returns ( <code dir="ltr" translate="no">             Operation            </code> )</p>
<p>Starts a notebook instance.</p>
<dl>
<dt>Authorization scopes</dt>
<dd><p>Requires the following OAuth scope:</p>
<ul>
<li><code dir="ltr" translate="no">https://www.googleapis.com/auth/cloud-platform</code></li>
</ul>
<p>For more information, see the <a href="https://docs.cloud.google.com/docs/authentication#authorization-gcp">Authentication Overview</a> .</p>
</dd>
</dl></td>
</tr>
</tbody>
</table>

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>StopInstance</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr" translate="no">rpc StopInstance(              StopInstanceRequest            </code> ) returns ( <code dir="ltr" translate="no">             Operation            </code> )</p>
<p>Stops a notebook instance.</p>
<dl>
<dt>Authorization scopes</dt>
<dd><p>Requires the following OAuth scope:</p>
<ul>
<li><code dir="ltr" translate="no">https://www.googleapis.com/auth/cloud-platform</code></li>
</ul>
<p>For more information, see the <a href="https://docs.cloud.google.com/docs/authentication#authorization-gcp">Authentication Overview</a> .</p>
</dd>
</dl></td>
</tr>
</tbody>
</table>

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>UpdateInstanceConfig</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr" translate="no">rpc UpdateInstanceConfig(              UpdateInstanceConfigRequest            </code> ) returns ( <code dir="ltr" translate="no">             Operation            </code> )</p>
<p>Update Notebook Instance configurations.</p>
<dl>
<dt>Authorization scopes</dt>
<dd><p>Requires the following OAuth scope:</p>
<ul>
<li><code dir="ltr" translate="no">https://www.googleapis.com/auth/cloud-platform</code></li>
</ul>
<p>For more information, see the <a href="https://docs.cloud.google.com/docs/authentication#authorization-gcp">Authentication Overview</a> .</p>
</dd>
</dl></td>
</tr>
</tbody>
</table>

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>UpdateInstanceMetadataItems</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr" translate="no">rpc UpdateInstanceMetadataItems(              UpdateInstanceMetadataItemsRequest            </code> ) returns ( <code dir="ltr" translate="no">             UpdateInstanceMetadataItemsResponse            </code> )</p>
<p>Add/update metadata items for an instance.</p>
<dl>
<dt>Authorization scopes</dt>
<dd><p>Requires the following OAuth scope:</p>
<ul>
<li><code dir="ltr" translate="no">https://www.googleapis.com/auth/cloud-platform</code></li>
</ul>
<p>For more information, see the <a href="https://docs.cloud.google.com/docs/authentication#authorization-gcp">Authentication Overview</a> .</p>
</dd>
</dl></td>
</tr>
</tbody>
</table>

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>UpdateShieldedInstanceConfig</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr" translate="no">rpc UpdateShieldedInstanceConfig(              UpdateShieldedInstanceConfigRequest            </code> ) returns ( <code dir="ltr" translate="no">             Operation            </code> )</p>
<p>Updates the Shielded instance configuration of a single Instance.</p>
<dl>
<dt>Authorization scopes</dt>
<dd><p>Requires the following OAuth scope:</p>
<ul>
<li><code dir="ltr" translate="no">https://www.googleapis.com/auth/cloud-platform</code></li>
</ul>
<p>For more information, see the <a href="https://docs.cloud.google.com/docs/authentication#authorization-gcp">Authentication Overview</a> .</p>
</dd>
</dl></td>
</tr>
</tbody>
</table>

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>UpgradeInstance</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr" translate="no">rpc UpgradeInstance(              UpgradeInstanceRequest            </code> ) returns ( <code dir="ltr" translate="no">             Operation            </code> )</p>
<p>Upgrades a notebook instance to the latest version.</p>
<dl>
<dt>Authorization scopes</dt>
<dd><p>Requires the following OAuth scope:</p>
<ul>
<li><code dir="ltr" translate="no">https://www.googleapis.com/auth/cloud-platform</code></li>
</ul>
<p>For more information, see the <a href="https://docs.cloud.google.com/docs/authentication#authorization-gcp">Authentication Overview</a> .</p>
</dd>
</dl></td>
</tr>
</tbody>
</table>

## ContainerImage

Definition of a container image for starting a notebook instance with the environment installed in a container.

Fields

`repository`

`string`

Required. The path to the container image repository. For example: `gcr.io/{project_id}/{image_name}`

`tag`

`string`

The tag of the container image. If not specified, this defaults to the latest tag.

## CreateEnvironmentRequest

Request for creating a notebook environment.

Fields

`parent`

`string`

Required. Format: `projects/{project_id}/locations/{location}`

Authorization requires the following [IAM](https://cloud.google.com/iam/docs/) permission on the specified resource `parent` :

  - `notebooks.environments.create`

`environment_id`

`string`

Required. User-defined unique ID of this environment. The `environment_id` must be 1 to 63 characters long and contain only lowercase letters, numeric characters, and dashes. The first character must be a lowercase letter and the last character cannot be a dash.

`environment`

`  Environment  `

Required. The environment to be created.

## CreateExecutionRequest

Request to create notebook execution

Fields

`parent`

`string`

Required. Format: `parent=projects/{project_id}/locations/{location}`

Authorization requires the following [IAM](https://cloud.google.com/iam/docs/) permission on the specified resource `parent` :

  - `notebooks.executions.create`

`execution_id`

`string`

Required. User-defined unique ID of this execution.

`execution`

`  Execution  `

Required. The execution to be created.

## CreateInstanceRequest

Request for creating a notebook instance.

Fields

`parent`

`string`

Required. Format: `parent=projects/{project_id}/locations/{location}`

Authorization requires the following [IAM](https://cloud.google.com/iam/docs/) permission on the specified resource `parent` :

  - `notebooks.instances.create`

`instance_id`

`string`

Required. User-defined unique ID of this instance.

`instance`

`  Instance  `

Required. The instance to be created.

## CreateRuntimeRequest

Request for creating a Managed Notebook Runtime.

Fields

`parent`

`string`

Required. Format: `parent=projects/{project_id}/locations/{location}`

Authorization requires the following [IAM](https://cloud.google.com/iam/docs/) permission on the specified resource `parent` :

  - `notebooks.runtimes.create`

`runtime_id`

`string`

Required. User-defined unique ID of this Runtime.

`runtime`

`  Runtime  `

Required. The Runtime to be created.

`request_id`

`string`

Idempotent request UUID.

## CreateScheduleRequest

Request for created scheduled notebooks

Fields

`parent`

`string`

Required. Format: `parent=projects/{project_id}/locations/{location}`

Authorization requires the following [IAM](https://cloud.google.com/iam/docs/) permission on the specified resource `parent` :

  - `notebooks.schedules.create`

`schedule_id`

`string`

Required. User-defined unique ID of this schedule.

`schedule`

`  Schedule  `

Required. The schedule to be created.

## DeleteEnvironmentRequest

Request for deleting a notebook environment.

Fields

`name`

`string`

Required. Format: `projects/{project_id}/locations/{location}/environments/{environment_id}`

Authorization requires the following [IAM](https://cloud.google.com/iam/docs/) permission on the specified resource `name` :

  - `notebooks.environments.delete`

## DeleteExecutionRequest

Request for deleting a scheduled notebook execution

Fields

`name`

`string`

Required. Format: `projects/{project_id}/locations/{location}/executions/{execution_id}`

Authorization requires the following [IAM](https://cloud.google.com/iam/docs/) permission on the specified resource `name` :

  - `notebooks.executions.delete`

## DeleteInstanceRequest

Request for deleting a notebook instance.

Fields

`name`

`string`

Required. Format: `projects/{project_id}/locations/{location}/instances/{instance_id}`

Authorization requires the following [IAM](https://cloud.google.com/iam/docs/) permission on the specified resource `name` :

  - `notebooks.instances.delete`

## DeleteRuntimeRequest

Request for deleting a Managed Notebook Runtime.

Fields

`name`

`string`

Required. Format: `projects/{project_id}/locations/{location}/runtimes/{runtime_id}`

Authorization requires the following [IAM](https://cloud.google.com/iam/docs/) permission on the specified resource `name` :

  - `notebooks.runtimes.delete`

`request_id`

`string`

Idempotent request UUID.

## DeleteScheduleRequest

Request for deleting an Schedule

Fields

`name`

`string`

Required. Format: `projects/{project_id}/locations/{location}/schedules/{schedule_id}`

Authorization requires the following [IAM](https://cloud.google.com/iam/docs/) permission on the specified resource `name` :

  - `notebooks.schedules.delete`

## DiagnoseInstanceRequest

Request for creating a notebook instance diagnostic file.

Fields

`name`

`string`

Required. Format: `projects/{project_id}/locations/{location}/instances/{instance_id}`

`diagnostic_config`

`  DiagnosticConfig  `

Required. Defines flags that are used to run the diagnostic tool

`timeout_minutes`

`int32`

Optional. Maximum amount of time in minutes before the operation times out.

## DiagnosticConfig

Defines flags that are used to run the diagnostic tool

Fields

`gcs_bucket`

`string`

Required. User Cloud Storage bucket location (REQUIRED). Must be formatted with path prefix ( `gs://$GCS_BUCKET` ).

Permissions: User Managed Notebooks: - storage.buckets.writer: Must be given to the project's service account attached to VM. Google Managed Notebooks: - storage.buckets.writer: Must be given to the project's service account or user credentials attached to VM depending on authentication mode.

Cloud Storage bucket Log file will be written to `gs://$GCS_BUCKET/$RELATIVE_PATH/$VM_DATE_$TIME.tar.gz`

`relative_path`

`string`

Optional. Defines the relative storage path in the Cloud Storage bucket where the diagnostic logs will be written: Default path will be the root directory of the Cloud Storage bucket ( `gs://$GCS_BUCKET/$DATE_$TIME.tar.gz` ) Example of full path where Log file will be written: `gs://$GCS_BUCKET/$RELATIVE_PATH/`

`repair_flag_enabled`

`bool`

Optional. Enables flag to repair service for instance

`packet_capture_flag_enabled`

`bool`

Optional. Enables flag to capture packets from the instance for 30 seconds

`copy_home_files_flag_enabled`

`bool`

Optional. Enables flag to copy all `/home/jupyter` folder contents

## EncryptionConfig

Represents a custom encryption key configuration that can be applied to a resource. This will encrypt all disks in Virtual Machine.

Fields

`kms_key`

`string`

The Cloud KMS resource identifier of the customer-managed encryption key used to protect a resource, such as a disks. It has the following format: `projects/{PROJECT_ID}/locations/{REGION}/keyRings/{KEY_RING_NAME}/cryptoKeys/{KEY_NAME}`

## Environment

Definition of a software environment that is used to start a notebook instance.

Fields

`name`

`string`

Output only. Name of this environment. Format: `projects/{project_id}/locations/{location}/environments/{environment_id}`

`display_name`

`string`

Display name of this environment for the UI.

`description`

`string`

A brief description of this environment.

`post_startup_script`

`string`

Path to a Bash script that automatically runs after a notebook instance fully boots up. The path must be a URL or Cloud Storage path. Example: `"gs://path-to-file/file-name"`

`create_time`

`  Timestamp  `

Output only. The time at which this environment was created.

Union field `image_type` . Type of the environment; can be one of VM image, or container image. `image_type` can be only one of the following:

`vm_image`

`  VmImage  `

Use a Compute Engine VM image to start the notebook instance.

`container_image`

`  ContainerImage  `

Use a container image to start the notebook instance.

## Event

The definition of an Event for a managed / semi-managed notebook instance.

Fields

`report_time`

`  Timestamp  `

Event report time.

`type`

`  EventType  `

Event type.

`details`

`map<string, string>`

Optional. Event details. This field is used to pass event information.

## EventType

The definition of the event types.

Enums

`EVENT_TYPE_UNSPECIFIED`

Event is not specified.

`IDLE`

The instance / runtime is idle

`HEARTBEAT`

The instance / runtime is available. This event indicates that instance / runtime underlying compute is operational.

`HEALTH`

The instance / runtime health is available. This event indicates that instance / runtime health information.

`MAINTENANCE`

The instance / runtime is available. This event allows instance / runtime to send Host maintenance information to Control Plane. <https://cloud.google.com/compute/docs/gpus/gpu-host-maintenance>

## Execution

The definition of a single executed notebook.

Fields

`execution_template`

`  ExecutionTemplate  `

execute metadata including name, hardware spec, region, labels, etc.

`name`

`string`

Output only. The resource name of the execute. Format: `projects/{project_id}/locations/{location}/executions/{execution_id}`

`display_name`

`string`

Output only. Name used for UI purposes. Name can only contain alphanumeric characters and underscores '\_'.

`description`

`string`

A brief description of this execution.

`create_time`

`  Timestamp  `

Output only. Time the Execution was instantiated.

`update_time`

`  Timestamp  `

Output only. Time the Execution was last updated.

`state`

`  State  `

Output only. State of the underlying AI Platform job.

`output_notebook_file`

`string`

Output notebook file generated by this execution

`job_uri`

`string`

Output only. The URI of the external job used to execute the notebook.

## State

Enum description of the state of the underlying AIP job.

Enums

`STATE_UNSPECIFIED`

The job state is unspecified.

`QUEUED`

The job has been just created and processing has not yet begun.

`PREPARING`

The service is preparing to execution the job.

`RUNNING`

The job is in progress.

`SUCCEEDED`

The job completed successfully.

`FAILED`

The job failed. `error_message` should contain the details of the failure.

`CANCELLING`

The job is being cancelled. `error_message` should describe the reason for the cancellation.

`CANCELLED`

The job has been cancelled. `error_message` should describe the reason for the cancellation.

`EXPIRED`

The job has become expired (relevant to Agent Platform jobs) <https://cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/JobState>

`INITIALIZING`

The Execution is being created.

## ExecutionTemplate

The description a notebook execution workload.

Fields

` scale_tier (deprecated)  `

`  ScaleTier  `

> This item is deprecated\!

Required. Scale tier of the hardware used for notebook execution. DEPRECATED Will be discontinued. As right now only CUSTOM is supported.

`master_type`

`string`

Specifies the type of virtual machine to use for your training job's master worker. You must specify this field when `scaleTier` is set to `CUSTOM` .

You can use certain Compute Engine machine types directly in this field. The following types are supported:

  - `n1-standard-4`
  - `n1-standard-8`
  - `n1-standard-16`
  - `n1-standard-32`
  - `n1-standard-64`
  - `n1-standard-96`
  - `n1-highmem-2`
  - `n1-highmem-4`
  - `n1-highmem-8`
  - `n1-highmem-16`
  - `n1-highmem-32`
  - `n1-highmem-64`
  - `n1-highmem-96`
  - `n1-highcpu-16`
  - `n1-highcpu-32`
  - `n1-highcpu-64`
  - `n1-highcpu-96`

Alternatively, you can use the following legacy machine types:

  - `standard`
  - `large_model`
  - `complex_model_s`
  - `complex_model_m`
  - `complex_model_l`
  - `standard_gpu`
  - `complex_model_m_gpu`
  - `complex_model_l_gpu`
  - `standard_p100`
  - `complex_model_m_p100`
  - `standard_v100`
  - `large_model_v100`
  - `complex_model_m_v100`
  - `complex_model_l_v100`

Finally, if you want to use a TPU for training, specify `cloud_tpu` in this field. Learn more about the [special configuration options for training with TPU](https://cloud.google.com/ai-platform/training/docs/using-tpus#configuring_a_custom_tpu_machine) .

`accelerator_config`

`  SchedulerAcceleratorConfig  `

Configuration (count and accelerator type) for hardware running notebook execution.

`labels`

`map<string, string>`

Labels for execution. If execution is scheduled, a field included will be 'nbs-scheduled'. Otherwise, it is an immediate execution, and an included field will be 'nbs-immediate'. Use fields to efficiently index between various types of executions.

`input_notebook_file`

`string`

Path to the notebook file to execute. Must be in a Google Cloud Storage bucket. Format: `gs://{bucket_name}/{folder}/{notebook_file_name}` Ex: `gs://notebook_user/scheduled_notebooks/sentiment_notebook.ipynb`

`container_image_uri`

`string`

Container Image URI to a DLVM Example: 'gcr.io/deeplearning-platform-release/base-cu100' More examples can be found at: <https://cloud.google.com/ai-platform/deep-learning-containers/docs/choosing-container>

`output_notebook_folder`

`string`

Path to the notebook folder to write to. Must be in a Google Cloud Storage bucket path. Format: `gs://{bucket_name}/{folder}` Ex: `gs://notebook_user/scheduled_notebooks`

`params_yaml_file`

`string`

Parameters to be overridden in the notebook during execution. Ref <https://papermill.readthedocs.io/en/latest/usage-parameterize.html> on how to specifying parameters in the input notebook and pass them here in an YAML file. Ex: `gs://notebook_user/scheduled_notebooks/sentiment_notebook_params.yaml`

`parameters`

`string`

Parameters used within the 'input\_notebook\_file' notebook.

`service_account`

`string`

The email address of a service account to use when running the execution. You must have the `iam.serviceAccounts.actAs` permission for the specified service account.

`job_type`

`  JobType  `

The type of Job to be used on this execution.

`kernel_spec`

`string`

Name of the kernel spec to use. This must be specified if the kernel spec name on the execution target does not match the name in the input notebook file.

`tensorboard`

`string`

The name of a Agent Platform \[Tensorboard\] resource to which this execution will upload Tensorboard logs. Format: `projects/{project}/locations/{location}/tensorboards/{tensorboard}`

Union field `job_parameters` . Parameters for an execution type. NOTE: There are currently no extra parameters for VertexAI jobs. `job_parameters` can be only one of the following:

`dataproc_parameters`

`  DataprocParameters  `

Parameters used in Dataproc JobType executions.

`vertex_ai_parameters`

`  VertexAIParameters  `

Parameters used in Agent Platform JobType executions.

## DataprocParameters

Parameters used in Dataproc JobType executions.

Fields

`cluster`

`string`

URI for cluster used to run Dataproc execution. Format: `projects/{PROJECT_ID}/regions/{REGION}/clusters/{CLUSTER_NAME}`

## JobType

The backend used for this execution.

Enums

`JOB_TYPE_UNSPECIFIED`

No type specified.

`VERTEX_AI`

Custom Job in `aiplatform.googleapis.com` . Default value for an execution.

`DATAPROC`

Run execution on a cluster with Dataproc as a job. <https://cloud.google.com/dataproc/docs/reference/rest/v1/projects.regions.jobs>

## ScaleTier

Required. Specifies the machine types, the number of replicas for workers and parameter servers.

Enums

`SCALE_TIER_UNSPECIFIED`

Unspecified Scale Tier.

`BASIC`

A single worker instance. This tier is suitable for learning how to use Cloud ML, and for experimenting with new models using small datasets.

`STANDARD_1`

Many workers and a few parameter servers.

`PREMIUM_1`

A large number of workers with many parameter servers.

`BASIC_GPU`

A single worker instance with a K80 GPU.

`BASIC_TPU`

A single worker instance with a Cloud TPU.

`CUSTOM`

The CUSTOM tier is not a set tier, but rather enables you to use your own cluster specification. When you use this tier, set values to configure your processing cluster according to these guidelines:

  - You *must* set `ExecutionTemplate.masterType` to specify the type of machine to use for your master node. This is the only required setting.

## SchedulerAcceleratorConfig

Definition of a hardware accelerator. Note that not all combinations of `type` and `core_count` are valid. See [GPUs on Compute Engine](https://cloud.google.com/compute/docs/gpus) to find a valid combination. TPUs are not supported.

Fields

`type`

`  SchedulerAcceleratorType  `

Type of this accelerator.

`core_count`

`int64`

Count of cores of this accelerator.

## SchedulerAcceleratorType

Hardware accelerator types for AI Platform Training jobs.

Enums

`SCHEDULER_ACCELERATOR_TYPE_UNSPECIFIED`

Unspecified accelerator type. Default to no GPU.

`NVIDIA_TESLA_K80`

Nvidia Tesla K80 GPU.

`NVIDIA_TESLA_P100`

Nvidia Tesla P100 GPU.

`NVIDIA_TESLA_V100`

Nvidia Tesla V100 GPU.

`NVIDIA_TESLA_P4`

Nvidia Tesla P4 GPU.

`NVIDIA_TESLA_T4`

Nvidia Tesla T4 GPU.

`NVIDIA_TESLA_A100`

Nvidia Tesla A100 GPU.

`TPU_V2`

TPU v2.

`TPU_V3`

TPU v3.

## VertexAIParameters

Parameters used in Agent Platform JobType executions.

Fields

`network`

`string`

The full name of the Compute Engine [network](https://cloud.google.com/compute/docs/networks-and-firewalls#networks) to which the Job should be peered. For example, `projects/12345/global/networks/myVPC` . [Format](https://cloud.google.com/compute/docs/reference/rest/v1/networks/insert) is of the form `projects/{project}/global/networks/{network}` . Where `{project}` is a project number, as in `12345` , and `{network}` is a network name.

Private services access must already be configured for the network. If left unspecified, the job is not peered with any network.

`env`

`map<string, string>`

Environment variables. At most 100 environment variables can be specified and unique. Example: `GCP_BUCKET=gs://my-bucket/samples/`

## GetEnvironmentRequest

Request for getting a notebook environment.

Fields

`name`

`string`

Required. Format: `projects/{project_id}/locations/{location}/environments/{environment_id}`

Authorization requires the following [IAM](https://cloud.google.com/iam/docs/) permission on the specified resource `name` :

  - `notebooks.environments.get`

## GetExecutionRequest

Request for getting scheduled notebook execution

Fields

`name`

`string`

Required. Format: `projects/{project_id}/locations/{location}/executions/{execution_id}`

Authorization requires the following [IAM](https://cloud.google.com/iam/docs/) permission on the specified resource `name` :

  - `notebooks.executions.get`

## GetInstanceHealthRequest

Request for checking if a notebook instance is healthy.

Fields

`name`

`string`

Required. Format: `projects/{project_id}/locations/{location}/instances/{instance_id}`

Authorization requires the following [IAM](https://cloud.google.com/iam/docs/) permission on the specified resource `name` :

  - `notebooks.instances.getHealth`

## GetInstanceHealthResponse

Response for checking if a notebook instance is healthy.

Fields

`health_state`

`  HealthState  `

Output only. Runtime health\_state.

`health_info`

`map<string, string>`

Output only. Additional information about instance health. Example: healthInfo": { "docker\_proxy\_agent\_status": "1", "docker\_status": "1", "jupyterlab\_api\_status": "-1", "jupyterlab\_status": "-1", "updated": "2020-10-18 09:40:03.573409" }

## HealthState

If an instance is healthy or not.

Enums

`HEALTH_STATE_UNSPECIFIED`

The instance substate is unknown.

`HEALTHY`

The instance is known to be in an healthy state (for example, critical daemons are running) Applies to ACTIVE state.

`UNHEALTHY`

The instance is known to be in an unhealthy state (for example, critical daemons are not running) Applies to ACTIVE state.

`AGENT_NOT_INSTALLED`

The instance has not installed health monitoring agent. Applies to ACTIVE state.

`AGENT_NOT_RUNNING`

The instance health monitoring agent is not running. Applies to ACTIVE state.

## GetInstanceRequest

Request for getting a notebook instance.

Fields

`name`

`string`

Required. Format: `projects/{project_id}/locations/{location}/instances/{instance_id}`

Authorization requires the following [IAM](https://cloud.google.com/iam/docs/) permission on the specified resource `name` :

  - `notebooks.instances.get`

## GetRuntimeRequest

Request for getting a Managed Notebook Runtime.

Fields

`name`

`string`

Required. Format: `projects/{project_id}/locations/{location}/runtimes/{runtime_id}`

Authorization requires the following [IAM](https://cloud.google.com/iam/docs/) permission on the specified resource `name` :

  - `notebooks.runtimes.get`

## GetScheduleRequest

Request for getting scheduled notebook.

Fields

`name`

`string`

Required. Format: `projects/{project_id}/locations/{location}/schedules/{schedule_id}`

Authorization requires the following [IAM](https://cloud.google.com/iam/docs/) permission on the specified resource `name` :

  - `notebooks.schedules.get`

## Instance

The definition of a notebook instance.

Fields

`name`

`string`

Output only. The name of this notebook instance. Format: `projects/{project_id}/locations/{location}/instances/{instance_id}`

`post_startup_script`

`string`

Path to a Bash script that automatically runs after a notebook instance fully boots up. The path must be a URL or Cloud Storage path ( `gs://path-to-file/file-name` ).

`proxy_uri`

`string`

Output only. The proxy endpoint that is used to access the Jupyter notebook.

`instance_owners[]`

`string`

Input only. The owner of this instance after creation. Format: `alias@example.com`

Currently supports one owner only. If not specified, all of the service account users of your VM instance's service account can use the instance.

`service_account`

`string`

The service account on this instance, giving access to other Google Cloud services. You can use any service account within the same project, but you must have the service account user permission to use the instance.

If not specified, the [Compute Engine default service account](https://cloud.google.com/compute/docs/access/service-accounts#default_service_account) is used.

`service_account_scopes[]`

`string`

Optional. The URIs of service account scopes to be included in Compute Engine instances.

If not specified, the following [scopes](https://cloud.google.com/compute/docs/access/service-accounts#accesscopesiam) are defined: - <https://www.googleapis.com/auth/cloud-platform> - <https://www.googleapis.com/auth/userinfo.email> If not using default scopes, you need at least: <https://www.googleapis.com/auth/compute>

`machine_type`

`string`

Required. The [Compute Engine machine type](https://cloud.google.com/compute/docs/machine-resource) of this instance.

`accelerator_config`

`  AcceleratorConfig  `

The hardware accelerator used on this instance. If you use accelerators, make sure that your configuration has [enough vCPUs and memory to support the `machine_type` you have selected](https://cloud.google.com/compute/docs/gpus/#gpus-list) .

`state`

`  State  `

Output only. The state of this instance.

`install_gpu_driver`

`bool`

Whether the end user authorizes Google Cloud to install GPU driver on this instance. If this field is empty or set to false, the GPU driver won't be installed. Only applicable to instances with GPUs.

`custom_gpu_driver_path`

`string`

Specify a custom Cloud Storage path where the GPU driver is stored. If not specified, we'll automatically choose from official GPU drivers.

`boot_disk_type`

`  DiskType  `

Input only. The type of the boot disk attached to this instance, defaults to standard persistent disk ( `PD_STANDARD` ).

`boot_disk_size_gb`

`int64`

Input only. The size of the boot disk in GB attached to this instance, up to a maximum of 64000 GB (64 TB). The minimum recommended value is 100 GB. If not specified, this defaults to 100.

`data_disk_type`

`  DiskType  `

Input only. The type of the data disk attached to this instance, defaults to standard persistent disk ( `PD_STANDARD` ).

`data_disk_size_gb`

`int64`

Input only. The size of the data disk in GB attached to this instance, up to a maximum of 64000 GB (64 TB). You can choose the size of the data disk based on how big your notebooks and data are. If not specified, this defaults to 100.

`no_remove_data_disk`

`bool`

Input only. If true, the data disk will not be auto deleted when deleting the instance.

`disk_encryption`

`  DiskEncryption  `

Input only. Disk encryption method used on the boot and data disks, defaults to GMEK.

`kms_key`

`string`

Input only. The KMS key used to encrypt the disks, only applicable if disk\_encryption is CMEK. Format: `projects/{project_id}/locations/{location}/keyRings/{key_ring_id}/cryptoKeys/{key_id}`

Learn more about [using your own encryption keys](https://docs.cloud.google.com/kms/docs/quickstart) .

`disks[]`

`  Disk  `

Output only. Attached disks to notebook instance.

`shielded_instance_config`

`  ShieldedInstanceConfig  `

Optional. Shielded VM configuration. [Images using supported Shielded VM features](https://cloud.google.com/compute/docs/instances/modifying-shielded-vm) .

`no_public_ip`

`bool`

If true, no external IP will be assigned to this instance.

`no_proxy_access`

`bool`

If true, the notebook instance will not register with the proxy.

`network`

`string`

The name of the VPC that this instance is in. Format: `projects/{project_id}/global/networks/{network_id}`

`subnet`

`string`

The name of the subnet that this instance is in. Format: `projects/{project_id}/regions/{region}/subnetworks/{subnetwork_id}`

`labels`

`map<string, string>`

Labels to apply to this instance. These can be later modified by the setLabels method.

`metadata`

`map<string, string>`

Custom metadata to apply to this instance. For example, to specify a Cloud Storage bucket for automatic backup, you can use the `gcs-data-bucket` metadata tag. Format: `"--metadata=gcs-data-bucket=BUCKET"` .

`tags[]`

`string`

Optional. The Compute Engine network tags to add to runtime (see [Add network tags](https://cloud.google.com/vpc/docs/add-remove-network-tags) ).

`upgrade_history[]`

`  UpgradeHistoryEntry  `

The upgrade history of this instance.

`nic_type`

`  NicType  `

Optional. The type of vNIC to be used on this interface. This may be gVNIC or VirtioNet.

`reservation_affinity`

`  ReservationAffinity  `

Optional. The optional reservation affinity. Setting this field will apply the specified [Zonal Compute Reservation](https://cloud.google.com/compute/docs/instances/reserving-zonal-resources) to this notebook instance.

`creator`

`string`

Output only. Email address of entity that sent original CreateInstance request.

`can_ip_forward`

`bool`

Optional. Flag to enable ip forwarding or not, default false/off. <https://cloud.google.com/vpc/docs/using-routes#canipforward>

`create_time`

`  Timestamp  `

Output only. Instance creation time.

`update_time`

`  Timestamp  `

Output only. Instance update time.

`instance_migration_eligibility`

`  InstanceMigrationEligibility  `

Output only. Checks how feasible a migration from UmN to WbI is.

Union field `environment` . Type of the environment; can be one of VM image, or container image. `environment` can be only one of the following:

`vm_image`

`  VmImage  `

Use a Compute Engine VM image to start the notebook instance.

`container_image`

`  ContainerImage  `

Use a container image to start the notebook instance.

`migrated`

`bool`

Output only. Bool indicating whether this notebook has been migrated to a Workbench Instance

## AcceleratorConfig

Definition of a hardware accelerator. Note that not all combinations of `type` and `core_count` are valid. See [GPUs on Compute Engine](https://cloud.google.com/compute/docs/gpus/#gpus-list) to find a valid combination. TPUs are not supported.

Fields

`type`

`  AcceleratorType  `

Type of this accelerator.

`core_count`

`int64`

Count of cores of this accelerator.

## AcceleratorType

Definition of the types of hardware accelerators that can be used on this instance.

Enums

`ACCELERATOR_TYPE_UNSPECIFIED`

Accelerator type is not specified.

`NVIDIA_TESLA_K80`

Accelerator type is Nvidia Tesla K80.

`NVIDIA_TESLA_P100`

Accelerator type is Nvidia Tesla P100.

`NVIDIA_TESLA_V100`

Accelerator type is Nvidia Tesla V100.

`NVIDIA_TESLA_P4`

Accelerator type is Nvidia Tesla P4.

`NVIDIA_TESLA_T4`

Accelerator type is Nvidia Tesla T4.

`NVIDIA_TESLA_A100`

Accelerator type is Nvidia Tesla A100.

`NVIDIA_L4`

Accelerator type is Nvidia Tesla L4.

`NVIDIA_A100_80GB`

Accelerator type is Nvidia Tesla A100 80GB.

`NVIDIA_TESLA_T4_VWS`

Accelerator type is NVIDIA Tesla T4 Virtual Workstations.

`NVIDIA_TESLA_P100_VWS`

Accelerator type is NVIDIA Tesla P100 Virtual Workstations.

`NVIDIA_TESLA_P4_VWS`

Accelerator type is NVIDIA Tesla P4 Virtual Workstations.

`NVIDIA_H100_80GB`

Accelerator type is NVIDIA H100 80GB.

`NVIDIA_H100_MEGA_80GB`

Accelerator type is NVIDIA H100 Mega 80GB.

`TPU_V2`

(Coming soon) Accelerator type is TPU V2.

`TPU_V3`

(Coming soon) Accelerator type is TPU V3.

## Disk

An instance-attached disk resource.

Fields

`auto_delete`

`bool`

Indicates whether the disk will be auto-deleted when the instance is deleted (but not when the disk is detached from the instance).

`boot`

`bool`

Indicates that this is a boot disk. The virtual machine will use the first partition of the disk for its root filesystem.

`device_name`

`string`

Indicates a unique device name of your choice that is reflected into the `/dev/disk/by-id/google-*` tree of a Linux operating system running within the instance. This name can be used to reference the device for mounting, resizing, and so on, from within the instance.

If not specified, the server chooses a default device name to apply to this disk, in the form persistent-disk-x, where x is a number assigned by Google Compute Engine.This field is only applicable for persistent disks.

`disk_size_gb`

`int64`

Indicates the size of the disk in base-2 GB.

`guest_os_features[]`

`  GuestOsFeature  `

Indicates a list of features to enable on the guest operating system. Applicable only for bootable images. Read Enabling guest operating system features to see a list of available options.

`index`

`int64`

A zero-based index to this disk, where 0 is reserved for the boot disk. If you have many disks attached to an instance, each disk would have a unique index number.

`interface`

`string`

Indicates the disk interface to use for attaching this disk, which is either SCSI or NVME. The default is SCSI. Persistent disks must always use SCSI and the request will fail if you attempt to attach a persistent disk in any other format than SCSI. Local SSDs can use either NVME or SCSI. For performance characteristics of SCSI over NVMe, see Local SSD performance. Valid values:

  - `NVME`
  - `SCSI`

`kind`

`string`

Type of the resource. Always compute\#attachedDisk for attached disks.

`licenses[]`

`string`

A list of publicly visible licenses. Reserved for Google's use. A License represents billing and aggregate usage data for public and marketplace images.

`mode`

`string`

The mode in which to attach this disk, either `READ_WRITE` or `READ_ONLY` . If not specified, the default is to attach the disk in `READ_WRITE` mode. Valid values:

  - `READ_ONLY`
  - `READ_WRITE`

`source`

`string`

Indicates a valid partial or full URL to an existing Persistent Disk resource.

`type`

`string`

Indicates the type of the disk, either `SCRATCH` or `PERSISTENT` . Valid values:

  - `PERSISTENT`
  - `SCRATCH`

## GuestOsFeature

Guest OS features for boot disk.

Fields

`type`

`string`

The ID of a supported feature. Read Enabling guest operating system features to see a list of available options. Valid values:

  - `FEATURE_TYPE_UNSPECIFIED`
  - `MULTI_IP_SUBNET`
  - `SECURE_BOOT`
  - `UEFI_COMPATIBLE`
  - `VIRTIO_SCSI_MULTIQUEUE`
  - `WINDOWS`

## DiskEncryption

Definition of the disk encryption options.

Enums

`DISK_ENCRYPTION_UNSPECIFIED`

Disk encryption is not specified.

`GMEK`

Use Google managed encryption keys to encrypt the boot disk.

`CMEK`

Use customer managed encryption keys to encrypt the boot disk.

## DiskType

Possible disk types for notebook instances.

Enums

`DISK_TYPE_UNSPECIFIED`

Disk type not set.

`PD_STANDARD`

Standard persistent disk type.

`PD_SSD`

SSD persistent disk type.

`PD_BALANCED`

Balanced persistent disk type.

`PD_EXTREME`

Extreme persistent disk type.

## NicType

The type of vNIC driver. Default should be UNSPECIFIED\_NIC\_TYPE.

Enums

`UNSPECIFIED_NIC_TYPE`

No type specified.

`VIRTIO_NET`

VIRTIO

`GVNIC`

GVNIC

## ShieldedInstanceConfig

A set of Shielded Instance options. See [Images using supported Shielded VM features](https://cloud.google.com/compute/docs/instances/modifying-shielded-vm) . Not all combinations are valid.

Fields

`enable_secure_boot`

`bool`

Defines whether the instance has Secure Boot enabled.

Secure Boot helps ensure that the system only runs authentic software by verifying the digital signature of all boot components, and halting the boot process if signature verification fails. Disabled by default.

`enable_vtpm`

`bool`

Defines whether the instance has the vTPM enabled. Enabled by default.

`enable_integrity_monitoring`

`bool`

Defines whether the instance has integrity monitoring enabled.

Enables monitoring and attestation of the boot integrity of the instance. The attestation is performed against the integrity policy baseline. This baseline is initially derived from the implicitly trusted boot image when the instance is created. Enabled by default.

## State

The definition of the states of this instance.

Enums

`STATE_UNSPECIFIED`

State is not specified.

`STARTING`

The control logic is starting the instance.

`PROVISIONING`

The control logic is installing required frameworks and registering the instance with notebook proxy

`ACTIVE`

The instance is running.

`STOPPING`

The control logic is stopping the instance.

`STOPPED`

The instance is stopped.

`DELETED`

The instance is deleted.

`UPGRADING`

The instance is upgrading.

`INITIALIZING`

The instance is being created.

`REGISTERING`

The instance is getting registered.

`SUSPENDING`

The instance is suspending.

`SUSPENDED`

The instance is suspended.

## UpgradeHistoryEntry

The entry of VM image upgrade history.

Fields

`snapshot`

`string`

The snapshot of the boot disk of this notebook instance before upgrade.

`vm_image`

`string`

The VM image before this instance upgrade.

`container_image`

`string`

The container image before this instance upgrade.

`framework`

`string`

The framework of this notebook instance.

`version`

`string`

The version of the notebook instance before this upgrade.

`state`

`  State  `

The state of this instance upgrade history entry.

`create_time`

`  Timestamp  `

The time that this instance upgrade history entry is created.

` target_image (deprecated)  `

`string`

> This item is deprecated\!

Target VM Image. Format: `ainotebooks-vm/project/image-name/name` .

`action`

`  Action  `

Action. Rolloback or Upgrade.

`target_version`

`string`

Target VM Version, like m63.

## Action

The definition of operations of this upgrade history entry.

Enums

`ACTION_UNSPECIFIED`

Operation is not specified.

`UPGRADE`

Upgrade.

`ROLLBACK`

Rollback.

## State

The definition of the states of this upgrade history entry.

Enums

`STATE_UNSPECIFIED`

State is not specified.

`STARTED`

The instance upgrade is started.

`SUCCEEDED`

The instance upgrade is succeeded.

`FAILED`

The instance upgrade is failed.

## InstanceConfig

Notebook instance configurations that can be updated.

Fields

`notebook_upgrade_schedule`

`string`

Cron expression in UTC timezone, used to schedule instance auto upgrade. Please follow the [cron format](https://en.wikipedia.org/wiki/Cron) .

`enable_health_monitoring`

`bool`

Verifies core internal services are running.

## InstanceMigrationEligibility

InstanceMigrationEligibility represents the feasibility information of a migration from UmN to WbI.

Fields

`warnings[]`

`  Warning  `

Output only. Certain configurations will be defaulted during the migration.

`errors[]`

`  Error  `

Output only. Certain configurations make the UmN ineligible for an automatic migration. A manual migration is required.

## Error

A migration error message means certain configurations make the UmN ineligible for an automatic migration. A manual migration is required.

Enums

`ERROR_UNSPECIFIED`

Default type.

`DATAPROC_HUB`

The UmN uses Dataproc Hub and cannot be migrated.

## Warning

A migration warning message means certain configurations will be defaulted during the migration.

Enums

`WARNING_UNSPECIFIED`

Default type.

`UNSUPPORTED_MACHINE_TYPE`

The UmN uses an machine type that's unsupported in WbI. It will be migrated with the default machine type e2-standard-4. Users can change the machine type after the migration.

`UNSUPPORTED_ACCELERATOR_TYPE`

The UmN uses an accelerator type that's unsupported in WbI. It will be migrated without an accelerator. User can attach an accelerator after the migration.

`UNSUPPORTED_OS`

The UmN uses an operating system that's unsupported in WbI (e.g. Debian 10, Ubuntu). It will be replaced with Debian 11 in WbI.

`NO_REMOVE_DATA_DISK`

This UmN is configured with no\_remove\_data\_disk, which is no longer available in WbI.

`GCS_BACKUP`

This UmN is configured with the Cloud Storage backup feature, which is no longer available in WbI.

`POST_STARTUP_SCRIPT`

This UmN is configured with a post startup script. Please optionally provide the `post_startup_script_option` for the migration.

## IsInstanceUpgradeableRequest

Request for checking if a notebook instance is upgradeable.

Fields

`notebook_instance`

`string`

Required. Format: `projects/{project_id}/locations/{location}/instances/{instance_id}`

Authorization requires the following [IAM](https://cloud.google.com/iam/docs/) permission on the specified resource `notebookInstance` :

  - `notebooks.instances.checkUpgradability`

`type`

`  UpgradeType  `

Optional. The optional UpgradeType. Setting this field will search for additional compute images to upgrade this instance.

## IsInstanceUpgradeableResponse

Response for checking if a notebook instance is upgradeable.

Fields

`upgradeable`

`bool`

If an instance is upgradeable.

`upgrade_version`

`string`

The version this instance will be upgraded to if calling the upgrade endpoint. This field will only be populated if field upgradeable is true.

`upgrade_info`

`string`

Additional information about upgrade.

`upgrade_image`

`string`

The new image self link this instance will be upgraded to if calling the upgrade endpoint. This field will only be populated if field upgradeable is true.

## ListEnvironmentsRequest

Request for listing environments.

Fields

`parent`

`string`

Required. Format: `projects/{project_id}/locations/{location}`

Authorization requires the following [IAM](https://cloud.google.com/iam/docs/) permission on the specified resource `parent` :

  - `notebooks.environments.list`

`page_size`

`int32`

Maximum return size of the list call.

`page_token`

`string`

A previous returned page token that can be used to continue listing from the last result.

## ListEnvironmentsResponse

Response for listing environments.

Fields

`environments[]`

`  Environment  `

A list of returned environments.

`next_page_token`

`string`

A page token that can be used to continue listing from the last result in the next list call.

`unreachable[]`

`string`

Locations that could not be reached.

## ListExecutionsRequest

Request for listing scheduled notebook executions.

Fields

`parent`

`string`

Required. Format: `parent=projects/{project_id}/locations/{location}`

Authorization requires the following [IAM](https://cloud.google.com/iam/docs/) permission on the specified resource `parent` :

  - `notebooks.executions.list`

`page_size`

`int32`

Maximum return size of the list call.

`page_token`

`string`

A previous returned page token that can be used to continue listing from the last result.

`filter`

`string`

Filter applied to resulting executions. Currently only supports filtering executions by a specified `schedule_id` . Format: `schedule_id=<Schedule_ID>`

`order_by`

`string`

Sort by field.

## ListExecutionsResponse

Response for listing scheduled notebook executions

Fields

`executions[]`

`  Execution  `

A list of returned instances.

`next_page_token`

`string`

Page token that can be used to continue listing from the last result in the next list call.

`unreachable[]`

`string`

Executions IDs that could not be reached. For example:

    ['projects/{project_id}/location/{location}/executions/imagenet_test1',
     'projects/{project_id}/location/{location}/executions/classifier_train1']

## ListInstancesRequest

Request for listing notebook instances.

Fields

`parent`

`string`

Required. Format: `parent=projects/{project_id}/locations/{location}`

Authorization requires the following [IAM](https://cloud.google.com/iam/docs/) permission on the specified resource `parent` :

  - `notebooks.instances.list`

`page_size`

`int32`

Maximum return size of the list call.

`page_token`

`string`

A previous returned page token that can be used to continue listing from the last result.

`order_by`

`string`

Optional. Sort results. Supported values are "name", "name desc" or "" (unsorted).

`filter`

`string`

Optional. List filter.

## ListInstancesResponse

Response for listing notebook instances.

Fields

`instances[]`

`  Instance  `

A list of returned instances.

`next_page_token`

`string`

Page token that can be used to continue listing from the last result in the next list call.

`unreachable[]`

`string`

Locations that could not be reached. For example, `['us-west1-a', 'us-central1-b']` . A ListInstancesResponse will only contain either instances or unreachables,

## ListRuntimesRequest

Request for listing Managed Notebook Runtimes.

Fields

`parent`

`string`

Required. Format: `parent=projects/{project_id}/locations/{location}`

Authorization requires the following [IAM](https://cloud.google.com/iam/docs/) permission on the specified resource `parent` :

  - `notebooks.runtimes.list`

`page_size`

`int32`

Maximum return size of the list call.

`page_token`

`string`

A previous returned page token that can be used to continue listing from the last result.

`order_by`

`string`

Optional. Sort results. Supported values are "name", "name desc" or "" (unsorted).

`filter`

`string`

Optional. List filter.

## ListRuntimesResponse

Response for listing Managed Notebook Runtimes.

Fields

`runtimes[]`

`  Runtime  `

A list of returned Runtimes.

`next_page_token`

`string`

Page token that can be used to continue listing from the last result in the next list call.

`unreachable[]`

`string`

Locations that could not be reached. For example, `['us-west1', 'us-central1']` . A ListRuntimesResponse will only contain either runtimes or unreachables,

## ListSchedulesRequest

Request for listing scheduled notebook job.

Fields

`parent`

`string`

Required. Format: `parent=projects/{project_id}/locations/{location}`

Authorization requires the following [IAM](https://cloud.google.com/iam/docs/) permission on the specified resource `parent` :

  - `notebooks.schedules.list`

`page_size`

`int32`

Maximum return size of the list call.

`page_token`

`string`

A previous returned page token that can be used to continue listing from the last result.

`filter`

`string`

Filter applied to resulting schedules.

`order_by`

`string`

Field to order results by.

## ListSchedulesResponse

Response for listing scheduled notebook job.

Fields

`schedules[]`

`  Schedule  `

A list of returned instances.

`next_page_token`

`string`

Page token that can be used to continue listing from the last result in the next list call.

`unreachable[]`

`string`

Schedules that could not be reached. For example:

    ['projects/{project_id}/location/{location}/schedules/monthly_digest',
     'projects/{project_id}/location/{location}/schedules/weekly_sentiment']

## LocalDisk

A Local attached disk resource.

Fields

`auto_delete`

`bool`

Optional. Output only. Specifies whether the disk will be auto-deleted when the instance is deleted (but not when the disk is detached from the instance).

`boot`

`bool`

Optional. Output only. Indicates that this is a boot disk. The virtual machine will use the first partition of the disk for its root filesystem.

`device_name`

`string`

Optional. Output only. Specifies a unique device name of your choice that is reflected into the `/dev/disk/by-id/google-*` tree of a Linux operating system running within the instance. This name can be used to reference the device for mounting, resizing, and so on, from within the instance.

If not specified, the server chooses a default device name to apply to this disk, in the form persistent-disk-x, where x is a number assigned by Google Compute Engine. This field is only applicable for persistent disks.

`guest_os_features[]`

`  RuntimeGuestOsFeature  `

Output only. Indicates a list of features to enable on the guest operating system. Applicable only for bootable images. Read Enabling guest operating system features to see a list of available options.

`index`

`int32`

Output only. A zero-based index to this disk, where 0 is reserved for the boot disk. If you have many disks attached to an instance, each disk would have a unique index number.

`initialize_params`

`  LocalDiskInitializeParams  `

Input only. Specifies the parameters for a new disk that will be created alongside the new instance. Use initialization parameters to create boot disks or local SSDs attached to the new instance.

This property is mutually exclusive with the source property; you can only define one or the other, but not both.

`interface`

`string`

Specifies the disk interface to use for attaching this disk, which is either SCSI or NVME. The default is SCSI. Persistent disks must always use SCSI and the request will fail if you attempt to attach a persistent disk in any other format than SCSI. Local SSDs can use either NVME or SCSI. For performance characteristics of SCSI over NVMe, see Local SSD performance. Valid values:

  - `NVME`
  - `SCSI`

`kind`

`string`

Output only. Type of the resource. Always compute\#attachedDisk for attached disks.

`licenses[]`

`string`

Output only. Any valid publicly visible licenses.

`mode`

`string`

The mode in which to attach this disk, either `READ_WRITE` or `READ_ONLY` . If not specified, the default is to attach the disk in `READ_WRITE` mode. Valid values:

  - `READ_ONLY`
  - `READ_WRITE`

`source`

`string`

Specifies a valid partial or full URL to an existing Persistent Disk resource.

`type`

`string`

Specifies the type of the disk, either `SCRATCH` or `PERSISTENT` . If not specified, the default is `PERSISTENT` . Valid values:

  - `PERSISTENT`
  - `SCRATCH`

## RuntimeGuestOsFeature

Optional. A list of features to enable on the guest operating system. Applicable only for bootable images. Read [Enabling guest operating system features](https://cloud.google.com/compute/docs/images/create-delete-deprecate-private-images#guest-os-features) to see a list of available options. Guest OS features for boot disk.

Fields

`type`

`string`

The ID of a supported feature. Read [Enabling guest operating system features](https://cloud.google.com/compute/docs/images/create-delete-deprecate-private-images#guest-os-features) to see a list of available options.

Valid values:

  - `FEATURE_TYPE_UNSPECIFIED`
  - `MULTI_IP_SUBNET`
  - `SECURE_BOOT`
  - `UEFI_COMPATIBLE`
  - `VIRTIO_SCSI_MULTIQUEUE`
  - `WINDOWS`

## LocalDiskInitializeParams

Input only. Specifies the parameters for a new disk that will be created alongside the new instance. Use initialization parameters to create boot disks or local SSDs attached to the new runtime. This property is mutually exclusive with the source property; you can only define one or the other, but not both.

Fields

`description`

`string`

Optional. Provide this property when creating the disk.

`disk_name`

`string`

Optional. Specifies the disk name. If not specified, the default is to use the name of the instance. If the disk with the instance name exists already in the given zone/region, a new name will be automatically generated.

`disk_size_gb`

`int64`

Optional. Specifies the size of the disk in base-2 GB. If not specified, the disk will be the same size as the image (usually 10GB). If specified, the size must be equal to or larger than 10GB. Default 100 GB.

`disk_type`

`  DiskType  `

Input only. The type of the boot disk attached to this instance, defaults to standard persistent disk ( `PD_STANDARD` ).

`labels`

`map<string, string>`

Optional. Labels to apply to this disk. These can be later modified by the disks.setLabels method. This field is only applicable for persistent disks.

## DiskType

Possible disk types.

Enums

`DISK_TYPE_UNSPECIFIED`

Disk type not set.

`PD_STANDARD`

Standard persistent disk type.

`PD_SSD`

SSD persistent disk type.

`PD_BALANCED`

Balanced persistent disk type.

`PD_EXTREME`

Extreme persistent disk type.

## MigrateInstanceRequest

Request for migrating a User-Managed Notebook to Workbench Instances.

Fields

`name`

`string`

Required. Format: `projects/{project_id}/locations/{location}/instances/{instance_id}`

Authorization requires one or more of the following [IAM](https://cloud.google.com/iam/docs/) permissions on the specified resource `name` :

  - `notebooks.instances.get`
  - `notebooks.instances.create`

`post_startup_script_option`

`  PostStartupScriptOption  `

Optional. Specifies the behavior of post startup script during migration.

## PostStartupScriptOption

Specifies the behavior of post startup script during migration.

Enums

`POST_STARTUP_SCRIPT_OPTION_UNSPECIFIED`

Post startup script option is not specified. Default is POST\_STARTUP\_SCRIPT\_OPTION\_SKIP.

`POST_STARTUP_SCRIPT_OPTION_SKIP`

Not migrate the post startup script to the new Workbench Instance.

`POST_STARTUP_SCRIPT_OPTION_RERUN`

Redownload and rerun the same post startup script as the User-Managed Notebook.

## MigrateInstanceResponse

This type has no fields.

Blank message response type for MigrateInstance.

## MigrateRuntimeRequest

Request for migrating a Runtime to a Workbench Instance.

Fields

`name`

`string`

Required. Format: `projects/{project_id}/locations/{location}/runtimes/{runtime_id}`

Authorization requires one or more of the following [IAM](https://cloud.google.com/iam/docs/) permissions on the specified resource `name` :

  - `notebooks.runtimes.get`
  - `notebooks.instances.create`

`network`

`string`

Optional. Name of the VPC that the new Instance is in. This is required if the Runtime uses google-managed network. If the Runtime uses customer-owned network, it will reuse the same VPC, and this field must be empty. Format: `projects/{project_id}/global/networks/{network_id}`

`subnet`

`string`

Optional. Name of the subnet that the new Instance is in. This is required if the Runtime uses google-managed network. If the Runtime uses customer-owned network, it will reuse the same subnet, and this field must be empty. Format: `projects/{project_id}/regions/{region}/subnetworks/{subnetwork_id}`

`service_account`

`string`

Optional. The service account to be included in the Compute Engine instance of the new Workbench Instance when the Runtime uses "single user only" mode for permission. If not specified, the [Compute Engine default service account](https://cloud.google.com/compute/docs/access/service-accounts#default_service_account) is used. When the Runtime uses service account mode for permission, it will reuse the same service account, and this field must be empty.

`request_id`

`string`

Optional. Idempotent request UUID.

`post_startup_script_option`

`  PostStartupScriptOption  `

Optional. Specifies the behavior of post startup script during migration.

## PostStartupScriptOption

Specifies the behavior of post startup script during migration.

Enums

`POST_STARTUP_SCRIPT_OPTION_UNSPECIFIED`

Post startup script option is not specified. Default is POST\_STARTUP\_SCRIPT\_OPTION\_SKIP.

`POST_STARTUP_SCRIPT_OPTION_SKIP`

Not migrate the post startup script to the new Workbench Instance.

`POST_STARTUP_SCRIPT_OPTION_RERUN`

Redownload and rerun the same post startup script as the Google-Managed Notebook.

## OperationMetadata

Represents the metadata of the long-running operation.

Fields

`create_time`

`  Timestamp  `

The time the operation was created.

`end_time`

`  Timestamp  `

The time the operation finished running.

`target`

`string`

Server-defined resource path for the target of the operation.

`verb`

`string`

Name of the verb executed by the operation.

`status_message`

`string`

Human-readable status of the operation, if any.

`requested_cancellation`

`bool`

Identifies whether the user has requested cancellation of the operation. Operations that have successfully been cancelled have `  google.longrunning.Operation.error  ` value with a `  google.rpc.Status.code  ` of `1` , corresponding to `Code.CANCELLED` .

`api_version`

`string`

API version used to start the operation.

`endpoint`

`string`

API endpoint name of this operation.

## RegisterInstanceRequest

Request for registering a notebook instance.

Fields

`parent`

`string`

Required. Format: `parent=projects/{project_id}/locations/{location}`

Authorization requires the following [IAM](https://cloud.google.com/iam/docs/) permission on the specified resource `parent` :

  - `notebooks.instances.create`

`instance_id`

`string`

Required. User defined unique ID of this instance. The `instance_id` must be 1 to 63 characters long and contain only lowercase letters, numeric characters, and dashes. The first character must be a lowercase letter and the last character cannot be a dash.

## ReportInstanceInfoRequest

Request for notebook instances to report information to Notebooks API.

Fields

`name`

`string`

Required. Format: `projects/{project_id}/locations/{location}/instances/{instance_id}`

`vm_id`

`string`

Required. The VM hardware token for authenticating the VM. <https://cloud.google.com/compute/docs/instances/verifying-instance-identity>

`metadata`

`map<string, string>`

The metadata reported to Notebooks API. This will be merged to the instance metadata store

## ReportRuntimeEventRequest

Request for reporting a Managed Notebook Event.

Fields

`name`

`string`

Required. Format: `projects/{project_id}/locations/{location}/runtimes/{runtime_id}`

Authorization requires the following [IAM](https://cloud.google.com/iam/docs/) permission on the specified resource `name` :

  - `iam.permissions.none`

`vm_id`

`string`

Required. The VM hardware token for authenticating the VM. <https://cloud.google.com/compute/docs/instances/verifying-instance-identity>

`event`

`  Event  `

Required. The Event to be reported.

## ReservationAffinity

Reservation Affinity for consuming Zonal reservation.

Fields

`consume_reservation_type`

`  Type  `

Optional. Type of reservation to consume

`key`

`string`

Optional. Corresponds to the label key of reservation resource.

`values[]`

`string`

Optional. Corresponds to the label values of reservation resource.

## Type

Indicates whether to consume capacity from an reservation or not.

Enums

`TYPE_UNSPECIFIED`

Default type.

`NO_RESERVATION`

Do not consume from any allocated capacity.

`ANY_RESERVATION`

Consume any reservation available.

`SPECIFIC_RESERVATION`

Must consume from a specific reservation. Must specify key value fields for specifying the reservations.

## ResetInstanceRequest

Request for resetting a notebook instance

Fields

`name`

`string`

Required. Format: `projects/{project_id}/locations/{location}/instances/{instance_id}`

Authorization requires the following [IAM](https://cloud.google.com/iam/docs/) permission on the specified resource `name` :

  - `notebooks.instances.reset`

## ResetRuntimeRequest

Request for resetting a Managed Notebook Runtime.

Fields

`name`

`string`

Required. Format: `projects/{project_id}/locations/{location}/runtimes/{runtime_id}`

Authorization requires the following [IAM](https://cloud.google.com/iam/docs/) permission on the specified resource `name` :

  - `notebooks.runtimes.reset`

`request_id`

`string`

Idempotent request UUID.

## RollbackInstanceRequest

Request for rollbacking a notebook instance

Fields

`name`

`string`

Required. Format: `projects/{project_id}/locations/{location}/instances/{instance_id}`

Authorization requires the following [IAM](https://cloud.google.com/iam/docs/) permission on the specified resource `name` :

  - `iam.permissions.none`

`target_snapshot`

`string`

Required. The snapshot for rollback. Example: `projects/test-project/global/snapshots/krwlzipynril` .

## Runtime

The definition of a Runtime for a managed notebook instance.

Fields

`name`

`string`

Output only. The resource name of the runtime. Format: `projects/{project}/locations/{location}/runtimes/{runtimeId}`

`state`

`  State  `

Output only. Runtime state.

`health_state`

`  HealthState  `

Output only. Runtime health\_state.

`access_config`

`  RuntimeAccessConfig  `

The config settings for accessing runtime.

`software_config`

`  RuntimeSoftwareConfig  `

The config settings for software inside the runtime.

`metrics`

`  RuntimeMetrics  `

Output only. Contains Runtime daemon metrics such as Service status and JupyterLab stats.

`create_time`

`  Timestamp  `

Output only. Runtime creation time.

`update_time`

`  Timestamp  `

Output only. Runtime update time.

`labels`

`map<string, string>`

Optional. The labels to associate with this Managed Notebook or Runtime. Label **keys** must contain 1 to 63 characters, and must conform to [RFC 1035](https://www.ietf.org/rfc/rfc1035.txt) . Label **values** may be empty, but, if present, must contain 1 to 63 characters, and must conform to [RFC 1035](https://www.ietf.org/rfc/rfc1035.txt) . No more than 32 labels can be associated with a cluster.

`runtime_migration_eligibility`

`  RuntimeMigrationEligibility  `

Output only. Checks how feasible a migration from GmN to WbI is.

Union field `runtime_type` . Type of the runtime; currently only supports Compute Engine VM. `runtime_type` can be only one of the following:

`virtual_machine`

`  VirtualMachine  `

Use a Compute Engine VM image to start the managed notebook instance.

`migrated`

`bool`

Output only. Bool indicating whether this notebook has been migrated to a Workbench Instance

## HealthState

The runtime substate.

Enums

`HEALTH_STATE_UNSPECIFIED`

The runtime substate is unknown.

`HEALTHY`

The runtime is known to be in an healthy state (for example, critical daemons are running) Applies to ACTIVE state.

`UNHEALTHY`

The runtime is known to be in an unhealthy state (for example, critical daemons are not running) Applies to ACTIVE state.

`AGENT_NOT_INSTALLED`

The runtime has not installed health monitoring agent. Applies to ACTIVE state.

`AGENT_NOT_RUNNING`

The runtime health monitoring agent is not running. Applies to ACTIVE state.

## State

The definition of the states of this runtime.

Enums

`STATE_UNSPECIFIED`

State is not specified.

`STARTING`

The compute layer is starting the runtime. It is not ready for use.

`PROVISIONING`

The compute layer is installing required frameworks and registering the runtime with notebook proxy. It cannot be used.

`ACTIVE`

The runtime is currently running. It is ready for use.

`STOPPING`

The control logic is stopping the runtime. It cannot be used.

`STOPPED`

The runtime is stopped. It cannot be used.

`DELETING`

The runtime is being deleted. It cannot be used.

`UPGRADING`

The runtime is upgrading. It cannot be used.

`INITIALIZING`

The runtime is being created and set up. It is not ready for use.

## RuntimeAcceleratorConfig

Definition of the types of hardware accelerators that can be used. See [Compute Engine AcceleratorTypes](https://cloud.google.com/compute/docs/reference/beta/acceleratorTypes) . Examples:

  - `nvidia-tesla-k80`
  - `nvidia-tesla-p100`
  - `nvidia-tesla-v100`
  - `nvidia-tesla-p4`
  - `nvidia-tesla-t4`
  - `nvidia-tesla-a100`

Fields

`type`

`  AcceleratorType  `

Accelerator model.

`core_count`

`int64`

Count of cores of this accelerator.

## AcceleratorType

Type of this accelerator.

Enums

`ACCELERATOR_TYPE_UNSPECIFIED`

Accelerator type is not specified.

`NVIDIA_TESLA_K80`

Accelerator type is Nvidia Tesla K80.

> This item is deprecated\!

`NVIDIA_TESLA_P100`

Accelerator type is Nvidia Tesla P100.

`NVIDIA_TESLA_V100`

Accelerator type is Nvidia Tesla V100.

`NVIDIA_TESLA_P4`

Accelerator type is Nvidia Tesla P4.

`NVIDIA_TESLA_T4`

Accelerator type is Nvidia Tesla T4.

`NVIDIA_TESLA_A100`

Accelerator type is Nvidia Tesla A100 - 40GB.

`NVIDIA_L4`

Accelerator type is Nvidia L4.

`TPU_V2`

(Coming soon) Accelerator type is TPU V2.

`TPU_V3`

(Coming soon) Accelerator type is TPU V3.

`NVIDIA_TESLA_T4_VWS`

Accelerator type is NVIDIA Tesla T4 Virtual Workstations.

`NVIDIA_TESLA_P100_VWS`

Accelerator type is NVIDIA Tesla P100 Virtual Workstations.

`NVIDIA_TESLA_P4_VWS`

Accelerator type is NVIDIA Tesla P4 Virtual Workstations.

## RuntimeAccessConfig

Specifies the login configuration for Runtime

Fields

`access_type`

`  RuntimeAccessType  `

The type of access mode this instance.

`runtime_owner`

`string`

The owner of this runtime after creation. Format: `alias@example.com` Currently supports one owner only.

`proxy_uri`

`string`

Output only. The proxy endpoint that is used to access the runtime.

## RuntimeAccessType

Possible ways to access runtime. Authentication mode. Currently supports: Single User only.

Enums

`RUNTIME_ACCESS_TYPE_UNSPECIFIED`

Unspecified access.

`SINGLE_USER`

Single user login.

`SERVICE_ACCOUNT`

Service Account mode. In Service Account mode, Runtime creator will specify a SA that exists in the consumer project. Using Runtime Service Account field. Users accessing the Runtime need ActAs (Service Account User) permission.

## RuntimeMetrics

Contains runtime daemon metrics, such as OS and kernels and sessions stats.

Fields

`system_metrics`

`map<string, string>`

Output only. The system metrics.

## RuntimeMigrationEligibility

RuntimeMigrationEligibility represents the feasibility information of a migration from GmN to WbI.

Fields

`warnings[]`

`  Warning  `

Output only. Certain configurations will be defaulted during the migration.

`errors[]`

`  Error  `

Output only. Certain configurations make the GmN ineligible for an automatic migration. A manual migration is required.

## Error

A migration error message means certain configurations make the GmN ineligible for an automatic migration. A manual migration is required.

Enums

`ERROR_UNSPECIFIED`

Default type.

`CUSTOM_CONTAINER`

The GmN is configured with custom container(s) and cannot be migrated.

## Warning

A migration warning message means certain configurations will be defaulted during the migration.

Enums

`WARNING_UNSPECIFIED`

Default type.

`UNSUPPORTED_ACCELERATOR_TYPE`

The GmN uses an accelerator type that's unsupported in WbI. It will be migrated without an accelerator. Users can attach an accelerator after the migration.

`UNSUPPORTED_OS`

The GmN uses an operating system that's unsupported in WbI (e.g. Debian 10). It will be replaced with Debian 11 in WbI.

`RESERVED_IP_RANGE`

This GmN is configured with reserved IP range, which is no longer applicable in WbI.

`GOOGLE_MANAGED_NETWORK`

This GmN is configured with a Google managed network. Please provide the `network` and `subnet` options for the migration.

`POST_STARTUP_SCRIPT`

This GmN is configured with a post startup script. Please optionally provide the `post_startup_script_option` for the migration.

`SINGLE_USER`

This GmN is configured with single user mode. Please optionally provide the `service_account` option for the migration.

## RuntimeShieldedInstanceConfig

A set of Shielded Instance options. See [Images using supported Shielded VM features](https://cloud.google.com/compute/docs/instances/modifying-shielded-vm) . Not all combinations are valid.

Fields

`enable_secure_boot`

`bool`

Defines whether the instance has Secure Boot enabled.

Secure Boot helps ensure that the system only runs authentic software by verifying the digital signature of all boot components, and halting the boot process if signature verification fails. Disabled by default.

`enable_vtpm`

`bool`

Defines whether the instance has the vTPM enabled. Enabled by default.

`enable_integrity_monitoring`

`bool`

Defines whether the instance has integrity monitoring enabled.

Enables monitoring and attestation of the boot integrity of the instance. The attestation is performed against the integrity policy baseline. This baseline is initially derived from the implicitly trusted boot image when the instance is created. Enabled by default.

## RuntimeSoftwareConfig

Specifies the selection and configuration of software inside the runtime. The properties to set on runtime. Properties keys are specified in `key:value` format, for example:

  - `idle_shutdown: true`
  - `idle_shutdown_timeout: 180`
  - `enable_health_monitoring: true`

Fields

`notebook_upgrade_schedule`

`string`

Cron expression in UTC timezone, used to schedule instance auto upgrade. Please follow the [cron format](https://en.wikipedia.org/wiki/Cron) .

`idle_shutdown_timeout`

`int32`

Time in minutes to wait before shutting down runtime. Default: 180 minutes

`install_gpu_driver`

`bool`

Install Nvidia Driver automatically. Default: True

`custom_gpu_driver_path`

`string`

Specify a custom Cloud Storage path where the GPU driver is stored. If not specified, we'll automatically choose from official GPU drivers.

`post_startup_script`

`string`

Path to a Bash script that automatically runs after a notebook instance fully boots up. The path must be a URL or Cloud Storage path ( `gs://path-to-file/file-name` ).

`kernels[]`

`  ContainerImage  `

Optional. Use a list of container images to use as Kernels in the notebook instance.

`post_startup_script_behavior`

`  PostStartupScriptBehavior  `

Behavior for the post startup script.

`enable_health_monitoring`

`bool`

Verifies core internal services are running. Default: True

`idle_shutdown`

`bool`

Runtime will automatically shutdown after idle\_shutdown\_time. Default: True

`upgradeable`

`bool`

Output only. Bool indicating whether an newer image is available in an image family.

`disable_terminal`

`bool`

Bool indicating whether JupyterLab terminal will be available or not. Default: False

`version`

`string`

Output only. version of boot image such as M100, from release label of the image.

`mixer_disabled`

`bool`

Bool indicating whether mixer client should be disabled. Default: False

## PostStartupScriptBehavior

Behavior for the post startup script.

Enums

`POST_STARTUP_SCRIPT_BEHAVIOR_UNSPECIFIED`

Unspecified post startup script behavior. Will run only once at creation.

`RUN_EVERY_START`

Runs the post startup script provided during creation at every start.

`DOWNLOAD_AND_RUN_EVERY_START`

Downloads and runs the provided post startup script at every start.

## Schedule

The definition of a schedule.

Fields

`name`

`string`

Output only. The name of this schedule. Format: `projects/{project_id}/locations/{location}/schedules/{schedule_id}`

`display_name`

`string`

Output only. Display name used for UI purposes. Name can only contain alphanumeric characters, hyphens `-` , and underscores `_` .

`description`

`string`

A brief description of this environment.

`state`

`  State  `

`cron_schedule`

`string`

Cron-tab formatted schedule by which the job will execute. Format: minute, hour, day of month, month, day of week, e.g. `0 0 * * WED` = every Wednesday More examples: <https://crontab.guru/examples.html>

`time_zone`

`string`

Timezone on which the cron\_schedule. The value of this field must be a time zone name from the tz database. TZ Database: <https://en.wikipedia.org/wiki/List_of_tz_database_time_zones>

Note that some time zones include a provision for daylight savings time. The rules for daylight saving time are determined by the chosen tz. For UTC use the string "utc". If a time zone is not specified, the default will be in UTC (also known as GMT).

`create_time`

`  Timestamp  `

Output only. Time the schedule was created.

`update_time`

`  Timestamp  `

Output only. Time the schedule was last updated.

`execution_template`

`  ExecutionTemplate  `

Notebook Execution Template corresponding to this schedule.

`recent_executions[]`

`  Execution  `

Output only. The most recent execution names triggered from this schedule and their corresponding states.

## State

State of the job.

Enums

`STATE_UNSPECIFIED`

Unspecified state.

`ENABLED`

The job is executing normally.

`PAUSED`

The job is paused by the user. It will not execute. A user can intentionally pause the job using [Cloud Scheduler](https://cloud.google.com/scheduler/docs/creating#pause) .

`DISABLED`

The job is disabled by the system due to error. The user cannot directly set a job to be disabled.

`UPDATE_FAILED`

The job state resulting from a failed [CloudScheduler.UpdateJob](https://cloud.google.com/scheduler/docs/creating#edit) operation. To recover a job from this state, retry [CloudScheduler.UpdateJob](https://cloud.google.com/scheduler/docs/creating#edit) until a successful response is received.

`INITIALIZING`

The schedule resource is being created.

`DELETING`

The schedule resource is being deleted.

## SetInstanceAcceleratorRequest

Request for setting instance accelerator.

Fields

`name`

`string`

Required. Format: `projects/{project_id}/locations/{location}/instances/{instance_id}`

Authorization requires the following [IAM](https://cloud.google.com/iam/docs/) permission on the specified resource `name` :

  - `notebooks.instances.setAccelerator`

`type`

`  AcceleratorType  `

Required. Type of this accelerator.

`core_count`

`int64`

Required. Count of cores of this accelerator. Note that not all combinations of `type` and `core_count` are valid. See [GPUs on Compute Engine](https://cloud.google.com/compute/docs/gpus/#gpus-list) to find a valid combination. TPUs are not supported.

## SetInstanceLabelsRequest

Request for setting instance labels.

Fields

`name`

`string`

Required. Format: `projects/{project_id}/locations/{location}/instances/{instance_id}`

Authorization requires the following [IAM](https://cloud.google.com/iam/docs/) permission on the specified resource `name` :

  - `notebooks.instances.setLabels`

`labels`

`map<string, string>`

Labels to apply to this instance. These can be later modified by the setLabels method

## SetInstanceMachineTypeRequest

Request for setting instance machine type.

Fields

`name`

`string`

Required. Format: `projects/{project_id}/locations/{location}/instances/{instance_id}`

Authorization requires the following [IAM](https://cloud.google.com/iam/docs/) permission on the specified resource `name` :

  - `notebooks.instances.setMachineType`

`machine_type`

`string`

Required. The [Compute Engine machine type](https://cloud.google.com/compute/docs/machine-resource) .

## StartInstanceRequest

Request for starting a notebook instance

Fields

`name`

`string`

Required. Format: `projects/{project_id}/locations/{location}/instances/{instance_id}`

Authorization requires the following [IAM](https://cloud.google.com/iam/docs/) permission on the specified resource `name` :

  - `notebooks.instances.start`

## StartRuntimeRequest

Request for starting a Managed Notebook Runtime.

Fields

`name`

`string`

Required. Format: `projects/{project_id}/locations/{location}/runtimes/{runtime_id}`

Authorization requires the following [IAM](https://cloud.google.com/iam/docs/) permission on the specified resource `name` :

  - `notebooks.runtimes.start`

`request_id`

`string`

Idempotent request UUID.

## StopInstanceRequest

Request for stopping a notebook instance

Fields

`name`

`string`

Required. Format: `projects/{project_id}/locations/{location}/instances/{instance_id}`

Authorization requires the following [IAM](https://cloud.google.com/iam/docs/) permission on the specified resource `name` :

  - `notebooks.instances.stop`

## StopRuntimeRequest

Request for stopping a Managed Notebook Runtime.

Fields

`name`

`string`

Required. Format: `projects/{project_id}/locations/{location}/runtimes/{runtime_id}`

Authorization requires the following [IAM](https://cloud.google.com/iam/docs/) permission on the specified resource `name` :

  - `notebooks.runtimes.stop`

`request_id`

`string`

Idempotent request UUID.

## SwitchRuntimeRequest

Request for switching a Managed Notebook Runtime.

Fields

`name`

`string`

Required. Format: `projects/{project_id}/locations/{location}/runtimes/{runtime_id}`

Authorization requires the following [IAM](https://cloud.google.com/iam/docs/) permission on the specified resource `name` :

  - `notebooks.runtimes.switch`

`machine_type`

`string`

machine type.

`accelerator_config`

`  RuntimeAcceleratorConfig  `

accelerator config.

`request_id`

`string`

Idempotent request UUID.

## UpdateInstanceConfigRequest

Request for updating instance configurations.

Fields

`name`

`string`

Required. Format: `projects/{project_id}/locations/{location}/instances/{instance_id}`

Authorization requires the following [IAM](https://cloud.google.com/iam/docs/) permission on the specified resource `name` :

  - `notebooks.instances.updateConfig`

`config`

`  InstanceConfig  `

The instance configurations to be updated.

## UpdateInstanceMetadataItemsRequest

Request for adding/changing metadata items for an instance.

Fields

`name`

`string`

Required. Format: `projects/{project_id}/locations/{location}/instances/{instance_id}`

Authorization requires the following [IAM](https://cloud.google.com/iam/docs/) permission on the specified resource `name` :

  - `notebooks.instances.updateConfig`

`items`

`map<string, string>`

Metadata items to add/update for the instance.

## UpdateInstanceMetadataItemsResponse

Response for adding/changing metadata items for an instance.

Fields

`items`

`map<string, string>`

Map of items that were added/updated to/in the metadata.

## UpdateRuntimeRequest

Request for updating a Managed Notebook configuration.

Fields

`runtime`

`  Runtime  `

Required. The Runtime to be updated.

Authorization requires the following [IAM](https://cloud.google.com/iam/docs/) permission on the specified resource `runtime` :

  - `notebooks.runtimes.update`

`update_mask`

`  FieldMask  `

Required. Specifies the path, relative to `Runtime` , of the field to update. For example, to change the software configuration kernels, the `update_mask` parameter would be specified as `software_config.kernels` , and the `PATCH` request body would specify the new value, as follows:

    {
      "software_config":{
        "kernels": [{
           'repository':
           'gcr.io/deeplearning-platform-release/pytorch-gpu', 'tag':
           'latest' }],
        }
    }

Currently, only the following fields can be updated:

  - `software_config.kernels`
  - `software_config.post_startup_script`
  - `software_config.custom_gpu_driver_path`
  - `software_config.idle_shutdown`
  - `software_config.idle_shutdown_timeout`
  - `software_config.disable_terminal`
  - `labels`

`request_id`

`string`

Idempotent request UUID.

## UpdateShieldedInstanceConfigRequest

Request for updating the Shielded Instance config for a notebook instance. You can only use this method on a stopped instance

Fields

`name`

`string`

Required. Format: `projects/{project_id}/locations/{location}/instances/{instance_id}`

Authorization requires the following [IAM](https://cloud.google.com/iam/docs/) permission on the specified resource `name` :

  - `notebooks.instances.updateShieldInstanceConfig`

`shielded_instance_config`

`  ShieldedInstanceConfig  `

ShieldedInstance configuration to be updated.

## UpgradeInstanceRequest

Request for upgrading a notebook instance

Fields

`name`

`string`

Required. Format: `projects/{project_id}/locations/{location}/instances/{instance_id}`

Authorization requires the following [IAM](https://cloud.google.com/iam/docs/) permission on the specified resource `name` :

  - `notebooks.instances.upgrade`

`type`

`  UpgradeType  `

Optional. The optional UpgradeType. Setting this field will search for additional compute images to upgrade this instance.

## UpgradeType

Definition of the types of upgrade that can be used on this instance.

Enums

`UPGRADE_TYPE_UNSPECIFIED`

Upgrade type is not specified.

`UPGRADE_FRAMEWORK`

Upgrade ML framework.

`UPGRADE_OS`

Upgrade Operating System.

`UPGRADE_CUDA`

Upgrade CUDA.

`UPGRADE_ALL`

Upgrade All (OS, Framework and CUDA).

## VirtualMachine

Runtime using Virtual Machine for computing.

Fields

`instance_name`

`string`

Output only. The user-friendly name of the Managed Compute Engine instance.

`instance_id`

`string`

Output only. The unique identifier of the Managed Compute Engine instance.

`virtual_machine_config`

`  VirtualMachineConfig  `

Virtual Machine configuration settings.

## VirtualMachineConfig

The config settings for virtual machine.

Fields

`zone`

`string`

Output only. The zone where the virtual machine is located. If using regional request, the notebooks service will pick a location in the corresponding runtime region. On a get request, zone will always be present. Example: \* `us-central1-b`

`machine_type`

`string`

Required. The Compute Engine machine type used for runtimes. Short name is valid. Examples: \* `n1-standard-2` \* `e2-standard-8`

`container_images[]`

`  ContainerImage  `

Optional. Use a list of container images to use as Kernels in the notebook instance.

`data_disk`

`  LocalDisk  `

Required. Data disk option configuration settings.

`encryption_config`

`  EncryptionConfig  `

Optional. Encryption settings for virtual machine data disk.

`shielded_instance_config`

`  RuntimeShieldedInstanceConfig  `

Optional. Shielded VM Instance configuration settings.

`accelerator_config`

`  RuntimeAcceleratorConfig  `

Optional. The Compute Engine accelerator configuration for this runtime.

`network`

`string`

Optional. The Compute Engine network to be used for machine communications. Cannot be specified with subnetwork. If neither `network` nor `subnet` is specified, the "default" network of the project is used, if it exists.

A full URL or partial URI. Examples:

  - `https://www.googleapis.com/compute/v1/projects/[project_id]/global/networks/default`
  - `projects/[project_id]/global/networks/default`

Runtimes are managed resources inside Google Infrastructure. Runtimes support the following network configurations:

  - Google Managed Network (Network & subnet are empty)
  - Consumer Project VPC (network & subnet are required). Requires configuring Private Service Access.
  - Shared VPC (network & subnet are required). Requires configuring Private Service Access.

`subnet`

`string`

Optional. The Compute Engine subnetwork to be used for machine communications. Cannot be specified with network.

A full URL or partial URI are valid. Examples:

  - `https://www.googleapis.com/compute/v1/projects/[project_id]/regions/us-east1/subnetworks/sub0`
  - `projects/[project_id]/regions/us-east1/subnetworks/sub0`

`internal_ip_only`

`bool`

Optional. If true, runtime will only have internal IP addresses. By default, runtimes are not restricted to internal IP addresses, and will have ephemeral external IP addresses assigned to each vm. This `internal_ip_only` restriction can only be enabled for subnetwork enabled networks, and all dependencies must be configured to be accessible without external IP addresses.

`tags[]`

`string`

Optional. The Compute Engine network tags to add to runtime (see [Add network tags](https://cloud.google.com/vpc/docs/add-remove-network-tags) ).

`guest_attributes`

`map<string, string>`

Output only. The Compute Engine guest attributes. (see [Project and instance guest attributes](https://cloud.google.com/compute/docs/storing-retrieving-metadata#guest_attributes) ).

`metadata`

`map<string, string>`

Optional. The Compute Engine metadata entries to add to virtual machine. (see [Project and instance metadata](https://cloud.google.com/compute/docs/storing-retrieving-metadata#project_and_instance_metadata) ).

`labels`

`map<string, string>`

Optional. The labels to associate with this runtime. Label **keys** must contain 1 to 63 characters, and must conform to [RFC 1035](https://www.ietf.org/rfc/rfc1035.txt) . Label **values** may be empty, but, if present, must contain 1 to 63 characters, and must conform to [RFC 1035](https://www.ietf.org/rfc/rfc1035.txt) . No more than 32 labels can be associated with a cluster.

`nic_type`

`  NicType  `

Optional. The type of vNIC to be used on this interface. This may be gVNIC or VirtioNet.

`reserved_ip_range`

`string`

Optional. Reserved IP Range name is used for VPC Peering. The subnetwork allocation will use the range *name* if it's assigned.

Example: managed-notebooks-range-c

    PEERING_RANGE_NAME_3=managed-notebooks-range-c
    gcloud compute addresses create $PEERING_RANGE_NAME_3 \
      --global \
      --prefix-length=24 \
      --description="Google Cloud Managed Notebooks Range 24 c" \
      --network=$NETWORK \
      --addresses=192.168.0.0 \
      --purpose=VPC_PEERING

Field value will be: `managed-notebooks-range-c`

`boot_image`

`  BootImage  `

Optional. Boot image metadata used for runtime upgradeability.

## BootImage

This type has no fields.

Definition of the boot image used by the Runtime. Used to facilitate runtime upgradeability.

## NicType

The type of vNIC driver. Default should be UNSPECIFIED\_NIC\_TYPE.

Enums

`UNSPECIFIED_NIC_TYPE`

No type specified.

`VIRTIO_NET`

VIRTIO

`GVNIC`

GVNIC

## VmImage

Definition of a custom Compute Engine virtual machine image for starting a notebook instance with the environment installed directly on the VM.

Fields

`project`

`string`

Required. The name of the Google Cloud project that this VM image belongs to. Format: `{project_id}`

Union field `image` . The reference to an external Compute Engine VM image. `image` can be only one of the following:

`image_name`

`string`

Use VM image name to find the image.

`image_family`

`string`

Use this VM image family to find the image; the newest image in this family will be used.
