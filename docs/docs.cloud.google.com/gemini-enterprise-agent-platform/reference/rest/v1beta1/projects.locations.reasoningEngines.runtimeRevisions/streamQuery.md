---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.reasoningEngines.runtimeRevisions/streamQuery
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.reasoningEngines.runtimeRevisions/streamQuery
title: 'Method: runtimeRevisions.streamQuery'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.reasoningEngines.runtimeRevisions.streamQuery

Streams queries using a reasoning engine.

### Endpoint

post `https: / /{service-endpoint} /v1beta1 /{name}:streamQuery`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`name` `string`

Required. The name of the ReasoningEngine resource to use. Format: `projects/{project}/locations/{location}/reasoningEngines/{reasoningEngine}`

### Request body

The request body contains data with the following structure:

Fields

`input` ` object ( Struct  ` format)

Optional. Input content provided by users in JSON object format. Examples include text query, function calling parameters, media bytes, etc.

`classMethod` `string`

Optional. Class method to be used for the stream query. It is optional and defaults to "stream\_query" if unspecified.

### Response body

If successful, the response is a generic HTTP response whose format is defined by the method.
