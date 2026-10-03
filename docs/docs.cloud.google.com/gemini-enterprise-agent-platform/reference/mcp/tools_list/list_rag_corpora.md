---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/list_rag_corpora
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/list_rag_corpora
title: 'MCP Tools Reference: aiplatform.googleapis.com'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

## Tool: `list_rag_corpora`

Lists all RagCorpora in a specified Google Cloud location. Use this to discover existing RAG resources. Format: 'projects/{project_id}/locations/{region}'. CRITICAL: For {region}, use the region specified in the current context window. If no region is specified, prompt the user to provide one. Do not use 'global'.

The following sample demonstrate how to use `curl` to invoke the `list_rag_corpora` MCP tool.

**Curl Request**

```
curl --location 'https://aiplatform.googleapis.com/mcp/generate' \
--header 'content-type: application/json' \
--header 'accept: application/json, text/event-stream' \
--data '{
  "method": "tools/call",
  "params": {
    "name": "list_rag_corpora",
    "arguments": {
      // provide these details according to the tool's MCP specification
    }
  },
  "jsonrpc": "2.0",
  "id": 1
}'
```

## Input Schema

Request message for `VertexRagDataService.ListRagCorpora` .

### ListRagCorporaRequest

**JSON representation**

```
{
  "parent": string,
  "pageSize": integer,
  "pageToken": string
}
```

| Fields      |                                                                                                                                                                              |
|-------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `parent`    | `string` Required. The resource name of the Location from which to list the RagCorpora. Format: `projects/{project}/locations/{location}`                                    |
| `pageSize`  | `integer` Optional. The standard list page size. The maximum value is 100. If not specified, a default value of 100 will be used.                                            |
| `pageToken` | `string` Optional. The standard list page token. Typically obtained via `ListRagCorporaResponse.next_page_token` of the previous `VertexRagDataService.ListRagCorpora` call. |

## Output Schema

Response message for `VertexRagDataService.ListRagCorpora` .

### ListRagCorporaResponse

**JSON representation**

```
{
  "ragCorpora": [
    {
      object (RagCorpus)
    }
  ],
  "nextPageToken": string
}
```

| Fields          |                                                                                                                                                                                                          |
|-----------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `ragCorpora[]`  | `object ( `[`RagCorpus`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/create_rag_corpus#Input.Schema.RagCorpus)` )` List of RagCorpora in the requested page. |
| `nextPageToken` | `string` A token to retrieve the next page of results. Pass to `ListRagCorporaRequest.page_token` to obtain that page.                                                                                   |

### RagCorpus

**JSON representation**

```
{
  "name": string,
  "displayName": string,
  "description": string,
  "createTime": string,
  "updateTime": string,
  "corpusStatus": {
    object (CorpusStatus)
  },
  "encryptionSpec": {
    object (EncryptionSpec)
  },
  "satisfiesPzs": boolean,
  "satisfiesPzi": boolean,

  // Union field backend_config can be only one of the following:
  "vectorDbConfig": {
    object (RagVectorDbConfig)
  },
  "vertexAiSearchConfig": {
    object (VertexAiSearchConfig)
  }
  // End of list of possible types for union field backend_config.
}
```

| Fields                                                                                                                                                               |                                                                                                                                                                                                                                                                                                                                                                                                                                    |
|----------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `name`                                                                                                                                                               | `string` Output only. The resource name of the RagCorpus.                                                                                                                                                                                                                                                                                                                                                                          |
| `displayName`                                                                                                                                                        | `string` Required. The display name of the RagCorpus. The name can be up to 128 characters long and can consist of any UTF-8 characters.                                                                                                                                                                                                                                                                                           |
| `description`                                                                                                                                                        | `string` Optional. The description of the RagCorpus.                                                                                                                                                                                                                                                                                                                                                                               |
| `createTime`                                                                                                                                                         | `string ( `[`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp)` format)` Output only. Timestamp when this RagCorpus was created. Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .      |
| `updateTime`                                                                                                                                                         | `string ( `[`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp)` format)` Output only. Timestamp when this RagCorpus was last updated. Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` . |
| `corpusStatus`                                                                                                                                                       | `object ( `[`CorpusStatus`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/create_rag_corpus#Input.Schema.CorpusStatus)` )` Output only. RagCorpus state.                                                                                                                                                                                                                                 |
| `encryptionSpec`                                                                                                                                                     | `object ( `[`EncryptionSpec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/upload_model#Input.Schema.EncryptionSpec)` )` Optional. Immutable. The CMEK key name used to encrypt at-rest data related to this Corpus. Only applicable to RagManagedDb option for Vector DB. This field can only be set at corpus creation time, and cannot be updated or deleted.                        |
| `satisfiesPzs`                                                                                                                                                       | `boolean` Output only. Reserved for future use.                                                                                                                                                                                                                                                                                                                                                                                    |
| `satisfiesPzi`                                                                                                                                                       | `boolean` Output only. Reserved for future use.                                                                                                                                                                                                                                                                                                                                                                                    |
| Union field `backend_config` . The backend config of the RagCorpus. It can be data store and/or retrieval engine. `backend_config` can be only one of the following: |                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| `vectorDbConfig`                                                                                                                                                     | `object ( `[`RagVectorDbConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/create_rag_corpus#Input.Schema.RagVectorDbConfig)` )` Optional. Immutable. The config for the Vector DBs.                                                                                                                                                                                                 |
| `vertexAiSearchConfig`                                                                                                                                               | `object ( `[`VertexAiSearchConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/create_rag_corpus#Input.Schema.VertexAiSearchConfig)` )` Optional. Immutable. The config for the Agent Platform Search.                                                                                                                                                                                |

### RagVectorDbConfig

**JSON representation**

```
{
  "apiAuth": {
    object (ApiAuth)
  },
  "ragEmbeddingModelConfig": {
    object (RagEmbeddingModelConfig)
  },

  // Union field vector_db can be only one of the following:
  "ragManagedDb": {
    object (RagManagedDb)
  },
  "pinecone": {
    object (Pinecone)
  },
  "vertexVectorSearch": {
    object (VertexVectorSearch)
  }
  // End of list of possible types for union field vector_db.
}
```

| Fields                                                                                                |                                                                                                                                                                                                                                                              |
|-------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `apiAuth`                                                                                             | `object ( `[`ApiAuth`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/create_rag_corpus#Input.Schema.ApiAuth)` )` Authentication config for the chosen Vector DB.                                                   |
| `ragEmbeddingModelConfig`                                                                             | `object ( `[`RagEmbeddingModelConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/create_rag_corpus#Input.Schema.RagEmbeddingModelConfig)` )` Optional. Immutable. The embedding model config of the Vector DB. |
| Union field `vector_db` . The config for the Vector DB. `vector_db` can be only one of the following: |                                                                                                                                                                                                                                                              |
| `ragManagedDb`                                                                                        | `object ( `[`RagManagedDb`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/create_rag_corpus#Input.Schema.RagManagedDb)` )` The config for the RAG-managed Vector DB.                                               |
| `pinecone`                                                                                            | `object ( `[`Pinecone`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/create_rag_corpus#Input.Schema.Pinecone)` )` The config for the Pinecone.                                                                    |
| `vertexVectorSearch`                                                                                  | `object ( `[`VertexVectorSearch`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/create_rag_corpus#Input.Schema.VertexVectorSearch)` )` The config for the Vertex Vector Search.                                    |

### RagManagedDb

**JSON representation**

```
{

  // Union field retrieval_strategy can be only one of the following:
  "knn": {
    object (KNN)
  },
  "ann": {
    object (ANN)
  }
  // End of list of possible types for union field retrieval_strategy.
}
```

| Fields                                                                                                                  |                                                                                                                                                                                                                                                                                               |
|-------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Union field `retrieval_strategy` . Choice of retrieval strategy. `retrieval_strategy` can be only one of the following: |                                                                                                                                                                                                                                                                                               |
| `knn`                                                                                                                   | `object ( ``KNN`` )` Performs a KNN search on RagCorpus. Default choice if not specified.                                                                                                                                                                                                     |
| `ann`                                                                                                                   | `object ( `[`ANN`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/create_rag_corpus#Input.Schema.ANN)` )` Performs an ANN search on RagCorpus. Use this if you have a lot of files (\> 10K) in your RagCorpus and want to reduce the search latency. |

### ANN

**JSON representation**

```
{
  "treeDepth": integer,
  "leafCount": integer
}
```

| Fields      |                                                                                                                                                                                                                                                          |
|-------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `treeDepth` | `integer` The depth of the tree-based structure. Only depth values of 2 and 3 are supported. Recommended value is 2 if you have if you have O(10K) files in the RagCorpus and set this to 3 if more than that. Default value is 2.                       |
| `leafCount` | `integer` Number of leaf nodes in the tree-based structure. Each leaf node contains groups of closely related vectors along with their corresponding centroid. Recommended value is 10 \* sqrt(num of RagFiles in your RagCorpus). Default value is 500. |

### Pinecone

**JSON representation**

```
{
  "indexName": string
}
```

| Fields      |                                                                            |
|-------------|----------------------------------------------------------------------------|
| `indexName` | `string` Pinecone index name. This value cannot be changed after it's set. |

### VertexVectorSearch

**JSON representation**

```
{
  "indexEndpoint": string,
  "index": string
}
```

| Fields          |                                                                                                                                     |
|-----------------|-------------------------------------------------------------------------------------------------------------------------------------|
| `indexEndpoint` | `string` The resource name of the Index Endpoint. Format: `projects/{project}/locations/{location}/indexEndpoints/{index_endpoint}` |
| `index`         | `string` The resource name of the Index. Format: `projects/{project}/locations/{location}/indexes/{index}`                          |

### ApiAuth

**JSON representation**

```
{

  // Union field auth_config can be only one of the following:
  "apiKeyConfig": {
    object (ApiKeyConfig)
  }
  // End of list of possible types for union field auth_config.
}
```

| Fields                                                                                       |                                                                                                                                                                                      |
|----------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Union field `auth_config` . The auth config. `auth_config` can be only one of the following: |                                                                                                                                                                                      |
| `apiKeyConfig`                                                                               | `object ( `[`ApiKeyConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/create_rag_corpus#Input.Schema.ApiKeyConfig)` )` The API secret. |

### ApiKeyConfig

**JSON representation**

```
{
  "apiKeySecretVersion": string,
  "apiKeyString": string
}
```

| Fields                |                                                                                                                                                |
|-----------------------|------------------------------------------------------------------------------------------------------------------------------------------------|
| `apiKeySecretVersion` | `string` Required. The SecretManager secret version resource name storing API key. e.g. projects/{project}/secrets/{secret}/versions/{version} |
| `apiKeyString`        | `string` The API key string. Either this or `api_key_secret_version` must be set.                                                              |

### RagEmbeddingModelConfig

**JSON representation**

```
{

  // Union field model_config can be only one of the following:
  "vertexPredictionEndpoint": {
    object (VertexPredictionEndpoint)
  }
  // End of list of possible types for union field model_config.
}
```

| Fields                                                                                                 |                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
|--------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Union field `model_config` . The model config to use. `model_config` can be only one of the following: |                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| `vertexPredictionEndpoint`                                                                             | `object ( `[`VertexPredictionEndpoint`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/create_rag_corpus#Input.Schema.VertexPredictionEndpoint)` )` The Agent Platform Prediction Endpoint that either refers to a publisher model or an endpoint that is hosting a 1P fine-tuned text embedding model. Endpoints hosting non-1P fine-tuned text embedding models are currently not supported. This is used for dense vector search. |

### VertexPredictionEndpoint

**JSON representation**

```
{
  "endpoint": string,
  "model": string,
  "modelVersionId": string
}
```

| Fields           |                                                                                                                                                                                                                   |
|------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `endpoint`       | `string` Required. The endpoint resource name. Format: `projects/{project}/locations/{location}/publishers/{publisher}/models/{model}` or `projects/{project}/locations/{location}/endpoints/{endpoint}`          |
| `model`          | `string` Output only. The resource name of the model that is deployed on the endpoint. Present only when the endpoint is not a publisher model. Pattern: `projects/{project}/locations/{location}/models/{model}` |
| `modelVersionId` | `string` Output only. Version ID of the model that is deployed on the endpoint. Present only when the endpoint is not a publisher model.                                                                          |

### VertexAiSearchConfig

**JSON representation**

```
{
  "servingConfig": string
}
```

| Fields          |                                                                                                                                                                                                                                                                                                                                    |
|-----------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `servingConfig` | `string` Agent Platform Search Serving Config resource full name. For example, `projects/{project}/locations/{location}/collections/{collection}/engines/{engine}/servingConfigs/{serving_config}` or `projects/{project}/locations/{location}/collections/{collection}/dataStores/{data_store}/servingConfigs/{serving_config}` . |

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

### CorpusStatus

**JSON representation**

```
{
  "state": enum (State),
  "errorStatus": string
}
```

| Fields        |                                                                                                                                                                                         |
|---------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `state`       | `enum ( `[`State`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/create_rag_corpus#Input.Schema.State)` )` Output only. RagCorpus life state. |
| `errorStatus` | `string` Output only. Only when the `state` field is ERROR.                                                                                                                             |

### EncryptionSpec

**JSON representation**

```
{
  "kmsKeyName": string
}
```

| Fields       |                                                                                                                                                                                                                                                                   |
|--------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `kmsKeyName` | `string` Required. Resource name of the Cloud KMS key used to protect the resource. The Cloud KMS key must be in the same region as the resource. It must have the format `projects/{project}/locations/{location}/keyRings/{key_ring}/cryptoKeys/{crypto_key}` . |

### State

RagCorpus life state.

| Enums         |                                                                                 |
|---------------|---------------------------------------------------------------------------------|
| `UNKNOWN`     | This state is not supposed to happen.                                           |
| `INITIALIZED` | RagCorpus resource entry is initialized, but hasn't done validation.            |
| `ACTIVE`      | RagCorpus is provisioned successfully and is ready to serve.                    |
| `ERROR`       | RagCorpus is in a problematic situation. See `error_message` field for details. |

### Tool Annotations

Destructive Hint: ❌ \| Idempotent Hint: ✅ \| Read Only Hint: ✅ \| Open World Hint: ❌
