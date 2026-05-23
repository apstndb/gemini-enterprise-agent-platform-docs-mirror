---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.endpoints/computeTokens
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.endpoints/computeTokens
title: 'Method: endpoints.computeTokens'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.endpoints.computeTokens

Return a list of tokens based on the input text.

### Endpoint

post `https: / /{service-endpoint} /v1 /{endpoint}:computeTokens`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`endpoint` `string`

Required. The name of the Endpoint requested to get lists of tokens and token ids.

### Request body

The request body contains data with the following structure:

Fields

`instances[]` ` value ( Value  ` format)

Optional. The instances that are the input to token computing API call. Schema is identical to the prediction schema of the text model, even for the non-text models, like chat models, or Codey models.

`model` `string`

Optional. The name of the publisher model requested to serve the prediction. Format: projects/{project}/locations/{location}/publishers/\*/models/\*

`contents[]` ` object ( Content  ` )

Optional. Input content.

### Response body

If successful, the response body contains an instance of `  ComputeTokensResponse  ` .
