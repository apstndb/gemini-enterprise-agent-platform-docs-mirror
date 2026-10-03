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

`createTime` `string ( `[`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp)` format)`

Output only. timestamp when this RagCorpus was created.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`updateTime` `string ( `[`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp)` format)`

Output only. timestamp when this RagCorpus was last updated.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`corpusStatus` `object ( `[`CorpusStatus`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.ragCorpora#CorpusStatus)` )`

Output only. RagCorpus state.

`encryptionSpec` `object ( `[`EncryptionSpec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/EncryptionSpec)` )`

Optional. Immutable. The CMEK key name used to encrypt at-rest data related to this Corpus. Only applicable to RagManagedDb option for Vector DB. This field can only be set at corpus creation time, and cannot be updated or deleted.

`satisfiesPzs` `boolean`

Output only. reserved for future use.

`satisfiesPzi` `boolean`

Output only. reserved for future use.

`backend_config` `Union type`

The backend config of the RagCorpus. It can be data store and/or retrieval engine. The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:

`vectorDbConfig` `object ( `[`RagVectorDbConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.ragCorpora#RagVectorDbConfig)` )`

Optional. Immutable. The config for the Vector DBs.

`vertexAiSearchConfig` `object ( `[`VertexAiSearchConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.ragCorpora#VertexAiSearchConfig)` )`

Optional. Immutable. The config for the Agent Platform Search.

End of mutually exclusive fields.

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

  // backend_config
  "vectorDbConfig": {
    object (RagVectorDbConfig)
  },
  "vertexAiSearchConfig": {
    object (VertexAiSearchConfig)
  }
  // Union type
}
```

## RagVectorDbConfig

Config for the Vector DB to use for RAG.

Fields

`apiAuth` `object ( `[`ApiAuth`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.ragCorpora#ApiAuth)` )`

Authentication config for the chosen Vector DB.

`ragEmbeddingModelConfig` `object ( `[`RagEmbeddingModelConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.ragCorpora#RagEmbeddingModelConfig)` )`

Optional. Immutable. The embedding model config of the Vector DB.

`vector_db` `Union type`

The config for the Vector DB. The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:

`ragManagedDb` `object ( `[`RagManagedDb`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.ragCorpora#RagManagedDb)` )`

The config for the RAG-managed Vector DB.

`pinecone` `object ( `[`Pinecone`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.ragCorpora#Pinecone)` )`

The config for the Pinecone.

`vertexVectorSearch` `object ( `[`VertexVectorSearch`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.ragCorpora#VertexVectorSearch)` )`

The config for the Vertex Vector Search.

End of mutually exclusive fields.

**JSON representation**

```
{
  "apiAuth": {
    object (ApiAuth)
  },
  "ragEmbeddingModelConfig": {
    object (RagEmbeddingModelConfig)
  },

  // vector_db
  "ragManagedDb": {
    object (RagManagedDb)
  },
  "pinecone": {
    object (Pinecone)
  },
  "vertexVectorSearch": {
    object (VertexVectorSearch)
  }
  // Union type
}
```

## RagManagedDb

The config for the default RAG-managed Vector DB.

Fields

`retrieval_strategy` `Union type`

Choice of retrieval strategy. The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:

`knn` `object ( `[`KNN`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.ragCorpora#KNN)` )`

Performs a KNN search on RagCorpus. Default choice if not specified.

`ann` `object ( `[`ANN`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.ragCorpora#ANN)` )`

Performs an ANN search on RagCorpus. Use this if you have a lot of files (\> 10K) in your RagCorpus and want to reduce the search latency.

End of mutually exclusive fields.

**JSON representation**

```
{

  // retrieval_strategy
  "knn": {
    object (KNN)
  },
  "ann": {
    object (ANN)
  }
  // Union type
}
```

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

**JSON representation**

```
{
  "treeDepth": integer,
  "leafCount": integer
}
```

## Pinecone

The config for the Pinecone.

Fields

`indexName` `string`

Pinecone index name. This value cannot be changed after it's set.

**JSON representation**

```
{
  "indexName": string
}
```

## VertexVectorSearch

The config for the Vertex Vector Search.

Fields

`indexEndpoint` `string`

The resource name of the Index Endpoint. Format: `projects/{project}/locations/{location}/indexEndpoints/{indexEndpoint}`

`index` `string`

The resource name of the Index. Format: `projects/{project}/locations/{location}/indexes/{index}`

**JSON representation**

```
{
  "indexEndpoint": string,
  "index": string
}
```

## ApiAuth

The generic reusable api auth config. Deprecated. Please use AuthConfig (google/cloud/aiplatform/master/auth.proto) instead.

Fields

`auth_config` `Union type`

The auth config. The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:

`apiKeyConfig` `object ( `[`ApiKeyConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/ApiKeyConfig)` )`

The API secret.

End of mutually exclusive fields.

**JSON representation**

```
{

  // auth_config
  "apiKeyConfig": {
    object (ApiKeyConfig)
  }
  // Union type
}
```

## RagEmbeddingModelConfig

Config for the embedding model to use for RAG.

Fields

`model_config` `Union type`

The model config to use. The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:

`vertexPredictionEndpoint` `object ( `[`VertexPredictionEndpoint`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.ragCorpora#VertexPredictionEndpoint)` )`

The Agent Platform Prediction Endpoint that either refers to a publisher model or an endpoint that is hosting a 1P fine-tuned text embedding model. endpoints hosting non-1P fine-tuned text embedding models are currently not supported. This is used for dense vector search.

End of mutually exclusive fields.

**JSON representation**

```
{

  // model_config
  "vertexPredictionEndpoint": {
    object (VertexPredictionEndpoint)
  }
  // Union type
}
```

## VertexPredictionEndpoint

Config representing a model hosted on Vertex Prediction Endpoint.

Fields

`endpoint` `string`

Required. The endpoint resource name. Format: `projects/{project}/locations/{location}/publishers/{publisher}/models/{model}` or `projects/{project}/locations/{location}/endpoints/{endpoint}`

`model` `string`

Output only. The resource name of the model that is deployed on the endpoint. Present only when the endpoint is not a publisher model. Pattern: `projects/{project}/locations/{location}/models/{model}`

`modelVersionId` `string`

Output only. version id of the model that is deployed on the endpoint. Present only when the endpoint is not a publisher model.

**JSON representation**

```
{
  "endpoint": string,
  "model": string,
  "modelVersionId": string
}
```

## VertexAiSearchConfig

Config for the Agent Platform Search.

Fields

`servingConfig` `string`

Agent Platform Search Serving Config resource full name. For example, `projects/{project}/locations/{location}/collections/{collection}/engines/{engine}/servingConfigs/{servingConfig}` or `projects/{project}/locations/{location}/collections/{collection}/dataStores/{dataStore}/servingConfigs/{servingConfig}` .

**JSON representation**

```
{
  "servingConfig": string
}
```

## CorpusStatus

RagCorpus status.

Fields

`state` `enum ( `[`State`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.ragCorpora#State)` )`

Output only. RagCorpus life state.

`errorStatus` `string`

Output only. Only when the `state` field is ERROR.

**JSON representation**

```
{
  "state": enum (State),
  "errorStatus": string
}
```

## State

RagCorpus life state.

| Enums         |                                                                                |
|---------------|--------------------------------------------------------------------------------|
| `UNKNOWN`     | This state is not supposed to happen.                                          |
| `INITIALIZED` | RagCorpus resource entry is initialized, but hasn't done validation.           |
| `ACTIVE`      | RagCorpus is provisioned successfully and is ready to serve.                   |
| `ERROR`       | RagCorpus is in a problematic situation. See `errorMessage` field for details. |

| Methods                                                                                                                           |                                 |
|-----------------------------------------------------------------------------------------------------------------------------------|---------------------------------|
| [`create`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.ragCorpora/create) | Creates a RagCorpus.            |
| [`delete`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.ragCorpora/delete) | Deletes a RagCorpus.            |
| [`get`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.ragCorpora/get)       | Gets a RagCorpus.               |
| [`list`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.ragCorpora/list)     | Lists RagCorpora in a Location. |
| [`patch`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.ragCorpora/patch)   | Updates a RagCorpus.            |
