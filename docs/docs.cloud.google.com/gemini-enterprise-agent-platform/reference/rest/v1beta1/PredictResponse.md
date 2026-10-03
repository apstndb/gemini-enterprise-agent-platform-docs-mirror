---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/PredictResponse
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/PredictResponse
title: PredictResponse
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Response message for [`PredictionService.Predict`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.endpoints/predict#google.cloud.aiplatform.v1beta1.PredictionService.Predict) .

Fields

`predictions[]` `value ( `[`Value`](https://protobuf.dev/reference/protobuf/google.protobuf/#value)` format)`

The predictions that are the output of the predictions call. The schema of each prediction depends on the type of request.

- For a generative AI request to a Text Embedding model, see `TextEmbeddingPredictionResult`
- For a generative AI request to a Multimodal Embedding model, see `VisionEmbeddingModelResult`
- For a video generation request to a Veo model, see `VideoGenerationModelResult`
- For a traditional machine learning request to a deployed custom model, the schema of each prediction is defined by the model's [`predictionSchemaUri`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/PredictSchemata#FIELDS.prediction_schema_uri) .

`deployedModelId` `string`

id of the Endpoint's DeployedModel that served this prediction.

`model` `string`

Output only. The resource name of the Model which is deployed as the DeployedModel that this prediction hits.

`modelVersionId` `string`

Output only. The version id of the Model which is deployed as the DeployedModel that this prediction hits.

`modelDisplayName` `string`

Output only. The [`display name`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.models#Model.FIELDS.display_name) of the Model which is deployed as the DeployedModel that this prediction hits.

`metadata` `value ( `[`Value`](https://protobuf.dev/reference/protobuf/google.protobuf/#value)` format)`

Output only. Request-level metadata returned by the model. The metadata type will be dependent upon the model implementation.

**JSON representation**

```
{
  "predictions": [
    value
  ],
  "deployedModelId": string,
  "model": string,
  "modelVersionId": string,
  "modelDisplayName": string,
  "metadata": value
}
```
