---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.models.evaluations.slices
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.models.evaluations.slices
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

## SliceSpec

Specification for how the data should be sliced.

Fields

`configs` ` map (key: string, value: object ( SliceConfig  ` ))

Mapping configuration for this SliceSpec. The key is the name of the feature. By default, the key will be prefixed by "instance" as a dictionary prefix for Vertex Batch Predictions output format.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;configs&quot;: {string: {object (SliceConfig)},...}}</code></pre></td>
</tr>
</tbody>
</table>

## SliceConfig

Specification message containing the config for this SliceSpec. When `kind` is selected as `value` and/or `range` , only a single slice will be computed. When `allValues` is present, a separate slice will be computed for each possible label/value for the corresponding key in `config` . Examples, with feature zip\_code with values 12345, 23334, 88888 and feature country with values "US", "Canada", "Mexico" in the dataset:

Example 1:

    {
      "zip_code": { "value": { "floatValue": 12345.0 } }
    }

A single slice for any data with zip\_code 12345 in the dataset.

Example 2:

    {
      "zip_code": { "range": { "low": 12345, "high": 20000 } }
    }

A single slice containing data where the zip\_codes between 12345 and 20000 For this example, data with the zip\_code of 12345 will be in this slice.

Example 3:

    {
      "zip_code": { "range": { "low": 10000, "high": 20000 } },
      "country": { "value": { "stringValue": "US" } }
    }

A single slice containing data where the zip\_codes between 10000 and 20000 has the country "US". For this example, data with the zip\_code of 12345 and country "US" will be in this slice.

Example 4:

    { "country": {"allValues": { "value": true } } }

Three slices are computed, one for each unique country in the dataset.

Example 5:

    {
      "country": { "allValues": { "value": true } },
      "zip_code": { "value": { "floatValue": 12345.0 } }
    }

Three slices are computed, one for each unique country in the dataset where the zip\_code is also 12345. For this example, data with zip\_code 12345 and country "US" will be in one slice, zip\_code 12345 and country "Canada" in another slice, and zip\_code 12345 and country "Mexico" in another slice, totaling 3 slices.

Fields

`kind` `Union type`

`kind` can be only one of the following:

`value` ` object ( Value  ` )

A unique specific value for a given feature. Example: `{ "value": { "stringValue": "12345" } }`

`range` ` object ( Range  ` )

A range of values for a numerical feature. Example: `{"range":{"low":10000.0,"high":50000.0}}` will capture 12345 and 23334 in the slice.

`allValues` `boolean`

If allValues is set to true, then all possible labels of the keyed feature will have another slice computed. Example: `{"allValues":{"value":true}}`

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{// kind&quot;value&quot;: {object (Value)},&quot;range&quot;: {object (Range)},&quot;allValues&quot;: boolean// Union type}</code></pre></td>
</tr>
</tbody>
</table>

## Value

Single value that supports strings and floats.

Fields

`kind` `Union type`

`kind` can be only one of the following:

`stringValue` `string`

String type.

`floatValue` `number`

Float type.

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

  // kind
  &quot;stringValue&quot;: string,
  &quot;floatValue&quot;: number
  // Union type
}</code></pre></td>
</tr>
</tbody>
</table>

## Range

A range of values for slice(s). `low` is inclusive, `high` is exclusive.

Fields

`low` `number`

Inclusive low value for the range.

`high` `number`

Exclusive high value for the range.

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
  &quot;low&quot;: number,
  &quot;high&quot;: number
}</code></pre></td>
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
