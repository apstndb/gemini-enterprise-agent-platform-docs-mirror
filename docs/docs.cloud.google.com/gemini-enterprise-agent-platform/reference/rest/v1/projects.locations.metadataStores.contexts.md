---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.metadataStores.contexts
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.metadataStores.contexts
title: 'REST Resource: projects.locations.metadataStores.contexts'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

## Resource: Context

Instance of a general context.

Fields

`name` `string`

Immutable. The resource name of the Context.

`displayName` `string`

user provided display name of the Context. May be up to 128 Unicode characters.

`etag` `string`

An eTag used to perform consistent read-modify-write updates. If not set, a blind "overwrite" update happens.

`labels` `map (key: string, value: string)`

The labels with user-defined metadata to organize your Contexts.

label keys and values can be no longer than 64 characters (Unicode codepoints), can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed. No more than 64 user labels can be associated with one Context (System labels are excluded).

`createTime` `string ( `[`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp)` format)`

Output only. timestamp when this Context was created.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`updateTime` `string ( `[`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp)` format)`

Output only. timestamp when this Context was last updated.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`parentContexts[]` `string`

Output only. A list of resource names of Contexts that are parents of this Context. A Context may have at most 10 parentContexts.

`schemaTitle` `string`

The title of the schema describing the metadata.

Schema title and version is expected to be registered in earlier Create Schema calls. And both are used together as unique identifiers to identify schemas within the local metadata store.

`schemaVersion` `string`

The version of the schema in schemaName to use.

Schema title and version is expected to be registered in earlier Create Schema calls. And both are used together as unique identifiers to identify schemas within the local metadata store.

`metadata` `object ( `[`Struct`](https://protobuf.dev/reference/protobuf/google.protobuf/#struct)` format)`

Properties of the Context. top level metadata keys' heading and trailing spaces will be trimmed. The size of this field should not exceed 200KB.

`description` `string`

description of the Context

**JSON representation**

```
{
  "name": string,
  "displayName": string,
  "etag": string,
  "labels": {
    string: string,
    ...
  },
  "createTime": string,
  "updateTime": string,
  "parentContexts": [
    string
  ],
  "schemaTitle": string,
  "schemaVersion": string,
  "metadata": {
    object
  },
  "description": string
}
```

| Methods                                                                                                                                                                                            |                                                                                                                              |
|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------|
| [`addContextArtifactsAndExecutions`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.metadataStores.contexts/addContextArtifactsAndExecutions) | Adds a set of Artifacts and Executions to a Context.                                                                         |
| [`addContextChildren`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.metadataStores.contexts/addContextChildren)                             | Adds a set of Contexts as children to a parent Context.                                                                      |
| [`create`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.metadataStores.contexts/create)                                                     | Creates a Context associated with a MetadataStore.                                                                           |
| [`delete`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.metadataStores.contexts/delete)                                                     | Deletes a stored Context.                                                                                                    |
| [`get`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.metadataStores.contexts/get)                                                           | Retrieves a specific Context.                                                                                                |
| [`list`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.metadataStores.contexts/list)                                                         | Lists Contexts on the MetadataStore.                                                                                         |
| [`patch`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.metadataStores.contexts/patch)                                                       | Updates a stored Context.                                                                                                    |
| [`purge`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.metadataStores.contexts/purge)                                                       | Purges Contexts.                                                                                                             |
| [`queryContextLineageSubgraph`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.metadataStores.contexts/queryContextLineageSubgraph)           | Retrieves Artifacts and Executions within the specified Context, connected by Event edges and returned as a LineageSubgraph. |
| [`removeContextChildren`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.metadataStores.contexts/removeContextChildren)                       | Remove a set of children contexts from a parent Context.                                                                     |
