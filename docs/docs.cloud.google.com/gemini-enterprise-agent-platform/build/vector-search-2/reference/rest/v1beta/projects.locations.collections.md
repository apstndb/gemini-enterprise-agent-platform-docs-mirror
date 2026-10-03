---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/rest/v1beta/projects.locations.collections
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/rest/v1beta/projects.locations.collections
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
  "schema": {
    object
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

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Fields</th>
<th></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code>name</code></td>
<td><p><code>string</code></p>
<p>Identifier. name of resource</p></td>
</tr>
<tr class="even">
<td><code>displayName</code></td>
<td><p><code>string</code></p>
<p>Optional. User-specified display name of the collection</p></td>
</tr>
<tr class="odd">
<td><code>description</code></td>
<td><p><code>string</code></p>
<p>Optional. User-specified description of the collection</p></td>
</tr>
<tr class="even">
<td><code>createTime</code></td>
<td><p><code>string ( </code><a href="https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp"><code>Timestamp</code></a><code> format)</code></p>
<p>Output only. [Output only] Create time stamp</p>
<p>Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: <code>"2014-10-02T15:01:23Z"</code> , <code>"2014-10-02T15:01:23.045123456Z"</code> or <code>"2014-10-02T15:01:23+05:30"</code> .</p></td>
</tr>
<tr class="odd">
<td><code>updateTime</code></td>
<td><p><code>string ( </code><a href="https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp"><code>Timestamp</code></a><code> format)</code></p>
<p>Output only. [Output only] Update time stamp</p>
<p>Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: <code>"2014-10-02T15:01:23Z"</code> , <code>"2014-10-02T15:01:23.045123456Z"</code> or <code>"2014-10-02T15:01:23+05:30"</code> .</p></td>
</tr>
<tr class="even">
<td><code>labels</code></td>
<td><p><code>map (key: string, value: string)</code></p>
<p>Optional. Labels as key value pairs.</p>
<p>An object containing a list of <code>"key": value</code> pairs. Example: <code>{ "name": "wrench", "mass": "1.3kg", "count": "3" }</code> .</p></td>
</tr>
<tr class="odd">
<td><code>schema </code><strong><code>(deprecated)</code></strong></td>
<td><p><code>object ( </code><a href="https://protobuf.dev/reference/protobuf/google.protobuf/#struct"><code>Struct</code></a><code> format)</code></p>
<blockquote>
<p>This item is deprecated!</p>
</blockquote>
<p>Optional. Deprecated: JSON Schema for data. Please use dataSchema instead.</p></td>
</tr>
<tr class="even">
<td><code>vectorSchema</code></td>
<td><p><code>map (key: string, value: object ( </code><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/rest/v1beta/projects.locations.collections#VectorField"><code>VectorField</code></a><code> ))</code></p>
<p>Optional. Schema for vector fields. Only vector fields in this schema will be searchable. Field names must contain only alphanumeric characters, underscores, and hyphens.</p>
<p>An object containing a list of <code>"key": value</code> pairs. Example: <code>{ "name": "wrench", "mass": "1.3kg", "count": "3" }</code> .</p></td>
</tr>
<tr class="odd">
<td><code>dataSchema</code></td>
<td><p><code>object ( </code><a href="https://protobuf.dev/reference/protobuf/google.protobuf/#struct"><code>Struct</code></a><code> format)</code></p>
<p>Optional. JSON Schema for data. Field names must contain only alphanumeric characters, underscores, and hyphens. The schema must be compliant with <a href="https://json-schema.org/draft-07/schema">JSON Schema Draft 7</a> .</p></td>
</tr>
<tr class="even">
<td><code>encryptionSpec</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/rest/v1beta/projects.locations.collections#EncryptionSpec"><code>EncryptionSpec</code></a><code> )</code></p>
<p>Optional. Immutable. Specifies the customer-managed encryption key spec for a Collection. If set, this Collection and all sub-resources of this Collection will be secured by this key.</p></td>
</tr>
</tbody>
</table>

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

| Fields                                                                                                               |                                                                                                                                                                                                                        |
|----------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Union field `vector_type_config` . Vector type configuration. `vector_type_config` can be only one of the following: |                                                                                                                                                                                                                        |
| `denseVector`                                                                                                        | `object ( `[`DenseVectorField`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/rest/v1beta/projects.locations.collections#DenseVectorField)` )` Dense vector field.    |
| `sparseVector`                                                                                                       | `object ( `[`SparseVectorField`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/rest/v1beta/projects.locations.collections#SparseVectorField)` )` Sparse vector field. |

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

| Fields                  |                                                                                                                                                                                                                                                                                                                                                              |
|-------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `dimensions`            | `integer` Dimensionality of the vector field.                                                                                                                                                                                                                                                                                                                |
| `vertexEmbeddingConfig` | `object ( `[`VertexEmbeddingConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/rest/v1beta/projects.locations.collections#VertexEmbeddingConfig)` )` Optional. Configuration for generating embeddings for the vector field. If not specified, the embedding field must be populated in the DataObject. |

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

| Fields         |                                                                                                                                                                                                                                                   |
|----------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `modelId`      | `string` Required. Required: ID of the embedding model to use. See <https://cloud.google.com/vertex-ai/generative-ai/docs/learn/models#embeddings-models> for the list of supported models.                                                       |
| `textTemplate` | `string` Required. Required: Text template for the input to the model. The template must contain one or more references to fields in the DataObject, e.g.: "Movie Title: {title} ---- Movie Plot: {plot}".                                        |
| `taskType`     | `enum ( `[`EmbeddingTaskType`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/rest/v1beta/projects.locations.collections#EmbeddingTaskType)` )` Required. Required: Task type for the embeddings. |

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

| Methods                                                                                                                                                                            |                                                                             |
|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------|
| [`create`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/rest/v1beta/projects.locations.collections/create)                       | Creates a new Collection in a given project and location.                   |
| [`delete`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/rest/v1beta/projects.locations.collections/delete)                       | Deletes a single Collection.                                                |
| [`exportDataObjects`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/rest/v1beta/projects.locations.collections/exportDataObjects) | Initiates a Long-Running Operation to export DataObjects from a Collection. |
| [`get`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/rest/v1beta/projects.locations.collections/get)                             | Gets details of a single Collection.                                        |
| [`importDataObjects`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/rest/v1beta/projects.locations.collections/importDataObjects) | Initiates a Long-Running Operation to import DataObjects into a Collection. |
| [`list`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/rest/v1beta/projects.locations.collections/list)                           | Lists Collections in a given project and location.                          |
| [`patch`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/rest/v1beta/projects.locations.collections/patch)                         | Updates the parameters of a single Collection.                              |
