---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.reasoningEngines/asyncQuery
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.reasoningEngines/asyncQuery
title: 'Method: reasoningEngines.asyncQuery'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.reasoningEngines.asyncQuery

Async query using a reasoning engine.

### Endpoint

post `https: / /{service-endpoint} /v1 /{name}:asyncQuery`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`name` `string`

Required. The name of the ReasoningEngine resource to use. Format: `projects/{project}/locations/{location}/reasoningEngines/{reasoningEngine}`

### Request body

The request body contains data with the following structure:

Fields

`inputGcsUri` `string`

Optional. Input Cloud Storage URI for the Async query. If you are not bringing your own container (BYOC), the content of the file should be a JSON object with an `input` field matching the `input` field of `QueryReasoningEngineRequest` (e.g. `{ "input": { "userId": "hello", "message":"$QUERY"} }` ). For BYOC, the content of the file depends on the the agent application.

`outputGcsUri` `string`

Optional. Output Cloud Storage URI for the Async query. This contains the final response of the query.

### Response body

If successful, the response body contains an instance of `  Operation  ` .
