---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/Metric
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/Metric
title: Metric
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

The metric used for running evaluations.

Fields

`aggregationMetrics[]` ` enum ( AggregationMetric  ` )

Optional. The aggregation metrics to use.

`metadata` ` object ( MetricMetadata  ` )

Optional. metadata about the metric, used for visualization and organization.

`metric_spec` `Union type`

The spec for the metric. It would be either a pre-defined metric, or a inline metric spec. `metric_spec` can be only one of the following:

`predefinedMetricSpec` ` object ( PredefinedMetricSpec  ` )

The spec for a pre-defined metric.

`computationBasedMetricSpec` ` object ( ComputationBasedMetricSpec  ` )

Spec for a computation based metric.

`llmBasedMetricSpec` ` object ( LLMBasedMetricSpec  ` )

Spec for an LLM based metric.

`customCodeExecutionSpec` ` object ( CustomCodeExecutionSpec  ` )

Spec for Custom code Execution metric.

`pointwiseMetricSpec` ` object ( PointwiseMetricSpec  ` )

Spec for pointwise metric.

`pairwiseMetricSpec` ` object ( PairwiseMetricSpec  ` )

Spec for pairwise metric.

`exactMatchSpec` ` object ( ExactMatchSpec  ` )

Spec for exact match metric.

`bleuSpec` ` object ( BleuSpec  ` )

Spec for bleu metric.

`rougeSpec` ` object ( RougeSpec  ` )

Spec for rouge metric.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;aggregationMetrics&quot;: [enum (AggregationMetric)],&quot;metadata&quot;: {object (MetricMetadata)},// metric_spec&quot;predefinedMetricSpec&quot;: {object (PredefinedMetricSpec)},&quot;computationBasedMetricSpec&quot;: {object (ComputationBasedMetricSpec)},&quot;llmBasedMetricSpec&quot;: {object (LLMBasedMetricSpec)},&quot;customCodeExecutionSpec&quot;: {object (CustomCodeExecutionSpec)},&quot;pointwiseMetricSpec&quot;: {object (PointwiseMetricSpec)},&quot;pairwiseMetricSpec&quot;: {object (PairwiseMetricSpec)},&quot;exactMatchSpec&quot;: {object (ExactMatchSpec)},&quot;bleuSpec&quot;: {object (BleuSpec)},&quot;rougeSpec&quot;: {object (RougeSpec)}// Union type}</code></pre></td>
</tr>
</tbody>
</table>

## PredefinedMetricSpec

The spec for a pre-defined metric.

Fields

`metricSpecName` `string`

Required. The name of a pre-defined metric, such as "instruction\_following\_v1" or "text\_quality\_v1".

`metricSpecParameters` ` object ( Struct  ` format)

Optional. The parameters needed to run the pre-defined metric.

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
  &quot;metricSpecName&quot;: string,
  &quot;metricSpecParameters&quot;: {
    object
  }
}</code></pre></td>
</tr>
</tbody>
</table>

## ComputationBasedMetricSpec

Specification for a computation based metric.

Fields

`type` ` enum ( ComputationBasedMetricType  ` )

Required. The type of the computation based metric.

`parameters` ` object ( Struct  ` format)

Optional. A map of parameters for the metric, e.g. {"rougeType": "rougeL"}.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;type&quot;: enum (ComputationBasedMetricType),&quot;parameters&quot;: {object}}</code></pre></td>
</tr>
</tbody>
</table>

## ComputationBasedMetricType

Types of computation based metrics.

Enums

`COMPUTATION_BASED_METRIC_TYPE_UNSPECIFIED`

Unspecified computation based metric type.

`EXACT_MATCH`

Exact match metric.

`BLEU`

BLEU metric.

`ROUGE`

ROUGE metric.

## LLMBasedMetricSpec

Specification for an LLM based metric.

Fields

`resultParserConfig` ` object ( EvaluationParserConfig  ` )

Optional. The parser config for the metric result.

`rubrics_source` `Union type`

Source of the rubrics to be used for evaluation. `rubrics_source` can be only one of the following:

`rubricGroupKey` `string`

Use a pre-defined group of rubrics associated with the input. Refers to a key in the rubricGroups map of EvaluationInstance.

`rubricGenerationSpec` ` object ( RubricGenerationSpec  ` )

Dynamically generate rubrics using this specification.

`predefinedRubricGenerationSpec` ` object ( PredefinedMetricSpec  ` )

Dynamically generate rubrics using a predefined spec.

`metricPromptTemplate` `string`

Required. Template for the prompt sent to the judge model.

`systemInstruction` `string`

Optional. System instructions for the judge model.

`judgeAutoraterConfig` ` object ( AutoraterConfig  ` )

Optional. Optional configuration for the judge LLM (Autorater).

`additionalConfig` ` object ( Struct  ` format)

Optional. Optional additional configuration for the metric.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;resultParserConfig&quot;: {object (EvaluationParserConfig)},// rubrics_source&quot;rubricGroupKey&quot;: string,&quot;rubricGenerationSpec&quot;: {object (RubricGenerationSpec)},&quot;predefinedRubricGenerationSpec&quot;: {object (PredefinedMetricSpec)}// Union type&quot;metricPromptTemplate&quot;: string,&quot;systemInstruction&quot;: string,&quot;judgeAutoraterConfig&quot;: {object (AutoraterConfig)},&quot;additionalConfig&quot;: {object}}</code></pre></td>
</tr>
</tbody>
</table>

## RubricGenerationSpec

Specification for how rubrics should be generated.

Fields

`promptTemplate` `string`

Template for the prompt used to generate rubrics. The details should be updated based on the most-recent recipe requirements.

`rubricContentType` ` enum ( RubricContentType  ` )

The type of rubric content to be generated.

`rubricTypeOntology[]` `string`

Optional. An optional, pre-defined list of allowed types for generated rubrics. If this field is provided, it implies `include_rubric_type` should be true, and the generated rubric types should be chosen from this ontology.

`modelConfig` ` object ( AutoraterConfig  ` )

Configuration for the model used in rubric generation. Configs including sampling count and base model can be specified here. Flipping is not supported for rubric generation.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;promptTemplate&quot;: string,&quot;rubricContentType&quot;: enum (RubricContentType),&quot;rubricTypeOntology&quot;: [string],&quot;modelConfig&quot;: {object (AutoraterConfig)}}</code></pre></td>
</tr>
</tbody>
</table>

## RubricContentType

Specifies the type of rubric content to generate.

Enums

`RUBRIC_CONTENT_TYPE_UNSPECIFIED`

The content type to generate is not specified.

`PROPERTY`

Generate rubrics based on properties.

`NL_QUESTION_ANSWER`

Generate rubrics in an NL question answer format.

`PYTHON_CODE_ASSERTION`

Generate rubrics in a unit test format.

## EvaluationParserConfig

Config for parsing LLM responses. It can be used to parse the LLM response to be evaluated, or the LLM response from LLM-based metrics/Autoraters.

Fields

`parser` `Union type`

The parser to use. `parser` can be only one of the following:

`customCodeParserConfig` ` object ( CustomCodeParserConfig  ` )

Optional. Use custom code to parse the LLM response.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{// parser&quot;customCodeParserConfig&quot;: {object (CustomCodeParserConfig)}// Union type}</code></pre></td>
</tr>
</tbody>
</table>

## CustomCodeParserConfig

Configuration for parsing the LLM response using custom code.

Fields

`parsingFunction` `string`

Required. Python function for parsing results. The function should be defined within this string.

The function takes a list of strings (LLM responses) and should return either a list of dictionaries (for rubrics) or a single dictionary (for a metric result).

Example function signature: def parse(responses: list\[str\]) -\> list\[dict\[str, Any\]\] | dict\[str, Any\]:

When parsing rubrics, return a list of dictionaries, where each dictionary represents a Rubric. Example for rubrics: \[ { "content": {"property": {"description": "The response is factual."}}, "type": "FACTUALITY", "importance": "HIGH" }, { "content": {"property": {"description": "The response is fluent."}}, "type": "FLUENCY", "importance": "MEDIUM" } \]

When parsing critique results, return a dictionary representing a MetricResult. Example for a metric result: { "score": 0.8, "explanation": "The model followed most instructions.", "rubricVerdicts": \[...\] }

... code for result extraction and aggregation

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
  &quot;parsingFunction&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

## CustomCodeExecutionSpec

Specificies a metric that is populated by evaluating user-defined Python code.

Fields

`evaluationFunction` `string`

Required. Python function. Expected user to define the following function, e.g.: def evaluate(instance: dict\[str, Any\]) -\> float: Please include this function signature in the code snippet. Instance is the evaluation instance, any fields populated in the instance are available to the function as instance\[fieldName\].

Example: Example input:

`instance= EvaluationInstance( response=EvaluationInstance.InstanceData(text="The answer is 4."), reference=EvaluationInstance.InstanceData(text="4") )`

Example converted input:

`{ 'response': {'text': 'The answer is 4.'}, 'reference': {'text': '4'} }`

Example python function:

`def evaluate(instance: dict[str, Any]) -> float: if instance['response']['text'] == instance['reference']['text']: return 1.0 return 0.0`

CustomCodeExecutionSpec is also supported in Batch Evaluation (EvalDataset RPC) and Tuning Evaluation. Each line in the input jsonl file will be converted to dict\[str, Any\] and passed to the evaluation function.

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
  &quot;evaluationFunction&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

## PointwiseMetricSpec

Spec for pointwise metric.

Fields

`customOutputFormatConfig` ` object ( CustomOutputFormatConfig  ` )

Optional. CustomOutputFormatConfig allows customization of metric output. By default, metrics return a score and explanation. When this config is set, the default output is replaced with either: - The raw output string. - A parsed output based on a user-defined schema. If a custom format is chosen, the `score` and `explanation` fields in the corresponding metric result will be empty.

`metricPromptTemplate` `string`

Required. Metric prompt template for pointwise metric.

`systemInstruction` `string`

Optional. System instructions for pointwise metric.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;customOutputFormatConfig&quot;: {object (CustomOutputFormatConfig)},&quot;metricPromptTemplate&quot;: string,&quot;systemInstruction&quot;: string}</code></pre></td>
</tr>
</tbody>
</table>

## CustomOutputFormatConfig

Spec for custom output format configuration.

Fields

`custom_output_format_config` `Union type`

Custom output format configuration. `custom_output_format_config` can be only one of the following:

`returnRawOutput` `boolean`

Optional. Whether to return raw output.

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

  // custom_output_format_config
  &quot;returnRawOutput&quot;: boolean
  // Union type
}</code></pre></td>
</tr>
</tbody>
</table>

## PairwiseMetricSpec

Spec for pairwise metric.

Fields

`candidateResponseFieldName` `string`

Optional. The field name of the candidate response.

`baselineResponseFieldName` `string`

Optional. The field name of the baseline response.

`customOutputFormatConfig` ` object ( CustomOutputFormatConfig  ` )

Optional. CustomOutputFormatConfig allows customization of metric output. When this config is set, the default output is replaced with the raw output string. If a custom format is chosen, the `pairwiseChoice` and `explanation` fields in the corresponding metric result will be empty.

`metricPromptTemplate` `string`

Required. Metric prompt template for pairwise metric.

`systemInstruction` `string`

Optional. System instructions for pairwise metric.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;candidateResponseFieldName&quot;: string,&quot;baselineResponseFieldName&quot;: string,&quot;customOutputFormatConfig&quot;: {object (CustomOutputFormatConfig)},&quot;metricPromptTemplate&quot;: string,&quot;systemInstruction&quot;: string}</code></pre></td>
</tr>
</tbody>
</table>

## ExactMatchSpec

This type has no fields.

Spec for exact match metric - returns 1 if prediction and reference exactly matches, otherwise 0.

## BleuSpec

Spec for bleu score metric - calculates the precision of n-grams in the prediction as compared to reference - returns a score ranging between 0 to 1.

Fields

`useEffectiveOrder` `boolean`

Optional. Whether to useEffectiveOrder to compute bleu score.

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
  &quot;useEffectiveOrder&quot;: boolean
}</code></pre></td>
</tr>
</tbody>
</table>

## RougeSpec

Spec for rouge score metric - calculates the recall of n-grams in prediction as compared to reference - returns a score ranging between 0 and 1.

Fields

`rougeType` `string`

Optional. Supported rouge types are rougen\[1-9\], rougeL, and rougeLsum.

`useStemmer` `boolean`

Optional. Whether to use stemmer to compute rouge score.

`splitSummaries` `boolean`

Optional. Whether to split summaries while using rougeLsum.

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
  &quot;rougeType&quot;: string,
  &quot;useStemmer&quot;: boolean,
  &quot;splitSummaries&quot;: boolean
}</code></pre></td>
</tr>
</tbody>
</table>

## MetricMetadata

metadata about the metric, used for visualization and organization.

Fields

`title` `string`

Optional. The user-friendly name for the metric. If not set for a registered metric, it will default to the metric's display name.

`scoreRange` ` object ( ScoreRange  ` )

Optional. The range of possible scores for this metric, used for plotting.

`otherMetadata` ` object ( Struct  ` format)

Optional. Flexible metadata for user-defined attributes.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;title&quot;: string,&quot;scoreRange&quot;: {object (ScoreRange)},&quot;otherMetadata&quot;: {object}}</code></pre></td>
</tr>
</tbody>
</table>

## ScoreRange

The range of possible scores for this metric, used for plotting.

Fields

`description` `string`

Optional. The description of the score explaining the directionality etc.

`min` `number`

Required. The minimum value of the score range (inclusive).

`max` `number`

Required. The maximum value of the score range (inclusive).

`step` `number`

Optional. The distance between discrete steps in the range. If unset, the range is assumed to be continuous.

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
  &quot;description&quot;: string,
  &quot;min&quot;: number,
  &quot;max&quot;: number,
  &quot;step&quot;: number
}</code></pre></td>
</tr>
</tbody>
</table>
