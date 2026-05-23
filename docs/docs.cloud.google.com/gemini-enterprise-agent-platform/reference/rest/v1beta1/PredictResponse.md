---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/PredictResponse
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/PredictResponse
title: PredictResponse
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Response message for `  PredictionService.Predict  ` .

Fields

`predictions[]` ` value ( Value  ` format)

The predictions that are the output of the predictions call. The schema of each prediction depends on the type of request.

  - For a generative AI request to a Text Embedding model, see `TextEmbeddingPredictionResult`
  - For a generative AI request to a Multimodal Embedding model, see `VisionEmbeddingModelResult`
  - For a video generation request to a Veo model, see `VideoGenerationModelResult`
  - For a traditional machine learning request to a deployed custom model, the schema of each prediction is defined by the model's `  predictionSchemaUri  ` .

`deployedModelId` `string`

id of the Endpoint's DeployedModel that served this prediction.

`model` `string`

Output only. The resource name of the Model which is deployed as the DeployedModel that this prediction hits.

`modelVersionId` `string`

Output only. The version id of the Model which is deployed as the DeployedModel that this prediction hits.

`modelDisplayName` `string`

Output only. The `  display name  ` of the Model which is deployed as the DeployedModel that this prediction hits.

`metadata` ` value ( Value  ` format)

Output only. Request-level metadata returned by the model. The metadata type will be dependent upon the model implementation.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;predictions&quot;: [
    value
  ],
  &quot;deployedModelId&quot;: string,
  &quot;model&quot;: string,
  &quot;modelVersionId&quot;: string,
  &quot;modelDisplayName&quot;: string,
  &quot;metadata&quot;: value
}</code></pre></td>
</tr>
</tbody>
</table>
