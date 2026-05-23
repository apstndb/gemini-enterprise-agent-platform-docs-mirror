---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.publishers.models/streamRawPredict
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.publishers.models/streamRawPredict
title: 'Method: models.streamRawPredict'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.publishers.models.streamRawPredict

Perform a streaming online prediction with an arbitrary HTTP payload.

### Endpoint

post `https: / /{service-endpoint} /v1beta1 /{endpoint}:streamRawPredict`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`endpoint` `string`

Required. The name of the Endpoint requested to serve the prediction. Format: `projects/{project}/locations/{location}/endpoints/{endpoint}` or `projects/{project}/locations/{location}/publishers/{publisher}/models/{model}`

### Request body

The request body contains data with the following structure:

Fields

`httpBody` ` object ( HttpBody  ` )

The prediction input. Supports HTTP headers and arbitrary data payload.

### Response body

If successful, the response is a generic HTTP response whose format is defined by the method.
