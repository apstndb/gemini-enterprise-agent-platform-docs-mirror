---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.reasoningEngines.sandboxEnvironmentSnapshots
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.reasoningEngines.sandboxEnvironmentSnapshots
title: 'REST Resource: projects.locations.reasoningEngines.sandboxEnvironmentSnapshots'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

## Resource: SandboxEnvironmentSnapshot

SandboxEnvironmentSnapshot is a snapshot of the SandboxEnvironment.

Fields

`name` `string`

Identifier. The resource name of the SandboxEnvironmentSnapshot. Format: `projects/{project}/locations/{location}/reasoningEngines/{reasoningEngine}/sandboxEnvironmentSnapshots/{sandboxEnvironmentSnapshot}`

`displayName` `string`

Required. The display name of the SandboxEnvironmentSnapshot.

`createTime` ` string ( Timestamp  ` format)

Output only. The timestamp when this SandboxEnvironmentSnapshot was created.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`updateTime` ` string ( Timestamp  ` format)

Output only. The timestamp when this SandboxEnvironment was most recently updated.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`sourceSandboxEnvironment` `string`

Required. The resource name of the source SandboxEnvironment this snapshot was taken from.

`parentSnapshot` `string`

Output only. The resource name of the parent SandboxEnvironmentSnapshot. Empty if this is a root Snapshot (the first snapshot from a newly created sandbox). Can be used to reconstruct the whole ancestry tree of snapshots.

`sizeBytes` `string ( int64 format)`

Optional. Output only. Size of the snapshot data in bytes.

`owner` `string`

Optional. owner information for this sandbox snapshot. Different owners will have isolations on snapshot storage and identity. If not set, snapshot will be created as the default owner.

`postSnapshotAction` ` enum ( PostSnapshotAction  ` )

Optional. Input only. Action to take on the source SandboxEnvironment after the snapshot is taken. This field is only used in CreateSandboxEnvironmentSnapshotRequest and it is not stored in the resource.

`expiration` `Union type`

The expiration of the SandboxEnvironmentSnapshot. If not set, the SandboxEnvironmentSnapshot will have a default TTL of 30 days. `expire_time` is recommended for specifying a precise expiration time. `expiration` can be only one of the following:

`expireTime` ` string ( Timestamp  ` format)

Optional. timestamp in UTC of when this SandboxEnvironmentSnapshot is considered expired. This is *always* provided on output, regardless of what `expiration` was sent on input.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`ttl` ` string ( Duration  ` format)

Optional. Input only. The TTL for the sandbox environment snapshot. The expiration time is computed: now + TTL.

A duration in seconds with up to nine fractional digits, ending with ' `s` '. Example: `"3.5s"` .

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;name&quot;: string,&quot;displayName&quot;: string,&quot;createTime&quot;: string,&quot;updateTime&quot;: string,&quot;sourceSandboxEnvironment&quot;: string,&quot;parentSnapshot&quot;: string,&quot;sizeBytes&quot;: string,&quot;owner&quot;: string,&quot;postSnapshotAction&quot;: enum (PostSnapshotAction),// expiration&quot;expireTime&quot;: string,&quot;ttl&quot;: string// Union type}</code></pre></td>
</tr>
</tbody>
</table>

## PostSnapshotAction

Action to take on the source SandboxEnvironment after the snapshot is taken.

Enums

`POST_SNAPSHOT_ACTION_UNSPECIFIED`

The default value. This value is unused.

`RUNNING`

Sandbox environment will continue to run after snapshot is taken.

`PAUSE`

Sandbox environment will be paused after snapshot is taken.

## Methods

### `            delete           `

Deletes the specific `  SandboxEnvironmentSnapshot  ` .

### `            get           `

Gets details of the specific `  SandboxEnvironmentSnapshot  ` .

### `            list           `

Lists `  SandboxEnvironmentSnapshot  ` s in a given reasoning engine.
