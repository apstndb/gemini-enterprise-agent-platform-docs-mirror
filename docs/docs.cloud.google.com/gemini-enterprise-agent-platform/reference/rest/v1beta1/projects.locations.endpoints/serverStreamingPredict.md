---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.endpoints/serverStreamingPredict
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.endpoints/serverStreamingPredict
title: 'Method: endpoints.serverStreamingPredict'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.endpoints.serverStreamingPredict

Perform a server-side streaming online prediction request for Vertex LLM streaming.

### Endpoint

post `https: / /{service-endpoint} /v1beta1 /{endpoint}:serverStreamingPredict`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`endpoint` `string`

Required. The name of the Endpoint requested to serve the prediction. Format: `projects/{project}/locations/{location}/endpoints/{endpoint}`

### Request body

The request body contains data with the following structure:

Fields

`inputs[]` ` object ( Tensor  ` )

The prediction input.

`parameters` ` object ( Tensor  ` )

The parameters that govern the prediction.

### Response body

If successful, the response body contains a stream of `  StreamingPredictResponse  ` instances.
