---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.reasoningEngines/create
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.reasoningEngines/create
title: 'Method: reasoningEngines.create'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.reasoningEngines.create

Creates a reasoning engine.

### Endpoint

post `https: / /{service-endpoint} /v1 /{parent} /reasoningEngines`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`parent` `string`

Required. The resource name of the Location to create the ReasoningEngine in. Format: `projects/{project}/locations/{location}`

### Request body

The request body contains an instance of `  ReasoningEngine  ` .

### Response body

If successful, the response body contains a newly created instance of `  Operation  ` .
