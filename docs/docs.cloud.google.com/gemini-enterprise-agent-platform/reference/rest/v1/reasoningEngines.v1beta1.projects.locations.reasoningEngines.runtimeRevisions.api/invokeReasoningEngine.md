---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/reasoningEngines.v1beta1.projects.locations.reasoningEngines.runtimeRevisions.api/invokeReasoningEngine
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/reasoningEngines.v1beta1.projects.locations.reasoningEngines.runtimeRevisions.api/invokeReasoningEngine
title: 'Method: api.invokeReasoningEngine'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : reasoningEngines.v1beta1.projects.locations.reasoningEngines.runtimeRevisions.api.invokeReasoningEngine

Invokes reasoning engine with arbitrary HTTP requests for both unary and server-side streaming cases.

### Endpoint

patch `https: / /{service-endpoint} /reasoningEngines /v1beta1 /{name} /api /**`  

`PATCH https://{service-endpoint}/reasoningEngines/v1beta1/{name}/api/**`

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`name` `string`

Required. The name of the ReasoningEngine resource to use. Format: `projects/{project}/locations/{location}/reasoningEngines/{reasoningEngine}` or `projects/{project}/locations/{location}/reasoningEngines/{reasoningEngine}/runtimeRevisions/{runtime_revision}`

### Request body

The request body contains an instance of `  HttpBody  ` .

### Response body

If successful, the response is a generic HTTP response whose format is defined by the method.
