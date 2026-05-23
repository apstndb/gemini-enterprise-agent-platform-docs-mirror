---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.models.evaluations
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.models.evaluations
title: 'REST Resource: projects.locations.models.evaluations'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

## Resource: ModelEvaluation

A collection of metrics calculated by comparing Model's predictions on all of the test data against annotations from the test data.

Fields

`name` `string`

Output only. The resource name of the ModelEvaluation.

`displayName` `string`

The display name of the ModelEvaluation.

`metricsSchemaUri` `string`

Points to a YAML file stored on Google Cloud Storage describing the `  metrics  ` of this ModelEvaluation. The schema is defined as an OpenAPI 3.0.2 [Schema Object](https://github.com/OAI/OpenAPI-Specification/blob/main/versions/3.0.2.md#schemaObject) .

`metrics` ` value ( Value  ` format)

Evaluation metrics of the Model. The schema of the metrics is stored in `  metricsSchemaUri  `

`createTime` ` string ( Timestamp  ` format)

Output only. timestamp when this ModelEvaluation was created.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`sliceDimensions[]` `string`

All possible `  dimensions  ` of ModelEvaluationSlices. The dimensions can be used as the filter of the `  ModelService.ListModelEvaluationSlices  ` request, in the form of `slice.dimension = <dimension>` .

`dataItemSchemaUri` `string`

Points to a YAML file stored on Google Cloud Storage describing \[EvaluatedDataItemView.data\_item\_payload\]\[\] and `  EvaluatedAnnotation.data_item_payload  ` . The schema is defined as an OpenAPI 3.0.2 [Schema Object](https://github.com/OAI/OpenAPI-Specification/blob/main/versions/3.0.2.md#schemaObject) .

This field is not populated if there are neither EvaluatedDataItemViews nor EvaluatedAnnotations under this ModelEvaluation.

`annotationSchemaUri` `string`

Points to a YAML file stored on Google Cloud Storage describing \[EvaluatedDataItemView.predictions\]\[\], \[EvaluatedDataItemView.ground\_truths\]\[\], `  EvaluatedAnnotation.predictions  ` , and `  EvaluatedAnnotation.ground_truths  ` . The schema is defined as an OpenAPI 3.0.2 [Schema Object](https://github.com/OAI/OpenAPI-Specification/blob/main/versions/3.0.2.md#schemaObject) .

This field is not populated if there are neither EvaluatedDataItemViews nor EvaluatedAnnotations under this ModelEvaluation.

`modelExplanation` ` object ( ModelExplanation  ` )

Aggregated explanation metrics for the Model's prediction output over the data this ModelEvaluation uses. This field is populated only if the Model is evaluated with explanations, and only for AutoML tabular Models.

`explanationSpecs[]` ` object ( ModelEvaluationExplanationSpec  ` )

Describes the values of `  ExplanationSpec  ` that are used for explaining the predicted values on the evaluated data.

`metadata` ` value ( Value  ` format)

The metadata of the ModelEvaluation. For the ModelEvaluation uploaded from Managed Pipeline, metadata contains a structured value with keys of "pipelineJobId", "evaluation\_dataset\_type", "evaluation\_dataset\_path", "row\_based\_metrics\_path".

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;name&quot;: string,&quot;displayName&quot;: string,&quot;metricsSchemaUri&quot;: string,&quot;metrics&quot;: value,&quot;createTime&quot;: string,&quot;sliceDimensions&quot;: [string],&quot;dataItemSchemaUri&quot;: string,&quot;annotationSchemaUri&quot;: string,&quot;modelExplanation&quot;: {object (ModelExplanation)},&quot;explanationSpecs&quot;: [{object (ModelEvaluationExplanationSpec)}],&quot;metadata&quot;: value}</code></pre></td>
</tr>
</tbody>
</table>

## ModelEvaluationExplanationSpec

Fields

`explanationType` `string`

Explanation type.

For AutoML Image Classification models, possible values are:

  - `image-integrated-gradients`
  - `image-xrai`

`explanationSpec` ` object ( ExplanationSpec  ` )

Explanation spec details.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;explanationType&quot;: string,&quot;explanationSpec&quot;: {object (ExplanationSpec)}}</code></pre></td>
</tr>
</tbody>
</table>

## Methods

### `            get           `

Gets a ModelEvaluation.

### `            import           `

Imports an externally generated ModelEvaluation.

### `            list           `

Lists ModelEvaluations in a Model.
