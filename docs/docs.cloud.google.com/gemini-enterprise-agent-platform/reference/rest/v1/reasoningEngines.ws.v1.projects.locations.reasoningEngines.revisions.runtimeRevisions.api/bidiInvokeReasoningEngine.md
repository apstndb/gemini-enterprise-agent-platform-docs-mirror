---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/reasoningEngines.ws.v1.projects.locations.reasoningEngines.revisions.runtimeRevisions.api/bidiInvokeReasoningEngine
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/reasoningEngines.ws.v1.projects.locations.reasoningEngines.revisions.runtimeRevisions.api/bidiInvokeReasoningEngine
title: 'Method: api.bidiInvokeReasoningEngine'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : reasoningEngines.ws.v1.projects.locations.reasoningEngines.revisions.runtimeRevisions.api.bidiInvokeReasoningEngine

Invokes reasoning engine with arbitrary WebSocket requests for bidi streaming

### Endpoint

post `https: / /{service-endpoint} /reasoningEngines /ws /v1 /{name} /api /**`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`name` `string`

Optional. The name of the ReasoningEngine. Format: `projects/{project}/locations/{location}/reasoningEngines/{reasoningEngine}` or `projects/{project}/locations/{location}/reasoningEngines/{reasoningEngine}/runtimeRevisions/{runtime_revision}`

### Request body

The request body contains an instance of `  HttpBody  ` .

### Response body

If successful, the response is a generic HTTP response whose format is defined by the method.
