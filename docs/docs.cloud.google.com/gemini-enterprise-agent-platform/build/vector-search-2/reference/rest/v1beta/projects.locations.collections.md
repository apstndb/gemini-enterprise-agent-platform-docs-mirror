---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/rest/v1beta/projects.locations.collections
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/rest/v1beta/projects.locations.collections
title: 'REST Resource: projects.locations.collections'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

## Resource: Collection

Message describing Collection object

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;name&quot;: string,&quot;displayName&quot;: string,&quot;description&quot;: string,&quot;createTime&quot;: string,&quot;updateTime&quot;: string,&quot;labels&quot;: {string: string,...},&quot;schema&quot;: {object},&quot;vectorSchema&quot;: {string: {object (VectorField)},...},&quot;dataSchema&quot;: {object},&quot;encryptionSpec&quot;: {object (EncryptionSpec)}}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`name`

`string`

Identifier. name of resource

`displayName`

`string`

Optional. User-specified display name of the collection

`description`

`string`

Optional. User-specified description of the collection

`createTime`

` string ( Timestamp  ` format)

Output only. \[Output only\] Create time stamp

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`updateTime`

` string ( Timestamp  ` format)

Output only. \[Output only\] Update time stamp

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`labels`

`map (key: string, value: string)`

Optional. Labels as key value pairs.

An object containing a list of `"key": value` pairs. Example: `{ "name": "wrench", "mass": "1.3kg", "count": "3" }` .

` schema (deprecated)  `

` object ( Struct  ` format)

> This item is deprecated\!

Optional. Deprecated: JSON Schema for data. Please use dataSchema instead.

`vectorSchema`

` map (key: string, value: object ( VectorField  ` ))

Optional. Schema for vector fields. Only vector fields in this schema will be searchable. Field names must contain only alphanumeric characters, underscores, and hyphens.

An object containing a list of `"key": value` pairs. Example: `{ "name": "wrench", "mass": "1.3kg", "count": "3" }` .

`dataSchema`

` object ( Struct  ` format)

Optional. JSON Schema for data. Field names must contain only alphanumeric characters, underscores, and hyphens. The schema must be compliant with [JSON Schema Draft 7](https://json-schema.org/draft-07/schema) .

`encryptionSpec`

` object ( EncryptionSpec  ` )

Optional. Immutable. Specifies the customer-managed encryption key spec for a Collection. If set, this Collection and all sub-resources of this Collection will be secured by this key.

## VectorField

Message describing a vector field.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{// Union field vector_type_config can be only one of the following:&quot;denseVector&quot;: {object (DenseVectorField)},&quot;sparseVector&quot;: {object (SparseVectorField)}// End of list of possible types for union field vector_type_config.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

Union field `vector_type_config` . Vector type configuration. `vector_type_config` can be only one of the following:

`denseVector`

` object ( DenseVectorField  ` )

Dense vector field.

`sparseVector`

` object ( SparseVectorField  ` )

Sparse vector field.

## DenseVectorField

Message describing a dense vector field.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;dimensions&quot;: integer,&quot;vertexEmbeddingConfig&quot;: {object (VertexEmbeddingConfig)}}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`dimensions`

`integer`

Dimensionality of the vector field.

`vertexEmbeddingConfig`

` object ( VertexEmbeddingConfig  ` )

Optional. Configuration for generating embeddings for the vector field. If not specified, the embedding field must be populated in the DataObject.

## VertexEmbeddingConfig

Message describing the configuration for generating embeddings for a vector field using Vertex AI embeddings API.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;modelId&quot;: string,&quot;textTemplate&quot;: string,&quot;taskType&quot;: enum (EmbeddingTaskType)}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`modelId`

`string`

Required. Required: ID of the embedding model to use. See <https://cloud.google.com/vertex-ai/generative-ai/docs/learn/models#embeddings-models> for the list of supported models.

`textTemplate`

`string`

Required. Required: Text template for the input to the model. The template must contain one or more references to fields in the DataObject, e.g.: "Movie Title: {title} ---- Movie Plot: {plot}".

`taskType`

` enum ( EmbeddingTaskType  ` )

Required. Required: Task type for the embeddings.

## EmbeddingTaskType

Represents the task the embeddings will be used for.

Enums

`EMBEDDING_TASK_TYPE_UNSPECIFIED`

Unspecified task type.

`RETRIEVAL_QUERY`

Specifies the given text is a query in a search/retrieval setting.

`RETRIEVAL_DOCUMENT`

Specifies the given text is a document from the corpus being searched.

`SEMANTIC_SIMILARITY`

Specifies the given text will be used for STS.

`CLASSIFICATION`

Specifies that the given text will be classified.

`CLUSTERING`

Specifies that the embeddings will be used for clustering.

`QUESTION_ANSWERING`

Specifies that the embeddings will be used for question answering.

`FACT_VERIFICATION`

Specifies that the embeddings will be used for fact verification.

`CODE_RETRIEVAL_QUERY`

Specifies that the embeddings will be used for code retrieval.

## SparseVectorField

This type has no fields.

Message describing a sparse vector field.

## EncryptionSpec

Represents a customer-managed encryption key specification that can be applied to a Vector Search collection.

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
  &quot;cryptoKeyName&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`cryptoKeyName`

`string`

Required. Resource name of the Cloud KMS key used to protect the resource.

The Cloud KMS key must be in the same region as the resource. It must have the format `projects/{project}/locations/{location}/keyRings/{key_ring}/cryptoKeys/{crypto_key}` .

## Methods

### `            create           `

Creates a new Collection in a given project and location.

### `            delete           `

Deletes a single Collection.

### `            exportDataObjects           `

Initiates a Long-Running Operation to export DataObjects from a Collection.

### `            get           `

Gets details of a single Collection.

### `            importDataObjects           `

Initiates a Long-Running Operation to import DataObjects into a Collection.

### `            list           `

Lists Collections in a given project and location.

### `            patch           `

Updates the parameters of a single Collection.
