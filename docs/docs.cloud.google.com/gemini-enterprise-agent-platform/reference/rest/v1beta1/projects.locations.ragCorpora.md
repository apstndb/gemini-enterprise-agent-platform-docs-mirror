---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.ragCorpora
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.ragCorpora
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

` ragEmbeddingModelConfig (deprecated)  ` ` object ( RagEmbeddingModelConfig  ` )

> This item is deprecated\!

Optional. Immutable. The embedding model config of the RagCorpus.

` ragVectorDbConfig (deprecated)  ` ` object ( RagVectorDbConfig  ` )

> This item is deprecated\!

Optional. Immutable. The Vector DB config of the RagCorpus.

`createTime` ` string ( Timestamp  ` format)

Output only. timestamp when this RagCorpus was created.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`updateTime` ` string ( Timestamp  ` format)

Output only. timestamp when this RagCorpus was last updated.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`corpusStatus` ` object ( CorpusStatus  ` )

Output only. RagCorpus state.

`ragFilesCount` `integer`

Output only. Number of RagFiles in the RagCorpus.

NOTE: This field is not populated in the response of `  VertexRagDataService.ListRagCorpora  ` .

`encryptionSpec` ` object ( EncryptionSpec  ` )

Optional. Immutable. The CMEK key name used to encrypt at-rest data related to this Corpus. Only applicable to RagManagedDb option for Vector DB. This field can only be set at corpus creation time, and cannot be updated or deleted.

`corpusTypeConfig` ` object ( CorpusTypeConfig  ` )

Optional. The corpus type config of the RagCorpus.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;name&quot;: string,&quot;displayName&quot;: string,&quot;description&quot;: string,&quot;ragEmbeddingModelConfig&quot;: {object (RagEmbeddingModelConfig)},&quot;ragVectorDbConfig&quot;: {object (RagVectorDbConfig)},&quot;createTime&quot;: string,&quot;updateTime&quot;: string,&quot;corpusStatus&quot;: {object (CorpusStatus)},&quot;ragFilesCount&quot;: integer,&quot;encryptionSpec&quot;: {object (EncryptionSpec)},&quot;corpusTypeConfig&quot;: {object (CorpusTypeConfig)},&quot;satisfiesPzs&quot;: boolean,&quot;satisfiesPzi&quot;: boolean,// backend_config&quot;vectorDbConfig&quot;: {object (RagVectorDbConfig)},&quot;vertexAiSearchConfig&quot;: {object (VertexAiSearchConfig)}// Union type}</code></pre></td>
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

`weaviate` ` object ( Weaviate  ` )

The config for the Weaviate.

`pinecone` ` object ( Pinecone  ` )

The config for the Pinecone.

`vertexFeatureStore` ` object ( VertexFeatureStore  ` )

The config for the Vertex feature Store.

`vertexVectorSearch` ` object ( VertexVectorSearch  ` )

The config for the Vertex Vector Search.

`ragManagedVertexVectorSearch` ` object ( RagManagedVertexVectorSearch  ` )

The config for the RAG-managed Vertex Vector Search 2.0.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;apiAuth&quot;: {object (ApiAuth)},&quot;ragEmbeddingModelConfig&quot;: {object (RagEmbeddingModelConfig)},// vector_db&quot;ragManagedDb&quot;: {object (RagManagedDb)},&quot;weaviate&quot;: {object (Weaviate)},&quot;pinecone&quot;: {object (Pinecone)},&quot;vertexFeatureStore&quot;: {object (VertexFeatureStore)},&quot;vertexVectorSearch&quot;: {object (VertexVectorSearch)},&quot;ragManagedVertexVectorSearch&quot;: {object (RagManagedVertexVectorSearch)}// Union type}</code></pre></td>
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

## Weaviate

The config for the Weaviate.

Fields

`httpEndpoint` `string`

Weaviate DB instance HTTP endpoint. e.g. 34.56.78.90:8080 Vertex RAG only supports HTTP connection to Weaviate. This value cannot be changed after it's set.

`collectionName` `string`

The corresponding collection this corpus maps to. This value cannot be changed after it's set.

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
  &quot;httpEndpoint&quot;: string,
  &quot;collectionName&quot;: string
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

## VertexFeatureStore

The config for the Vertex feature Store.

Fields

`featureViewResourceName` `string`

The resource name of the FeatureView. Format: `projects/{project}/locations/{location}/featureOnlineStores/{featureOnlineStore}/featureViews/{featureView}`

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
  &quot;featureViewResourceName&quot;: string
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

## RagManagedVertexVectorSearch

The config for the RAG-managed Vertex Vector Search 2.0.

Fields

`collectionName` `string`

Output only. The resource name of the Vector Search 2.0 Collection that RAG Created for the corpus. Only populated after the corpus is successfully created. Format: `projects/{project}/locations/{location}/collections/{collectionId}`

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
  &quot;collectionName&quot;: string
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

`hybridSearchConfig` ` object ( HybridSearchConfig  ` )

Configuration for hybrid search.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{// model_config&quot;vertexPredictionEndpoint&quot;: {object (VertexPredictionEndpoint)},&quot;hybridSearchConfig&quot;: {object (HybridSearchConfig)}// Union type}</code></pre></td>
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

## HybridSearchConfig

Config for hybrid search.

Fields

`sparseEmbeddingConfig` ` object ( SparseEmbeddingConfig  ` )

Optional. The configuration for sparse embedding generation. This field is optional the default behavior depends on the vector database choice on the RagCorpus.

`denseEmbeddingModelPredictionEndpoint` ` object ( VertexPredictionEndpoint  ` )

Required. The Agent Platform Prediction Endpoint that hosts the embedding model for dense embedding generations.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;sparseEmbeddingConfig&quot;: {object (SparseEmbeddingConfig)},&quot;denseEmbeddingModelPredictionEndpoint&quot;: {object (VertexPredictionEndpoint)}}</code></pre></td>
</tr>
</tbody>
</table>

## SparseEmbeddingConfig

Configuration for sparse emebdding generation.

Fields

`model` `Union type`

The model to use for sparse embedding generation. `model` can be only one of the following:

`bm25` ` object ( Bm25  ` )

Use BM25 scoring algorithm.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{// model&quot;bm25&quot;: {object (Bm25)}// Union type}</code></pre></td>
</tr>
</tbody>
</table>

## Bm25

message for BM25 parameters.

Fields

`multilingual` `boolean`

Optional. Use multilingual tokenizer if set to true.

`k1` `number`

Optional. The parameter to control term frequency saturation. It determines the scaling between the matching term frequency and final score. k1 is in the range of \[1.2, 3\]. The default value is 1.2.

`b` `number`

Optional. The parameter to control document length normalization. It determines how much the document length affects the final score. b is in the range of \[0, 1\]. The default value is 0.75.

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
  &quot;multilingual&quot;: boolean,
  &quot;k1&quot;: number,
  &quot;b&quot;: number
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

## CorpusTypeConfig

The config for the corpus type of the RagCorpus.

Fields

`corpus_type_config` `Union type`

Optional. Whether the RagCorpus is used as document store or memory store. `corpus_type_config` can be only one of the following:

`documentCorpus` ` object ( DocumentCorpus  ` )

Optional. Config for the document corpus.

`memoryCorpus` ` object ( MemoryCorpus  ` )

Optional. Config for the memory corpus.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{// corpus_type_config&quot;documentCorpus&quot;: {object (DocumentCorpus)},&quot;memoryCorpus&quot;: {object (MemoryCorpus)}// Union type}</code></pre></td>
</tr>
</tbody>
</table>

## DocumentCorpus

This type has no fields.

Config for the document corpus.

## MemoryCorpus

Config for the memory corpus.

Fields

`llmParser` ` object ( LlmParser  ` )

The LLM parser to use for the memory corpus.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;llmParser&quot;: {object (LlmParser)}}</code></pre></td>
</tr>
</tbody>
</table>

## LlmParser

Specifies the LLM parsing for RagFiles.

Fields

`modelName` `string`

The name of a LLM model used for parsing. Format: \* `projects/{projectId}/locations/{location}/publishers/{publisher}/models/{model}`

`maxParsingRequestsPerMin` `integer`

The maximum number of requests the job is allowed to make to the LLM model per minute. Consult <https://cloud.google.com/vertex-ai/generative-ai/docs/quotas> and your document size to set an appropriate value here. If unspecified, a default value of 5000 QPM would be used.

`globalMaxParsingRequestsPerMin` `integer`

The maximum number of requests the job is allowed to make to the LLM model per minute in this project. Consult <https://cloud.google.com/vertex-ai/generative-ai/docs/quotas> and your document size to set an appropriate value here. If this value is not specified, maxParsingRequestsPerMin will be used by indexing pipeline job as the global limit.

`customParsingPrompt` `string`

The prompt to use for parsing. If not specified, a default prompt will be used.

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
  &quot;modelName&quot;: string,
  &quot;maxParsingRequestsPerMin&quot;: integer,
  &quot;globalMaxParsingRequestsPerMin&quot;: integer,
  &quot;customParsingPrompt&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

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
