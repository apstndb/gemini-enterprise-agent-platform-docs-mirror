---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/PredictSchemata
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/PredictSchemata
title: PredictSchemata
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Contains the schemata used in Model's predictions and explanations via `  PredictionService.Predict  ` , `  PredictionService.Explain  ` and `  BatchPredictionJob  ` .

Fields

`instanceSchemaUri` `string`

Immutable. Points to a YAML file stored on Google Cloud Storage describing the format of a single instance, which are used in `  PredictRequest.instances  ` , `  ExplainRequest.instances  ` and `  BatchPredictionJob.input_config  ` . The schema is defined as an OpenAPI 3.0.2 [Schema Object](https://github.com/OAI/OpenAPI-Specification/blob/main/versions/3.0.2.md#schemaObject) . AutoML Models always have this field populated by Agent Platform. Note: The URI given on output will be immutable and probably different, including the URI scheme, than the one given on input. The output URI will point to a location where the user only has a read access.

`parametersSchemaUri` `string`

Immutable. Points to a YAML file stored on Google Cloud Storage describing the parameters of prediction and explanation via `  PredictRequest.parameters  ` , `  ExplainRequest.parameters  ` and `  BatchPredictionJob.model_parameters  ` . The schema is defined as an OpenAPI 3.0.2 [Schema Object](https://github.com/OAI/OpenAPI-Specification/blob/main/versions/3.0.2.md#schemaObject) . AutoML Models always have this field populated by Agent Platform, if no parameters are supported, then it is set to an empty string. Note: The URI given on output will be immutable and probably different, including the URI scheme, than the one given on input. The output URI will point to a location where the user only has a read access.

`predictionSchemaUri` `string`

Immutable. Points to a YAML file stored on Google Cloud Storage describing the format of a single prediction produced by this Model, which are returned via `  PredictResponse.predictions  ` , `  ExplainResponse.explanations  ` , and `  BatchPredictionJob.output_config  ` . The schema is defined as an OpenAPI 3.0.2 [Schema Object](https://github.com/OAI/OpenAPI-Specification/blob/main/versions/3.0.2.md#schemaObject) . AutoML Models always have this field populated by Agent Platform. Note: The URI given on output will be immutable and probably different, including the URI scheme, than the one given on input. The output URI will point to a location where the user only has a read access.

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
  &quot;instanceSchemaUri&quot;: string,
  &quot;parametersSchemaUri&quot;: string,
  &quot;predictionSchemaUri&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>
