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

` isDefault (deprecated)  ` `boolean`

> This item is deprecated\!

Output only. Deprecated: This field has no behavior. Use notebookRuntimeType = 'ONE\_CLICK' instead.

The default template to use if not specified.

`machineSpec` `object ( MachineSpec` )

Optional. Immutable. The specification of a single machine for the template.

`dataPersistentDiskSpec` ` object ( PersistentDiskSpec  ` )

Optional. The specification of \[persistent disk\]\[https://cloud.google.com/compute/docs/disks/persistent-disks\] attached to the runtime as data disk storage.

`networkSpec` ` object ( NetworkSpec  ` )

Optional. Network spec.

` serviceAccount (deprecated)  ` `string`

> This item is deprecated\!

Deprecated: This field is ignored and the "Agent Platform Notebook service Account" ( <service-PROJECT_NUMBER@gcp-sa-aiplatform-vm.iam.gserviceaccount.com> ) is used for the runtime workload identity. See <https://cloud.google.com/iam/docs/service-agents#vertex-ai-notebook-service-account> for more details. For NotebookExecutionJob, use NotebookExecutionJob.service\_account instead.

The service account that the runtime workload runs as. You can use any service account within the same project, but you must have the service account user permission to use the instance.

If not specified, the [Compute Engine default service account](https://cloud.google.com/compute/docs/access/service-accounts#default_service_account) is used.

`etag` `string`

Used to perform consistent read-modify-write updates. If not set, a blind "overwrite" update happens.

`labels` `map (key: string, value: string)`

The labels with user-defined metadata to organize the NotebookRuntimeTemplates.

label keys and values can be no longer than 64 characters (Unicode codepoints), can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed.

See <https://goo.gl/xmQnxf> for more information and examples of labels.

`idleShutdownConfig` ` object ( NotebookIdleShutdownConfig  ` )

The idle shutdown configuration of NotebookRuntimeTemplate. This config will only be set when idle shutdown is enabled.

`eucConfig` ` object ( NotebookEucConfig  ` )

EUC configuration of the NotebookRuntimeTemplate.

`createTime` ` string ( Timestamp  ` format)

Output only. timestamp when this NotebookRuntimeTemplate was created.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`updateTime` ` string ( Timestamp  ` format)

Output only. timestamp when this NotebookRuntimeTemplate was most recently updated.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`notebookRuntimeType` ` enum ( NotebookRuntimeType  ` )

Optional. Immutable. The type of the notebook runtime template.

`shieldedVmConfig` ` object ( ShieldedVmConfig  ` )

Optional. Immutable. Runtime Shielded VM spec.

`networkTags[]` `string`

Optional. The Compute Engine tags to add to runtime (see [Tagging instances](https://cloud.google.com/vpc/docs/add-remove-network-tags) ).

`encryptionSpec` ` object ( EncryptionSpec  ` )

Customer-managed encryption key spec for the notebook runtime.

`softwareConfig` ` object ( NotebookSoftwareConfig  ` )

Optional. The notebook software configuration of the notebook runtime.

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

## Methods

### `            create           `

Creates a NotebookRuntimeTemplate.

### `            delete           `

Deletes a NotebookRuntimeTemplate.

### `            get           `

Gets a NotebookRuntimeTemplate.

### `            getIamPolicy           `

Gets the access control policy for a resource.

### `            list           `

Lists NotebookRuntimeTemplates in a Location.

### `            patch           `

Updates a NotebookRuntimeTemplate.

### `            setIamPolicy           `

Sets the access control policy on the specified resource.

### `            testIamPermissions           `

Returns permissions that a caller has on the specified resource.
