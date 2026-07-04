---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.memoryBanks.memories/retrieve
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.memoryBanks.memories/retrieve
title: 'Method: memories.retrieve'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.memoryBanks.memories.retrieve

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

If successful, the response body contains an instance of `  RetrieveMemoriesResponse  ` .
