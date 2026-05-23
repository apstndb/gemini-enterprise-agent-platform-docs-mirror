---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.endpoints.chat/completions
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.endpoints.chat/completions
title: 'Method: chat.completions'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.endpoints.chat.completions

Exposes an OpenAI-compatible endpoint for chat completions.

### Endpoint

post `https: / /{service-endpoint} /v1beta1 /{endpoint} /chat /completions`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`endpoint` `string`

Required. The name of the endpoint requested to serve the prediction. Format: `projects/{project}/locations/{location}/endpoints/{endpoint}`

### Request body

The request body contains an instance of `  HttpBody  ` .

### Response body

If successful, the response is a generic HTTP response whose format is defined by the method.
