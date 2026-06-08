---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.reasoningEngines.sessions/appendEvent
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.reasoningEngines.sessions/appendEvent
title: 'Method: sessions.appendEvent'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.reasoningEngines.sessions.appendEvent

Appends an event to a given session.

### Endpoint

post `https: / /{service-endpoint} /v1 /{name}:appendEvent`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`name` `string`

Required. The resource name of the session to append event to. Format: `projects/{project}/locations/{location}/reasoningEngines/{reasoningEngine}/sessions/{session}`

### Request body

The request body contains an instance of `  SessionEvent  ` .

### Response body

If successful, the response body is empty.
