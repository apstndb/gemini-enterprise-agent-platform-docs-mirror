---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/models/rag-api-v1
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/models/rag-api-v1
title: RAG Engine API
description: Reference for the RAG Engine on Gemini Enterprise Agent Platform API, which includes parameters and examples for corpus management, file management, and retrieval.
data_source: docs.cloud.google.com
---

The RAG Engine is a component of the Gemini Enterprise Agent Platform platform, which facilitates Retrieval-Augmented Generation (RAG). RAG Engine enables Large Language Models (LLMs) to access and incorporate data from external knowledge sources, such as documents and databases. By using RAG, LLMs can generate more accurate and informative LLM responses.

## Parameters list

This section lists the following:

| Parameters                                                                                                                                                      | Examples                                                                                                                                                        |
| --------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| See [Corpus management parameters](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/models/rag-api-v1#corpus-management-params-api) .   | See [Corpus management examples](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/models/rag-api-v1#corpus-management-examples-api) .   |
| See [File management parameters](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/models/rag-api-v1#file-management-params-api) .       | See [File management examples](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/models/rag-api-v1#file-management-examples-api) .       |
| See [Project management parameters](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/models/rag-api-v1#project-management-params-api) . | See [Project management examples](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/models/rag-api-v1#project-management-examples-api) . |

### Corpus management parameters

For information about a RAG corpus, see [Corpus management](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/rag-engine/manage-your-rag-corpus#corpus-management) .

#### Create a RAG corpus

This table lists the parameters used to create a RAG corpus.

##### Body Request

Parameters

`display_name`

Required: `string`

The display name of the RAG corpus.

`description`

Optional: `string`

The description of the RAG corpus.

`encryption_spec`

Optional: Immutable: `string`

The CMEK key name is used to encrypt at-rest data that's related to the RAG corpus. The key name is only applicable to the `RagManaged` option for the vector database. When the corpus is created, this field can be set and can't be updated or deleted.

Format: `projects/{project}/locations/{location}/keyRings/{key_ring}/cryptoKeys/{key_name}`

`vector_db_config`

Optional: Immutable: `vectorDbConfig`

The configuration for the Vector DBs.

`vertex_ai_search_config.serving_config`

Optional: `string`

The configuration for the Agent Search.

Format: `projects/{project}/locations/{location}/collections/{collection}/engines/{engine}/servingConfigs/{serving_config}` or `projects/{project}/locations/{location}/collections/{collection}/dataStores/{data_store}/servingConfigs/{serving_config}`

##### `vectorDbConfig`

Parameters

`rag_managed_db`

`oneof` `vector_db` : `vectorDbConfig.RagManagedDb`

If no vector database is specified, `rag_managed_db` is the default vector database.

`pinecone`

`oneof` `vector_db` : `vectorDbConfig.Pinecone`

Specifies your Pinecone instance.

`pinecone.index_name`

`string`

This is the name used to create the Pinecone index that's used with the RAG corpus.

This value can't be changed after it's set. You can leave it empty in the `CreateRagCorpus` API call, and set it with a non-empty value in a follow up `UpdateRagCorpus` API call.

`vertex_vector_search`

`oneof` `vector_db` : `vectorDbConfig.VertexVectorSearch`

Specifies your Vector Search on Gemini Enterprise Agent Platform instance.

`vertex_vector_search.index`

`string`

This is the resource name of the Vector Search index that's used with the RAG corpus.

Format: `projects/{project}/locations/{location}/indexEndpoints/{index_endpoint}`

This value can't be changed after it's set. You can leave it empty in the `CreateRagCorpus` API call, and set it with a non-empty value in a follow up `UpdateRagCorpus` API call.

`vertex_vector_search.index_endpoint`

`string`

This is the resource name of the Vector Search index endpoint that's used with the RAG corpus.

Format: `projects/{project}/locations/{location}/indexes/{index}`

This value can't be changed after it's set. You can leave it empty in the `CreateRagCorpus` API call, and set it with a non-empty value in a follow up `UpdateRagCorpus` API call.

`api_auth.api_key_config.api_key_secret_version`

`string`

This the full resource name of the secret that is stored in Secret Manager, which contains your Pinecone API key.

Format: `projects/{PROJECT_NUMBER}/secrets/{SECRET_ID}/versions/{VERSION_ID}`

You can leave it empty in the `CreateRagCorpus` API call, and set it with a non-empty value in a follow up `UpdateRagCorpus` API call.

`rag_embedding_model_config.vertex_prediction_endpoint.endpoint`

Optional: Immutable: `string`

The embedding model to use for the RAG corpus. This value can't be changed after it's set. If you leave it empty, we use [text-embedding-005](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/models/text-embeddings-api) as the embedding model.

#### Update a RAG corpus

This table lists the parameters used to update a RAG corpus.

##### Body Request

Parameters

`display_name`

Optional: `string`

The display name of the RAG corpus.

`description`

Optional: `string`

The description of the RAG corpus.

`rag_vector_db.pinecone.index_name`

`string`

This is the name used to create the Pinecone index that's used with the RAG corpus.

If your `RagCorpus` was created with a `Pinecone` configuration, and this field has never been set before, then you can update the Pinecone instance's index name.

`rag_vector_db.vertex_vector_search.index`

`string`

This is the resource name of the Vector Search index that's used with the RAG corpus.

Format: `projects/{project}/locations/{location}/indexEndpoints/{index_endpoint}`

If your `RagCorpus` was created with a Vector Search configuration, and this field has never been set before, then you can update it.

`rag_vector_db.vertex_vector_search.index_endpoint`

`string`

This is the resource name of the Vector Search index endpoint that's used with the RAG corpus.

Format: `projects/{project}/locations/{location}/indexes/{index}`

If your `RagCorpus` was created with a Vector Search configuration, and this field has never been set before, then you can update it.

`rag_vector_db.api_auth.api_key_config.api_key_secret_version`

`string`

The full resource name of the secret that is stored in Secret Manager, which contains your Pinecone API key.

Format: `projects/{PROJECT_NUMBER}/secrets/{SECRET_ID}/versions/{VERSION_ID}`

#### List RAG corpora

This table lists the parameters used to list RAG corpora.

Parameters

`page_size`

Optional: `int`

The standard list page size.

`page_token`

Optional: `string`

The standard list page token. Typically obtained from `[ListRagCorporaResponse.next_page_token][]` of the previous `[VertexRagDataService.ListRagCorpora][]` call.

#### Get a RAG corpus

This table lists parameters used to get a RAG corpus.

Parameters

`name`

`string`

The name of the `RagCorpus` resource. Format: `projects/{project}/locations/{location}/ragCorpora/{rag_corpus_id}`

#### Delete a RAG corpus

This table lists parameters used to delete a RAG corpus.

Parameters

`name`

`string`

The name of the `RagCorpus` resource. Format: `projects/{project}/locations/{location}/ragCorpora/{rag_corpus_id}`

### File management parameters

For information about a RAG file, see [File management](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/rag-engine/manage-your-rag-corpus#file-management) .

#### Upload a RAG file

This table lists parameters used to upload a RAG file.

##### Body Request

Parameters

`parent`

`string`

The name of the `RagCorpus` resource. Format: `projects/{project}/locations/{location}/ragCorpora/{rag_corpus_id}`

`rag_file`

Required: `RagFile`

The file to upload.

`upload_rag_file_config`

Required: `UploadRagFileConfig`

The configuration for the `RagFile` to be uploaded into the `RagCorpus` .

`RagFile`

`display_name`

Required: `string`

The display name of the RAG file.

`description`

Optional: `string`

The description of the RAG file.

`UploadRagFileConfig`

`rag_file_transformation_config.rag_file_chunking_config.fixed_length_chunking.chunk_size`

`int32`

Number of tokens each chunk has.

`rag_file_transformation_config.rag_file_chunking_config.fixed_length_chunking.chunk_overlap`

`int32`

The overlap between chunks.

#### Import RAG files

This table lists parameters used to import a RAG file.

Parameters

`parent`

Required: `string`

The name of the `RagCorpus` resource.

Format: `projects/{project}/locations/{location}/ragCorpora/{rag_corpus_id}`

`gcs_source`

`oneof` `import_source` : `GcsSource`

Cloud Storage location.

Supports importing individual files as well as entire Cloud Storage directories.

`gcs_source.uris`

`list` of `string`

Cloud Storage URI that contains the upload file.

`google_drive_source`

`oneof` `import_source` : `GoogleDriveSource`

Google Drive location.

Supports importing individual files as well as Google Drive folders.

`slack_source`

`oneof` `import_source` : `SlackSource`

The slack channel where the file is uploaded.

`jira_source`

`oneof` `import_source` : `JiraSource`

The Jira query where the file is uploaded.

`share_point_sources`

`oneof` `import_source` : `SharePointSources`

The SharePoint sources where the file is uploaded.

`rag_file_transformation_config.rag_file_chunking_config.fixed_length_chunking.chunk_size`

`int32`

Number of tokens each chunk has.

`rag_file_transformation_config.rag_file_chunking_config.fixed_length_chunking.chunk_overlap`

`int32`

The overlap between chunks.

`rag_file_parsing_config`

Optional: `RagFileParsingConfig`

Specifies the parsing configuration for `RagFiles` .

If this field isn't set, RAG uses the default parser.

`max_embedding_requests_per_min`

Optional: `int32`

The maximum number of queries per minute that this job is allowed to make to the embedding model specified on the corpus. This value is specific to this job and not shared across other import jobs. Consult the Quotas page on the project to set an appropriate value.

If unspecified, a default value of 1,000 QPM is used.

`GoogleDriveSource`

`resource_ids.resource_id`

Required: `string`

The ID of the Google Drive resource.

`resource_ids.resource_type`

Required: `string`

The type of the Google Drive resource.

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

`JiraSource`

`jira_queries.projects`

Repeated: `string`

A list of Jira projects to import in their entirety.

`jira_queries.custom_queries`

Repeated: `string`

A list of custom Jira queries to import. For information about JQL (Jira Query Language), see  
[Jira Support](https://support.atlassian.com/jira-service-management-cloud/docs/use-advanced-search-with-jira-query-language-jql/)

`jira_queries.email`

Required: `string`

The Jira email address.

`jira_queries.server_uri`

Required: `string`

The Jira server URI.

`jira_queries.api_key_config.api_key_secret_version`

Required: `string`

The full resource name of the secret that is stored in Secret Manager, which contains Jira API key that has access to the slack channel IDs.  
See: https://support.atlassian.com/atlassian-account/docs/manage-api-tokens-for-your-atlassian-account/

Format: `projects/{PROJECT_NUMBER}/secrets/{SECRET_ID}/versions/{VERSION_ID}`

`SharePointSources`

`share_point_sources.sharepoint_folder_path`

`oneof` in `folder_source` : `string`

The path of the SharePoint folder to download from.

`share_point_sources.sharepoint_folder_id`

`oneof` in `folder_source` : `string`

The ID of the SharePoint folder to download from.

`share_point_sources.drive_name`

`oneof` in `drive_source` : `string`

The name of the drive to download from.

`share_point_sources.drive_id`

`oneof` in `drive_source` : `string`

The ID of the drive to download from.

`share_point_sources.client_id`

`string`

The Application ID for the app registered in Microsoft Azure Portal.  
The application must also be configured with MS Graph permissions "Files.ReadAll", "Sites.ReadAll" and BrowserSiteLists.Read.All.

`share_point_sources.client_secret.api_key_secret_version`

Required: `string`

The full resource name of the secret that is stored in Secret Manager, which contains the application secret for the app registered in Azure.

Format: `projects/{PROJECT_NUMBER}/secrets/{SECRET_ID}/versions/{VERSION_ID}`

`share_point_sources.tenant_id`

`string`

Unique identifier of the Azure Active Directory Instance.

`share_point_sources.sharepoint_site_name`

`string`

The name of the SharePoint site to download from. This can be the site name or the site id.

`RagFileParsingConfig`

`layout_parser`

`oneof` `parser` : `RagFileParsingConfig.LayoutParser`

The Layout Parser to use for `RagFile` s.

`layout_parser.processor_name`

`string`

The full resource name of a Document AI processor or processor version.

Format:  
`projects/{project_id}/locations/{location}/processors/{processor_id}`  
`projects/{project_id}/locations/{location}/processors/{processor_id}/processorVersions/{processor_version_id}`

`layout_parser.max_parsing_requests_per_min`

`string`

The maximum number of requests the job is allowed to make to the Document AI processor per minute.

Consult [Document AI quotas](https://docs.cloud.google.com/document-ai/quotas) and the Quota page for your project to set an appropriate value here. If unspecified, a default value of 120 QPM is used.

`llm_parser`

`oneof` `parser` : `RagFileParsingConfig.LlmParser`

The LLM parser to use for `RagFile` s.

`llm_parser.model_name`

`string`

The resource name of an LLM model.

Format:  
`{publisher}/models/{model}`

`llm_parser.max_parsing_requests_per_min`

`string`

The maximum number of requests the job is allowed to make to the LLM model per minute.

To set an appropriate value for your project, see the [model quota section](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/quotas#quota_system_by_model) and the Quota page for your project to set an appropriate value here. If unspecified, a default value of 5000 QPM is used.

#### Get a RAG file

This table lists parameters used to get a RAG file.

Parameters

`name`

`string`

The name of the `RagFile` resource. Format: `projects/{project}/locations/{location}/ragCorpora/{rag_file_id}`

#### Delete a RAG file

This table lists parameters used to delete a RAG file.

Parameters

`name`

`string`

The name of the `RagFile` resource. Format: `projects/{project}/locations/{location}/ragCorpora/{rag_file_id}`

### Retrieval and prediction parameters

This section lists the retrieval and prediction parameters.

#### Retrieval parameters

This table lists parameters for `retrieveContexts` API.

Parameters

`parent`

Required: `string`

The resource name of the Location to retrieve `RagContexts` .  
The users must have permission to make a call in the project.

Format: `projects/{project}/locations/{location}`

`vertex_rag_store`

`VertexRagStore`

The data source for RagStore.

`query`

Required: `RagQuery`

Single RAG retrieve query.

##### `VertexRagStore`

`VertexRagStore`

`rag_resources`

list: `RagResource`

The representation of the RAG source. It can be used to specify the corpus only or `RagFile` s. Only support one corpus or multiple files from one corpus.

`rag_resources.rag_corpus`

Optional: `string`

`RagCorpora` resource name.

Format: `projects/{project}/locations/{location}/ragCorpora/{rag_corpus}`

`rag_resources.rag_file_ids`

list: `string`

A list of `RagFile` resources.

Format: `projects/{project}/locations/{location}/ragCorpora/{rag_corpus}/ragFiles/{rag_file}`

`RagQuery`

`text`

`string`

The query in text format to get relevant contexts.

`rag_retrieval_config`

Optional: `RagRetrievalConfig`

The retrieval configuration for the query.

`RagRetrievalConfig`

`top_k`

Optional: `int32`

The number of contexts to retrieve.

`filter.vector_distance_threshold`

`oneof vector_db_threshold` : `double`

Only returns contexts with a vector distance smaller than the threshold.

`filter.vector_similarity_threshold`

`oneof vector_db_threshold` : `double`

Only returns contexts with vector similarity larger than the threshold.

`ranking.rank_service.model_name`

Optional: `string`

The model name of the rank service.

Example: `semantic-ranker-512@latest`

`ranking.llm_ranker.model_name`

Optional: `string`

The model name used for ranking.

Example: `gemini-2.5-flash`

#### Prediction parameters

This table lists prediction parameters.

`GenerateContentRequest`

`tools.retrieval.vertex_rag_store`

`VertexRagStore`

Set to use a data source powered by Agent Platform RAG store.

See [VertexRagStore](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/models/rag-api-v1#ragStore) for details.

### Project management parameters

This table lists project-level parameters.

##### `RagEngineConfig`

| **Parameters**                     | ****                                                                                 |
| ---------------------------------- | ------------------------------------------------------------------------------------ |
| `RagManagedDbConfig.scaled`        | This tier offers production-scale performance along with auto scaling functionality. |
| `RagManagedDbConfig.basic`         | This tier offers a cost-effective and low-compute tier.                              |
| `RagManagedDbConfig.unprovisioned` | This tier deletes the `RagManagedDb` and its underlying Spanner instance.            |

## Corpus management examples

This section provides examples of how to use the API to manage your RAG corpus.

### Create a RAG corpus example

These code samples demonstrate how to create a RAG corpus.

### REST

Before using any of the request data, make the following replacements:

  - **PROJECT\_ID** : Your project ID.
  - **LOCATION** : The region to process the request.
  - **CORPUS\_DISPLAY\_NAME** : The display name of the RAG corpus.
  - **CORPUS\_DESCRIPTION** : The description of the RAG corpus.

HTTP method and URL:

    POST https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/ragCorpora

Request JSON body:

    {
      "display_name" : "CORPUS_DISPLAY_NAME",
      "description": "CORPUS_DESCRIPTION",
    }

To send your request, choose one of these options:

### curl

> **Note:** The following command assumes that you have signed in to the Google Cloud CLI CLI with your user account by running gcloud CLI `init` or gcloud CLI `auth login` , or by using Cloud Shell, which automatically signs you into the gcloud CLI CLI . You can check the active account by running gcloud CLI `auth list` .

Save the request body in a file named request.json, and run the following command:

    curl -X POST \
        -H "Authorization: Bearer $(gcloud auth print-access-token)" \
        -H "Content-Type: application/json; charset=utf-8" \
        -d @request.json \
        "https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/ragCorpora"

### Powershell

> **Note:** The following command assumes that you have signed in to the gcloud CLI CLI with your user account by running gcloud CLI `init` or gcloud CLI `auth login` . You can check the active account by running gcloud CLI `auth list` .

Save the request body in a file named request.json, and run the following command:

``` 
  $cred = gcloud auth print-access-token
  $headers = @{ "Authorization" = "Bearer $cred" }

  Invoke-WebRequest `
      -Method POST `
      -Headers $headers `
      -ContentType: "application/json; charset=utf-8" `
      -InFile request.json `
      -Uri "https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/ragCorpora" | Select-Object -Expand Content
```

You should receive a successful status code (2xx).

The following example demonstrates how to create a RAG corpus by using the REST API.

``` 
  // CreateRagCorpus
  // Input: LOCATION, PROJECT_ID, CORPUS_DISPLAY_NAME
  // Output: CreateRagCorpusOperationMetadata
  curl -X POST \
  -H "Authorization: Bearer $(gcloud auth print-access-token)" \
  -H "Content-Type: application/json" \
  https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/ragCorpora \
  -d '{
        "display_name" : "CORPUS_DISPLAY_NAME"
    }'
```

### Python

To learn how to install or update the Vertex AI SDK for Python, see [Install the Vertex AI SDK for Python](https://docs.cloud.google.com/vertex-ai/docs/start/use-vertex-ai-python-sdk) . For more information, see the [Python API reference documentation](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest) .

    import agentplatform
    from agentplatform import types
    
    # TODO(developer): Update and un-comment below lines
    # PROJECT_ID = "your-project-id"
    # display_name = "test_corpus"
    # description = "Corpus Description"
    
    # Initialize Agent Platform client once per session
    client = agentplatform.Client(project=PROJECT_ID, location="us-central1")
    
    # Configure project-level config
    backend_config = types.RagVectorDbConfig(
        rag_embedding_model_config=types.RagEmbeddingModelConfig(
            vertex_prediction_endpoint=types.RagEmbeddingModelConfigVertexPredictionEndpoint(
                endpoint="publishers/google/models/text-embedding-005"
            )
        )
    )
    
    # Create a corpus
    corpus = client.rag.create_corpus(
        rag_corpus=types.RagCorpus(
            display_name=display_name,
            description=description,
            rag_vector_db_config=backend_config,
        )
    )
    print(corpus)
    # Example response:
    # RagCorpus(name='projects/1234567890/locations/us-central1/ragCorpora/1234567890',
    # display_name='test_corpus', description='Corpus Description', embedding_model_config=...
    # ...

### Update a RAG corpus example

You can update your RAG corpus with a new display name, description, and vector database configuration. However, you can't change the following [parameters](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/models/rag-api-v1#update-a-rag-corpus-params-api) in your RAG corpus:

  - The vector database type. For example, you can't change the vector database from Weaviate to Feature Store on Gemini Enterprise Agent Platform.
  - If you're using the managed database option, you can't update the vector database configuration.

These examples demonstrate how to update a RAG corpus.

### REST

Before using any of the request data, make the following replacements:

  - **PROJECT\_ID** : Your project ID.
  - **LOCATION** : The region to process the request.
  - **CORPUS\_ID** : The corpus ID of your RAG corpus.
  - **CORPUS\_DISPLAY\_NAME** : The display name of the RAG corpus.
  - **CORPUS\_DESCRIPTION** : The description of the RAG corpus.
  - **INDEX\_NAME** : The resource name of the Vector Search Index. Format: `projects/{project}/locations/{location}/indexes/{index}` .
  - **INDEX\_ENDPOINT\_NAME** : The resource name of the Vector Search index endpoint. Format: `projects/{project}/locations/{location}/indexEndpoints/{index_endpoint}` .

HTTP method and URL:

    PATCH https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/ragCorpora/CORPUS_ID

Request JSON body:

    {
      "display_name" : "CORPUS_DISPLAY_NAME",
      "description": "CORPUS_DESCRIPTION",
      "vector_db_config": {
        "vertex_vector_search": {
            "index": "INDEX_NAME",
            "index_endpoint": "INDEX_ENDPOINT_NAME",
        }
      }
    }

To send your request, choose one of these options:

### curl

> **Note:** The following command assumes that you have signed in to the Google Cloud CLI CLI with your user account by running gcloud CLI `init` or gcloud CLI `auth login` , or by using Cloud Shell, which automatically signs you into the gcloud CLI CLI . You can check the active account by running gcloud CLI `auth list` .

Save the request body in a file named request.json, and run the following command:

    curl -X PATCH \
        -H "Authorization: Bearer $(gcloud auth print-access-token)" \
        -H "Content-Type: application/json; charset=utf-8" \
        -d @request.json \
        "https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/ragCorpora/CORPUS_ID"

### Powershell

> **Note:** The following command assumes that you have signed in to the gcloud CLI CLI with your user account by running gcloud CLI `init` or gcloud CLI `auth login` . You can check the active account by running gcloud CLI `auth list` .

Save the request body in a file named request.json, and run the following command:

    $cred = gcloud auth print-access-token
    $headers = @{ "Authorization" = "Bearer $cred" }
    
    Invoke-WebRequest `
        -Method PATCH `
        -Headers $headers `
        -ContentType: "application/json; charset=utf-8" `
        -InFile request.json `
        -Uri "https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/ragCorpora/CORPUS_ID" | Select-Object -Expand Content

You should receive a successful status code (2xx).

### List RAG corpora example

These code samples demonstrate how to list all of the RAG corpora.

### REST

Before using any of the request data, make the following replacements:

  - **PROJECT\_ID** : Your project ID.
  - **LOCATION** : The region to process the request.
  - **PAGE\_SIZE** : The standard list page size. You might adjust the number of RAG corpora to return per page by updating the `page_size` parameter.
  - **PAGE\_TOKEN** : The standard list page token. Obtained typically using `ListRagCorporaResponse.next_page_token` of the previous `VertexRagDataService.ListRagCorpora` call.

HTTP method and URL:

    GET https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/ragCorpora?page_size=PAGE_SIZE&page_token=PAGE_TOKEN

To send your request, choose one of these options:

### curl

> **Note:** The following command assumes that you have signed in to the Google Cloud CLI CLI with your user account by running gcloud CLI `init` or gcloud CLI `auth login` , or by using Cloud Shell, which automatically signs you into the gcloud CLI CLI . You can check the active account by running gcloud CLI `auth list` .

Run the following command:

    curl -X GET \
        -H "Authorization: Bearer $(gcloud auth print-access-token)" \
        "https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/ragCorpora?page_size=PAGE_SIZE&page_token=PAGE_TOKEN"

### Powershell

> **Note:** The following command assumes that you have signed in to the gcloud CLI CLI with your user account by running gcloud CLI `init` or gcloud CLI `auth login` . You can check the active account by running gcloud CLI `auth list` .

Run the following command:

    $cred = gcloud auth print-access-token
    $headers = @{ "Authorization" = "Bearer $cred" }
    
    Invoke-WebRequest `
        -Method GET `
        -Headers $headers `
        -Uri "https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/ragCorpora?page_size=PAGE_SIZE&page_token=PAGE_TOKEN" | Select-Object -Expand Content

You should receive a successful status code ( `2xx` ) and a list of RAG corpora under the given `PROJECT_ID` .

### Python

To learn how to install or update the Vertex AI SDK for Python, see [Install the Vertex AI SDK for Python](https://docs.cloud.google.com/vertex-ai/docs/start/use-vertex-ai-python-sdk) . For more information, see the [Python API reference documentation](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest) .

    import agentplatform
    
    # TODO(developer): Update and un-comment below lines
    # PROJECT_ID = "your-project-id"
    
    # Initialize Agent Platform client once per session
    client = agentplatform.Client(project=PROJECT_ID, location="us-central1")
    
    corpora = client.rag.list_corpora()
    print(corpora)
    # Example response:
    # ListRagCorporaPager<rag_corpora {
    #   name: "projects/[PROJECT_ID]/locations/us-central1/ragCorpora/2305843009213693952"
    #   display_name: "test_corpus"
    #   create_time {
    # ...

### Get a RAG corpus example

These code samples demonstrate how to get a RAG corpus.

### REST

Before using any of the request data, make the following replacements:

  - **PROJECT\_ID** : Your project ID.
  - **LOCATION** : The region to process the request.
  - **RAG\_CORPUS\_ID** : The ID of the RAG corpus resource.

HTTP method and URL:

    GET https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/ragCorpora/RAG_CORPUS_ID

To send your request, choose one of these options:

### curl

> **Note:** The following command assumes that you have signed in to the Google Cloud CLI CLI with your user account by running gcloud CLI `init` or gcloud CLI `auth login` , or by using Cloud Shell, which automatically signs you into the gcloud CLI CLI . You can check the active account by running gcloud CLI `auth list` .

Run the following command:

    curl -X GET \
        -H "Authorization: Bearer $(gcloud auth print-access-token)" \
        "https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/ragCorpora/RAG_CORPUS_ID"

### Powershell

> **Note:** The following command assumes that you have signed in to the gcloud CLI CLI with your user account by running gcloud CLI `init` or gcloud CLI `auth login` . You can check the active account by running gcloud CLI `auth list` .

Run the following command:

    $cred = gcloud auth print-access-token
    $headers = @{ "Authorization" = "Bearer $cred" }
    
    Invoke-WebRequest `
        -Method GET `
        -Headers $headers `
        -Uri "https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/ragCorpora/RAG_CORPUS_ID" | Select-Object -Expand Content

A successful response returns the `RagCorpus` resource.

The `get` and `list` commands are used in an example to demonstrate how `RagCorpus` uses the `rag_embedding_model_config` field with in the `vector_db_config` , which points to the embedding model you have chosen.

```` 
    PROJECT_ID: Your project ID.
    LOCATION: The region to process the request.
    RAG_CORPUS_ID: The corpus ID of your RAG corpus.
  ```

```sh
  // GetRagCorpus
  // Input: LOCATION, PROJECT_ID, RAG_CORPUS_ID
  // Output: RagCorpus
  curl -X GET \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer $(gcloud auth print-access-token)" \
  https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/ragCorpora/RAG_CORPUS_ID

  // ListRagCorpora
  curl -sS -X GET \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer $(gcloud auth print-access-token)" \
  https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/ragCorpora/
  ```
````

### Python

To learn how to install or update the Vertex AI SDK for Python, see [Install the Vertex AI SDK for Python](https://docs.cloud.google.com/vertex-ai/docs/start/use-vertex-ai-python-sdk) . For more information, see the [Python API reference documentation](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest) .

    import agentplatform
    
    # TODO(developer): Update and un-comment below lines
    # PROJECT_ID = "your-project-id"
    # corpus_name = "projects/{PROJECT_ID}/locations/us-central1/ragCorpora/{rag_corpus_id}"
    
    # Initialize Agent Platform client once per session
    client = agentplatform.Client(project=PROJECT_ID, location="us-central1")
    
    corpus = client.rag.get_corpus(name=corpus_name)
    print(corpus)
    # Example response:
    # RagCorpus(name='projects/[PROJECT_ID]/locations/us-central1/ragCorpora/1234567890',
    # display_name='test_corpus', description='Corpus Description',
    # ...

### Delete a RAG corpus example

These code samples demonstrate how to delete a RAG corpus.

### REST

Before using any of the request data, make the following replacements:

  - **PROJECT\_ID** : Your project ID.
  - **LOCATION** : The region to process the request.
  - **RAG\_CORPUS\_ID** : The ID of the `RagCorpus` resource.

HTTP method and URL:

    DELETE https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/ragCorpora/RAG_CORPUS_ID

To send your request, choose one of these options:

### curl

> **Note:** The following command assumes that you have signed in to the Google Cloud CLI CLI with your user account by running gcloud CLI `init` or gcloud CLI `auth login` , or by using Cloud Shell, which automatically signs you into the gcloud CLI CLI . You can check the active account by running gcloud CLI `auth list` .

Run the following command:

    curl -X DELETE \
        -H "Authorization: Bearer $(gcloud auth print-access-token)" \
        "https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/ragCorpora/RAG_CORPUS_ID"

### Powershell

> **Note:** The following command assumes that you have signed in to the gcloud CLI CLI with your user account by running gcloud CLI `init` or gcloud CLI `auth login` . You can check the active account by running gcloud CLI `auth list` .

Run the following command:

    $cred = gcloud auth print-access-token
    $headers = @{ "Authorization" = "Bearer $cred" }
    
    Invoke-WebRequest `
        -Method DELETE `
        -Headers $headers `
        -Uri "https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/ragCorpora/RAG_CORPUS_ID" | Select-Object -Expand Content

A successful response returns the `DeleteOperationMetadata` .

### Python

To learn how to install or update the Vertex AI SDK for Python, see [Install the Vertex AI SDK for Python](https://docs.cloud.google.com/vertex-ai/docs/start/use-vertex-ai-python-sdk) . For more information, see the [Python API reference documentation](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest) .

    import agentplatform
    
    # TODO(developer): Update and un-comment below lines
    # PROJECT_ID = "your-project-id"
    # corpus_name = "projects/{PROJECT_ID}/locations/us-central1/ragCorpora/{rag_corpus_id}"
    
    # Initialize Agent Platform client once per session
    client = agentplatform.Client(project=PROJECT_ID, location="us-central1")
    
    client.rag.delete_corpus(name=corpus_name)
    print(f"Corpus {corpus_name} deleted.")
    # Example response:
    # Successfully deleted the RagCorpus.
    # Corpus projects/[PROJECT_ID]/locations/us-central1/ragCorpora/123456789012345 deleted.

## File management examples

This section provides examples of how to use the API to manage RAG files.

### Upload a RAG file example

These code samples demonstrate how to upload a RAG file.

### REST

Before using any of the request data, make the following replacements:

  - **PROJECT\_ID** : Your project ID.
  - **LOCATION** : The region to process the request.
  - **RAG\_CORPUS\_ID** : The corpus ID of your RAG corpus.
  - **LOCAL\_FILE\_PATH** : The local path to the file to be uploaded.
  - **DISPLAY\_NAME** : The display name of the RAG file.
  - **DESCRIPTION** : The description of the RAG file.

To send your request, use the following command:

    curl -X POST \
    -H "X-Goog-Upload-Protocol: multipart" \
    -H "Authorization: Bearer $(gcloud auth print-access-token)" \
    -F metadata="{'rag_file': {'display_name':' DISPLAY_NAME', 'description':'DESCRIPTION'}}" \
    -F file=@LOCAL_FILE_PATH \
    "https://LOCATION-aiplatform.googleapis.com/upload/v1/projects/PROJECT_ID/locations/LOCATION/ragCorpora/RAG_CORPUS_ID/ragFiles:upload"

### Python

To learn how to install or update the Vertex AI SDK for Python, see [Install the Vertex AI SDK for Python](https://docs.cloud.google.com/vertex-ai/docs/start/use-vertex-ai-python-sdk) . For more information, see the [Python API reference documentation](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest) .

    import agentplatform
    
    # TODO(developer): Update and un-comment below lines
    # PROJECT_ID = "your-project-id"
    # corpus_name = "projects/{PROJECT_ID}/locations/us-central1/ragCorpora/{rag_corpus_id}"
    # path = "path/to/local/file.txt"
    # display_name = "file_display_name"
    
    # Initialize Agent Platform client once per session
    client = agentplatform.Client(project=PROJECT_ID, location="us-east4")
    
    rag_file = client.rag.upload_file(
        corpus_name=corpus_name,
        path=path,
        display_name=display_name,
    )
    print(rag_file)
    # RagFile(name='projects/[PROJECT_ID]/locations/us-central1/ragCorpora/1234567890/ragFiles/09876543',
    #  display_name='file_display_name')

### Import RAG files example

Files and folders can be imported from Drive or Cloud Storage. You can use `response.metadata` to view partial failures, request time, and response time in the SDK's `response` object.

The `response.skipped_rag_files_count` refers to the number of files that were skipped during import. A file is skipped when the following conditions are met:

1.  The file has already been imported.
2.  The file hasn't changed.
3.  The chunking configuration for the file hasn't changed.

### Python

    from vertexai import rag
    import vertexai
    
    # TODO(developer): Update and un-comment below lines
    # PROJECT_ID = "your-project-id"
    # corpus_name = "projects/{PROJECT_ID}/locations/us-central1/ragCorpora/{rag_corpus_id}"
    # paths = ["https://drive.google.com/file/123", "gs://my_bucket/my_files_dir"]  # Supports Cloud Storage and Google Drive Links
    
    # Initialize API once per session
    vertexai.init(project=PROJECT_ID, location="us-central1")
    
    response = rag.import_files(
        corpus_name=corpus_name,
        paths=paths,
        transformation_config=rag.TransformationConfig(
            rag.ChunkingConfig(chunk_size=1024, chunk_overlap=256)
        ),
        import_result_sink="gs://sample-existing-folder/sample_import_result_unique.ndjson",  # Optional: This must be an existing Cloud Storage bucket folder, and the filename must be unique (non-existent).
        llm_parser=rag.LlmParserConfig(
          model_name="gemini-2.5-pro-preview-05-06",
          max_parsing_requests_per_min=100,
        ),  # Optional
        max_embedding_requests_per_min=900,  # Optional
    )
    print(f"Imported {response.imported_rag_files_count} files.")

### REST

Before using any of the request data, make the following replacements:

  - **PROJECT\_ID** : Your project ID.
  - **LOCATION** : The region to process the request.
  - **RAG\_CORPUS\_ID** : The corpus ID of your RAG corpus.
  - **FOLDER\_RESOURCE\_ID** : The resource ID of your Drive folder.
  - **GCS\_URIS** : A list of Cloud Storage locations. Example: `gs://my-bucket1` .
  - **CHUNK\_SIZE** : Number of tokens each chunk should have.
  - **CHUNK\_OVERLAP** : Number of tokens overlap between chunks.
  - **EMBEDDING\_MODEL\_QPM\_RATE** : The QPM rate to limit RAG's access to your embedding model. Example: 1,000.

HTTP method and URL:

    POST https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/ragCorpora/RAG_CORPUS_ID/ragFiles:import

Request JSON body:

    {
      "import_rag_files_config": {
        "gcs_source": {
          "uris": "GCS_URIS"
        },
        "rag_file_chunking_config": {
          "chunk_size": "CHUNK_SIZE",
          "chunk_overlap": "CHUNK_OVERLAP"
        }
      }
    }

To send your request, choose one of these options:

### curl

> **Note:** The following command assumes that you have signed in to the Google Cloud CLI CLI with your user account by running gcloud CLI `init` or gcloud CLI `auth login` , or by using Cloud Shell, which automatically signs you into the gcloud CLI CLI . You can check the active account by running gcloud CLI `auth list` .

Save the request body in a file named request.json, and run the following command:

    curl -X POST \
        -H "Authorization: Bearer $(gcloud auth print-access-token)" \
        -H "Content-Type: application/json; charset=utf-8" \
        -d @request.json \
        "https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/ragCorpora/RAG_CORPUS_ID/ragFiles:import"

### Powershell

> **Note:** The following command assumes that you have signed in to the gcloud CLI CLI with your user account by running gcloud CLI `init` or gcloud CLI `auth login` . You can check the active account by running gcloud CLI `auth list` .

Save the request body in a file named request.json, and run the following command:

    $cred = gcloud auth print-access-token
    $headers = @{ "Authorization" = "Bearer $cred" }
    
    Invoke-WebRequest `
        -Method POST `
        -Headers $headers `
        -ContentType: "application/json; charset=utf-8" `
        -InFile request.json `
        -Uri "https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/ragCorpora/RAG_CORPUS_ID/ragFiles:import" | Select-Object -Expand Content

A successful response returns the `ImportRagFilesOperationMetadata` resource.

The following sample demonstrates how to import a file from Cloud Storage. Use the `max_embedding_requests_per_min` control field to limit the rate at which RAG Engine calls the embedding model during the `ImportRagFiles` indexing process. The field has a default value of `1000` calls per minute.

  - **PROJECT\_ID** : Your project ID.
  - **LOCATION** : The region to process the request.
  - **RAG\_CORPUS\_ID** : The corpus ID of your RAG corpus.
  - **GCS\_URIS** : A list of Cloud Storage locations. Example: `gs://my-bucket1` .
  - **CHUNK\_SIZE** : Number of tokens each chunk should have.
  - **CHUNK\_OVERLAP** : Number of tokens overlap between chunks.
  - **EMBEDDING\_MODEL\_QPM\_RATE** : The QPM rate to limit RAGs access to your embedding model. Example: 1,000.

<!-- end list -->

    // ImportRagFiles
    // Import a single Cloud Storage file or all files in a Cloud Storage bucket.
    // Input: LOCATION, PROJECT_ID, RAG_CORPUS_ID, GCS_URIS
    // Output: ImportRagFilesOperationMetadataNumber
    // Use ListRagFiles to find the server-generated rag_file_id.
    curl -X POST \
    -H "Authorization: Bearer $(gcloud auth print-access-token)" \
    -H "Content-Type: application/json" \
    https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/ragCorpora/RAG_CORPUS_ID/ragFiles:import \
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

The following sample demonstrates how to import a file from Drive. Use the `max_embedding_requests_per_min` control field to limit the rate at which RAG Engine calls the embedding model during the `ImportRagFiles` indexing process. The field has a default value of `1000` calls per minute.

  - **PROJECT\_ID** : Your project ID.
  - **LOCATION** : The region to process the request.
  - **RAG\_CORPUS\_ID** : The corpus ID of your RAG corpus.
  - **FOLDER\_RESOURCE\_ID** : The resource ID of your Drive folder.
  - **CHUNK\_SIZE** : Number of tokens each chunk should have.
  - **CHUNK\_OVERLAP** : Number of tokens overlap between chunks.
  - **EMBEDDING\_MODEL\_QPM\_RATE** : The QPM rate to limit RAG's access to your embedding model. Example: 1,000.

<!-- end list -->

    // ImportRagFiles
    // Import all files in a Google Drive folder.
    // Input: LOCATION, PROJECT_ID, RAG_CORPUS_ID, FOLDER_RESOURCE_ID
    // Output: ImportRagFilesOperationMetadataNumber
    // Use ListRagFiles to find the server-generated rag_file_id.
    curl -X POST \
    -H "Authorization: Bearer $(gcloud auth print-access-token)" \
    -H "Content-Type: application/json" \
    https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/ragCorpora/RAG_CORPUS_ID/ragFiles:import \
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

### List RAG files example

These code samples demonstrate how to list RAG files.

### REST

Before using any of the request data, make the following replacements:

  - **PROJECT\_ID** : Your project ID.
  - **LOCATION** : The region to process the request.
  - **RAG\_CORPUS\_ID** : The ID of the `RagCorpus` resource.
  - **PAGE\_SIZE** : The standard list page size. You might adjust the number of `RagFiles` to return per page by updating the page\_size parameter.
  - **PAGE\_TOKEN** : The standard list page token. Obtained using `ListRagFilesResponse.next_page_token` of the previous `VertexRagDataService.ListRagFiles` call.

HTTP method and URL:

    GET https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/ragCorpora/RAG_CORPUS_ID/ragFiles?page_size=PAGE_SIZE&page_token=PAGE_TOKEN

To send your request, choose one of these options:

### curl

> **Note:** The following command assumes that you have signed in to the Google Cloud CLI CLI with your user account by running gcloud CLI `init` or gcloud CLI `auth login` , or by using Cloud Shell, which automatically signs you into the gcloud CLI CLI . You can check the active account by running gcloud CLI `auth list` .

Run the following command:

    curl -X GET \
        -H "Authorization: Bearer $(gcloud auth print-access-token)" \
        "https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/ragCorpora/RAG_CORPUS_ID/ragFiles?page_size=PAGE_SIZE&page_token=PAGE_TOKEN"

### Powershell

> **Note:** The following command assumes that you have signed in to the gcloud CLI CLI with your user account by running gcloud CLI `init` or gcloud CLI `auth login` . You can check the active account by running gcloud CLI `auth list` .

Run the following command:

    $cred = gcloud auth print-access-token
    $headers = @{ "Authorization" = "Bearer $cred" }
    
    Invoke-WebRequest `
        -Method GET `
        -Headers $headers `
        -Uri "https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/ragCorpora/RAG_CORPUS_ID/ragFiles?page_size=PAGE_SIZE&page_token=PAGE_TOKEN" | Select-Object -Expand Content

You should receive a successful status code (2xx) along with a list of `RagFiles` under the given `RAG_CORPUS_ID` .

### Python

To learn how to install or update the Vertex AI SDK for Python, see [Install the Vertex AI SDK for Python](https://docs.cloud.google.com/vertex-ai/docs/start/use-vertex-ai-python-sdk) . For more information, see the [Python API reference documentation](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest) .

    import agentplatform
    
    # TODO(developer): Update and un-comment below lines
    # PROJECT_ID = "your-project-id"
    # corpus_name = "projects/{PROJECT_ID}/locations/us-central1/ragCorpora/{rag_corpus_id}"
    
    # Initialize Agent Platform client once per session
    client = agentplatform.Client(project=PROJECT_ID, location="us-central1")
    
    files_response = client.rag.list_files(name=corpus_name)
    for file in files_response.rag_files:
        print(file.display_name)
        print(file.name)
    # Example response:
    # g-drive_file.txt
    # projects/1234567890/locations/us-central1/ragCorpora/111111111111/ragFiles/222222222222
    # g_cloud_file.txt
    # projects/1234567890/locations/us-central1/ragCorpora/111111111111/ragFiles/333333333333

### Get a RAG file example

These code samples demonstrate how to get a RAG file.

### REST

Before using any of the request data, make the following replacements:

  - **PROJECT\_ID** : Your project ID.
  - **LOCATION** : The region to process the request.
  - **RAG\_CORPUS\_ID** : The ID of the `RagCorpus` resource.
  - **RAG\_FILE\_ID** : The ID of the `RagFile` resource.

HTTP method and URL:

    GET https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/ragCorpora/RAG_CORPUS_ID/ragFiles/RAG_FILE_ID

To send your request, choose one of these options:

### curl

> **Note:** The following command assumes that you have signed in to the Google Cloud CLI CLI with your user account by running gcloud CLI `init` or gcloud CLI `auth login` , or by using Cloud Shell, which automatically signs you into the gcloud CLI CLI . You can check the active account by running gcloud CLI `auth list` .

Run the following command:

    curl -X GET \
        -H "Authorization: Bearer $(gcloud auth print-access-token)" \
        "https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/ragCorpora/RAG_CORPUS_ID/ragFiles/RAG_FILE_ID"

### Powershell

> **Note:** The following command assumes that you have signed in to the gcloud CLI CLI with your user account by running gcloud CLI `init` or gcloud CLI `auth login` . You can check the active account by running gcloud CLI `auth list` .

Run the following command:

    $cred = gcloud auth print-access-token
    $headers = @{ "Authorization" = "Bearer $cred" }
    
    Invoke-WebRequest `
        -Method GET `
        -Headers $headers `
        -Uri "https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/ragCorpora/RAG_CORPUS_ID/ragFiles/RAG_FILE_ID" | Select-Object -Expand Content

A successful response returns the `RagFile` resource.

### Python

To learn how to install or update the Vertex AI SDK for Python, see [Install the Vertex AI SDK for Python](https://docs.cloud.google.com/vertex-ai/docs/start/use-vertex-ai-python-sdk) . For more information, see the [Python API reference documentation](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest) .

    import agentplatform
    
    # TODO(developer): Update and un-comment below lines
    # PROJECT_ID = "your-project-id"
    # file_name = "projects/{PROJECT_ID}/locations/us-central1/ragCorpora/{rag_corpus_id}/ragFiles/{rag_file_id}"
    
    # Initialize Agent Platform client once per session
    client = agentplatform.Client(project=PROJECT_ID, location="us-central1")
    
    rag_file = client.rag.get_file(name=file_name)
    print(rag_file)
    # Example response:
    # RagFile(name='projects/1234567890/locations/us-central1/ragCorpora/11111111111/ragFiles/22222222222',
    # display_name='file_display_name', description='file description')

### Delete a RAG file example

These code samples demonstrate how to delete a RAG file.

### REST

Before using any of the request data, make the following replacements:

  - **PROJECT\_ID** \>: Your project ID.
  - **LOCATION** : The region to process the request.
  - **RAG\_CORPUS\_ID** : The ID of the RagCorpus resource.
  - **RAG\_FILE\_ID** : The ID of the RagFile resource. Format: `projects/{project}/locations/{location}/ragCorpora/{rag_corpus}/ragFiles/{rag_file_id}` .

HTTP method and URL:

    DELETE https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/ragCorpora/RAG_CORPUS_ID/ragFiles/RAG_FILE_ID

To send your request, choose one of these options:

### curl

> **Note:** The following command assumes that you have signed in to the Google Cloud CLI CLI with your user account by running gcloud CLI `init` or gcloud CLI `auth login` , or by using Cloud Shell, which automatically signs you into the gcloud CLI CLI . You can check the active account by running gcloud CLI `auth list` .

Run the following command:

    curl -X DELETE \
        -H "Authorization: Bearer $(gcloud auth print-access-token)" \
        "https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/ragCorpora/RAG_CORPUS_ID/ragFiles/RAG_FILE_ID"

### Powershell

> **Note:** The following command assumes that you have signed in to the gcloud CLI CLI with your user account by running gcloud CLI `init` or gcloud CLI `auth login` . You can check the active account by running gcloud CLI `auth list` .

Run the following command:

    $cred = gcloud auth print-access-token
    $headers = @{ "Authorization" = "Bearer $cred" }
    
    Invoke-WebRequest `
        -Method DELETE `
        -Headers $headers `
        -Uri "https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/ragCorpora/RAG_CORPUS_ID/ragFiles/RAG_FILE_ID" | Select-Object -Expand Content

### Python

To learn how to install or update the Vertex AI SDK for Python, see [Install the Vertex AI SDK for Python](https://docs.cloud.google.com/vertex-ai/docs/start/use-vertex-ai-python-sdk) . For more information, see the [Python API reference documentation](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest) .

    import agentplatform
    
    # TODO(developer): Update and un-comment below lines
    # PROJECT_ID = "your-project-id"
    # file_name = "projects/{PROJECT_ID}/locations/us-central1/ragCorpora/{rag_corpus_id}/ragFiles/{rag_file_id}"
    
    # Initialize Agent Platform client once per session
    client = agentplatform.Client(project=PROJECT_ID, location="us-central1")
    
    client.rag.delete_file(name=file_name)
    print(f"File {file_name} deleted.")
    # Example response:
    # Successfully deleted the RagFile.
    # File projects/1234567890/locations/us-central1/ragCorpora/1111111111/ragFiles/2222222222 deleted.

### Retrieval query example

When a user asks a question or provides a prompt, the retrieval component in RAG searches through its knowledge base to find information that is relevant to the query.

### Python

To learn how to install or update the Vertex AI SDK for Python, see [Install the Vertex AI SDK for Python](https://docs.cloud.google.com/vertex-ai/docs/start/use-vertex-ai-python-sdk) . For more information, see the [Python API reference documentation](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest) .

    import agentplatform
    
    from agentplatform import types
    from google.genai import types as genai_types
    
    # TODO(developer): Update and un-comment below lines
    # PROJECT_ID = "your-project-id"
    # corpus_name = "projects/[PROJECT_ID]/locations/us-central1/ragCorpora/[rag_corpus_id]"
    
    # Initialize Agent Platform client once per session
    client = agentplatform.Client(project=PROJECT_ID, location="us-east4")
    
    response = client.rag.retrieve_contexts(
        vertex_rag_store=genai_types.VertexRagStore(
            rag_resources=[
                genai_types.VertexRagStoreRagResource(
                    rag_corpus=corpus_name,
                    # Optional: supply IDs from `rag.list_files()`.
                    # rag_file_ids=["rag-file-1", "rag-file-2", ...],
                )
            ],
        ),
        query=types.RagQuery(
            text="Hello World!",
            rag_retrieval_config=genai_types.RagRetrievalConfig(
                top_k=10,
                filter=genai_types.RagRetrievalConfigFilter(
                    vector_distance_threshold=0.5
                ),
            ),
        )
    )
    print(response)
    # Example response:
    # contexts {
    #   contexts {
    #     source_uri: "gs://your-bucket-name/file.txt"
    #     text: "....
    #   ....

### REST

Before using any of the request data, make the following replacements:

  - **LOCATION** : The region to process the request.
  - **PROJECT\_ID** : Your project ID.
  - **TEXT** : The query text to get relevant contexts.
  - **SIMILARITY\_TOP\_K** : The number of top contexts to retrieve.
  - **VECTOR\_DISTANCE\_THRESHOLD** : Only contexts with a vector distance smaller than the threshold are returned.
  - **RAG\_CORPUS\_RESOURCE** : The name of the `RagCorpus` resource. Format: `projects/{project}/locations/{location}/ragCorpora/{rag_corpus}` .

HTTP method and URL:

    POST https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION:retrieveContexts

Request JSON body:

    {
      "query": {
        "text": TEXT,
        "ragRetrievalConfig": {
          "topK": SIMILARITY_TOP_K,
          "filter": {
            "vectorDistanceThreshold": VECTOR_DISTANCE_THRESHOLD
          }
        },
        "vertex_rag_store": {
          "rag_resources": {
            "rag_corpus": "RAG_CORPUS_RESOURCE"
          }
        }
      }
    }

### curl

> **Note:** The following command assumes that you have signed in to the Google Cloud CLI CLI with your user account by running gcloud CLI `init` or gcloud CLI `auth login` , or by using Cloud Shell, which automatically signs you into the gcloud CLI CLI . You can check the active account by running gcloud CLI `auth list` .

Save the request body in a file named request.json, and run the following command:

    curl -X POST \
        -H "Authorization: Bearer $(gcloud auth print-access-token)" \
        -H "Content-Type: application/json; charset=utf-8" \
        -d @request.json \
        "https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION:retrieveContexts"

### Powershell

> **Note:** The following command assumes that you have signed in to the gcloud CLI CLI with your user account by running gcloud CLI `init` or gcloud CLI `auth login` . You can check the active account by running gcloud CLI `auth list` .

Save the request body in a file named request.json, and run the following command:

    $cred = gcloud auth print-access-token
    $headers = @{ "Authorization" = "Bearer $cred" }
    
    Invoke-WebRequest `
        -Method POST `
        -Headers $headers `
        -ContentType: "application/json; charset=utf-8" `
        -InFile request.json `
        -Uri "https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION:retrieveContexts" | Select-Object -Expand Content

You should receive a successful status code (2xx) and a list of related `RagFiles` .

### Generation example

The LLM generates a grounded response using the retrieved contexts.

### REST

Before using any of the request data, make the following replacements:

  - **PROJECT\_ID** : Your project ID.
  - **LOCATION** : The region to process the request.
  - **MODEL\_ID** : LLM model for content generation. Example: `gemini-2.5-flash` .
  - **GENERATION\_METHOD** : LLM method for content generation. Options: `generateContent` , `streamGenerateContent` .
  - **INPUT\_PROMPT** : The text sent to the LLM for content generation. Try to use a prompt relevant to the uploaded rag Files.
  - **RAG\_CORPUS\_RESOURCE** : The name of the `RagCorpus` resource. Format: `projects/{project}/locations/{location}/ragCorpora/{rag_corpus}` .
  - **SIMILARITY\_TOP\_K** : Optional: The number of top contexts to retrieve.
  - **VECTOR\_DISTANCE\_THRESHOLD** : Optional: Contexts with a vector distance smaller than the threshold are returned.
  - **USER** : Your username.

HTTP method and URL:

    POST https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/publishers/google/models/MODEL_ID:GENERATION_METHOD

Request JSON body:

    {
    "contents": {
      "role": "USER",
      "parts": {
        "text": "INPUT_PROMPT"
      }
    },
    "tools": {
      "retrieval": {
      "disable_attribution": false,
      "vertex_rag_store": {
        "rag_resources": {
          "rag_corpus": "RAG_CORPUS_RESOURCE"
        },
        "similarity_top_k": "SIMILARITY_TOP_K",
        "vector_distance_threshold": VECTOR_DISTANCE_THRESHOLD
      }
      }
    }
    }

To send your request, choose one of these options:

### curl

> **Note:** The following command assumes that you have signed in to the Google Cloud CLI CLI with your user account by running gcloud CLI `init` or gcloud CLI `auth login` , or by using Cloud Shell, which automatically signs you into the gcloud CLI CLI . You can check the active account by running gcloud CLI `auth list` .

Save the request body in a file named request.json, and execute the following command:

    curl -X POST \
        -H "Authorization: Bearer $(gcloud auth print-access-token)" \
        -H "Content-Type: application/json; charset=utf-8" \
        -d @request.json \
        "https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/publishers/google/models/MODEL_ID:GENERATION_METHOD"

### Powershell

> **Note:** The following command assumes that you have signed in to the gcloud CLI CLI with your user account by running gcloud CLI `init` or gcloud CLI `auth login` . You can check the active account by running gcloud CLI `auth list` .

Save the request body in a file named request.json, and execute the following command:

    $cred = gcloud auth print-access-token
    $headers = @{ "Authorization" = "Bearer $cred" }
    
    Invoke-WebRequest `
        -Method POST `
        -Headers $headers `
        -ContentType: "application/json; charset=utf-8" `
        -InFile request.json `
        -Uri "https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/publishers/google/models/MODEL_ID:GENERATION_METHOD" | Select-Object -Expand Content

A successful response returns the generated content with citations.

### Python

To learn how to install or update the Vertex AI SDK for Python, see [Install the Vertex AI SDK for Python](https://docs.cloud.google.com/vertex-ai/docs/start/use-vertex-ai-python-sdk) . For more information, see the [Python API reference documentation](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest) .

    from google import genai
    from google.genai import types as genai_types
    
    # TODO(developer): Update and un-comment below lines
    # PROJECT_ID = "your-project-id"
    # corpus_name = "projects/{PROJECT_ID}/locations/us-central1/ragCorpora/{rag_corpus_id}"
    
    rag_retrieval_tool = genai_types.Tool(
        retrieval=genai_types.Retrieval(
            vertex_rag_store=genai_types.VertexRagStore(
                rag_resources=[
                    genai_types.VertexRagStoreRagResource(
                        rag_corpus=corpus_name
                    )
                ],
                rag_retrieval_config=genai_types.RagRetrievalConfig(
                    top_k=10,
                    filter=genai_types.RagRetrievalConfigFilter(
                        vector_distance_threshold=0.5
                    ),
                ),
            ),
        )
    )
    
    # Create a GenAI SDK client to make a generate_content request
    genai_client = genai.Client(enterprise=True, project=PROJECT_ID, location="us-central1")
    
    response = genai_client.models.generate_content(
        model="gemini-2.5-pro",
        contents="Why is the sky blue?",
        config=genai_types.GenerateContentConfig(
            tools=[rag_retrieval_tool]
        )
    )
    print(response.text)
    # Example response:
    #   The sky appears blue due to a phenomenon called Rayleigh scattering.
    #   Sunlight, which contains all colors of the rainbow, is scattered
    #   by the tiny particles in the Earth's atmosphere....
    #   ...

## Project management examples

Tier is a project-level setting available under the `RagEngineConfig` resource and impacts RAG corpora using `RagManagedDb` . To get the tier configuration, use `GetRagEngineConfig` . To update the tier configuration, use `UpdateRagEngineConfig` .

For more information on tiers and tier configuration, see [Deployment modes](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/rag-engine/deployment-modes) .

### Get project configuration

The following code samples demonstrate how to read your `RagEngineConfig` :

### Console

1.  In the Google Cloud console, go to the **RAG Engine** page.
2.  Select the region in which your RAG Engine is running. Your list of RAG corpora is updated.
3.  Click **Configure RAG Engine** . The **Configure RAG Engine** pane appears. You can see the tier that's selected for your RAG Engine.
4.  Click **Cancel** .

### Python

    from vertexai import rag
    import vertexai
    
    PROJECT_ID = YOUR_PROJECT_ID
    LOCATION = YOUR_RAG_ENGINE_LOCATION
    
    # Initialize API once per session
    vertexai.init(project=PROJECT_ID, location=LOCATION)
    
    rag_engine_config = rag.rag_data.get_rag_engine_config(
        name=f"projects/{PROJECT_ID}/locations/{LOCATION}/ragEngineConfig"
    )
    
    print(rag_engine_config)

### REST

    curl -X GET \
    -H "Content-Type: application/json" \
    -H "Authorization: Bearer $(gcloud auth print-access-token)" \
    https://${LOCATION}-aiplatform.googleapis.com/v1/projects/${PROJECT_ID}/locations/${LOCATION}/ragEngineConfig

### Update project configuration

This section provides code samples to demonstrate how to change your configuration to a Scaled, Basic, or Unprovisioned tier.

#### Update your `RagEngineConfig` to the Scaled tier

The following code samples demonstrate how to set the `RagEngineConfig` to the Scaled tier:

### Console

1.  In the Google Cloud console, go to the **RAG Engine** page.
2.  Select the region in which your RAG Engine is running. Your list of RAG corpora is updated.
3.  Click **Configure RAG Engine** . The **Configure RAG Engine** pane appears.
4.  Select the tier that you want to run your RAG Engine.
5.  Click **Save** .

### Python

    from vertexai import rag
    import vertexai
    
    PROJECT_ID = YOUR_PROJECT_ID
    LOCATION = YOUR_RAG_ENGINE_LOCATION
    
    # Initialize API once per session
    vertexai.init(project=PROJECT_ID, location=LOCATION)
    
    rag_engine_config_name=f"projects/{PROJECT_ID}/locations/{LOCATION}/ragEngineConfig"
    
    new_rag_engine_config = rag.RagEngineConfig(
    name=rag_engine_config_name,
    rag_managed_db_config=rag.RagManagedDbConfig(tier=rag.Scaled()),
    )
    
    updated_rag_engine_config = rag.rag_data.update_rag_engine_config(
    rag_engine_config=new_rag_engine_config
    )
    
    print(updated_rag_engine_config)

### REST

    curl -X PATCH \
    -H "Content-Type: application/json" \
    -H "Authorization: Bearer $(gcloud auth print-access-token)" \
    https://${LOCATION}-aiplatform.googleapis.com/v1/projects/${PROJECT_ID}/locations/${LOCATION}/ragEngineConfig -d "{'ragManagedDbConfig': {'scaled': {}}}"

#### Update your `RagEngineConfig` to the Basic tier

The following code samples demonstrate how to set the `RagEngineConfig` to the Basic tier:

> **Note:** If you have a large amount of data in your `RagManagedDb` across your RAG corpora, downgrading to a Basic tier can fail due to insufficient compute and storage capacity.

### Console

1.  In the Google Cloud console, go to the **RAG Engine** page.
2.  Select the region in which your RAG Engine is running. Your list of RAG corpora is updated.
3.  Click **Configure RAG Engine** . The **Configure RAG Engine** pane appears.
4.  Select the tier that you want to run your RAG Engine.
5.  Click **Save** .

### Python

    from vertexai import rag
    import vertexai
    
    PROJECT_ID = YOUR_PROJECT_ID
    LOCATION = YOUR_RAG_ENGINE_LOCATION
    
    # Initialize API once per session
    vertexai.init(project=PROJECT_ID, location=LOCATION)
    
    rag_engine_config_name=f"projects/{PROJECT_ID}/locations/{LOCATION}/ragEngineConfig"
    
    new_rag_engine_config = rag.RagEngineConfig(
    name=rag_engine_config_name,
    rag_managed_db_config=rag.RagManagedDbConfig(tier=rag.Basic()),
    )
    
    updated_rag_engine_config = rag.rag_data.update_rag_engine_config(
    rag_engine_config=new_rag_engine_config
    )
    
    print(updated_rag_engine_config)

### REST

    curl -X PATCH \
    -H "Content-Type: application/json" \
    -H "Authorization: Bearer $(gcloud auth print-access-token)" \
    https://${LOCATION}-aiplatform.googleapis.com/v1/projects/${PROJECT_ID}/locations/${LOCATION}/ragEngineConfig -d "{'ragManagedDbConfig': {'basic': {}}}"

#### Update your `RagEngineConfig` to the Unprovisioned tier

The following code samples demonstrate how to set the `RagEngineConfig` to the Unprovisioned tier:

### Console

1.  In the Google Cloud console, go to the **RAG Engine** page.
2.  Select the region in which your RAG Engine is running. Your list of RAG corpora is updated.
3.  Click **Configure RAG Engine** . The **Configure RAG Engine** pane appears.
4.  Click **Delete RAG Engine** . A confirmation dialog appears.
5.  Verify that you're about to delete your data in RAG Engine by typing *delete* , then click **Confirm** .
6.  Click **Save** .

### Python

    from vertexai import rag
    import vertexai
    
    PROJECT_ID = YOUR_PROJECT_ID
    LOCATION = YOUR_RAG_ENGINE_LOCATION
    
    # Initialize API once per session
    vertexai.init(project=PROJECT_ID, location=LOCATION)
    
    rag_engine_config_name=f"projects/{PROJECT_ID}/locations/{LOCATION}/ragEngineConfig"
    
    new_rag_engine_config = rag.RagEngineConfig(
      name=rag_engine_config_name,
      rag_managed_db_config=rag.RagManagedDbConfig(tier=rag.Unprovisioned()),
    )
    
    updated_rag_engine_config = rag.rag_data.update_rag_engine_config(
      rag_engine_config=new_rag_engine_config
    )
    
    print(updated_rag_engine_config)

### REST

    curl -X PATCH \
    -H "Content-Type: application/json" \
    -H "Authorization: Bearer $(gcloud auth print-access-token)" \
    https://${LOCATION}-aiplatform.googleapis.com/v1/projects/${PROJECT_ID}/locations/${LOCATION}/ragEngineConfig -d "{'ragManagedDbConfig': {'unprovisioned': {}}}"

## What's next

  - To learn more about supported generation models, see [Generative AI models that support RAG](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/rag-engine/supported-rag-models) .
  - To learn more about supported embedding models, see [Embedding models](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/rag-engine/use-embedding-models#supported-embedding-models) .
  - To learn more about open models, see [Open models](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/rag-engine/use-embedding-models#use-oss-embedding-models) .
  - To learn more about RAG Engine, see [RAG Engine overview](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/rag-engine/rag-overview) .
