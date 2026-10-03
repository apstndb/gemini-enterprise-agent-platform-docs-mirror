---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.endpoints/directPredict
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.endpoints/directPredict
title: 'Method: endpoints.directPredict'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.endpoints.directPredict

Perform an unary online prediction request to a gRPC model server for Vertex first-party products and frameworks.

### Endpoint

post `https: / /{service-endpoint} /v1beta1 /{endpoint}:directPredict`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`endpoint` `string`

Required. The name of the Endpoint requested to serve the prediction. Format: `projects/{project}/locations/{location}/endpoints/{endpoint}`

### Request body

The request body contains data with the following structure:

Fields

`inputs[]` `object ( `[`Tensor`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/Tensor)` )`

The prediction input.

`parameters` `object ( `[`Tensor`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/Tensor)` )`

The parameters that govern the prediction.

### Response body

Response message for [`PredictionService.DirectPredict`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.endpoints/directPredict#google.cloud.aiplatform.v1beta1.PredictionService.DirectPredict) .

If successful, the response body contains data with the following structure:

Fields

`outputs[]` `object ( `[`Tensor`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/Tensor)` )`

The prediction output.

`parameters` `object ( `[`Tensor`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/Tensor)` )`

The parameters that govern the prediction.

**JSON representation**

```
{
  "outputs": [
    {
      object (Tensor)
    }
  ],
  "parameters": {
    object (Tensor)
  }
}
```
