---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations/evaluateInstances
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations/evaluateInstances
title: 'Method: locations.evaluateInstances'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.evaluateInstances

Evaluates instances based on a given metric.

### Endpoint

post `https: / /{service-endpoint} /v1 /{location}:evaluateInstances`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`location` `string`

Required. The resource name of the Location to evaluate the instances. Format: `projects/{project}/locations/{location}`

### Request body

The request body contains data with the following structure:

Fields

`autoraterConfig` ` object ( AutoraterConfig  ` )

Optional. Autorater config used for evaluation. Not applicable for predefined metrics (PredefinedMetricSpec); the server uses its own model configuration for predefined metrics and this field is ignored.

`metric_inputs` `Union type`

Instances and specs for evaluation `metric_inputs` can be only one of the following:

`exactMatchInput` ` object ( ExactMatchInput  ` )

Auto metric instances. Instances and metric spec for exact match metric.

`bleuInput` ` object ( BleuInput  ` )

Instances and metric spec for bleu metric.

`rougeInput` ` object ( RougeInput  ` )

Instances and metric spec for rouge metric.

`fluencyInput` ` object ( FluencyInput  ` )

LLM-based metric instance. General text generation metrics, applicable to other categories. Input for fluency metric.

`coherenceInput` ` object ( CoherenceInput  ` )

Input for coherence metric.

`safetyInput` ` object ( SafetyInput  ` )

Input for safety metric.

`groundednessInput` ` object ( GroundednessInput  ` )

Input for groundedness metric.

`fulfillmentInput` ` object ( FulfillmentInput  ` )

Input for fulfillment metric.

`summarizationQualityInput` ` object ( SummarizationQualityInput  ` )

Input for summarization quality metric.

`pairwiseSummarizationQualityInput` ` object ( PairwiseSummarizationQualityInput  ` )

Input for pairwise summarization quality metric.

`summarizationHelpfulnessInput` ` object ( SummarizationHelpfulnessInput  ` )

Input for summarization helpfulness metric.

`summarizationVerbosityInput` ` object ( SummarizationVerbosityInput  ` )

Input for summarization verbosity metric.

`questionAnsweringQualityInput` ` object ( QuestionAnsweringQualityInput  ` )

Input for question answering quality metric.

`pairwiseQuestionAnsweringQualityInput` ` object ( PairwiseQuestionAnsweringQualityInput  ` )

Input for pairwise question answering quality metric.

`questionAnsweringRelevanceInput` ` object ( QuestionAnsweringRelevanceInput  ` )

Input for question answering relevance metric.

`questionAnsweringHelpfulnessInput` ` object ( QuestionAnsweringHelpfulnessInput  ` )

Input for question answering helpfulness metric.

`questionAnsweringCorrectnessInput` ` object ( QuestionAnsweringCorrectnessInput  ` )

Input for question answering correctness metric.

`pointwiseMetricInput` ` object ( PointwiseMetricInput  ` )

Input for pointwise metric.

`pairwiseMetricInput` ` object ( PairwiseMetricInput  ` )

Input for pairwise metric.

`toolCallValidInput` ` object ( ToolCallValidInput  ` )

Tool call metric instances. Input for tool call valid metric.

`toolNameMatchInput` ` object ( ToolNameMatchInput  ` )

Input for tool name match metric.

`toolParameterKeyMatchInput` ` object ( ToolParameterKeyMatchInput  ` )

Input for tool parameter key match metric.

`toolParameterKvMatchInput` ` object ( ToolParameterKVMatchInput  ` )

Input for tool parameter key value match metric.

`cometInput` ` object ( CometInput  ` )

Translation metrics. Input for Comet metric.

`metricxInput` ` object ( MetricxInput  ` )

Input for Metricx metric.

`trajectoryExactMatchInput` ` object ( TrajectoryExactMatchInput  ` )

Input for trajectory exact match metric.

`trajectoryInOrderMatchInput` ` object ( TrajectoryInOrderMatchInput  ` )

Input for trajectory in order match metric.

`trajectoryAnyOrderMatchInput` ` object ( TrajectoryAnyOrderMatchInput  ` )

Input for trajectory match any order metric.

`trajectoryPrecisionInput` ` object ( TrajectoryPrecisionInput  ` )

Input for trajectory precision metric.

`trajectoryRecallInput` ` object ( TrajectoryRecallInput  ` )

Input for trajectory recall metric.

`trajectorySingleToolUseInput` ` object ( TrajectorySingleToolUseInput  ` )

Input for trajectory single tool use metric.

### Response body

Response message for EvaluationService.EvaluateInstances.

If successful, the response body contains data with the following structure:

Fields

`metricResults[]` ` object ( MetricResult  ` )

Metric results for each instance. The order of the metric results is guaranteed to be the same as the order of the instances in the request.

`evaluation_results` `Union type`

Evaluation results will be served in the same order as presented in EvaluationRequest.instances. `evaluation_results` can be only one of the following:

`exactMatchResults` ` object ( ExactMatchResults  ` )

Auto metric evaluation results. Results for exact match metric.

`bleuResults` ` object ( BleuResults  ` )

Results for bleu metric.

`rougeResults` ` object ( RougeResults  ` )

Results for rouge metric.

`fluencyResult` ` object ( FluencyResult  ` )

LLM-based metric evaluation result. General text generation metrics, applicable to other categories. result for fluency metric.

`coherenceResult` ` object ( CoherenceResult  ` )

result for coherence metric.

`safetyResult` ` object ( SafetyResult  ` )

result for safety metric.

`groundednessResult` ` object ( GroundednessResult  ` )

result for groundedness metric.

`fulfillmentResult` ` object ( FulfillmentResult  ` )

result for fulfillment metric.

`summarizationQualityResult` ` object ( SummarizationQualityResult  ` )

Summarization only metrics. result for summarization quality metric.

`pairwiseSummarizationQualityResult` ` object ( PairwiseSummarizationQualityResult  ` )

result for pairwise summarization quality metric.

`summarizationHelpfulnessResult` ` object ( SummarizationHelpfulnessResult  ` )

result for summarization helpfulness metric.

`summarizationVerbosityResult` ` object ( SummarizationVerbosityResult  ` )

result for summarization verbosity metric.

`questionAnsweringQualityResult` ` object ( QuestionAnsweringQualityResult  ` )

Question answering only metrics. result for question answering quality metric.

`pairwiseQuestionAnsweringQualityResult` ` object ( PairwiseQuestionAnsweringQualityResult  ` )

result for pairwise question answering quality metric.

`questionAnsweringRelevanceResult` ` object ( QuestionAnsweringRelevanceResult  ` )

result for question answering relevance metric.

`questionAnsweringHelpfulnessResult` ` object ( QuestionAnsweringHelpfulnessResult  ` )

result for question answering helpfulness metric.

`questionAnsweringCorrectnessResult` ` object ( QuestionAnsweringCorrectnessResult  ` )

result for question answering correctness metric.

`pointwiseMetricResult` ` object ( PointwiseMetricResult  ` )

Generic metrics. result for pointwise metric.

`pairwiseMetricResult` ` object ( PairwiseMetricResult  ` )

result for pairwise metric.

`toolCallValidResults` ` object ( ToolCallValidResults  ` )

Tool call metrics. Results for tool call valid metric.

`toolNameMatchResults` ` object ( ToolNameMatchResults  ` )

Results for tool name match metric.

`toolParameterKeyMatchResults` ` object ( ToolParameterKeyMatchResults  ` )

Results for tool parameter key match metric.

`toolParameterKvMatchResults` ` object ( ToolParameterKVMatchResults  ` )

Results for tool parameter key value match metric.

`cometResult` ` object ( CometResult  ` )

Translation metrics. result for Comet metric.

`metricxResult` ` object ( MetricxResult  ` )

result for Metricx metric.

`trajectoryExactMatchResults` ` object ( TrajectoryExactMatchResults  ` )

result for trajectory exact match metric.

`trajectoryInOrderMatchResults` ` object ( TrajectoryInOrderMatchResults  ` )

result for trajectory in order match metric.

`trajectoryAnyOrderMatchResults` ` object ( TrajectoryAnyOrderMatchResults  ` )

result for trajectory any order match metric.

`trajectoryPrecisionResults` ` object ( TrajectoryPrecisionResults  ` )

result for trajectory precision metric.

`trajectoryRecallResults` ` object ( TrajectoryRecallResults  ` )

Results for trajectory recall metric.

`trajectorySingleToolUseResults` ` object ( TrajectorySingleToolUseResults  ` )

Results for trajectory single tool use metric.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;metricResults&quot;: [{object (MetricResult)}],// evaluation_results&quot;exactMatchResults&quot;: {object (ExactMatchResults)},&quot;bleuResults&quot;: {object (BleuResults)},&quot;rougeResults&quot;: {object (RougeResults)},&quot;fluencyResult&quot;: {object (FluencyResult)},&quot;coherenceResult&quot;: {object (CoherenceResult)},&quot;safetyResult&quot;: {object (SafetyResult)},&quot;groundednessResult&quot;: {object (GroundednessResult)},&quot;fulfillmentResult&quot;: {object (FulfillmentResult)},&quot;summarizationQualityResult&quot;: {object (SummarizationQualityResult)},&quot;pairwiseSummarizationQualityResult&quot;: {object (PairwiseSummarizationQualityResult)},&quot;summarizationHelpfulnessResult&quot;: {object (SummarizationHelpfulnessResult)},&quot;summarizationVerbosityResult&quot;: {object (SummarizationVerbosityResult)},&quot;questionAnsweringQualityResult&quot;: {object (QuestionAnsweringQualityResult)},&quot;pairwiseQuestionAnsweringQualityResult&quot;: {object (PairwiseQuestionAnsweringQualityResult)},&quot;questionAnsweringRelevanceResult&quot;: {object (QuestionAnsweringRelevanceResult)},&quot;questionAnsweringHelpfulnessResult&quot;: {object (QuestionAnsweringHelpfulnessResult)},&quot;questionAnsweringCorrectnessResult&quot;: {object (QuestionAnsweringCorrectnessResult)},&quot;pointwiseMetricResult&quot;: {object (PointwiseMetricResult)},&quot;pairwiseMetricResult&quot;: {object (PairwiseMetricResult)},&quot;toolCallValidResults&quot;: {object (ToolCallValidResults)},&quot;toolNameMatchResults&quot;: {object (ToolNameMatchResults)},&quot;toolParameterKeyMatchResults&quot;: {object (ToolParameterKeyMatchResults)},&quot;toolParameterKvMatchResults&quot;: {object (ToolParameterKVMatchResults)},&quot;cometResult&quot;: {object (CometResult)},&quot;metricxResult&quot;: {object (MetricxResult)},&quot;trajectoryExactMatchResults&quot;: {object (TrajectoryExactMatchResults)},&quot;trajectoryInOrderMatchResults&quot;: {object (TrajectoryInOrderMatchResults)},&quot;trajectoryAnyOrderMatchResults&quot;: {object (TrajectoryAnyOrderMatchResults)},&quot;trajectoryPrecisionResults&quot;: {object (TrajectoryPrecisionResults)},&quot;trajectoryRecallResults&quot;: {object (TrajectoryRecallResults)},&quot;trajectorySingleToolUseResults&quot;: {object (TrajectorySingleToolUseResults)}// Union type}</code></pre></td>
</tr>
</tbody>
</table>

## ExactMatchInput

Input for exact match metric.

Fields

`metricSpec` ` object ( ExactMatchSpec  ` )

Required. Spec for exact match metric.

`instances[]` ` object ( ExactMatchInstance  ` )

Required. Repeated exact match instances.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;metricSpec&quot;: {object (ExactMatchSpec)},&quot;instances&quot;: [{object (ExactMatchInstance)}]}</code></pre></td>
</tr>
</tbody>
</table>

## ExactMatchInstance

Spec for exact match instance.

Fields

`prediction` `string`

Required. Output of the evaluated model.

`reference` `string`

Required. Ground truth used to compare against the prediction.

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
  &quot;prediction&quot;: string,
  &quot;reference&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

## BleuInput

Input for bleu metric.

Fields

`metricSpec` ` object ( BleuSpec  ` )

Required. Spec for bleu score metric.

`instances[]` ` object ( BleuInstance  ` )

Required. Repeated bleu instances.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;metricSpec&quot;: {object (BleuSpec)},&quot;instances&quot;: [{object (BleuInstance)}]}</code></pre></td>
</tr>
</tbody>
</table>

## BleuInstance

Spec for bleu instance.

Fields

`prediction` `string`

Required. Output of the evaluated model.

`reference` `string`

Required. Ground truth used to compare against the prediction.

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
  &quot;prediction&quot;: string,
  &quot;reference&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

## RougeInput

Input for rouge metric.

Fields

`metricSpec` ` object ( RougeSpec  ` )

Required. Spec for rouge score metric.

`instances[]` ` object ( RougeInstance  ` )

Required. Repeated rouge instances.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;metricSpec&quot;: {object (RougeSpec)},&quot;instances&quot;: [{object (RougeInstance)}]}</code></pre></td>
</tr>
</tbody>
</table>

## RougeInstance

Spec for rouge instance.

Fields

`prediction` `string`

Required. Output of the evaluated model.

`reference` `string`

Required. Ground truth used to compare against the prediction.

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
  &quot;prediction&quot;: string,
  &quot;reference&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

## FluencyInput

Input for fluency metric.

Fields

`metricSpec` ` object ( FluencySpec  ` )

Required. Spec for fluency score metric.

`instance` ` object ( FluencyInstance  ` )

Required. Fluency instance.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;metricSpec&quot;: {object (FluencySpec)},&quot;instance&quot;: {object (FluencyInstance)}}</code></pre></td>
</tr>
</tbody>
</table>

## FluencySpec

Spec for fluency score metric.

Fields

`version` `integer`

Optional. Which version to use for evaluation.

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
  &quot;version&quot;: integer
}</code></pre></td>
</tr>
</tbody>
</table>

## FluencyInstance

Spec for fluency instance.

Fields

`prediction` `string`

Required. Output of the evaluated model.

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
  &quot;prediction&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

## CoherenceInput

Input for coherence metric.

Fields

`metricSpec` ` object ( CoherenceSpec  ` )

Required. Spec for coherence score metric.

`instance` ` object ( CoherenceInstance  ` )

Required. Coherence instance.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;metricSpec&quot;: {object (CoherenceSpec)},&quot;instance&quot;: {object (CoherenceInstance)}}</code></pre></td>
</tr>
</tbody>
</table>

## CoherenceSpec

Spec for coherence score metric.

Fields

`version` `integer`

Optional. Which version to use for evaluation.

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
  &quot;version&quot;: integer
}</code></pre></td>
</tr>
</tbody>
</table>

## CoherenceInstance

Spec for coherence instance.

Fields

`prediction` `string`

Required. Output of the evaluated model.

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
  &quot;prediction&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

## SafetyInput

Input for safety metric.

Fields

`metricSpec` ` object ( SafetySpec  ` )

Required. Spec for safety metric.

`instance` ` object ( SafetyInstance  ` )

Required. Safety instance.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;metricSpec&quot;: {object (SafetySpec)},&quot;instance&quot;: {object (SafetyInstance)}}</code></pre></td>
</tr>
</tbody>
</table>

## SafetySpec

Spec for safety metric.

Fields

`version` `integer`

Optional. Which version to use for evaluation.

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
  &quot;version&quot;: integer
}</code></pre></td>
</tr>
</tbody>
</table>

## SafetyInstance

Spec for safety instance.

Fields

`prediction` `string`

Required. Output of the evaluated model.

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
  &quot;prediction&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

## GroundednessInput

Input for groundedness metric.

Fields

`metricSpec` ` object ( GroundednessSpec  ` )

Required. Spec for groundedness metric.

`instance` ` object ( GroundednessInstance  ` )

Required. Groundedness instance.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;metricSpec&quot;: {object (GroundednessSpec)},&quot;instance&quot;: {object (GroundednessInstance)}}</code></pre></td>
</tr>
</tbody>
</table>

## GroundednessSpec

Spec for groundedness metric.

Fields

`version` `integer`

Optional. Which version to use for evaluation.

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
  &quot;version&quot;: integer
}</code></pre></td>
</tr>
</tbody>
</table>

## GroundednessInstance

Spec for groundedness instance.

Fields

`prediction` `string`

Required. Output of the evaluated model.

`context` `string`

Required. Background information provided in context used to compare against the prediction.

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
  &quot;prediction&quot;: string,
  &quot;context&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

## FulfillmentInput

Input for fulfillment metric.

Fields

`metricSpec` ` object ( FulfillmentSpec  ` )

Required. Spec for fulfillment score metric.

`instance` ` object ( FulfillmentInstance  ` )

Required. Fulfillment instance.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;metricSpec&quot;: {object (FulfillmentSpec)},&quot;instance&quot;: {object (FulfillmentInstance)}}</code></pre></td>
</tr>
</tbody>
</table>

## FulfillmentSpec

Spec for fulfillment metric.

Fields

`version` `integer`

Optional. Which version to use for evaluation.

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
  &quot;version&quot;: integer
}</code></pre></td>
</tr>
</tbody>
</table>

## FulfillmentInstance

Spec for fulfillment instance.

Fields

`prediction` `string`

Required. Output of the evaluated model.

`instruction` `string`

Required. Inference instruction prompt to compare prediction with.

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
  &quot;prediction&quot;: string,
  &quot;instruction&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

## SummarizationQualityInput

Input for summarization quality metric.

Fields

`metricSpec` ` object ( SummarizationQualitySpec  ` )

Required. Spec for summarization quality score metric.

`instance` ` object ( SummarizationQualityInstance  ` )

Required. Summarization quality instance.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;metricSpec&quot;: {object (SummarizationQualitySpec)},&quot;instance&quot;: {object (SummarizationQualityInstance)}}</code></pre></td>
</tr>
</tbody>
</table>

## SummarizationQualitySpec

Spec for summarization quality score metric.

Fields

`useReference` `boolean`

Optional. Whether to use instance.reference to compute summarization quality.

`version` `integer`

Optional. Which version to use for evaluation.

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
  &quot;useReference&quot;: boolean,
  &quot;version&quot;: integer
}</code></pre></td>
</tr>
</tbody>
</table>

## SummarizationQualityInstance

Spec for summarization quality instance.

Fields

`prediction` `string`

Required. Output of the evaluated model.

`reference` `string`

Optional. Ground truth used to compare against the prediction.

`context` `string`

Required. Text to be summarized.

`instruction` `string`

Required. Summarization prompt for LLM.

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
  &quot;prediction&quot;: string,
  &quot;reference&quot;: string,
  &quot;context&quot;: string,
  &quot;instruction&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

## PairwiseSummarizationQualityInput

Input for pairwise summarization quality metric.

Fields

`metricSpec` ` object ( PairwiseSummarizationQualitySpec  ` )

Required. Spec for pairwise summarization quality score metric.

`instance` ` object ( PairwiseSummarizationQualityInstance  ` )

Required. Pairwise summarization quality instance.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;metricSpec&quot;: {object (PairwiseSummarizationQualitySpec)},&quot;instance&quot;: {object (PairwiseSummarizationQualityInstance)}}</code></pre></td>
</tr>
</tbody>
</table>

## PairwiseSummarizationQualitySpec

Spec for pairwise summarization quality score metric.

Fields

`useReference` `boolean`

Optional. Whether to use instance.reference to compute pairwise summarization quality.

`version` `integer`

Optional. Which version to use for evaluation.

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
  &quot;useReference&quot;: boolean,
  &quot;version&quot;: integer
}</code></pre></td>
</tr>
</tbody>
</table>

## PairwiseSummarizationQualityInstance

Spec for pairwise summarization quality instance.

Fields

`prediction` `string`

Required. Output of the candidate model.

`baselinePrediction` `string`

Required. Output of the baseline model.

`reference` `string`

Optional. Ground truth used to compare against the prediction.

`context` `string`

Required. Text to be summarized.

`instruction` `string`

Required. Summarization prompt for LLM.

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
  &quot;prediction&quot;: string,
  &quot;baselinePrediction&quot;: string,
  &quot;reference&quot;: string,
  &quot;context&quot;: string,
  &quot;instruction&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

## SummarizationHelpfulnessInput

Input for summarization helpfulness metric.

Fields

`metricSpec` ` object ( SummarizationHelpfulnessSpec  ` )

Required. Spec for summarization helpfulness score metric.

`instance` ` object ( SummarizationHelpfulnessInstance  ` )

Required. Summarization helpfulness instance.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;metricSpec&quot;: {object (SummarizationHelpfulnessSpec)},&quot;instance&quot;: {object (SummarizationHelpfulnessInstance)}}</code></pre></td>
</tr>
</tbody>
</table>

## SummarizationHelpfulnessSpec

Spec for summarization helpfulness score metric.

Fields

`useReference` `boolean`

Optional. Whether to use instance.reference to compute summarization helpfulness.

`version` `integer`

Optional. Which version to use for evaluation.

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
  &quot;useReference&quot;: boolean,
  &quot;version&quot;: integer
}</code></pre></td>
</tr>
</tbody>
</table>

## SummarizationHelpfulnessInstance

Spec for summarization helpfulness instance.

Fields

`prediction` `string`

Required. Output of the evaluated model.

`reference` `string`

Optional. Ground truth used to compare against the prediction.

`context` `string`

Required. Text to be summarized.

`instruction` `string`

Optional. Summarization prompt for LLM.

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
  &quot;prediction&quot;: string,
  &quot;reference&quot;: string,
  &quot;context&quot;: string,
  &quot;instruction&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

## SummarizationVerbosityInput

Input for summarization verbosity metric.

Fields

`metricSpec` ` object ( SummarizationVerbositySpec  ` )

Required. Spec for summarization verbosity score metric.

`instance` ` object ( SummarizationVerbosityInstance  ` )

Required. Summarization verbosity instance.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;metricSpec&quot;: {object (SummarizationVerbositySpec)},&quot;instance&quot;: {object (SummarizationVerbosityInstance)}}</code></pre></td>
</tr>
</tbody>
</table>

## SummarizationVerbositySpec

Spec for summarization verbosity score metric.

Fields

`useReference` `boolean`

Optional. Whether to use instance.reference to compute summarization verbosity.

`version` `integer`

Optional. Which version to use for evaluation.

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
  &quot;useReference&quot;: boolean,
  &quot;version&quot;: integer
}</code></pre></td>
</tr>
</tbody>
</table>

## SummarizationVerbosityInstance

Spec for summarization verbosity instance.

Fields

`prediction` `string`

Required. Output of the evaluated model.

`reference` `string`

Optional. Ground truth used to compare against the prediction.

`context` `string`

Required. Text to be summarized.

`instruction` `string`

Optional. Summarization prompt for LLM.

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
  &quot;prediction&quot;: string,
  &quot;reference&quot;: string,
  &quot;context&quot;: string,
  &quot;instruction&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

## QuestionAnsweringQualityInput

Input for question answering quality metric.

Fields

`metricSpec` ` object ( QuestionAnsweringQualitySpec  ` )

Required. Spec for question answering quality score metric.

`instance` ` object ( QuestionAnsweringQualityInstance  ` )

Required. Question answering quality instance.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;metricSpec&quot;: {object (QuestionAnsweringQualitySpec)},&quot;instance&quot;: {object (QuestionAnsweringQualityInstance)}}</code></pre></td>
</tr>
</tbody>
</table>

## QuestionAnsweringQualitySpec

Spec for question answering quality score metric.

Fields

`useReference` `boolean`

Optional. Whether to use instance.reference to compute question answering quality.

`version` `integer`

Optional. Which version to use for evaluation.

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
  &quot;useReference&quot;: boolean,
  &quot;version&quot;: integer
}</code></pre></td>
</tr>
</tbody>
</table>

## QuestionAnsweringQualityInstance

Spec for question answering quality instance.

Fields

`prediction` `string`

Required. Output of the evaluated model.

`reference` `string`

Optional. Ground truth used to compare against the prediction.

`context` `string`

Required. Text to answer the question.

`instruction` `string`

Required. Question Answering prompt for LLM.

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
  &quot;prediction&quot;: string,
  &quot;reference&quot;: string,
  &quot;context&quot;: string,
  &quot;instruction&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

## PairwiseQuestionAnsweringQualityInput

Input for pairwise question answering quality metric.

Fields

`metricSpec` ` object ( PairwiseQuestionAnsweringQualitySpec  ` )

Required. Spec for pairwise question answering quality score metric.

`instance` ` object ( PairwiseQuestionAnsweringQualityInstance  ` )

Required. Pairwise question answering quality instance.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;metricSpec&quot;: {object (PairwiseQuestionAnsweringQualitySpec)},&quot;instance&quot;: {object (PairwiseQuestionAnsweringQualityInstance)}}</code></pre></td>
</tr>
</tbody>
</table>

## PairwiseQuestionAnsweringQualitySpec

Spec for pairwise question answering quality score metric.

Fields

`useReference` `boolean`

Optional. Whether to use instance.reference to compute question answering quality.

`version` `integer`

Optional. Which version to use for evaluation.

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
  &quot;useReference&quot;: boolean,
  &quot;version&quot;: integer
}</code></pre></td>
</tr>
</tbody>
</table>

## PairwiseQuestionAnsweringQualityInstance

Spec for pairwise question answering quality instance.

Fields

`prediction` `string`

Required. Output of the candidate model.

`baselinePrediction` `string`

Required. Output of the baseline model.

`reference` `string`

Optional. Ground truth used to compare against the prediction.

`context` `string`

Required. Text to answer the question.

`instruction` `string`

Required. Question Answering prompt for LLM.

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
  &quot;prediction&quot;: string,
  &quot;baselinePrediction&quot;: string,
  &quot;reference&quot;: string,
  &quot;context&quot;: string,
  &quot;instruction&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

## QuestionAnsweringRelevanceInput

Input for question answering relevance metric.

Fields

`metricSpec` ` object ( QuestionAnsweringRelevanceSpec  ` )

Required. Spec for question answering relevance score metric.

`instance` ` object ( QuestionAnsweringRelevanceInstance  ` )

Required. Question answering relevance instance.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;metricSpec&quot;: {object (QuestionAnsweringRelevanceSpec)},&quot;instance&quot;: {object (QuestionAnsweringRelevanceInstance)}}</code></pre></td>
</tr>
</tbody>
</table>

## QuestionAnsweringRelevanceSpec

Spec for question answering relevance metric.

Fields

`useReference` `boolean`

Optional. Whether to use instance.reference to compute question answering relevance.

`version` `integer`

Optional. Which version to use for evaluation.

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
  &quot;useReference&quot;: boolean,
  &quot;version&quot;: integer
}</code></pre></td>
</tr>
</tbody>
</table>

## QuestionAnsweringRelevanceInstance

Spec for question answering relevance instance.

Fields

`prediction` `string`

Required. Output of the evaluated model.

`reference` `string`

Optional. Ground truth used to compare against the prediction.

`context` `string`

Optional. Text provided as context to answer the question.

`instruction` `string`

Required. The question asked and other instruction in the inference prompt.

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
  &quot;prediction&quot;: string,
  &quot;reference&quot;: string,
  &quot;context&quot;: string,
  &quot;instruction&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

## QuestionAnsweringHelpfulnessInput

Input for question answering helpfulness metric.

Fields

`metricSpec` ` object ( QuestionAnsweringHelpfulnessSpec  ` )

Required. Spec for question answering helpfulness score metric.

`instance` ` object ( QuestionAnsweringHelpfulnessInstance  ` )

Required. Question answering helpfulness instance.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;metricSpec&quot;: {object (QuestionAnsweringHelpfulnessSpec)},&quot;instance&quot;: {object (QuestionAnsweringHelpfulnessInstance)}}</code></pre></td>
</tr>
</tbody>
</table>

## QuestionAnsweringHelpfulnessSpec

Spec for question answering helpfulness metric.

Fields

`useReference` `boolean`

Optional. Whether to use instance.reference to compute question answering helpfulness.

`version` `integer`

Optional. Which version to use for evaluation.

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
  &quot;useReference&quot;: boolean,
  &quot;version&quot;: integer
}</code></pre></td>
</tr>
</tbody>
</table>

## QuestionAnsweringHelpfulnessInstance

Spec for question answering helpfulness instance.

Fields

`prediction` `string`

Required. Output of the evaluated model.

`reference` `string`

Optional. Ground truth used to compare against the prediction.

`context` `string`

Optional. Text provided as context to answer the question.

`instruction` `string`

Required. The question asked and other instruction in the inference prompt.

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
  &quot;prediction&quot;: string,
  &quot;reference&quot;: string,
  &quot;context&quot;: string,
  &quot;instruction&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

## QuestionAnsweringCorrectnessInput

Input for question answering correctness metric.

Fields

`metricSpec` ` object ( QuestionAnsweringCorrectnessSpec  ` )

Required. Spec for question answering correctness score metric.

`instance` ` object ( QuestionAnsweringCorrectnessInstance  ` )

Required. Question answering correctness instance.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;metricSpec&quot;: {object (QuestionAnsweringCorrectnessSpec)},&quot;instance&quot;: {object (QuestionAnsweringCorrectnessInstance)}}</code></pre></td>
</tr>
</tbody>
</table>

## QuestionAnsweringCorrectnessSpec

Spec for question answering correctness metric.

Fields

`useReference` `boolean`

Optional. Whether to use instance.reference to compute question answering correctness.

`version` `integer`

Optional. Which version to use for evaluation.

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
  &quot;useReference&quot;: boolean,
  &quot;version&quot;: integer
}</code></pre></td>
</tr>
</tbody>
</table>

## QuestionAnsweringCorrectnessInstance

Spec for question answering correctness instance.

Fields

`prediction` `string`

Required. Output of the evaluated model.

`reference` `string`

Optional. Ground truth used to compare against the prediction.

`context` `string`

Optional. Text provided as context to answer the question.

`instruction` `string`

Required. The question asked and other instruction in the inference prompt.

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
  &quot;prediction&quot;: string,
  &quot;reference&quot;: string,
  &quot;context&quot;: string,
  &quot;instruction&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

## PointwiseMetricInput

Input for pointwise metric.

Fields

`metricSpec` ` object ( PointwiseMetricSpec  ` )

Required. Spec for pointwise metric.

`instance` ` object ( PointwiseMetricInstance  ` )

Required. Pointwise metric instance.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;metricSpec&quot;: {object (PointwiseMetricSpec)},&quot;instance&quot;: {object (PointwiseMetricInstance)}}</code></pre></td>
</tr>
</tbody>
</table>

## PointwiseMetricInstance

Pointwise metric instance. Usually one instance corresponds to one row in an evaluation dataset.

Fields

`instance` `Union type`

Instance for pointwise metric. `instance` can be only one of the following:

`jsonInstance` `string`

Instance specified as a json string. String key-value pairs are expected in the jsonInstance to render PointwiseMetricSpec.instance\_prompt\_template.

`contentMapInstance` ` object ( ContentMap  ` )

Key-value contents for the mutlimodality input, including text, image, video, audio, and pdf, etc. The key is placeholder in metric prompt template, and the value is the multimodal content.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{// instance&quot;jsonInstance&quot;: string,&quot;contentMapInstance&quot;: {object (ContentMap)}// Union type}</code></pre></td>
</tr>
</tbody>
</table>

## ContentMap

Map of placeholder in metric prompt template to contents of model input.

Fields

`values` ` map (key: string, value: object ( Contents  ` ))

Optional. Map of placeholder to contents.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;values&quot;: {string: {object (Contents)},...}}</code></pre></td>
</tr>
</tbody>
</table>

## Contents

Repeated Content type.

Fields

`contents[]` ` object ( Content  ` )

Optional. Repeated contents.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;contents&quot;: [{object (Content)}]}</code></pre></td>
</tr>
</tbody>
</table>

## PairwiseMetricInput

Input for pairwise metric.

Fields

`metricSpec` ` object ( PairwiseMetricSpec  ` )

Required. Spec for pairwise metric.

`instance` ` object ( PairwiseMetricInstance  ` )

Required. Pairwise metric instance.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;metricSpec&quot;: {object (PairwiseMetricSpec)},&quot;instance&quot;: {object (PairwiseMetricInstance)}}</code></pre></td>
</tr>
</tbody>
</table>

## PairwiseMetricInstance

Pairwise metric instance. Usually one instance corresponds to one row in an evaluation dataset.

Fields

`instance` `Union type`

Instance for pairwise metric. `instance` can be only one of the following:

`jsonInstance` `string`

Instance specified as a json string. String key-value pairs are expected in the jsonInstance to render PairwiseMetricSpec.instance\_prompt\_template.

`contentMapInstance` ` object ( ContentMap  ` )

Key-value contents for the mutlimodality input, including text, image, video, audio, and pdf, etc. The key is placeholder in metric prompt template, and the value is the multimodal content.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{// instance&quot;jsonInstance&quot;: string,&quot;contentMapInstance&quot;: {object (ContentMap)}// Union type}</code></pre></td>
</tr>
</tbody>
</table>

## ToolCallValidInput

Input for tool call valid metric.

Fields

`metricSpec` ` object ( ToolCallValidSpec  ` )

Required. Spec for tool call valid metric.

`instances[]` ` object ( ToolCallValidInstance  ` )

Required. Repeated tool call valid instances.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;metricSpec&quot;: {object (ToolCallValidSpec)},&quot;instances&quot;: [{object (ToolCallValidInstance)}]}</code></pre></td>
</tr>
</tbody>
</table>

## ToolCallValidSpec

This type has no fields.

Spec for tool call valid metric.

## ToolCallValidInstance

Spec for tool call valid instance.

Fields

`prediction` `string`

Required. Output of the evaluated model.

`reference` `string`

Required. Ground truth used to compare against the prediction.

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
  &quot;prediction&quot;: string,
  &quot;reference&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

## ToolNameMatchInput

Input for tool name match metric.

Fields

`metricSpec` ` object ( ToolNameMatchSpec  ` )

Required. Spec for tool name match metric.

`instances[]` ` object ( ToolNameMatchInstance  ` )

Required. Repeated tool name match instances.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;metricSpec&quot;: {object (ToolNameMatchSpec)},&quot;instances&quot;: [{object (ToolNameMatchInstance)}]}</code></pre></td>
</tr>
</tbody>
</table>

## ToolNameMatchSpec

This type has no fields.

Spec for tool name match metric.

## ToolNameMatchInstance

Spec for tool name match instance.

Fields

`prediction` `string`

Required. Output of the evaluated model.

`reference` `string`

Required. Ground truth used to compare against the prediction.

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
  &quot;prediction&quot;: string,
  &quot;reference&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

## ToolParameterKeyMatchInput

Input for tool parameter key match metric.

Fields

`metricSpec` ` object ( ToolParameterKeyMatchSpec  ` )

Required. Spec for tool parameter key match metric.

`instances[]` ` object ( ToolParameterKeyMatchInstance  ` )

Required. Repeated tool parameter key match instances.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;metricSpec&quot;: {object (ToolParameterKeyMatchSpec)},&quot;instances&quot;: [{object (ToolParameterKeyMatchInstance)}]}</code></pre></td>
</tr>
</tbody>
</table>

## ToolParameterKeyMatchSpec

This type has no fields.

Spec for tool parameter key match metric.

## ToolParameterKeyMatchInstance

Spec for tool parameter key match instance.

Fields

`prediction` `string`

Required. Output of the evaluated model.

`reference` `string`

Required. Ground truth used to compare against the prediction.

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
  &quot;prediction&quot;: string,
  &quot;reference&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

## ToolParameterKVMatchInput

Input for tool parameter key value match metric.

Fields

`metricSpec` ` object ( ToolParameterKVMatchSpec  ` )

Required. Spec for tool parameter key value match metric.

`instances[]` ` object ( ToolParameterKVMatchInstance  ` )

Required. Repeated tool parameter key value match instances.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;metricSpec&quot;: {object (ToolParameterKVMatchSpec)},&quot;instances&quot;: [{object (ToolParameterKVMatchInstance)}]}</code></pre></td>
</tr>
</tbody>
</table>

## ToolParameterKVMatchSpec

Spec for tool parameter key value match metric.

Fields

`useStrictStringMatch` `boolean`

Optional. Whether to use STRICT string match on parameter values.

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
  &quot;useStrictStringMatch&quot;: boolean
}</code></pre></td>
</tr>
</tbody>
</table>

## ToolParameterKVMatchInstance

Spec for tool parameter key value match instance.

Fields

`prediction` `string`

Required. Output of the evaluated model.

`reference` `string`

Required. Ground truth used to compare against the prediction.

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
  &quot;prediction&quot;: string,
  &quot;reference&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

## CometInput

Input for Comet metric.

Fields

`metricSpec` ` object ( CometSpec  ` )

Required. Spec for comet metric.

`instance` ` object ( CometInstance  ` )

Required. Comet instance.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;metricSpec&quot;: {object (CometSpec)},&quot;instance&quot;: {object (CometInstance)}}</code></pre></td>
</tr>
</tbody>
</table>

## CometSpec

Spec for Comet metric.

Fields

`sourceLanguage` `string`

Optional. Source language in BCP-47 format.

`targetLanguage` `string`

Optional. Target language in BCP-47 format. Covers both prediction and reference.

`version` ` enum ( CometVersion  ` )

Required. Which version to use for evaluation.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;sourceLanguage&quot;: string,&quot;targetLanguage&quot;: string,&quot;version&quot;: enum (CometVersion)}</code></pre></td>
</tr>
</tbody>
</table>

## CometVersion

Comet version options.

Enums

`COMET_VERSION_UNSPECIFIED`

Comet version unspecified.

`COMET_22_SRC_REF`

Comet 22 for translation + source + reference (source-reference-combined).

## CometInstance

Spec for Comet instance - The fields used for evaluation are dependent on the comet version.

Fields

`prediction` `string`

Required. Output of the evaluated model.

`reference` `string`

Optional. Ground truth used to compare against the prediction.

`source` `string`

Optional. Source text in original language.

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
  &quot;prediction&quot;: string,
  &quot;reference&quot;: string,
  &quot;source&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

## MetricxInput

Input for MetricX metric.

Fields

`metricSpec` ` object ( MetricxSpec  ` )

Required. Spec for Metricx metric.

`instance` ` object ( MetricxInstance  ` )

Required. Metricx instance.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;metricSpec&quot;: {object (MetricxSpec)},&quot;instance&quot;: {object (MetricxInstance)}}</code></pre></td>
</tr>
</tbody>
</table>

## MetricxSpec

Spec for MetricX metric.

Fields

`sourceLanguage` `string`

Optional. Source language in BCP-47 format.

`targetLanguage` `string`

Optional. Target language in BCP-47 format. Covers both prediction and reference.

`version` ` enum ( MetricxVersion  ` )

Required. Which version to use for evaluation.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;sourceLanguage&quot;: string,&quot;targetLanguage&quot;: string,&quot;version&quot;: enum (MetricxVersion)}</code></pre></td>
</tr>
</tbody>
</table>

## MetricxVersion

MetricX version options.

Enums

`METRICX_VERSION_UNSPECIFIED`

MetricX version unspecified.

`METRICX_24_REF`

MetricX 2024 (2.6) for translation + reference (reference-based).

`METRICX_24_SRC`

MetricX 2024 (2.6) for translation + source (QE).

`METRICX_24_SRC_REF`

MetricX 2024 (2.6) for translation + source + reference (source-reference-combined).

## MetricxInstance

Spec for MetricX instance - The fields used for evaluation are dependent on the MetricX version.

Fields

`prediction` `string`

Required. Output of the evaluated model.

`reference` `string`

Optional. Ground truth used to compare against the prediction.

`source` `string`

Optional. Source text in original language.

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
  &quot;prediction&quot;: string,
  &quot;reference&quot;: string,
  &quot;source&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

## TrajectoryExactMatchInput

Instances and metric spec for TrajectoryExactMatch metric.

Fields

`metricSpec` ` object ( TrajectoryExactMatchSpec  ` )

Required. Spec for TrajectoryExactMatch metric.

`instances[]` ` object ( TrajectoryExactMatchInstance  ` )

Required. Repeated TrajectoryExactMatch instance.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;metricSpec&quot;: {object (TrajectoryExactMatchSpec)},&quot;instances&quot;: [{object (TrajectoryExactMatchInstance)}]}</code></pre></td>
</tr>
</tbody>
</table>

## TrajectoryExactMatchSpec

This type has no fields.

Spec for TrajectoryExactMatch metric - returns 1 if tool calls in the reference trajectory exactly match the predicted trajectory, else 0.

## TrajectoryExactMatchInstance

Spec for TrajectoryExactMatch instance.

Fields

`predictedTrajectory` ` object ( Trajectory  ` )

Required. Spec for predicted tool call trajectory.

`referenceTrajectory` ` object ( Trajectory  ` )

Required. Spec for reference tool call trajectory.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;predictedTrajectory&quot;: {object (Trajectory)},&quot;referenceTrajectory&quot;: {object (Trajectory)}}</code></pre></td>
</tr>
</tbody>
</table>

## Trajectory

Spec for trajectory.

Fields

`toolCalls[]` ` object ( ToolCall  ` )

Required. Tool calls in the trajectory.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;toolCalls&quot;: [{object (ToolCall)}]}</code></pre></td>
</tr>
</tbody>
</table>

## ToolCall

Spec for tool call.

Fields

`toolName` `string`

Required. Spec for tool name

`toolInput` `string`

Optional. Spec for tool input

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
  &quot;toolName&quot;: string,
  &quot;toolInput&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

## TrajectoryInOrderMatchInput

Instances and metric spec for TrajectoryInOrderMatch metric.

Fields

`metricSpec` ` object ( TrajectoryInOrderMatchSpec  ` )

Required. Spec for TrajectoryInOrderMatch metric.

`instances[]` ` object ( TrajectoryInOrderMatchInstance  ` )

Required. Repeated TrajectoryInOrderMatch instance.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;metricSpec&quot;: {object (TrajectoryInOrderMatchSpec)},&quot;instances&quot;: [{object (TrajectoryInOrderMatchInstance)}]}</code></pre></td>
</tr>
</tbody>
</table>

## TrajectoryInOrderMatchSpec

This type has no fields.

Spec for TrajectoryInOrderMatch metric - returns 1 if tool calls in the reference trajectory appear in the predicted trajectory in the same order, else 0.

## TrajectoryInOrderMatchInstance

Spec for TrajectoryInOrderMatch instance.

Fields

`predictedTrajectory` ` object ( Trajectory  ` )

Required. Spec for predicted tool call trajectory.

`referenceTrajectory` ` object ( Trajectory  ` )

Required. Spec for reference tool call trajectory.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;predictedTrajectory&quot;: {object (Trajectory)},&quot;referenceTrajectory&quot;: {object (Trajectory)}}</code></pre></td>
</tr>
</tbody>
</table>

## TrajectoryAnyOrderMatchInput

Instances and metric spec for TrajectoryAnyOrderMatch metric.

Fields

`metricSpec` ` object ( TrajectoryAnyOrderMatchSpec  ` )

Required. Spec for TrajectoryAnyOrderMatch metric.

`instances[]` ` object ( TrajectoryAnyOrderMatchInstance  ` )

Required. Repeated TrajectoryAnyOrderMatch instance.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;metricSpec&quot;: {object (TrajectoryAnyOrderMatchSpec)},&quot;instances&quot;: [{object (TrajectoryAnyOrderMatchInstance)}]}</code></pre></td>
</tr>
</tbody>
</table>

## TrajectoryAnyOrderMatchSpec

This type has no fields.

Spec for TrajectoryAnyOrderMatch metric - returns 1 if all tool calls in the reference trajectory appear in the predicted trajectory in any order, else 0.

## TrajectoryAnyOrderMatchInstance

Spec for TrajectoryAnyOrderMatch instance.

Fields

`predictedTrajectory` ` object ( Trajectory  ` )

Required. Spec for predicted tool call trajectory.

`referenceTrajectory` ` object ( Trajectory  ` )

Required. Spec for reference tool call trajectory.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;predictedTrajectory&quot;: {object (Trajectory)},&quot;referenceTrajectory&quot;: {object (Trajectory)}}</code></pre></td>
</tr>
</tbody>
</table>

## TrajectoryPrecisionInput

Instances and metric spec for TrajectoryPrecision metric.

Fields

`metricSpec` ` object ( TrajectoryPrecisionSpec  ` )

Required. Spec for TrajectoryPrecision metric.

`instances[]` ` object ( TrajectoryPrecisionInstance  ` )

Required. Repeated TrajectoryPrecision instance.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;metricSpec&quot;: {object (TrajectoryPrecisionSpec)},&quot;instances&quot;: [{object (TrajectoryPrecisionInstance)}]}</code></pre></td>
</tr>
</tbody>
</table>

## TrajectoryPrecisionSpec

This type has no fields.

Spec for TrajectoryPrecision metric - returns a float score based on average precision of individual tool calls.

## TrajectoryPrecisionInstance

Spec for TrajectoryPrecision instance.

Fields

`predictedTrajectory` ` object ( Trajectory  ` )

Required. Spec for predicted tool call trajectory.

`referenceTrajectory` ` object ( Trajectory  ` )

Required. Spec for reference tool call trajectory.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;predictedTrajectory&quot;: {object (Trajectory)},&quot;referenceTrajectory&quot;: {object (Trajectory)}}</code></pre></td>
</tr>
</tbody>
</table>

## TrajectoryRecallInput

Instances and metric spec for TrajectoryRecall metric.

Fields

`metricSpec` ` object ( TrajectoryRecallSpec  ` )

Required. Spec for TrajectoryRecall metric.

`instances[]` ` object ( TrajectoryRecallInstance  ` )

Required. Repeated TrajectoryRecall instance.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;metricSpec&quot;: {object (TrajectoryRecallSpec)},&quot;instances&quot;: [{object (TrajectoryRecallInstance)}]}</code></pre></td>
</tr>
</tbody>
</table>

## TrajectoryRecallSpec

This type has no fields.

Spec for TrajectoryRecall metric - returns a float score based on average recall of individual tool calls.

## TrajectoryRecallInstance

Spec for TrajectoryRecall instance.

Fields

`predictedTrajectory` ` object ( Trajectory  ` )

Required. Spec for predicted tool call trajectory.

`referenceTrajectory` ` object ( Trajectory  ` )

Required. Spec for reference tool call trajectory.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;predictedTrajectory&quot;: {object (Trajectory)},&quot;referenceTrajectory&quot;: {object (Trajectory)}}</code></pre></td>
</tr>
</tbody>
</table>

## TrajectorySingleToolUseInput

Instances and metric spec for TrajectorySingleToolUse metric.

Fields

`metricSpec` ` object ( TrajectorySingleToolUseSpec  ` )

Required. Spec for TrajectorySingleToolUse metric.

`instances[]` ` object ( TrajectorySingleToolUseInstance  ` )

Required. Repeated TrajectorySingleToolUse instance.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;metricSpec&quot;: {object (TrajectorySingleToolUseSpec)},&quot;instances&quot;: [{object (TrajectorySingleToolUseInstance)}]}</code></pre></td>
</tr>
</tbody>
</table>

## TrajectorySingleToolUseSpec

Spec for TrajectorySingleToolUse metric - returns 1 if tool is present in the predicted trajectory, else 0.

Fields

`toolName` `string`

Required. Spec for tool name to be checked for in the predicted trajectory.

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
  &quot;toolName&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

## TrajectorySingleToolUseInstance

Spec for TrajectorySingleToolUse instance.

Fields

`predictedTrajectory` ` object ( Trajectory  ` )

Required. Spec for predicted tool call trajectory.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;predictedTrajectory&quot;: {object (Trajectory)}}</code></pre></td>
</tr>
</tbody>
</table>

## ExactMatchResults

Results for exact match metric.

Fields

`exactMatchMetricValues[]` ` object ( ExactMatchMetricValue  ` )

Output only. Exact match metric values.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;exactMatchMetricValues&quot;: [{object (ExactMatchMetricValue)}]}</code></pre></td>
</tr>
</tbody>
</table>

## BleuResults

Results for bleu metric.

Fields

`bleuMetricValues[]` ` object ( BleuMetricValue  ` )

Output only. Bleu metric values.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;bleuMetricValues&quot;: [{object (BleuMetricValue)}]}</code></pre></td>
</tr>
</tbody>
</table>

## RougeResults

Results for rouge metric.

Fields

`rougeMetricValues[]` ` object ( RougeMetricValue  ` )

Output only. Rouge metric values.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;rougeMetricValues&quot;: [{object (RougeMetricValue)}]}</code></pre></td>
</tr>
</tbody>
</table>

## FluencyResult

Spec for fluency result.

Fields

`explanation` `string`

Output only. Explanation for fluency score.

`score` `number`

Output only. Fluency score.

`confidence` `number`

Output only. confidence for fluency score.

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
  &quot;explanation&quot;: string,
  &quot;score&quot;: number,
  &quot;confidence&quot;: number
}</code></pre></td>
</tr>
</tbody>
</table>

## CoherenceResult

Spec for coherence result.

Fields

`explanation` `string`

Output only. Explanation for coherence score.

`score` `number`

Output only. Coherence score.

`confidence` `number`

Output only. confidence for coherence score.

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
  &quot;explanation&quot;: string,
  &quot;score&quot;: number,
  &quot;confidence&quot;: number
}</code></pre></td>
</tr>
</tbody>
</table>

## SafetyResult

Spec for safety result.

Fields

`explanation` `string`

Output only. Explanation for safety score.

`score` `number`

Output only. Safety score.

`confidence` `number`

Output only. confidence for safety score.

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
  &quot;explanation&quot;: string,
  &quot;score&quot;: number,
  &quot;confidence&quot;: number
}</code></pre></td>
</tr>
</tbody>
</table>

## GroundednessResult

Spec for groundedness result.

Fields

`explanation` `string`

Output only. Explanation for groundedness score.

`score` `number`

Output only. Groundedness score.

`confidence` `number`

Output only. confidence for groundedness score.

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
  &quot;explanation&quot;: string,
  &quot;score&quot;: number,
  &quot;confidence&quot;: number
}</code></pre></td>
</tr>
</tbody>
</table>

## FulfillmentResult

Spec for fulfillment result.

Fields

`explanation` `string`

Output only. Explanation for fulfillment score.

`score` `number`

Output only. Fulfillment score.

`confidence` `number`

Output only. confidence for fulfillment score.

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
  &quot;explanation&quot;: string,
  &quot;score&quot;: number,
  &quot;confidence&quot;: number
}</code></pre></td>
</tr>
</tbody>
</table>

## SummarizationQualityResult

Spec for summarization quality result.

Fields

`explanation` `string`

Output only. Explanation for summarization quality score.

`score` `number`

Output only. Summarization Quality score.

`confidence` `number`

Output only. confidence for summarization quality score.

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
  &quot;explanation&quot;: string,
  &quot;score&quot;: number,
  &quot;confidence&quot;: number
}</code></pre></td>
</tr>
</tbody>
</table>

## PairwiseSummarizationQualityResult

Spec for pairwise summarization quality result.

Fields

`pairwiseChoice` ` enum ( PairwiseChoice  ` )

Output only. Pairwise summarization prediction choice.

`explanation` `string`

Output only. Explanation for summarization quality score.

`confidence` `number`

Output only. confidence for summarization quality score.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;pairwiseChoice&quot;: enum (PairwiseChoice),&quot;explanation&quot;: string,&quot;confidence&quot;: number}</code></pre></td>
</tr>
</tbody>
</table>

## SummarizationHelpfulnessResult

Spec for summarization helpfulness result.

Fields

`explanation` `string`

Output only. Explanation for summarization helpfulness score.

`score` `number`

Output only. Summarization Helpfulness score.

`confidence` `number`

Output only. confidence for summarization helpfulness score.

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
  &quot;explanation&quot;: string,
  &quot;score&quot;: number,
  &quot;confidence&quot;: number
}</code></pre></td>
</tr>
</tbody>
</table>

## SummarizationVerbosityResult

Spec for summarization verbosity result.

Fields

`explanation` `string`

Output only. Explanation for summarization verbosity score.

`score` `number`

Output only. Summarization Verbosity score.

`confidence` `number`

Output only. confidence for summarization verbosity score.

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
  &quot;explanation&quot;: string,
  &quot;score&quot;: number,
  &quot;confidence&quot;: number
}</code></pre></td>
</tr>
</tbody>
</table>

## QuestionAnsweringQualityResult

Spec for question answering quality result.

Fields

`explanation` `string`

Output only. Explanation for question answering quality score.

`score` `number`

Output only. Question Answering Quality score.

`confidence` `number`

Output only. confidence for question answering quality score.

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
  &quot;explanation&quot;: string,
  &quot;score&quot;: number,
  &quot;confidence&quot;: number
}</code></pre></td>
</tr>
</tbody>
</table>

## PairwiseQuestionAnsweringQualityResult

Spec for pairwise question answering quality result.

Fields

`pairwiseChoice` ` enum ( PairwiseChoice  ` )

Output only. Pairwise question answering prediction choice.

`explanation` `string`

Output only. Explanation for question answering quality score.

`confidence` `number`

Output only. confidence for question answering quality score.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;pairwiseChoice&quot;: enum (PairwiseChoice),&quot;explanation&quot;: string,&quot;confidence&quot;: number}</code></pre></td>
</tr>
</tbody>
</table>

## QuestionAnsweringRelevanceResult

Spec for question answering relevance result.

Fields

`explanation` `string`

Output only. Explanation for question answering relevance score.

`score` `number`

Output only. Question Answering Relevance score.

`confidence` `number`

Output only. confidence for question answering relevance score.

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
  &quot;explanation&quot;: string,
  &quot;score&quot;: number,
  &quot;confidence&quot;: number
}</code></pre></td>
</tr>
</tbody>
</table>

## QuestionAnsweringHelpfulnessResult

Spec for question answering helpfulness result.

Fields

`explanation` `string`

Output only. Explanation for question answering helpfulness score.

`score` `number`

Output only. Question Answering Helpfulness score.

`confidence` `number`

Output only. confidence for question answering helpfulness score.

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
  &quot;explanation&quot;: string,
  &quot;score&quot;: number,
  &quot;confidence&quot;: number
}</code></pre></td>
</tr>
</tbody>
</table>

## QuestionAnsweringCorrectnessResult

Spec for question answering correctness result.

Fields

`explanation` `string`

Output only. Explanation for question answering correctness score.

`score` `number`

Output only. Question Answering Correctness score.

`confidence` `number`

Output only. confidence for question answering correctness score.

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
  &quot;explanation&quot;: string,
  &quot;score&quot;: number,
  &quot;confidence&quot;: number
}</code></pre></td>
</tr>
</tbody>
</table>

## ToolCallValidResults

Results for tool call valid metric.

Fields

`toolCallValidMetricValues[]` ` object ( ToolCallValidMetricValue  ` )

Output only. Tool call valid metric values.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;toolCallValidMetricValues&quot;: [{object (ToolCallValidMetricValue)}]}</code></pre></td>
</tr>
</tbody>
</table>

## ToolCallValidMetricValue

Tool call valid metric value for an instance.

Fields

`score` `number`

Output only. Tool call valid score.

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
  &quot;score&quot;: number
}</code></pre></td>
</tr>
</tbody>
</table>

## ToolNameMatchResults

Results for tool name match metric.

Fields

`toolNameMatchMetricValues[]` ` object ( ToolNameMatchMetricValue  ` )

Output only. Tool name match metric values.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;toolNameMatchMetricValues&quot;: [{object (ToolNameMatchMetricValue)}]}</code></pre></td>
</tr>
</tbody>
</table>

## ToolNameMatchMetricValue

Tool name match metric value for an instance.

Fields

`score` `number`

Output only. Tool name match score.

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
  &quot;score&quot;: number
}</code></pre></td>
</tr>
</tbody>
</table>

## ToolParameterKeyMatchResults

Results for tool parameter key match metric.

Fields

`toolParameterKeyMatchMetricValues[]` ` object ( ToolParameterKeyMatchMetricValue  ` )

Output only. Tool parameter key match metric values.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;toolParameterKeyMatchMetricValues&quot;: [{object (ToolParameterKeyMatchMetricValue)}]}</code></pre></td>
</tr>
</tbody>
</table>

## ToolParameterKeyMatchMetricValue

Tool parameter key match metric value for an instance.

Fields

`score` `number`

Output only. Tool parameter key match score.

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
  &quot;score&quot;: number
}</code></pre></td>
</tr>
</tbody>
</table>

## ToolParameterKVMatchResults

Results for tool parameter key value match metric.

Fields

`toolParameterKvMatchMetricValues[]` ` object ( ToolParameterKVMatchMetricValue  ` )

Output only. Tool parameter key value match metric values.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;toolParameterKvMatchMetricValues&quot;: [{object (ToolParameterKVMatchMetricValue)}]}</code></pre></td>
</tr>
</tbody>
</table>

## ToolParameterKVMatchMetricValue

Tool parameter key value match metric value for an instance.

Fields

`score` `number`

Output only. Tool parameter key value match score.

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
  &quot;score&quot;: number
}</code></pre></td>
</tr>
</tbody>
</table>

## CometResult

Spec for Comet result - calculates the comet score for the given instance using the version specified in the spec.

Fields

`score` `number`

Output only. Comet score. Range depends on version.

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
  &quot;score&quot;: number
}</code></pre></td>
</tr>
</tbody>
</table>

## MetricxResult

Spec for MetricX result - calculates the MetricX score for the given instance using the version specified in the spec.

Fields

`score` `number`

Output only. MetricX score. Range depends on version.

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
  &quot;score&quot;: number
}</code></pre></td>
</tr>
</tbody>
</table>

## TrajectoryExactMatchResults

Results for TrajectoryExactMatch metric.

Fields

`trajectoryExactMatchMetricValues[]` ` object ( TrajectoryExactMatchMetricValue  ` )

Output only. TrajectoryExactMatch metric values.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;trajectoryExactMatchMetricValues&quot;: [{object (TrajectoryExactMatchMetricValue)}]}</code></pre></td>
</tr>
</tbody>
</table>

## TrajectoryExactMatchMetricValue

TrajectoryExactMatch metric value for an instance.

Fields

`score` `number`

Output only. TrajectoryExactMatch score.

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
  &quot;score&quot;: number
}</code></pre></td>
</tr>
</tbody>
</table>

## TrajectoryInOrderMatchResults

Results for TrajectoryInOrderMatch metric.

Fields

`trajectoryInOrderMatchMetricValues[]` ` object ( TrajectoryInOrderMatchMetricValue  ` )

Output only. TrajectoryInOrderMatch metric values.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;trajectoryInOrderMatchMetricValues&quot;: [{object (TrajectoryInOrderMatchMetricValue)}]}</code></pre></td>
</tr>
</tbody>
</table>

## TrajectoryInOrderMatchMetricValue

TrajectoryInOrderMatch metric value for an instance.

Fields

`score` `number`

Output only. TrajectoryInOrderMatch score.

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
  &quot;score&quot;: number
}</code></pre></td>
</tr>
</tbody>
</table>

## TrajectoryAnyOrderMatchResults

Results for TrajectoryAnyOrderMatch metric.

Fields

`trajectoryAnyOrderMatchMetricValues[]` ` object ( TrajectoryAnyOrderMatchMetricValue  ` )

Output only. TrajectoryAnyOrderMatch metric values.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;trajectoryAnyOrderMatchMetricValues&quot;: [{object (TrajectoryAnyOrderMatchMetricValue)}]}</code></pre></td>
</tr>
</tbody>
</table>

## TrajectoryAnyOrderMatchMetricValue

TrajectoryAnyOrderMatch metric value for an instance.

Fields

`score` `number`

Output only. TrajectoryAnyOrderMatch score.

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
  &quot;score&quot;: number
}</code></pre></td>
</tr>
</tbody>
</table>

## TrajectoryPrecisionResults

Results for TrajectoryPrecision metric.

Fields

`trajectoryPrecisionMetricValues[]` ` object ( TrajectoryPrecisionMetricValue  ` )

Output only. TrajectoryPrecision metric values.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;trajectoryPrecisionMetricValues&quot;: [{object (TrajectoryPrecisionMetricValue)}]}</code></pre></td>
</tr>
</tbody>
</table>

## TrajectoryPrecisionMetricValue

TrajectoryPrecision metric value for an instance.

Fields

`score` `number`

Output only. TrajectoryPrecision score.

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
  &quot;score&quot;: number
}</code></pre></td>
</tr>
</tbody>
</table>

## TrajectoryRecallResults

Results for TrajectoryRecall metric.

Fields

`trajectoryRecallMetricValues[]` ` object ( TrajectoryRecallMetricValue  ` )

Output only. TrajectoryRecall metric values.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;trajectoryRecallMetricValues&quot;: [{object (TrajectoryRecallMetricValue)}]}</code></pre></td>
</tr>
</tbody>
</table>

## TrajectoryRecallMetricValue

TrajectoryRecall metric value for an instance.

Fields

`score` `number`

Output only. TrajectoryRecall score.

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
  &quot;score&quot;: number
}</code></pre></td>
</tr>
</tbody>
</table>

## TrajectorySingleToolUseResults

Results for TrajectorySingleToolUse metric.

Fields

`trajectorySingleToolUseMetricValues[]` ` object ( TrajectorySingleToolUseMetricValue  ` )

Output only. TrajectorySingleToolUse metric values.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;trajectorySingleToolUseMetricValues&quot;: [{object (TrajectorySingleToolUseMetricValue)}]}</code></pre></td>
</tr>
</tbody>
</table>

## TrajectorySingleToolUseMetricValue

TrajectorySingleToolUse metric value for an instance.

Fields

`score` `number`

Output only. TrajectorySingleToolUse score.

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
  &quot;score&quot;: number
}</code></pre></td>
</tr>
</tbody>
</table>

## MetricResult

result for a single metric on a single instance.

Fields

`score` `number`

Output only. The score for the metric. Please refer to each metric's documentation for the meaning of the score.

`explanation` `string`

Output only. The explanation for the metric result.

`error` ` object ( Status  ` )

Output only. The error status for the metric result.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;score&quot;: number,&quot;explanation&quot;: string,&quot;error&quot;: {object (Status)}}</code></pre></td>
</tr>
</tbody>
</table>
