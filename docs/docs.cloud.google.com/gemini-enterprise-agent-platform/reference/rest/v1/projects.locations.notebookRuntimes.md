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

`notebookRuntimeTemplateRef` `object ( `[`NotebookRuntimeTemplateRef`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.notebookRuntimes#NotebookRuntimeTemplateRef)` )`

Output only. The pointer to NotebookRuntimeTemplate this NotebookRuntime is created from.

`proxyUri` `string`

Output only. The proxy endpoint used to access the NotebookRuntime.

`createTime` `string ( `[`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp)` format)`

Output only. timestamp when this NotebookRuntime was created.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`updateTime` `string ( `[`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp)` format)`

Output only. timestamp when this NotebookRuntime was most recently updated.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`healthState` `enum ( `[`HealthState`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.notebookRuntimes#HealthState)` )`

Output only. The health state of the NotebookRuntime.

`displayName` `string`

Required. The display name of the NotebookRuntime. The name can be up to 128 characters long and can consist of any UTF-8 characters.

`description` `string`

The description of the NotebookRuntime.

`serviceAccount` `string`

Output only. Deprecated: This field is no longer used and the "Agent Platform Notebook service Account" ( <service-PROJECT_NUMBER@gcp-sa-aiplatform-vm.iam.gserviceaccount.com> ) is used for the runtime workload identity. See <https://cloud.google.com/iam/docs/service-agents#vertex-ai-notebook-service-account> for more details.

The service account that the NotebookRuntime workload runs as.

`runtimeState` `enum ( `[`RuntimeState`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.notebookRuntimes#RuntimeState)` )`

Output only. The runtime (instance) state of the NotebookRuntime.

`isUpgradable` `boolean`

Output only. Whether NotebookRuntime is upgradable.

`labels` `map (key: string, value: string)`

The labels with user-defined metadata to organize your NotebookRuntime.

label keys and values can be no longer than 64 characters (Unicode codepoints), can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed. No more than 64 user labels can be associated with one NotebookRuntime (System labels are excluded).

See <https://goo.gl/xmQnxf> for more information and examples of labels. System reserved label keys are prefixed with "aiplatform.googleapis.com/" and are immutable. Following system labels exist for NotebookRuntime:

- "aiplatform.googleapis.com/notebook_runtime_gce_instance_id": output only, its value is the Compute Engine instance id.
- "aiplatform.googleapis.com/colab_enterprise_entry_service": its value is either "bigquery" or "vertex"; if absent, it should be "vertex". This is to describe the entry service, either BigQuery or Vertex.

`expirationTime` `string ( `[`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp)` format)`

Output only. timestamp when this NotebookRuntime will be expired: 1. System Predefined NotebookRuntime: 24 hours after creation. After expiration, system predifined runtime will be deleted. 2. user created NotebookRuntime: 6 months after last upgrade. After expiration, user created runtime will be stopped and allowed for upgrade.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`version` `string`

Output only. The VM os image version of NotebookRuntime.

`notebookRuntimeType` `enum ( `[`NotebookRuntimeType`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/NotebookRuntimeType)` )`

Output only. The type of the notebook runtime.

`machineSpec` `object ( `[`MachineSpec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/CustomJobSpec#MachineSpec)` )`

Output only. The specification of a single machine used by the notebook runtime.

`dataPersistentDiskSpec` `object ( `[`PersistentDiskSpec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/PersistentDiskSpec)` )`

Output only. The specification of \[persistent disk\]\[https://cloud.google.com/compute/docs/disks/persistent-disks\] attached to the notebook runtime as data disk storage.

`networkSpec` `object ( `[`NetworkSpec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/NetworkSpec)` )`

Output only. Network spec of the notebook runtime.

`idleShutdownConfig` `object ( `[`NotebookIdleShutdownConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/NotebookIdleShutdownConfig)` )`

Output only. The idle shutdown configuration of the notebook runtime.

`eucConfig` `object ( `[`NotebookEucConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/NotebookEucConfig)` )`

Output only. EUC configuration of the notebook runtime.

`shieldedVmConfig` `object ( `[`ShieldedVmConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/ShieldedVmConfig)` )`

Output only. Runtime Shielded VM spec.

`networkTags[]` `string`

Optional. The Compute Engine tags to add to runtime (see [Tagging instances](https://cloud.google.com/vpc/docs/add-remove-network-tags) ).

`softwareConfig` `object ( `[`NotebookSoftwareConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/NotebookSoftwareConfig)` )`

Output only. Software config of the notebook runtime.

`encryptionSpec` `object ( `[`EncryptionSpec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/EncryptionSpec)` )`

Output only. Customer-managed encryption key spec for the notebook runtime.

`satisfiesPzs` `boolean`

Output only. reserved for future use.

`satisfiesPzi` `boolean`

Output only. reserved for future use.

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

## NotebookRuntimeTemplateRef

Points to a NotebookRuntimeTemplateRef.

Fields

`notebookRuntimeTemplate` `string`

Immutable. A resource name of the NotebookRuntimeTemplate.

**JSON representation**

```
{
  "notebookRuntimeTemplate": string
}
```

## HealthState

The substate of the NotebookRuntime to display health information.

| Enums                      |                                                                 |
|----------------------------|-----------------------------------------------------------------|
| `HEALTH_STATE_UNSPECIFIED` | Unspecified health state.                                       |
| `HEALTHY`                  | NotebookRuntime is in healthy state. Applies to ACTIVE state.   |
| `UNHEALTHY`                | NotebookRuntime is in unhealthy state. Applies to ACTIVE state. |

## RuntimeState

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

| Methods                                                                                                                                   |                                                                     |
|-------------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------|
| [`assign`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.notebookRuntimes/assign)   | Assigns a NotebookRuntime to a user for a particular Notebook file. |
| [`delete`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.notebookRuntimes/delete)   | Deletes a NotebookRuntime.                                          |
| [`get`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.notebookRuntimes/get)         | Gets a NotebookRuntime.                                             |
| [`list`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.notebookRuntimes/list)       | Lists NotebookRuntimes in a Location.                               |
| [`start`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.notebookRuntimes/start)     | Starts a NotebookRuntime.                                           |
| [`stop`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.notebookRuntimes/stop)       | Stops a NotebookRuntime.                                            |
| [`upgrade`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.notebookRuntimes/upgrade) | Upgrades a NotebookRuntime.                                         |
