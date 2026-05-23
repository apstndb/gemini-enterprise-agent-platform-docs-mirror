---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.ragCorpora
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.ragCorpora
title: 'REST Resource: projects.locations.ragCorpora'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

## Resource: RagCorpus

A RagCorpus is a RagFile container and a project can have multiple RagCorpora.

Fields

`name` `string`

Output only. The resource name of the RagCorpus.

`displayName` `string`

Required. The display name of the RagCorpus. The name can be up to 128 characters long and can consist of any UTF-8 characters.

`description` `string`

Optional. The description of the RagCorpus.

`createTime` ` string ( Timestamp  ` format)

Output only. timestamp when this RagCorpus was created.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`updateTime` ` string ( Timestamp  ` format)

Output only. timestamp when this RagCorpus was last updated.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`corpusStatus` ` object ( CorpusStatus  ` )

Output only. RagCorpus state.

`encryptionSpec` ` object ( EncryptionSpec  ` )

Optional. Immutable. The CMEK key name used to encrypt at-rest data related to this Corpus. Only applicable to RagManagedDb option for Vector DB. This field can only be set at corpus creation time, and cannot be updated or deleted.

`satisfiesPzs` `boolean`

Output only. reserved for future use.

`satisfiesPzi` `boolean`

Output only. reserved for future use.

`backend_config` `Union type`

The backend config of the RagCorpus. It can be data store and/or retrieval engine. `backend_config` can be only one of the following:

`vectorDbConfig` ` object ( RagVectorDbConfig  ` )

Optional. Immutable. The config for the Vector DBs.

`vertexAiSearchConfig` ` object ( VertexAiSearchConfig  ` )

Optional. Immutable. The config for the Agent Platform Search.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;name&quot;: string,&quot;displayName&quot;: string,&quot;description&quot;: string,&quot;createTime&quot;: string,&quot;updateTime&quot;: string,&quot;corpusStatus&quot;: {object (CorpusStatus)},&quot;encryptionSpec&quot;: {object (EncryptionSpec)},&quot;satisfiesPzs&quot;: boolean,&quot;satisfiesPzi&quot;: boolean,// backend_config&quot;vectorDbConfig&quot;: {object (RagVectorDbConfig)},&quot;vertexAiSearchConfig&quot;: {object (VertexAiSearchConfig)}// Union type}</code></pre></td>
</tr>
</tbody>
</table>

## RagVectorDbConfig

Config for the Vector DB to use for RAG.

Fields

`apiAuth` ` object ( ApiAuth  ` )

Authentication config for the chosen Vector DB.

`ragEmbeddingModelConfig` ` object ( RagEmbeddingModelConfig  ` )

Optional. Immutable. The embedding model config of the Vector DB.

`vector_db` `Union type`

The config for the Vector DB. `vector_db` can be only one of the following:

`ragManagedDb` ` object ( RagManagedDb  ` )

The config for the RAG-managed Vector DB.

`pinecone` ` object ( Pinecone  ` )

The config for the Pinecone.

`vertexVectorSearch` ` object ( VertexVectorSearch  ` )

The config for the Vertex Vector Search.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;apiAuth&quot;: {object (ApiAuth)},&quot;ragEmbeddingModelConfig&quot;: {object (RagEmbeddingModelConfig)},// vector_db&quot;ragManagedDb&quot;: {object (RagManagedDb)},&quot;pinecone&quot;: {object (Pinecone)},&quot;vertexVectorSearch&quot;: {object (VertexVectorSearch)}// Union type}</code></pre></td>
</tr>
</tbody>
</table>

## RagManagedDb

The config for the default RAG-managed Vector DB.

Fields

`retrieval_strategy` `Union type`

Choice of retrieval strategy. `retrieval_strategy` can be only one of the following:

`knn` ` object ( KNN  ` )

Performs a KNN search on RagCorpus. Default choice if not specified.

`ann` ` object ( ANN  ` )

Performs an ANN search on RagCorpus. Use this if you have a lot of files (\> 10K) in your RagCorpus and want to reduce the search latency.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{// retrieval_strategy&quot;knn&quot;: {object (KNN)},&quot;ann&quot;: {object (ANN)}// Union type}</code></pre></td>
</tr>
</tbody>
</table>

## KNN

This type has no fields.

Config for KNN search.

## ANN

Config for ANN search.

RagManagedDb uses a tree-based structure to partition data and facilitate faster searches. As a tradeoff, it requires longer indexing time and manual triggering of index rebuild via the ImportRagFiles and ragCorpora.patch API.

Fields

`treeDepth` `integer`

The depth of the tree-based structure. Only depth values of 2 and 3 are supported.

Recommended value is 2 if you have if you have O(10K) files in the RagCorpus and set this to 3 if more than that.

Default value is 2.

`leafCount` `integer`

Number of leaf nodes in the tree-based structure. Each leaf node contains groups of closely related vectors along with their corresponding centroid.

Recommended value is 10 \* sqrt(num of RagFiles in your RagCorpus).

Default value is 500.

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
  &quot;treeDepth&quot;: integer,
  &quot;leafCount&quot;: integer
}</code></pre></td>
</tr>
</tbody>
</table>

## Pinecone

The config for the Pinecone.

Fields

`indexName` `string`

Pinecone index name. This value cannot be changed after it's set.

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
  &quot;indexName&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

## VertexVectorSearch

The config for the Vertex Vector Search.

Fields

`indexEndpoint` `string`

The resource name of the Index Endpoint. Format: `projects/{project}/locations/{location}/indexEndpoints/{indexEndpoint}`

`index` `string`

The resource name of the Index. Format: `projects/{project}/locations/{location}/indexes/{index}`

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
  &quot;indexEndpoint&quot;: string,
  &quot;index&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

## ApiAuth

The generic reusable api auth config. Deprecated. Please use AuthConfig (google/cloud/aiplatform/master/auth.proto) instead.

Fields

`auth_config` `Union type`

The auth config. `auth_config` can be only one of the following:

`apiKeyConfig` ` object ( ApiKeyConfig  ` )

The API secret.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{// auth_config&quot;apiKeyConfig&quot;: {object (ApiKeyConfig)}// Union type}</code></pre></td>
</tr>
</tbody>
</table>

## RagEmbeddingModelConfig

Config for the embedding model to use for RAG.

Fields

`model_config` `Union type`

The model config to use. `model_config` can be only one of the following:

`vertexPredictionEndpoint` ` object ( VertexPredictionEndpoint  ` )

The Agent Platform Prediction Endpoint that either refers to a publisher model or an endpoint that is hosting a 1P fine-tuned text embedding model. endpoints hosting non-1P fine-tuned text embedding models are currently not supported. This is used for dense vector search.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{// model_config&quot;vertexPredictionEndpoint&quot;: {object (VertexPredictionEndpoint)}// Union type}</code></pre></td>
</tr>
</tbody>
</table>

## VertexPredictionEndpoint

Config representing a model hosted on Vertex Prediction Endpoint.

Fields

`endpoint` `string`

Required. The endpoint resource name. Format: `projects/{project}/locations/{location}/publishers/{publisher}/models/{model}` or `projects/{project}/locations/{location}/endpoints/{endpoint}`

`model` `string`

Output only. The resource name of the model that is deployed on the endpoint. Present only when the endpoint is not a publisher model. Pattern: `projects/{project}/locations/{location}/models/{model}`

`modelVersionId` `string`

Output only. version id of the model that is deployed on the endpoint. Present only when the endpoint is not a publisher model.

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
  &quot;endpoint&quot;: string,
  &quot;model&quot;: string,
  &quot;modelVersionId&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

## VertexAiSearchConfig

Config for the Agent Platform Search.

Fields

`servingConfig` `string`

Agent Platform Search Serving Config resource full name. For example, `projects/{project}/locations/{location}/collections/{collection}/engines/{engine}/servingConfigs/{servingConfig}` or `projects/{project}/locations/{location}/collections/{collection}/dataStores/{dataStore}/servingConfigs/{servingConfig}` .

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
  &quot;servingConfig&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

## CorpusStatus

RagCorpus status.

Fields

`state` ` enum ( State  ` )

Output only. RagCorpus life state.

`errorStatus` `string`

Output only. Only when the `state` field is ERROR.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;state&quot;: enum (State),&quot;errorStatus&quot;: string}</code></pre></td>
</tr>
</tbody>
</table>

## State

RagCorpus life state.

Enums

`UNKNOWN`

This state is not supposed to happen.

`INITIALIZED`

RagCorpus resource entry is initialized, but hasn't done validation.

`ACTIVE`

RagCorpus is provisioned successfully and is ready to serve.

`ERROR`

RagCorpus is in a problematic situation. See `errorMessage` field for details.

## Methods

### `            create           `

Creates a RagCorpus.

### `            delete           `

Deletes a RagCorpus.

### `            get           `

Gets a RagCorpus.

### `            list           `

Lists RagCorpora in a Location.

### `            patch           `

Updates a RagCorpus.
