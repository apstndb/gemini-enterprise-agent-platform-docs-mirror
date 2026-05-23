---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/models/rag-api
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/models/rag-api
title: RAG Engine API
description: Reference for the RAG Engine on Gemini Enterprise Agent Platform API, which includes parameters and examples for corpus management, file management, and retrieval.
data_source: docs.cloud.google.com
---

The RAG Engine is a component of the Gemini Enterprise Agent Platform platform, which facilitates Retrieval-Augmented Generation (RAG). RAG Engine enables Large Language Models (LLMs) to access and incorporate data from external knowledge sources, such as documents and databases. By using RAG, LLMs can generate more accurate and informative LLM responses.

## Parameters list

This section lists the following:

| Parameters                                                                                                                                                               | Examples                                                                                                                                                   |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------- |
| See [Corpus management parameters](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/models/rag-api#corpus-management-params-api) .               | See [Corpus management examples](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/models/rag-api#corpus-management-examples-api) . |
| See [File management parameters](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/models/rag-api#file-management-params-api) .                   | See [File management examples](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/models/rag-api#file-management-examples-api) .     |
| See [Retrieval and prediction parameters](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/models/rag-api#retrieval-and-prediction-params-api) . | See [Retrieval query example](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/models/rag-api#retrieval-query-api) .               |
| See [Project management parameters](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/models/rag-api#project-management-params-api) .             | See [Project management examples](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/models/rag-api#project-management-params-api) . |

### Corpus management parameters

For information about a RAG corpus, see [Corpus management](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/rag-engine/manage-your-rag-corpus#corpus-management) .

#### Create a RAG corpus

This table lists the parameters used to create a RAG corpus.

##### Body Request

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th><strong>Parameters</strong></th>
<th><strong></strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr" translate="no">corpus_type_config</code></p></td>
<td><p>Optional: Immutable.</p>
<p><code dir="ltr" translate="no">RagCorpus.CorpusTypeConfig</code></p>
<p>The configuration to specify the corpus type.</p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr" translate="no">display_name</code></p></td>
<td><p>Required: <code dir="ltr" translate="no">string</code></p>
<p>The display name of the RAG corpus.</p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr" translate="no">description</code></p></td>
<td><p>Optional: <code dir="ltr" translate="no">string</code></p>
<p>The description of the RAG corpus.</p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr" translate="no">encryption_spec</code></p></td>
<td><p>Optional: Immutable: <code dir="ltr" translate="no">string</code></p>
<p>The CMEK key name is used to encrypt at-rest data that's related to the RAG corpus. The key name is only applicable to the <code dir="ltr" translate="no">RagManaged</code> option for the vector database. When the corpus is created, this field can be set and can't be updated or deleted.</p>
<p>Format: <code dir="ltr" translate="no">projects/{project}/locations/{location}/keyRings/{key_ring}/cryptoKeys/{key_name}</code></p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr" translate="no">vector_db_config</code></p></td>
<td><p>Optional: Immutable: <code dir="ltr" translate="no">RagVectorDbConfig</code></p>
<p>The configuration for the vector databases.</p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr" translate="no">vertex_ai_search_config.serving_config</code></p></td>
<td><p>Optional: <code dir="ltr" translate="no">string</code></p>
<p>The configuration for the Agent Search.</p>
<p>Format: <code dir="ltr" translate="no">projects/{project}/locations/{location}/collections/{collection}/engines/{engine}/servingConfigs/{serving_config}</code> or <code dir="ltr" translate="no">projects/{project}/locations/{location}/collections/{collection}/dataStores/{data_store}/servingConfigs/{serving_config}</code></p></td>
</tr>
</tbody>
</table>

##### `CorpusTypeConfig`

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th><strong>Parameters</strong></th>
<th><strong></strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr" translate="no">document_corpus</code></p></td>
<td><p><code dir="ltr" translate="no">oneof</code> <code dir="ltr" translate="no">RagCorpus.CorpusTypeConfig.DocumentCorpus</code></p>
<p>The default value of <code dir="ltr" translate="no">corpus_type_config</code> , which represents a conventional document-based RAG corpus.</p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr" translate="no">memory_corpus</code></p></td>
<td><p><code dir="ltr" translate="no">oneof</code> <code dir="ltr" translate="no">RagCorpus.CorpusTypeConfig.MemoryCorpus</code></p>
<p>If you set this type, the RAG corpus is a <code dir="ltr" translate="no">MemoryCorpus</code> that can be used with the Gemini Live API as a memory store.</p>
<p>For more information, see <a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/rag-engine/use-rag-in-multimodal-live#use-rag-memory-store">Use RAG Engine as the memory store</a> .</p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr" translate="no">memory_corpus.llm_parser</code></p></td>
<td><p><code dir="ltr" translate="no">oneof</code> <code dir="ltr" translate="no">RagFileParsingConfig.LlmParser</code></p>
<p>The LLM parser that's used to parse and store session contexts from the Gemini Live API. You can build memories for indexing.</p></td>
</tr>
</tbody>
</table>

##### `RagVectorDbConfig`

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th><strong>Parameters</strong></th>
<th><strong></strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr" translate="no">rag_managed_db</code></p></td>
<td><p><code dir="ltr" translate="no">oneof</code> <code dir="ltr" translate="no">vector_db</code> : <code dir="ltr" translate="no">RagVectorDbConfig.RagManagedDb</code></p>
<p>If no vector database is specified, <code dir="ltr" translate="no">rag_managed_db</code> is the default vector database.</p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr" translate="no">rag_managed_db.knn</code></p></td>
<td><p><code dir="ltr" translate="no">oneof</code> <code dir="ltr" translate="no">retrieval_strategy</code> : <code dir="ltr" translate="no">KNN</code></p>
<p>Default.</p>
<p>Finds the exact nearest neighbors by comparing all data points in your RAG corpus.</p>
<p>If you don't specify a strategy during the creation of your RAG corpus, KNN is the default retrieval strategy used.</p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr" translate="no">rag_managed_db.ann</code></p></td>
<td><p><code dir="ltr" translate="no">oneof</code> <code dir="ltr" translate="no">retrieval_strategy</code> : <code dir="ltr" translate="no">ANN</code></p>
<p><code dir="ltr" translate="no">tree_depth</code></p>
<p>Determines the number of layers or levels in the tree.</p>
If you have <code dir="ltr" translate="no">O(10K)</code> RAG files in the RAG corpus, set thi value to 2.
<ul>
<li>If more layers or levels are required, set this value to 3.</li>
<li>If the number of layers or levels isn't specified, RAG Engine assigns a default value of 2 for this parameter.</li>
</ul>
<p><code dir="ltr" translate="no">leaf_count</code></p>
<p>Determines the number of leaf nodes in the tree-based structure.</p>
<ul>
<li>The recommended value is <code dir="ltr" translate="no">10 * sqrt(num of RAG files in your RAG corpus)</code> .</li>
<li>If not specified, RAG Engine assigns a <em>default value of 500</em> for this parameter.</li>
</ul>
<p><code dir="ltr" translate="no">rebuild_ann_index</code></p>
<ul>
<li>RAG Engine rebuilds your ANN index.</li>
<li>Set to <code dir="ltr" translate="no">true</code> in your <code dir="ltr" translate="no">ImportRagFiles</code> API request.</li>
<li>Before you query the RAG corpus, it's required to rebuild the ANN index once.</li>
<li>Only one concurrent index rebuild is supported on a project in each location.</li>
</ul></td>
</tr>
<tr class="even">
<td><p><code dir="ltr" translate="no">weaviate</code></p></td>
<td><p><code dir="ltr" translate="no">oneof</code> <code dir="ltr" translate="no">vector_db</code> : <code dir="ltr" translate="no">RagVectorDbConfig.Weaviate</code></p>
<p>Specifies your Weaviate instance.</p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr" translate="no">weaviate.http_endpoint</code></p></td>
<td><p><code dir="ltr" translate="no">string</code></p>
<p>The Weaviate instance's HTTP endpoint.</p>
<p>This value can't be changed after it's set. You can leave it empty in the <code dir="ltr" translate="no">CreateRagCorpus</code> API call, and set it with a non-empty value in a follow up <code dir="ltr" translate="no">UpdateRagCorpus</code> API call.</p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr" translate="no">weaviate.collection_name</code></p></td>
<td><p><code dir="ltr" translate="no">string</code></p>
<p>The Weaviate collection that the RAG corpus maps to.</p>
<p>This value can't be changed after it's set. You can leave it empty in the <code dir="ltr" translate="no">CreateRagCorpus</code> API call, and set it with a non-empty value in a follow up <code dir="ltr" translate="no">UpdateRagCorpus</code> API call.</p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr" translate="no">pinecone</code></p></td>
<td><p><code dir="ltr" translate="no">oneof</code> <code dir="ltr" translate="no">vector_db</code> : <code dir="ltr" translate="no">RagVectorDbConfig.Pinecone</code></p>
<p>Specifies your Pinecone instance.</p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr" translate="no">pinecone.index_name</code></p></td>
<td><p><code dir="ltr" translate="no">string</code></p>
<p>This is the name used to create the Pinecone index that's used with the RAG corpus.</p>
<p>This value can't be changed after it's set. You can leave it empty in the <code dir="ltr" translate="no">CreateRagCorpus</code> API call, and set it with a non-empty value in a follow up <code dir="ltr" translate="no">UpdateRagCorpus</code> API call.</p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr" translate="no">vertex_feature_store</code></p></td>
<td><p><code dir="ltr" translate="no">oneof</code> <code dir="ltr" translate="no">vector_db</code> : <code dir="ltr" translate="no">RagVectorDbConfig.VertexFeatureStore</code></p>
<p>Specifies your Feature Store on Gemini Enterprise Agent Platform instance.</p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr" translate="no">vertex_feature_store.feature_view_resource_name</code></p></td>
<td><p><code dir="ltr" translate="no">string</code></p>
<p>The Agent Platform Feature Store <code dir="ltr" translate="no">FeatureView</code> that the RAG corpus maps to.</p>
<p>Format: <code dir="ltr" translate="no">projects/{project}/locations/{location}/featureOnlineStores/{feature_online_store}/featureViews/{feature_view}</code></p>
<p>This value can't be changed after it's set. You can leave it empty in the <code dir="ltr" translate="no">CreateRagCorpus</code> API call, and set it with a non-empty value in a follow up <code dir="ltr" translate="no">UpdateRagCorpus</code> API call.</p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr" translate="no">vertex_vector_search</code></p></td>
<td><p><code dir="ltr" translate="no">oneof</code> <code dir="ltr" translate="no">vector_db</code> : <code dir="ltr" translate="no">RagVectorDbConfig.VertexVectorSearch</code></p>
<p>Specifies your Vector Search on Gemini Enterprise Agent Platform instance.</p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr" translate="no">vertex_vector_search.index</code></p></td>
<td><p><code dir="ltr" translate="no">string</code></p>
<p>This is the resource name of the Vector Search index that's used with the RAG corpus.</p>
<p>Format: <code dir="ltr" translate="no">projects/{project}/locations/{location}/indexEndpoints/{index_endpoint}</code></p>
<p>This value can't be changed after it's set. You can leave it empty in the <code dir="ltr" translate="no">CreateRagCorpus</code> API call, and set it with a non-empty value in a follow up <code dir="ltr" translate="no">UpdateRagCorpus</code> API call.</p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr" translate="no">vertex_vector_search.index_endpoint</code></p></td>
<td><p><code dir="ltr" translate="no">string</code></p>
<p>This is the resource name of the Vector Search index endpoint that's used with the RAG corpus.</p>
<p>Format: <code dir="ltr" translate="no">projects/{project}/locations/{location}/indexes/{index}</code></p>
<p>This value can't be changed after it's set. You can leave it empty in the <code dir="ltr" translate="no">CreateRagCorpus</code> API call, and set it with a non-empty value in a follow up <code dir="ltr" translate="no">UpdateRagCorpus</code> API call.</p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr" translate="no">api_auth.api_key_config.api_key_secret_version</code></p></td>
<td><p><code dir="ltr" translate="no">string</code></p>
<p>This the full resource name of the secret that is stored in Secret Manager, which contains your Weaviate or Pinecone API key that depends on your choice of vector database.</p>
<p>Format: <code dir="ltr" translate="no">projects/{PROJECT_NUMBER}/secrets/{SECRET_ID}/versions/{VERSION_ID}</code></p>
<p>You can leave it empty in the <code dir="ltr" translate="no">CreateRagCorpus</code> API call, and set it with a non-empty value in a follow up <code dir="ltr" translate="no">UpdateRagCorpus</code> API call.</p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr" translate="no">rag_embedding_model_config.vertex_prediction_endpoint.endpoint</code></p></td>
<td><p>Optional: Immutable: <code dir="ltr" translate="no">string</code></p>
<p>The embedding model to use for the RAG corpus. This value can't be changed after it's set. If you leave it empty, we use <a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/models/text-embeddings-api">text-embedding-005</a> as the embedding model.</p></td>
</tr>
</tbody>
</table>

#### Update a RAG corpus

This table lists the parameters used to update a RAG corpus.

##### Body Request

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th><strong>Parameters</strong></th>
<th><strong></strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr" translate="no">display_name</code></p></td>
<td><p>Optional: <code dir="ltr" translate="no">string</code></p>
<p>The display name of the RAG corpus.</p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr" translate="no">description</code></p></td>
<td><p>Optional: <code dir="ltr" translate="no">string</code></p>
<p>The description of the RAG corpus.</p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr" translate="no">rag_vector_db.weaviate.http_endpoint</code></p></td>
<td><p><code dir="ltr" translate="no">string</code></p>
<p>The Weaviate instance's HTTP endpoint.</p>
<p>If your <code dir="ltr" translate="no">RagCorpus</code> was created with a <code dir="ltr" translate="no">Weaviate</code> configuration, and this field has never been set before, then you can update the Weaviate instance's HTTP endpoint.</p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr" translate="no">rag_vector_db.weaviate.collection_name</code></p></td>
<td><p><code dir="ltr" translate="no">string</code></p>
<p>The Weaviate collection that the RAG corpus maps to.</p>
<p>If your <code dir="ltr" translate="no">RagCorpus</code> was created with a <code dir="ltr" translate="no">Weaviate</code> configuration, and this field has never been set before, then you can update the Weaviate instance's collection name.</p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr" translate="no">rag_vector_db.pinecone.index_name</code></p></td>
<td><p><code dir="ltr" translate="no">string</code></p>
<p>This is the name used to create the Pinecone index that's used with the RAG corpus.</p>
<p>If your <code dir="ltr" translate="no">RagCorpus</code> was created with a <code dir="ltr" translate="no">Pinecone</code> configuration, and this field has never been set before, then you can update the Pinecone instance's index name.</p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr" translate="no">rag_vector_db.vertex_feature_store.feature_view_resource_name</code></p></td>
<td><p><code dir="ltr" translate="no">string</code></p>
<p>The Agent Platform Feature Store <code dir="ltr" translate="no">FeatureView</code> that the RAG corpus maps to.</p>
<p>Format: <code dir="ltr" translate="no">projects/{project}/locations/{location}/featureOnlineStores/{feature_online_store}/featureViews/{feature_view}</code></p>
<p>If your <code dir="ltr" translate="no">RagCorpus</code> was created with a Agent Platform Feature Store configuration, and this field has never been set before, then you can update it.</p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr" translate="no">rag_vector_db.vertex_vector_search.index</code></p></td>
<td><p><code dir="ltr" translate="no">string</code></p>
<p>This is the resource name of the Vector Search index that's used with the RAG corpus.</p>
<p>Format: <code dir="ltr" translate="no">projects/{project}/locations/{location}/indexEndpoints/{index_endpoint}</code></p>
<p>If your <code dir="ltr" translate="no">RagCorpus</code> was created with a <code dir="ltr" translate="no">Vector Search</code> configuration, and this field has never been set before, then you can update it.</p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr" translate="no">rag_vector_db.vertex_vector_search.index_endpoint</code></p></td>
<td><p><code dir="ltr" translate="no">string</code></p>
<p>This is the resource name of the Vector Search index endpoint that's used with the RAG corpus.</p>
<p>Format: <code dir="ltr" translate="no">projects/{project}/locations/{location}/indexes/{index}</code></p>
<p>If your <code dir="ltr" translate="no">RagCorpus</code> was created with a <code dir="ltr" translate="no">Vector Search</code> configuration, and this field has never been set before, then you can update it.</p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr" translate="no">rag_vector_db.api_auth.api_key_config.api_key_secret_version</code></p></td>
<td><p><code dir="ltr" translate="no">string</code></p>
<p>The full resource name of the secret that is stored in Secret Manager, which contains your Weaviate or Pinecone API key depends on your choice of vector database.</p>
<p>Format: <code dir="ltr" translate="no">projects/{PROJECT_NUMBER}/secrets/{SECRET_ID}/versions/{VERSION_ID}</code></p></td>
</tr>
</tbody>
</table>

#### List RAG corpora

This table lists the parameters used to list RAG corpora.

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th><strong>Parameters</strong></th>
<th><strong></strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr" translate="no">page_size</code></p></td>
<td><p>Optional: <code dir="ltr" translate="no">int</code></p>
<p>The standard list page size.</p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr" translate="no">page_token</code></p></td>
<td><p>Optional: <code dir="ltr" translate="no">string</code></p>
<p>The standard list page token. Typically obtained from <code dir="ltr" translate="no">[ListRagCorporaResponse.next_page_token][]</code> of the previous <code dir="ltr" translate="no">[VertexRagDataService.ListRagCorpora][]</code> call.</p></td>
</tr>
</tbody>
</table>

#### Get a RAG corpus

This table lists parameters used to get a RAG corpus.

Parameters

`name`

`string`

The name of the `RagCorpus` resource. Format: `projects/{project}/locations/{location}/ragCorpora/{rag_corpus_id}`

#### Delete a RAG corpus

This table lists parameters used to delete a RAG corpus.

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th><strong>Parameters</strong></th>
<th><strong></strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr" translate="no">name</code></p></td>
<td><p><code dir="ltr" translate="no">string</code></p>
<p>The name of the <code dir="ltr" translate="no">RagCorpus</code> resource. Format: <code dir="ltr" translate="no">projects/{project}/locations/{location}/ragCorpora/{rag_corpus_id}</code></p></td>
</tr>
</tbody>
</table>

#### Batch create metadata schemas

This table lists the parameters used to batch create metadata schemas for a RAG corpus.

##### Body Request

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th><strong>Parameters</strong></th>
<th><strong></strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr" translate="no">requests</code></p></td>
<td><p>Required: list of <code dir="ltr" translate="no">CreateRagDataSchemaRequest</code></p>
<p>The request messages for <code dir="ltr" translate="no">CreateRagDataSchema</code> .</p></td>
</tr>
</tbody>
</table>

##### `CreateRagDataSchemaRequest`

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th><strong>Parameters</strong></th>
<th><strong></strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr" translate="no">rag_data_schema</code></p></td>
<td><p>Required: <code dir="ltr" translate="no">RagDataSchema</code></p>
<p>The metadata schema to create.</p></td>
</tr>
</tbody>
</table>

##### `RagDataSchema`

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th><strong>Parameters</strong></th>
<th><strong></strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr" translate="no">key</code></p></td>
<td><p>Required: <code dir="ltr" translate="no">string</code></p>
<p>The key of the metadata schema.</p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr" translate="no">schema_details</code></p></td>
<td><p><code dir="ltr" translate="no">RagMetadataSchemaDetails</code></p>
<p>The details of the metadata schema.</p></td>
</tr>
</tbody>
</table>

##### `RagMetadataSchemaDetails`

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th><strong>Parameters</strong></th>
<th><strong></strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr" translate="no">type</code></p></td>
<td><p><code dir="ltr" translate="no">DataType</code></p>
<p>The data type of the metadata schema. Options: <code dir="ltr" translate="no">INTEGER</code> , <code dir="ltr" translate="no">FLOAT</code> , <code dir="ltr" translate="no">STRING</code> , <code dir="ltr" translate="no">DATETIME</code> , <code dir="ltr" translate="no">BOOLEAN</code> , <code dir="ltr" translate="no">LIST</code> .</p></td>
</tr>
</tbody>
</table>

#### List metadata schemas

This table lists the parameters used to list metadata schemas.

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th><strong>Parameters</strong></th>
<th><strong>Description</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr" translate="no">parent</code></p></td>
<td><p>Required: <code dir="ltr" translate="no">string</code></p>
<p>The resource name of the <code dir="ltr" translate="no">RagCorpus</code> . Format: <code dir="ltr" translate="no">projects/{project}/locations/{location}/ragCorpora/{rag_corpus_id}</code></p></td>
</tr>
</tbody>
</table>

#### Batch delete metadata schemas

This table lists the parameters used to batch delete metadata schemas.

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th><strong>Parameters</strong></th>
<th><strong></strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr" translate="no">names</code></p></td>
<td><p>Required: list of <code dir="ltr" translate="no">string</code></p>
<p>The resource names of the <code dir="ltr" translate="no">RagDataSchema</code> to delete. Format: <code dir="ltr" translate="no">projects/{project}/locations/{location}/ragCorpora/{rag_corpus_id}/ragDataSchemas/{rag_data_schema_id}</code></p></td>
</tr>
</tbody>
</table>

### File management parameters

For information about a RAG file and its metadata, see [File management](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/rag-engine/manage-your-rag-corpus#file-management) .

#### Upload a RAG file

This table lists parameters used to upload a RAG file.

##### Body Request

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th><strong>Parameters</strong></th>
<th><strong></strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr" translate="no">parent</code></p></td>
<td><p><code dir="ltr" translate="no">string</code></p>
<p>The name of the <code dir="ltr" translate="no">RagCorpus</code> resource. Format: <code dir="ltr" translate="no">projects/{project}/locations/{location}/ragCorpora/{rag_corpus_id}</code></p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr" translate="no">rag_file</code></p></td>
<td><p>Required: <code dir="ltr" translate="no">RagFile</code></p>
<p>The file to upload.</p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr" translate="no">upload_rag_file_config</code></p></td>
<td><p>Required: <code dir="ltr" translate="no">UploadRagFileConfig</code></p>
<p>The configuration for the <code dir="ltr" translate="no">RagFile</code> to be uploaded into the <code dir="ltr" translate="no">RagCorpus</code> .</p></td>
</tr>
</tbody>
</table>

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th><code dir="ltr" translate="no">RagFile</code></th>
<th><strong>Description</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr" translate="no">display_name</code></p></td>
<td><p>Required: <code dir="ltr" translate="no">string</code></p>
<p>The display name of the RAG file.</p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr" translate="no">description</code></p></td>
<td><p>Optional: <code dir="ltr" translate="no">string</code></p>
<p>The description of the RAG file.</p></td>
</tr>
</tbody>
</table>

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th><code dir="ltr" translate="no">UploadRagFileConfig</code></th>
<th><strong>Description</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr" translate="no">rag_file_transformation_config.rag_file_chunking_config.fixed_length_chunking.chunk_size</code></p></td>
<td><p><code dir="ltr" translate="no">int32</code></p>
<p>Number of tokens each chunk has.</p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr" translate="no">rag_file_transformation_config.rag_file_chunking_config.fixed_length_chunking.chunk_overlap</code></p></td>
<td><p><code dir="ltr" translate="no">int32</code></p>
<p>The overlap between chunks.</p></td>
</tr>
</tbody>
</table>

#### Import RAG files

This table lists parameters used to import a RAG file.

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th><strong>Parameters</strong></th>
<th><strong></strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr" translate="no">parent</code></p></td>
<td><p>Required: <code dir="ltr" translate="no">string</code></p>
<p>The name of the <code dir="ltr" translate="no">RagCorpus</code> resource.</p>
<p>Format: <code dir="ltr" translate="no">projects/{project}/locations/{location}/ragCorpora/{rag_corpus_id}</code></p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr" translate="no">gcs_source</code></p></td>
<td><p><code dir="ltr" translate="no">oneof</code> <code dir="ltr" translate="no">import_source</code> : <code dir="ltr" translate="no">GcsSource</code></p>
<p>Cloud Storage location.</p>
<p>Supports importing individual files as well as entire Cloud Storage directories.</p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr" translate="no">gcs_source.uris</code></p></td>
<td><p><code dir="ltr" translate="no">list</code> of <code dir="ltr" translate="no">string</code></p>
<p>Cloud Storage URI that contains the upload file.</p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr" translate="no">google_drive_source</code></p></td>
<td><p><code dir="ltr" translate="no">oneof</code> <code dir="ltr" translate="no">import_source</code> : <code dir="ltr" translate="no">GoogleDriveSource</code></p>
<p>Google Drive location.</p>
<p>Supports importing individual files as well as Google Drive folders.</p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr" translate="no">slack_source</code></p></td>
<td><p><code dir="ltr" translate="no">oneof</code> <code dir="ltr" translate="no">import_source</code> : <code dir="ltr" translate="no">SlackSource</code></p>
<p>The slack channel where the file is uploaded.</p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr" translate="no">jira_source</code></p></td>
<td><p><code dir="ltr" translate="no">oneof</code> <code dir="ltr" translate="no">import_source</code> : <code dir="ltr" translate="no">JiraSource</code></p>
<p>The Jira query where the file is uploaded.</p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr" translate="no">share_point_sources</code></p></td>
<td><p><code dir="ltr" translate="no">oneof</code> <code dir="ltr" translate="no">import_source</code> : <code dir="ltr" translate="no">SharePointSources</code></p>
<p>The SharePoint sources where the file is uploaded.</p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr" translate="no">rag_file_transformation_config.rag_file_chunking_config.fixed_length_chunking.chunk_size</code></p></td>
<td><p><code dir="ltr" translate="no">int32</code></p>
<p>Number of tokens each chunk has.</p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr" translate="no">rag_file_transformation_config.rag_file_chunking_config.fixed_length_chunking.chunk_overlap</code></p></td>
<td><p><code dir="ltr" translate="no">int32</code></p>
<p>The overlap between chunks.</p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr" translate="no">rag_file_parsing_config</code></p></td>
<td><p>Optional: <code dir="ltr" translate="no">RagFileParsingConfig</code></p>
<p>Specifies the parsing configuration for <code dir="ltr" translate="no">RagFiles</code> .</p>
<p>If this field isn't set, RAG uses the default parser.</p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr" translate="no">max_embedding_requests_per_min</code></p></td>
<td><p>Optional: <code dir="ltr" translate="no">int32</code></p>
<p>The maximum number of queries per minute that this job is allowed to make to the embedding model specified on the corpus. This value is specific to this job and not shared across other import jobs. Consult the Quotas page on the project to set an appropriate value.</p>
<p>If unspecified, a default value of 1,000 QPM is used.</p></td>
</tr>
</tbody>
</table>

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th><code dir="ltr" translate="no">GoogleDriveSource</code></th>
<th><strong></strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr" translate="no">resource_ids.resource_id</code></p></td>
<td><p>Required: <code dir="ltr" translate="no">string</code></p>
<p>The ID of the Google Drive resource.</p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr" translate="no">resource_ids.resource_type</code></p></td>
<td><p>Required: <code dir="ltr" translate="no">string</code></p>
<p>The type of the Google Drive resource.</p></td>
</tr>
</tbody>
</table>

`SlackSource`

`channels.channels`

Repeated: `SlackSource.SlackChannels.SlackChannel`

Slack channel information, include ID and time range to import.

`channels.channels.channel_id`

Required: `string`

The Slack channel ID.

`channels.channels.start_time`

Optional: `google.protobuf.Timestamp`

The starting timestamp for messages to import.

`channels.channels.end_time`

Optional: `google.protobuf.Timestamp`

The ending timestamp for messages to import.

`channels.api_key_config.api_key_secret_version`

Required: `string`

The full resource name of the secret that is stored in Secret Manager, which contains a Slack channel access token that has access to the slack channel IDs.  
See: https://api.slack.com/tutorials/tracks/getting-a-token.

Format: `projects/{PROJECT_NUMBER}/secrets/{SECRET_ID}/versions/{VERSION_ID}`

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th><code dir="ltr" translate="no">JiraSource</code></th>
<th><strong></strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr" translate="no">jira_queries.projects</code></p></td>
<td><p>Repeated: <code dir="ltr" translate="no">string</code></p>
<p>A list of Jira projects to import in their entirety.</p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr" translate="no">jira_queries.custom_queries</code></p></td>
<td><p>Repeated: <code dir="ltr" translate="no">string</code></p>
<p>A list of custom Jira queries to import. For information about JQL (Jira Query Language), see<br />
<a href="https://support.atlassian.com/jira-service-management-cloud/docs/use-advanced-search-with-jira-query-language-jql/">Jira Support</a></p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr" translate="no">jira_queries.email</code></p></td>
<td><p>Required: <code dir="ltr" translate="no">string</code></p>
<p>The Jira email address.</p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr" translate="no">jira_queries.server_uri</code></p></td>
<td><p>Required: <code dir="ltr" translate="no">string</code></p>
<p>The Jira server URI.</p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr" translate="no">jira_queries.api_key_config.api_key_secret_version</code></p></td>
<td><p>Required: <code dir="ltr" translate="no">string</code></p>
<p>The full resource name of the secret that is stored in Secret Manager, which contains Jira API key that has access to the slack channel IDs.<br />
See: https://support.atlassian.com/atlassian-account/docs/manage-api-tokens-for-your-atlassian-account/</p>
<p>Format: <code dir="ltr" translate="no">projects/{PROJECT_NUMBER}/secrets/{SECRET_ID}/versions/{VERSION_ID}</code></p></td>
</tr>
</tbody>
</table>

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th><code dir="ltr" translate="no">SharePointSources</code></th>
<th><strong></strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr" translate="no">share_point_sources.sharepoint_folder_path</code></p></td>
<td><p><code dir="ltr" translate="no">oneof</code> in <code dir="ltr" translate="no">folder_source</code> : <code dir="ltr" translate="no">string</code></p>
<p>The path of the SharePoint folder to download from.</p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr" translate="no">share_point_sources.sharepoint_folder_id</code></p></td>
<td><p><code dir="ltr" translate="no">oneof</code> in <code dir="ltr" translate="no">folder_source</code> : <code dir="ltr" translate="no">string</code></p>
<p>The ID of the SharePoint folder to download from.</p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr" translate="no">share_point_sources.drive_name</code></p></td>
<td><p><code dir="ltr" translate="no">oneof</code> in <code dir="ltr" translate="no">drive_source</code> : <code dir="ltr" translate="no">string</code></p>
<p>The name of the drive to download from.</p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr" translate="no">share_point_sources.drive_id</code></p></td>
<td><p><code dir="ltr" translate="no">oneof</code> in <code dir="ltr" translate="no">drive_source</code> : <code dir="ltr" translate="no">string</code></p>
<p>The ID of the drive to download from.</p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr" translate="no">share_point_sources.client_id</code></p></td>
<td><p><code dir="ltr" translate="no">string</code></p>
<p>The Application ID for the app registered in Microsoft Azure Portal.<br />
The application must also be configured with MS Graph permissions "Files.ReadAll", "Sites.ReadAll" and BrowserSiteLists.Read.All.</p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr" translate="no">share_point_sources.client_secret.api_key_secret_version</code></p></td>
<td><p>Required: <code dir="ltr" translate="no">string</code></p>
<p>The full resource name of the secret that is stored in Secret Manager, which contains the application secret for the app registered in Azure.</p>
<p>Format: <code dir="ltr" translate="no">projects/{PROJECT_NUMBER}/secrets/{SECRET_ID}/versions/{VERSION_ID}</code></p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr" translate="no">share_point_sources.tenant_id</code></p></td>
<td><p><code dir="ltr" translate="no">string</code></p>
<p>Unique identifier of the Azure Active Directory Instance.</p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr" translate="no">share_point_sources.sharepoint_site_name</code></p></td>
<td><p><code dir="ltr" translate="no">string</code></p>
<p>The name of the SharePoint site to download from. This can be the site name or the site id.</p></td>
</tr>
</tbody>
</table>

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th><code dir="ltr" translate="no">RagFileParsingConfig</code></th>
<th><strong></strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr" translate="no">layout_parser</code></p></td>
<td><p><code dir="ltr" translate="no">oneof</code> <code dir="ltr" translate="no">parser</code> : <code dir="ltr" translate="no">RagFileParsingConfig.LayoutParser</code></p>
<p>The Layout Parser to use for <code dir="ltr" translate="no">RagFile</code> s.</p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr" translate="no">layout_parser.processor_name</code></p></td>
<td><p><code dir="ltr" translate="no">string</code></p>
<p>The full resource name of a Document AI processor or processor version.</p>
<p>Format:<br />
<code dir="ltr" translate="no">projects/{project_id}/locations/{location}/processors/{processor_id}</code><br />
<code dir="ltr" translate="no">projects/{project_id}/locations/{location}/processors/{processor_id}/processorVersions/{processor_version_id}</code></p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr" translate="no">layout_parser.max_parsing_requests_per_min</code></p></td>
<td><p><code dir="ltr" translate="no">string</code></p>
<p>The maximum number of requests the job is allowed to make to the Document AI processor per minute.</p>
<p>Consult https://cloud.google.com/document-ai/quotas and the Quota page for your project to set an appropriate value here. If unspecified, a default value of 120 QPM is used.</p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr" translate="no">llm_parser</code></p></td>
<td><p><code dir="ltr" translate="no">oneof</code> <code dir="ltr" translate="no">parser</code> : <code dir="ltr" translate="no">RagFileParsingConfig.LlmParser</code></p>
<p>The LLM parser to use for <code dir="ltr" translate="no">RagFile</code> s.</p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr" translate="no">llm_parser.model_name</code></p></td>
<td><p><code dir="ltr" translate="no">string</code></p>
<p>The resource name of an LLM model.</p>
<p>Format:<br />
<code dir="ltr" translate="no">{publisher}/models/{model}</code></p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr" translate="no">llm_parser.max_parsing_requests_per_min</code></p></td>
<td><p><code dir="ltr" translate="no">string</code></p>
<p>The maximum number of requests the job is allowed to make to the LLM model per minute.</p>
<p>To set an appropriate value for your project, see the <a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/quotas#quota_system_by_model">model quota section</a> and the Quota page for your project to set an appropriate value here. If unspecified, a default value of 5000 QPM is used.</p></td>
</tr>
</tbody>
</table>

#### Get a RAG file

This table lists parameters used to get a RAG file.

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th><strong>Parameters</strong></th>
<th><strong></strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr" translate="no">name</code></p></td>
<td><p><code dir="ltr" translate="no">string</code></p>
<p>The name of the <code dir="ltr" translate="no">RagFile</code> resource. Format: <code dir="ltr" translate="no">projects/{project}/locations/{location}/ragCorpora/{rag_file_id}</code></p></td>
</tr>
</tbody>
</table>

#### Delete a RAG file

This table lists parameters used to delete a RAG file.

Parameters

`name`

`string`

The name of the `RagFile` resource. Format: `projects/{project}/locations/{location}/ragCorpora/{rag_file_id}`

#### Batch create metadata

This table lists the parameters used to batch create metadata for a RAG file.

##### Body Request

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th><strong>Parameters</strong></th>
<th><strong></strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr" translate="no">requests</code></p></td>
<td><p>Required: list of <code dir="ltr" translate="no">CreateRagMetadataRequest</code></p>
<p>The request messages for <code dir="ltr" translate="no">CreateRagMetadata</code> .</p></td>
</tr>
</tbody>
</table>

##### `CreateRagMetadataRequest`

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th><strong>Parameters</strong></th>
<th><strong></strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr" translate="no">rag_metadata</code></p></td>
<td><p>Required: <code dir="ltr" translate="no">RagMetadata</code></p>
<p>The metadata to create.</p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr" translate="no">rag_metadata_id</code></p></td>
<td><p>Optional: <code dir="ltr" translate="no">string</code></p>
<p>The ID to use for the metadata, which will become the final component of the metadata's resource name.</p></td>
</tr>
</tbody>
</table>

##### `RagMetadata`

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th><strong>Parameters</strong></th>
<th><strong></strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr" translate="no">user_specified_metadata</code></p></td>
<td><p><code dir="ltr" translate="no">UserSpecifiedMetadata</code></p>
<p>The metadata provided by users.</p></td>
</tr>
</tbody>
</table>

##### `UserSpecifiedMetadata`

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th><strong>Parameters</strong></th>
<th><strong></strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr" translate="no">key</code></p></td>
<td><p>Required: <code dir="ltr" translate="no">string</code></p>
<p>The key of the metadata. The key must correspond to a key defined in a <code dir="ltr" translate="no">RagDataSchema</code> .</p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr" translate="no">value</code></p></td>
<td><p><code dir="ltr" translate="no">MetadataValue</code></p>
<p>The value of the metadata.</p></td>
</tr>
</tbody>
</table>

##### `MetadataValue`

| **Parameters**   | ****                           |
| ---------------- | ------------------------------ |
| `int_value`      | `oneof value` : `int64`        |
| `float_value`    | `oneof value` : `float`        |
| `str_value`      | `oneof value` : `string`       |
| `datetime_value` | `oneof value` : `string`       |
| `bool_value`     | `oneof value` : `boolean`      |
| `list_value`     | `oneof value` : `MetadataList` |

#### List metadata

This table lists the parameters used to list metadata for a RAG file.

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th><strong>Parameters</strong></th>
<th><strong></strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr" translate="no">parent</code></p></td>
<td><p>Required: <code dir="ltr" translate="no">string</code></p>
<p>The resource name of the <code dir="ltr" translate="no">RagFile</code> . Format: <code dir="ltr" translate="no">projects/{project}/locations/{location}/ragCorpora/{rag_corpus_id}/ragFiles/{rag_file_id}</code></p></td>
</tr>
</tbody>
</table>

#### Update metadata

This table lists the parameters used to update metadata.

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th><strong>Parameters</strong></th>
<th><strong></strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr" translate="no">rag_metadata</code></p></td>
<td><p>Required: <code dir="ltr" translate="no">RagMetadata</code></p>
<p>The <code dir="ltr" translate="no">RagMetadata</code> which replaces the resource on the server.</p></td>
</tr>
</tbody>
</table>

#### Batch delete metadata

This table lists the parameters used to batch delete metadata.

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th><strong>Parameters</strong></th>
<th><strong></strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr" translate="no">names</code></p></td>
<td><p>Required: list of <code dir="ltr" translate="no">string</code></p>
<p>The resource names of the <code dir="ltr" translate="no">RagMetadata</code> to delete. Format: <code dir="ltr" translate="no">projects/{project}/locations/{location}/ragCorpora/{rag_corpus_id}/ragFiles/{rag_file_id}/ragMetadata/{rag_metadata_id}</code></p></td>
</tr>
</tbody>
</table>

### Retrieval and prediction parameters

This section lists the retrieval and prediction parameters.

#### Retrieval parameters

This table lists parameters for `retrieveContexts` API.

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th><strong>Parameters</strong></th>
<th><strong></strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr" translate="no">parent</code></p></td>
<td><p>Required: <code dir="ltr" translate="no">string</code></p>
<p>The resource name of the Location to perform the retrieval.<br />
The users must have permission to make a call in the project.</p>
<p>Format: <code dir="ltr" translate="no">projects/{project}/locations/{location}</code></p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr" translate="no">vertex_rag_store</code></p></td>
<td><p><code dir="ltr" translate="no">VertexRagStore</code></p>
<p>The data source for RagStore.</p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr" translate="no">query</code></p></td>
<td><p>Required: <code dir="ltr" translate="no">RagQuery</code></p>
<p>Single RAG retrieve query.</p></td>
</tr>
</tbody>
</table>

##### `VertexRagStore`

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th><code dir="ltr" translate="no">VertexRagStore</code></th>
<th><strong></strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr" translate="no">rag_resources</code></p></td>
<td><p>list: <code dir="ltr" translate="no">RagResource</code></p>
<p>The representation of the RAG source. It can be used to specify the corpus only or <code dir="ltr" translate="no">RagFile</code> s. Only support one corpus or multiple files from one corpus.</p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr" translate="no">rag_resources.rag_corpus</code></p></td>
<td><p>Optional: <code dir="ltr" translate="no">string</code></p>
<p><code dir="ltr" translate="no">RagCorpora</code> resource name.</p>
<p>Format: <code dir="ltr" translate="no">projects/{project}/locations/{location}/ragCorpora/{rag_corpus}</code></p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr" translate="no">rag_resources.rag_file_ids</code></p></td>
<td><p>list: <code dir="ltr" translate="no">string</code></p>
<p>A list of <code dir="ltr" translate="no">RagFile</code> resources.</p>
<p>Format: <code dir="ltr" translate="no">projects/{project}/locations/{location}/ragCorpora/{rag_corpus}/ragFiles/{rag_file}</code></p></td>
</tr>
</tbody>
</table>

`RagQuery`

`text`

`string`

The query in text format to get relevant contexts.

`rag_retrieval_config`

Optional: `RagRetrievalConfig`

The retrieval configuration for the query.

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th><code dir="ltr" translate="no">RagRetrievalConfig</code></th>
<th><strong></strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr" translate="no">top_k</code></p></td>
<td><p>Optional: <code dir="ltr" translate="no">int32</code></p>
<p>The number of contexts to retrieve.</p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr" translate="no">hybrid_search.alpha</code></p></td>
<td><p>Optional: <code dir="ltr" translate="no">float</code></p>
<p>Alpha value controls the weight between dense and sparse vector search results. The range is [0, 1], where 0 means sparse vector search only and 1 means dense vector search only. The default value is 0.5, which balances sparse and dense vector search equally.</p>
<p>Hybrid Search is only available for Weaviate.</p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr" translate="no">filter.vector_distance_threshold</code></p></td>
<td><p><code dir="ltr" translate="no">oneof vector_db_threshold</code> : <code dir="ltr" translate="no">double</code></p>
<p>Only returns contexts with a vector distance smaller than the threshold.</p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr" translate="no">filter.metadata_filter</code></p></td>
<td><p>Optional: <code dir="ltr" translate="no">string</code></p>
<p>The metadata filter to apply during retrieval, using Common Expression Language (CEL). For more information, see [Metadata search](/gemini-enterprise-agent-platform/build/rag-engine/use-metadata-search).</p>
<p>Example: <code dir="ltr" translate="no">author == "Shakespeare" &amp;&amp; page_number == 42</code></p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr" translate="no">filter.vector_similarity_threshold</code></p></td>
<td><p><code dir="ltr" translate="no">oneof vector_db_threshold</code> : <code dir="ltr" translate="no">double</code></p>
<p>Only returns contexts with vector similarity larger than the threshold.</p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr" translate="no">ranking.rank_service.model_name</code></p></td>
<td><p>Optional: <code dir="ltr" translate="no">string</code></p>
<p>The model name of the rank service.</p>
<p>Example: <code dir="ltr" translate="no">semantic-ranker-512@latest</code></p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr" translate="no">ranking.llm_ranker.model_name</code></p></td>
<td><p>Optional: <code dir="ltr" translate="no">string</code></p>
<p>The model name used for ranking.</p>
<p>Example: <code dir="ltr" translate="no">gemini-2.5-flash</code></p></td>
</tr>
</tbody>
</table>

#### Async retrieval parameters

This table lists parameters for `asyncRetrieveContexts` API.

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th><strong>Parameters</strong></th>
<th><strong></strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr" translate="no">parent</code></p></td>
<td><p>Required: <code dir="ltr" translate="no">string</code></p>
<p>The resource name of the Location to retrieve <code dir="ltr" translate="no">RagContexts</code> .<br />
The users must have permission to make a call in the project.</p>
<p>Format: <code dir="ltr" translate="no">projects/{project}/locations/{location}</code></p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr" translate="no">query</code></p></td>
<td><p>Required: <code dir="ltr" translate="no">RagQuery</code></p>
<p>Single RAG retrieve query.</p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr" translate="no">tools</code></p></td>
<td><p>Optional: list of <code dir="ltr" translate="no">Tool</code></p>
<p>The tools to use for retrieval. Supported tools include <code dir="ltr" translate="no">retrieval</code> which specifies the <code dir="ltr" translate="no">vertex_rag_store</code> .</p></td>
</tr>
</tbody>
</table>

#### Ask contexts parameters

This table lists parameters for `askContexts` API.

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th><strong>Parameters</strong></th>
<th><strong></strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr" translate="no">parent</code></p></td>
<td><p>Required: <code dir="ltr" translate="no">string</code></p>
<p>The resource name of the Location to retrieve <code dir="ltr" translate="no">RagContexts</code> .<br />
The users must have permission to make a call in the project.</p>
<p>Format: <code dir="ltr" translate="no">projects/{project}/locations/{location}</code></p></td>
</tr>
<tr class="even">
<td><p><code dir="ltr" translate="no">query</code></p></td>
<td><p>Required: <code dir="ltr" translate="no">RagQuery</code></p>
<p>Single RAG retrieve query.</p></td>
</tr>
<tr class="odd">
<td><p><code dir="ltr" translate="no">tools</code></p></td>
<td><p>Optional: list of <code dir="ltr" translate="no">Tool</code></p>
<p>The tools to use for retrieval. Supported tools include <code dir="ltr" translate="no">retrieval</code> which specifies the <code dir="ltr" translate="no">vertex_rag_store</code> .</p></td>
</tr>
</tbody>
</table>

#### Prediction parameters

This table lists prediction parameters.

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th><code dir="ltr" translate="no">GenerateContentRequest</code></th>
<th><strong></strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr" translate="no">tools.retrieval.vertex_rag_store</code></p></td>
<td><p><code dir="ltr" translate="no">VertexRagStore</code></p>
<p>Set to use a data source powered by Agent Platform RAG store.</p></td>
</tr>
</tbody>
</table>

See [VertexRagStore](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/models/rag-api#ragStore) for details.

### Project management parameters

This table lists project-level parameters.

##### `RagEngineConfig`

| **Parameters**                             | ****                                                                                                                                       |
| ------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------ |
| `RagManagedDbConfig.serverless`            | Sets/Switches the deployment mode to Serverless, providing a fully-managed and highly scalable database to back your RAG Engine resources. |
| `RagManagedDbConfig.spanner`               | Sets/Switches the deployment mode to Spanner, backed by a production-ready Spanner instance.                                               |
| `RagManagedDbConfig.spanner.scaled`        | This tier offers production-scale performance along with autoscaling functionality under Spanner mode.                                     |
| `RagManagedDbConfig.spanner.basic`         | This tier offers a cost-effective and low-compute tier under Spanner mode.                                                                 |
| `RagManagedDbConfig.spanner.unprovisioned` | This tier deletes the `RagManagedDb` and its underlying Spanner instance.                                                                  |

## Corpus management examples

This section provides examples of how to use the API to manage your RAG corpus.

### Create a RAG corpus example

This code sample demonstrates how to create a RAG corpus.

### REST

Before using any of the request data, make the following replacements:

  - PROJECT\_ID : Your \[project ID\](/resource-manager/docs/creating-managing-projects\#identifiers). .
  - LOCATION : The region to process the request.
  - CORPUS\_DISPLAY\_NAME : The display name of the `RagCorpus` .
  - CORPUS\_DESCRIPTION : The description of the `RagCorpus` .

HTTP method and URL:

    POST https://LOCATION-aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/LOCATION/ragCorpora

Request JSON body:

    {
      "display_name" : "CORPUS_DISPLAY_NAME",
      "description": "CORPUS_DESCRIPTION",
    }

To send your request, choose one of these options:

#### curl

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) , or by using [Cloud Shell](https://docs.cloud.google.com/shell/docs) , which automatically logs you into the `gcloud` CLI . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Save the request body in a file named `request.json` , and execute the following command:

    curl -X POST \
         -H "Authorization: Bearer $(gcloud auth print-access-token)" \
         -H "Content-Type: application/json; charset=utf-8" \
         -d @request.json \
         "https://LOCATION-aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/LOCATION/ragCorpora"

#### PowerShell

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Save the request body in a file named `request.json` , and execute the following command:

    $cred = gcloud auth print-access-token
    $headers = @{ "Authorization" = "Bearer $cred" }
    
    Invoke-WebRequest `
        -Method POST `
        -Headers $headers `
        -ContentType: "application/json; charset=utf-8" `
        -InFile request.json `
        -Uri "https://LOCATION-aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/LOCATION/ragCorpora" | Select-Object -Expand Content

You should receive a successful status code (2xx).

The following example demonstrates how to create a RAG corpus by using the REST API.

``` 
  PROJECT_ID: Your project ID.
  LOCATION: The region to process the request.
  CORPUS_DISPLAY_NAME: The display name of the <code>RagCorpus</code>.
```

``` 
    // CreateRagCorpus
    // Input: LOCATION, PROJECT_ID, CORPUS_DISPLAY_NAME
    // Output: CreateRagCorpusOperationMetadata
    curl -X POST \
    -H "Authorization: Bearer $(gcloud auth print-access-token)" \
    -H "Content-Type: application/json" \
    https://LOCATION-aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/LOCATION/ragCorpora \
    -d '{
          "display_name" : "CORPUS_DISPLAY_NAME"
      }'
```

### Update a RAG corpus example

You can update your RAG corpus with a new display name, description, and vector database configuration. However, you can't change the following [parameters](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/models/rag-api#update-a-rag-corpus-params-api) in your RAG corpus:

  - The vector database type. For example, you can't change the vector database from Weaviate to Agent Platform Feature Store.
  - If you're using the managed database option, you can't update the vector database configuration.

These examples demonstrate how to update a RAG corpus.

### REST

Before using any of the request data, make the following replacements:

  - PROJECT\_ID : Your \[project ID\](/resource-manager/docs/creating-managing-projects\#identifiers). .
  - LOCATION : The region to process the request.
  - CORPUS\_ID : The corpus ID of your RAG corpus.
  - CORPUS\_DISPLAY\_NAME : The display name of the `RagCorpus` .
  - CORPUS\_DESCRIPTION : The description of the `RagCorpus` .
  - INDEX\_NAME : The resource name of the `Vector Search Index` . Format: `projects/{project}/locations/{location}/indexes/{index}`
  - INDEX\_ENDPOINT\_NAME : The resource name of the `Vector Search Index Endpoint` . Format: `projects/{project}/locations/{location}/indexEndpoints/{index_endpoint}`

HTTP method and URL:

    PATCH https://LOCATION-aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/LOCATION/ragCorpora/CORPUS_ID

Request JSON body:

    {
      "display_name" : "CORPUS_DISPLAY_NAME",
      "description": "CORPUS_DESCRIPTION",
      "rag_vector_db_config": {
         "vertex_vector_search": {
             "index": "INDEX_NAME",
             "index_endpoint": "INDEX_ENDPOINT_NAME",
         }
      }
    }

To send your request, choose one of these options:

#### curl

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) , or by using [Cloud Shell](https://docs.cloud.google.com/shell/docs) , which automatically logs you into the `gcloud` CLI . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Save the request body in a file named `request.json` , and execute the following command:

    curl -X PATCH \
         -H "Authorization: Bearer $(gcloud auth print-access-token)" \
         -H "Content-Type: application/json; charset=utf-8" \
         -d @request.json \
         "https://LOCATION-aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/LOCATION/ragCorpora/CORPUS_ID"

#### PowerShell

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Save the request body in a file named `request.json` , and execute the following command:

    $cred = gcloud auth print-access-token
    $headers = @{ "Authorization" = "Bearer $cred" }
    
    Invoke-WebRequest `
        -Method PATCH `
        -Headers $headers `
        -ContentType: "application/json; charset=utf-8" `
        -InFile request.json `
        -Uri "https://LOCATION-aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/LOCATION/ragCorpora/CORPUS_ID" | Select-Object -Expand Content

You should receive a successful status code (2xx).

### List RAG corpora example

This code sample demonstrates how to list all of the RAG corpora.

### REST

Before using any of the request data, make the following replacements:

  - PROJECT\_ID : Your \[project ID\](/resource-manager/docs/creating-managing-projects\#identifiers). .
  - LOCATION : The region to process the request.
  - PAGE\_SIZE : The standard list page size. You may adjust the number of `RagCorpora` to return per page by updating the `page_size` parameter.
  - PAGE\_TOKEN : The standard list page token. Obtained typically using `ListRagCorporaResponse.next_page_token` of the previous `VertexRagDataService.ListRagCorpora` call.

HTTP method and URL:

    GET https://LOCATION-aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/LOCATION/ragCorpora?page_size=PAGE_SIZE&page_token=PAGE_TOKEN

To send your request, choose one of these options:

#### curl

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) , or by using [Cloud Shell](https://docs.cloud.google.com/shell/docs) , which automatically logs you into the `gcloud` CLI . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Execute the following command:

    curl -X GET \
         -H "Authorization: Bearer $(gcloud auth print-access-token)" \
         "https://LOCATION-aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/LOCATION/ragCorpora?page_size=PAGE_SIZE&page_token=PAGE_TOKEN"

#### PowerShell

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Execute the following command:

    $cred = gcloud auth print-access-token
    $headers = @{ "Authorization" = "Bearer $cred" }
    
    Invoke-WebRequest `
        -Method GET `
        -Headers $headers `
        -Uri "https://LOCATION-aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/LOCATION/ragCorpora?page_size=PAGE_SIZE&page_token=PAGE_TOKEN" | Select-Object -Expand Content

You should receive a successful status code (\`2xx\`) and a list of `RagCorpora` under the given `PROJECT_ID` .

### Get a RAG corpus example

### REST

Before using any of the request data, make the following replacements:

  - PROJECT\_ID : Your \[project ID\](/resource-manager/docs/creating-managing-projects\#identifiers). .
  - LOCATION : The region to process the request.
  - RAG\_CORPUS\_ID : The ID of the `RagCorpus` resource.

HTTP method and URL:

    GET https://LOCATION-aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/LOCATION/ragCorpora/RAG_CORPUS_ID

To send your request, choose one of these options:

#### curl

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) , or by using [Cloud Shell](https://docs.cloud.google.com/shell/docs) , which automatically logs you into the `gcloud` CLI . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Execute the following command:

    curl -X GET \
         -H "Authorization: Bearer $(gcloud auth print-access-token)" \
         "https://LOCATION-aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/LOCATION/ragCorpora/RAG_CORPUS_ID"

#### PowerShell

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Execute the following command:

    $cred = gcloud auth print-access-token
    $headers = @{ "Authorization" = "Bearer $cred" }
    
    Invoke-WebRequest `
        -Method GET `
        -Headers $headers `
        -Uri "https://LOCATION-aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/LOCATION/ragCorpora/RAG_CORPUS_ID" | Select-Object -Expand Content

A successful response returns the `RagCorpus` resource.

The `get` and `list` commands are used in an example to demonstrate how `RagCorpus` uses the `rag_embedding_model_config` field with in the `vector_db_config` , which points to the embedding model you have chosen.

``` 
  PROJECT_ID: Your project ID.
  LOCATION: The region to process the request.
  RAG_CORPUS_ID: The corpus ID of your RAG corpus.
```

    // GetRagCorpus
    // Input: LOCATION, PROJECT_ID, RAG_CORPUS_ID
    // Output: RagCorpus
    curl -X GET \
    -H "Content-Type: application/json" \
    -H "Authorization: Bearer $(gcloud auth print-access-token)" \
    https://LOCATION-aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/LOCATION/ragCorpora/RAG_CORPUS_ID
    
    // ListRagCorpora
    curl -sS -X GET \
    -H "Content-Type: application/json" \
    -H "Authorization: Bearer $(gcloud auth print-access-token)" \
    https://LOCATION-aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/LOCATION/ragCorpora/

### Delete a RAG corpus example

### REST

Before using any of the request data, make the following replacements:

  - PROJECT\_ID : Your \[project ID\](/resource-manager/docs/creating-managing-projects\#identifiers). .
  - LOCATION : The region to process the request.
  - RAG\_CORPUS\_ID : The ID of the `RagCorpus` resource.

HTTP method and URL:

    DELETE https://LOCATION-aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/LOCATION/ragCorpora/RAG_CORPUS_ID

To send your request, choose one of these options:

#### curl

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) , or by using [Cloud Shell](https://docs.cloud.google.com/shell/docs) , which automatically logs you into the `gcloud` CLI . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Execute the following command:

    curl -X DELETE \
         -H "Authorization: Bearer $(gcloud auth print-access-token)" \
         "https://LOCATION-aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/LOCATION/ragCorpora/RAG_CORPUS_ID"

#### PowerShell

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Execute the following command:

    $cred = gcloud auth print-access-token
    $headers = @{ "Authorization" = "Bearer $cred" }
    
    Invoke-WebRequest `
        -Method DELETE `
        -Headers $headers `
        -Uri "https://LOCATION-aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/LOCATION/ragCorpora/RAG_CORPUS_ID" | Select-Object -Expand Content

A successful response returns the `DeleteOperationMetadata` .

### Batch create metadata schemas example

This code sample demonstrates how to batch create metadata schemas for a RAG corpus.

### REST

Before using any of the request data, make the following replacements:

  - PROJECT\_ID : Your \[project ID\](/resource-manager/docs/creating-managing-projects\#identifiers). .
  - LOCATION : The region to process the request.
  - RAG\_CORPUS\_ID : The ID of the `RagCorpus` resource.
  - SCHEMA\_KEY\_1 : The key for the first metadata schema.
  - SCHEMA\_TYPE\_1 : The data type for the first metadata schema (e.g., `INTEGER` ).
  - SCHEMA\_KEY\_2 : The key for the second metadata schema.
  - SCHEMA\_TYPE\_2 : The data type for the second metadata schema (e.g., `STRING` ).

HTTP method and URL:

    POST https://LOCATION-aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/LOCATION/ragCorpora/RAG_CORPUS_ID/ragDataSchemas:batchCreate

Request JSON body:

    {
      "requests": [
        {
          "rag_data_schema": {
            "key": "SCHEMA_KEY_1",
            "schema_details": {"type": "SCHEMA_TYPE_1"}
          }
        },
        {
          "rag_data_schema": {
            "key": "SCHEMA_KEY_2",
            "schema_details": {"type": "SCHEMA_TYPE_2"}
          }
        }
      ]
    }

To send your request, choose one of these options:

#### curl

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) , or by using [Cloud Shell](https://docs.cloud.google.com/shell/docs) , which automatically logs you into the `gcloud` CLI . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Save the request body in a file named `request.json` , and execute the following command:

    curl -X POST \
         -H "Authorization: Bearer $(gcloud auth print-access-token)" \
         -H "Content-Type: application/json; charset=utf-8" \
         -d @request.json \
         "https://LOCATION-aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/LOCATION/ragCorpora/RAG_CORPUS_ID/ragDataSchemas:batchCreate"

#### PowerShell

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Save the request body in a file named `request.json` , and execute the following command:

    $cred = gcloud auth print-access-token
    $headers = @{ "Authorization" = "Bearer $cred" }
    
    Invoke-WebRequest `
        -Method POST `
        -Headers $headers `
        -ContentType: "application/json; charset=utf-8" `
        -InFile request.json `
        -Uri "https://LOCATION-aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/LOCATION/ragCorpora/RAG_CORPUS_ID/ragDataSchemas:batchCreate" | Select-Object -Expand Content

You should receive a successful status code (2xx).

### List metadata schemas example

This code sample demonstrates how to list metadata schemas for a RAG corpus.

### REST

Before using any of the request data, make the following replacements:

  - PROJECT\_ID : Your \[project ID\](/resource-manager/docs/creating-managing-projects\#identifiers). .
  - LOCATION : The region to process the request.
  - RAG\_CORPUS\_ID : The ID of the `RagCorpus` resource.

HTTP method and URL:

    GET https://LOCATION-aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/LOCATION/ragCorpora/RAG_CORPUS_ID/ragDataSchemas

To send your request, choose one of these options:

#### curl

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) , or by using [Cloud Shell](https://docs.cloud.google.com/shell/docs) , which automatically logs you into the `gcloud` CLI . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Execute the following command:

    curl -X GET \
         -H "Authorization: Bearer $(gcloud auth print-access-token)" \
         "https://LOCATION-aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/LOCATION/ragCorpora/RAG_CORPUS_ID/ragDataSchemas"

#### PowerShell

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Execute the following command:

    $cred = gcloud auth print-access-token
    $headers = @{ "Authorization" = "Bearer $cred" }
    
    Invoke-WebRequest `
        -Method GET `
        -Headers $headers `
        -Uri "https://LOCATION-aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/LOCATION/ragCorpora/RAG_CORPUS_ID/ragDataSchemas" | Select-Object -Expand Content

A successful response returns a list of `RagDataSchema` resources.

### Batch delete metadata schemas example

This code sample demonstrates how to batch delete metadata schemas.

### REST

Before using any of the request data, make the following replacements:

  - PROJECT\_ID : Your \[project ID\](/resource-manager/docs/creating-managing-projects\#identifiers). .
  - LOCATION : The region to process the request.
  - RAG\_CORPUS\_ID : The ID of the `RagCorpus` resource.
  - SCHEMA\_ID\_1 : The ID of the first metadata schema to delete.
  - SCHEMA\_ID\_2 : The ID of the second metadata schema to delete.

HTTP method and URL:

    POST https://LOCATION-aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/LOCATION/ragCorpora/RAG_CORPUS_ID/ragDataSchemas:batchDelete

Request JSON body:

    {
      "names": [
        "projects/PROJECT_ID/locations/LOCATION/ragCorpora/RAG_CORPUS_ID/ragDataSchemas/SCHEMA_ID_1",
        "projects/PROJECT_ID/locations/LOCATION/ragCorpora/RAG_CORPUS_ID/ragDataSchemas/SCHEMA_ID_2"
      ]
    }

To send your request, choose one of these options:

#### curl

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) , or by using [Cloud Shell](https://docs.cloud.google.com/shell/docs) , which automatically logs you into the `gcloud` CLI . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Save the request body in a file named `request.json` , and execute the following command:

    curl -X POST \
         -H "Authorization: Bearer $(gcloud auth print-access-token)" \
         -H "Content-Type: application/json; charset=utf-8" \
         -d @request.json \
         "https://LOCATION-aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/LOCATION/ragCorpora/RAG_CORPUS_ID/ragDataSchemas:batchDelete"

#### PowerShell

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Save the request body in a file named `request.json` , and execute the following command:

    $cred = gcloud auth print-access-token
    $headers = @{ "Authorization" = "Bearer $cred" }
    
    Invoke-WebRequest `
        -Method POST `
        -Headers $headers `
        -ContentType: "application/json; charset=utf-8" `
        -InFile request.json `
        -Uri "https://LOCATION-aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/LOCATION/ragCorpora/RAG_CORPUS_ID/ragDataSchemas:batchDelete" | Select-Object -Expand Content

You should receive a successful status code (2xx).

## File management examples

This section provides examples of how to use the API to manage RAG files.

### Upload a RAG file example

### REST

Before using any of the request data, make the following replacements:

``` 
  PROJECT_ID: Your project ID.
  LOCATION: The region to process the request.
  RAG_CORPUS_ID: The corpus ID of your RAG corpus.
  LOCAL_FILE_PATH: The local path to the file to be uploaded.
  DISPLAY_NAME: The display name of the RAG file.
  DESCRIPTION: The description of the RAG file.
```

To send your request, use the following command:

``` 
  curl -X POST \
    -H "X-Goog-Upload-Protocol: multipart" \
    -H "Authorization: Bearer $(gcloud auth print-access-token)" \
    -F metadata="{'rag_file': {'display_name':' DISPLAY_NAME', 'description':'DESCRIPTION'}}" \
    -F file=@LOCAL_FILE_PATH \
    "https://LOCATION-aiplatform.googleapis.com/upload/v1beta1/projects/PROJECT_ID/locations/LOCATION/ragCorpora/RAG_CORPUS_ID/ragFiles:upload"
```

### Import RAG files example

Files and folders can be imported from Drive or Cloud Storage.

The `response.skipped_rag_files_count` refers to the number of files that were skipped during import. A file is skipped when the following conditions are met:

1.  The file has already been imported.
2.  The file hasn't changed.
3.  The chunking configuration for the file hasn't changed.

### REST

Before using any of the request data, make the following replacements:

  - PROJECT\_ID : Your \[project ID\](/resource-manager/docs/creating-managing-projects\#identifiers). .
  - LOCATION : The region to process the request.
  - RAG\_CORPUS\_ID : The ID of the `RagCorpus` resource.
  - GCS\_URIS : A list of Cloud Storage locations. Example: `gs://my-bucket1, gs://my-bucket2` .
  - CHUNK\_SIZE : Optional: Number of tokens each chunk should have.
  - CHUNK\_OVERLAP : Optional: Number of tokens overlap between chunks.

HTTP method and URL:

    POST https://LOCATION-aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/LOCATION/ragCorpora/RAG_CORPUS_ID/ragFiles:import

Request JSON body:

    {
      "import_rag_files_config": {
        "gcs_source": {
          "uris": "GCS_URIS"
        },
        "rag_file_chunking_config": {
          "chunk_size": CHUNK_SIZE,
          "chunk_overlap": CHUNK_OVERLAP
        }
      }
    }

To send your request, choose one of these options:

#### curl

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) , or by using [Cloud Shell](https://docs.cloud.google.com/shell/docs) , which automatically logs you into the `gcloud` CLI . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Save the request body in a file named `request.json` , and execute the following command:

    curl -X POST \
         -H "Authorization: Bearer $(gcloud auth print-access-token)" \
         -H "Content-Type: application/json; charset=utf-8" \
         -d @request.json \
         "https://LOCATION-aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/LOCATION/ragCorpora/RAG_CORPUS_ID/ragFiles:import"

#### PowerShell

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Save the request body in a file named `request.json` , and execute the following command:

    $cred = gcloud auth print-access-token
    $headers = @{ "Authorization" = "Bearer $cred" }
    
    Invoke-WebRequest `
        -Method POST `
        -Headers $headers `
        -ContentType: "application/json; charset=utf-8" `
        -InFile request.json `
        -Uri "https://LOCATION-aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/LOCATION/ragCorpora/RAG_CORPUS_ID/ragFiles:import" | Select-Object -Expand Content

A successful response returns the `ImportRagFilesOperationMetadata` resource.

The following sample demonstrates how to import a file from Cloud Storage. Use the `max_embedding_requests_per_min` control field to limit the rate at which RAG Engine calls the embedding model during the `ImportRagFiles` indexing process. The field has a default value of `1000` calls per minute.

``` 
  PROJECT_ID: Your project ID.
  LOCATION: The region to process the request.
  RAG_CORPUS_ID: The corpus ID of your RAG corpus.
  GCS_URIS: A list of Cloud Storage locations. Example: gs://my-bucket1.
  CHUNK_SIZE: Number of tokens each chunk should have.
  CHUNK_OVERLAP: Number of tokens overlap between chunks.
  EMBEDDING_MODEL_QPM_RATE: The QPM rate to limit RAGs access to your embedding model. Example: 1000.
```

    // ImportRagFiles
    // Import a single Cloud Storage file or all files in a Cloud Storage bucket.
    // Input: LOCATION, PROJECT_ID, RAG_CORPUS_ID, GCS_URIS
    // Output: ImportRagFilesOperationMetadataNumber
    // Use ListRagFiles to find the server-generated rag_file_id.
    curl -X POST \
    -H "Authorization: Bearer $(gcloud auth print-access-token)" \
    -H "Content-Type: application/json" \
    https://LOCATION-aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/LOCATION/ragCorpora/RAG_CORPUS_ID/ragFiles:import \
    -d '{
      "import_rag_files_config": {
        "gcs_source": {
          "uris": "GCS_URIS"
        },
        "rag_file_chunking_config": {
          "chunk_size": CHUNK_SIZE,
          "chunk_overlap": CHUNK_OVERLAP
        },
        "max_embedding_requests_per_min": EMBEDDING_MODEL_QPM_RATE
      }
    }'
    
    // Poll the operation status.
    // The response contains the number of files imported.
    OPERATION_ID: The operation ID you get from the response of the previous command.
    poll_op_wait OPERATION_ID

The following sample demonstrates how to import a file from Drive. Use the `max_embedding_requests_per_min` control field to limit the rate at which RAG Engine calls the embedding model during the `ImportRagFiles` indexing process. The field has a default value of `1000` calls per minute.

``` 
  PROJECT_ID: Your project ID.
  LOCATION: The region to process the request.
  RAG_CORPUS_ID: The corpus ID of your RAG corpus.
  FOLDER_RESOURCE_ID: The resource ID of your Google Drive folder.
  CHUNK_SIZE: Number of tokens each chunk should have.
  CHUNK_OVERLAP: Number of tokens overlap between chunks.
  EMBEDDING_MODEL_QPM_RATE: The QPM rate to limit RAGs access to your embedding model. Example: 1000.
```

    // ImportRagFiles
    // Import all files in a Google Drive folder.
    // Input: LOCATION, PROJECT_ID, RAG_CORPUS_ID, FOLDER_RESOURCE_ID
    // Output: ImportRagFilesOperationMetadataNumber
    // Use ListRagFiles to find the server-generated rag_file_id.
    curl -X POST \
    -H "Authorization: Bearer $(gcloud auth print-access-token)" \
    -H "Content-Type: application/json" \
    https://LOCATION-aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/LOCATION/ragCorpora/RAG_CORPUS_ID/ragFiles:import \
    -d '{
      "import_rag_files_config": {
        "google_drive_source": {
          "resource_ids": {
            "resource_id": "FOLDER_RESOURCE_ID",
            "resource_type": "RESOURCE_TYPE_FOLDER"
          }
        },
        "max_embedding_requests_per_min": EMBEDDING_MODEL_QPM_RATE
      }
    }'
    
    // Poll the operation status.
    // The response contains the number of files imported.
    OPERATION_ID: The operation ID you get from the response of the previous command.
    poll_op_wait OPERATION_ID

### List RAG files example

This code sample demonstrates how to list RAG files.

### REST

Before using any of the request data, make the following replacements:

  - PROJECT\_ID : Your \[project ID\](/resource-manager/docs/creating-managing-projects\#identifiers). .
  - LOCATION : The region to process the request.
  - RAG\_CORPUS\_ID : The ID of the `RagCorpus` resource.
  - PAGE\_SIZE : The standard list page size. You may adjust the number of `RagFiles` to return per page by updating the `page_size` parameter.
  - PAGE\_TOKEN : The standard list page token. Obtained typically using `ListRagFilesResponse.next_page_token` of the previous `VertexRagDataService.ListRagFiles` call.

HTTP method and URL:

    GET https://LOCATION-aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/LOCATION/ragCorpora/RAG_CORPUS_ID/ragFiles?page_size=PAGE_SIZE&page_token=PAGE_TOKEN

To send your request, choose one of these options:

#### curl

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) , or by using [Cloud Shell](https://docs.cloud.google.com/shell/docs) , which automatically logs you into the `gcloud` CLI . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Execute the following command:

    curl -X GET \
         -H "Authorization: Bearer $(gcloud auth print-access-token)" \
         "https://LOCATION-aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/LOCATION/ragCorpora/RAG_CORPUS_ID/ragFiles?page_size=PAGE_SIZE&page_token=PAGE_TOKEN"

#### PowerShell

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Execute the following command:

    $cred = gcloud auth print-access-token
    $headers = @{ "Authorization" = "Bearer $cred" }
    
    Invoke-WebRequest `
        -Method GET `
        -Headers $headers `
        -Uri "https://LOCATION-aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/LOCATION/ragCorpora/RAG_CORPUS_ID/ragFiles?page_size=PAGE_SIZE&page_token=PAGE_TOKEN" | Select-Object -Expand Content

You should receive a successful status code (2xx) along with a list of `RagFiles` under the given `RAG_CORPUS_ID` .

### Get a RAG file example

This code sample demonstrates how to get a RAG file.

### REST

Before using any of the request data, make the following replacements:

  - PROJECT\_ID : Your \[project ID\](/resource-manager/docs/creating-managing-projects\#identifiers). .
  - LOCATION : The region to process the request.
  - RAG\_CORPUS\_ID : The ID of the `RagCorpus` resource.
  - RAG\_FILE\_ID : The ID of the `RagFile` resource.

HTTP method and URL:

    GET https://LOCATION-aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/LOCATION/ragCorpora/RAG_CORPUS_ID/ragFiles/RAG_FILE_ID

To send your request, choose one of these options:

#### curl

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) , or by using [Cloud Shell](https://docs.cloud.google.com/shell/docs) , which automatically logs you into the `gcloud` CLI . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Execute the following command:

    curl -X GET \
         -H "Authorization: Bearer $(gcloud auth print-access-token)" \
         "https://LOCATION-aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/LOCATION/ragCorpora/RAG_CORPUS_ID/ragFiles/RAG_FILE_ID"

#### PowerShell

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Execute the following command:

    $cred = gcloud auth print-access-token
    $headers = @{ "Authorization" = "Bearer $cred" }
    
    Invoke-WebRequest `
        -Method GET `
        -Headers $headers `
        -Uri "https://LOCATION-aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/LOCATION/ragCorpora/RAG_CORPUS_ID/ragFiles/RAG_FILE_ID" | Select-Object -Expand Content

A successful response returns the `RagFile` resource.

### Delete a RAG file example

This code sample demonstrates how to delete a RAG file.

### REST

Before using any of the request data, make the following replacements:

  - PROJECT\_ID : Your \[project ID\](/resource-manager/docs/creating-managing-projects\#identifiers). .
  - LOCATION : The region to process the request.
  - RAG\_CORPUS\_ID : The ID of the `RagCorpus` resource.
  - RAG\_FILE\_ID : The ID of the `RagFile` resource. Format: `projects/{project}/locations/{location}/ragCorpora/{rag_corpus}/ragFiles/{rag_file_id}` .

HTTP method and URL:

    DELETE https://LOCATION-aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/LOCATION/ragCorpora/RAG_CORPUS_ID/ragFiles/RAG_FILE_ID

To send your request, choose one of these options:

#### curl

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) , or by using [Cloud Shell](https://docs.cloud.google.com/shell/docs) , which automatically logs you into the `gcloud` CLI . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Execute the following command:

    curl -X DELETE \
         -H "Authorization: Bearer $(gcloud auth print-access-token)" \
         "https://LOCATION-aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/LOCATION/ragCorpora/RAG_CORPUS_ID/ragFiles/RAG_FILE_ID"

#### PowerShell

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Execute the following command:

    $cred = gcloud auth print-access-token
    $headers = @{ "Authorization" = "Bearer $cred" }
    
    Invoke-WebRequest `
        -Method DELETE `
        -Headers $headers `
        -Uri "https://LOCATION-aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/LOCATION/ragCorpora/RAG_CORPUS_ID/ragFiles/RAG_FILE_ID" | Select-Object -Expand Content

A successful response returns the `DeleteOperationMetadata` resource.

### Batch create metadata example

This code sample demonstrates how to batch create metadata for a RAG file.

### REST

Before using any of the request data, make the following replacements:

  - PROJECT\_ID : Your \[project ID\](/resource-manager/docs/creating-managing-projects\#identifiers). .
  - LOCATION : The region to process the request.
  - RAG\_CORPUS\_ID : The ID of the `RagCorpus` resource.
  - RAG\_FILE\_ID : The ID of the `RagFile` resource.
  - METADATA\_KEY\_1 : The key for the first metadata entry.
  - VALUE\_TYPE\_1 : The value type field for the first metadata entry (e.g., `int_value` ).
  - METADATA\_VALUE\_1 : The value for the first metadata entry.
  - METADATA\_KEY\_2 : The key for the second metadata entry.
  - VALUE\_TYPE\_2 : The value type field for the second metadata entry (e.g., `str_value` ).
  - METADATA\_VALUE\_2 : The value for the second metadata entry.

HTTP method and URL:

    POST https://LOCATION-aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/LOCATION/ragCorpora/RAG_CORPUS_ID/ragFiles/RAG_FILE_ID/ragMetadata:batchCreate

Request JSON body:

    {
      "requests": [
        {
          "rag_metadata": {
            "user_specified_metadata": {
              "key": "METADATA_KEY_1",
              "value": { "VALUE_TYPE_1": METADATA_VALUE_1 }
            }
          }
        },
        {
          "rag_metadata": {
            "user_specified_metadata": {
              "key": "METADATA_KEY_2",
              "value": { "VALUE_TYPE_2": "METADATA_VALUE_2" }
            }
          }
        }
      ]
    }

To send your request, choose one of these options:

#### curl

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) , or by using [Cloud Shell](https://docs.cloud.google.com/shell/docs) , which automatically logs you into the `gcloud` CLI . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Save the request body in a file named `request.json` , and execute the following command:

    curl -X POST \
         -H "Authorization: Bearer $(gcloud auth print-access-token)" \
         -H "Content-Type: application/json; charset=utf-8" \
         -d @request.json \
         "https://LOCATION-aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/LOCATION/ragCorpora/RAG_CORPUS_ID/ragFiles/RAG_FILE_ID/ragMetadata:batchCreate"

#### PowerShell

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Save the request body in a file named `request.json` , and execute the following command:

    $cred = gcloud auth print-access-token
    $headers = @{ "Authorization" = "Bearer $cred" }
    
    Invoke-WebRequest `
        -Method POST `
        -Headers $headers `
        -ContentType: "application/json; charset=utf-8" `
        -InFile request.json `
        -Uri "https://LOCATION-aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/LOCATION/ragCorpora/RAG_CORPUS_ID/ragFiles/RAG_FILE_ID/ragMetadata:batchCreate" | Select-Object -Expand Content

You should receive a successful status code (2xx).

### List metadata example

This code sample demonstrates how to list metadata for a RAG file.

### REST

Before using any of the request data, make the following replacements:

  - PROJECT\_ID : Your \[project ID\](/resource-manager/docs/creating-managing-projects\#identifiers). .
  - LOCATION : The region to process the request.
  - RAG\_CORPUS\_ID : The ID of the `RagCorpus` resource.
  - RAG\_FILE\_ID : The ID of the `RagFile` resource.

HTTP method and URL:

    GET https://LOCATION-aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/LOCATION/ragCorpora/RAG_CORPUS_ID/ragFiles/RAG_FILE_ID/ragMetadata

To send your request, choose one of these options:

#### curl

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) , or by using [Cloud Shell](https://docs.cloud.google.com/shell/docs) , which automatically logs you into the `gcloud` CLI . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Execute the following command:

    curl -X GET \
         -H "Authorization: Bearer $(gcloud auth print-access-token)" \
         "https://LOCATION-aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/LOCATION/ragCorpora/RAG_CORPUS_ID/ragFiles/RAG_FILE_ID/ragMetadata"

#### PowerShell

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Execute the following command:

    $cred = gcloud auth print-access-token
    $headers = @{ "Authorization" = "Bearer $cred" }
    
    Invoke-WebRequest `
        -Method GET `
        -Headers $headers `
        -Uri "https://LOCATION-aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/LOCATION/ragCorpora/RAG_CORPUS_ID/ragFiles/RAG_FILE_ID/ragMetadata" | Select-Object -Expand Content

A successful response returns a list of `RagMetadata` resources.

### Update metadata example

This code sample demonstrates how to update metadata for a RAG file.

### REST

Before using any of the request data, make the following replacements:

  - PROJECT\_ID : Your \[project ID\](/resource-manager/docs/creating-managing-projects\#identifiers). .
  - LOCATION : The region to process the request.
  - RAG\_CORPUS\_ID : The ID of the `RagCorpus` resource.
  - RAG\_FILE\_ID : The ID of the `RagFile` resource.
  - METADATA\_ID : The ID of the metadata entry to update.
  - METADATA\_KEY : The key for the metadata entry.
  - VALUE\_TYPE : The value type field (e.g., `int_value` ).
  - METADATA\_VALUE : The new value for the metadata entry.

HTTP method and URL:

    PATCH https://LOCATION-aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/LOCATION/ragCorpora/RAG_CORPUS_ID/ragFiles/RAG_FILE_ID/ragMetadata/METADATA_ID

Request JSON body:

    {
      "user_specified_metadata": {
        "key": "METADATA_KEY",
        "value": { "VALUE_TYPE": METADATA_VALUE }
      }
    }

To send your request, choose one of these options:

#### curl

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) , or by using [Cloud Shell](https://docs.cloud.google.com/shell/docs) , which automatically logs you into the `gcloud` CLI . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Save the request body in a file named `request.json` , and execute the following command:

    curl -X PATCH \
         -H "Authorization: Bearer $(gcloud auth print-access-token)" \
         -H "Content-Type: application/json; charset=utf-8" \
         -d @request.json \
         "https://LOCATION-aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/LOCATION/ragCorpora/RAG_CORPUS_ID/ragFiles/RAG_FILE_ID/ragMetadata/METADATA_ID"

#### PowerShell

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Save the request body in a file named `request.json` , and execute the following command:

    $cred = gcloud auth print-access-token
    $headers = @{ "Authorization" = "Bearer $cred" }
    
    Invoke-WebRequest `
        -Method PATCH `
        -Headers $headers `
        -ContentType: "application/json; charset=utf-8" `
        -InFile request.json `
        -Uri "https://LOCATION-aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/LOCATION/ragCorpora/RAG_CORPUS_ID/ragFiles/RAG_FILE_ID/ragMetadata/METADATA_ID" | Select-Object -Expand Content

You should receive a successful status code (2xx).

### Batch delete metadata example

This code sample demonstrates how to batch delete metadata entries for a RAG file.

### REST

Before using any of the request data, make the following replacements:

  - PROJECT\_ID : Your \[project ID\](/resource-manager/docs/creating-managing-projects\#identifiers). .
  - LOCATION : The region to process the request.
  - RAG\_CORPUS\_ID : The ID of the `RagCorpus` resource.
  - RAG\_FILE\_ID : The ID of the `RagFile` resource.
  - METADATA\_ID\_1 : The ID of the first metadata entry to delete.
  - METADATA\_ID\_2 : The ID of the second metadata entry to delete.

HTTP method and URL:

    POST https://LOCATION-aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/LOCATION/ragCorpora/RAG_CORPUS_ID/ragFiles/RAG_FILE_ID/ragMetadata:batchDelete

Request JSON body:

    {
      "names": [
        "projects/PROJECT_ID/locations/LOCATION/ragCorpora/RAG_CORPUS_ID/ragFiles/RAG_FILE_ID/ragMetadata/METADATA_ID_1",
        "projects/PROJECT_ID/locations/LOCATION/ragCorpora/RAG_CORPUS_ID/ragFiles/RAG_FILE_ID/ragMetadata/METADATA_ID_2"
      ]
    }

To send your request, choose one of these options:

#### curl

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) , or by using [Cloud Shell](https://docs.cloud.google.com/shell/docs) , which automatically logs you into the `gcloud` CLI . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Save the request body in a file named `request.json` , and execute the following command:

    curl -X POST \
         -H "Authorization: Bearer $(gcloud auth print-access-token)" \
         -H "Content-Type: application/json; charset=utf-8" \
         -d @request.json \
         "https://LOCATION-aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/LOCATION/ragCorpora/RAG_CORPUS_ID/ragFiles/RAG_FILE_ID/ragMetadata:batchDelete"

#### PowerShell

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Save the request body in a file named `request.json` , and execute the following command:

    $cred = gcloud auth print-access-token
    $headers = @{ "Authorization" = "Bearer $cred" }
    
    Invoke-WebRequest `
        -Method POST `
        -Headers $headers `
        -ContentType: "application/json; charset=utf-8" `
        -InFile request.json `
        -Uri "https://LOCATION-aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/LOCATION/ragCorpora/RAG_CORPUS_ID/ragFiles/RAG_FILE_ID/ragMetadata:batchDelete" | Select-Object -Expand Content

You should receive a successful status code (2xx).

### Retrieval query example

When a user asks a question or provides a prompt, the retrieval component in RAG searches through its knowledge base to find information that is relevant to the query.

### REST

Before using any of the request data, make the following replacements:

  - LOCATION : The region to process the request.
  - PROJECT\_ID : Your \[project ID\](/resource-manager/docs/creating-managing-projects\#identifiers). .
  - RAG\_CORPUS\_RESOURCE : The name of the `RagCorpus` resource. Format: `projects/{project}/locations/{location}/ragCorpora/{rag_corpus}` .
  - TOP\_K : The number of top contexts to retrieve.
  - VECTOR\_DISTANCE\_THRESHOLD : Only contexts with a vector distance smaller than the threshold are returned.
  - METADATA\_FILTER : Optional: The metadata filter to apply during retrieval.
  - TEXT : The query text to get relevant contexts.

HTTP method and URL:

    POST https://LOCATION-aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/LOCATION:retrieveContexts

Request JSON body:

    {
      "vertex_rag_store": {
        "rag_resources": [
          {
            "rag_corpus": "RAG_CORPUS_RESOURCE"
          }
        ]
      },
      "query": {
        "text": "TEXT",
        "rag_retrieval_config": {
          "top_k": TOP_K,
          "filter": {
            "vector_distance_threshold": VECTOR_DISTANCE_THRESHOLD,
            "metadata_filter": "METADATA_FILTER"
          }
        }
      }
    }

To send your request, choose one of these options:

#### curl

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) , or by using [Cloud Shell](https://docs.cloud.google.com/shell/docs) , which automatically logs you into the `gcloud` CLI . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Save the request body in a file named `request.json` , and execute the following command:

    curl -X POST \
         -H "Authorization: Bearer $(gcloud auth print-access-token)" \
         -H "Content-Type: application/json; charset=utf-8" \
         -d @request.json \
         "https://LOCATION-aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/LOCATION:retrieveContexts"

#### PowerShell

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Save the request body in a file named `request.json` , and execute the following command:

    $cred = gcloud auth print-access-token
    $headers = @{ "Authorization" = "Bearer $cred" }
    
    Invoke-WebRequest `
        -Method POST `
        -Headers $headers `
        -ContentType: "application/json; charset=utf-8" `
        -InFile request.json `
        -Uri "https://LOCATION-aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/LOCATION:retrieveContexts" | Select-Object -Expand Content

You should receive a successful status code (2xx) and a list of related `RagFiles` .

### Generation example

The LLM generates a grounded response using the retrieved contexts.

### REST

Before using any of the request data, make the following replacements:

  - PROJECT\_ID : Your \[project ID\](/resource-manager/docs/creating-managing-projects\#identifiers). .
  - LOCATION : The region to process the request.
  - MODEL\_ID : LLM model for content generation. Example: `gemini-2.5-flash`
  - GENERATION\_METHOD : LLM method for content generation. Options: `generateContent` , `streamGenerateContent`
  - INPUT\_PROMPT : The text sent to the LLM for content generation. Try to use a prompt relevant to the uploaded rag Files.
  - RAG\_CORPUS\_RESOURCE : The name of the `RagCorpus` resource. Format: `projects/{project}/locations/{location}/ragCorpora/{rag_corpus}` .
  - TOP\_K : Optional: The number of top contexts to retrieve.
  - VECTOR\_DISTANCE\_THRESHOLD : Optional: Contexts with a vector distance smaller than the threshold are returned.
  - METADATA\_FILTER : Optional: The metadata filter to apply during retrieval.

HTTP method and URL:

    POST https://LOCATION-aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/LOCATION/publishers/google/models/MODEL_ID:GENERATION_METHOD

Request JSON body:

    {
      "contents": {
        "role": "user",
        "parts": {
          "text": "INPUT_PROMPT"
        }
      },
      "tools": {
        "retrieval": {
          "disable_attribution": false,
          "vertex_rag_store": {
            "rag_resources": [
              {
                "rag_corpus": "RAG_CORPUS_RESOURCE"
              }
            ],
            "rag_retrieval_config": {
              "top_k": TOP_K,
              "filter": {
                "vector_distance_threshold": VECTOR_DISTANCE_THRESHOLD,
                "metadata_filter": "METADATA_FILTER"
              }
            }
          }
        }
      }
    }

To send your request, choose one of these options:

#### curl

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) , or by using [Cloud Shell](https://docs.cloud.google.com/shell/docs) , which automatically logs you into the `gcloud` CLI . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Save the request body in a file named `request.json` , and execute the following command:

    curl -X POST \
         -H "Authorization: Bearer $(gcloud auth print-access-token)" \
         -H "Content-Type: application/json; charset=utf-8" \
         -d @request.json \
         "https://LOCATION-aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/LOCATION/publishers/google/models/MODEL_ID:GENERATION_METHOD"

#### PowerShell

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Save the request body in a file named `request.json` , and execute the following command:

    $cred = gcloud auth print-access-token
    $headers = @{ "Authorization" = "Bearer $cred" }
    
    Invoke-WebRequest `
        -Method POST `
        -Headers $headers `
        -ContentType: "application/json; charset=utf-8" `
        -InFile request.json `
        -Uri "https://LOCATION-aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/LOCATION/publishers/google/models/MODEL_ID:GENERATION_METHOD" | Select-Object -Expand Content

A successful response returns the generated content with citations.

## Project management examples

The deployment mode and tier is a project-level setting available under the `RagEngineConfig` resource and impacts RAG corpora using `RagManagedDb` . To get the current configuration, use `GetRagEngineConfig` . To update the configuration, use `UpdateRagEngineConfig` .

For more information on managing your mode and tier configuration, see [Deployment modes in RAG Engine](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/rag-engine/deployment-modes) .

### Read your current RagEngineConfig

The following code samples demonstrate how to read your `RagEngineConfig` to see what mode and tier is currently chosen:

### Console

1.  In the Google Cloud console, go to the **RAG Engine** page.
2.  Select the region in which your RAG Engine is running. Your list of RAG corpora is updated.
3.  Click **Configure RAG Engine** . The **Configure RAG Engine** pane appears. You can see the tier that's selected for your RAG Engine.
4.  Click **Cancel** .

### REST

    PROJECT_ID: Your project ID.
    LOCATION: The region to process the request.

    curl -X GET \
    -H "Content-Type: application/json" \
    -H "Authorization: Bearer $(gcloud auth print-access-token)" \
    https://LOCATION-aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/LOCATION/ragEngineConfig

### Python

    from vertexai.preview import rag
    import vertexai
    
    PROJECT_ID = YOUR_PROJECT_ID
    LOCATION = YOUR_RAG_ENGINE_LOCATION
    
    # Initialize API once per session
    vertexai.init(project=PROJECT_ID, location=LOCATION)
    
    rag_engine_config = rag.rag_data.get_rag_engine_config(
        name=f"projects/{PROJECT_ID}/locations/{LOCATION}/ragEngineConfig"
    )
    
    print(rag_engine_config)

### Switch to Serverless mode

The following code samples demonstrate how to switch your `RagEngineConfig` to the Serverless mode:

### Console

1.  In the Google Cloud console, go to the **RAG Engine** page.
2.  Select the region in which your RAG Engine is running.
3.  Click the **Switch to Serverless** button. This button might not be visible if you are already on Serverless mode. You can verify your current mode from the mode label at the top right section of the page.

### REST

    PROJECT_ID: Your project ID.
    LOCATION: The region to process the request.

    curl -X PATCH \
    -H "Content-Type: application/json" \
    -H "Authorization: Bearer $(gcloud auth print-access-token)" \
    https://LOCATION-aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/LOCATION/ragEngineConfig -d "{'ragManagedDbConfig': {'serverless': {}}}"

### Python

    from vertexai.preview import rag
    import vertexai
    
    PROJECT_ID = YOUR_PROJECT_ID
    LOCATION = YOUR_RAG_ENGINE_LOCATION
    
    # Initialize API once per session
    vertexai.init(project=PROJECT_ID, location=LOCATION)
    
    rag_engine_config_name=f"projects/{PROJECT_ID}/locations/{LOCATION}/ragEngineConfig"
    
    new_rag_engine_config = rag.RagEngineConfig(
        name=rag_engine_config_name,
        rag_managed_db_config=rag.RagManagedDbConfig(mode=rag.Serverless()),
    )
    
    updated_rag_engine_config = rag.rag_data.update_rag_engine_config(
        rag_engine_config=new_rag_engine_config
    )
    
    print(updated_rag_engine_config)

### Switch to Spanner mode

The following code samples demonstrate how to switch your `RagEngineConfig` to the Spanner mode. If you previously have used Spanner mode, and have chosen a tier, you no longer need to provide it explicitly while switching. If not, refer to the lower code examples on how to switch to Spanner mode while providing a tier.

### Console

1.  In the Google Cloud console, go to the **RAG Engine** page.
2.  Select the region in which your RAG Engine is running.
3.  Click the **Switch to Spanner** button. This button might not be visible if you are already on Spanner mode. You can verify your current mode from the mode label at the top right section of the page.

### REST

    PROJECT_ID: Your project ID.
    LOCATION: The region to process the request.

    curl -X PATCH \
    -H "Content-Type: application/json" \
    -H "Authorization: Bearer $(gcloud auth print-access-token)" \
    https://LOCATION-aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/LOCATION/ragEngineConfig -d "{'ragManagedDbConfig': {'spanner': {}}}"

### Python

    from vertexai.preview import rag
    import vertexai
    
    PROJECT_ID = YOUR_PROJECT_ID
    LOCATION = YOUR_RAG_ENGINE_LOCATION
    
    # Initialize API once per session
    vertexai.init(project=PROJECT_ID, location=LOCATION)
    
    rag_engine_config_name=f"projects/{PROJECT_ID}/locations/{LOCATION}/ragEngineConfig"
    
    new_rag_engine_config = rag.RagEngineConfig(
        name=rag_engine_config_name,
        rag_managed_db_config=rag.RagManagedDbConfig(mode=rag.Spanner()),
    )
    
    updated_rag_engine_config = rag.rag_data.update_rag_engine_config(
        rag_engine_config=new_rag_engine_config
    )
    
    print(updated_rag_engine_config)

### Update your `RagEngineConfig` to Spanner mode Scaled tier

The following code samples demonstrate how to set the `RagEngineConfig` to the Spanner mode with Scaled tier:

### Console

1.  In the Google Cloud console, go to the **RAG Engine** page.
2.  Select the region in which your RAG Engine is running.
3.  Click the **Switch to Spanner** button if not already on Spanner mode.
4.  Click **Configure RAG Engine** . The **Configure RAG Engine** pane appears.
5.  Select the tier that you want to run your RAG Engine.
6.  Click **Save** .

### REST

    PROJECT_ID: Your project ID.
    LOCATION: The region to process the request.

    curl -X PATCH \
    -H "Content-Type: application/json" \
    -H "Authorization: Bearer $(gcloud auth print-access-token)" \
    https://LOCATION-aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/LOCATION/ragEngineConfig -d "{'ragManagedDbConfig': {'spanner': {'scaled': {}}}}"

### Python

    from vertexai.preview import rag
    import vertexai
    
    PROJECT_ID = YOUR_PROJECT_ID
    LOCATION = YOUR_RAG_ENGINE_LOCATION
    
    # Initialize API once per session
    vertexai.init(project=PROJECT_ID, location=LOCATION)
    
    rag_engine_config_name=f"projects/{PROJECT_ID}/locations/{LOCATION}/ragEngineConfig"
    
    new_rag_engine_config = rag.RagEngineConfig(
        name=rag_engine_config_name,
        rag_managed_db_config=rag.RagManagedDbConfig(mode=rag.Spanner(tier=rag.Scaled())),
    )
    
    updated_rag_engine_config = rag.rag_data.update_rag_engine_config(
        rag_engine_config=new_rag_engine_config
    )
    
    print(updated_rag_engine_config)

### Update your `RagEngineConfig` to Spanner mode with Basic tier

The following code samples demonstrate how to set the `RagEngineConfig` to the Spanner mode with Basic tier:

### Console

1.  In the Google Cloud console, go to the **RAG Engine** page.
2.  Select the region in which your RAG Engine is running.
3.  Click the **Switch to Spanner** button if not already on Spanner mode.
4.  Click **Configure RAG Engine** . The **Configure RAG Engine** pane appears.
5.  Select the tier that you want to run your RAG Engine.
6.  Click **Save** .

### REST

    PROJECT_ID: Your project ID.
    LOCATION: The region to process the request.

    curl -X PATCH \
    -H "Content-Type: application/json" \
    -H "Authorization: Bearer $(gcloud auth print-access-token)" \
    https://LOCATION-aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/LOCATION/ragEngineConfig -d "{'ragManagedDbConfig': {'spanner': {'basic': {}}}}"

### Python

    from vertexai.preview import rag
    import vertexai
    
    PROJECT_ID = YOUR_PROJECT_ID
    LOCATION = YOUR_RAG_ENGINE_LOCATION
    
    # Initialize API once per session
    vertexai.init(project=PROJECT_ID, location=LOCATION)
    
    rag_engine_config_name=f"projects/{PROJECT_ID}/locations/{LOCATION}/ragEngineConfig"
    
    new_rag_engine_config = rag.RagEngineConfig(
        name=rag_engine_config_name,
        rag_managed_db_config=rag.RagManagedDbConfig(mode=rag.Spanner(tier=rag.Basic())),
    )
    
    updated_rag_engine_config = rag.rag_data.update_rag_engine_config(
        rag_engine_config=new_rag_engine_config
    )
    
    print(updated_rag_engine_config)

### Update your `RagEngineConfig` to Unprovisioned tier

The following code samples demonstrate how to set the `RagEngineConfig` to the Spanner mode with Unprovisioned tier. This will permanently delete all the data from your Spanner deployment mode and halt billing expenses arising from it.

### Console

1.  In the Google Cloud console, go to the **RAG Engine** page.
2.  Select the region in which your RAG Engine is running.
3.  Click the **Switch to Spanner** button if not already on Spanner mode.
4.  Click **Delete RAG Engine** . A confirmation dialog appears.
5.  Verify that you're about to delete your data in RAG Engine by typing delete, then click **Confirm** .
6.  Click **Save** .

### REST

    PROJECT_ID: Your project ID.
    LOCATION: The region to process the request.

    curl -X PATCH \
    -H "Content-Type: application/json" \
    -H "Authorization: Bearer $(gcloud auth print-access-token)" \
    https://LOCATION-aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/LOCATION/ragEngineConfig -d "{'ragManagedDbConfig': {'spanner': {'unprovisioned': {}}}}"

### Python

    from vertexai.preview import rag
    import vertexai
    
    PROJECT_ID = YOUR_PROJECT_ID
    LOCATION = YOUR_RAG_ENGINE_LOCATION
    
    # Initialize API once per session
    vertexai.init(project=PROJECT_ID, location=LOCATION)
    
    rag_engine_config_name=f"projects/{PROJECT_ID}/locations/{LOCATION}/ragEngineConfig"
    
    new_rag_engine_config = rag.RagEngineConfig(
        name=rag_engine_config_name,
        rag_managed_db_config=rag.RagManagedDbConfig(mode=rag.Spanner(tier=rag.Unprovisioned())),
    )
    
    updated_rag_engine_config = rag.rag_data.update_rag_engine_config(
        rag_engine_config=new_rag_engine_config
    )
    
    print(updated_rag_engine_config)

## What's next

  - To learn more about supported generation models, see [Generative AI models that support RAG](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/rag-engine/supported-rag-models) .
  - To learn more about supported embedding models, see [Embedding models](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/rag-engine/use-embedding-models#supported-embedding-models) .
  - To learn more about open models, see [Open models](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/rag-engine/use-embedding-models#use-oss-embedding-models) .
  - To learn more about RAG Engine, see [RAG Engine overview](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/rag-engine/rag-overview) .
