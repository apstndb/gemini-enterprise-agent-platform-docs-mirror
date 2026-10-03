---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/rest/v1/projects.locations.collections
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/rest/v1/projects.locations.collections
title: 'REST Resource: projects.locations.collections'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

## Resource: Collection

Message describing Collection object

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

| Fields           |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
|------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `name`           | `string` Identifier. name of resource                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| `displayName`    | `string` Optional. User-specified display name of the collection                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| `description`    | `string` Optional. User-specified description of the collection                                                                                                                                                                                                                                                                                                                                                                                                                                              |
| `createTime`     | `string ( `[`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp)` format)` Output only. \[Output only\] Create time stamp Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .                                                                                         |
| `updateTime`     | `string ( `[`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp)` format)` Output only. \[Output only\] Update time stamp Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .                                                                                         |
| `labels`         | `map (key: string, value: string)` Optional. Labels as key value pairs. An object containing a list of `"key": value` pairs. Example: `{ "name": "wrench", "mass": "1.3kg", "count": "3" }` .                                                                                                                                                                                                                                                                                                                |
| `vectorSchema`   | `map (key: string, value: object ( `[`VectorField`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/rest/v1/projects.locations.collections#VectorField)` ))` Optional. Schema for vector fields. Only vector fields in this schema will be searchable. Field names must contain only alphanumeric characters, underscores, and hyphens. An object containing a list of `"key": value` pairs. Example: `{ "name": "wrench", "mass": "1.3kg", "count": "3" }` . |
| `dataSchema`     | `object ( `[`Struct`](https://protobuf.dev/reference/protobuf/google.protobuf/#struct)` format)` Optional. JSON Schema for data. Field names must contain only alphanumeric characters, underscores, and hyphens. The schema must be compliant with [JSON Schema Draft 7](https://json-schema.org/draft-07/schema) .                                                                                                                                                                                         |
| `encryptionSpec` | `object ( `[`EncryptionSpec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/rest/v1/projects.locations.collections#EncryptionSpec)` )` Optional. Immutable. Specifies the customer-managed encryption key spec for a Collection. If set, this Collection and all sub-resources of this Collection will be secured by this key.                                                                                                                              |

## VectorField

Message describing a vector field.

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

| Fields                                                                                                               |                                                                                                                                                                                                                    |
|----------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Union field `vector_type_config` . Vector type configuration. `vector_type_config` can be only one of the following: |                                                                                                                                                                                                                    |
| `denseVector`                                                                                                        | `object ( `[`DenseVectorField`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/rest/v1/projects.locations.collections#DenseVectorField)` )` Dense vector field.    |
| `sparseVector`                                                                                                       | `object ( `[`SparseVectorField`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/rest/v1/projects.locations.collections#SparseVectorField)` )` Sparse vector field. |

## DenseVectorField

Message describing a dense vector field.

**JSON representation**

```
{
  "dimensions": integer,
  "vertexEmbeddingConfig": {
    object (VertexEmbeddingConfig)
  }
}
```

| Fields                  |                                                                                                                                                                                                                                                                                                                                                          |
|-------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `dimensions`            | `integer` Dimensionality of the vector field.                                                                                                                                                                                                                                                                                                            |
| `vertexEmbeddingConfig` | `object ( `[`VertexEmbeddingConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/rest/v1/projects.locations.collections#VertexEmbeddingConfig)` )` Optional. Configuration for generating embeddings for the vector field. If not specified, the embedding field must be populated in the DataObject. |

## VertexEmbeddingConfig

Message describing the configuration for generating embeddings for a vector field using Vertex AI embeddings API.

**JSON representation**

```
{
  "modelId": string,
  "textTemplate": string,
  "taskType": enum (EmbeddingTaskType)
}
```

| Fields         |                                                                                                                                                                                                                                               |
|----------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `modelId`      | `string` Required. Required: ID of the embedding model to use. See <https://cloud.google.com/vertex-ai/generative-ai/docs/learn/models#embeddings-models> for the list of supported models.                                                   |
| `textTemplate` | `string` Required. Required: Text template for the input to the model. The template must contain one or more references to fields in the DataObject, e.g.: "Movie Title: {title} ---- Movie Plot: {plot}".                                    |
| `taskType`     | `enum ( `[`EmbeddingTaskType`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/rest/v1/projects.locations.collections#EmbeddingTaskType)` )` Required. Required: Task type for the embeddings. |

## EmbeddingTaskType

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

## SparseVectorField

This type has no fields.

Message describing a sparse vector field.

## EncryptionSpec

Represents a customer-managed encryption key specification that can be applied to a Vector Search collection.

**JSON representation**

```
{
  "cryptoKeyName": string
}
```

| Fields          |                                                                                                                                                                                                                                                                   |
|-----------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `cryptoKeyName` | `string` Required. Resource name of the Cloud KMS key used to protect the resource. The Cloud KMS key must be in the same region as the resource. It must have the format `projects/{project}/locations/{location}/keyRings/{key_ring}/cryptoKeys/{crypto_key}` . |

| Methods                                                                                                                                                                        |                                                                             |
|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------|
| [`create`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/rest/v1/projects.locations.collections/create)                       | Creates a new Collection in a given project and location.                   |
| [`delete`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/rest/v1/projects.locations.collections/delete)                       | Deletes a single Collection.                                                |
| [`exportDataObjects`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/rest/v1/projects.locations.collections/exportDataObjects) | Initiates a Long-Running Operation to export DataObjects from a Collection. |
| [`get`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/rest/v1/projects.locations.collections/get)                             | Gets details of a single Collection.                                        |
| [`importDataObjects`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/rest/v1/projects.locations.collections/importDataObjects) | Initiates a Long-Running Operation to import DataObjects into a Collection. |
| [`list`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/rest/v1/projects.locations.collections/list)                           | Lists Collections in a given project and location.                          |
| [`patch`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/rest/v1/projects.locations.collections/patch)                         | Updates the parameters of a single Collection.                              |
