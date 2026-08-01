---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/interactions/getPoll
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/interactions/getPoll
title: 'Method: interactions.getPoll'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : interactions.getPoll

Fully typed proto, unary version of interactions.getPoll that returns Interaction proto.

### Endpoint

get `https: / /{service-endpoint} /v1beta1 /{name}:poll`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`name` `string`

Required. The name of the interaction to retrieve. Format: interactions/{interaction}

### Query parameters

`stream` `boolean`

Optional. If true, streams the interaction events as Server-Sent events.

`lastEventId` `string`

Optional. If set, resumes the interaction stream from the chunk after the event marked by the event id. Can only be used if `stream` is true.

` includeInput (deprecated)  ` `boolean`

Optional. If true, includes the input in the response.

### Request body

The request body must be empty.

### Response body

If successful, the response body contains an instance of `  Interaction  ` .
