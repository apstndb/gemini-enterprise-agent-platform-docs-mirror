---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/rest/v1/projects.locations.collections.dataObjects
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/rest/v1/projects.locations.collections.dataObjects
title: 'REST Resource: projects.locations.collections.dataObjects'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

## Resource: DataObject

A dataObject resource in Vector Search.

**JSON representation**

```
{
  "name": string,
  "dataObjectId": string,
  "createTime": string,
  "updateTime": string,
  "data": {
    object
  },
  "vectors": {
    string: {
      object (Vector)
    },
    ...
  },
  "etag": string
}
```

| Fields         |                                                                                                                                                                                                                                                                                                                                                                                                                               |
|----------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `name`         | `string` Identifier. The fully qualified resource name of the dataObject. Format: `projects/{project}/locations/{location}/collections/{collection}/dataObjects/{dataObjectId}` The dataObjectId must be 1-63 characters long, and comply with [RFC1035](https://www.ietf.org/rfc/rfc1035.txt) .                                                                                                                              |
| `dataObjectId` | `string` Output only. The id of the dataObject.                                                                                                                                                                                                                                                                                                                                                                               |
| `createTime`   | `string ( `[`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp)` format)` Output only. Timestamp the dataObject was created at. Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .   |
| `updateTime`   | `string ( `[`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp)` format)` Output only. Timestamp the dataObject was last updated. Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` . |
| `data`         | `object ( `[`Struct`](https://protobuf.dev/reference/protobuf/google.protobuf/#struct)` format)` Optional. The data of the dataObject.                                                                                                                                                                                                                                                                                        |
| `vectors`      | `map (key: string, value: object ( `[`Vector`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/rest/v1/projects.locations.collections.dataObjects#Vector)` ))` Optional. The vectors of the dataObject. An object containing a list of `"key": value` pairs. Example: `{ "name": "wrench", "mass": "1.3kg", "count": "3" }` .                                                  |
| `etag`         | `string` Optional. The etag of the dataObject.                                                                                                                                                                                                                                                                                                                                                                                |

## Vector

A vector which can be either dense or sparse.

**JSON representation**

```
{

  // Union field vector_type can be only one of the following:
  "dense": {
    object (DenseVector)
  },
  "sparse": {
    object (SparseVector)
  }
  // End of list of possible types for union field vector_type.
}
```

| Fields                                                                                              |                                                                                                                                                                                                                  |
|-----------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Union field `vector_type` . The type of the vector. `vector_type` can be only one of the following: |                                                                                                                                                                                                                  |
| `dense`                                                                                             | `object ( `[`DenseVector`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/rest/v1/projects.locations.collections.dataObjects#DenseVector)` )` A dense vector.    |
| `sparse`                                                                                            | `object ( `[`SparseVector`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/rest/v1/projects.locations.collections.dataObjects#SparseVector)` )` A sparse vector. |

## DenseVector

A dense vector.

**JSON representation**

```
{
  "values": [
    number
  ]
}
```

| Fields     |                                              |
|------------|----------------------------------------------|
| `values[]` | `number` Required. The values of the vector. |

## SparseVector

A sparse vector.

**JSON representation**

```
{
  "values": [
    number
  ],
  "indices": [
    integer
  ]
}
```

| Fields      |                                                               |
|-------------|---------------------------------------------------------------|
| `values[]`  | `number` Required. The values of the vector.                  |
| `indices[]` | `integer` Required. The corresponding indices for the values. |

| Methods                                                                                                                                                                        |                                 |
|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------------------------|
| [`aggregate`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/rest/v1/projects.locations.collections.dataObjects/aggregate)     | Aggregates data objects.        |
| [`batchCreate`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/rest/v1/projects.locations.collections.dataObjects/batchCreate) | Creates a batch of dataObjects. |
| [`batchDelete`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/rest/v1/projects.locations.collections.dataObjects/batchDelete) | Deletes dataObjects in a batch. |
| [`batchSearch`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/rest/v1/projects.locations.collections.dataObjects/batchSearch) | Batch searches data objects.    |
| [`batchUpdate`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/rest/v1/projects.locations.collections.dataObjects/batchUpdate) | Updates dataObjects in a batch. |
| [`create`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/rest/v1/projects.locations.collections.dataObjects/create)           | Creates a dataObject.           |
| [`delete`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/rest/v1/projects.locations.collections.dataObjects/delete)           | Deletes a dataObject.           |
| [`get`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/rest/v1/projects.locations.collections.dataObjects/get)                 | Gets a data object.             |
| [`patch`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/rest/v1/projects.locations.collections.dataObjects/patch)             | Updates a dataObject.           |
| [`query`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/rest/v1/projects.locations.collections.dataObjects/query)             | Queries data objects.           |
| [`search`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/rest/v1/projects.locations.collections.dataObjects/search)           | Searches data objects.          |
