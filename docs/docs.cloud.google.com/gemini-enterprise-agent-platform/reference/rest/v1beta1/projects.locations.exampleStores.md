---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.exampleStores
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.exampleStores
title: 'REST Resource: projects.locations.exampleStores'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

## Resource: ExampleStore

Represents an executable service to manage and retrieve examples.

Fields

`name` `string`

Identifier. The resource name of the ExampleStore. This is a unique identifier. Format: projects/{project}/locations/{location}/exampleStores/{exampleStore}

`displayName` `string`

Required. Display name of the ExampleStore.

`description` `string`

Optional. description of the ExampleStore.

`createTime` `string ( `[`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp)` format)`

Output only. timestamp when this ExampleStore was created.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`updateTime` `string ( `[`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp)` format)`

Output only. timestamp when this ExampleStore was most recently updated.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`exampleStoreConfig` `object ( `[`ExampleStoreConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.exampleStores#ExampleStoreConfig)` )`

Required. Example Store config.

**JSON representation**

```
{
  "name": string,
  "displayName": string,
  "description": string,
  "createTime": string,
  "updateTime": string,
  "exampleStoreConfig": {
    object (ExampleStoreConfig)
  }
}
```

## ExampleStoreConfig

Configuration for the Example Store.

Fields

`vertexEmbeddingModel` `string`

Required. The embedding model to be used for vector embedding. Immutable. Supported models: \* "text-embedding-005" \* "text-multilingual-embedding-002"

**JSON representation**

```
{
  "vertexEmbeddingModel": string
}
```

| Methods                                                                                                                                                   |                                                           |
|-----------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------|
| [`create`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.exampleStores/create)                 | Create an ExampleStore.                                   |
| [`delete`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.exampleStores/delete)                 | Delete an ExampleStore.                                   |
| [`fetchExamples`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.exampleStores/fetchExamples)   | Get Examples from the Example Store.                      |
| [`get`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.exampleStores/get)                       | Get an ExampleStore.                                      |
| [`list`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.exampleStores/list)                     | List ExampleStores in a Location.                         |
| [`patch`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.exampleStores/patch)                   | Update an ExampleStore.                                   |
| [`removeExamples`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.exampleStores/removeExamples) | Remove Examples from the Example Store.                   |
| [`searchExamples`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.exampleStores/searchExamples) | Search for similar Examples for given selection criteria. |
| [`upsertExamples`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.exampleStores/upsertExamples) | Create or update Examples in the Example Store.           |
