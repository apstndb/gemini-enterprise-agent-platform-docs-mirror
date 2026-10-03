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
|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------|
| See [Corpus management parameters](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/models/rag-api#corpus-management-params-api) .               | See [Corpus management examples](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/models/rag-api#corpus-management-examples-api) . |
| See [File management parameters](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/models/rag-api#file-management-params-api) .                   | See [File management examples](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/models/rag-api#file-management-examples-api) .     |
| See [Retrieval and prediction parameters](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/models/rag-api#retrieval-and-prediction-params-api) . | See [Retrieval query example](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/models/rag-api#retrieval-query-api) .               |
| See [Project management parameters](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/models/rag-api#project-management-params-api) .             | See [Project management examples](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/models/rag-api#project-management-params-api) . |

### Corpus management parameters

For information about a RAG corpus, see [Corpus management](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/rag-engine/manage-your-rag-corpus#corpus-management) .

#### Create a RAG corpus

This table lists the parameters used to create a RAG corpus.

##### Body Request

| **Parameters**                           |                                                                                                                                                                                                                                                                                                                                                                                      |
|------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `corpus_type_config`                     | Optional: Immutable. `RagCorpus.CorpusTypeConfig` The configuration to specify the corpus type.                                                                                                                                                                                                                                                                                      |
| `display_name`                           | Required: `string` The display name of the RAG corpus.                                                                                                                                                                                                                                                                                                                               |
| `description`                            | Optional: `string` The description of the RAG corpus.                                                                                                                                                                                                                                                                                                                                |
| `encryption_spec`                        | Optional: Immutable: `string` The CMEK key name is used to encrypt at-rest data that's related to the RAG corpus. The key name is only applicable to the `RagManaged` option for the vector database. When the corpus is created, this field can be set and can't be updated or deleted. Format: `projects/{project}/locations/{location}/keyRings/{key_ring}/cryptoKeys/{key_name}` |
| `vector_db_config`                       | Optional: Immutable: `RagVectorDbConfig` The configuration for the vector databases.                                                                                                                                                                                                                                                                                                 |
| `vertex_ai_search_config.serving_config` | Optional: `string` The configuration for the Agent Search. Format: `projects/{project}/locations/{location}/collections/{collection}/engines/{engine}/servingConfigs/{serving_config}` or `projects/{project}/locations/{location}/collections/{collection}/dataStores/{data_store}/servingConfigs/{serving_config}`                                                                 |

##### `CorpusTypeConfig`

| **Parameters**             |                                                                                                                                                                                                                                                                                                                                                                           |
|----------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `document_corpus`          | `oneof` `RagCorpus.CorpusTypeConfig.DocumentCorpus` The default value of `corpus_type_config` , which represents a conventional document-based RAG corpus.                                                                                                                                                                                                                |
| `memory_corpus`            | `oneof` `RagCorpus.CorpusTypeConfig.MemoryCorpus` If you set this type, the RAG corpus is a `MemoryCorpus` that can be used with the Gemini Live API as a memory store. For more information, see [Use RAG Engine as the memory store](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/rag-engine/use-rag-in-multimodal-live#use-rag-memory-store) . |
| `memory_corpus.llm_parser` | `oneof` `RagFileParsingConfig.LlmParser` The LLM parser that's used to parse and store session contexts from the Gemini Live API. You can build memories for indexing.                                                                                                                                                                                                    |

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
<td><p><code>rag_managed_db</code></p></td>
<td><p><code>oneof</code> <code>vector_db</code> : <code>RagVectorDbConfig.RagManagedDb</code></p>
<p>If no vector database is specified, <code>rag_managed_db</code> is the default vector database.</p></td>
</tr>
<tr class="even">
<td><p><code>rag_managed_db.knn</code></p></td>
<td><p><code>oneof</code> <code>retrieval_strategy</code> : <code>KNN</code></p>
<p>Default.</p>
<p>Finds the exact nearest neighbors by comparing all data points in your RAG corpus.</p>
<p>If you don't specify a strategy during the creation of your RAG corpus, KNN is the default retrieval strategy used.</p></td>
</tr>
<tr class="odd">
<td><p><code>rag_managed_db.ann</code></p></td>
<td><p><code>oneof</code> <code>retrieval_strategy</code> : <code>ANN</code></p>
<p><code>tree_depth</code></p>
<p>Determines the number of layers or levels in the tree.</p>
If you have <code>O(10K)</code> RAG files in the RAG corpus, set thi value to 2.
<ul>
<li>If more layers or levels are required, set this value to 3.</li>
<li>If the number of layers or levels isn't specified, RAG Engine assigns a default value of 2 for this parameter.</li>
</ul>
<p><code>leaf_count</code></p>
<p>Determines the number of leaf nodes in the tree-based structure.</p>
<ul>
<li>The recommended value is <code>10 * sqrt(num of RAG files in your RAG corpus)</code> .</li>
<li>If not specified, RAG Engine assigns a <em>default value of 500</em> for this parameter.</li>
</ul>
<p><code>rebuild_ann_index</code></p>
<ul>
<li>RAG Engine rebuilds your ANN index.</li>
<li>Set to <code>true</code> in your <code>ImportRagFiles</code> API request.</li>
<li>Before you query the RAG corpus, it's required to rebuild the ANN index once.</li>
<li>Only one concurrent index rebuild is supported on a project in each location.</li>
</ul></td>
</tr>
<tr class="even">
<td><p><code>weaviate</code></p></td>
<td><p><code>oneof</code> <code>vector_db</code> : <code>RagVectorDbConfig.Weaviate</code></p>
<p>Specifies your Weaviate instance.</p></td>
</tr>
<tr class="odd">
<td><p><code>weaviate.http_endpoint</code></p></td>
<td><p><code>string</code></p>
<p>The Weaviate instance's HTTP endpoint.</p>
<p>This value can't be changed after it's set. You can leave it empty in the <code>CreateRagCorpus</code> API call, and set it with a non-empty value in a follow up <code>UpdateRagCorpus</code> API call.</p></td>
</tr>
<tr class="even">
<td><p><code>weaviate.collection_name</code></p></td>
<td><p><code>string</code></p>
<p>The Weaviate collection that the RAG corpus maps to.</p>
<p>This value can't be changed after it's set. You can leave it empty in the <code>CreateRagCorpus</code> API call, and set it with a non-empty value in a follow up <code>UpdateRagCorpus</code> API call.</p></td>
</tr>
<tr class="odd">
<td><p><code>pinecone</code></p></td>
<td><p><code>oneof</code> <code>vector_db</code> : <code>RagVectorDbConfig.Pinecone</code></p>
<p>Specifies your Pinecone instance.</p></td>
</tr>
<tr class="even">
<td><p><code>pinecone.index_name</code></p></td>
<td><p><code>string</code></p>
<p>This is the name used to create the Pinecone index that's used with the RAG corpus.</p>
<p>This value can't be changed after it's set. You can leave it empty in the <code>CreateRagCorpus</code> API call, and set it with a non-empty value in a follow up <code>UpdateRagCorpus</code> API call.</p></td>
</tr>
<tr class="odd">
<td><p><code>vertex_feature_store</code></p></td>
<td><p><code>oneof</code> <code>vector_db</code> : <code>RagVectorDbConfig.VertexFeatureStore</code></p>
<p>Specifies your Feature Store on Gemini Enterprise Agent Platform instance.</p></td>
</tr>
<tr class="even">
<td><p><code>vertex_feature_store.feature_view_resource_name</code></p></td>
<td><p><code>string</code></p>
<p>The Agent Platform Feature Store <code>FeatureView</code> that the RAG corpus maps to.</p>
<p>Format: <code>projects/{project}/locations/{location}/featureOnlineStores/{feature_online_store}/featureViews/{feature_view}</code></p>
<p>This value can't be changed after it's set. You can leave it empty in the <code>CreateRagCorpus</code> API call, and set it with a non-empty value in a follow up <code>UpdateRagCorpus</code> API call.</p></td>
</tr>
<tr class="odd">
<td><p><code>vertex_vector_search</code></p></td>
<td><p><code>oneof</code> <code>vector_db</code> : <code>RagVectorDbConfig.VertexVectorSearch</code></p>
<p>Specifies your Vector Search on Gemini Enterprise Agent Platform instance.</p></td>
</tr>
<tr class="even">
<td><p><code>vertex_vector_search.index</code></p></td>
<td><p><code>string</code></p>
<p>This is the resource name of the Vector Search index that's used with the RAG corpus.</p>
<p>Format: <code>projects/{project}/locations/{location}/indexEndpoints/{index_endpoint}</code></p>
<p>This value can't be changed after it's set. You can leave it empty in the <code>CreateRagCorpus</code> API call, and set it with a non-empty value in a follow up <code>UpdateRagCorpus</code> API call.</p></td>
</tr>
<tr class="odd">
<td><p><code>vertex_vector_search.index_endpoint</code></p></td>
<td><p><code>string</code></p>
<p>This is the resource name of the Vector Search index endpoint that's used with the RAG corpus.</p>
<p>Format: <code>projects/{project}/locations/{location}/indexes/{index}</code></p>
<p>This value can't be changed after it's set. You can leave it empty in the <code>CreateRagCorpus</code> API call, and set it with a non-empty value in a follow up <code>UpdateRagCorpus</code> API call.</p></td>
</tr>
<tr class="even">
<td><p><code>api_auth.api_key_config.api_key_secret_version</code></p></td>
<td><p><code>string</code></p>
<p>This the full resource name of the secret that is stored in Secret Manager, which contains your Weaviate or Pinecone API key that depends on your choice of vector database.</p>
<p>Format: <code>projects/{PROJECT_NUMBER}/secrets/{SECRET_ID}/versions/{VERSION_ID}</code></p>
<p>You can leave it empty in the <code>CreateRagCorpus</code> API call, and set it with a non-empty value in a follow up <code>UpdateRagCorpus</code> API call.</p></td>
</tr>
<tr class="odd">
<td><p><code>rag_embedding_model_config.vertex_prediction_endpoint.endpoint</code></p></td>
<td><p>Optional: Immutable: <code>string</code></p>
<p>The embedding model to use for the RAG corpus. This value can't be changed after it's set. If you leave it empty, we use <a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/models/text-embeddings-api">text-embedding-005</a> as the embedding model.</p></td>
</tr>
</tbody>
</table>

#### Update a RAG corpus

This table lists the parameters used to update a RAG corpus.

##### Body Request

| **Parameters**                                                  |                                                                                                                                                                                                                                                                                                                                                                    |
|-----------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `display_name`                                                  | Optional: `string` The display name of the RAG corpus.                                                                                                                                                                                                                                                                                                             |
| `description`                                                   | Optional: `string` The description of the RAG corpus.                                                                                                                                                                                                                                                                                                              |
| `rag_vector_db.weaviate.http_endpoint`                          | `string` The Weaviate instance's HTTP endpoint. If your `RagCorpus` was created with a `Weaviate` configuration, and this field has never been set before, then you can update the Weaviate instance's HTTP endpoint.                                                                                                                                              |
| `rag_vector_db.weaviate.collection_name`                        | `string` The Weaviate collection that the RAG corpus maps to. If your `RagCorpus` was created with a `Weaviate` configuration, and this field has never been set before, then you can update the Weaviate instance's collection name.                                                                                                                              |
| `rag_vector_db.pinecone.index_name`                             | `string` This is the name used to create the Pinecone index that's used with the RAG corpus. If your `RagCorpus` was created with a `Pinecone` configuration, and this field has never been set before, then you can update the Pinecone instance's index name.                                                                                                    |
| `rag_vector_db.vertex_feature_store.feature_view_resource_name` | `string` The Agent Platform Feature Store `FeatureView` that the RAG corpus maps to. Format: `projects/{project}/locations/{location}/featureOnlineStores/{feature_online_store}/featureViews/{feature_view}` If your `RagCorpus` was created with a Agent Platform Feature Store configuration, and this field has never been set before, then you can update it. |
| `rag_vector_db.vertex_vector_search.index`                      | `string` This is the resource name of the Vector Search index that's used with the RAG corpus. Format: `projects/{project}/locations/{location}/indexEndpoints/{index_endpoint}` If your `RagCorpus` was created with a `Vector Search` configuration, and this field has never been set before, then you can update it.                                           |
| `rag_vector_db.vertex_vector_search.index_endpoint`             | `string` This is the resource name of the Vector Search index endpoint that's used with the RAG corpus. Format: `projects/{project}/locations/{location}/indexes/{index}` If your `RagCorpus` was created with a `Vector Search` configuration, and this field has never been set before, then you can update it.                                                  |
| `rag_vector_db.api_auth.api_key_config.api_key_secret_version`  | `string` The full resource name of the secret that is stored in Secret Manager, which contains your Weaviate or Pinecone API key depends on your choice of vector database. Format: `projects/{PROJECT_NUMBER}/secrets/{SECRET_ID}/versions/{VERSION_ID}`                                                                                                          |

#### List RAG corpora

This table lists the parameters used to list RAG corpora.

| **Parameters** |                                                                                                                                                                                       |
|----------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `page_size`    | Optional: `int` The standard list page size.                                                                                                                                          |
| `page_token`   | Optional: `string` The standard list page token. Typically obtained from `[ListRagCorporaResponse.next_page_token][]` of the previous `[VertexRagDataService.ListRagCorpora][]` call. |

#### Get a RAG corpus

This table lists parameters used to get a RAG corpus.

| Parameters |                                                                                                                             |
|------------|-----------------------------------------------------------------------------------------------------------------------------|
| `name`     | `string` The name of the `RagCorpus` resource. Format: `projects/{project}/locations/{location}/ragCorpora/{rag_corpus_id}` |

#### Delete a RAG corpus

This table lists parameters used to delete a RAG corpus.

| **Parameters** |                                                                                                                             |
|----------------|-----------------------------------------------------------------------------------------------------------------------------|
| `name`         | `string` The name of the `RagCorpus` resource. Format: `projects/{project}/locations/{location}/ragCorpora/{rag_corpus_id}` |

#### Batch create metadata schemas

This table lists the parameters used to batch create metadata schemas for a RAG corpus.

##### Body Request

| **Parameters** |                                                                                                 |
|----------------|-------------------------------------------------------------------------------------------------|
| `requests`     | Required: list of `CreateRagDataSchemaRequest` The request messages for `CreateRagDataSchema` . |

##### `CreateRagDataSchemaRequest`

| **Parameters**    |                                                          |
|-------------------|----------------------------------------------------------|
| `rag_data_schema` | Required: `RagDataSchema` The metadata schema to create. |

##### `RagDataSchema`

| **Parameters**   |                                                                |
|------------------|----------------------------------------------------------------|
| `key`            | Required: `string` The key of the metadata schema.             |
| `schema_details` | `RagMetadataSchemaDetails` The details of the metadata schema. |

##### `RagMetadataSchemaDetails`

| **Parameters** |                                                                                                                              |
|----------------|------------------------------------------------------------------------------------------------------------------------------|
| `type`         | `DataType` The data type of the metadata schema. Options: `INTEGER` , `FLOAT` , `STRING` , `DATETIME` , `BOOLEAN` , `LIST` . |

#### List metadata schemas

This table lists the parameters used to list metadata schemas.

| **Parameters** | **Description**                                                                                                                        |
|----------------|----------------------------------------------------------------------------------------------------------------------------------------|
| `parent`       | Required: `string` The resource name of the `RagCorpus` . Format: `projects/{project}/locations/{location}/ragCorpora/{rag_corpus_id}` |

#### Batch delete metadata schemas

This table lists the parameters used to batch delete metadata schemas.

| **Parameters** |                                                                                                                                                                                                  |
|----------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `names`        | Required: list of `string` The resource names of the `RagDataSchema` to delete. Format: `projects/{project}/locations/{location}/ragCorpora/{rag_corpus_id}/ragDataSchemas/{rag_data_schema_id}` |

### File management parameters

For information about a RAG file and its metadata, see [File management](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/rag-engine/manage-your-rag-corpus#file-management) .

#### Upload a RAG file

This table lists parameters used to upload a RAG file.

##### Body Request

| **Parameters**           |                                                                                                                             |
|--------------------------|-----------------------------------------------------------------------------------------------------------------------------|
| `parent`                 | `string` The name of the `RagCorpus` resource. Format: `projects/{project}/locations/{location}/ragCorpora/{rag_corpus_id}` |
| `rag_file`               | Required: `RagFile` The file to upload.                                                                                     |
| `upload_rag_file_config` | Required: `UploadRagFileConfig` The configuration for the `RagFile` to be uploaded into the `RagCorpus` .                   |

| `RagFile`      | **Description**                                      |
|----------------|------------------------------------------------------|
| `display_name` | Required: `string` The display name of the RAG file. |
| `description`  | Optional: `string` The description of the RAG file.  |

| `UploadRagFileConfig`                                                                         | **Description**                          |
|-----------------------------------------------------------------------------------------------|------------------------------------------|
| `rag_file_transformation_config.rag_file_chunking_config.fixed_length_chunking.chunk_size`    | `int32` Number of tokens each chunk has. |
| `rag_file_transformation_config.rag_file_chunking_config.fixed_length_chunking.chunk_overlap` | `int32` The overlap between chunks.      |

#### Import RAG files

This table lists parameters used to import a RAG file.

| **Parameters**                                                                                |                                                                                                                                                                                                                                                                                                                                                   |
|-----------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `parent`                                                                                      | Required: `string` The name of the `RagCorpus` resource. Format: `projects/{project}/locations/{location}/ragCorpora/{rag_corpus_id}`                                                                                                                                                                                                             |
| `gcs_source`                                                                                  | `oneof` `import_source` : `GcsSource` Cloud Storage location. Supports importing individual files as well as entire Cloud Storage directories.                                                                                                                                                                                                    |
| `gcs_source.uris`                                                                             | `list` of `string` Cloud Storage URI that contains the upload file.                                                                                                                                                                                                                                                                               |
| `google_drive_source`                                                                         | `oneof` `import_source` : `GoogleDriveSource` Google Drive location. Supports importing individual files as well as Google Drive folders.                                                                                                                                                                                                         |
| `slack_source`                                                                                | `oneof` `import_source` : `SlackSource` The slack channel where the file is uploaded.                                                                                                                                                                                                                                                             |
| `jira_source`                                                                                 | `oneof` `import_source` : `JiraSource` The Jira query where the file is uploaded.                                                                                                                                                                                                                                                                 |
| `share_point_sources`                                                                         | `oneof` `import_source` : `SharePointSources` The SharePoint sources where the file is uploaded.                                                                                                                                                                                                                                                  |
| `rag_file_transformation_config.rag_file_chunking_config.fixed_length_chunking.chunk_size`    | `int32` Number of tokens each chunk has.                                                                                                                                                                                                                                                                                                          |
| `rag_file_transformation_config.rag_file_chunking_config.fixed_length_chunking.chunk_overlap` | `int32` The overlap between chunks.                                                                                                                                                                                                                                                                                                               |
| `rag_file_parsing_config`                                                                     | Optional: `RagFileParsingConfig` Specifies the parsing configuration for `RagFiles` . If this field isn't set, RAG uses the default parser.                                                                                                                                                                                                       |
| `max_embedding_requests_per_min`                                                              | Optional: `int32` The maximum number of queries per minute that this job is allowed to make to the embedding model specified on the corpus. This value is specific to this job and not shared across other import jobs. Consult the Quotas page on the project to set an appropriate value. If unspecified, a default value of 1,000 QPM is used. |

| `GoogleDriveSource`          |                                                           |
|------------------------------|-----------------------------------------------------------|
| `resource_ids.resource_id`   | Required: `string` The ID of the Google Drive resource.   |
| `resource_ids.resource_type` | Required: `string` The type of the Google Drive resource. |

| `SlackSource`                                    |                                                                                                                                                                                                                                                                                                                            |
|--------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `channels.channels`                              | Repeated: `SlackSource.SlackChannels.SlackChannel` Slack channel information, include ID and time range to import.                                                                                                                                                                                                         |
| `channels.channels.channel_id`                   | Required: `string` The Slack channel ID.                                                                                                                                                                                                                                                                                   |
| `channels.channels.start_time`                   | Optional: `google.protobuf.Timestamp` The starting timestamp for messages to import.                                                                                                                                                                                                                                       |
| `channels.channels.end_time`                     | Optional: `google.protobuf.Timestamp` The ending timestamp for messages to import.                                                                                                                                                                                                                                         |
| `channels.api_key_config.api_key_secret_version` | Required: `string` The full resource name of the secret that is stored in Secret Manager, which contains a Slack channel access token that has access to the slack channel IDs. See: https://api.slack.com/tutorials/tracks/getting-a-token. Format: `projects/{PROJECT_NUMBER}/secrets/{SECRET_ID}/versions/{VERSION_ID}` |

| `JiraSource`                                         |                                                                                                                                                                                                                                                                                                                                                       |
|------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `jira_queries.projects`                              | Repeated: `string` A list of Jira projects to import in their entirety.                                                                                                                                                                                                                                                                               |
| `jira_queries.custom_queries`                        | Repeated: `string` A list of custom Jira queries to import. For information about JQL (Jira Query Language), see [Jira Support](https://support.atlassian.com/jira-service-management-cloud/docs/use-advanced-search-with-jira-query-language-jql/)                                                                                                   |
| `jira_queries.email`                                 | Required: `string` The Jira email address.                                                                                                                                                                                                                                                                                                            |
| `jira_queries.server_uri`                            | Required: `string` The Jira server URI.                                                                                                                                                                                                                                                                                                               |
| `jira_queries.api_key_config.api_key_secret_version` | Required: `string` The full resource name of the secret that is stored in Secret Manager, which contains Jira API key that has access to the slack channel IDs. See: https://support.atlassian.com/atlassian-account/docs/manage-api-tokens-for-your-atlassian-account/ Format: `projects/{PROJECT_NUMBER}/secrets/{SECRET_ID}/versions/{VERSION_ID}` |

| `SharePointSources`                                        |                                                                                                                                                                                                                                                |
|------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `share_point_sources.sharepoint_folder_path`               | `oneof` in `folder_source` : `string` The path of the SharePoint folder to download from.                                                                                                                                                      |
| `share_point_sources.sharepoint_folder_id`                 | `oneof` in `folder_source` : `string` The ID of the SharePoint folder to download from.                                                                                                                                                        |
| `share_point_sources.drive_name`                           | `oneof` in `drive_source` : `string` The name of the drive to download from.                                                                                                                                                                   |
| `share_point_sources.drive_id`                             | `oneof` in `drive_source` : `string` The ID of the drive to download from.                                                                                                                                                                     |
| `share_point_sources.client_id`                            | `string` The Application ID for the app registered in Microsoft Azure Portal. The application must also be configured with MS Graph permissions "Files.ReadAll", "Sites.ReadAll" and BrowserSiteLists.Read.All.                                |
| `share_point_sources.client_secret.api_key_secret_version` | Required: `string` The full resource name of the secret that is stored in Secret Manager, which contains the application secret for the app registered in Azure. Format: `projects/{PROJECT_NUMBER}/secrets/{SECRET_ID}/versions/{VERSION_ID}` |
| `share_point_sources.tenant_id`                            | `string` Unique identifier of the Azure Active Directory Instance.                                                                                                                                                                             |
| `share_point_sources.sharepoint_site_name`                 | `string` The name of the SharePoint site to download from. This can be the site name or the site id.                                                                                                                                           |

| `RagFileParsingConfig`                       |                                                                                                                                                                                                                                                                                                                                                                                                            |
|----------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `layout_parser`                              | `oneof` `parser` : `RagFileParsingConfig.LayoutParser` The Layout Parser to use for `RagFile` s.                                                                                                                                                                                                                                                                                                           |
| `layout_parser.processor_name`               | `string` The full resource name of a Document AI processor or processor version. Format: `projects/{project_id}/locations/{location}/processors/{processor_id}` `projects/{project_id}/locations/{location}/processors/{processor_id}/processorVersions/{processor_version_id}`                                                                                                                            |
| `layout_parser.max_parsing_requests_per_min` | `string` The maximum number of requests the job is allowed to make to the Document AI processor per minute. Consult https://cloud.google.com/document-ai/quotas and the Quota page for your project to set an appropriate value here. If unspecified, a default value of 120 QPM is used.                                                                                                                  |
| `llm_parser`                                 | `oneof` `parser` : `RagFileParsingConfig.LlmParser` The LLM parser to use for `RagFile` s.                                                                                                                                                                                                                                                                                                                 |
| `llm_parser.model_name`                      | `string` The resource name of an LLM model. Format: `{publisher}/models/{model}`                                                                                                                                                                                                                                                                                                                           |
| `llm_parser.max_parsing_requests_per_min`    | `string` The maximum number of requests the job is allowed to make to the LLM model per minute. To set an appropriate value for your project, see the [model quota section](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/quotas#quota_system_by_model) and the Quota page for your project to set an appropriate value here. If unspecified, a default value of 5000 QPM is used. |

#### Get a RAG file

This table lists parameters used to get a RAG file.

| **Parameters** |                                                                                                                         |
|----------------|-------------------------------------------------------------------------------------------------------------------------|
| `name`         | `string` The name of the `RagFile` resource. Format: `projects/{project}/locations/{location}/ragCorpora/{rag_file_id}` |

#### Delete a RAG file

This table lists parameters used to delete a RAG file.

| Parameters |                                                                                                                         |
|------------|-------------------------------------------------------------------------------------------------------------------------|
| `name`     | `string` The name of the `RagFile` resource. Format: `projects/{project}/locations/{location}/ragCorpora/{rag_file_id}` |

#### Batch create metadata

This table lists the parameters used to batch create metadata for a RAG file.

##### Body Request

| **Parameters** |                                                                                             |
|----------------|---------------------------------------------------------------------------------------------|
| `requests`     | Required: list of `CreateRagMetadataRequest` The request messages for `CreateRagMetadata` . |

##### `CreateRagMetadataRequest`

| **Parameters**    |                                                                                                                           |
|-------------------|---------------------------------------------------------------------------------------------------------------------------|
| `rag_metadata`    | Required: `RagMetadata` The metadata to create.                                                                           |
| `rag_metadata_id` | Optional: `string` The ID to use for the metadata, which will become the final component of the metadata's resource name. |

##### `RagMetadata`

| **Parameters**            |                                                         |
|---------------------------|---------------------------------------------------------|
| `user_specified_metadata` | `UserSpecifiedMetadata` The metadata provided by users. |

##### `UserSpecifiedMetadata`

| **Parameters** |                                                                                                             |
|----------------|-------------------------------------------------------------------------------------------------------------|
| `key`          | Required: `string` The key of the metadata. The key must correspond to a key defined in a `RagDataSchema` . |
| `value`        | `MetadataValue` The value of the metadata.                                                                  |

##### `MetadataValue`

| **Parameters**   |                                |
|------------------|--------------------------------|
| `int_value`      | `oneof value` : `int64`        |
| `float_value`    | `oneof value` : `float`        |
| `str_value`      | `oneof value` : `string`       |
| `datetime_value` | `oneof value` : `string`       |
| `bool_value`     | `oneof value` : `boolean`      |
| `list_value`     | `oneof value` : `MetadataList` |

#### List metadata

This table lists the parameters used to list metadata for a RAG file.

| **Parameters** |                                                                                                                                                             |
|----------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `parent`       | Required: `string` The resource name of the `RagFile` . Format: `projects/{project}/locations/{location}/ragCorpora/{rag_corpus_id}/ragFiles/{rag_file_id}` |

#### Update metadata

This table lists the parameters used to update metadata.

| **Parameters** |                                                                                      |
|----------------|--------------------------------------------------------------------------------------|
| `rag_metadata` | Required: `RagMetadata` The `RagMetadata` which replaces the resource on the server. |

#### Batch delete metadata

This table lists the parameters used to batch delete metadata.

| **Parameters** |                                                                                                                                                                                                                 |
|----------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `names`        | Required: list of `string` The resource names of the `RagMetadata` to delete. Format: `projects/{project}/locations/{location}/ragCorpora/{rag_corpus_id}/ragFiles/{rag_file_id}/ragMetadata/{rag_metadata_id}` |

### Retrieval and prediction parameters

This section lists the retrieval and prediction parameters.

#### Retrieval parameters

This table lists parameters for `retrieveContexts` API.

| **Parameters**     |                                                                                                                                                                                                |
|--------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `parent`           | Required: `string` The resource name of the Location to perform the retrieval. The users must have permission to make a call in the project. Format: `projects/{project}/locations/{location}` |
| `vertex_rag_store` | `VertexRagStore` The data source for RagStore.                                                                                                                                                 |
| `query`            | Required: `RagQuery` Single RAG retrieve query.                                                                                                                                                |

##### `VertexRagStore`

| `VertexRagStore`             |                                                                                                                                                                                |
|------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `rag_resources`              | list: `RagResource` The representation of the RAG source. It can be used to specify the corpus only or `RagFile` s. Only support one corpus or multiple files from one corpus. |
| `rag_resources.rag_corpus`   | Optional: `string` `RagCorpora` resource name. Format: `projects/{project}/locations/{location}/ragCorpora/{rag_corpus}`                                                       |
| `rag_resources.rag_file_ids` | list: `string` A list of `RagFile` resources. Format: `projects/{project}/locations/{location}/ragCorpora/{rag_corpus}/ragFiles/{rag_file}`                                    |

| `RagQuery`             |                                                                           |
|------------------------|---------------------------------------------------------------------------|
| `text`                 | `string` The query in text format to get relevant contexts.               |
| `rag_retrieval_config` | Optional: `RagRetrievalConfig` The retrieval configuration for the query. |

| `RagRetrievalConfig`                 |                                                                                                                                                                                                                                                                                                                                       |
|--------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `top_k`                              | Optional: `int32` The number of contexts to retrieve.                                                                                                                                                                                                                                                                                 |
| `hybrid_search.alpha`                | Optional: `float` Alpha value controls the weight between dense and sparse vector search results. The range is \[0, 1\], where 0 means sparse vector search only and 1 means dense vector search only. The default value is 0.5, which balances sparse and dense vector search equally. Hybrid Search is only available for Weaviate. |
| `filter.vector_distance_threshold`   | `oneof vector_db_threshold` : `double` Only returns contexts with a vector distance smaller than the threshold.                                                                                                                                                                                                                       |
| `filter.metadata_filter`             | Optional: `string` The metadata filter to apply during retrieval, using Common Expression Language (CEL). For more information, see \[Metadata search\](/gemini-enterprise-agent-platform/build/rag-engine/use-metadata-search). Example: `author == "Shakespeare" && page_number == 42`                                              |
| `filter.vector_similarity_threshold` | `oneof vector_db_threshold` : `double` Only returns contexts with vector similarity larger than the threshold.                                                                                                                                                                                                                        |
| `ranking.rank_service.model_name`    | Optional: `string` The model name of the rank service. Example: `semantic-ranker-512@latest`                                                                                                                                                                                                                                          |
| `ranking.llm_ranker.model_name`      | Optional: `string` The model name used for ranking. Example: `gemini-3.5-flash`                                                                                                                                                                                                                                                       |

#### Async retrieval parameters

This table lists parameters for `asyncRetrieveContexts` API.

| **Parameters** |                                                                                                                                                                                                  |
|----------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `parent`       | Required: `string` The resource name of the Location to retrieve `RagContexts` . The users must have permission to make a call in the project. Format: `projects/{project}/locations/{location}` |
| `query`        | Required: `RagQuery` Single RAG retrieve query.                                                                                                                                                  |
| `tools`        | Optional: list of `Tool` The tools to use for retrieval. Supported tools include `retrieval` which specifies the `vertex_rag_store` .                                                            |

#### Ask contexts parameters

This table lists parameters for `askContexts` API.

| **Parameters** |                                                                                                                                                                                                  |
|----------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `parent`       | Required: `string` The resource name of the Location to retrieve `RagContexts` . The users must have permission to make a call in the project. Format: `projects/{project}/locations/{location}` |
| `query`        | Required: `RagQuery` Single RAG retrieve query.                                                                                                                                                  |
| `tools`        | Optional: list of `Tool` The tools to use for retrieval. Supported tools include `retrieval` which specifies the `vertex_rag_store` .                                                            |

#### Prediction parameters

This table lists prediction parameters.

| `GenerateContentRequest`           |                                                                                |
|------------------------------------|--------------------------------------------------------------------------------|
| `tools.retrieval.vertex_rag_store` | `VertexRagStore` Set to use a data source powered by Agent Platform RAG store. |

See [VertexRagStore](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/models/rag-api#ragStore) for details.

### Project management parameters

This table lists project-level parameters.

##### `RagEngineConfig`

| **Parameters**                             |                                                                                                                                            |
|--------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------|
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

- ` PROJECT_ID ` : Your [project ID](https://docs.cloud.google.com/resource-manager/docs/creating-managing-projects#identifiers) . .
- ` LOCATION ` : The region to process the request.
- ` CORPUS_DISPLAY_NAME ` : The display name of the `RagCorpus` .
- ` CORPUS_DESCRIPTION ` : The description of the `RagCorpus` .

HTTP method and URL:

```
POST https://LOCATION-aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/LOCATION/ragCorpora
```

Request JSON body:

```
{
  "display_name" : "CORPUS_DISPLAY_NAME",
  "description": "CORPUS_DESCRIPTION",
}
```

To send your request, choose one of these options:

#### curl

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) , or by using [Cloud Shell](https://docs.cloud.google.com/shell/docs) , which automatically logs you into the `gcloud` CLI . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Save the request body in a file named `request.json` , and execute the following command:

```
curl -X POST \
     -H "Authorization: Bearer $(gcloud auth print-access-token)" \
     -H "Content-Type: application/json; charset=utf-8" \
     -d @request.json \
     "https://LOCATION-aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/LOCATION/ragCorpora"
```

#### PowerShell

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Save the request body in a file named `request.json` , and execute the following command:

```
$cred = gcloud auth print-access-token
$headers = @{ "Authorization" = "Bearer $cred" }

Invoke-WebRequest `
    -Method POST `
    -Headers $headers `
    -ContentType: "application/json; charset=utf-8" `
    -InFile request.json `
    -Uri "https://LOCATION-aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/LOCATION/ragCorpora" | Select-Object -Expand Content
```

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

- ` PROJECT_ID ` : Your [project ID](https://docs.cloud.google.com/resource-manager/docs/creating-managing-projects#identifiers) . .
- ` LOCATION ` : The region to process the request.
- ` CORPUS_ID ` : The corpus ID of your RAG corpus.
- ` CORPUS_DISPLAY_NAME ` : The display name of the `RagCorpus` .
- ` CORPUS_DESCRIPTION ` : The description of the `RagCorpus` .
- ` INDEX_NAME ` : The resource name of the `Vector Search Index` . Format: `projects/{project}/locations/{location}/indexes/{index}`
- ` INDEX_ENDPOINT_NAME ` : The resource name of the `Vector Search Index Endpoint` . Format: `projects/{project}/locations/{location}/indexEndpoints/{index_endpoint}`

HTTP method and URL:

```
PATCH https://LOCATION-aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/LOCATION/ragCorpora/CORPUS_ID
```

Request JSON body:

```
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
```

To send your request, choose one of these options:

#### curl

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) , or by using [Cloud Shell](https://docs.cloud.google.com/shell/docs) , which automatically logs you into the `gcloud` CLI . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Save the request body in a file named `request.json` , and execute the following command:

```
curl -X PATCH \
     -H "Authorization: Bearer $(gcloud auth print-access-token)" \
     -H "Content-Type: application/json; charset=utf-8" \
     -d @request.json \
     "https://LOCATION-aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/LOCATION/ragCorpora/CORPUS_ID"
```

#### PowerShell

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Save the request body in a file named `request.json` , and execute the following command:

```
$cred = gcloud auth print-access-token
$headers = @{ "Authorization" = "Bearer $cred" }

Invoke-WebRequest `
    -Method PATCH `
    -Headers $headers `
    -ContentType: "application/json; charset=utf-8" `
    -InFile request.json `
    -Uri "https://LOCATION-aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/LOCATION/ragCorpora/CORPUS_ID" | Select-Object -Expand Content
```

You should receive a successful status code (2xx).

### List RAG corpora example

This code sample demonstrates how to list all of the RAG corpora.

### REST

Before using any of the request data, make the following replacements:

- ` PROJECT_ID ` : Your [project ID](https://docs.cloud.google.com/resource-manager/docs/creating-managing-projects#identifiers) . .
- ` LOCATION ` : The region to process the request.
- ` PAGE_SIZE ` : The standard list page size. You may adjust the number of `RagCorpora` to return per page by updating the `page_size` parameter.
- ` PAGE_TOKEN ` : The standard list page token. Obtained typically using `ListRagCorporaResponse.next_page_token` of the previous `VertexRagDataService.ListRagCorpora` call.

HTTP method and URL:

```
GET https://LOCATION-aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/LOCATION/ragCorpora?page_size=PAGE_SIZE&page_token=PAGE_TOKEN
```

To send your request, choose one of these options:

#### curl

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) , or by using [Cloud Shell](https://docs.cloud.google.com/shell/docs) , which automatically logs you into the `gcloud` CLI . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Execute the following command:

```
curl -X GET \
     -H "Authorization: Bearer $(gcloud auth print-access-token)" \
     "https://LOCATION-aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/LOCATION/ragCorpora?page_size=PAGE_SIZE&page_token=PAGE_TOKEN"
```

#### PowerShell

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Execute the following command:

```
$cred = gcloud auth print-access-token
$headers = @{ "Authorization" = "Bearer $cred" }

Invoke-WebRequest `
    -Method GET `
    -Headers $headers `
    -Uri "https://LOCATION-aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/LOCATION/ragCorpora?page_size=PAGE_SIZE&page_token=PAGE_TOKEN" | Select-Object -Expand Content
```

You should receive a successful status code (\`2xx\`) and a list of `RagCorpora` under the given `PROJECT_ID` .

### Get a RAG corpus example

### REST

Before using any of the request data, make the following replacements:

- ` PROJECT_ID ` : Your [project ID](https://docs.cloud.google.com/resource-manager/docs/creating-managing-projects#identifiers) . .
- ` LOCATION ` : The region to process the request.
- ` RAG_CORPUS_ID ` : The ID of the `RagCorpus` resource.

HTTP method and URL:

```
GET https://LOCATION-aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/LOCATION/ragCorpora/RAG_CORPUS_ID
```

To send your request, choose one of these options:

#### curl

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) , or by using [Cloud Shell](https://docs.cloud.google.com/shell/docs) , which automatically logs you into the `gcloud` CLI . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Execute the following command:

```
curl -X GET \
     -H "Authorization: Bearer $(gcloud auth print-access-token)" \
     "https://LOCATION-aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/LOCATION/ragCorpora/RAG_CORPUS_ID"
```

#### PowerShell

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Execute the following command:

```
$cred = gcloud auth print-access-token
$headers = @{ "Authorization" = "Bearer $cred" }

Invoke-WebRequest `
    -Method GET `
    -Headers $headers `
    -Uri "https://LOCATION-aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/LOCATION/ragCorpora/RAG_CORPUS_ID" | Select-Object -Expand Content
```

A successful response returns the `RagCorpus` resource.

The `get` and `list` commands are used in an example to demonstrate how `RagCorpus` uses the `rag_embedding_model_config` field with in the `vector_db_config` , which points to the embedding model you have chosen.

```
  PROJECT_ID: Your project ID.
  LOCATION: The region to process the request.
  RAG_CORPUS_ID: The corpus ID of your RAG corpus.
```

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
```

### Delete a RAG corpus example

### REST

Before using any of the request data, make the following replacements:

- ` PROJECT_ID ` : Your [project ID](https://docs.cloud.google.com/resource-manager/docs/creating-managing-projects#identifiers) . .
- ` LOCATION ` : The region to process the request.
- ` RAG_CORPUS_ID ` : The ID of the `RagCorpus` resource.

HTTP method and URL:

```
DELETE https://LOCATION-aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/LOCATION/ragCorpora/RAG_CORPUS_ID
```

To send your request, choose one of these options:

#### curl

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) , or by using [Cloud Shell](https://docs.cloud.google.com/shell/docs) , which automatically logs you into the `gcloud` CLI . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Execute the following command:

```
curl -X DELETE \
     -H "Authorization: Bearer $(gcloud auth print-access-token)" \
     "https://LOCATION-aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/LOCATION/ragCorpora/RAG_CORPUS_ID"
```

#### PowerShell

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Execute the following command:

```
$cred = gcloud auth print-access-token
$headers = @{ "Authorization" = "Bearer $cred" }

Invoke-WebRequest `
    -Method DELETE `
    -Headers $headers `
    -Uri "https://LOCATION-aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/LOCATION/ragCorpora/RAG_CORPUS_ID" | Select-Object -Expand Content
```

A successful response returns the `DeleteOperationMetadata` .

### Batch create metadata schemas example

This code sample demonstrates how to batch create metadata schemas for a RAG corpus.

### REST

Before using any of the request data, make the following replacements:

- ` PROJECT_ID ` : Your [project ID](https://docs.cloud.google.com/resource-manager/docs/creating-managing-projects#identifiers) . .
- ` LOCATION ` : The region to process the request.
- ` RAG_CORPUS_ID ` : The ID of the `RagCorpus` resource.
- ` SCHEMA_KEY_1 ` : The key for the first metadata schema.
- ` SCHEMA_TYPE_1 ` : The data type for the first metadata schema (e.g., `INTEGER` ).
- ` SCHEMA_KEY_2 ` : The key for the second metadata schema.
- ` SCHEMA_TYPE_2 ` : The data type for the second metadata schema (e.g., `STRING` ).

HTTP method and URL:

```
POST https://LOCATION-aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/LOCATION/ragCorpora/RAG_CORPUS_ID/ragDataSchemas:batchCreate
```

Request JSON body:

```
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
```

To send your request, choose one of these options:

#### curl

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) , or by using [Cloud Shell](https://docs.cloud.google.com/shell/docs) , which automatically logs you into the `gcloud` CLI . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Save the request body in a file named `request.json` , and execute the following command:

```
curl -X POST \
     -H "Authorization: Bearer $(gcloud auth print-access-token)" \
     -H "Content-Type: application/json; charset=utf-8" \
     -d @request.json \
     "https://LOCATION-aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/LOCATION/ragCorpora/RAG_CORPUS_ID/ragDataSchemas:batchCreate"
```

#### PowerShell

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Save the request body in a file named `request.json` , and execute the following command:

```
$cred = gcloud auth print-access-token
$headers = @{ "Authorization" = "Bearer $cred" }

Invoke-WebRequest `
    -Method POST `
    -Headers $headers `
    -ContentType: "application/json; charset=utf-8" `
    -InFile request.json `
    -Uri "https://LOCATION-aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/LOCATION/ragCorpora/RAG_CORPUS_ID/ragDataSchemas:batchCreate" | Select-Object -Expand Content
```

You should receive a successful status code (2xx).

### List metadata schemas example

This code sample demonstrates how to list metadata schemas for a RAG corpus.

### REST

Before using any of the request data, make the following replacements:

- ` PROJECT_ID ` : Your [project ID](https://docs.cloud.google.com/resource-manager/docs/creating-managing-projects#identifiers) . .
- ` LOCATION ` : The region to process the request.
- ` RAG_CORPUS_ID ` : The ID of the `RagCorpus` resource.

HTTP method and URL:

```
GET https://LOCATION-aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/LOCATION/ragCorpora/RAG_CORPUS_ID/ragDataSchemas
```

To send your request, choose one of these options:

#### curl

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) , or by using [Cloud Shell](https://docs.cloud.google.com/shell/docs) , which automatically logs you into the `gcloud` CLI . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Execute the following command:

```
curl -X GET \
     -H "Authorization: Bearer $(gcloud auth print-access-token)" \
     "https://LOCATION-aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/LOCATION/ragCorpora/RAG_CORPUS_ID/ragDataSchemas"
```

#### PowerShell

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Execute the following command:

```
$cred = gcloud auth print-access-token
$headers = @{ "Authorization" = "Bearer $cred" }

Invoke-WebRequest `
    -Method GET `
    -Headers $headers `
    -Uri "https://LOCATION-aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/LOCATION/ragCorpora/RAG_CORPUS_ID/ragDataSchemas" | Select-Object -Expand Content
```

A successful response returns a list of `RagDataSchema` resources.

### Batch delete metadata schemas example

This code sample demonstrates how to batch delete metadata schemas.

### REST

Before using any of the request data, make the following replacements:

- ` PROJECT_ID ` : Your [project ID](https://docs.cloud.google.com/resource-manager/docs/creating-managing-projects#identifiers) . .
- ` LOCATION ` : The region to process the request.
- ` RAG_CORPUS_ID ` : The ID of the `RagCorpus` resource.
- ` SCHEMA_ID_1 ` : The ID of the first metadata schema to delete.
- ` SCHEMA_ID_2 ` : The ID of the second metadata schema to delete.

HTTP method and URL:

```
POST https://LOCATION-aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/LOCATION/ragCorpora/RAG_CORPUS_ID/ragDataSchemas:batchDelete
```

Request JSON body:

```
{
  "names": [
    "projects/PROJECT_ID/locations/LOCATION/ragCorpora/RAG_CORPUS_ID/ragDataSchemas/SCHEMA_ID_1",
    "projects/PROJECT_ID/locations/LOCATION/ragCorpora/RAG_CORPUS_ID/ragDataSchemas/SCHEMA_ID_2"
  ]
}
```

To send your request, choose one of these options:

#### curl

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) , or by using [Cloud Shell](https://docs.cloud.google.com/shell/docs) , which automatically logs you into the `gcloud` CLI . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Save the request body in a file named `request.json` , and execute the following command:

```
curl -X POST \
     -H "Authorization: Bearer $(gcloud auth print-access-token)" \
     -H "Content-Type: application/json; charset=utf-8" \
     -d @request.json \
     "https://LOCATION-aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/LOCATION/ragCorpora/RAG_CORPUS_ID/ragDataSchemas:batchDelete"
```

#### PowerShell

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Save the request body in a file named `request.json` , and execute the following command:

```
$cred = gcloud auth print-access-token
$headers = @{ "Authorization" = "Bearer $cred" }

Invoke-WebRequest `
    -Method POST `
    -Headers $headers `
    -ContentType: "application/json; charset=utf-8" `
    -InFile request.json `
    -Uri "https://LOCATION-aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/LOCATION/ragCorpora/RAG_CORPUS_ID/ragDataSchemas:batchDelete" | Select-Object -Expand Content
```

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

- ` PROJECT_ID ` : Your [project ID](https://docs.cloud.google.com/resource-manager/docs/creating-managing-projects#identifiers) . .
- ` LOCATION ` : The region to process the request.
- ` RAG_CORPUS_ID ` : The ID of the `RagCorpus` resource.
- ` GCS_URIS ` : A list of Cloud Storage locations. Example: `gs://my-bucket1, gs://my-bucket2` .
- ` CHUNK_SIZE ` : Optional: Number of tokens each chunk should have.
- ` CHUNK_OVERLAP ` : Optional: Number of tokens overlap between chunks.

HTTP method and URL:

```
POST https://LOCATION-aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/LOCATION/ragCorpora/RAG_CORPUS_ID/ragFiles:import
```

Request JSON body:

```
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
```

To send your request, choose one of these options:

#### curl

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) , or by using [Cloud Shell](https://docs.cloud.google.com/shell/docs) , which automatically logs you into the `gcloud` CLI . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Save the request body in a file named `request.json` , and execute the following command:

```
curl -X POST \
     -H "Authorization: Bearer $(gcloud auth print-access-token)" \
     -H "Content-Type: application/json; charset=utf-8" \
     -d @request.json \
     "https://LOCATION-aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/LOCATION/ragCorpora/RAG_CORPUS_ID/ragFiles:import"
```

#### PowerShell

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Save the request body in a file named `request.json` , and execute the following command:

```
$cred = gcloud auth print-access-token
$headers = @{ "Authorization" = "Bearer $cred" }

Invoke-WebRequest `
    -Method POST `
    -Headers $headers `
    -ContentType: "application/json; charset=utf-8" `
    -InFile request.json `
    -Uri "https://LOCATION-aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/LOCATION/ragCorpora/RAG_CORPUS_ID/ragFiles:import" | Select-Object -Expand Content
```

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
```

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
```

### List RAG files example

This code sample demonstrates how to list RAG files.

### REST

Before using any of the request data, make the following replacements:

- ` PROJECT_ID ` : Your [project ID](https://docs.cloud.google.com/resource-manager/docs/creating-managing-projects#identifiers) . .
- ` LOCATION ` : The region to process the request.
- ` RAG_CORPUS_ID ` : The ID of the `RagCorpus` resource.
- ` PAGE_SIZE ` : The standard list page size. You may adjust the number of `RagFiles` to return per page by updating the `page_size` parameter.
- ` PAGE_TOKEN ` : The standard list page token. Obtained typically using `ListRagFilesResponse.next_page_token` of the previous `VertexRagDataService.ListRagFiles` call.

HTTP method and URL:

```
GET https://LOCATION-aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/LOCATION/ragCorpora/RAG_CORPUS_ID/ragFiles?page_size=PAGE_SIZE&page_token=PAGE_TOKEN
```

To send your request, choose one of these options:

#### curl

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) , or by using [Cloud Shell](https://docs.cloud.google.com/shell/docs) , which automatically logs you into the `gcloud` CLI . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Execute the following command:

```
curl -X GET \
     -H "Authorization: Bearer $(gcloud auth print-access-token)" \
     "https://LOCATION-aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/LOCATION/ragCorpora/RAG_CORPUS_ID/ragFiles?page_size=PAGE_SIZE&page_token=PAGE_TOKEN"
```

#### PowerShell

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Execute the following command:

```
$cred = gcloud auth print-access-token
$headers = @{ "Authorization" = "Bearer $cred" }

Invoke-WebRequest `
    -Method GET `
    -Headers $headers `
    -Uri "https://LOCATION-aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/LOCATION/ragCorpora/RAG_CORPUS_ID/ragFiles?page_size=PAGE_SIZE&page_token=PAGE_TOKEN" | Select-Object -Expand Content
```

You should receive a successful status code (2xx) along with a list of `RagFiles` under the given `RAG_CORPUS_ID` .

### Get a RAG file example

This code sample demonstrates how to get a RAG file.

### REST

Before using any of the request data, make the following replacements:

- ` PROJECT_ID ` : Your [project ID](https://docs.cloud.google.com/resource-manager/docs/creating-managing-projects#identifiers) . .
- ` LOCATION ` : The region to process the request.
- ` RAG_CORPUS_ID ` : The ID of the `RagCorpus` resource.
- ` RAG_FILE_ID ` : The ID of the `RagFile` resource.

HTTP method and URL:

```
GET https://LOCATION-aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/LOCATION/ragCorpora/RAG_CORPUS_ID/ragFiles/RAG_FILE_ID
```

To send your request, choose one of these options:

#### curl

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) , or by using [Cloud Shell](https://docs.cloud.google.com/shell/docs) , which automatically logs you into the `gcloud` CLI . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Execute the following command:

```
curl -X GET \
     -H "Authorization: Bearer $(gcloud auth print-access-token)" \
     "https://LOCATION-aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/LOCATION/ragCorpora/RAG_CORPUS_ID/ragFiles/RAG_FILE_ID"
```

#### PowerShell

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Execute the following command:

```
$cred = gcloud auth print-access-token
$headers = @{ "Authorization" = "Bearer $cred" }

Invoke-WebRequest `
    -Method GET `
    -Headers $headers `
    -Uri "https://LOCATION-aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/LOCATION/ragCorpora/RAG_CORPUS_ID/ragFiles/RAG_FILE_ID" | Select-Object -Expand Content
```

A successful response returns the `RagFile` resource.

### Delete a RAG file example

This code sample demonstrates how to delete a RAG file.

### REST

Before using any of the request data, make the following replacements:

- ` PROJECT_ID ` : Your [project ID](https://docs.cloud.google.com/resource-manager/docs/creating-managing-projects#identifiers) . .
- ` LOCATION ` : The region to process the request.
- ` RAG_CORPUS_ID ` : The ID of the `RagCorpus` resource.
- ` RAG_FILE_ID ` : The ID of the `RagFile` resource. Format: `projects/{project}/locations/{location}/ragCorpora/{rag_corpus}/ragFiles/{rag_file_id}` .

HTTP method and URL:

```
DELETE https://LOCATION-aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/LOCATION/ragCorpora/RAG_CORPUS_ID/ragFiles/RAG_FILE_ID
```

To send your request, choose one of these options:

#### curl

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) , or by using [Cloud Shell](https://docs.cloud.google.com/shell/docs) , which automatically logs you into the `gcloud` CLI . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Execute the following command:

```
curl -X DELETE \
     -H "Authorization: Bearer $(gcloud auth print-access-token)" \
     "https://LOCATION-aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/LOCATION/ragCorpora/RAG_CORPUS_ID/ragFiles/RAG_FILE_ID"
```

#### PowerShell

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Execute the following command:

```
$cred = gcloud auth print-access-token
$headers = @{ "Authorization" = "Bearer $cred" }

Invoke-WebRequest `
    -Method DELETE `
    -Headers $headers `
    -Uri "https://LOCATION-aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/LOCATION/ragCorpora/RAG_CORPUS_ID/ragFiles/RAG_FILE_ID" | Select-Object -Expand Content
```

A successful response returns the `DeleteOperationMetadata` resource.

### Batch create metadata example

This code sample demonstrates how to batch create metadata for a RAG file.

### REST

Before using any of the request data, make the following replacements:

- ` PROJECT_ID ` : Your [project ID](https://docs.cloud.google.com/resource-manager/docs/creating-managing-projects#identifiers) . .
- ` LOCATION ` : The region to process the request.
- ` RAG_CORPUS_ID ` : The ID of the `RagCorpus` resource.
- ` RAG_FILE_ID ` : The ID of the `RagFile` resource.
- ` METADATA_KEY_1 ` : The key for the first metadata entry.
- ` VALUE_TYPE_1 ` : The value type field for the first metadata entry (e.g., `int_value` ).
- ` METADATA_VALUE_1 ` : The value for the first metadata entry.
- ` METADATA_KEY_2 ` : The key for the second metadata entry.
- ` VALUE_TYPE_2 ` : The value type field for the second metadata entry (e.g., `str_value` ).
- ` METADATA_VALUE_2 ` : The value for the second metadata entry.

HTTP method and URL:

```
POST https://LOCATION-aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/LOCATION/ragCorpora/RAG_CORPUS_ID/ragFiles/RAG_FILE_ID/ragMetadata:batchCreate
```

Request JSON body:

```
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
```

To send your request, choose one of these options:

#### curl

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) , or by using [Cloud Shell](https://docs.cloud.google.com/shell/docs) , which automatically logs you into the `gcloud` CLI . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Save the request body in a file named `request.json` , and execute the following command:

```
curl -X POST \
     -H "Authorization: Bearer $(gcloud auth print-access-token)" \
     -H "Content-Type: application/json; charset=utf-8" \
     -d @request.json \
     "https://LOCATION-aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/LOCATION/ragCorpora/RAG_CORPUS_ID/ragFiles/RAG_FILE_ID/ragMetadata:batchCreate"
```

#### PowerShell

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Save the request body in a file named `request.json` , and execute the following command:

```
$cred = gcloud auth print-access-token
$headers = @{ "Authorization" = "Bearer $cred" }

Invoke-WebRequest `
    -Method POST `
    -Headers $headers `
    -ContentType: "application/json; charset=utf-8" `
    -InFile request.json `
    -Uri "https://LOCATION-aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/LOCATION/ragCorpora/RAG_CORPUS_ID/ragFiles/RAG_FILE_ID/ragMetadata:batchCreate" | Select-Object -Expand Content
```

You should receive a successful status code (2xx).

### List metadata example

This code sample demonstrates how to list metadata for a RAG file.

### REST

Before using any of the request data, make the following replacements:

- ` PROJECT_ID ` : Your [project ID](https://docs.cloud.google.com/resource-manager/docs/creating-managing-projects#identifiers) . .
- ` LOCATION ` : The region to process the request.
- ` RAG_CORPUS_ID ` : The ID of the `RagCorpus` resource.
- ` RAG_FILE_ID ` : The ID of the `RagFile` resource.

HTTP method and URL:

```
GET https://LOCATION-aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/LOCATION/ragCorpora/RAG_CORPUS_ID/ragFiles/RAG_FILE_ID/ragMetadata
```

To send your request, choose one of these options:

#### curl

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) , or by using [Cloud Shell](https://docs.cloud.google.com/shell/docs) , which automatically logs you into the `gcloud` CLI . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Execute the following command:

```
curl -X GET \
     -H "Authorization: Bearer $(gcloud auth print-access-token)" \
     "https://LOCATION-aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/LOCATION/ragCorpora/RAG_CORPUS_ID/ragFiles/RAG_FILE_ID/ragMetadata"
```

#### PowerShell

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Execute the following command:

```
$cred = gcloud auth print-access-token
$headers = @{ "Authorization" = "Bearer $cred" }

Invoke-WebRequest `
    -Method GET `
    -Headers $headers `
    -Uri "https://LOCATION-aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/LOCATION/ragCorpora/RAG_CORPUS_ID/ragFiles/RAG_FILE_ID/ragMetadata" | Select-Object -Expand Content
```

A successful response returns a list of `RagMetadata` resources.

### Update metadata example

This code sample demonstrates how to update metadata for a RAG file.

### REST

Before using any of the request data, make the following replacements:

- ` PROJECT_ID ` : Your [project ID](https://docs.cloud.google.com/resource-manager/docs/creating-managing-projects#identifiers) . .
- ` LOCATION ` : The region to process the request.
- ` RAG_CORPUS_ID ` : The ID of the `RagCorpus` resource.
- ` RAG_FILE_ID ` : The ID of the `RagFile` resource.
- ` METADATA_ID ` : The ID of the metadata entry to update.
- ` METADATA_KEY ` : The key for the metadata entry.
- ` VALUE_TYPE ` : The value type field (e.g., `int_value` ).
- ` METADATA_VALUE ` : The new value for the metadata entry.

HTTP method and URL:

```
PATCH https://LOCATION-aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/LOCATION/ragCorpora/RAG_CORPUS_ID/ragFiles/RAG_FILE_ID/ragMetadata/METADATA_ID
```

Request JSON body:

```
{
  "user_specified_metadata": {
    "key": "METADATA_KEY",
    "value": { "VALUE_TYPE": METADATA_VALUE }
  }
}
```

To send your request, choose one of these options:

#### curl

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) , or by using [Cloud Shell](https://docs.cloud.google.com/shell/docs) , which automatically logs you into the `gcloud` CLI . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Save the request body in a file named `request.json` , and execute the following command:

```
curl -X PATCH \
     -H "Authorization: Bearer $(gcloud auth print-access-token)" \
     -H "Content-Type: application/json; charset=utf-8" \
     -d @request.json \
     "https://LOCATION-aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/LOCATION/ragCorpora/RAG_CORPUS_ID/ragFiles/RAG_FILE_ID/ragMetadata/METADATA_ID"
```

#### PowerShell

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Save the request body in a file named `request.json` , and execute the following command:

```
$cred = gcloud auth print-access-token
$headers = @{ "Authorization" = "Bearer $cred" }

Invoke-WebRequest `
    -Method PATCH `
    -Headers $headers `
    -ContentType: "application/json; charset=utf-8" `
    -InFile request.json `
    -Uri "https://LOCATION-aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/LOCATION/ragCorpora/RAG_CORPUS_ID/ragFiles/RAG_FILE_ID/ragMetadata/METADATA_ID" | Select-Object -Expand Content
```

You should receive a successful status code (2xx).

### Batch delete metadata example

This code sample demonstrates how to batch delete metadata entries for a RAG file.

### REST

Before using any of the request data, make the following replacements:

- ` PROJECT_ID ` : Your [project ID](https://docs.cloud.google.com/resource-manager/docs/creating-managing-projects#identifiers) . .
- ` LOCATION ` : The region to process the request.
- ` RAG_CORPUS_ID ` : The ID of the `RagCorpus` resource.
- ` RAG_FILE_ID ` : The ID of the `RagFile` resource.
- ` METADATA_ID_1 ` : The ID of the first metadata entry to delete.
- ` METADATA_ID_2 ` : The ID of the second metadata entry to delete.

HTTP method and URL:

```
POST https://LOCATION-aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/LOCATION/ragCorpora/RAG_CORPUS_ID/ragFiles/RAG_FILE_ID/ragMetadata:batchDelete
```

Request JSON body:

```
{
  "names": [
    "projects/PROJECT_ID/locations/LOCATION/ragCorpora/RAG_CORPUS_ID/ragFiles/RAG_FILE_ID/ragMetadata/METADATA_ID_1",
    "projects/PROJECT_ID/locations/LOCATION/ragCorpora/RAG_CORPUS_ID/ragFiles/RAG_FILE_ID/ragMetadata/METADATA_ID_2"
  ]
}
```

To send your request, choose one of these options:

#### curl

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) , or by using [Cloud Shell](https://docs.cloud.google.com/shell/docs) , which automatically logs you into the `gcloud` CLI . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Save the request body in a file named `request.json` , and execute the following command:

```
curl -X POST \
     -H "Authorization: Bearer $(gcloud auth print-access-token)" \
     -H "Content-Type: application/json; charset=utf-8" \
     -d @request.json \
     "https://LOCATION-aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/LOCATION/ragCorpora/RAG_CORPUS_ID/ragFiles/RAG_FILE_ID/ragMetadata:batchDelete"
```

#### PowerShell

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Save the request body in a file named `request.json` , and execute the following command:

```
$cred = gcloud auth print-access-token
$headers = @{ "Authorization" = "Bearer $cred" }

Invoke-WebRequest `
    -Method POST `
    -Headers $headers `
    -ContentType: "application/json; charset=utf-8" `
    -InFile request.json `
    -Uri "https://LOCATION-aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/LOCATION/ragCorpora/RAG_CORPUS_ID/ragFiles/RAG_FILE_ID/ragMetadata:batchDelete" | Select-Object -Expand Content
```

You should receive a successful status code (2xx).

### Retrieval query example

When a user asks a question or provides a prompt, the retrieval component in RAG searches through its knowledge base to find information that is relevant to the query.

### REST

Before using any of the request data, make the following replacements:

- ` LOCATION ` : The region to process the request.
- ` PROJECT_ID ` : Your [project ID](https://docs.cloud.google.com/resource-manager/docs/creating-managing-projects#identifiers) . .
- ` RAG_CORPUS_RESOURCE ` : The name of the `RagCorpus` resource. Format: `projects/{project}/locations/{location}/ragCorpora/{rag_corpus}` .
- ` TOP_K ` : The number of top contexts to retrieve.
- ` VECTOR_DISTANCE_THRESHOLD ` : Only contexts with a vector distance smaller than the threshold are returned.
- ` METADATA_FILTER ` : Optional: The metadata filter to apply during retrieval.
- ` TEXT ` : The query text to get relevant contexts.

HTTP method and URL:

```
POST https://LOCATION-aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/LOCATION:retrieveContexts
```

Request JSON body:

```
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
```

To send your request, choose one of these options:

#### curl

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) , or by using [Cloud Shell](https://docs.cloud.google.com/shell/docs) , which automatically logs you into the `gcloud` CLI . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Save the request body in a file named `request.json` , and execute the following command:

```
curl -X POST \
     -H "Authorization: Bearer $(gcloud auth print-access-token)" \
     -H "Content-Type: application/json; charset=utf-8" \
     -d @request.json \
     "https://LOCATION-aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/LOCATION:retrieveContexts"
```

#### PowerShell

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Save the request body in a file named `request.json` , and execute the following command:

```
$cred = gcloud auth print-access-token
$headers = @{ "Authorization" = "Bearer $cred" }

Invoke-WebRequest `
    -Method POST `
    -Headers $headers `
    -ContentType: "application/json; charset=utf-8" `
    -InFile request.json `
    -Uri "https://LOCATION-aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/LOCATION:retrieveContexts" | Select-Object -Expand Content
```

You should receive a successful status code (2xx) and a list of related `RagFiles` .

### Generation example

The LLM generates a grounded response using the retrieved contexts.

### REST

Before using any of the request data, make the following replacements:

- ` PROJECT_ID ` : Your [project ID](https://docs.cloud.google.com/resource-manager/docs/creating-managing-projects#identifiers) . .
- ` LOCATION ` : The region to process the request.
- ` MODEL_ID ` : LLM model for content generation. Example: `gemini-3.5-flash`
- ` GENERATION_METHOD ` : LLM method for content generation. Options: `generateContent` , `streamGenerateContent`
- ` INPUT_PROMPT ` : The text sent to the LLM for content generation. Try to use a prompt relevant to the uploaded rag Files.
- ` RAG_CORPUS_RESOURCE ` : The name of the `RagCorpus` resource. Format: `projects/{project}/locations/{location}/ragCorpora/{rag_corpus}` .
- ` TOP_K ` : Optional: The number of top contexts to retrieve.
- ` VECTOR_DISTANCE_THRESHOLD ` : Optional: Contexts with a vector distance smaller than the threshold are returned.
- ` METADATA_FILTER ` : Optional: The metadata filter to apply during retrieval.

HTTP method and URL:

```
POST https://LOCATION-aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/LOCATION/publishers/google/models/MODEL_ID:GENERATION_METHOD
```

Request JSON body:

```
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
```

To send your request, choose one of these options:

#### curl

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) , or by using [Cloud Shell](https://docs.cloud.google.com/shell/docs) , which automatically logs you into the `gcloud` CLI . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Save the request body in a file named `request.json` , and execute the following command:

```
curl -X POST \
     -H "Authorization: Bearer $(gcloud auth print-access-token)" \
     -H "Content-Type: application/json; charset=utf-8" \
     -d @request.json \
     "https://LOCATION-aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/LOCATION/publishers/google/models/MODEL_ID:GENERATION_METHOD"
```

#### PowerShell

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Save the request body in a file named `request.json` , and execute the following command:

```
$cred = gcloud auth print-access-token
$headers = @{ "Authorization" = "Bearer $cred" }

Invoke-WebRequest `
    -Method POST `
    -Headers $headers `
    -ContentType: "application/json; charset=utf-8" `
    -InFile request.json `
    -Uri "https://LOCATION-aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/LOCATION/publishers/google/models/MODEL_ID:GENERATION_METHOD" | Select-Object -Expand Content
```

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

```
PROJECT_ID: Your project ID.
LOCATION: The region to process the request.
```

```
curl -X GET \
-H "Content-Type: application/json" \
-H "Authorization: Bearer $(gcloud auth print-access-token)" \
https://LOCATION-aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/LOCATION/ragEngineConfig
```

### Python

```
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
```

### Switch to Serverless mode

The following code samples demonstrate how to switch your `RagEngineConfig` to the Serverless mode:

### Console

1.  In the Google Cloud console, go to the **RAG Engine** page.
2.  Select the region in which your RAG Engine is running.
3.  Click the **Switch to Serverless** button. This button might not be visible if you are already on Serverless mode. You can verify your current mode from the mode label at the top right section of the page.

### REST

```
PROJECT_ID: Your project ID.
LOCATION: The region to process the request.
```

```
curl -X PATCH \
-H "Content-Type: application/json" \
-H "Authorization: Bearer $(gcloud auth print-access-token)" \
https://LOCATION-aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/LOCATION/ragEngineConfig -d "{'ragManagedDbConfig': {'serverless': {}}}"
```

### Python

```
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
```

### Switch to Spanner mode

The following code samples demonstrate how to switch your `RagEngineConfig` to the Spanner mode. If you previously have used Spanner mode, and have chosen a tier, you no longer need to provide it explicitly while switching. If not, refer to the lower code examples on how to switch to Spanner mode while providing a tier.

### Console

1.  In the Google Cloud console, go to the **RAG Engine** page.
2.  Select the region in which your RAG Engine is running.
3.  Click the **Switch to Spanner** button. This button might not be visible if you are already on Spanner mode. You can verify your current mode from the mode label at the top right section of the page.

### REST

```
PROJECT_ID: Your project ID.
LOCATION: The region to process the request.
```

```
curl -X PATCH \
-H "Content-Type: application/json" \
-H "Authorization: Bearer $(gcloud auth print-access-token)" \
https://LOCATION-aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/LOCATION/ragEngineConfig -d "{'ragManagedDbConfig': {'spanner': {}}}"
```

### Python

```
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
```

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

```
PROJECT_ID: Your project ID.
LOCATION: The region to process the request.
```

```
curl -X PATCH \
-H "Content-Type: application/json" \
-H "Authorization: Bearer $(gcloud auth print-access-token)" \
https://LOCATION-aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/LOCATION/ragEngineConfig -d "{'ragManagedDbConfig': {'spanner': {'scaled': {}}}}"
```

### Python

```
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
```

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

```
PROJECT_ID: Your project ID.
LOCATION: The region to process the request.
```

```
curl -X PATCH \
-H "Content-Type: application/json" \
-H "Authorization: Bearer $(gcloud auth print-access-token)" \
https://LOCATION-aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/LOCATION/ragEngineConfig -d "{'ragManagedDbConfig': {'spanner': {'basic': {}}}}"
```

### Python

```
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
```

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

```
PROJECT_ID: Your project ID.
LOCATION: The region to process the request.
```

```
curl -X PATCH \
-H "Content-Type: application/json" \
-H "Authorization: Bearer $(gcloud auth print-access-token)" \
https://LOCATION-aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/LOCATION/ragEngineConfig -d "{'ragManagedDbConfig': {'spanner': {'unprovisioned': {}}}}"
```

### Python

```
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
```

## What's next

- To learn more about supported generation models, see [Generative AI models that support RAG](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/rag-engine/supported-rag-models) .
- To learn more about supported embedding models, see [Embedding models](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/rag-engine/use-embedding-models#supported-embedding-models) .
- To learn more about open models, see [Open models](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/rag-engine/use-embedding-models#use-oss-embedding-models) .
- To learn more about RAG Engine, see [RAG Engine overview](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/rag-engine/rag-overview) .
