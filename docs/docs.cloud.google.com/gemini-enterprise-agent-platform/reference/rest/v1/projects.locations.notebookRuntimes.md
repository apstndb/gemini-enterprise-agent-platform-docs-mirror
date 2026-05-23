---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.notebookRuntimes
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.notebookRuntimes
title: 'REST Resource: projects.locations.notebookRuntimes'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

## Resource: NotebookRuntime

A runtime is a virtual machine allocated to a particular user for a particular Notebook file on temporary basis with lifetime. Default runtimes have a lifetime of 18 hours, while custom runtimes last for 6 months from their creation or last upgrade.

Fields

`name` `string`

Output only. The resource name of the NotebookRuntime.

`runtimeUser` `string`

Required. The user email of the NotebookRuntime.

`notebookRuntimeTemplateRef` ` object ( NotebookRuntimeTemplateRef  ` )

Output only. The pointer to NotebookRuntimeTemplate this NotebookRuntime is created from.

`proxyUri` `string`

Output only. The proxy endpoint used to access the NotebookRuntime.

`createTime` ` string ( Timestamp  ` format)

Output only. timestamp when this NotebookRuntime was created.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`updateTime` ` string ( Timestamp  ` format)

Output only. timestamp when this NotebookRuntime was most recently updated.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`healthState` ` enum ( HealthState  ` )

Output only. The health state of the NotebookRuntime.

`displayName` `string`

Required. The display name of the NotebookRuntime. The name can be up to 128 characters long and can consist of any UTF-8 characters.

`description` `string`

The description of the NotebookRuntime.

`serviceAccount` `string`

Output only. Deprecated: This field is no longer used and the "Agent Platform Notebook service Account" ( <service-PROJECT_NUMBER@gcp-sa-aiplatform-vm.iam.gserviceaccount.com> ) is used for the runtime workload identity. See <https://cloud.google.com/iam/docs/service-agents#vertex-ai-notebook-service-account> for more details.

The service account that the NotebookRuntime workload runs as.

`runtimeState` ` enum ( RuntimeState  ` )

Output only. The runtime (instance) state of the NotebookRuntime.

`isUpgradable` `boolean`

Output only. Whether NotebookRuntime is upgradable.

`labels` `map (key: string, value: string)`

The labels with user-defined metadata to organize your NotebookRuntime.

label keys and values can be no longer than 64 characters (Unicode codepoints), can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed. No more than 64 user labels can be associated with one NotebookRuntime (System labels are excluded).

See <https://goo.gl/xmQnxf> for more information and examples of labels. System reserved label keys are prefixed with "aiplatform.googleapis.com/" and are immutable. Following system labels exist for NotebookRuntime:

  - "aiplatform.googleapis.com/notebook\_runtime\_gce\_instance\_id": output only, its value is the Compute Engine instance id.
  - "aiplatform.googleapis.com/colab\_enterprise\_entry\_service": its value is either "bigquery" or "vertex"; if absent, it should be "vertex". This is to describe the entry service, either BigQuery or Vertex.

`expirationTime` ` string ( Timestamp  ` format)

Output only. timestamp when this NotebookRuntime will be expired: 1. System Predefined NotebookRuntime: 24 hours after creation. After expiration, system predifined runtime will be deleted. 2. user created NotebookRuntime: 6 months after last upgrade. After expiration, user created runtime will be stopped and allowed for upgrade.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`version` `string`

Output only. The VM os image version of NotebookRuntime.

`notebookRuntimeType` ` enum ( NotebookRuntimeType  ` )

Output only. The type of the notebook runtime.

`machineSpec` ` object ( MachineSpec  ` )

Output only. The specification of a single machine used by the notebook runtime.

`dataPersistentDiskSpec` ` object ( PersistentDiskSpec  ` )

Output only. The specification of \[persistent disk\]\[https://cloud.google.com/compute/docs/disks/persistent-disks\] attached to the notebook runtime as data disk storage.

`networkSpec` ` object ( NetworkSpec  ` )

Output only. Network spec of the notebook runtime.

`idleShutdownConfig` ` object ( NotebookIdleShutdownConfig  ` )

Output only. The idle shutdown configuration of the notebook runtime.

`eucConfig` ` object ( NotebookEucConfig  ` )

Output only. EUC configuration of the notebook runtime.

`shieldedVmConfig` ` object ( ShieldedVmConfig  ` )

Output only. Runtime Shielded VM spec.

`networkTags[]` `string`

Optional. The Compute Engine tags to add to runtime (see [Tagging instances](https://cloud.google.com/vpc/docs/add-remove-network-tags) ).

`softwareConfig` ` object ( NotebookSoftwareConfig  ` )

Output only. Software config of the notebook runtime.

`encryptionSpec` ` object ( EncryptionSpec  ` )

Output only. Customer-managed encryption key spec for the notebook runtime.

`satisfiesPzs` `boolean`

Output only. reserved for future use.

`satisfiesPzi` `boolean`

Output only. reserved for future use.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;name&quot;: string,&quot;runtimeUser&quot;: string,&quot;notebookRuntimeTemplateRef&quot;: {object (NotebookRuntimeTemplateRef)},&quot;proxyUri&quot;: string,&quot;createTime&quot;: string,&quot;updateTime&quot;: string,&quot;healthState&quot;: enum (HealthState),&quot;displayName&quot;: string,&quot;description&quot;: string,&quot;serviceAccount&quot;: string,&quot;runtimeState&quot;: enum (RuntimeState),&quot;isUpgradable&quot;: boolean,&quot;labels&quot;: {string: string,...},&quot;expirationTime&quot;: string,&quot;version&quot;: string,&quot;notebookRuntimeType&quot;: enum (NotebookRuntimeType),&quot;machineSpec&quot;: {object (MachineSpec)},&quot;dataPersistentDiskSpec&quot;: {object (PersistentDiskSpec)},&quot;networkSpec&quot;: {object (NetworkSpec)},&quot;idleShutdownConfig&quot;: {object (NotebookIdleShutdownConfig)},&quot;eucConfig&quot;: {object (NotebookEucConfig)},&quot;shieldedVmConfig&quot;: {object (ShieldedVmConfig)},&quot;networkTags&quot;: [string],&quot;softwareConfig&quot;: {object (NotebookSoftwareConfig)},&quot;encryptionSpec&quot;: {object (EncryptionSpec)},&quot;satisfiesPzs&quot;: boolean,&quot;satisfiesPzi&quot;: boolean}</code></pre></td>
</tr>
</tbody>
</table>

## NotebookRuntimeTemplateRef

Points to a NotebookRuntimeTemplateRef.

Fields

`notebookRuntimeTemplate` `string`

Immutable. A resource name of the NotebookRuntimeTemplate.

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
  &quot;notebookRuntimeTemplate&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

## HealthState

The substate of the NotebookRuntime to display health information.

Enums

`HEALTH_STATE_UNSPECIFIED`

Unspecified health state.

`HEALTHY`

NotebookRuntime is in healthy state. Applies to ACTIVE state.

`UNHEALTHY`

NotebookRuntime is in unhealthy state. Applies to ACTIVE state.

## RuntimeState

The substate of the NotebookRuntime to display state of runtime. The resource of NotebookRuntime is in ACTIVE state for these sub state.

Enums

`RUNTIME_STATE_UNSPECIFIED`

Unspecified runtime state.

`RUNNING`

NotebookRuntime is in running state.

`BEING_STARTED`

NotebookRuntime is in starting state. This is when the runtime is being started from a stopped state.

`BEING_STOPPED`

NotebookRuntime is in stopping state.

`STOPPED`

NotebookRuntime is in stopped state.

`BEING_UPGRADED`

NotebookRuntime is in upgrading state. It is in the middle of upgrading process.

`ERROR`

NotebookRuntime was unable to start/stop properly.

`INVALID`

NotebookRuntime is in invalid state. Cannot be recovered.

## Methods

### `            assign           `

Assigns a NotebookRuntime to a user for a particular Notebook file.

### `            delete           `

Deletes a NotebookRuntime.

### `            get           `

Gets a NotebookRuntime.

### `            list           `

Lists NotebookRuntimes in a Location.

### `            start           `

Starts a NotebookRuntime.

### `            stop           `

Stops a NotebookRuntime.

### `            upgrade           `

Upgrades a NotebookRuntime.
