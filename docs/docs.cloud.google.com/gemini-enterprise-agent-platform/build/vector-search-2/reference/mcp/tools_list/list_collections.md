---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/mcp/tools_list/list_collections
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/mcp/tools_list/list_collections
title: 'MCP Tools Reference: vectorsearch.googleapis.com'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

## Tool: `list_collections`

Lists available vector search collections in a given project and location.

The following code sample shows how to use `curl` to call the `list_collections` MCP tool.

**Curl Request**

```
curl --location 'https://vectorsearch.googleapis.com/mcp' \
--header 'content-type: application/json' \
--header 'accept: application/json, text/event-stream' \
--data '{
  "method": "tools/call",
  "params": {
    "name": "list_collections",
    "arguments": {
      // Provide these details according to the MCP tool specification.
    }
  },
  "jsonrpc": "2.0",
  "id": 1
}'
```

## Input Schema

Request for `list_collections` .

### ListCollectionsRequest

**JSON representation**

```
{
  "projectId": string,
  "location": string,
  "pageSize": integer,
  "pageToken": string,
  "filter": string,
  "orderBy": string
}
```

| Fields      |                                                                                                                                                 |
|-------------|-------------------------------------------------------------------------------------------------------------------------------------------------|
| `projectId` | `string` Required. The project ID or number.                                                                                                    |
| `location`  | `string` Required. The region to list Collections in, e.g. `us-central1` .                                                                      |
| `pageSize`  | `integer` Optional. Requested page size. Server may return fewer items than requested. If unspecified, server will pick an appropriate default. |
| `pageToken` | `string` Optional. A token identifying a page of results the server should return.                                                              |
| `filter`    | `string` Optional. Filtering results.                                                                                                           |
| `orderBy`   | `string` Optional. Hint for how to order the results.                                                                                           |

## Output Schema

Message for response to listing Collections

### ListCollectionsResponse

**JSON representation**

```
{
  "collections": [
    {
      object (Collection)
    }
  ],
  "nextPageToken": string,
  "unreachable": [
    string
  ]
}
```

| Fields          |                                                                                                                                                                                                               |
|-----------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `collections[]` | `object ( `[`Collection`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/mcp/tools_list/list_collections#Output.Schema.Collection)` )` The list of Collection |
| `nextPageToken` | `string` A token identifying a page of results the server should return.                                                                                                                                      |
| `unreachable[]` | `string` Unordered list. Locations that could not be reached.                                                                                                                                                 |

### Collection

**JSON representation**

```
{
  "name": string,
  "displayName": string,
  "description": string,
  "createTime": string,
  "updateTime": string,
  "labels": {
    string: string,
    ...
  },
  "vectorSchema": {
    string: {
      object (VectorField)
    },
    ...
  },
  "dataSchema": {
    object
  },
  "encryptionSpec": {
    object (EncryptionSpec)
  }
}
```

| Fields           |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
|------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `name`           | `string` Identifier. name of resource                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| `displayName`    | `string` Optional. User-specified display name of the collection                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| `description`    | `string` Optional. User-specified description of the collection                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| `createTime`     | `string ( `[`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp)` format)` Output only. \[Output only\] Create time stamp Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .                                                                                                |
| `updateTime`     | `string ( `[`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp)` format)` Output only. \[Output only\] Update time stamp Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .                                                                                                |
| `labels`         | `map (key: string, value: string)` Optional. Labels as key value pairs. An object containing a list of `"key": value` pairs. Example: `{ "name": "wrench", "mass": "1.3kg", "count": "3" }` .                                                                                                                                                                                                                                                                                                                       |
| `vectorSchema`   | `map (key: string, value: object ( `[`VectorField`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/mcp/tools_list/list_collections#Output.Schema.VectorField)` ))` Optional. Schema for vector fields. Only vector fields in this schema will be searchable. Field names must contain only alphanumeric characters, underscores, and hyphens. An object containing a list of `"key": value` pairs. Example: `{ "name": "wrench", "mass": "1.3kg", "count": "3" }` . |
| `dataSchema`     | `object ( `[`Struct`](https://protobuf.dev/reference/protobuf/google.protobuf/#struct)` format)` Optional. JSON Schema for data. Field names must contain only alphanumeric characters, underscores, and hyphens. The schema must be compliant with [JSON Schema Draft 7](https://json-schema.org/draft-07/schema) .                                                                                                                                                                                                |
| `encryptionSpec` | `object ( `[`EncryptionSpec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/mcp/tools_list/list_collections#Output.Schema.EncryptionSpec)` )` Optional. Immutable. Specifies the customer-managed encryption key spec for a Collection. If set, this Collection and all sub-resources of this Collection will be secured by this key.                                                                                                                              |

### Timestamp

**JSON representation**

```
{
  "seconds": string,
  "nanos": integer
}
```

| Fields    |                                                                                                                                                                                                                                                                                                                      |
|-----------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `seconds` | `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)` Represents seconds of UTC time since Unix epoch 1970-01-01T00:00:00Z. Must be between -62135596800 and 253402300799 inclusive (which corresponds to 0001-01-01T00:00:00Z to 9999-12-31T23:59:59Z).                            |
| `nanos`   | `integer` Non-negative fractions of a second at nanosecond resolution. This field is the nanosecond portion of the duration, not an alternative to seconds. Negative second values with fractions must still have non-negative nanos values that count forward in time. Must be between 0 and 999,999,999 inclusive. |

### LabelsEntry

**JSON representation**

```
{
  "key": string,
  "value": string
}
```

| Fields  |          |
|---------|----------|
| `key`   | `string` |
| `value` | `string` |

### VectorSchemaEntry

**JSON representation**

```
{
  "key": string,
  "value": {
    object (VectorField)
  }
}
```

| Fields  |                                                                                                                                                                                          |
|---------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `key`   | `string`                                                                                                                                                                                 |
| `value` | `object ( `[`VectorField`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/mcp/tools_list/list_collections#Output.Schema.VectorField)` )` |

### VectorField

**JSON representation**

```
{

  // Union field vector_type_config can be only one of the following:
  "denseVector": {
    object (DenseVectorField)
  },
  "sparseVector": {
    object (SparseVectorField)
  }
  // End of list of possible types for union field vector_type_config.
}
```

| Fields                                                                                                               |                                                                                                                                                                                                                        |
|----------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Union field `vector_type_config` . Vector type configuration. `vector_type_config` can be only one of the following: |                                                                                                                                                                                                                        |
| `denseVector`                                                                                                        | `object ( `[`DenseVectorField`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/mcp/tools_list/list_collections#Output.Schema.DenseVectorField)` )` Dense vector field. |
| `sparseVector`                                                                                                       | `object ( ``SparseVectorField`` )` Sparse vector field.                                                                                                                                                                |
|                                                                                                                      |                                                                                                                                                                                                                        |

### DenseVectorField

**JSON representation**

```
{
  "dimensions": integer,
  "vertexEmbeddingConfig": {
    object (VertexEmbeddingConfig)
  }
}
```

| Fields                  |                                                                                                                                                                                                                                                                                                                                                                 |
|-------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `dimensions`            | `integer` Dimensionality of the vector field.                                                                                                                                                                                                                                                                                                                   |
| `vertexEmbeddingConfig` | `object ( `[`VertexEmbeddingConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/mcp/tools_list/list_collections#Output.Schema.VertexEmbeddingConfig)` )` Optional. Configuration for generating embeddings for the vector field. If not specified, the embedding field must be populated in the DataObject. |

### VertexEmbeddingConfig

**JSON representation**

```
{
  "modelId": string,
  "textTemplate": string,
  "taskType": enum (EmbeddingTaskType)
}
```

| Fields         |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
|----------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `modelId`      | `string` Required. Required: ID of the embedding model to use. See <https://cloud.google.com/vertex-ai/generative-ai/docs/learn/models#embeddings-models> for the list of supported models.                                                                                                                                                                                                                                                                                                                                                                                             |
| `textTemplate` | `string` Optional. Text template for the input to the model. The template must contain one or more references to fields in the DataObject, e.g.: "Movie Title: {title} ---- Movie Plot: {plot}". Required when using the text-only path.                                                                                                                                                                                                                                                                                                                                                |
| `taskType`     | `enum ( `[`EmbeddingTaskType`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/mcp/tools_list/list_collections#Output.Schema.EmbeddingTaskType)` )` Optional. Optional: Task type for the embeddings. Required for text-only embedding models, see <https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/embeddings/task-types> Not needed for multi modal embedding models, see <https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/embeddings/get-multimodal-embeddings#specify-task-instructions> |

### Struct

**JSON representation**

```
{
  "fields": {
    string: value,
    ...
  }
}
```

| Fields   |                                                                                                                                                                                                                                                                                          |
|----------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `fields` | `map (key: string, value: value ( `[`Value`](https://protobuf.dev/reference/protobuf/google.protobuf/#value)` format))` Unordered map of dynamically typed values. An object containing a list of `"key": value` pairs. Example: `{ "name": "wrench", "mass": "1.3kg", "count": "3" }` . |

### FieldsEntry

**JSON representation**

```
{
  "key": string,
  "value": value
}
```

| Fields  |                                                                                               |
|---------|-----------------------------------------------------------------------------------------------|
| `key`   | `string`                                                                                      |
| `value` | `value ( `[`Value`](https://protobuf.dev/reference/protobuf/google.protobuf/#value)` format)` |

### Value

**JSON representation**

```
{

  // Union field kind can be only one of the following:
  "nullValue": null,
  "numberValue": number,
  "stringValue": string,
  "boolValue": boolean,
  "structValue": {
    object
  },
  "listValue": array
  // End of list of possible types for union field kind.
}
```

| Fields                                                                           |                                                                                                                                                                                                                                                |
|----------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Union field `kind` . The kind of value. `kind` can be only one of the following: |                                                                                                                                                                                                                                                |
| `nullValue`                                                                      | `null` Represents a JSON `null` .                                                                                                                                                                                                              |
| `numberValue`                                                                    | `number` Represents a JSON number. Must not be `NaN` , `Infinity` or `-Infinity` , since those are not supported in JSON. This also cannot represent large Int64 values, since JSON format generally does not support them in its number type. |
| `stringValue`                                                                    | `string` Represents a JSON string.                                                                                                                                                                                                             |
| `boolValue`                                                                      | `boolean` Represents a JSON boolean ( `true` or `false` literal in JSON).                                                                                                                                                                      |
| `structValue`                                                                    | `object ( `[`Struct`](https://protobuf.dev/reference/protobuf/google.protobuf/#struct)` format)` Represents a JSON object.                                                                                                                     |
| `listValue`                                                                      | `array ( `[`ListValue`](https://protobuf.dev/reference/protobuf/google.protobuf/#list-value)` format)` Represents a JSON array.                                                                                                                |
|                                                                                  |                                                                                                                                                                                                                                                |

### ListValue

**JSON representation**

```
{
  "values": [
    value
  ]
}
```

| Fields     |                                                                                                                                           |
|------------|-------------------------------------------------------------------------------------------------------------------------------------------|
| `values[]` | `value ( `[`Value`](https://protobuf.dev/reference/protobuf/google.protobuf/#value)` format)` Repeated field of dynamically typed values. |

### EncryptionSpec

**JSON representation**

```
{
  "cryptoKeyName": string
}
```

| Fields          |                                                                                                                                                                                                                                                                   |
|-----------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `cryptoKeyName` | `string` Required. Resource name of the Cloud KMS key used to protect the resource. The Cloud KMS key must be in the same region as the resource. It must have the format `projects/{project}/locations/{location}/keyRings/{key_ring}/cryptoKeys/{crypto_key}` . |

### EmbeddingTaskType

Represents the task the embeddings will be used for.

| Enums                             |                                                                        |
|-----------------------------------|------------------------------------------------------------------------|
| `EMBEDDING_TASK_TYPE_UNSPECIFIED` | Unspecified task type.                                                 |
| `RETRIEVAL_QUERY`                 | Specifies the given text is a query in a search/retrieval setting.     |
| `RETRIEVAL_DOCUMENT`              | Specifies the given text is a document from the corpus being searched. |
| `SEMANTIC_SIMILARITY`             | Specifies the given text will be used for STS.                         |
| `CLASSIFICATION`                  | Specifies that the given text will be classified.                      |
| `CLUSTERING`                      | Specifies that the embeddings will be used for clustering.             |
| `QUESTION_ANSWERING`              | Specifies that the embeddings will be used for question answering.     |
| `FACT_VERIFICATION`               | Specifies that the embeddings will be used for fact verification.      |
| `CODE_RETRIEVAL_QUERY`            | Specifies that the embeddings will be used for code retrieval.         |

### NullValue

Represents a JSON `null` .

`NullValue` is a sentinel, using an enum with only one value to represent the null value for the `Value` type union.

A field of type `NullValue` with any value other than `0` is considered invalid. Most ProtoJSON serializers will emit a `Value` with a `null_value` set as a JSON `null` regardless of the integer value, and so will round trip to a `0` value.

| Enums        |             |
|--------------|-------------|
| `NULL_VALUE` | Null value. |

### Tool Annotations

[Tool annotations](https://modelcontextprotocol.io/specification/latest/schema#toolannotations) are sent to MCP clients to describe the basic risk of a given tool. Most clients treat these hints as untrusted, but they can be used to decide when a confirmation prompt might be sent to a user.

Along with the title string, the following boolean hints are defined as follows:

- `readOnlyHint` : If true, the tool doesn't modify its environment. Default: false.
- `destructiveHint` : If true, then the tool can perform destructive actions. If false, then the tool can only perform additive actions. Default: true.
- `idempotentHint` : If true, then calling the tool repeatedly with the same arguments will have no additional effect on its environment. Default: false.
- `openWorldHint` : If true, then the tool can interact with an 'open world' of external entities. If false, then the tool can only interact with internal entities. For example, a web search tool would be open world, while a memory tool would not be open world.

Destructive Hint: ❌ \| Idempotent Hint: ✅ \| Read Only Hint: ✅ \| Open World Hint: ❌
