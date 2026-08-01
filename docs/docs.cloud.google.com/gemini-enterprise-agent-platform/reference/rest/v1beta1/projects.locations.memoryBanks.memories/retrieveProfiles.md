---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.memoryBanks.memories/retrieveProfiles
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.memoryBanks.memories/retrieveProfiles
title: 'Method: memories.retrieveProfiles'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.memoryBanks.memories.retrieveProfiles

Retrieves profiles.

### Endpoint

post `https: / /{service-endpoint} /v1beta1 /{parent} /memories:retrieveProfiles`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`parent` `string`

Required. The resource name of the ReasoningEngine to retrieve profiles from. Format: `projects/{project}/locations/{location}/reasoningEngines/{reasoningEngine}`

### Request body

The request body contains data with the following structure:

Fields

`scope` `map (key: string, value: string)`

Required. The scope of the profiles to retrieve.

### Response body

If successful, the response body contains an instance of `  RetrieveProfilesResponse  ` .
