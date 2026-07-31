---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/create_rag_corpus
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/create_rag_corpus
title: 'MCP Tools Reference: aiplatform.googleapis.com'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

## Tool: `create_rag_corpus`

Creates a new RagCorpus to store documents for RAG. This is a long-running operation. Format: 'projects/{project\_id}/locations/{region}'. CRITICAL: For {region}, use the region specified in the current context window. If no region is specified, prompt the user to provide one. Do not use 'global'.

The following sample demonstrate how to use `curl` to invoke the `create_rag_corpus` MCP tool.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>Curl Request</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" data-syntax="Bash" translate="no"><code>                  
curl --location &#39;https://aiplatform.googleapis.com/mcp/generate&#39; \
--header &#39;content-type: application/json&#39; \
--header &#39;accept: application/json, text/event-stream&#39; \
--data &#39;{
  &quot;method&quot;: &quot;tools/call&quot;,
  &quot;params&quot;: {
    &quot;name&quot;: &quot;create_rag_corpus&quot;,
    &quot;arguments&quot;: {
      // provide these details according to the tool&#39;s MCP specification
    }
  },
  &quot;jsonrpc&quot;: &quot;2.0&quot;,
  &quot;id&quot;: 1
}&#39;
                </code></pre></td>
</tr>
</tbody>
</table>

## Input Schema

Request message for `VertexRagDataService.CreateRagCorpus` .

### CreateRagCorpusRequest

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;parent&quot;: string,&quot;ragCorpus&quot;: {object (RagCorpus)}}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`parent`

`string`

Required. The resource name of the Location to create the RagCorpus in. Format: `projects/{project}/locations/{location}`

`ragCorpus`

` object ( RagCorpus  ` )

Required. The RagCorpus to create.

### RagCorpus

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;name&quot;: string,&quot;displayName&quot;: string,&quot;description&quot;: string,&quot;createTime&quot;: string,&quot;updateTime&quot;: string,&quot;corpusStatus&quot;: {object (CorpusStatus)},&quot;encryptionSpec&quot;: {object (EncryptionSpec)},&quot;satisfiesPzs&quot;: boolean,&quot;satisfiesPzi&quot;: boolean,// Union field backend_config can be only one of the following:&quot;vectorDbConfig&quot;: {object (RagVectorDbConfig)},&quot;vertexAiSearchConfig&quot;: {object (VertexAiSearchConfig)}// End of list of possible types for union field backend_config.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`name`

`string`

Output only. The resource name of the RagCorpus.

`displayName`

`string`

Required. The display name of the RagCorpus. The name can be up to 128 characters long and can consist of any UTF-8 characters.

`description`

`string`

Optional. The description of the RagCorpus.

`createTime`

` string ( Timestamp  ` format)

Output only. Timestamp when this RagCorpus was created.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`updateTime`

` string ( Timestamp  ` format)

Output only. Timestamp when this RagCorpus was last updated.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`corpusStatus`

` object ( CorpusStatus  ` )

Output only. RagCorpus state.

`encryptionSpec`

` object ( EncryptionSpec  ` )

Optional. Immutable. The CMEK key name used to encrypt at-rest data related to this Corpus. Only applicable to RagManagedDb option for Vector DB. This field can only be set at corpus creation time, and cannot be updated or deleted.

`satisfiesPzs`

`boolean`

Output only. Reserved for future use.

`satisfiesPzi`

`boolean`

Output only. Reserved for future use.

Union field `backend_config` . The backend config of the RagCorpus. It can be data store and/or retrieval engine. `backend_config` can be only one of the following:

`vectorDbConfig`

` object ( RagVectorDbConfig  ` )

Optional. Immutable. The config for the Vector DBs.

`vertexAiSearchConfig`

` object ( VertexAiSearchConfig  ` )

Optional. Immutable. The config for the Agent Platform Search.

### RagVectorDbConfig

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;apiAuth&quot;: {object (ApiAuth)},&quot;ragEmbeddingModelConfig&quot;: {object (RagEmbeddingModelConfig)},// Union field vector_db can be only one of the following:&quot;ragManagedDb&quot;: {object (RagManagedDb)},&quot;pinecone&quot;: {object (Pinecone)},&quot;vertexVectorSearch&quot;: {object (VertexVectorSearch)}// End of list of possible types for union field vector_db.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`apiAuth`

` object ( ApiAuth  ` )

Authentication config for the chosen Vector DB.

`ragEmbeddingModelConfig`

` object ( RagEmbeddingModelConfig  ` )

Optional. Immutable. The embedding model config of the Vector DB.

Union field `vector_db` . The config for the Vector DB. `vector_db` can be only one of the following:

`ragManagedDb`

` object ( RagManagedDb  ` )

The config for the RAG-managed Vector DB.

`pinecone`

` object ( Pinecone  ` )

The config for the Pinecone.

`vertexVectorSearch`

` object ( VertexVectorSearch  ` )

The config for the Vertex Vector Search.

### RagManagedDb

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{// Union field retrieval_strategy can be only one of the following:&quot;knn&quot;: {object (KNN)},&quot;ann&quot;: {object (ANN)}// End of list of possible types for union field retrieval_strategy.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

Union field `retrieval_strategy` . Choice of retrieval strategy. `retrieval_strategy` can be only one of the following:

`knn`

`object ( KNN` )

Performs a KNN search on RagCorpus. Default choice if not specified.

`ann`

` object ( ANN  ` )

Performs an ANN search on RagCorpus. Use this if you have a lot of files (\> 10K) in your RagCorpus and want to reduce the search latency.

### ANN

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

Fields

`treeDepth`

`integer`

The depth of the tree-based structure. Only depth values of 2 and 3 are supported.

Recommended value is 2 if you have if you have O(10K) files in the RagCorpus and set this to 3 if more than that.

Default value is 2.

`leafCount`

`integer`

Number of leaf nodes in the tree-based structure. Each leaf node contains groups of closely related vectors along with their corresponding centroid.

Recommended value is 10 \* sqrt(num of RagFiles in your RagCorpus).

Default value is 500.

### Pinecone

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

Fields

`indexName`

`string`

Pinecone index name. This value cannot be changed after it's set.

### VertexVectorSearch

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

Fields

`indexEndpoint`

`string`

The resource name of the Index Endpoint. Format: `projects/{project}/locations/{location}/indexEndpoints/{index_endpoint}`

`index`

`string`

The resource name of the Index. Format: `projects/{project}/locations/{location}/indexes/{index}`

### ApiAuth

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{// Union field auth_config can be only one of the following:&quot;apiKeyConfig&quot;: {object (ApiKeyConfig)}// End of list of possible types for union field auth_config.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

Union field `auth_config` . The auth config. `auth_config` can be only one of the following:

`apiKeyConfig`

` object ( ApiKeyConfig  ` )

The API secret.

### ApiKeyConfig

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
  &quot;apiKeySecretVersion&quot;: string,
  &quot;apiKeyString&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`apiKeySecretVersion`

`string`

Required. The SecretManager secret version resource name storing API key. e.g. projects/{project}/secrets/{secret}/versions/{version}

`apiKeyString`

`string`

The API key string.

Either this or `api_key_secret_version` must be set.

### RagEmbeddingModelConfig

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{// Union field model_config can be only one of the following:&quot;vertexPredictionEndpoint&quot;: {object (VertexPredictionEndpoint)}// End of list of possible types for union field model_config.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

Union field `model_config` . The model config to use. `model_config` can be only one of the following:

`vertexPredictionEndpoint`

` object ( VertexPredictionEndpoint  ` )

The Agent Platform Prediction Endpoint that either refers to a publisher model or an endpoint that is hosting a 1P fine-tuned text embedding model. Endpoints hosting non-1P fine-tuned text embedding models are currently not supported. This is used for dense vector search.

### VertexPredictionEndpoint

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

Fields

`endpoint`

`string`

Required. The endpoint resource name. Format: `projects/{project}/locations/{location}/publishers/{publisher}/models/{model}` or `projects/{project}/locations/{location}/endpoints/{endpoint}`

`model`

`string`

Output only. The resource name of the model that is deployed on the endpoint. Present only when the endpoint is not a publisher model. Pattern: `projects/{project}/locations/{location}/models/{model}`

`modelVersionId`

`string`

Output only. Version ID of the model that is deployed on the endpoint. Present only when the endpoint is not a publisher model.

### VertexAiSearchConfig

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

Fields

`servingConfig`

`string`

Agent Platform Search Serving Config resource full name. For example, `projects/{project}/locations/{location}/collections/{collection}/engines/{engine}/servingConfigs/{serving_config}` or `projects/{project}/locations/{location}/collections/{collection}/dataStores/{data_store}/servingConfigs/{serving_config}` .

### Timestamp

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
  &quot;seconds&quot;: string,
  &quot;nanos&quot;: integer
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`seconds`

`string ( int64 format)`

Represents seconds of UTC time since Unix epoch 1970-01-01T00:00:00Z. Must be between -62135596800 and 253402300799 inclusive (which corresponds to 0001-01-01T00:00:00Z to 9999-12-31T23:59:59Z).

`nanos`

`integer`

Non-negative fractions of a second at nanosecond resolution. This field is the nanosecond portion of the duration, not an alternative to seconds. Negative second values with fractions must still have non-negative nanos values that count forward in time. Must be between 0 and 999,999,999 inclusive.

### CorpusStatus

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

Fields

`state`

` enum ( State  ` )

Output only. RagCorpus life state.

`errorStatus`

`string`

Output only. Only when the `state` field is ERROR.

### EncryptionSpec

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
  &quot;kmsKeyName&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`kmsKeyName`

`string`

Required. Resource name of the Cloud KMS key used to protect the resource.

The Cloud KMS key must be in the same region as the resource. It must have the format `projects/{project}/locations/{location}/keyRings/{key_ring}/cryptoKeys/{crypto_key}` .

### State

RagCorpus life state.

Enums

`UNKNOWN`

This state is not supposed to happen.

`INITIALIZED`

RagCorpus resource entry is initialized, but hasn't done validation.

`ACTIVE`

RagCorpus is provisioned successfully and is ready to serve.

`ERROR`

RagCorpus is in a problematic situation. See `error_message` field for details.

## Output Schema

This resource represents a long-running operation that is the result of a network API call.

### Operation

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;name&quot;: string,&quot;metadata&quot;: {&quot;@type&quot;: string,field1: ...,...},&quot;done&quot;: boolean,// Union field result can be only one of the following:&quot;error&quot;: {object (Status)},&quot;response&quot;: {&quot;@type&quot;: string,field1: ...,...}// End of list of possible types for union field result.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`name`

`string`

The server-assigned name, which is only unique within the same service that originally returns it. If you use the default HTTP mapping, the `name` should be a resource name ending with `operations/{unique_id}` .

`metadata`

`object`

Service-specific metadata associated with the operation. It typically contains progress information and common metadata such as create time. Some services might not provide such metadata. Any method that returns a long-running operation should document the metadata type, if any.

An object containing fields of an arbitrary type. An additional field `"@type"` contains a URI identifying the type. Example: `{ "id": 1234, "@type": "types.example.com/standard/id" }` .

`done`

`boolean`

If the value is `false` , it means the operation is still in progress. If `true` , the operation is completed, and either `error` or `response` is available.

Union field `result` . The operation result, which can be either an `error` or a valid `response` . If `done` == `false` , neither `error` nor `response` is set. If `done` == `true` , exactly one of `error` or `response` can be set. Some services might not provide the result. `result` can be only one of the following:

`error`

` object ( Status  ` )

The error result of the operation in case of failure or cancellation.

`response`

`object`

The normal, successful response of the operation. If the original method returns no data on success, such as `Delete` , the response is `google.protobuf.Empty` . If the original method is standard `Get` / `Create` / `Update` , the response should be the resource. For other methods, the response should have the type `XxxResponse` , where `Xxx` is the original method name. For example, if the original method name is `TakeSnapshot()` , the inferred response type is `TakeSnapshotResponse` .

An object containing fields of an arbitrary type. An additional field `"@type"` contains a URI identifying the type. Example: `{ "id": 1234, "@type": "types.example.com/standard/id" }` .

### Any

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
  &quot;typeUrl&quot;: string,
  &quot;value&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`typeUrl`

`string`

Identifies the type of the serialized Protobuf message with a URI reference consisting of a prefix ending in a slash and the fully-qualified type name.

Example: type.googleapis.com/google.protobuf.StringValue

This string must contain at least one `/` character, and the content after the last `/` must be the fully-qualified name of the type in canonical form, without a leading dot. Do not write a scheme on these URI references so that clients do not attempt to contact them.

The prefix is arbitrary and Protobuf implementations are expected to simply strip off everything up to and including the last `/` to identify the type. `type.googleapis.com/` is a common default prefix that some legacy implementations require. This prefix does not indicate the origin of the type, and URIs containing it are not expected to respond to any requests.

All type URL strings must be legal URI references with the additional restriction (for the text format) that the content of the reference must consist only of alphanumeric characters, percent-encoded escapes, and characters in the following set (not including the outer backticks): `/-.~_!$&()*+,;=` . Despite our allowing percent encodings, implementations should not unescape them to prevent confusion with existing parsers. For example, `type.googleapis.com%2FFoo` should be rejected.

In the original design of `Any` , the possibility of launching a type resolution service at these type URLs was considered but Protobuf never implemented one and considers contacting these URLs to be problematic and a potential security issue. Do not attempt to contact type URLs.

`value`

`string ( bytes format)`

Holds a Protobuf serialization of the type described by type\_url.

A base64-encoded string.

### Status

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
  &quot;code&quot;: integer,
  &quot;message&quot;: string,
  &quot;details&quot;: [
    {
      &quot;@type&quot;: string,
      field1: ...,
      ...
    }
  ]
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`code`

`integer`

The status code, which should be an enum value of `google.rpc.Code` .

`message`

`string`

A developer-facing error message, which should be in English. Any user-facing error message should be localized and sent in the `google.rpc.Status.details` field, or localized by the client.

`details[]`

`object`

A list of messages that carry the error details. There is a common set of message types for APIs to use.

An object containing fields of an arbitrary type. An additional field `"@type"` contains a URI identifying the type. Example: `{ "id": 1234, "@type": "types.example.com/standard/id" }` .

### Tool Annotations

Destructive Hint: ❌ | Idempotent Hint: ❌ | Read Only Hint: ❌ | Open World Hint: ❌
