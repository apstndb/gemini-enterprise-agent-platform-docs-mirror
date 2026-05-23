---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.endpoints/predict
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.endpoints/predict
title: 'Method: endpoints.predict'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.endpoints.predict

Perform an online inference. Use this method to run inference on Google's generative AI models as well as custom models deployed to Gemini Enterprise Agent Platform. This method supports both generative AI tasks (such as image generation, virtual try-on, text generation, and multimodal embeddings) and traditional machine learning tasks (such as classification and regression).

To run inference on a base (non-tuned) Gemini model, see `  endpoints.generateContent  ` .

### Endpoint

post `https: / /{service-endpoint} /v1beta1 /{endpoint}:predict`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`endpoint` `string`

Required. The resource name of the publisher model or endpoint requested to serve the prediction. For Google models like Embedding or Veo, use the publisher model format. For tuned models or other models deployed to an Agent Platform endpoint, use the endpoint format.

  - Publisher model format: `projects/{project}/locations/{location}/publishers/google/models/{model}`
  - Endpoint format: `projects/{project}/locations/{location}/endpoints/{endpoint}`

### Request body

The request body contains data with the following structure:

Fields

`instances[]` ` value ( Value  ` format)

Required. The instances that are the input to the prediction call. A DeployedModel may have an upper limit on the number of instances it supports per request, and when it is exceeded the prediction call errors in case of AutoML Models, or, in case of customer created Models, the behavior is as documented by that Model. The schema of each instance depends on the type of request.

  - For a generative AI request to a Text Embedding model, see `TextEmbeddingPredictionInstance`
  - For a generative AI request to a Multimodal Embedding model, see `VisionEmbeddingModelInstance`
  - For a video generation request to a Veo model, see `VideoGenerationModelInstance`
  - For a traditional machine learning request to a deployed custom model, the schema of any single instance is defined by the model's `  instanceSchemaUri  ` .

`parameters` ` value ( Value  ` format)

The parameters that govern the prediction. The schema of the parameters depends on the type of request.

  - For a generative AI request to a Text Embedding model, see `TextEmbeddingPredictionParams`
  - For a generative AI request to a Multimodal Embedding model, see `VisionEmbeddingModelParams`
  - For a video generation request to a Veo model, see `VideoGenerationModelParams`
  - For a traditional machine learning request to a deployed custom model, the schema of the parameters is defined by the model's `  parametersSchemaUri  ` .

`labels` `map (key: string, value: string)`

Optional. The user labels for Imagen billing usage only. Only Imagen supports labels. For other use cases, it will be ignored.

### Response body

If successful, the response body contains an instance of `  PredictResponse  ` .
