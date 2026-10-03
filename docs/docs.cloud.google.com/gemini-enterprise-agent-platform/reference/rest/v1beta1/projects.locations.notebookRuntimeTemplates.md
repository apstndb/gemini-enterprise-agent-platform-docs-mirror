---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.notebookRuntimeTemplates
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.notebookRuntimeTemplates
title: 'REST Resource: projects.locations.notebookRuntimeTemplates'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

## Resource: NotebookRuntimeTemplate

A template that specifies runtime configurations such as machine type, runtime version, network configurations, etc. Multiple runtimes can be created from a runtime template.

Fields

`name` `string`

The resource name of the NotebookRuntimeTemplate.

`displayName` `string`

Required. The display name of the NotebookRuntimeTemplate. The name can be up to 128 characters long and can consist of any UTF-8 characters.

`description` `string`

The description of the NotebookRuntimeTemplate.

`isDefault `**`(deprecated)`** `boolean`

> This item is deprecated!

Output only. Deprecated: This field has no behavior. Use notebookRuntimeType = 'ONE_CLICK' instead.

The default template to use if not specified.

`machineSpec` `object ( ``MachineSpec`` )`

Optional. Immutable. The specification of a single machine for the template.

`dataPersistentDiskSpec` `object ( `[`PersistentDiskSpec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/PersistentDiskSpec)` )`

Optional. The specification of \[persistent disk\]\[https://cloud.google.com/compute/docs/disks/persistent-disks\] attached to the runtime as data disk storage.

`networkSpec` `object ( `[`NetworkSpec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/NetworkSpec)` )`

Optional. Network spec.

`serviceAccount `**`(deprecated)`** `string`

> This item is deprecated!

Deprecated: This field is ignored and the "Agent Platform Notebook service Account" ( <service-PROJECT_NUMBER@gcp-sa-aiplatform-vm.iam.gserviceaccount.com> ) is used for the runtime workload identity. See <https://cloud.google.com/iam/docs/service-agents#vertex-ai-notebook-service-account> for more details. For NotebookExecutionJob, use NotebookExecutionJob.service_account instead.

The service account that the runtime workload runs as. You can use any service account within the same project, but you must have the service account user permission to use the instance.

If not specified, the [Compute Engine default service account](https://cloud.google.com/compute/docs/access/service-accounts#default_service_account) is used.

`etag` `string`

Used to perform consistent read-modify-write updates. If not set, a blind "overwrite" update happens.

`labels` `map (key: string, value: string)`

The labels with user-defined metadata to organize the NotebookRuntimeTemplates.

label keys and values can be no longer than 64 characters (Unicode codepoints), can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed.

See <https://goo.gl/xmQnxf> for more information and examples of labels.

`idleShutdownConfig` `object ( `[`NotebookIdleShutdownConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/NotebookIdleShutdownConfig)` )`

The idle shutdown configuration of NotebookRuntimeTemplate. This config will only be set when idle shutdown is enabled.

`eucConfig` `object ( `[`NotebookEucConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/NotebookEucConfig)` )`

EUC configuration of the NotebookRuntimeTemplate.

`createTime` `string ( `[`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp)` format)`

Output only. timestamp when this NotebookRuntimeTemplate was created.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`updateTime` `string ( `[`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp)` format)`

Output only. timestamp when this NotebookRuntimeTemplate was most recently updated.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`notebookRuntimeType` `enum ( `[`NotebookRuntimeType`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/NotebookRuntimeType)` )`

Optional. Immutable. The type of the notebook runtime template.

`shieldedVmConfig` `object ( `[`ShieldedVmConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/ShieldedVmConfig)` )`

Optional. Immutable. Runtime Shielded VM spec.

`networkTags[]` `string`

Optional. The Compute Engine tags to add to runtime (see [Tagging instances](https://cloud.google.com/vpc/docs/add-remove-network-tags) ).

`encryptionSpec` `object ( `[`EncryptionSpec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/EncryptionSpec)` )`

Customer-managed encryption key spec for the notebook runtime.

`softwareConfig` `object ( `[`NotebookSoftwareConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/NotebookSoftwareConfig)` )`

Optional. The notebook software configuration of the notebook runtime.

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

| Methods                                                                                                                                                                      |                                                                  |
|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------|
| [`create`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.notebookRuntimeTemplates/create)                         | Creates a NotebookRuntimeTemplate.                               |
| [`delete`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.notebookRuntimeTemplates/delete)                         | Deletes a NotebookRuntimeTemplate.                               |
| [`get`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.notebookRuntimeTemplates/get)                               | Gets a NotebookRuntimeTemplate.                                  |
| [`getIamPolicy`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.notebookRuntimeTemplates/getIamPolicy)             | Gets the access control policy for a resource.                   |
| [`list`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.notebookRuntimeTemplates/list)                             | Lists NotebookRuntimeTemplates in a Location.                    |
| [`patch`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.notebookRuntimeTemplates/patch)                           | Updates a NotebookRuntimeTemplate.                               |
| [`setIamPolicy`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.notebookRuntimeTemplates/setIamPolicy)             | Sets the access control policy on the specified resource.        |
| [`testIamPermissions`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.notebookRuntimeTemplates/testIamPermissions) | Returns permissions that a caller has on the specified resource. |
