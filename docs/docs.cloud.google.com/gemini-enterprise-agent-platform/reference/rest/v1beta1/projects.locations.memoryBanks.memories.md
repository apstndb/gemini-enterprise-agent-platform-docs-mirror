---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.memoryBanks.memories
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.memoryBanks.memories
title: 'REST Resource: projects.locations.memoryBanks.memories'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

## Resource: Memory

A memory.

Fields

`name` `string`

Identifier. Represents the resource name of the Memory. Format: `projects/{project}/locations/{location}/reasoningEngines/{reasoningEngine}/memories/{memory}`

`displayName` `string`

Optional. Represents the display name of the Memory.

`description` `string`

Optional. Represents the description of the Memory.

`createTime` ` string ( Timestamp  ` format)

Output only. Represents the timestamp when this Memory was created.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`updateTime` ` string ( Timestamp  ` format)

Output only. Represents the timestamp when this Memory was most recently updated.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`fact` `string`

Optional. Represents semantic knowledge extracted from the source content.

`scope` `map (key: string, value: string)`

Required. Immutable. Represents the scope of the Memory. Memories are isolated within their scope. The scope is defined when creating or generating memories. scope values cannot contain the wildcard character '\*'.

`revisionLabels` `map (key: string, value: string)`

Optional. Input only. Represents the labels to apply to the Memory Revision created as a result of this request.

`memoryType` ` enum ( MemoryType  ` )

Optional. Represents the type of the memory. If not set, the `NATURAL_LANGUAGE_COLLECTION` type is used. If `STRUCTURED_COLLECTION` or `STRUCTURED_PROFILE` is used, then `structuredData` must be provided.

`structuredContent` ` object ( StructuredContent  ` )

Optional. Represents the structured content of the memory.

`expiration` `Union type`

The expiration of the Memory. If not set, the Memory will not be automatically deleted. `expiration` can be only one of the following:

`expireTime` ` string ( Timestamp  ` format)

Optional. Represents the timestamp of when this resource is considered expired. This is *always* provided on output when `expiration` is set on input, regardless of whether `expireTime` or `ttl` was provided.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`ttl` ` string ( Duration  ` format)

Optional. Input only. Represents the TTL for this resource. The expiration time is computed: now + TTL.

A duration in seconds with up to nine fractional digits, ending with ' `s` '. Example: `"3.5s"` .

`revision_expiration` `Union type`

(Input-only) The expiration of the Memory Revision created as a result of this request. If not set, Memory Bank will defer to `MemoryBankConfig.memory_revision_default_ttl` or the global default, 365 days. `revision_expiration` can be only one of the following:

`revisionExpireTime` ` string ( Timestamp  ` format)

Optional. Input only. Represents the timestamp of when the revision is considered expired. If not set, the memory revision will be kept until manually deleted.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`revisionTtl` ` string ( Duration  ` format)

Optional. Input only. Represents the TTL for the revision. The expiration time is computed: now + TTL.

A duration in seconds with up to nine fractional digits, ending with ' `s` '. Example: `"3.5s"` .

`disableMemoryRevisions` `boolean`

Optional. Input only. Indicates whether no revision will be created for this request.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;name&quot;: string,&quot;displayName&quot;: string,&quot;description&quot;: string,&quot;createTime&quot;: string,&quot;updateTime&quot;: string,&quot;fact&quot;: string,&quot;scope&quot;: {string: string,...},&quot;revisionLabels&quot;: {string: string,...},&quot;memoryType&quot;: enum (MemoryType),&quot;structuredContent&quot;: {object (StructuredContent)},// expiration&quot;expireTime&quot;: string,&quot;ttl&quot;: string// Union type// revision_expiration&quot;revisionExpireTime&quot;: string,&quot;revisionTtl&quot;: string,&quot;disableMemoryRevisions&quot;: boolean// Union type}</code></pre></td>
</tr>
</tbody>
</table>

### StructuredContent

Represents the structured value of the memory.

Fields

`data` ` object ( Struct  ` format)

Required. Represents the structured value of the memory.

`schemaId` `string`

Required. Represents the schema id for which this structured memory belongs to.

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
  &quot;data&quot;: {
    object
  },
  &quot;schemaId&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

## Methods

### `            create           `

Create a Memory.

### `            delete           `

Delete a Memory.

### `            generate           `

Generate memories.

### `            get           `

Get a Memory.

### `            list           `

List Memories.

### `            patch           `

Update a Memory.

### `            retrieve           `

Retrieve memories.
