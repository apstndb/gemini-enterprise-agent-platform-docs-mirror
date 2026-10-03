---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.reasoningEngines.memories
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.reasoningEngines.memories
title: 'REST Resource: projects.locations.reasoningEngines.memories'
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

`createTime` `string ( `[`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp)` format)`

Output only. Represents the timestamp when this Memory was created.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`updateTime` `string ( `[`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp)` format)`

Output only. Represents the timestamp when this Memory was most recently updated.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`fact` `string`

Optional. Represents semantic knowledge extracted from the source content.

`scope` `map (key: string, value: string)`

Required. Immutable. Represents the scope of the Memory. Memories are isolated within their scope. The scope is defined when creating or generating memories. scope values cannot contain the wildcard character '\*'.

`revisionLabels` `map (key: string, value: string)`

Optional. Input only. Represents the labels to apply to the Memory Revision created as a result of this request.

`memoryType` `enum ( `[`MemoryType`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/MemoryType)` )`

Optional. Represents the type of the memory. If not set, the `NATURAL_LANGUAGE_COLLECTION` type is used. If `STRUCTURED_COLLECTION` or `STRUCTURED_PROFILE` is used, then `structuredData` must be provided.

`structuredContent` `object ( `[`StructuredContent`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.memoryBanks.memories#Memory.StructuredContent)` )`

Optional. Represents the structured content of the memory.

`expiration` `Union type`

The expiration of the Memory. If not set, the Memory will not be automatically deleted. The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:

`expireTime` `string ( `[`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp)` format)`

Optional. Represents the timestamp of when this resource is considered expired. This is *always* provided on output when `expiration` is set on input, regardless of whether `expireTime` or `ttl` was provided.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`ttl` `string ( `[`Duration`](https://protobuf.dev/reference/protobuf/google.protobuf/#duration)` format)`

Optional. Input only. Represents the TTL for this resource. The expiration time is computed: now + TTL.

A duration in seconds with up to nine fractional digits, ending with ' `s` '. Example: `"3.5s"` .

End of mutually exclusive fields.

`revision_expiration` `Union type`

(Input-only) The expiration of the Memory Revision created as a result of this request. If not set, Memory Bank will defer to `MemoryBankConfig.memory_revision_default_ttl` or the global default, 365 days. The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:

`revisionExpireTime` `string ( `[`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp)` format)`

Optional. Input only. Represents the timestamp of when the revision is considered expired. If not set, the memory revision will be kept until manually deleted.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`revisionTtl` `string ( `[`Duration`](https://protobuf.dev/reference/protobuf/google.protobuf/#duration)` format)`

Optional. Input only. Represents the TTL for the revision. The expiration time is computed: now + TTL.

A duration in seconds with up to nine fractional digits, ending with ' `s` '. Example: `"3.5s"` .

`disableMemoryRevisions` `boolean`

Optional. Input only. Indicates whether no revision will be created for this request.

End of mutually exclusive fields.

**JSON representation**

```
{
  "name": string,
  "displayName": string,
  "description": string,
  "createTime": string,
  "updateTime": string,
  "fact": string,
  "scope": {
    string: string,
    ...
  },
  "revisionLabels": {
    string: string,
    ...
  },
  "memoryType": enum (MemoryType),
  "structuredContent": {
    object (StructuredContent)
  },

  // expiration
  "expireTime": string,
  "ttl": string
  // Union type

  // revision_expiration
  "revisionExpireTime": string,
  "revisionTtl": string,
  "disableMemoryRevisions": boolean
  // Union type
}
```

| Methods                                                                                                                                                                   |                                   |
|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------|
| [`create`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.reasoningEngines.memories/create)                     | Create a Memory.                  |
| [`delete`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.reasoningEngines.memories/delete)                     | Delete a Memory.                  |
| [`generate`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.reasoningEngines.memories/generate)                 | Generate memories.                |
| [`get`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.reasoningEngines.memories/get)                           | Get a Memory.                     |
| [`ingestEvents`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.reasoningEngines.memories/ingestEvents)         | Ingests events for a Memory Bank. |
| [`list`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.reasoningEngines.memories/list)                         | List Memories.                    |
| [`patch`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.reasoningEngines.memories/patch)                       | Update a Memory.                  |
| [`retrieve`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.reasoningEngines.memories/retrieve)                 | Retrieve memories.                |
| [`retrieveProfiles`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.reasoningEngines.memories/retrieveProfiles) | Retrieves profiles.               |
