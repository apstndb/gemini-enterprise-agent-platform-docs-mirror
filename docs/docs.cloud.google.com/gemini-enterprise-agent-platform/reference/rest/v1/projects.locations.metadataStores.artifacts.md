---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.metadataStores.artifacts
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.metadataStores.artifacts
title: 'REST Resource: projects.locations.metadataStores.artifacts'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

## Resource: Artifact

Instance of a general artifact.

Fields

`name` `string`

Output only. The resource name of the Artifact.

`displayName` `string`

user provided display name of the Artifact. May be up to 128 Unicode characters.

`uri` `string`

The uniform resource identifier of the artifact file. May be empty if there is no actual artifact file.

`etag` `string`

An eTag used to perform consistent read-modify-write updates. If not set, a blind "overwrite" update happens.

`labels` `map (key: string, value: string)`

The labels with user-defined metadata to organize your Artifacts.

label keys and values can be no longer than 64 characters (Unicode codepoints), can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed. No more than 64 user labels can be associated with one Artifact (System labels are excluded).

`createTime` ` string ( Timestamp  ` format)

Output only. timestamp when this Artifact was created.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`updateTime` ` string ( Timestamp  ` format)

Output only. timestamp when this Artifact was last updated.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`state` ` enum ( State  ` )

The state of this Artifact. This is a property of the Artifact, and does not imply or capture any ongoing process. This property is managed by clients (such as Agent Platform Pipelines), and the system does not prescribe or check the validity of state transitions.

`schemaTitle` `string`

The title of the schema describing the metadata.

Schema title and version is expected to be registered in earlier Create Schema calls. And both are used together as unique identifiers to identify schemas within the local metadata store.

`schemaVersion` `string`

The version of the schema in schemaName to use.

Schema title and version is expected to be registered in earlier Create Schema calls. And both are used together as unique identifiers to identify schemas within the local metadata store.

`metadata` ` object ( Struct  ` format)

Properties of the Artifact. top level metadata keys' heading and trailing spaces will be trimmed. The size of this field should not exceed 200KB.

`description` `string`

description of the Artifact

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;name&quot;: string,&quot;displayName&quot;: string,&quot;uri&quot;: string,&quot;etag&quot;: string,&quot;labels&quot;: {string: string,...},&quot;createTime&quot;: string,&quot;updateTime&quot;: string,&quot;state&quot;: enum (State),&quot;schemaTitle&quot;: string,&quot;schemaVersion&quot;: string,&quot;metadata&quot;: {object},&quot;description&quot;: string}</code></pre></td>
</tr>
</tbody>
</table>

### State

Describes the state of the Artifact.

Enums

`STATE_UNSPECIFIED`

Unspecified state for the Artifact.

`PENDING`

A state used by systems like Agent Platform Pipelines to indicate that the underlying data item represented by this Artifact is being created.

`LIVE`

A state indicating that the Artifact should exist, unless something external to the system deletes it.

## Methods

### `            create           `

Creates an Artifact associated with a MetadataStore.

### `            delete           `

Deletes an Artifact.

### `            get           `

Retrieves a specific Artifact.

### `            list           `

Lists Artifacts in the MetadataStore.

### `            patch           `

Updates a stored Artifact.

### `            purge           `

Purges Artifacts.

### `            queryArtifactLineageSubgraph           `

Retrieves lineage of an Artifact represented through Artifacts and Executions connected by Event edges and returned as a LineageSubgraph.
