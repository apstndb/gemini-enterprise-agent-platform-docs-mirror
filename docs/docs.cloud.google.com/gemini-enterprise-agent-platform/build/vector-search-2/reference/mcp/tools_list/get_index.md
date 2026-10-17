---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/mcp/tools_list/get_index
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/mcp/tools_list/get_index
title: 'MCP Tools Reference: vectorsearch.googleapis.com'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

## Tool: `get_index`

Retrieves details of a specific index within a collection.

The following code sample shows how to use `curl` to call the `get_index` MCP tool.

**Curl Request**

```
curl --location 'https://vectorsearch.googleapis.com/mcp' \
--header 'content-type: application/json' \
--header 'accept: application/json, text/event-stream' \
--data '{
  "method": "tools/call",
  "params": {
    "name": "get_index",
    "arguments": {
      // Provide these details according to the MCP tool specification.
    }
  },
  "jsonrpc": "2.0",
  "id": 1
}'
```

## Input Schema

Message for getting an Index

### GetIndexRequest

**JSON representation**

```
{
  "name": string
}
```

| Fields |                                         |
|--------|-----------------------------------------|
| `name` | `string` Required. Name of the resource |

## Output Schema

Message describing Index object

### Index

**JSON representation**

```
{
  "name": string,
  "displayName": string,
  "description": string,
  "labels": {
    string: string,
    ...
  },
  "createTime": string,
  "updateTime": string,
  "distanceMetric": enum (DistanceMetric),
  "indexField": string,
  "filterFields": [
    string
  ],
  "storeFields": [
    string
  ],

  // Union field infra_type can be only one of the following:
  "dedicatedInfrastructure": {
    object (DedicatedInfrastructure)
  }
  // End of list of possible types for union field infra_type.

  // Union field index_type can be only one of the following:
  "denseScann": {
    object (DenseScannIndex)
  }
  // End of list of possible types for union field index_type.
}
```

| Fields                                                                                                          |                                                                                                                                                                                                                                                                                                                                                                                                                      |
|-----------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `name`                                                                                                          | `string` Identifier. name of resource                                                                                                                                                                                                                                                                                                                                                                                |
| `displayName`                                                                                                   | `string` Optional. User-specified display name of the index                                                                                                                                                                                                                                                                                                                                                          |
| `description`                                                                                                   | `string` Optional. User-specified description of the index                                                                                                                                                                                                                                                                                                                                                           |
| `labels`                                                                                                        | `map (key: string, value: string)` Optional. Labels as key value pairs. An object containing a list of `"key": value` pairs. Example: `{ "name": "wrench", "mass": "1.3kg", "count": "3" }` .                                                                                                                                                                                                                        |
| `createTime`                                                                                                    | `string ( `[`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp)` format)` Output only. \[Output only\] Create time stamp Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` . |
| `updateTime`                                                                                                    | `string ( `[`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp)` format)` Output only. \[Output only\] Update time stamp Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` . |
| `distanceMetric`                                                                                                | `enum ( `[`DistanceMetric`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/mcp/tools_list/list_indexes#Output.Schema.DistanceMetric)` )` Optional. Distance metric used for indexing. If not specified, will default to DOT_PRODUCT.                                                                                                                                 |
| `indexField`                                                                                                    | `string` Required. The collection schema field to index.                                                                                                                                                                                                                                                                                                                                                             |
| `filterFields[]`                                                                                                | `string` Optional. The fields to push into the index to enable fast ANN inline filtering.                                                                                                                                                                                                                                                                                                                            |
| `storeFields[]`                                                                                                 | `string` Optional. The fields to push into the index to enable inline data retrieval.                                                                                                                                                                                                                                                                                                                                |
| Union field `infra_type` . The infrastructure type of the index. `infra_type` can be only one of the following: |                                                                                                                                                                                                                                                                                                                                                                                                                      |
| `dedicatedInfrastructure`                                                                                       | `object ( `[`DedicatedInfrastructure`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/mcp/tools_list/list_indexes#Output.Schema.DedicatedInfrastructure)` )` Optional. Dedicated infrastructure for the index.                                                                                                                                                       |
|                                                                                                                 |                                                                                                                                                                                                                                                                                                                                                                                                                      |
| Union field `index_type` . The type of the index. `index_type` can be only one of the following:                |                                                                                                                                                                                                                                                                                                                                                                                                                      |
| `denseScann`                                                                                                    | `object ( `[`DenseScannIndex`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/mcp/tools_list/list_indexes#Output.Schema.DenseScannIndex)` )` Optional. Dense ScaNN index.                                                                                                                                                                                            |
|                                                                                                                 |                                                                                                                                                                                                                                                                                                                                                                                                                      |

### DedicatedInfrastructure

**JSON representation**

```
{
  "autoscalingSpec": {
    object (AutoscalingSpec)
  },

  // Union field _mode can be only one of the following:
  "mode": enum (Mode)
  // End of list of possible types for union field _mode.
}
```

| Fields                                                          |                                                                                                                                                                                                                                   |
|-----------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `autoscalingSpec`                                               | `object ( `[`AutoscalingSpec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/mcp/tools_list/list_indexes#Output.Schema.AutoscalingSpec)` )` Optional. Autoscaling specification. |
| Union field `_mode` . `_mode` can be only one of the following: |                                                                                                                                                                                                                                   |
| `mode`                                                          | `enum ( `[`Mode`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/mcp/tools_list/list_indexes#Output.Schema.Mode)` )` Optional. Mode of the dedicated infrastructure.              |
|                                                                 |                                                                                                                                                                                                                                   |

### AutoscalingSpec

**JSON representation**

```
{
  "minReplicaCount": integer,
  "maxReplicaCount": integer
}
```

| Fields            |                                                                                                                                                                                                                                                                                                                              |
|-------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `minReplicaCount` | `integer` Optional. The minimum number of replicas. If not set or set to `0` , defaults to `2` . Must be \>= `1` and \<= `1000` .                                                                                                                                                                                            |
| `maxReplicaCount` | `integer` Optional. The maximum number of replicas. Must be \>= `min_replica_count` and \<= `1000` . For the v1beta version, if not set or set to `0` , defaults to the greater of `min_replica_count` and `5` . For all other versions, if not set or set to `0` , defaults to the greater of `min_replica_count` and `2` . |

### DenseScannIndex

**JSON representation**

```
{
  "featureNormType": enum (FeatureNormType)
}
```

| Fields            |                                                                                                                                                                                                                         |
|-------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `featureNormType` | `enum ( `[`FeatureNormType`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/mcp/tools_list/list_indexes#Output.Schema.FeatureNormType)` )` Optional. Feature norm type. |

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

### Mode

Mode of the dedicated infrastructure.

| Enums                   |                                                           |
|-------------------------|-----------------------------------------------------------|
| `MODE_UNSPECIFIED`      | Default will use `PERFORMANCE_OPTIMIZED` .                |
| `STORAGE_OPTIMIZED`     | This is storage optimized variation.                      |
| `PERFORMANCE_OPTIMIZED` | This is Performance optimized on E2 or equivalent family. |

### FeatureNormType

Feature norm type for ScaNN index.

| Enums                           |                                |
|---------------------------------|--------------------------------|
| `FEATURE_NORM_TYPE_UNSPECIFIED` | Unspecified feature norm type. |
| `NONE`                          | No norm applied.               |
| `UNIT_L2_NORM`                  | Unit L2 norm.                  |

### DistanceMetric

Distance metric for vector search.

| Enums                         |                                                  |
|-------------------------------|--------------------------------------------------|
| `DISTANCE_METRIC_UNSPECIFIED` | Default value, distance metric is not specified. |
| `DOT_PRODUCT`                 | Dot product distance metric.                     |
| `COSINE_DISTANCE`             | Cosine distance metric.                          |

### Tool Annotations

[Tool annotations](https://modelcontextprotocol.io/specification/latest/schema#toolannotations) are sent to MCP clients to describe the basic risk of a given tool. Most clients treat these hints as untrusted, but they can be used to decide when a confirmation prompt might be sent to a user.

Along with the title string, the following boolean hints are defined as follows:

- `readOnlyHint` : If true, the tool doesn't modify its environment. Default: false.
- `destructiveHint` : If true, then the tool can perform destructive actions. If false, then the tool can only perform additive actions. Default: true.
- `idempotentHint` : If true, then calling the tool repeatedly with the same arguments will have no additional effect on its environment. Default: false.
- `openWorldHint` : If true, then the tool can interact with an 'open world' of external entities. If false, then the tool can only interact with internal entities. For example, a web search tool would be open world, while a memory tool would not be open world.

Destructive Hint: ❌ \| Idempotent Hint: ✅ \| Read Only Hint: ✅ \| Open World Hint: ❌
