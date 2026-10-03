---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/rest/v1/projects.locations.collections.indexes
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/rest/v1/projects.locations.collections.indexes
title: 'REST Resource: projects.locations.collections.indexes'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

## Resource: Index

Message describing Index object

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
| `distanceMetric`                                                                                                | `enum ( `[`DistanceMetric`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/rest/v1/projects.locations.collections.indexes#DistanceMetric)` )` Optional. Distance metric used for indexing. If not specified, will default to DOT_PRODUCT.                                                                                                                            |
| `indexField`                                                                                                    | `string` Required. The collection schema field to index.                                                                                                                                                                                                                                                                                                                                                             |
| `filterFields[]`                                                                                                | `string` Optional. The fields to push into the index to enable fast ANN inline filtering.                                                                                                                                                                                                                                                                                                                            |
| `storeFields[]`                                                                                                 | `string` Optional. The fields to push into the index to enable inline data retrieval.                                                                                                                                                                                                                                                                                                                                |
| Union field `infra_type` . The infrastructure type of the index. `infra_type` can be only one of the following: |                                                                                                                                                                                                                                                                                                                                                                                                                      |
| `dedicatedInfrastructure`                                                                                       | `object ( `[`DedicatedInfrastructure`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/rest/v1/projects.locations.collections.indexes#DedicatedInfrastructure)` )` Optional. Dedicated infrastructure for the index.                                                                                                                                                  |
| Union field `index_type` . The type of the index. `index_type` can be only one of the following:                |                                                                                                                                                                                                                                                                                                                                                                                                                      |
| `denseScann`                                                                                                    | `object ( `[`DenseScannIndex`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/rest/v1/projects.locations.collections.indexes#DenseScannIndex)` )` Optional. Dense ScaNN index.                                                                                                                                                                                       |

## DedicatedInfrastructure

Represents dedicated infrastructure for the index.

**JSON representation**

```
{
  "autoscalingSpec": {
    object (AutoscalingSpec)
  },
  "mode": enum (Mode)
}
```

| Fields            |                                                                                                                                                                                                                                        |
|-------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `autoscalingSpec` | `object ( `[`AutoscalingSpec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/rest/v1/projects.locations.collections.indexes#AutoscalingSpec)` )` Optional. Autoscaling specification. |
| `mode`            | `enum ( `[`Mode`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/rest/v1/projects.locations.collections.indexes#Mode)` )` Optional. Mode of the dedicated infrastructure.              |

## Mode

Mode of the dedicated infrastructure.

| Enums                   |                                                           |
|-------------------------|-----------------------------------------------------------|
| `MODE_UNSPECIFIED`      | Default will use `PERFORMANCE_OPTIMIZED` .                |
| `STORAGE_OPTIMIZED`     | This is storage optimized variation.                      |
| `PERFORMANCE_OPTIMIZED` | This is Performance optimized on E2 or equivalent family. |

## AutoscalingSpec

Specification for autoscaling.

**JSON representation**

```
{
  "minReplicaCount": integer,
  "maxReplicaCount": integer
}
```

| Fields            |                                                                                                                                                                                                                                                                                                                        |
|-------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `minReplicaCount` | `integer` Optional. The minimum number of replicas. If not set or set to `0` , defaults to `2` . Must be \>= `1` and \<= `1000` .                                                                                                                                                                                      |
| `maxReplicaCount` | `integer` Optional. The maximum number of replicas. Must be \>= `minReplicaCount` and \<= `1000` . For the v1beta version, if not set or set to `0` , defaults to the greater of `minReplicaCount` and `5` . For all other versions, if not set or set to `0` , defaults to the greater of `minReplicaCount` and `2` . |

## DenseScannIndex

Dense ScaNN index configuration.

**JSON representation**

```
{
  "featureNormType": enum (FeatureNormType)
}
```

| Fields            |                                                                                                                                                                                                                              |
|-------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `featureNormType` | `enum ( `[`FeatureNormType`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/rest/v1/projects.locations.collections.indexes#FeatureNormType)` )` Optional. Feature norm type. |

## FeatureNormType

Feature norm type for ScaNN index.

| Enums                           |                                |
|---------------------------------|--------------------------------|
| `FEATURE_NORM_TYPE_UNSPECIFIED` | Unspecified feature norm type. |
| `NONE`                          | No norm applied.               |
| `UNIT_L2_NORM`                  | Unit L2 norm.                  |

## DistanceMetric

Distance metric for vector search.

| Enums                         |                                                  |
|-------------------------------|--------------------------------------------------|
| `DISTANCE_METRIC_UNSPECIFIED` | Default value, distance metric is not specified. |
| `DOT_PRODUCT`                 | Dot product distance metric.                     |
| `COSINE_DISTANCE`             | Cosine distance metric.                          |

| Methods                                                                                                                                                          |                                                      |
|------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------|
| [`create`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/rest/v1/projects.locations.collections.indexes/create) | Creates a new Index in a given project and location. |
| [`delete`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/rest/v1/projects.locations.collections.indexes/delete) | Deletes a single Index.                              |
| [`get`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/rest/v1/projects.locations.collections.indexes/get)       | Gets details of a single Index.                      |
| [`list`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/rest/v1/projects.locations.collections.indexes/list)     | Lists Indexes in a given project and location.       |
| [`patch`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/rest/v1/projects.locations.collections.indexes/patch)   | Updates the parameters of a single Index.            |
