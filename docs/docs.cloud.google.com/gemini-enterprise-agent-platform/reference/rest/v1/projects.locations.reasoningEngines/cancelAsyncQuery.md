---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.reasoningEngines/cancelAsyncQuery
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.reasoningEngines/cancelAsyncQuery
title: 'Method: reasoningEngines.cancelAsyncQuery'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.reasoningEngines.cancelAsyncQuery

Cancels an reasoningEngines.asyncQuery operation.

### Endpoint

post `https: / /{service-endpoint} /v1 /{name}:cancelAsyncQuery`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`name` `string`

Required. The name of the ReasoningEngine resource to use. Format: `projects/{project}/locations/{location}/reasoningEngines/{reasoningEngine}`

### Request body

The request body contains data with the following structure:

Fields

`operationName` `string`

Required. The name of the longrunning operation returned from reasoningEngines.asyncQuery. Format: `projects/{project}/locations/{location}/operations/{operation}`

### Response body

If successful, the response body is empty.
