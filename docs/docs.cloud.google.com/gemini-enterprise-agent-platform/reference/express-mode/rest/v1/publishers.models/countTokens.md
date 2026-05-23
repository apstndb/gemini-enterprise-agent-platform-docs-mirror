---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/express-mode/rest/v1/publishers.models/countTokens
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/express-mode/rest/v1/publishers.models/countTokens
title: 'Method: publishers.models.countTokens'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Perform a token count in express mode.

### Endpoint

post `https: / /aiplatform.googleapis.com /v1 /{model}:countTokens`

### Path parameters

`model` `string`

Required. The name of the model requested to perform token counting. Format: `/publishers/google/models/*`

### Request body

The request body contains data with the following structure:

Fields

`model` `string`

Optional. The name of the publisher model requested to serve the prediction. Format: `publishers/*/models/*`

`instances[]` ` value ( Value  ` format)

Optional. The instances that are the input to token counting call. Schema is identical to the prediction schema of the underlying model.

`contents[]` ` object ( Content  ` )

Optional. Input content.

`tools[]` ` object ( Tool  ` )

Optional. A list of `Tools` the model may use to generate the next response.

A `Tool` is a piece of code that enables the system to interact with external systems to perform an action, or set of actions, outside of knowledge and scope of the model.

`systemInstruction` ` object ( Content  ` )

Optional. The user provided system instructions for the model. Note: only text should be used in parts and content in each part will be in a separate paragraph.

`generationConfig` ` object ( GenerationConfig  ` )

Optional. Generation config that the model will use to generate the response.

### Response body

If successful, the response body contains an instance of `  CountTokensResponse  ` .
