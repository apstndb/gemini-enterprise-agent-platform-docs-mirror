---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.reasoningEngines.memories/create
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.reasoningEngines.memories/create
title: 'Method: memories.create'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.reasoningEngines.memories.create

Create a Memory.

### Endpoint

post `https: / /{service-endpoint} /v1beta1 /{parent} /memories`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`parent` `string`

Required. The resource name of the ReasoningEngine to create the Memory under. Format: `projects/{project}/locations/{location}/reasoningEngines/{reasoningEngine}`

### Query parameters

`memoryId` `string`

Optional. The user defined id to use for memory, which will become the final component of the memory resource name. If not provided, Agent Platform will generate a value for this id.

This value may be up to 63 characters, and valid characters are `[a-z0-9-]` . The first character must be a letter, and the last character must be a letter or number.

### Request body

The request body contains an instance of `  Memory  ` .

### Response body

If successful, the response body contains a newly created instance of `  Operation  ` .
