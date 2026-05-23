---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/ModelExplanation
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/ModelExplanation
title: ModelExplanation
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Aggregated explanation metrics for a Model over a set of instances.

Fields

`meanAttributions[]` ` object ( Attribution  ` )

Output only. Aggregated attributions explaining the Model's prediction outputs over the set of instances. The attributions are grouped by outputs.

For Models that predict only one output, such as regression Models that predict only one score, there is only one attibution that explains the predicted output. For Models that predict multiple outputs, such as multiclass Models that predict multiple classes, each element explains one specific item. `  Attribution.output_index  ` can be used to identify which output this attribution is explaining.

The `  baselineOutputValue  ` , `  instanceOutputValue  ` and `  featureAttributions  ` fields are averaged over the test data.

NOTE: Currently AutoML tabular classification Models produce only one attribution, which averages attributions over all the classes it predicts. `  Attribution.approximation_error  ` is not populated.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;meanAttributions&quot;: [{object (Attribution)}]}</code></pre></td>
</tr>
</tbody>
</table>

## Attribution

Attribution that explains a particular prediction output.

Fields

`baselineOutputValue` `number`

Output only. Model predicted output if the input instance is constructed from the baselines of all the features defined in `  ExplanationMetadata.inputs  ` . The field name of the output is determined by the key in `  ExplanationMetadata.outputs  ` .

If the Model's predicted output has multiple dimensions (rank \> 1), this is the value in the output located by `  outputIndex  ` .

If there are multiple baselines, their output values are averaged.

`instanceOutputValue` `number`

Output only. Model predicted output on the corresponding \[explanation instance\]\[ExplainRequest.instances\]. The field name of the output is determined by the key in `  ExplanationMetadata.outputs  ` .

If the Model predicted output has multiple dimensions, this is the value in the output located by `  outputIndex  ` .

`featureAttributions` ` value ( Value  ` format)

Output only. Attributions of each explained feature. Features are extracted from the `  prediction instances  ` according to `  explanation metadata for inputs  ` .

The value is a struct, whose keys are the name of the feature. The values are how much the feature in the `  instance  ` contributed to the predicted result.

The format of the value is determined by the feature's input format:

  - If the feature is a scalar value, the attribution value is a `  floating number  ` .

  - If the feature is an array of scalar values, the attribution value is an `  array  ` .

  - If the feature is a struct, the attribution value is a `  struct  ` . The keys in the attribution value struct are the same as the keys in the feature struct. The formats of the values in the attribution struct are determined by the formats of the values in the feature struct.

The `  ExplanationMetadata.feature_attributions_schema_uri  ` field, pointed to by the `  ExplanationSpec  ` field of the `  Endpoint.deployed_models  ` object, points to the schema file that describes the features and their attribution values (if it is populated).

`outputIndex[]` `integer`

Output only. The index that locates the explained prediction output.

If the prediction output is a scalar value, outputIndex is not populated. If the prediction output has multiple dimensions, the length of the outputIndex list is the same as the number of dimensions of the output. The i-th element in outputIndex is the element index of the i-th dimension of the output vector. Indices start from 0.

`outputDisplayName` `string`

Output only. The display name of the output identified by `  outputIndex  ` . For example, the predicted class name by a multi-classification Model.

This field is only populated iff the Model predicts display names as a separate field along with the explained output. The predicted display name must has the same shape of the explained output, and can be located using outputIndex.

`approximationError` `number`

Output only. Error of `  featureAttributions  ` caused by approximation used in the explanation method. Lower value means more precise attributions.

  - For Sampled Shapley `  attribution  ` , increasing `  pathCount  ` might reduce the error.
  - For Integrated Gradients `  attribution  ` , increasing `  stepCount  ` might reduce the error.
  - For `  XRAI attribution  ` , increasing `  stepCount  ` might reduce the error.

See [this introduction](https://docs.cloud.google.com/vertex-ai/docs/explainable-ai/overview) for more information.

`outputName` `string`

Output only. name of the explain output. Specified as the key in `  ExplanationMetadata.outputs  ` .

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
  &quot;baselineOutputValue&quot;: number,
  &quot;instanceOutputValue&quot;: number,
  &quot;featureAttributions&quot;: value,
  &quot;outputIndex&quot;: [
    integer
  ],
  &quot;outputDisplayName&quot;: string,
  &quot;approximationError&quot;: number,
  &quot;outputName&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>
