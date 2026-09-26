---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.interactionsHttp/get
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.interactionsHttp/get
title: 'Method: interactionsHttp.get'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.interactionsHttp.get

Retrieves the full details of a single interaction based on its `Interaction.id` .

### Endpoint

get `https: / /{service-endpoint} /v1beta1 /{name}`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`name` `string`

Required. The name of the interaction to retrieve. Format: interactions/{interaction}

### Query parameters

`stream` `boolean`

If true, streams the interaction events as Server-Sent events.

`lastEventId` `string`

If set, resumes the interaction stream from the chunk after the event marked by the event id. Can only be used if `stream` is true.

` includeInput (deprecated)  ` `boolean`

If true, includes the input in the response.

### Request body

The request body must be empty.

### Response body

If successful, the response is a generic HTTP response whose format is defined by the method.
