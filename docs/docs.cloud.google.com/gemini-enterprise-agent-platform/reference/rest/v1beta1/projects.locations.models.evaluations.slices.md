---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.models.evaluations.slices
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.models.evaluations.slices
title: 'REST Resource: projects.locations.models.evaluations.slices'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

## Resource: ModelEvaluationSlice

A collection of metrics calculated by comparing Model's predictions on a slice of the test data against ground truth annotations.

Fields

`name` `string`

Output only. The resource name of the ModelEvaluationSlice.

`slice` ` object ( Slice  ` )

Output only. The slice of the test data that is used to evaluate the Model.

`metricsSchemaUri` `string`

Output only. Points to a YAML file stored on Google Cloud Storage describing the `  metrics  ` of this ModelEvaluationSlice. The schema is defined as an OpenAPI 3.0.2 [Schema Object](https://github.com/OAI/OpenAPI-Specification/blob/main/versions/3.0.2.md#schemaObject) .

`metrics` ` value ( Value  ` format)

Output only. Sliced evaluation metrics of the Model. The schema of the metrics is stored in `  metricsSchemaUri  `

`createTime` ` string ( Timestamp  ` format)

Output only. timestamp when this ModelEvaluationSlice was created.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`modelExplanation` ` object ( ModelExplanation  ` )

Output only. Aggregated explanation metrics for the Model's prediction output over the data this ModelEvaluation uses. This field is populated only if the Model is evaluated with explanations, and only for tabular Models.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;name&quot;: string,&quot;slice&quot;: {object (Slice)},&quot;metricsSchemaUri&quot;: string,&quot;metrics&quot;: value,&quot;createTime&quot;: string,&quot;modelExplanation&quot;: {object (ModelExplanation)}}</code></pre></td>
</tr>
</tbody>
</table>

## Slice

Definition of a slice.

Fields

`dimension` `string`

Output only. The dimension of the slice. Well-known dimensions are: \* `annotationSpec` : This slice is on the test data that has either ground truth or prediction with `  AnnotationSpec.display_name  ` equals to `  value  ` . \* `slice` : This slice is a user customized slice defined by its SliceSpec.

`value` `string`

Output only. The value of the dimension in this slice.

`sliceSpec` ` object ( SliceSpec  ` )

Output only. Specification for how the data was sliced.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;dimension&quot;: string,&quot;value&quot;: string,&quot;sliceSpec&quot;: {object (SliceSpec)}}</code></pre></td>
</tr>
</tbody>
</table>

## Methods

### `            batchImport           `

Imports a list of externally generated EvaluatedAnnotations.

### `            get           `

Gets a ModelEvaluationSlice.

### `            list           `

Lists ModelEvaluationSlices in a ModelEvaluation.
