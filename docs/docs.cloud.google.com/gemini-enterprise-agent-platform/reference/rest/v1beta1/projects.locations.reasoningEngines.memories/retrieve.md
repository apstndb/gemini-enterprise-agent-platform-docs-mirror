---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.reasoningEngines.memories/retrieve
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.reasoningEngines.memories/retrieve
title: 'Method: memories.retrieve'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.reasoningEngines.memories.retrieve

Retrieve memories.

### Endpoint

post `https: / /{service-endpoint} /v1beta1 /{parent} /memories:retrieve`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`parent` `string`

Required. The resource name of the ReasoningEngine to retrieve memories from. Format: `projects/{project}/locations/{location}/reasoningEngines/{reasoningEngine}`

### Request body

The request body contains data with the following structure:

Fields

`scope` `map (key: string, value: string)`

Required. The scope of the memories to retrieve. A memory must have exactly the same scope ( `Memory.scope` ) as the scope provided here to be retrieved (same keys and values). Order does not matter, but it is case-sensitive.

`filter` `string`

Optional. The standard list filter that will be applied to the retrieved memories. More detail in [AIP-160](https://google.aip.dev/160) .

Supported fields: \* `fact` \* `createTime` \* `updateTime` \* `topics` (i.e. `topics.custom_memory_topic_label: "example topic" OR topics.managed_memory_topic: USER_PREFERENCES` )

`memoryTypes[]` ` enum ( MemoryType  ` )

Optional. Specifies the types of memories to retrieve. If this field is empty or not provided, the request will default to retrieving only memories of type `NATURAL_LANGUAGE_COLLECTION` . If populated, the request will retrieve memories matching any of the specified `MemoryType` values.

`retrieval_params` `Union type`

Parameters for retrieval. `retrieval_params` can be only one of the following:

`similaritySearchParams` ` object ( SimilaritySearchParams  ` )

Parameters for semantic similarity search based retrieval.

`simpleRetrievalParams` ` object ( SimpleRetrievalParams  ` )

Parameters for simple (non-similarity search) retrieval.

### Response body

Response message for `  MemoryBankService.RetrieveMemories  ` .

If successful, the response body contains data with the following structure:

Fields

`retrievedMemories[]` ` object ( RetrievedMemory  ` )

The retrieved memories.

`nextPageToken` `string`

A token that can be sent as `pageToken` to retrieve the next page. If this field is omitted, there are no subsequent pages. This token is not set if similarity search was used for retrieval.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;retrievedMemories&quot;: [{object (RetrievedMemory)}],&quot;nextPageToken&quot;: string}</code></pre></td>
</tr>
</tbody>
</table>

## SimilaritySearchParams

Parameters for semantic similarity search based retrieval.

Fields

`searchQuery` `string`

Required. Query to use for similarity search retrieval. If provided, then the parent ReasoningEngine must have `  ReasoningEngineContextSpec.MemoryBankConfig.SimilaritySearchConfig  ` set.

`topK` `integer`

Optional. The maximum number of memories to return. The service may return fewer than this value. If unspecified, at most 3 memories will be returned. The maximum value is 100; values above 100 will be coerced to 100.

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
  &quot;searchQuery&quot;: string,
  &quot;topK&quot;: integer
}</code></pre></td>
</tr>
</tbody>
</table>

## SimpleRetrievalParams

Parameters for simple (non-similarity search) retrieval.

Fields

`pageSize` `integer`

Optional. The maximum number of memories to return. The service may return fewer than this value. If unspecified, at most 3 memories will be returned. The maximum value is 100; values above 100 will be coerced to 100.

`pageToken` `string`

Optional. A page token, received from a previous `memories.retrieve` call. Provide this to retrieve the subsequent page.

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
  &quot;pageSize&quot;: integer,
  &quot;pageToken&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

## RetrievedMemory

A retrieved memory.

Fields

`memory` ` object ( Memory  ` )

The retrieved Memory.

`distance` `number`

The distance between the query and the retrieved Memory. Smaller values indicate more similar memories. This is only set if similarity search was used for retrieval.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;memory&quot;: {object (Memory)},&quot;distance&quot;: number}</code></pre></td>
</tr>
</tbody>
</table>
