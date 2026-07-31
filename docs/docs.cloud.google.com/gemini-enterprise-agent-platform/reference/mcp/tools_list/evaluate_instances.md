---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances
title: 'MCP Tools Reference: aiplatform.googleapis.com'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

## Tool: `evaluate_instances`

Evaluates instances based on a given metric. Use this to perform online evaluation of model responses using metrics like fluency, coherence, safety, and more.

The following sample demonstrate how to use `curl` to invoke the `evaluate_instances` MCP tool.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>Curl Request</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" data-syntax="Bash" translate="no"><code>                  
curl --location &#39;https://aiplatform.googleapis.com/mcp/generate&#39; \
--header &#39;content-type: application/json&#39; \
--header &#39;accept: application/json, text/event-stream&#39; \
--data &#39;{
  &quot;method&quot;: &quot;tools/call&quot;,
  &quot;params&quot;: {
    &quot;name&quot;: &quot;evaluate_instances&quot;,
    &quot;arguments&quot;: {
      // provide these details according to the tool&#39;s MCP specification
    }
  },
  &quot;jsonrpc&quot;: &quot;2.0&quot;,
  &quot;id&quot;: 1
}&#39;
                </code></pre></td>
</tr>
</tbody>
</table>

## Input Schema

Request message for EvaluationService.EvaluateInstances.

### EvaluateInstancesRequest

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;location&quot;: string,&quot;metrics&quot;: [{object (Metric)}],&quot;metricSources&quot;: [{object (MetricSource)}],&quot;instance&quot;: {object (EvaluationInstance)},&quot;autoraterConfig&quot;: {object (AutoraterConfig)},// Union field metric_inputs can be only one of the following:&quot;exactMatchInput&quot;: {object (ExactMatchInput)},&quot;bleuInput&quot;: {object (BleuInput)},&quot;rougeInput&quot;: {object (RougeInput)},&quot;fluencyInput&quot;: {object (FluencyInput)},&quot;coherenceInput&quot;: {object (CoherenceInput)},&quot;safetyInput&quot;: {object (SafetyInput)},&quot;groundednessInput&quot;: {object (GroundednessInput)},&quot;fulfillmentInput&quot;: {object (FulfillmentInput)},&quot;summarizationQualityInput&quot;: {object (SummarizationQualityInput)},&quot;pairwiseSummarizationQualityInput&quot;: {object (PairwiseSummarizationQualityInput)},&quot;summarizationHelpfulnessInput&quot;: {object (SummarizationHelpfulnessInput)},&quot;summarizationVerbosityInput&quot;: {object (SummarizationVerbosityInput)},&quot;questionAnsweringQualityInput&quot;: {object (QuestionAnsweringQualityInput)},&quot;pairwiseQuestionAnsweringQualityInput&quot;: {object (PairwiseQuestionAnsweringQualityInput)},&quot;questionAnsweringRelevanceInput&quot;: {object (QuestionAnsweringRelevanceInput)},&quot;questionAnsweringHelpfulnessInput&quot;: {object (QuestionAnsweringHelpfulnessInput)},&quot;questionAnsweringCorrectnessInput&quot;: {object (QuestionAnsweringCorrectnessInput)},&quot;pointwiseMetricInput&quot;: {object (PointwiseMetricInput)},&quot;pairwiseMetricInput&quot;: {object (PairwiseMetricInput)},&quot;toolCallValidInput&quot;: {object (ToolCallValidInput)},&quot;toolNameMatchInput&quot;: {object (ToolNameMatchInput)},&quot;toolParameterKeyMatchInput&quot;: {object (ToolParameterKeyMatchInput)},&quot;toolParameterKvMatchInput&quot;: {object (ToolParameterKVMatchInput)},&quot;cometInput&quot;: {object (CometInput)},&quot;metricxInput&quot;: {object (MetricxInput)},&quot;trajectoryExactMatchInput&quot;: {object (TrajectoryExactMatchInput)},&quot;trajectoryInOrderMatchInput&quot;: {object (TrajectoryInOrderMatchInput)},&quot;trajectoryAnyOrderMatchInput&quot;: {object (TrajectoryAnyOrderMatchInput)},&quot;trajectoryPrecisionInput&quot;: {object (TrajectoryPrecisionInput)},&quot;trajectoryRecallInput&quot;: {object (TrajectoryRecallInput)},&quot;trajectorySingleToolUseInput&quot;: {object (TrajectorySingleToolUseInput)},&quot;rubricBasedInstructionFollowingInput&quot;: {object (RubricBasedInstructionFollowingInput)}// End of list of possible types for union field metric_inputs.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`location`

`string`

Required. The resource name of the Location to evaluate the instances. Format: `projects/{project}/locations/{location}`

`metrics[]`

` object ( Metric  ` )

The metrics used for evaluation. Currently, we only support evaluating a single metric. If multiple metrics are provided, only the first one will be evaluated.

`metricSources[]`

` object ( MetricSource  ` )

Optional. The metrics (either inline or registered) used for evaluation. Currently, we only support evaluating a single metric. If multiple metrics are provided, only the first one will be evaluated.

`instance`

` object ( EvaluationInstance  ` )

The instance to be evaluated.

`autoraterConfig`

` object ( AutoraterConfig  ` )

Optional. Autorater config used for evaluation. Not applicable for predefined metrics (PredefinedMetricSpec); the server uses its own model configuration for predefined metrics and this field is ignored.

Union field `metric_inputs` . Instances and specs for evaluation `metric_inputs` can be only one of the following:

`exactMatchInput`

` object ( ExactMatchInput  ` )

Auto metric instances. Instances and metric spec for exact match metric.

`bleuInput`

` object ( BleuInput  ` )

Instances and metric spec for bleu metric.

`rougeInput`

` object ( RougeInput  ` )

Instances and metric spec for rouge metric.

`fluencyInput`

` object ( FluencyInput  ` )

LLM-based metric instance. General text generation metrics, applicable to other categories. Input for fluency metric.

`coherenceInput`

` object ( CoherenceInput  ` )

Input for coherence metric.

`safetyInput`

` object ( SafetyInput  ` )

Input for safety metric.

`groundednessInput`

` object ( GroundednessInput  ` )

Input for groundedness metric.

`fulfillmentInput`

` object ( FulfillmentInput  ` )

Input for fulfillment metric.

`summarizationQualityInput`

` object ( SummarizationQualityInput  ` )

Input for summarization quality metric.

`pairwiseSummarizationQualityInput`

` object ( PairwiseSummarizationQualityInput  ` )

Input for pairwise summarization quality metric.

`summarizationHelpfulnessInput`

` object ( SummarizationHelpfulnessInput  ` )

Input for summarization helpfulness metric.

`summarizationVerbosityInput`

` object ( SummarizationVerbosityInput  ` )

Input for summarization verbosity metric.

`questionAnsweringQualityInput`

` object ( QuestionAnsweringQualityInput  ` )

Input for question answering quality metric.

`pairwiseQuestionAnsweringQualityInput`

` object ( PairwiseQuestionAnsweringQualityInput  ` )

Input for pairwise question answering quality metric.

`questionAnsweringRelevanceInput`

` object ( QuestionAnsweringRelevanceInput  ` )

Input for question answering relevance metric.

`questionAnsweringHelpfulnessInput`

` object ( QuestionAnsweringHelpfulnessInput  ` )

Input for question answering helpfulness metric.

`questionAnsweringCorrectnessInput`

` object ( QuestionAnsweringCorrectnessInput  ` )

Input for question answering correctness metric.

`pointwiseMetricInput`

` object ( PointwiseMetricInput  ` )

Input for pointwise metric.

`pairwiseMetricInput`

` object ( PairwiseMetricInput  ` )

Input for pairwise metric.

`toolCallValidInput`

` object ( ToolCallValidInput  ` )

Tool call metric instances. Input for tool call valid metric.

`toolNameMatchInput`

` object ( ToolNameMatchInput  ` )

Input for tool name match metric.

`toolParameterKeyMatchInput`

` object ( ToolParameterKeyMatchInput  ` )

Input for tool parameter key match metric.

`toolParameterKvMatchInput`

` object ( ToolParameterKVMatchInput  ` )

Input for tool parameter key value match metric.

`cometInput`

` object ( CometInput  ` )

Translation metrics. Input for Comet metric.

`metricxInput`

` object ( MetricxInput  ` )

Input for Metricx metric.

`trajectoryExactMatchInput`

` object ( TrajectoryExactMatchInput  ` )

Input for trajectory exact match metric.

`trajectoryInOrderMatchInput`

` object ( TrajectoryInOrderMatchInput  ` )

Input for trajectory in order match metric.

`trajectoryAnyOrderMatchInput`

` object ( TrajectoryAnyOrderMatchInput  ` )

Input for trajectory match any order metric.

`trajectoryPrecisionInput`

` object ( TrajectoryPrecisionInput  ` )

Input for trajectory precision metric.

`trajectoryRecallInput`

` object ( TrajectoryRecallInput  ` )

Input for trajectory recall metric.

`trajectorySingleToolUseInput`

` object ( TrajectorySingleToolUseInput  ` )

Input for trajectory single tool use metric.

`rubricBasedInstructionFollowingInput`

` object ( RubricBasedInstructionFollowingInput  ` )

Rubric Based Instruction Following metric.

### ExactMatchInput

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

Fields

`metricSpec`

`object ( ExactMatchSpec` )

Required. Spec for exact match metric.

`instances[]`

` object ( ExactMatchInstance  ` )

Required. Repeated exact match instances.

### ExactMatchInstance

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{// Union field _prediction can be only one of the following:&quot;prediction&quot;: string// End of list of possible types for union field _prediction.// Union field _reference can be only one of the following:&quot;reference&quot;: string// End of list of possible types for union field _reference.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

Union field `_prediction` .

`_prediction` can be only one of the following:

`prediction`

`string`

Required. Output of the evaluated model.

Union field `_reference` .

`_reference` can be only one of the following:

`reference`

`string`

Required. Ground truth used to compare against the prediction.

### BleuInput

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

Fields

`metricSpec`

` object ( BleuSpec  ` )

Required. Spec for bleu score metric.

`instances[]`

` object ( BleuInstance  ` )

Required. Repeated bleu instances.

### BleuSpec

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

Fields

`useEffectiveOrder`

`boolean`

Optional. Whether to use\_effective\_order to compute bleu score.

### BleuInstance

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{// Union field _prediction can be only one of the following:&quot;prediction&quot;: string// End of list of possible types for union field _prediction.// Union field _reference can be only one of the following:&quot;reference&quot;: string// End of list of possible types for union field _reference.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

Union field `_prediction` .

`_prediction` can be only one of the following:

`prediction`

`string`

Required. Output of the evaluated model.

Union field `_reference` .

`_reference` can be only one of the following:

`reference`

`string`

Required. Ground truth used to compare against the prediction.

### RougeInput

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

Fields

`metricSpec`

` object ( RougeSpec  ` )

Required. Spec for rouge score metric.

`instances[]`

` object ( RougeInstance  ` )

Required. Repeated rouge instances.

### RougeSpec

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

Fields

`rougeType`

`string`

Optional. Supported rouge types are rougen\[1-9\], rougeL, and rougeLsum.

`useStemmer`

`boolean`

Optional. Whether to use stemmer to compute rouge score.

`splitSummaries`

`boolean`

Optional. Whether to split summaries while using rougeLsum.

### RougeInstance

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{// Union field _prediction can be only one of the following:&quot;prediction&quot;: string// End of list of possible types for union field _prediction.// Union field _reference can be only one of the following:&quot;reference&quot;: string// End of list of possible types for union field _reference.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

Union field `_prediction` .

`_prediction` can be only one of the following:

`prediction`

`string`

Required. Output of the evaluated model.

Union field `_reference` .

`_reference` can be only one of the following:

`reference`

`string`

Required. Ground truth used to compare against the prediction.

### FluencyInput

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

Fields

`metricSpec`

` object ( FluencySpec  ` )

Required. Spec for fluency score metric.

`instance`

` object ( FluencyInstance  ` )

Required. Fluency instance.

### FluencySpec

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

Fields

`version`

`integer`

Optional. Which version to use for evaluation.

### FluencyInstance

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{// Union field _prediction can be only one of the following:&quot;prediction&quot;: string// End of list of possible types for union field _prediction.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

Union field `_prediction` .

`_prediction` can be only one of the following:

`prediction`

`string`

Required. Output of the evaluated model.

### CoherenceInput

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

Fields

`metricSpec`

` object ( CoherenceSpec  ` )

Required. Spec for coherence score metric.

`instance`

` object ( CoherenceInstance  ` )

Required. Coherence instance.

### CoherenceSpec

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

Fields

`version`

`integer`

Optional. Which version to use for evaluation.

### CoherenceInstance

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{// Union field _prediction can be only one of the following:&quot;prediction&quot;: string// End of list of possible types for union field _prediction.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

Union field `_prediction` .

`_prediction` can be only one of the following:

`prediction`

`string`

Required. Output of the evaluated model.

### SafetyInput

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

Fields

`metricSpec`

` object ( SafetySpec  ` )

Required. Spec for safety metric.

`instance`

` object ( SafetyInstance  ` )

Required. Safety instance.

### SafetySpec

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

Fields

`version`

`integer`

Optional. Which version to use for evaluation.

### SafetyInstance

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{// Union field _prediction can be only one of the following:&quot;prediction&quot;: string// End of list of possible types for union field _prediction.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

Union field `_prediction` .

`_prediction` can be only one of the following:

`prediction`

`string`

Required. Output of the evaluated model.

### GroundednessInput

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

Fields

`metricSpec`

` object ( GroundednessSpec  ` )

Required. Spec for groundedness metric.

`instance`

` object ( GroundednessInstance  ` )

Required. Groundedness instance.

### GroundednessSpec

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

Fields

`version`

`integer`

Optional. Which version to use for evaluation.

### GroundednessInstance

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{// Union field _prediction can be only one of the following:&quot;prediction&quot;: string// End of list of possible types for union field _prediction.// Union field _context can be only one of the following:&quot;context&quot;: string// End of list of possible types for union field _context.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

Union field `_prediction` .

`_prediction` can be only one of the following:

`prediction`

`string`

Required. Output of the evaluated model.

Union field `_context` .

`_context` can be only one of the following:

`context`

`string`

Required. Background information provided in context used to compare against the prediction.

### FulfillmentInput

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

Fields

`metricSpec`

` object ( FulfillmentSpec  ` )

Required. Spec for fulfillment score metric.

`instance`

` object ( FulfillmentInstance  ` )

Required. Fulfillment instance.

### FulfillmentSpec

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

Fields

`version`

`integer`

Optional. Which version to use for evaluation.

### FulfillmentInstance

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{// Union field _prediction can be only one of the following:&quot;prediction&quot;: string// End of list of possible types for union field _prediction.// Union field _instruction can be only one of the following:&quot;instruction&quot;: string// End of list of possible types for union field _instruction.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

Union field `_prediction` .

`_prediction` can be only one of the following:

`prediction`

`string`

Required. Output of the evaluated model.

Union field `_instruction` .

`_instruction` can be only one of the following:

`instruction`

`string`

Required. Inference instruction prompt to compare prediction with.

### SummarizationQualityInput

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

Fields

`metricSpec`

` object ( SummarizationQualitySpec  ` )

Required. Spec for summarization quality score metric.

`instance`

` object ( SummarizationQualityInstance  ` )

Required. Summarization quality instance.

### SummarizationQualitySpec

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

Fields

`useReference`

`boolean`

Optional. Whether to use instance.reference to compute summarization quality.

`version`

`integer`

Optional. Which version to use for evaluation.

### SummarizationQualityInstance

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{// Union field _prediction can be only one of the following:&quot;prediction&quot;: string// End of list of possible types for union field _prediction.// Union field _reference can be only one of the following:&quot;reference&quot;: string// End of list of possible types for union field _reference.// Union field _context can be only one of the following:&quot;context&quot;: string// End of list of possible types for union field _context.// Union field _instruction can be only one of the following:&quot;instruction&quot;: string// End of list of possible types for union field _instruction.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

Union field `_prediction` .

`_prediction` can be only one of the following:

`prediction`

`string`

Required. Output of the evaluated model.

Union field `_reference` .

`_reference` can be only one of the following:

`reference`

`string`

Optional. Ground truth used to compare against the prediction.

Union field `_context` .

`_context` can be only one of the following:

`context`

`string`

Required. Text to be summarized.

Union field `_instruction` .

`_instruction` can be only one of the following:

`instruction`

`string`

Required. Summarization prompt for LLM.

### PairwiseSummarizationQualityInput

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

Fields

`metricSpec`

` object ( PairwiseSummarizationQualitySpec  ` )

Required. Spec for pairwise summarization quality score metric.

`instance`

` object ( PairwiseSummarizationQualityInstance  ` )

Required. Pairwise summarization quality instance.

### PairwiseSummarizationQualitySpec

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

Fields

`useReference`

`boolean`

Optional. Whether to use instance.reference to compute pairwise summarization quality.

`version`

`integer`

Optional. Which version to use for evaluation.

### PairwiseSummarizationQualityInstance

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{// Union field _prediction can be only one of the following:&quot;prediction&quot;: string// End of list of possible types for union field _prediction.// Union field _baseline_prediction can be only one of the following:&quot;baselinePrediction&quot;: string// End of list of possible types for union field _baseline_prediction.// Union field _reference can be only one of the following:&quot;reference&quot;: string// End of list of possible types for union field _reference.// Union field _context can be only one of the following:&quot;context&quot;: string// End of list of possible types for union field _context.// Union field _instruction can be only one of the following:&quot;instruction&quot;: string// End of list of possible types for union field _instruction.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

Union field `_prediction` .

`_prediction` can be only one of the following:

`prediction`

`string`

Required. Output of the candidate model.

Union field `_baseline_prediction` .

`_baseline_prediction` can be only one of the following:

`baselinePrediction`

`string`

Required. Output of the baseline model.

Union field `_reference` .

`_reference` can be only one of the following:

`reference`

`string`

Optional. Ground truth used to compare against the prediction.

Union field `_context` .

`_context` can be only one of the following:

`context`

`string`

Required. Text to be summarized.

Union field `_instruction` .

`_instruction` can be only one of the following:

`instruction`

`string`

Required. Summarization prompt for LLM.

### SummarizationHelpfulnessInput

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

Fields

`metricSpec`

` object ( SummarizationHelpfulnessSpec  ` )

Required. Spec for summarization helpfulness score metric.

`instance`

` object ( SummarizationHelpfulnessInstance  ` )

Required. Summarization helpfulness instance.

### SummarizationHelpfulnessSpec

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

Fields

`useReference`

`boolean`

Optional. Whether to use instance.reference to compute summarization helpfulness.

`version`

`integer`

Optional. Which version to use for evaluation.

### SummarizationHelpfulnessInstance

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{// Union field _prediction can be only one of the following:&quot;prediction&quot;: string// End of list of possible types for union field _prediction.// Union field _reference can be only one of the following:&quot;reference&quot;: string// End of list of possible types for union field _reference.// Union field _context can be only one of the following:&quot;context&quot;: string// End of list of possible types for union field _context.// Union field _instruction can be only one of the following:&quot;instruction&quot;: string// End of list of possible types for union field _instruction.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

Union field `_prediction` .

`_prediction` can be only one of the following:

`prediction`

`string`

Required. Output of the evaluated model.

Union field `_reference` .

`_reference` can be only one of the following:

`reference`

`string`

Optional. Ground truth used to compare against the prediction.

Union field `_context` .

`_context` can be only one of the following:

`context`

`string`

Required. Text to be summarized.

Union field `_instruction` .

`_instruction` can be only one of the following:

`instruction`

`string`

Optional. Summarization prompt for LLM.

### SummarizationVerbosityInput

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

Fields

`metricSpec`

` object ( SummarizationVerbositySpec  ` )

Required. Spec for summarization verbosity score metric.

`instance`

` object ( SummarizationVerbosityInstance  ` )

Required. Summarization verbosity instance.

### SummarizationVerbositySpec

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

Fields

`useReference`

`boolean`

Optional. Whether to use instance.reference to compute summarization verbosity.

`version`

`integer`

Optional. Which version to use for evaluation.

### SummarizationVerbosityInstance

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{// Union field _prediction can be only one of the following:&quot;prediction&quot;: string// End of list of possible types for union field _prediction.// Union field _reference can be only one of the following:&quot;reference&quot;: string// End of list of possible types for union field _reference.// Union field _context can be only one of the following:&quot;context&quot;: string// End of list of possible types for union field _context.// Union field _instruction can be only one of the following:&quot;instruction&quot;: string// End of list of possible types for union field _instruction.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

Union field `_prediction` .

`_prediction` can be only one of the following:

`prediction`

`string`

Required. Output of the evaluated model.

Union field `_reference` .

`_reference` can be only one of the following:

`reference`

`string`

Optional. Ground truth used to compare against the prediction.

Union field `_context` .

`_context` can be only one of the following:

`context`

`string`

Required. Text to be summarized.

Union field `_instruction` .

`_instruction` can be only one of the following:

`instruction`

`string`

Optional. Summarization prompt for LLM.

### QuestionAnsweringQualityInput

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

Fields

`metricSpec`

` object ( QuestionAnsweringQualitySpec  ` )

Required. Spec for question answering quality score metric.

`instance`

` object ( QuestionAnsweringQualityInstance  ` )

Required. Question answering quality instance.

### QuestionAnsweringQualitySpec

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

Fields

`useReference`

`boolean`

Optional. Whether to use instance.reference to compute question answering quality.

`version`

`integer`

Optional. Which version to use for evaluation.

### QuestionAnsweringQualityInstance

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{// Union field _prediction can be only one of the following:&quot;prediction&quot;: string// End of list of possible types for union field _prediction.// Union field _reference can be only one of the following:&quot;reference&quot;: string// End of list of possible types for union field _reference.// Union field _context can be only one of the following:&quot;context&quot;: string// End of list of possible types for union field _context.// Union field _instruction can be only one of the following:&quot;instruction&quot;: string// End of list of possible types for union field _instruction.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

Union field `_prediction` .

`_prediction` can be only one of the following:

`prediction`

`string`

Required. Output of the evaluated model.

Union field `_reference` .

`_reference` can be only one of the following:

`reference`

`string`

Optional. Ground truth used to compare against the prediction.

Union field `_context` .

`_context` can be only one of the following:

`context`

`string`

Required. Text to answer the question.

Union field `_instruction` .

`_instruction` can be only one of the following:

`instruction`

`string`

Required. Question Answering prompt for LLM.

### PairwiseQuestionAnsweringQualityInput

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

Fields

`metricSpec`

` object ( PairwiseQuestionAnsweringQualitySpec  ` )

Required. Spec for pairwise question answering quality score metric.

`instance`

` object ( PairwiseQuestionAnsweringQualityInstance  ` )

Required. Pairwise question answering quality instance.

### PairwiseQuestionAnsweringQualitySpec

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

Fields

`useReference`

`boolean`

Optional. Whether to use instance.reference to compute question answering quality.

`version`

`integer`

Optional. Which version to use for evaluation.

### PairwiseQuestionAnsweringQualityInstance

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{// Union field _prediction can be only one of the following:&quot;prediction&quot;: string// End of list of possible types for union field _prediction.// Union field _baseline_prediction can be only one of the following:&quot;baselinePrediction&quot;: string// End of list of possible types for union field _baseline_prediction.// Union field _reference can be only one of the following:&quot;reference&quot;: string// End of list of possible types for union field _reference.// Union field _context can be only one of the following:&quot;context&quot;: string// End of list of possible types for union field _context.// Union field _instruction can be only one of the following:&quot;instruction&quot;: string// End of list of possible types for union field _instruction.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

Union field `_prediction` .

`_prediction` can be only one of the following:

`prediction`

`string`

Required. Output of the candidate model.

Union field `_baseline_prediction` .

`_baseline_prediction` can be only one of the following:

`baselinePrediction`

`string`

Required. Output of the baseline model.

Union field `_reference` .

`_reference` can be only one of the following:

`reference`

`string`

Optional. Ground truth used to compare against the prediction.

Union field `_context` .

`_context` can be only one of the following:

`context`

`string`

Required. Text to answer the question.

Union field `_instruction` .

`_instruction` can be only one of the following:

`instruction`

`string`

Required. Question Answering prompt for LLM.

### QuestionAnsweringRelevanceInput

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

Fields

`metricSpec`

` object ( QuestionAnsweringRelevanceSpec  ` )

Required. Spec for question answering relevance score metric.

`instance`

` object ( QuestionAnsweringRelevanceInstance  ` )

Required. Question answering relevance instance.

### QuestionAnsweringRelevanceSpec

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

Fields

`useReference`

`boolean`

Optional. Whether to use instance.reference to compute question answering relevance.

`version`

`integer`

Optional. Which version to use for evaluation.

### QuestionAnsweringRelevanceInstance

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{// Union field _prediction can be only one of the following:&quot;prediction&quot;: string// End of list of possible types for union field _prediction.// Union field _reference can be only one of the following:&quot;reference&quot;: string// End of list of possible types for union field _reference.// Union field _context can be only one of the following:&quot;context&quot;: string// End of list of possible types for union field _context.// Union field _instruction can be only one of the following:&quot;instruction&quot;: string// End of list of possible types for union field _instruction.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

Union field `_prediction` .

`_prediction` can be only one of the following:

`prediction`

`string`

Required. Output of the evaluated model.

Union field `_reference` .

`_reference` can be only one of the following:

`reference`

`string`

Optional. Ground truth used to compare against the prediction.

Union field `_context` .

`_context` can be only one of the following:

`context`

`string`

Optional. Text provided as context to answer the question.

Union field `_instruction` .

`_instruction` can be only one of the following:

`instruction`

`string`

Required. The question asked and other instruction in the inference prompt.

### QuestionAnsweringHelpfulnessInput

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

Fields

`metricSpec`

` object ( QuestionAnsweringHelpfulnessSpec  ` )

Required. Spec for question answering helpfulness score metric.

`instance`

` object ( QuestionAnsweringHelpfulnessInstance  ` )

Required. Question answering helpfulness instance.

### QuestionAnsweringHelpfulnessSpec

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

Fields

`useReference`

`boolean`

Optional. Whether to use instance.reference to compute question answering helpfulness.

`version`

`integer`

Optional. Which version to use for evaluation.

### QuestionAnsweringHelpfulnessInstance

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{// Union field _prediction can be only one of the following:&quot;prediction&quot;: string// End of list of possible types for union field _prediction.// Union field _reference can be only one of the following:&quot;reference&quot;: string// End of list of possible types for union field _reference.// Union field _context can be only one of the following:&quot;context&quot;: string// End of list of possible types for union field _context.// Union field _instruction can be only one of the following:&quot;instruction&quot;: string// End of list of possible types for union field _instruction.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

Union field `_prediction` .

`_prediction` can be only one of the following:

`prediction`

`string`

Required. Output of the evaluated model.

Union field `_reference` .

`_reference` can be only one of the following:

`reference`

`string`

Optional. Ground truth used to compare against the prediction.

Union field `_context` .

`_context` can be only one of the following:

`context`

`string`

Optional. Text provided as context to answer the question.

Union field `_instruction` .

`_instruction` can be only one of the following:

`instruction`

`string`

Required. The question asked and other instruction in the inference prompt.

### QuestionAnsweringCorrectnessInput

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

Fields

`metricSpec`

` object ( QuestionAnsweringCorrectnessSpec  ` )

Required. Spec for question answering correctness score metric.

`instance`

` object ( QuestionAnsweringCorrectnessInstance  ` )

Required. Question answering correctness instance.

### QuestionAnsweringCorrectnessSpec

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

Fields

`useReference`

`boolean`

Optional. Whether to use instance.reference to compute question answering correctness.

`version`

`integer`

Optional. Which version to use for evaluation.

### QuestionAnsweringCorrectnessInstance

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{// Union field _prediction can be only one of the following:&quot;prediction&quot;: string// End of list of possible types for union field _prediction.// Union field _reference can be only one of the following:&quot;reference&quot;: string// End of list of possible types for union field _reference.// Union field _context can be only one of the following:&quot;context&quot;: string// End of list of possible types for union field _context.// Union field _instruction can be only one of the following:&quot;instruction&quot;: string// End of list of possible types for union field _instruction.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

Union field `_prediction` .

`_prediction` can be only one of the following:

`prediction`

`string`

Required. Output of the evaluated model.

Union field `_reference` .

`_reference` can be only one of the following:

`reference`

`string`

Optional. Ground truth used to compare against the prediction.

Union field `_context` .

`_context` can be only one of the following:

`context`

`string`

Optional. Text provided as context to answer the question.

Union field `_instruction` .

`_instruction` can be only one of the following:

`instruction`

`string`

Required. The question asked and other instruction in the inference prompt.

### PointwiseMetricInput

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

Fields

`metricSpec`

` object ( PointwiseMetricSpec  ` )

Required. Spec for pointwise metric.

`instance`

` object ( PointwiseMetricInstance  ` )

Required. Pointwise metric instance.

### PointwiseMetricSpec

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;customOutputFormatConfig&quot;: {object (CustomOutputFormatConfig)},// Union field _metric_prompt_template can be only one of the following:&quot;metricPromptTemplate&quot;: string// End of list of possible types for union field _metric_prompt_template.// Union field _system_instruction can be only one of the following:&quot;systemInstruction&quot;: string// End of list of possible types for union field _system_instruction.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`customOutputFormatConfig`

` object ( CustomOutputFormatConfig  ` )

Optional. CustomOutputFormatConfig allows customization of metric output. By default, metrics return a score and explanation. When this config is set, the default output is replaced with either: - The raw output string. - A parsed output based on a user-defined schema. If a custom format is chosen, the `score` and `explanation` fields in the corresponding metric result will be empty.

Union field `_metric_prompt_template` .

`_metric_prompt_template` can be only one of the following:

`metricPromptTemplate`

`string`

Required. Metric prompt template for pointwise metric.

Union field `_system_instruction` .

`_system_instruction` can be only one of the following:

`systemInstruction`

`string`

Optional. System instructions for pointwise metric.

### CustomOutputFormatConfig

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{// Union field custom_output_format_config can be only one of the following:&quot;returnRawOutput&quot;: boolean// End of list of possible types for union field custom_output_format_config.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

Union field `custom_output_format_config` . Custom output format configuration. `custom_output_format_config` can be only one of the following:

`returnRawOutput`

`boolean`

Optional. Whether to return raw output.

### PointwiseMetricInstance

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{// Union field instance can be only one of the following:&quot;jsonInstance&quot;: string,&quot;contentMapInstance&quot;: {object (ContentMap)}// End of list of possible types for union field instance.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

Union field `instance` . Instance for pointwise metric. `instance` can be only one of the following:

`jsonInstance`

`string`

Instance specified as a json string. String key-value pairs are expected in the json\_instance to render PointwiseMetricSpec.instance\_prompt\_template.

`contentMapInstance`

` object ( ContentMap  ` )

Key-value contents for the mutlimodality input, including text, image, video, audio, and pdf, etc. The key is placeholder in metric prompt template, and the value is the multimodal content.

### ContentMap

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

Fields

`values`

` map (key: string, value: object ( Contents  ` ))

Optional. Map of placeholder to contents.

An object containing a list of `"key": value` pairs. Example: `{ "name": "wrench", "mass": "1.3kg", "count": "3" }` .

### ValuesEntry

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;key&quot;: string,&quot;value&quot;: {object (Contents)}}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`key`

`string`

`value`

` object ( Contents  ` )

### Contents

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

Fields

`contents[]`

` object ( Content  ` )

Optional. Repeated contents.

### Content

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;role&quot;: string,&quot;parts&quot;: [{object (Part)}]}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`role`

`string`

Optional. The producer of the content. Must be either 'user' or 'model'.

If not set, the service will default to 'user'.

`parts[]`

` object ( Part  ` )

Required. A list of `Part` objects that make up a single message. Parts of a message can have different MIME types.

A `Content` message must have at least one `Part` .

### Part

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;thought&quot;: boolean,&quot;thoughtSignature&quot;: string,&quot;mediaResolution&quot;: {object (MediaResolution)},&quot;audioTranscription&quot;: {object (AudioTranscription)},// Union field data can be only one of the following:&quot;text&quot;: string,&quot;inlineData&quot;: {object (Blob)},&quot;fileData&quot;: {object (FileData)},&quot;functionCall&quot;: {object (FunctionCall)},&quot;functionResponse&quot;: {object (FunctionResponse)},&quot;executableCode&quot;: {object (ExecutableCode)},&quot;codeExecutionResult&quot;: {object (CodeExecutionResult)}// End of list of possible types for union field data.// Union field metadata can be only one of the following:&quot;videoMetadata&quot;: {object (VideoMetadata)}// End of list of possible types for union field metadata.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`thought`

`boolean`

Optional. Indicates whether the `part` represents the model's thought process or reasoning.

`thoughtSignature`

`string ( bytes format)`

Optional. An opaque signature for the thought so it can be reused in subsequent requests.

A base64-encoded string.

`mediaResolution`

` object ( MediaResolution  ` )

per part media resolution. Media resolution for the input media.

`audioTranscription`

` object ( AudioTranscription  ` )

Optional. Audio (input or output) transcription. This is only set when this Part contains audio data.

Union field `data` .

`data` can be only one of the following:

`text`

`string`

Optional. The text content of the part. When sent from the VSCode Gemini Code Assist extension, references to @mentioned items will be converted to markdown boldface text. For example `@my-repo` will be converted to and sent as `**my-repo**` by the IDE agent.

`inlineData`

` object ( Blob  ` )

Optional. The inline data content of the part. This can be used to include images, audio, or video in a request.

`fileData`

` object ( FileData  ` )

Optional. The URI-based data of the part. This can be used to include files from Google Cloud Storage.

`functionCall`

` object ( FunctionCall  ` )

Optional. A predicted function call returned from the model. This contains the name of the function to call and the arguments to pass to the function.

`functionResponse`

` object ( FunctionResponse  ` )

Optional. The result of a function call. This is used to provide the model with the result of a function call that it predicted.

`executableCode`

` object ( ExecutableCode  ` )

Optional. Code generated by the model that is intended to be executed.

`codeExecutionResult`

` object ( CodeExecutionResult  ` )

Optional. The result of executing the `ExecutableCode` .

Union field `metadata` .

`metadata` can be only one of the following:

`videoMetadata`

` object ( VideoMetadata  ` )

Optional. Video metadata. The metadata should only be specified while the video data is presented in inline\_data or file\_data.

### Blob

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
  &quot;mimeType&quot;: string,
  &quot;data&quot;: string,
  &quot;displayName&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`mimeType`

`string`

Required. The IANA standard MIME type of the source data.

`data`

`string ( bytes format)`

Required. The raw bytes of the data.

A base64-encoded string.

`displayName`

`string`

Optional. The display name of the blob. Used to provide a label or filename to distinguish blobs.

This field is only returned in `PromptMessage` for prompt management. It is used in the Gemini calls only when server-side tools ( `code_execution` , `google_search` , and `url_context` ) are enabled.

### FileData

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
  &quot;mimeType&quot;: string,
  &quot;fileUri&quot;: string,
  &quot;displayName&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`mimeType`

`string`

Required. The IANA standard MIME type of the source data.

`fileUri`

`string`

Required. The URI of the file in Google Cloud Storage.

`displayName`

`string`

Optional. The display name of the file. Used to provide a label or filename to distinguish files.

This field is only returned in `PromptMessage` for prompt management. It is used in the Gemini calls only when server side tools ( `code_execution` , `google_search` , and `url_context` ) are enabled.

### FunctionCall

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;id&quot;: string,&quot;name&quot;: string,&quot;args&quot;: {object},&quot;partialArgs&quot;: [{object (PartialArg)}],&quot;willContinue&quot;: boolean}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`id`

`string`

Optional. The unique id of the function call. If populated, the client to execute the `function_call` and return the response with the matching `id` .

`name`

`string`

Optional. The name of the function to call. Matches `FunctionDeclaration.name` .

`args`

` object ( Struct  ` format)

Optional. The function parameters and values in JSON object format. See `FunctionDeclaration.parameters` for parameter details.

`partialArgs[]`

` object ( PartialArg  ` )

Optional. The partial argument value of the function call. If provided, represents the arguments/fields that are streamed incrementally.

`willContinue`

`boolean`

Optional. Whether this is the last part of the FunctionCall. If true, another partial message for the current FunctionCall is expected to follow.

### Struct

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
  &quot;fields&quot;: {
    string: value,
    ...
  }
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`fields`

` map (key: string, value: value ( Value  ` format))

Unordered map of dynamically typed values.

An object containing a list of `"key": value` pairs. Example: `{ "name": "wrench", "mass": "1.3kg", "count": "3" }` .

### FieldsEntry

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
  &quot;key&quot;: string,
  &quot;value&quot;: value
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`key`

`string`

`value`

` value ( Value  ` format)

### Value

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{// Union field kind can be only one of the following:&quot;nullValue&quot;: null,&quot;numberValue&quot;: number,&quot;stringValue&quot;: string,&quot;boolValue&quot;: boolean,&quot;structValue&quot;: {object},&quot;listValue&quot;: array// End of list of possible types for union field kind.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

Union field `kind` . The kind of value. `kind` can be only one of the following:

`nullValue`

`null`

Represents a JSON `null` .

`numberValue`

`number`

Represents a JSON number. Must not be `NaN` , `Infinity` or `-Infinity` , since those are not supported in JSON. This also cannot represent large Int64 values, since JSON format generally does not support them in its number type.

`stringValue`

`string`

Represents a JSON string.

`boolValue`

`boolean`

Represents a JSON boolean ( `true` or `false` literal in JSON).

`structValue`

` object ( Struct  ` format)

Represents a JSON object.

`listValue`

` array ( ListValue  ` format)

Represents a JSON array.

### ListValue

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
  &quot;values&quot;: [
    value
  ]
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`values[]`

` value ( Value  ` format)

Repeated field of dynamically typed values.

### PartialArg

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;jsonPath&quot;: string,&quot;willContinue&quot;: boolean,// Union field delta can be only one of the following:&quot;nullValue&quot;: null,&quot;numberValue&quot;: number,&quot;stringValue&quot;: string,&quot;boolValue&quot;: boolean// End of list of possible types for union field delta.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`jsonPath`

`string`

Required. A JSON Path (RFC 9535) to the argument being streamed. <https://datatracker.ietf.org/doc/html/rfc9535> . e.g. "$.foo.bar\[0\].data".

`willContinue`

`boolean`

Optional. Whether this is not the last part of the same json\_path. If true, another PartialArg message for the current json\_path is expected to follow.

Union field `delta` . The delta of field value being streamed. `delta` can be only one of the following:

`nullValue`

`null`

Optional. Represents a null value.

`numberValue`

`number`

Optional. Represents a double value.

`stringValue`

`string`

Optional. Represents a string value.

`boolValue`

`boolean`

Optional. Represents a boolean value.

### FunctionResponse

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;id&quot;: string,&quot;name&quot;: string,&quot;response&quot;: {object},&quot;parts&quot;: [{object (FunctionResponsePart)}]}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`id`

`string`

Optional. The id of the function call this response is for. Populated by the client to match the corresponding function call `id` .

`name`

`string`

Required. The name of the function to call. Matches `FunctionDeclaration.name` and `FunctionCall.name` .

`response`

` object ( Struct  ` format)

Required. The function response in JSON object format. Use "output" key to specify function output and "error" key to specify error details (if any). If "output" and "error" keys are not specified, then whole "response" is treated as function output.

`parts[]`

` object ( FunctionResponsePart  ` )

Optional. Ordered `Parts` that constitute a function response. Parts may have different IANA MIME types.

### FunctionResponsePart

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{// Union field data can be only one of the following:&quot;inlineData&quot;: {object (FunctionResponseBlob)},&quot;fileData&quot;: {object (FunctionResponseFileData)}// End of list of possible types for union field data.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

Union field `data` . The data of the function response part. `data` can be only one of the following:

`inlineData`

` object ( FunctionResponseBlob  ` )

Inline media bytes.

`fileData`

` object ( FunctionResponseFileData  ` )

URI based data.

### FunctionResponseBlob

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
  &quot;mimeType&quot;: string,
  &quot;data&quot;: string,
  &quot;displayName&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`mimeType`

`string`

Required. The IANA standard MIME type of the source data.

`data`

`string ( bytes format)`

Required. Raw bytes.

A base64-encoded string.

`displayName`

`string`

Optional. Display name of the blob.

Used to provide a label or filename to distinguish blobs.

This field is only returned in PromptMessage for prompt management. It is currently used in the Gemini GenerateContent calls only when server side tools (code\_execution, google\_search, and url\_context) are enabled.

### FunctionResponseFileData

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
  &quot;mimeType&quot;: string,
  &quot;fileUri&quot;: string,
  &quot;displayName&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`mimeType`

`string`

Required. The IANA standard MIME type of the source data.

`fileUri`

`string`

Required. URI.

`displayName`

`string`

Optional. Display name of the file data.

Used to provide a label or filename to distinguish file datas.

This field is only returned in PromptMessage for prompt management. It is currently used in the Gemini GenerateContent calls only when server side tools (code\_execution, google\_search, and url\_context) are enabled.

### ExecutableCode

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;language&quot;: enum (Language),&quot;code&quot;: string,// Union field _id can be only one of the following:&quot;id&quot;: string// End of list of possible types for union field _id.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`language`

` enum ( Language  ` )

Required. Programming language of the `code` .

`code`

`string`

Required. The code to be executed.

Union field `_id` .

`_id` can be only one of the following:

`id`

`string`

Optional. Unique identifier of the `ExecutableCode` part. The server returns the `CodeExecutionResult` with the matching `id` .

### CodeExecutionResult

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;outcome&quot;: enum (Outcome),&quot;output&quot;: string,// Union field _id can be only one of the following:&quot;id&quot;: string// End of list of possible types for union field _id.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`outcome`

` enum ( Outcome  ` )

Required. Outcome of the code execution.

`output`

`string`

Optional. Contains stdout when code execution is successful, stderr or other description otherwise.

Union field `_id` .

`_id` can be only one of the following:

`id`

`string`

Optional. The identifier of the `ExecutableCode` part this result is for. Only populated if the corresponding `ExecutableCode` has an id.

### VideoMetadata

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
  &quot;startOffset&quot;: string,
  &quot;endOffset&quot;: string,
  &quot;fps&quot;: number
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`startOffset`

` string ( Duration  ` format)

Optional. The start offset of the video.

A duration in seconds with up to nine fractional digits, ending with ' `s` '. Example: `"3.5s"` .

`endOffset`

` string ( Duration  ` format)

Optional. The end offset of the video.

A duration in seconds with up to nine fractional digits, ending with ' `s` '. Example: `"3.5s"` .

`fps`

`number`

Optional. The frame rate of the video sent to the model. If not specified, the default value is 1.0. The valid range is (0.0, 24.0\].

### Duration

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
  &quot;seconds&quot;: string,
  &quot;nanos&quot;: integer
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`seconds`

`string ( int64 format)`

Signed seconds of the span of time. Must be from -315,576,000,000 to +315,576,000,000 inclusive. Note: these bounds are computed from: 60 sec/min \* 60 min/hr \* 24 hr/day \* 365.25 days/year \* 10000 years

`nanos`

`integer`

Signed fractions of a second at nanosecond resolution of the span of time. Durations less than one second are represented with a 0 `seconds` field and a positive or negative `nanos` field. For durations of one second or more, a non-zero value for the `nanos` field must be of the same sign as the `seconds` field. Must be from -999,999,999 to +999,999,999 inclusive.

### MediaResolution

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{// Union field value can be only one of the following:&quot;level&quot;: enum (Level)// End of list of possible types for union field value.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

Union field `value` .

`value` can be only one of the following:

`level`

` enum ( Level  ` )

The tokenization quality used for given media.

### AudioTranscription

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;text&quot;: string,&quot;speakerLabel&quot;: string,&quot;words&quot;: [{object (WordInfo)}]}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`text`

`string`

Required. The transcription text of this audio segment.

`speakerLabel`

`string`

Optional. A label identifying the speaker of this audio segment (e.g. "spk\_1", "spk\_2"). Present when diarization is set.

`words[]`

` object ( WordInfo  ` )

Optional. Detailed word-level transcriptions and timing details. Present when word\_timestamp is set.

### WordInfo

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
  &quot;word&quot;: string,
  &quot;startOffset&quot;: string,
  &quot;endOffset&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`word`

`string`

Required. Transcript of the word.

`startOffset`

` string ( Duration  ` format)

Optional. Start offset in time of the word relative to the start of the audio.

A duration in seconds with up to nine fractional digits, ending with ' `s` '. Example: `"3.5s"` .

`endOffset`

` string ( Duration  ` format)

Optional. End offset in time of the word relative to the start of the audio.

A duration in seconds with up to nine fractional digits, ending with ' `s` '. Example: `"3.5s"` .

### PairwiseMetricInput

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

Fields

`metricSpec`

` object ( PairwiseMetricSpec  ` )

Required. Spec for pairwise metric.

`instance`

` object ( PairwiseMetricInstance  ` )

Required. Pairwise metric instance.

### PairwiseMetricSpec

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;candidateResponseFieldName&quot;: string,&quot;baselineResponseFieldName&quot;: string,&quot;customOutputFormatConfig&quot;: {object (CustomOutputFormatConfig)},// Union field _metric_prompt_template can be only one of the following:&quot;metricPromptTemplate&quot;: string// End of list of possible types for union field _metric_prompt_template.// Union field _system_instruction can be only one of the following:&quot;systemInstruction&quot;: string// End of list of possible types for union field _system_instruction.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`candidateResponseFieldName`

`string`

Optional. The field name of the candidate response.

`baselineResponseFieldName`

`string`

Optional. The field name of the baseline response.

`customOutputFormatConfig`

` object ( CustomOutputFormatConfig  ` )

Optional. CustomOutputFormatConfig allows customization of metric output. When this config is set, the default output is replaced with the raw output string. If a custom format is chosen, the `pairwise_choice` and `explanation` fields in the corresponding metric result will be empty.

Union field `_metric_prompt_template` .

`_metric_prompt_template` can be only one of the following:

`metricPromptTemplate`

`string`

Required. Metric prompt template for pairwise metric.

Union field `_system_instruction` .

`_system_instruction` can be only one of the following:

`systemInstruction`

`string`

Optional. System instructions for pairwise metric.

### PairwiseMetricInstance

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{// Union field instance can be only one of the following:&quot;jsonInstance&quot;: string,&quot;contentMapInstance&quot;: {object (ContentMap)}// End of list of possible types for union field instance.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

Union field `instance` . Instance for pairwise metric. `instance` can be only one of the following:

`jsonInstance`

`string`

Instance specified as a json string. String key-value pairs are expected in the json\_instance to render PairwiseMetricSpec.instance\_prompt\_template.

`contentMapInstance`

` object ( ContentMap  ` )

Key-value contents for the mutlimodality input, including text, image, video, audio, and pdf, etc. The key is placeholder in metric prompt template, and the value is the multimodal content.

### ToolCallValidInput

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

Fields

`metricSpec`

`object ( ToolCallValidSpec` )

Required. Spec for tool call valid metric.

`instances[]`

` object ( ToolCallValidInstance  ` )

Required. Repeated tool call valid instances.

### ToolCallValidInstance

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{// Union field _prediction can be only one of the following:&quot;prediction&quot;: string// End of list of possible types for union field _prediction.// Union field _reference can be only one of the following:&quot;reference&quot;: string// End of list of possible types for union field _reference.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

Union field `_prediction` .

`_prediction` can be only one of the following:

`prediction`

`string`

Required. Output of the evaluated model.

Union field `_reference` .

`_reference` can be only one of the following:

`reference`

`string`

Required. Ground truth used to compare against the prediction.

### ToolNameMatchInput

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

Fields

`metricSpec`

`object ( ToolNameMatchSpec` )

Required. Spec for tool name match metric.

`instances[]`

` object ( ToolNameMatchInstance  ` )

Required. Repeated tool name match instances.

### ToolNameMatchInstance

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{// Union field _prediction can be only one of the following:&quot;prediction&quot;: string// End of list of possible types for union field _prediction.// Union field _reference can be only one of the following:&quot;reference&quot;: string// End of list of possible types for union field _reference.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

Union field `_prediction` .

`_prediction` can be only one of the following:

`prediction`

`string`

Required. Output of the evaluated model.

Union field `_reference` .

`_reference` can be only one of the following:

`reference`

`string`

Required. Ground truth used to compare against the prediction.

### ToolParameterKeyMatchInput

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

Fields

`metricSpec`

`object ( ToolParameterKeyMatchSpec` )

Required. Spec for tool parameter key match metric.

`instances[]`

` object ( ToolParameterKeyMatchInstance  ` )

Required. Repeated tool parameter key match instances.

### ToolParameterKeyMatchInstance

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{// Union field _prediction can be only one of the following:&quot;prediction&quot;: string// End of list of possible types for union field _prediction.// Union field _reference can be only one of the following:&quot;reference&quot;: string// End of list of possible types for union field _reference.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

Union field `_prediction` .

`_prediction` can be only one of the following:

`prediction`

`string`

Required. Output of the evaluated model.

Union field `_reference` .

`_reference` can be only one of the following:

`reference`

`string`

Required. Ground truth used to compare against the prediction.

### ToolParameterKVMatchInput

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

Fields

`metricSpec`

` object ( ToolParameterKVMatchSpec  ` )

Required. Spec for tool parameter key value match metric.

`instances[]`

` object ( ToolParameterKVMatchInstance  ` )

Required. Repeated tool parameter key value match instances.

### ToolParameterKVMatchSpec

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

Fields

`useStrictStringMatch`

`boolean`

Optional. Whether to use STRICT string match on parameter values.

### ToolParameterKVMatchInstance

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{// Union field _prediction can be only one of the following:&quot;prediction&quot;: string// End of list of possible types for union field _prediction.// Union field _reference can be only one of the following:&quot;reference&quot;: string// End of list of possible types for union field _reference.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

Union field `_prediction` .

`_prediction` can be only one of the following:

`prediction`

`string`

Required. Output of the evaluated model.

Union field `_reference` .

`_reference` can be only one of the following:

`reference`

`string`

Required. Ground truth used to compare against the prediction.

### CometInput

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

Fields

`metricSpec`

` object ( CometSpec  ` )

Required. Spec for comet metric.

`instance`

` object ( CometInstance  ` )

Required. Comet instance.

### CometSpec

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;sourceLanguage&quot;: string,&quot;targetLanguage&quot;: string,// Union field _version can be only one of the following:&quot;version&quot;: enum (CometVersion)// End of list of possible types for union field _version.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`sourceLanguage`

`string`

Optional. Source language in BCP-47 format.

`targetLanguage`

`string`

Optional. Target language in BCP-47 format. Covers both prediction and reference.

Union field `_version` .

`_version` can be only one of the following:

`version`

` enum ( CometVersion  ` )

Required. Which version to use for evaluation.

### CometInstance

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{// Union field _prediction can be only one of the following:&quot;prediction&quot;: string// End of list of possible types for union field _prediction.// Union field _reference can be only one of the following:&quot;reference&quot;: string// End of list of possible types for union field _reference.// Union field _source can be only one of the following:&quot;source&quot;: string// End of list of possible types for union field _source.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

Union field `_prediction` .

`_prediction` can be only one of the following:

`prediction`

`string`

Required. Output of the evaluated model.

Union field `_reference` .

`_reference` can be only one of the following:

`reference`

`string`

Optional. Ground truth used to compare against the prediction.

Union field `_source` .

`_source` can be only one of the following:

`source`

`string`

Optional. Source text in original language.

### MetricxInput

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

Fields

`metricSpec`

` object ( MetricxSpec  ` )

Required. Spec for Metricx metric.

`instance`

` object ( MetricxInstance  ` )

Required. Metricx instance.

### MetricxSpec

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;sourceLanguage&quot;: string,&quot;targetLanguage&quot;: string,// Union field _version can be only one of the following:&quot;version&quot;: enum (MetricxVersion)// End of list of possible types for union field _version.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`sourceLanguage`

`string`

Optional. Source language in BCP-47 format.

`targetLanguage`

`string`

Optional. Target language in BCP-47 format. Covers both prediction and reference.

Union field `_version` .

`_version` can be only one of the following:

`version`

` enum ( MetricxVersion  ` )

Required. Which version to use for evaluation.

### MetricxInstance

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{// Union field _prediction can be only one of the following:&quot;prediction&quot;: string// End of list of possible types for union field _prediction.// Union field _reference can be only one of the following:&quot;reference&quot;: string// End of list of possible types for union field _reference.// Union field _source can be only one of the following:&quot;source&quot;: string// End of list of possible types for union field _source.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

Union field `_prediction` .

`_prediction` can be only one of the following:

`prediction`

`string`

Required. Output of the evaluated model.

Union field `_reference` .

`_reference` can be only one of the following:

`reference`

`string`

Optional. Ground truth used to compare against the prediction.

Union field `_source` .

`_source` can be only one of the following:

`source`

`string`

Optional. Source text in original language.

### TrajectoryExactMatchInput

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

Fields

`metricSpec`

`object ( TrajectoryExactMatchSpec` )

Required. Spec for TrajectoryExactMatch metric.

`instances[]`

` object ( TrajectoryExactMatchInstance  ` )

Required. Repeated TrajectoryExactMatch instance.

### TrajectoryExactMatchInstance

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{// Union field _predicted_trajectory can be only one of the following:&quot;predictedTrajectory&quot;: {object (Trajectory)}// End of list of possible types for union field _predicted_trajectory.// Union field _reference_trajectory can be only one of the following:&quot;referenceTrajectory&quot;: {object (Trajectory)}// End of list of possible types for union field _reference_trajectory.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

Union field `_predicted_trajectory` .

`_predicted_trajectory` can be only one of the following:

`predictedTrajectory`

` object ( Trajectory  ` )

Required. Spec for predicted tool call trajectory.

Union field `_reference_trajectory` .

`_reference_trajectory` can be only one of the following:

`referenceTrajectory`

` object ( Trajectory  ` )

Required. Spec for reference tool call trajectory.

### Trajectory

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

Fields

`toolCalls[]`

` object ( ToolCall  ` )

Required. Tool calls in the trajectory.

### ToolCall

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{// Union field _tool_name can be only one of the following:&quot;toolName&quot;: string// End of list of possible types for union field _tool_name.// Union field _tool_input can be only one of the following:&quot;toolInput&quot;: string// End of list of possible types for union field _tool_input.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

Union field `_tool_name` .

`_tool_name` can be only one of the following:

`toolName`

`string`

Required. Spec for tool name

Union field `_tool_input` .

`_tool_input` can be only one of the following:

`toolInput`

`string`

Optional. Spec for tool input

### TrajectoryInOrderMatchInput

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

Fields

`metricSpec`

`object ( TrajectoryInOrderMatchSpec` )

Required. Spec for TrajectoryInOrderMatch metric.

`instances[]`

` object ( TrajectoryInOrderMatchInstance  ` )

Required. Repeated TrajectoryInOrderMatch instance.

### TrajectoryInOrderMatchInstance

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{// Union field _predicted_trajectory can be only one of the following:&quot;predictedTrajectory&quot;: {object (Trajectory)}// End of list of possible types for union field _predicted_trajectory.// Union field _reference_trajectory can be only one of the following:&quot;referenceTrajectory&quot;: {object (Trajectory)}// End of list of possible types for union field _reference_trajectory.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

Union field `_predicted_trajectory` .

`_predicted_trajectory` can be only one of the following:

`predictedTrajectory`

` object ( Trajectory  ` )

Required. Spec for predicted tool call trajectory.

Union field `_reference_trajectory` .

`_reference_trajectory` can be only one of the following:

`referenceTrajectory`

` object ( Trajectory  ` )

Required. Spec for reference tool call trajectory.

### TrajectoryAnyOrderMatchInput

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

Fields

`metricSpec`

`object ( TrajectoryAnyOrderMatchSpec` )

Required. Spec for TrajectoryAnyOrderMatch metric.

`instances[]`

` object ( TrajectoryAnyOrderMatchInstance  ` )

Required. Repeated TrajectoryAnyOrderMatch instance.

### TrajectoryAnyOrderMatchInstance

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{// Union field _predicted_trajectory can be only one of the following:&quot;predictedTrajectory&quot;: {object (Trajectory)}// End of list of possible types for union field _predicted_trajectory.// Union field _reference_trajectory can be only one of the following:&quot;referenceTrajectory&quot;: {object (Trajectory)}// End of list of possible types for union field _reference_trajectory.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

Union field `_predicted_trajectory` .

`_predicted_trajectory` can be only one of the following:

`predictedTrajectory`

` object ( Trajectory  ` )

Required. Spec for predicted tool call trajectory.

Union field `_reference_trajectory` .

`_reference_trajectory` can be only one of the following:

`referenceTrajectory`

` object ( Trajectory  ` )

Required. Spec for reference tool call trajectory.

### TrajectoryPrecisionInput

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

Fields

`metricSpec`

`object ( TrajectoryPrecisionSpec` )

Required. Spec for TrajectoryPrecision metric.

`instances[]`

` object ( TrajectoryPrecisionInstance  ` )

Required. Repeated TrajectoryPrecision instance.

### TrajectoryPrecisionInstance

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{// Union field _predicted_trajectory can be only one of the following:&quot;predictedTrajectory&quot;: {object (Trajectory)}// End of list of possible types for union field _predicted_trajectory.// Union field _reference_trajectory can be only one of the following:&quot;referenceTrajectory&quot;: {object (Trajectory)}// End of list of possible types for union field _reference_trajectory.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

Union field `_predicted_trajectory` .

`_predicted_trajectory` can be only one of the following:

`predictedTrajectory`

` object ( Trajectory  ` )

Required. Spec for predicted tool call trajectory.

Union field `_reference_trajectory` .

`_reference_trajectory` can be only one of the following:

`referenceTrajectory`

` object ( Trajectory  ` )

Required. Spec for reference tool call trajectory.

### TrajectoryRecallInput

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

Fields

`metricSpec`

`object ( TrajectoryRecallSpec` )

Required. Spec for TrajectoryRecall metric.

`instances[]`

` object ( TrajectoryRecallInstance  ` )

Required. Repeated TrajectoryRecall instance.

### TrajectoryRecallInstance

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{// Union field _predicted_trajectory can be only one of the following:&quot;predictedTrajectory&quot;: {object (Trajectory)}// End of list of possible types for union field _predicted_trajectory.// Union field _reference_trajectory can be only one of the following:&quot;referenceTrajectory&quot;: {object (Trajectory)}// End of list of possible types for union field _reference_trajectory.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

Union field `_predicted_trajectory` .

`_predicted_trajectory` can be only one of the following:

`predictedTrajectory`

` object ( Trajectory  ` )

Required. Spec for predicted tool call trajectory.

Union field `_reference_trajectory` .

`_reference_trajectory` can be only one of the following:

`referenceTrajectory`

` object ( Trajectory  ` )

Required. Spec for reference tool call trajectory.

### TrajectorySingleToolUseInput

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

Fields

`metricSpec`

` object ( TrajectorySingleToolUseSpec  ` )

Required. Spec for TrajectorySingleToolUse metric.

`instances[]`

` object ( TrajectorySingleToolUseInstance  ` )

Required. Repeated TrajectorySingleToolUse instance.

### TrajectorySingleToolUseSpec

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{// Union field _tool_name can be only one of the following:&quot;toolName&quot;: string// End of list of possible types for union field _tool_name.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

Union field `_tool_name` .

`_tool_name` can be only one of the following:

`toolName`

`string`

Required. Spec for tool name to be checked for in the predicted trajectory.

### TrajectorySingleToolUseInstance

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{// Union field _predicted_trajectory can be only one of the following:&quot;predictedTrajectory&quot;: {object (Trajectory)}// End of list of possible types for union field _predicted_trajectory.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

Union field `_predicted_trajectory` .

`_predicted_trajectory` can be only one of the following:

`predictedTrajectory`

` object ( Trajectory  ` )

Required. Spec for predicted tool call trajectory.

### RubricBasedInstructionFollowingInput

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;metricSpec&quot;: {object (RubricBasedInstructionFollowingSpec)},&quot;instance&quot;: {object (RubricBasedInstructionFollowingInstance)}}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`metricSpec`

`object ( RubricBasedInstructionFollowingSpec` )

Required. Spec for RubricBasedInstructionFollowing metric.

`instance`

` object ( RubricBasedInstructionFollowingInstance  ` )

Required. Instance for RubricBasedInstructionFollowing metric.

### RubricBasedInstructionFollowingInstance

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{// Union field instance can be only one of the following:&quot;jsonInstance&quot;: string// End of list of possible types for union field instance.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

Union field `instance` . Instance for RubricBasedInstructionFollowing metric. `instance` can be only one of the following:

`jsonInstance`

`string`

Required. Instance specified as a json string. String key-value pairs are expected in the json\_instance to render RubricBasedInstructionFollowing prompt templates.

### Metric

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;aggregationMetrics&quot;: [enum (AggregationMetric)],&quot;metadata&quot;: {object (MetricMetadata)},// Union field metric_spec can be only one of the following:&quot;predefinedMetricSpec&quot;: {object (PredefinedMetricSpec)},&quot;computationBasedMetricSpec&quot;: {object (ComputationBasedMetricSpec)},&quot;llmBasedMetricSpec&quot;: {object (LLMBasedMetricSpec)},&quot;customCodeExecutionSpec&quot;: {object (CustomCodeExecutionSpec)},&quot;pointwiseMetricSpec&quot;: {object (PointwiseMetricSpec)},&quot;pairwiseMetricSpec&quot;: {object (PairwiseMetricSpec)},&quot;exactMatchSpec&quot;: {object (ExactMatchSpec)},&quot;bleuSpec&quot;: {object (BleuSpec)},&quot;rougeSpec&quot;: {object (RougeSpec)}// End of list of possible types for union field metric_spec.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`aggregationMetrics[]`

` enum ( AggregationMetric  ` )

Optional. The aggregation metrics to use.

`metadata`

` object ( MetricMetadata  ` )

Optional. Metadata about the metric, used for visualization and organization.

Union field `metric_spec` . The spec for the metric. It would be either a pre-defined metric, or a inline metric spec. `metric_spec` can be only one of the following:

`predefinedMetricSpec`

` object ( PredefinedMetricSpec  ` )

The spec for a pre-defined metric.

`computationBasedMetricSpec`

` object ( ComputationBasedMetricSpec  ` )

Spec for a computation based metric.

`llmBasedMetricSpec`

` object ( LLMBasedMetricSpec  ` )

Spec for an LLM based metric.

`customCodeExecutionSpec`

` object ( CustomCodeExecutionSpec  ` )

Spec for Custom Code Execution metric.

`pointwiseMetricSpec`

` object ( PointwiseMetricSpec  ` )

Spec for pointwise metric.

`pairwiseMetricSpec`

` object ( PairwiseMetricSpec  ` )

Spec for pairwise metric.

`exactMatchSpec`

`object ( ExactMatchSpec` )

Spec for exact match metric.

`bleuSpec`

` object ( BleuSpec  ` )

Spec for bleu metric.

`rougeSpec`

` object ( RougeSpec  ` )

Spec for rouge metric.

### PredefinedMetricSpec

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

Fields

`metricSpecName`

`string`

Required. The name of a pre-defined metric, such as "instruction\_following\_v1" or "text\_quality\_v1".

`metricSpecParameters`

` object ( Struct  ` format)

Optional. The parameters needed to run the pre-defined metric.

### ComputationBasedMetricSpec

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{// Union field _type can be only one of the following:&quot;type&quot;: enum (ComputationBasedMetricType)// End of list of possible types for union field _type.// Union field _parameters can be only one of the following:&quot;parameters&quot;: {object}// End of list of possible types for union field _parameters.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

Union field `_type` .

`_type` can be only one of the following:

`type`

` enum ( ComputationBasedMetricType  ` )

Required. The type of the computation based metric.

Union field `_parameters` .

`_parameters` can be only one of the following:

`parameters`

` object ( Struct  ` format)

Optional. A map of parameters for the metric, e.g. {"rouge\_type": "rougeL"}.

### LLMBasedMetricSpec

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;resultParserConfig&quot;: {object (EvaluationParserConfig)},// Union field rubrics_source can be only one of the following:&quot;rubricGroupKey&quot;: string,&quot;rubricGenerationSpec&quot;: {object (RubricGenerationSpec)},&quot;predefinedRubricGenerationSpec&quot;: {object (PredefinedMetricSpec)}// End of list of possible types for union field rubrics_source.// Union field _metric_prompt_template can be only one of the following:&quot;metricPromptTemplate&quot;: string// End of list of possible types for union field _metric_prompt_template.// Union field _system_instruction can be only one of the following:&quot;systemInstruction&quot;: string// End of list of possible types for union field _system_instruction.// Union field _judge_autorater_config can be only one of the following:&quot;judgeAutoraterConfig&quot;: {object (AutoraterConfig)}// End of list of possible types for union field _judge_autorater_config.// Union field _additional_config can be only one of the following:&quot;additionalConfig&quot;: {object}// End of list of possible types for union field _additional_config.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`resultParserConfig`

` object ( EvaluationParserConfig  ` )

Optional. The parser config for the metric result.

Union field `rubrics_source` . Source of the rubrics to be used for evaluation. `rubrics_source` can be only one of the following:

`rubricGroupKey`

`string`

Use a pre-defined group of rubrics associated with the input. Refers to a key in the rubric\_groups map of EvaluationInstance.

`rubricGenerationSpec`

` object ( RubricGenerationSpec  ` )

Dynamically generate rubrics using this specification.

`predefinedRubricGenerationSpec`

` object ( PredefinedMetricSpec  ` )

Dynamically generate rubrics using a predefined spec.

Union field `_metric_prompt_template` .

`_metric_prompt_template` can be only one of the following:

`metricPromptTemplate`

`string`

Required. Template for the prompt sent to the judge model.

Union field `_system_instruction` .

`_system_instruction` can be only one of the following:

`systemInstruction`

`string`

Optional. System instructions for the judge model.

Union field `_judge_autorater_config` .

`_judge_autorater_config` can be only one of the following:

`judgeAutoraterConfig`

` object ( AutoraterConfig  ` )

Optional. Optional configuration for the judge LLM (Autorater).

Union field `_additional_config` .

`_additional_config` can be only one of the following:

`additionalConfig`

` object ( Struct  ` format)

Optional. Optional additional configuration for the metric.

### RubricGenerationSpec

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;promptTemplate&quot;: string,&quot;rubricContentType&quot;: enum (RubricContentType),&quot;rubricTypeOntology&quot;: [string],// Union field _model_config can be only one of the following:&quot;modelConfig&quot;: {object (AutoraterConfig)}// End of list of possible types for union field _model_config.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`promptTemplate`

`string`

Template for the prompt used to generate rubrics. The details should be updated based on the most-recent recipe requirements.

`rubricContentType`

` enum ( RubricContentType  ` )

The type of rubric content to be generated.

`rubricTypeOntology[]`

`string`

Optional. An optional, pre-defined list of allowed types for generated rubrics. If this field is provided, it implies `include_rubric_type` should be true, and the generated rubric types should be chosen from this ontology.

Union field `_model_config` .

`_model_config` can be only one of the following:

`modelConfig`

` object ( AutoraterConfig  ` )

Configuration for the model used in rubric generation. Configs including sampling count and base model can be specified here. Flipping is not supported for rubric generation.

### AutoraterConfig

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;autoraterModel&quot;: string,&quot;generationConfig&quot;: {object (GenerationConfig)},// Union field _sampling_count can be only one of the following:&quot;samplingCount&quot;: integer// End of list of possible types for union field _sampling_count.// Union field _flip_enabled can be only one of the following:&quot;flipEnabled&quot;: boolean// End of list of possible types for union field _flip_enabled.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`autoraterModel`

`string`

Optional. The fully qualified name of the publisher model or tuned autorater endpoint to use.

Publisher model format: `projects/{project}/locations/{location}/publishers/*/models/*`

Tuned model endpoint format: `projects/{project}/locations/{location}/endpoints/{endpoint}`

`generationConfig`

` object ( GenerationConfig  ` )

Optional. Configuration options for model generation and outputs.

Union field `_sampling_count` .

`_sampling_count` can be only one of the following:

`samplingCount`

`integer`

Optional. Number of samples for each instance in the dataset. If not specified, the default is 4. Minimum value is 1, maximum value is 32.

Union field `_flip_enabled` .

`_flip_enabled` can be only one of the following:

`flipEnabled`

`boolean`

Optional. Default is true. Whether to flip the candidate and baseline responses. This is only applicable to the pairwise metric. If enabled, also provide PairwiseMetricSpec.candidate\_response\_field\_name and PairwiseMetricSpec.baseline\_response\_field\_name. When rendering PairwiseMetricSpec.metric\_prompt\_template, the candidate and baseline fields will be flipped for half of the samples to reduce bias.

### GenerationConfig

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;stopSequences&quot;: [string],&quot;responseMimeType&quot;: string,&quot;responseModalities&quot;: [enum (Modality)],&quot;thinkingConfig&quot;: {object (ThinkingConfig)},&quot;modelConfig&quot;: {object (ModelConfig)},&quot;responseFormat&quot;: [{object (ResponseFormat)}],// Union field _temperature can be only one of the following:&quot;temperature&quot;: number// End of list of possible types for union field _temperature.// Union field _top_p can be only one of the following:&quot;topP&quot;: number// End of list of possible types for union field _top_p.// Union field _top_k can be only one of the following:&quot;topK&quot;: number// End of list of possible types for union field _top_k.// Union field _candidate_count can be only one of the following:&quot;candidateCount&quot;: integer// End of list of possible types for union field _candidate_count.// Union field _max_output_tokens can be only one of the following:&quot;maxOutputTokens&quot;: integer// End of list of possible types for union field _max_output_tokens.// Union field _response_logprobs can be only one of the following:&quot;responseLogprobs&quot;: boolean// End of list of possible types for union field _response_logprobs.// Union field _logprobs can be only one of the following:&quot;logprobs&quot;: integer// End of list of possible types for union field _logprobs.// Union field _presence_penalty can be only one of the following:&quot;presencePenalty&quot;: number// End of list of possible types for union field _presence_penalty.// Union field _frequency_penalty can be only one of the following:&quot;frequencyPenalty&quot;: number// End of list of possible types for union field _frequency_penalty.// Union field _seed can be only one of the following:&quot;seed&quot;: integer// End of list of possible types for union field _seed.// Union field _response_schema can be only one of the following:&quot;responseSchema&quot;: {object (Schema)}// End of list of possible types for union field _response_schema.// Union field _response_json_schema can be only one of the following:&quot;responseJsonSchema&quot;: value// End of list of possible types for union field _response_json_schema.// Union field _routing_config can be only one of the following:&quot;routingConfig&quot;: {object (RoutingConfig)}// End of list of possible types for union field _routing_config.// Union field _audio_timestamp can be only one of the following:&quot;audioTimestamp&quot;: boolean// End of list of possible types for union field _audio_timestamp.// Union field _media_resolution can be only one of the following:&quot;mediaResolution&quot;: enum (MediaResolution)// End of list of possible types for union field _media_resolution.// Union field _speech_config can be only one of the following:&quot;speechConfig&quot;: {object (SpeechConfig)}// End of list of possible types for union field _speech_config.// Union field _enable_affective_dialog can be only one of the following:&quot;enableAffectiveDialog&quot;: boolean// End of list of possible types for union field _enable_affective_dialog.// Union field _image_config can be only one of the following:&quot;imageConfig&quot;: {object (ImageConfig)}// End of list of possible types for union field _image_config.// Union field _audio_transcription_config can be only one of the following:&quot;audioTranscriptionConfig&quot;: {object (AudioTranscriptionConfig)}// End of list of possible types for union field _audio_transcription_config.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`stopSequences[]`

`string`

Optional. A list of character sequences that will stop the model from generating further tokens. If a stop sequence is generated, the output will end at that point. This is useful for controlling the length and structure of the output. For example, you can use \["\\n", "\#\#\#"\] to stop generation at a new line or a specific marker.

` responseMimeType (deprecated)  `

`string`

> This item is deprecated\!

Optional. The IANA standard MIME type of the response. The model will generate output that conforms to this MIME type. Supported values include 'text/plain' (default) and 'application/json'. The model needs to be prompted to output the appropriate response type, otherwise the behavior is undefined. Deprecated: Use `response_format` instead.

`responseModalities[]`

` enum ( Modality  ` )

Optional. The modalities of the response. The model will generate a response that includes all the specified modalities. For example, if this is set to `[TEXT, IMAGE]` , the response will include both text and an image.

`thinkingConfig`

` object ( ThinkingConfig  ` )

Optional. Configuration for thinking features. An error will be returned if this field is set for models that don't support thinking.

` modelConfig (deprecated)  `

` object ( ModelConfig  ` )

> Optional. The `model_config` field is deprecated and is not supported anymore. Use `routing_config` instead.

Optional. Config for model selection.

`responseFormat[]`

` object ( ResponseFormat  ` )

Optional. New response format field for the model to configure output formatting and delivery.

Union field `_temperature` .

`_temperature` can be only one of the following:

`temperature`

`number`

Optional. Controls the randomness of the output. A higher temperature results in more creative and diverse responses, while a lower temperature makes the output more predictable and focused. The valid range is (0.0, 2.0\].

Union field `_top_p` .

`_top_p` can be only one of the following:

`topP`

`number`

Optional. Specifies the nucleus sampling threshold. The model considers only the smallest set of tokens whose cumulative probability is at least `top_p` . This helps generate more diverse and less repetitive responses. For example, a `top_p` of 0.9 means the model considers tokens until the cumulative probability of the tokens to select from reaches 0.9. It's recommended to adjust either temperature or `top_p` , but not both.

Union field `_top_k` .

`_top_k` can be only one of the following:

`topK`

`number`

Optional. Specifies the top-k sampling threshold. The model considers only the top k most probable tokens for the next token. This can be useful for generating more coherent and less random text. For example, a `top_k` of 40 means the model will choose the next word from the 40 most likely words.

Union field `_candidate_count` .

`_candidate_count` can be only one of the following:

`candidateCount`

`integer`

Optional. The number of candidate responses to generate.

A higher `candidate_count` can provide more options to choose from, but it also consumes more resources. This can be useful for generating a variety of responses and selecting the best one.

Union field `_max_output_tokens` .

`_max_output_tokens` can be only one of the following:

`maxOutputTokens`

`integer`

Optional. The maximum number of tokens to generate in the response.

A token is approximately four characters. The default value varies by model. This parameter can be used to control the length of the generated text and prevent overly long responses.

Union field `_response_logprobs` .

`_response_logprobs` can be only one of the following:

`responseLogprobs`

`boolean`

Optional. If set to true, the log probabilities of the output tokens are returned.

Log probabilities are the logarithm of the probability of a token appearing in the output. A higher log probability means the token is more likely to be generated. This can be useful for analyzing the model's confidence in its own output and for debugging.

Union field `_logprobs` .

`_logprobs` can be only one of the following:

`logprobs`

`integer`

Optional. The number of top log probabilities to return for each token.

This can be used to see which other tokens were considered likely candidates for a given position. A higher value will return more options, but it will also increase the size of the response.

Union field `_presence_penalty` .

`_presence_penalty` can be only one of the following:

`presencePenalty`

`number`

Optional. Penalizes tokens that have already appeared in the generated text. A positive value encourages the model to generate more diverse and less repetitive text. Valid values can range from \[-2.0, 2.0\].

Union field `_frequency_penalty` .

`_frequency_penalty` can be only one of the following:

`frequencyPenalty`

`number`

Optional. Penalizes tokens based on their frequency in the generated text. A positive value helps to reduce the repetition of words and phrases. Valid values can range from \[-2.0, 2.0\].

Union field `_seed` .

`_seed` can be only one of the following:

`seed`

`integer`

Optional. A seed for the random number generator.

By setting a seed, you can make the model's output mostly deterministic. For a given prompt and parameters (like temperature, top\_p, etc.), the model will produce the same response every time. However, it's not a guaranteed absolute deterministic behavior. This is different from parameters like `temperature` , which control the *level* of randomness. `seed` ensures that the "random" choices the model makes are the same on every run, making it essential for testing and ensuring reproducible results.

Union field `_response_schema` .

`_response_schema` can be only one of the following:

` responseSchema (deprecated)  `

` object ( Schema  ` )

> This item is deprecated\!

Optional. Lets you to specify a schema for the model's response, ensuring that the output conforms to a particular structure. This is useful for generating structured data such as JSON. The schema is a subset of the [OpenAPI 3.0 schema object](https://spec.openapis.org/oas/v3.0.3#schema) object.

When this field is set, you must also set the `response_mime_type` to `application/json` . Deprecated: Use `response_format` instead.

Union field `_response_json_schema` .

`_response_json_schema` can be only one of the following:

` responseJsonSchema (deprecated)  `

` value ( Value  ` format)

> This item is deprecated\!

Optional. When this field is set, `response_schema` must be omitted and `response_mime_type` must be set to `application/json` . Deprecated: Use `response_format` instead.

Union field `_routing_config` .

`_routing_config` can be only one of the following:

`routingConfig`

` object ( RoutingConfig  ` )

Optional. Routing configuration.

Union field `_audio_timestamp` .

`_audio_timestamp` can be only one of the following:

`audioTimestamp`

`boolean`

Optional. If enabled, audio timestamps will be included in the request to the model. This can be useful for synchronizing audio with other modalities in the response.

Union field `_media_resolution` .

`_media_resolution` can be only one of the following:

`mediaResolution`

` enum ( MediaResolution  ` )

Optional. The token resolution at which input media content is sampled. This is used to control the trade-off between the quality of the response and the number of tokens used to represent the media. A higher resolution allows the model to perceive more detail, which can lead to a more nuanced response, but it will also use more tokens. This does not affect the image dimensions sent to the model.

Union field `_speech_config` .

`_speech_config` can be only one of the following:

`speechConfig`

` object ( SpeechConfig  ` )

Optional. The speech generation config.

Union field `_enable_affective_dialog` .

`_enable_affective_dialog` can be only one of the following:

`enableAffectiveDialog`

`boolean`

Optional. If enabled, the model will detect emotions and adapt its responses accordingly. For example, if the model detects that the user is frustrated, it may provide a more empathetic response.

Union field `_image_config` .

`_image_config` can be only one of the following:

` imageConfig (deprecated)  `

` object ( ImageConfig  ` )

> This item is deprecated\!

Optional. Config for image generation features. Deprecated: Use `response_format.image` instead.

Union field `_audio_transcription_config` .

`_audio_transcription_config` can be only one of the following:

`audioTranscriptionConfig`

` object ( AudioTranscriptionConfig  ` )

Optional. Config for audio transcription (speech recognition).

### Schema

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;type&quot;: enum (Type),&quot;format&quot;: string,&quot;title&quot;: string,&quot;description&quot;: string,&quot;nullable&quot;: boolean,&quot;default&quot;: value,&quot;items&quot;: {object (Schema)},&quot;minItems&quot;: string,&quot;maxItems&quot;: string,&quot;enum&quot;: [string],&quot;properties&quot;: {string: {object (Schema)},...},&quot;propertyOrdering&quot;: [string],&quot;required&quot;: [string],&quot;minProperties&quot;: string,&quot;maxProperties&quot;: string,&quot;minimum&quot;: number,&quot;maximum&quot;: number,&quot;minLength&quot;: string,&quot;maxLength&quot;: string,&quot;pattern&quot;: string,&quot;example&quot;: value,&quot;anyOf&quot;: [{object (Schema)}],&quot;additionalProperties&quot;: value,&quot;ref&quot;: string,&quot;defs&quot;: {string: {object (Schema)},...}}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`type`

` enum ( Type  ` )

Optional. Data type of the schema field.

`format`

`string`

Optional. The format of the data. For `NUMBER` type, format can be `float` or `double` . For `INTEGER` type, format can be `int32` or `int64` . For `STRING` type, format can be `email` , `byte` , `date` , `date-time` , `password` , and other formats to further refine the data type.

`title`

`string`

Optional. Title for the schema.

`description`

`string`

Optional. Describes the data. The model uses this field to understand the purpose of the schema and how to use it. It is a best practice to provide a clear and descriptive explanation for the schema and its properties here, rather than in the prompt.

`nullable`

`boolean`

Optional. Indicates if the value of this field can be null.

`default`

` value ( Value  ` format)

Optional. Default value to use if the field is not specified.

`items`

` object ( Schema  ` )

Optional. If type is `ARRAY` , `items` specifies the schema of elements in the array.

`minItems`

`string ( int64 format)`

Optional. If type is `ARRAY` , `min_items` specifies the minimum number of items in an array.

`maxItems`

`string ( int64 format)`

Optional. If type is `ARRAY` , `max_items` specifies the maximum number of items in an array.

`enum[]`

`string`

Optional. Possible values of the field. This field can be used to restrict a value to a fixed set of values. To mark a field as an enum, set `format` to `enum` and provide the list of possible values in `enum` . For example: 1. To define directions: `{type:STRING, format:enum, enum:["EAST", "NORTH", "SOUTH", "WEST"]}` 2. To define apartment numbers: `{type:INTEGER, format:enum, enum:["101", "201", "301"]}`

`properties`

` map (key: string, value: object ( Schema  ` ))

Optional. If type is `OBJECT` , `properties` is a map of property names to schema definitions for each property of the object.

An object containing a list of `"key": value` pairs. Example: `{ "name": "wrench", "mass": "1.3kg", "count": "3" }` .

`propertyOrdering[]`

`string`

Optional. Order of properties displayed or used where order matters. This is not a standard field in OpenAPI specification, but can be used to control the order of properties.

`required[]`

`string`

Optional. If type is `OBJECT` , `required` lists the names of properties that must be present.

`minProperties`

`string ( int64 format)`

Optional. If type is `OBJECT` , `min_properties` specifies the minimum number of properties that can be provided.

`maxProperties`

`string ( int64 format)`

Optional. If type is `OBJECT` , `max_properties` specifies the maximum number of properties that can be provided.

`minimum`

`number`

Optional. If type is `INTEGER` or `NUMBER` , `minimum` specifies the minimum allowed value.

`maximum`

`number`

Optional. If type is `INTEGER` or `NUMBER` , `maximum` specifies the maximum allowed value.

`minLength`

`string ( int64 format)`

Optional. If type is `STRING` , `min_length` specifies the minimum length of the string.

`maxLength`

`string ( int64 format)`

Optional. If type is `STRING` , `max_length` specifies the maximum length of the string.

`pattern`

`string`

Optional. If type is `STRING` , `pattern` specifies a regular expression that the string must match.

`example`

` value ( Value  ` format)

Optional. Example of an instance of this schema.

`anyOf[]`

` object ( Schema  ` )

Optional. The instance must be valid against any (one or more) of the subschemas listed in `any_of` .

`additionalProperties`

` value ( Value  ` format)

Optional. If `type` is `OBJECT` , specifies how to handle properties not defined in `properties` . If it is a boolean `false` , no additional properties are allowed. If it is a schema, additional properties are allowed if they conform to the schema.

`ref`

`string`

Optional. Allows referencing another schema definition to use in place of this schema. The value must be a valid reference to a schema in `defs` .

For example, the following schema defines a reference to a schema node named "Pet":

type: object properties: pet: ref: \#/defs/Pet defs: Pet: type: object properties: name: type: string

The value of the "pet" property is a reference to the schema node named "Pet". See details in <https://json-schema.org/understanding-json-schema/structuring>

`defs`

` map (key: string, value: object ( Schema  ` ))

Optional. `defs` provides a map of schema definitions that can be reused by `ref` elsewhere in the schema. Only allowed at root level of the schema.

An object containing a list of `"key": value` pairs. Example: `{ "name": "wrench", "mass": "1.3kg", "count": "3" }` .

### PropertiesEntry

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;key&quot;: string,&quot;value&quot;: {object (Schema)}}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`key`

`string`

`value`

` object ( Schema  ` )

### DefsEntry

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;key&quot;: string,&quot;value&quot;: {object (Schema)}}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`key`

`string`

`value`

` object ( Schema  ` )

### RoutingConfig

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{// Union field routing_config can be only one of the following:&quot;autoMode&quot;: {object (AutoRoutingMode)},&quot;manualMode&quot;: {object (ManualRoutingMode)}// End of list of possible types for union field routing_config.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

Union field `routing_config` . The routing mode for the request. `routing_config` can be only one of the following:

`autoMode`

` object ( AutoRoutingMode  ` )

In this mode, the model is selected automatically based on the content of the request.

`manualMode`

` object ( ManualRoutingMode  ` )

In this mode, the model is specified manually.

### AutoRoutingMode

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{// Union field _model_routing_preference can be only one of the following:&quot;modelRoutingPreference&quot;: enum (ModelRoutingPreference)// End of list of possible types for union field _model_routing_preference.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

Union field `_model_routing_preference` .

`_model_routing_preference` can be only one of the following:

`modelRoutingPreference`

` enum ( ModelRoutingPreference  ` )

The model routing preference.

### ManualRoutingMode

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{// Union field _model_name can be only one of the following:&quot;modelName&quot;: string// End of list of possible types for union field _model_name.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

Union field `_model_name` .

`_model_name` can be only one of the following:

`modelName`

`string`

The name of the model to use. Only public LLM models are accepted.

### SpeechConfig

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;voiceConfig&quot;: {object (VoiceConfig)},&quot;languageCode&quot;: string,&quot;multiSpeakerVoiceConfig&quot;: {object (MultiSpeakerVoiceConfig)}}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`voiceConfig`

` object ( VoiceConfig  ` )

The configuration for the voice to use.

`languageCode`

`string`

Optional. The language code (ISO 639-1) for the speech synthesis.

`multiSpeakerVoiceConfig`

` object ( MultiSpeakerVoiceConfig  ` )

The configuration for a multi-speaker text-to-speech request. This field is mutually exclusive with `voice_config` .

### VoiceConfig

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{// Union field voice_config can be only one of the following:&quot;prebuiltVoiceConfig&quot;: {object (PrebuiltVoiceConfig)},&quot;replicatedVoiceConfig&quot;: {object (ReplicatedVoiceConfig)}// End of list of possible types for union field voice_config.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

Union field `voice_config` . The configuration for the speaker to use. `voice_config` can be only one of the following:

`prebuiltVoiceConfig`

` object ( PrebuiltVoiceConfig  ` )

The configuration for a prebuilt voice.

`replicatedVoiceConfig`

` object ( ReplicatedVoiceConfig  ` )

Optional. The configuration for a replicated voice. This enables users to replicate a voice from an audio sample.

### PrebuiltVoiceConfig

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{// Union field _voice_name can be only one of the following:&quot;voiceName&quot;: string// End of list of possible types for union field _voice_name.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

Union field `_voice_name` .

`_voice_name` can be only one of the following:

`voiceName`

`string`

The name of the prebuilt voice to use.

### ReplicatedVoiceConfig

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
  &quot;mimeType&quot;: string,
  &quot;voiceSampleAudio&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`mimeType`

`string`

Optional. The mimetype of the voice sample. The only currently supported value is `audio/wav` . This represents 16-bit signed little-endian wav data, with a 24kHz sampling rate. `mime_type` will default to `audio/wav` if not set.

`voiceSampleAudio`

`string ( bytes format)`

Optional. The sample of the custom voice.

A base64-encoded string.

### MultiSpeakerVoiceConfig

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;speakerVoiceConfigs&quot;: [{object (SpeakerVoiceConfig)}]}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`speakerVoiceConfigs[]`

` object ( SpeakerVoiceConfig  ` )

Required. A list of configurations for the voices of the speakers. Exactly two speaker voice configurations must be provided.

### SpeakerVoiceConfig

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;speaker&quot;: string,&quot;voiceConfig&quot;: {object (VoiceConfig)}}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`speaker`

`string`

Required. The name of the speaker. This should be the same as the speaker name used in the prompt.

`voiceConfig`

` object ( VoiceConfig  ` )

Required. The configuration for the voice of this speaker.

### ThinkingConfig

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{// Union field _include_thoughts can be only one of the following:&quot;includeThoughts&quot;: boolean// End of list of possible types for union field _include_thoughts.// Union field _thinking_budget can be only one of the following:&quot;thinkingBudget&quot;: integer// End of list of possible types for union field _thinking_budget.// Union field _thinking_level can be only one of the following:&quot;thinkingLevel&quot;: enum (ThinkingLevel)// End of list of possible types for union field _thinking_level.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

Union field `_include_thoughts` .

`_include_thoughts` can be only one of the following:

`includeThoughts`

`boolean`

Optional. If true, the model will include its thoughts in the response. "Thoughts" are the intermediate steps the model takes to arrive at the final response. They can provide insights into the model's reasoning process and help with debugging. If this is true, thoughts are returned only when available.

Union field `_thinking_budget` .

`_thinking_budget` can be only one of the following:

`thinkingBudget`

`integer`

Optional. The token budget for the model's thinking process. The model will make a best effort to stay within this budget. This can be used to control the trade-off between response quality and latency.

Union field `_thinking_level` .

`_thinking_level` can be only one of the following:

`thinkingLevel`

` enum ( ThinkingLevel  ` )

Optional. The number of thoughts tokens that the model should generate.

### ModelConfig

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;featureSelectionPreference&quot;: enum (FeatureSelectionPreference)}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`featureSelectionPreference`

` enum ( FeatureSelectionPreference  ` )

Required. Feature selection preference.

### ImageConfig

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{// Union field _image_output_options can be only one of the following:&quot;imageOutputOptions&quot;: {object (ImageOutputOptions)}// End of list of possible types for union field _image_output_options.// Union field _aspect_ratio can be only one of the following:&quot;aspectRatio&quot;: string// End of list of possible types for union field _aspect_ratio.// Union field _person_generation can be only one of the following:&quot;personGeneration&quot;: enum (PersonGeneration)// End of list of possible types for union field _person_generation.// Union field _image_size can be only one of the following:&quot;imageSize&quot;: string// End of list of possible types for union field _image_size.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

Union field `_image_output_options` .

`_image_output_options` can be only one of the following:

`imageOutputOptions`

` object ( ImageOutputOptions  ` )

Optional. The image output format for generated images.

Union field `_aspect_ratio` .

`_aspect_ratio` can be only one of the following:

`aspectRatio`

`string`

Optional. The desired aspect ratio for the generated images. The following aspect ratios are supported:

"1:1" "2:3", "3:2" "3:4", "4:3" "4:5", "5:4" "9:16", "16:9" "21:9"

Union field `_person_generation` .

`_person_generation` can be only one of the following:

`personGeneration`

` enum ( PersonGeneration  ` )

Optional. Controls whether the model can generate people.

Union field `_image_size` .

`_image_size` can be only one of the following:

`imageSize`

`string`

Optional. Specifies the size of generated images. Supported values are `1K` , `2K` , `4K` . If not specified, the model will use default value `1K` .

### ImageOutputOptions

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{// Union field _mime_type can be only one of the following:&quot;mimeType&quot;: string// End of list of possible types for union field _mime_type.// Union field _compression_quality can be only one of the following:&quot;compressionQuality&quot;: integer// End of list of possible types for union field _compression_quality.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

Union field `_mime_type` .

`_mime_type` can be only one of the following:

`mimeType`

`string`

Optional. The image format that the output should be saved as.

Union field `_compression_quality` .

`_compression_quality` can be only one of the following:

`compressionQuality`

`integer`

Optional. The compression quality of the output image.

### ResponseFormat

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{// Union field format can be only one of the following:&quot;text&quot;: {object (TextResponseFormat)},&quot;audio&quot;: {object (AudioResponseFormat)},&quot;image&quot;: {object (ImageResponseFormat)},&quot;video&quot;: {object (VideoResponseFormat)}// End of list of possible types for union field format.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

Union field `format` . The format of the output content. `format` can be only one of the following:

`text`

` object ( TextResponseFormat  ` )

Text output format.

`audio`

` object ( AudioResponseFormat  ` )

Audio output format.

`image`

` object ( ImageResponseFormat  ` )

Image output format.

`video`

` object ( VideoResponseFormat  ` )

Video output format.

### TextResponseFormat

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{// Union field _mime_type can be only one of the following:&quot;mimeType&quot;: enum (MimeType)// End of list of possible types for union field _mime_type.// Union field _schema can be only one of the following:&quot;schema&quot;: value// End of list of possible types for union field _schema.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

Union field `_mime_type` .

`_mime_type` can be only one of the following:

`mimeType`

` enum ( MimeType  ` )

Optional. The IANA standard MIME type of the response.

Union field `_schema` .

`_schema` can be only one of the following:

`schema`

` value ( Value  ` format)

Optional. The JSON schema that the output should conform to. Only applicable when mime\_type is APPLICATION\_JSON.

### AudioResponseFormat

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;delivery&quot;: enum (DeliveryMode),// Union field _mime_type can be only one of the following:&quot;mimeType&quot;: enum (MimeType)// End of list of possible types for union field _mime_type.// Union field _sample_rate can be only one of the following:&quot;sampleRate&quot;: integer// End of list of possible types for union field _sample_rate.// Union field _bit_rate can be only one of the following:&quot;bitRate&quot;: integer// End of list of possible types for union field _bit_rate.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`delivery`

` enum ( DeliveryMode  ` )

Optional. Delivery mode for the generated content.

Union field `_mime_type` .

`_mime_type` can be only one of the following:

`mimeType`

` enum ( MimeType  ` )

Optional. The MIME type of the audio output.

Union field `_sample_rate` .

`_sample_rate` can be only one of the following:

`sampleRate`

`integer`

Optional. Sample rate for the generated audio in Hertz.

Union field `_bit_rate` .

`_bit_rate` can be only one of the following:

`bitRate`

`integer`

Optional. Bit rate in bits per second (bps). Only applicable for compressed formats (MP3, Opus).

### ImageResponseFormat

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;delivery&quot;: enum (DeliveryMode),// Union field _mime_type can be only one of the following:&quot;mimeType&quot;: enum (MimeType)// End of list of possible types for union field _mime_type.// Union field _aspect_ratio can be only one of the following:&quot;aspectRatio&quot;: enum (AspectRatio)// End of list of possible types for union field _aspect_ratio.// Union field _image_size can be only one of the following:&quot;imageSize&quot;: enum (ImageSize)// End of list of possible types for union field _image_size.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`delivery`

` enum ( DeliveryMode  ` )

Optional. Delivery mode for the generated content.

Union field `_mime_type` .

`_mime_type` can be only one of the following:

`mimeType`

` enum ( MimeType  ` )

Optional. The MIME type of the image output.

Union field `_aspect_ratio` .

`_aspect_ratio` can be only one of the following:

`aspectRatio`

` enum ( AspectRatio  ` )

Optional. The aspect ratio for the image output.

Union field `_image_size` .

`_image_size` can be only one of the following:

`imageSize`

` enum ( ImageSize  ` )

Optional. The size of the image output.

### VideoResponseFormat

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;delivery&quot;: enum (DeliveryMode),&quot;gcsUri&quot;: string,&quot;aspectRatio&quot;: enum (AspectRatio),// Union field _duration can be only one of the following:&quot;duration&quot;: string// End of list of possible types for union field _duration.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`delivery`

` enum ( DeliveryMode  ` )

Optional. Delivery mode for the generated content.

`gcsUri`

`string`

Optional. The Google Cloud Storage URI to store the video output. Required for Vertex if delivery is URI.

`aspectRatio`

` enum ( AspectRatio  ` )

The aspect ratio for the video output.

Union field `_duration` .

`_duration` can be only one of the following:

`duration`

` string ( Duration  ` format)

Optional. The duration for the video output.

A duration in seconds with up to nine fractional digits, ending with ' `s` '. Example: `"3.5s"` .

### AudioTranscriptionConfig

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;adaptationPhrases&quot;: [string],&quot;customVocabulary&quot;: [string],&quot;wordTimestamp&quot;: boolean,&quot;diarization&quot;: boolean,// Union field language_config can be only one of the following:&quot;languageAuto&quot;: {object (LanguageAuto)},&quot;languageHints&quot;: {object (LanguageHints)}// End of list of possible types for union field language_config.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

` adaptationPhrases[] (deprecated)  `

`string`

> This item is deprecated\!

Optional. A list of phrases to bias the ASR model towards.

`customVocabulary[]`

`string`

Optional. A list of custom vocabulary phrases to bias the speech recognition model toward recognizing specific terms.

`wordTimestamp`

`boolean`

Optional. Configures word-level timestamp generation.

`diarization`

`boolean`

Optional. Configures speaker diarization.

Union field `language_config` . Required. Specifies how to handle the languages in the audio. `language_config` can be only one of the following:

`languageAuto`

`object ( LanguageAuto` )

Optional. The model will detect the language automatically.

`languageHints`

` object ( LanguageHints  ` )

Optional. Specifies one or more languages in the audio.

### LanguageHints

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
  &quot;languageCodes&quot;: [
    string
  ]
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`languageCodes[]`

`string`

Required. BCP-47 language codes. At least one must be specified.

### EvaluationParserConfig

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{// Union field parser can be only one of the following:&quot;customCodeParserConfig&quot;: {object (CustomCodeParserConfig)}// End of list of possible types for union field parser.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

Union field `parser` .

`parser` can be only one of the following:

`customCodeParserConfig`

` object ( CustomCodeParserConfig  ` )

Optional. Use custom code to parse the LLM response.

### CustomCodeParserConfig

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{// Union field _parsing_function can be only one of the following:&quot;parsingFunction&quot;: string// End of list of possible types for union field _parsing_function.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

Union field `_parsing_function` .

`_parsing_function` can be only one of the following:

`parsingFunction`

`string`

Required. Python function for parsing results. The function should be defined within this string.

The function takes a list of strings (LLM responses) and should return either a list of dictionaries (for rubrics) or a single dictionary (for a metric result).

Example function signature: def parse(responses: list\[str\]) -\> list\[dict\[str, Any\]\] | dict\[str, Any\]:

When parsing rubrics, return a list of dictionaries, where each dictionary represents a Rubric. Example for rubrics: \[ { "content": {"property": {"description": "The response is factual."}}, "type": "FACTUALITY", "importance": "HIGH" }, { "content": {"property": {"description": "The response is fluent."}}, "type": "FLUENCY", "importance": "MEDIUM" } \]

When parsing critique results, return a dictionary representing a MetricResult. Example for a metric result: { "score": 0.8, "explanation": "The model followed most instructions.", "rubric\_verdicts": \[...\] }

... code for result extraction and aggregation

### CustomCodeExecutionSpec

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{// Union field _evaluation_function can be only one of the following:&quot;evaluationFunction&quot;: string// End of list of possible types for union field _evaluation_function.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

Union field `_evaluation_function` .

`_evaluation_function` can be only one of the following:

`evaluationFunction`

`string`

Required. Python function. Expected user to define the following function, e.g.: def evaluate(instance: dict\[str, Any\]) -\> float: Please include this function signature in the code snippet. Instance is the evaluation instance, any fields populated in the instance are available to the function as instance\[field\_name\].

Example: Example input:

`instance= EvaluationInstance( response=EvaluationInstance.InstanceData(text="The answer is 4."), reference=EvaluationInstance.InstanceData(text="4") )`

Example converted input:

`{ 'response': {'text': 'The answer is 4.'}, 'reference': {'text': '4'} }`

Example python function:

`def evaluate(instance: dict[str, Any]) -> float: if instance['response']['text'] == instance['reference']['text']: return 1.0 return 0.0`

CustomCodeExecutionSpec is also supported in Batch Evaluation (EvalDataset RPC) and Tuning Evaluation. Each line in the input jsonl file will be converted to dict\[str, Any\] and passed to the evaluation function.

### MetricMetadata

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

Fields

`title`

`string`

Optional. The user-friendly name for the metric. If not set for a registered metric, it will default to the metric's display name.

`scoreRange`

` object ( ScoreRange  ` )

Optional. The range of possible scores for this metric, used for plotting.

`otherMetadata`

` object ( Struct  ` format)

Optional. Flexible metadata for user-defined attributes.

### ScoreRange

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;description&quot;: string,// Union field _min can be only one of the following:&quot;min&quot;: number// End of list of possible types for union field _min.// Union field _max can be only one of the following:&quot;max&quot;: number// End of list of possible types for union field _max.// Union field _step can be only one of the following:&quot;step&quot;: number// End of list of possible types for union field _step.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`description`

`string`

Optional. The description of the score explaining the directionality etc.

Union field `_min` .

`_min` can be only one of the following:

`min`

`number`

Required. The minimum value of the score range (inclusive).

Union field `_max` .

`_max` can be only one of the following:

`max`

`number`

Required. The maximum value of the score range (inclusive).

Union field `_step` .

`_step` can be only one of the following:

`step`

`number`

Optional. The distance between discrete steps in the range. If unset, the range is assumed to be continuous.

### MetricSource

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{// Union field metric_source can be only one of the following:&quot;metric&quot;: {object (Metric)},&quot;metricResourceName&quot;: string// End of list of possible types for union field metric_source.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

Union field `metric_source` . The source of the metric. `metric_source` can be only one of the following:

`metric`

` object ( Metric  ` )

Inline metric config.

`metricResourceName`

`string`

Optional. Resource name for registered metric.

### EvaluationInstance

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;prompt&quot;: {object (InstanceData)},&quot;rubricGroups&quot;: {string: {object (RubricGroup)},...},&quot;response&quot;: {object (InstanceData)},&quot;reference&quot;: {object (InstanceData)},&quot;otherData&quot;: {object (MapInstance)},&quot;agentData&quot;: {object (DeprecatedAgentData)},&quot;agentEvalData&quot;: {object (AgentData)}}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`prompt`

` object ( InstanceData  ` )

Optional. Data used to populate placeholder `prompt` in a metric prompt template.

`rubricGroups`

` map (key: string, value: object ( RubricGroup  ` ))

Optional. Named groups of rubrics associated with the prompt. This is used for rubric-based evaluations where rubrics can be referenced by a key. The key could represent versions, associated metrics, etc.

An object containing a list of `"key": value` pairs. Example: `{ "name": "wrench", "mass": "1.3kg", "count": "3" }` .

`response`

` object ( InstanceData  ` )

Optional. Data used to populate placeholder `response` in a metric prompt template.

`reference`

` object ( InstanceData  ` )

Optional. Data used to populate placeholder `reference` in a metric prompt template.

`otherData`

` object ( MapInstance  ` )

Optional. Other data used to populate placeholders based on their key. If a key conflicts with a field in the EvaluationInstance (e.g. `prompt` ), the value of the field will take precedence over the value in other\_data.

` agentData (deprecated)  `

` object ( DeprecatedAgentData  ` )

> This item is deprecated\!

Optional. Deprecated: Use `agent_eval_data` instead. Data used for agent evaluation.

`agentEvalData`

` object ( AgentData  ` )

Optional. Data used for agent evaluation.

### InstanceData

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{// Union field data can be only one of the following:&quot;text&quot;: string,&quot;contents&quot;: {object (Contents)}// End of list of possible types for union field data.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

Union field `data` . Supported formats for instance data. `data` can be only one of the following:

`text`

`string`

Text data.

`contents`

` object ( Contents  ` )

List of Gemini content data.

### Contents

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

Fields

`contents[]`

` object ( Content  ` )

Optional. Repeated contents.

### RubricGroupsEntry

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;key&quot;: string,&quot;value&quot;: {object (RubricGroup)}}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`key`

`string`

`value`

` object ( RubricGroup  ` )

### RubricGroup

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;groupId&quot;: string,&quot;displayName&quot;: string,&quot;rubrics&quot;: [{object (Rubric)}]}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`groupId`

`string`

Unique identifier for the group.

`displayName`

`string`

Human-readable name for the group. This should be unique within a given context if used for display or selection. Example: "Instruction Following V1", "Content Quality - Summarization Task".

`rubrics[]`

` object ( Rubric  ` )

Rubrics that are part of this group.

### Rubric

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;rubricId&quot;: string,&quot;content&quot;: {object (Content)},// Union field _type can be only one of the following:&quot;type&quot;: string// End of list of possible types for union field _type.// Union field _importance can be only one of the following:&quot;importance&quot;: enum (Importance)// End of list of possible types for union field _importance.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`rubricId`

`string`

Unique identifier for the rubric. This ID is used to refer to this rubric, e.g., in RubricVerdict.

`content`

` object ( Content  ` )

Required. The actual testable criteria for the rubric.

Union field `_type` .

`_type` can be only one of the following:

`type`

`string`

Optional. A type designator for the rubric, which can inform how it's evaluated or interpreted by systems or users. It's recommended to use consistent, well-defined, upper snake\_case strings. Examples: "SUMMARIZATION\_QUALITY", "SAFETY\_HARMFUL\_CONTENT", "INSTRUCTION\_ADHERENCE".

Union field `_importance` .

`_importance` can be only one of the following:

`importance`

` enum ( Importance  ` )

Optional. The relative importance of this rubric.

### Content

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{// Union field content_type can be only one of the following:&quot;property&quot;: {object (Property)}// End of list of possible types for union field content_type.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

Union field `content_type` .

`content_type` can be only one of the following:

`property`

` object ( Property  ` )

Evaluation criteria based on a specific property.

### Property

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
  &quot;description&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`description`

`string`

Description of the property being evaluated. Example: "The model's response is grammatically correct."

### MapInstance

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;mapInstance&quot;: {string: {object (InstanceData)},...}}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`mapInstance`

` map (key: string, value: object ( InstanceData  ` ))

Optional. Map of instance data.

An object containing a list of `"key": value` pairs. Example: `{ "name": "wrench", "mass": "1.3kg", "count": "3" }` .

### MapInstanceEntry

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;key&quot;: string,&quot;value&quot;: {object (InstanceData)}}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`key`

`string`

`value`

` object ( InstanceData  ` )

### DeprecatedAgentData

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;agents&quot;: {string: {object (DeprecatedAgentConfig)},...},&quot;turns&quot;: [{object (ConversationTurn)}],&quot;developerInstruction&quot;: {object (InstanceData)},&quot;agentConfig&quot;: {object (DeprecatedAgentConfig)},// Union field tools_data can be only one of the following:&quot;toolsText&quot;: string,&quot;tools&quot;: {object (Tools)}// End of list of possible types for union field tools_data.// Union field events_data can be only one of the following:&quot;events&quot;: {object (Events)}// End of list of possible types for union field events_data.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`agents`

` map (key: string, value: object ( DeprecatedAgentConfig  ` ))

Optional. The static Agent Configuration. This map defines the graph structure of the agent system. Key: agent\_id (matches the `author` field in events). Value: The static configuration of the agent (tools, instructions, sub-agents).

An object containing a list of `"key": value` pairs. Example: `{ "name": "wrench", "mass": "1.3kg", "count": "3" }` .

`turns[]`

` object ( ConversationTurn  ` )

Optional. The chronological list of conversation turns. Each turn represents a logical execution cycle (e.g., User Input -\> Agent Response).

` developerInstruction (deprecated)  `

` object ( InstanceData  ` )

> This item is deprecated\!

Optional. Deprecated: Use `agents.developer_instruction` or `turns.events.active_instruction` instead. A field containing instructions from the developer for the agent.

`agentConfig`

` object ( DeprecatedAgentConfig  ` )

Optional. Deprecated: Use `agent_eval_data` instead. Agent configuration.

Union field `tools_data` . --- Legacy fields below. To be deprecated. --- Deprecated: Use `agents` instead. Data for the tools available to the agent. `tools_data` can be only one of the following:

` toolsText (deprecated)  `

`string`

> This item is deprecated\!

A JSON string containing a list of tools available to an agent with info such as name, description, parameters and required parameters.

` tools (deprecated)  `

` object ( Tools  ` )

> This item is deprecated\!

List of tools.

Union field `events_data` .

`events_data` can be only one of the following:

`events`

` object ( Events  ` )

A list of events.

### Tools

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;tool&quot;: [{object (Tool)}]}</code></pre></td>
</tr>
</tbody>
</table>

Fields

` tool[] (deprecated)  `

` object ( Tool  ` )

> This item is deprecated\!

Optional. List of tools: each tool can have multiple function declarations.

### Tool

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;functionDeclarations&quot;: [{object (FunctionDeclaration)}],&quot;retrieval&quot;: {object (Retrieval)},&quot;googleSearch&quot;: {object (GoogleSearch)},&quot;googleSearchRetrieval&quot;: {object (GoogleSearchRetrieval)},&quot;googleMaps&quot;: {object (GoogleMaps)},&quot;enterpriseWebSearch&quot;: {object (EnterpriseWebSearch)},&quot;parallelAiSearch&quot;: {object (ParallelAiSearch)},&quot;codeExecution&quot;: {object (CodeExecution)},&quot;urlContext&quot;: {object (UrlContext)},&quot;computerUse&quot;: {object (ComputerUse)}}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`functionDeclarations[]`

` object ( FunctionDeclaration  ` )

Optional. Function tool type. One or more function declarations to be passed to the model along with the current user query. Model may decide to call a subset of these functions by populating `FunctionCall` in the response. User should provide a `FunctionResponse` for each function call in the next turn. Based on the function responses, Model will generate the final response back to the user. Maximum 512 function declarations can be provided.

`retrieval`

` object ( Retrieval  ` )

Optional. Retrieval tool type. System will always execute the provided retrieval tool(s) to get external knowledge to answer the prompt. Retrieval results are presented to the model for generation.

`googleSearch`

` object ( GoogleSearch  ` )

Optional. GoogleSearch tool type. Tool to support Google Search in Model. Powered by Google.

` googleSearchRetrieval (deprecated)  `

` object ( GoogleSearchRetrieval  ` )

> Optional. The `google_search_retrieval` field is deprecated. Use `google_search` instead. This field is for use with Gemini 1.5 models; `google_search` is used for Gemini 2.0 and newer models.

Optional. Specialized retrieval tool that is powered by Google Search.

`googleMaps`

` object ( GoogleMaps  ` )

Optional. GoogleMaps tool type. Tool to support Google Maps in Model.

`enterpriseWebSearch`

` object ( EnterpriseWebSearch  ` )

Optional. Tool to support searching public web data, powered by Agent Platform Search and Sec4 compliance.

`parallelAiSearch`

` object ( ParallelAiSearch  ` )

Optional. If specified, Agent Platform will use Parallel.ai to search for information to answer user queries. The search results will be grounded on Parallel.ai and presented to the model for response generation

`codeExecution`

`object ( CodeExecution` )

Optional. CodeExecution tool type. Enables the model to execute code as part of generation.

`urlContext`

`object ( UrlContext` )

Optional. Tool to support URL context retrieval.

`computerUse`

` object ( ComputerUse  ` )

Optional. Tool to support the model interacting directly with the computer. If enabled, it automatically populates computer-use specific Function Declarations.

### FunctionDeclaration

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;name&quot;: string,&quot;description&quot;: string,&quot;parameters&quot;: {object (Schema)},&quot;parametersJsonSchema&quot;: value,&quot;response&quot;: {object (Schema)},&quot;responseJsonSchema&quot;: value}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`name`

`string`

Required. The name of the function to call. Must start with a letter or an underscore. Must be a-z, A-Z, 0-9, or contain underscores, dots, colons and dashes, with a maximum length of 128.

`description`

`string`

Optional. Description and purpose of the function. Model uses it to decide how and whether to call the function.

`parameters`

` object ( Schema  ` )

Optional. Describes the parameters to this function in JSON Schema Object format. Reflects the Open API 3.03 Parameter Object. string Key: the name of the parameter. Parameter names are case sensitive. Schema Value: the Schema defining the type used for the parameter. For function with no parameters, this can be left unset. Parameter names must start with a letter or an underscore and must only contain chars a-z, A-Z, 0-9, or underscores with a maximum length of 64. Example with 1 required and 1 optional parameter: type: OBJECT properties: param1: type: STRING param2: type: INTEGER required: - param1

`parametersJsonSchema`

` value ( Value  ` format)

Optional. Describes the parameters to the function in JSON Schema format. The schema must describe an object where the properties are the parameters to the function. For example:

    {
      "type": "object",
      "properties": {
        "name": { "type": "string" },
        "age": { "type": "integer" }
      },
      "additionalProperties": false,
      "required": ["name", "age"],
      "propertyOrdering": ["name", "age"]
    }

This field is mutually exclusive with `parameters` .

`response`

` object ( Schema  ` )

Optional. Describes the output from this function in JSON Schema format. Reflects the Open API 3.03 Response Object. The Schema defines the type used for the response value of the function.

`responseJsonSchema`

` value ( Value  ` format)

Optional. Describes the output from this function in JSON Schema format. The value specified by the schema is the response value of the function.

This field is mutually exclusive with `response` .

### Retrieval

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;disableAttribution&quot;: boolean,// Union field source can be only one of the following:&quot;vertexAiSearch&quot;: {object (VertexAISearch)},&quot;vertexRagStore&quot;: {object (VertexRagStore)}// End of list of possible types for union field source.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

` disableAttribution (deprecated)  `

`boolean`

> This item is deprecated\!

Optional. Deprecated. This option is no longer supported.

Union field `source` . The source of the retrieval. `source` can be only one of the following:

`vertexAiSearch`

` object ( VertexAISearch  ` )

Set to use data source powered by Agent Platform Search.

`vertexRagStore`

` object ( VertexRagStore  ` )

Set to use data source powered by Vertex RAG store. User data is uploaded via the VertexRagDataService.

### VertexAISearch

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;datastore&quot;: string,&quot;engine&quot;: string,&quot;maxResults&quot;: integer,&quot;filter&quot;: string,&quot;dataStoreSpecs&quot;: [{object (DataStoreSpec)}]}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`datastore`

`string`

Optional. Fully-qualified Agent Platform Search data store resource ID. Format: `projects/{project}/locations/{location}/collections/{collection}/dataStores/{dataStore}`

`engine`

`string`

Optional. Fully-qualified Agent Platform Search engine resource ID. Format: `projects/{project}/locations/{location}/collections/{collection}/engines/{engine}`

`maxResults`

`integer`

Optional. Number of search results to return per query. The default value is 10. The maximumm allowed value is 10.

`filter`

`string`

Optional. Filter strings to be passed to the search API.

`dataStoreSpecs[]`

` object ( DataStoreSpec  ` )

Specifications that define the specific DataStores to be searched, along with configurations for those data stores. This is only considered for Engines with multiple data stores. It should only be set if engine is used.

### DataStoreSpec

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
  &quot;dataStore&quot;: string,
  &quot;filter&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`dataStore`

`string`

Full resource name of DataStore, such as Format: `projects/{project}/locations/{location}/collections/{collection}/dataStores/{dataStore}`

`filter`

`string`

Optional. Filter specification to filter documents in the data store specified by data\_store field. For more information on filtering, see [Filtering](https://cloud.google.com/generative-ai-app-builder/docs/filter-search-metadata)

### VertexRagStore

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;ragCorpora&quot;: [string],&quot;ragResources&quot;: [{object (RagResource)}],&quot;ragRetrievalConfig&quot;: {object (RagRetrievalConfig)},&quot;storeContext&quot;: boolean,// Union field _similarity_top_k can be only one of the following:&quot;similarityTopK&quot;: integer// End of list of possible types for union field _similarity_top_k.// Union field _vector_distance_threshold can be only one of the following:&quot;vectorDistanceThreshold&quot;: number// End of list of possible types for union field _vector_distance_threshold.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

` ragCorpora[] (deprecated)  `

`string`

> This item is deprecated\!

Optional. Deprecated. Please use rag\_resources instead.

`ragResources[]`

` object ( RagResource  ` )

Optional. The representation of the rag source. It can be used to specify corpus only or ragfiles. Currently only support one corpus or multiple files from one corpus. In the future we may open up multiple corpora support.

`ragRetrievalConfig`

` object ( RagRetrievalConfig  ` )

Optional. The retrieval config for the Rag query.

`storeContext`

`boolean`

Optional. Currently only supported for Gemini Multimodal Live API.

In Gemini Multimodal Live API, if `store_context` bool is specified, Gemini will leverage it to automatically memorize the interactions between the client and Gemini, and retrieve context when needed to augment the response generation for users' ongoing and future interactions.

Union field `_similarity_top_k` .

`_similarity_top_k` can be only one of the following:

` similarityTopK (deprecated)  `

`integer`

> This item is deprecated\!

Optional. Number of top k results to return from the selected corpora.

Union field `_vector_distance_threshold` .

`_vector_distance_threshold` can be only one of the following:

` vectorDistanceThreshold (deprecated)  `

`number`

> This item is deprecated\!

Optional. Only return results with vector distance smaller than the threshold.

### RagResource

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
  &quot;ragCorpus&quot;: string,
  &quot;ragFileIds&quot;: [
    string
  ]
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`ragCorpus`

`string`

Optional. RagCorpora resource name. Format: `projects/{project}/locations/{location}/ragCorpora/{rag_corpus}`

`ragFileIds[]`

`string`

Optional. rag\_file\_id. The files should be in the same rag\_corpus set in rag\_corpus field.

### RagRetrievalConfig

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;topK&quot;: integer,&quot;hybridSearch&quot;: {object (HybridSearch)},&quot;filter&quot;: {object (Filter)},&quot;ranking&quot;: {object (Ranking)}}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`topK`

`integer`

Optional. The number of contexts to retrieve.

`hybridSearch`

` object ( HybridSearch  ` )

Optional. Config for Hybrid Search.

`filter`

` object ( Filter  ` )

Optional. Config for filters.

`ranking`

` object ( Ranking  ` )

Optional. Config for ranking and reranking.

### HybridSearch

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{// Union field _alpha can be only one of the following:&quot;alpha&quot;: number// End of list of possible types for union field _alpha.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

Union field `_alpha` .

`_alpha` can be only one of the following:

`alpha`

`number`

Optional. Alpha value controls the weight between dense and sparse vector search results. The range is \[0, 1\], while 0 means sparse vector search only and 1 means dense vector search only. The default value is 0.5 which balances sparse and dense vector search equally.

### Filter

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;metadataFilter&quot;: string,// Union field vector_db_threshold can be only one of the following:&quot;vectorDistanceThreshold&quot;: number,&quot;vectorSimilarityThreshold&quot;: number// End of list of possible types for union field vector_db_threshold.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`metadataFilter`

`string`

Optional. String for metadata filtering.

Union field `vector_db_threshold` . Filter contexts retrieved from the vector DB based on either vector distance or vector similarity. `vector_db_threshold` can be only one of the following:

`vectorDistanceThreshold`

`number`

Optional. Only returns contexts with vector distance smaller than the threshold.

`vectorSimilarityThreshold`

`number`

Optional. Only returns contexts with vector similarity larger than the threshold.

### Ranking

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{// Union field ranking_config can be only one of the following:&quot;rankService&quot;: {object (RankService)},&quot;llmRanker&quot;: {object (LlmRanker)}// End of list of possible types for union field ranking_config.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

Union field `ranking_config` . Config options for ranking. Currently only Rank Service is supported. `ranking_config` can be only one of the following:

`rankService`

` object ( RankService  ` )

Optional. Config for Rank Service.

`llmRanker`

` object ( LlmRanker  ` )

Optional. Config for LlmRanker.

### RankService

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{// Union field _model_name can be only one of the following:&quot;modelName&quot;: string// End of list of possible types for union field _model_name.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

Union field `_model_name` .

`_model_name` can be only one of the following:

`modelName`

`string`

Optional. The model name of the rank service. Format: `semantic-ranker-512@latest`

### LlmRanker

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{// Union field _model_name can be only one of the following:&quot;modelName&quot;: string// End of list of possible types for union field _model_name.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

Union field `_model_name` .

`_model_name` can be only one of the following:

`modelName`

`string`

Optional. The model name used for ranking. See [Supported models](https://cloud.google.com/vertex-ai/generative-ai/docs/model-reference/inference#supported-models) .

### GoogleSearch

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;excludeDomains&quot;: [string],// Union field _blocking_confidence can be only one of the following:&quot;blockingConfidence&quot;: enum (PhishBlockThreshold)// End of list of possible types for union field _blocking_confidence.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`excludeDomains[]`

`string`

Optional. List of domains to be excluded from the search results. The default limit is 2000 domains. Example: \["amazon.com", "facebook.com"\].

Union field `_blocking_confidence` .

`_blocking_confidence` can be only one of the following:

`blockingConfidence`

` enum ( PhishBlockThreshold  ` )

Optional. Sites with confidence level chosen & above this value will be blocked from the search results.

### GoogleSearchRetrieval

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;dynamicRetrievalConfig&quot;: {object (DynamicRetrievalConfig)}}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`dynamicRetrievalConfig`

` object ( DynamicRetrievalConfig  ` )

Specifies the dynamic retrieval configuration for the given source.

### DynamicRetrievalConfig

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;mode&quot;: enum (Mode),// Union field _dynamic_threshold can be only one of the following:&quot;dynamicThreshold&quot;: number// End of list of possible types for union field _dynamic_threshold.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`mode`

` enum ( Mode  ` )

The mode of the predictor to be used in dynamic retrieval.

Union field `_dynamic_threshold` .

`_dynamic_threshold` can be only one of the following:

`dynamicThreshold`

`number`

Optional. The threshold to be used in dynamic retrieval. If not set, a system default value is used.

### GoogleMaps

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;enableWidget&quot;: boolean,&quot;groundingTypes&quot;: {object (GroundingTypes)}}</code></pre></td>
</tr>
</tbody>
</table>

Fields

` enableWidget (deprecated)  `

`boolean`

> This item is deprecated\!

Optional. Deprecated: The Google Maps contextual widget behavior in Grounding with Google Maps is being deprecated; this field is planned for removal and no longer has any effect once removed.

If true, include the widget context token in the response.

`groundingTypes`

` object ( GroundingTypes  ` )

Optional. Specifies the types of Google Maps grounding to enable. Defaults to `places` when unset.

### GroundingTypes

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;places&quot;: {object (Places)},&quot;routing&quot;: {object (Routing)}}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`places`

`object ( Places` )

Optional. Enables grounding with Google Maps Places. This is the default grounding type when no `GroundingTypes` are specified.

`routing`

`object ( Routing` )

Optional. Enables grounding with Google Maps Routing APIs (ComputeRoutes and SearchAlongRoute).

### EnterpriseWebSearch

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;excludeDomains&quot;: [string],// Union field _blocking_confidence can be only one of the following:&quot;blockingConfidence&quot;: enum (PhishBlockThreshold)// End of list of possible types for union field _blocking_confidence.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`excludeDomains[]`

`string`

Optional. List of domains to be excluded from the search results. The default limit is 2000 domains.

Union field `_blocking_confidence` .

`_blocking_confidence` can be only one of the following:

`blockingConfidence`

` enum ( PhishBlockThreshold  ` )

Optional. Sites with confidence level chosen & above this value will be blocked from the search results.

### ParallelAiSearch

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
  &quot;apiKey&quot;: string,
  &quot;customConfigs&quot;: {
    object
  }
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`apiKey`

`string`

Optional. The API key for ParallelAiSearch. If an API key is not provided, the system will attempt to verify access by checking for an active Parallel.ai subscription through the Google Cloud Marketplace. See <https://docs.parallel.ai/search/search-quickstart> for more details.

`customConfigs`

` object ( Struct  ` format)

Optional. Custom configs for ParallelAiSearch. This field can be used to pass any parameter from the Parallel.ai Search API. See the Parallel.ai documentation for the full list of available parameters and their usage: <https://docs.parallel.ai/api-reference/search-beta/search> Currently only `source_policy` , `excerpts` , `max_results` , `mode` , `fetch_policy` can be set via this field. For example: { "source\_policy": { "include\_domains": \["google.com", "wikipedia.org"\], "exclude\_domains": \["example.com"\] }, "fetch\_policy": { "max\_age\_seconds": 3600 } }

### ComputerUse

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;environment&quot;: enum (Environment),&quot;excludedPredefinedFunctions&quot;: [string]}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`environment`

` enum ( Environment  ` )

Required. The environment being operated.

`excludedPredefinedFunctions[]`

`string`

Optional. By default, [predefined functions](https://cloud.google.com/vertex-ai/generative-ai/docs/computer-use#supported-actions) are included in the final model call. Some of them can be explicitly excluded from being automatically included. This can serve two purposes: 1. Using a more restricted / different action space. 2. Improving the definitions / instructions of predefined functions.

### Events

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;event&quot;: [{object (Content)}]}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`event[]`

` object ( Content  ` )

Optional. A list of events.

### AgentsEntry

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;key&quot;: string,&quot;value&quot;: {object (DeprecatedAgentConfig)}}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`key`

`string`

`value`

` object ( DeprecatedAgentConfig  ` )

### DeprecatedAgentConfig

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;agentId&quot;: string,&quot;agentType&quot;: string,&quot;description&quot;: string,&quot;subAgents&quot;: [string],&quot;developerInstruction&quot;: {object (InstanceData)},// Union field tools_data can be only one of the following:&quot;toolsText&quot;: string,&quot;tools&quot;: {object (Tools)}// End of list of possible types for union field tools_data.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`agentId`

`string`

Optional. Unique identifier of the agent. This ID is used to refer to this agent, e.g., in AgentEvent.author, or in the `sub_agents` field. It must be unique within the `agents` map.

`agentType`

`string`

Optional. The type or class of the agent (e.g., "LlmAgent", "RouterAgent", "ToolUseAgent"). Useful for the autorater to understand the expected behavior of the agent.

`description`

`string`

Optional. A high-level description of the agent's role and responsibilities. Critical for evaluating if the agent is routing tasks correctly.

`subAgents[]`

`string`

Optional. The list of valid agent IDs (names) that this agent can delegate to. This defines the directed edges in the agent system graph topology.

`developerInstruction`

` object ( InstanceData  ` )

Optional. Contains instructions from the developer for the agent. Can be static or a dynamic prompt template used with the `AgentEvent.state_delta` field.

Union field `tools_data` . Data for the tools available to the agent. `tools_data` can be only one of the following:

`toolsText`

`string`

A JSON string containing a list of tools available to an agent with info such as name, description, parameters and required parameters.

`tools`

` object ( Tools  ` )

List of tools.

### Tools

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;tool&quot;: [{object (Tool)}]}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`tool[]`

` object ( Tool  ` )

Optional. List of tools: each tool can have multiple function declarations.

### ConversationTurn

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;turnId&quot;: string,&quot;events&quot;: [{object (AgentEvent)}],// Union field _turn_index can be only one of the following:&quot;turnIndex&quot;: integer// End of list of possible types for union field _turn_index.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`turnId`

`string`

Optional. A unique identifier for the turn. Useful for referencing specific turns across systems.

`events[]`

` object ( AgentEvent  ` )

Optional. The list of events that occurred during this turn.

Union field `_turn_index` .

`_turn_index` can be only one of the following:

`turnIndex`

`integer`

Required. The 0-based index of the turn in the conversation sequence.

### AgentEvent

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;content&quot;: {object (Content)},&quot;eventTime&quot;: string,&quot;stateDelta&quot;: {object},&quot;activeTools&quot;: [{object (Tool)}],// Union field _author can be only one of the following:&quot;author&quot;: string// End of list of possible types for union field _author.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`content`

` object ( Content  ` )

Required. The content of the event (e.g., text response, tool call, tool response).

`eventTime`

` string ( Timestamp  ` format)

Optional. The timestamp when the event occurred.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`stateDelta`

` object ( Struct  ` format)

Optional. The change in the session state caused by this event. This is a key-value map of fields that were modified or added by the event.

`activeTools[]`

` object ( Tool  ` )

Optional. The list of tools that were active/available to the agent at the time of this event. This overrides the `AgentConfig.tools` if set.

Union field `_author` .

`_author` can be only one of the following:

`author`

`string`

Required. The ID of the agent or entity that generated this event.

### Timestamp

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
  &quot;seconds&quot;: string,
  &quot;nanos&quot;: integer
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`seconds`

`string ( int64 format)`

Represents seconds of UTC time since Unix epoch 1970-01-01T00:00:00Z. Must be between -62135596800 and 253402300799 inclusive (which corresponds to 0001-01-01T00:00:00Z to 9999-12-31T23:59:59Z).

`nanos`

`integer`

Non-negative fractions of a second at nanosecond resolution. This field is the nanosecond portion of the duration, not an alternative to seconds. Negative second values with fractions must still have non-negative nanos values that count forward in time. Must be between 0 and 999,999,999 inclusive.

### AgentData

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;agents&quot;: {string: {object (AgentConfig)},...},&quot;turns&quot;: [{object (ConversationTurn)}]}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`agents`

` map (key: string, value: object ( AgentConfig  ` ))

Optional. A map containing the static configurations for each agent in the system. Key: agent\_id (matches the `author` field in events). Value: The static configuration of the agent.

An object containing a list of `"key": value` pairs. Example: `{ "name": "wrench", "mass": "1.3kg", "count": "3" }` .

`turns[]`

` object ( ConversationTurn  ` )

Optional. A chronological list of conversation turns. Each turn represents a logical execution cycle (e.g., User Input -\> Agent Response).

### AgentsEntry

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;key&quot;: string,&quot;value&quot;: {object (AgentConfig)}}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`key`

`string`

`value`

` object ( AgentConfig  ` )

### AgentConfig

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;agentType&quot;: string,&quot;description&quot;: string,&quot;instruction&quot;: string,&quot;tools&quot;: [{object (Tool)}],&quot;subAgents&quot;: [string],// Union field _agent_id can be only one of the following:&quot;agentId&quot;: string// End of list of possible types for union field _agent_id.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`agentType`

`string`

Optional. The type or class of the agent (e.g., "LlmAgent", "RouterAgent", "ToolUseAgent"). Useful for the autorater to understand the expected behavior of the agent.

`description`

`string`

Optional. A high-level description of the agent's role and responsibilities. Critical for evaluating if the agent is routing tasks correctly.

`instruction`

`string`

Optional. Provides instructions for the LLM model, guiding the agent's behavior. Can be static or dynamic. Dynamic instructions can contain placeholders like {variable\_name} that will be resolved at runtime using the `AgentEvent.state_delta` field.

`tools[]`

` object ( Tool  ` )

Optional. The list of tools available to this agent.

`subAgents[]`

`string`

Optional. The list of valid agent IDs that this agent can delegate to. This defines the directed edges in the multi-agent system graph topology.

Union field `_agent_id` .

`_agent_id` can be only one of the following:

`agentId`

`string`

Required. Unique identifier of the agent. This ID is used to refer to this agent, e.g., in AgentEvent.author, or in the `sub_agents` field. It must be unique within the `agents` map.

### ConversationTurn

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;turnId&quot;: string,&quot;events&quot;: [{object (AgentEvent)}],// Union field _turn_index can be only one of the following:&quot;turnIndex&quot;: integer// End of list of possible types for union field _turn_index.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`turnId`

`string`

Optional. A unique identifier for the turn. Useful for referencing specific turns across systems.

`events[]`

` object ( AgentEvent  ` )

Optional. The list of events that occurred during this turn.

Union field `_turn_index` .

`_turn_index` can be only one of the following:

`turnIndex`

`integer`

Required. The 0-based index of the turn in the conversation sequence.

### AgentEvent

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;eventTime&quot;: string,&quot;stateDelta&quot;: {object},&quot;activeTools&quot;: [{object (Tool)}],// Union field _author can be only one of the following:&quot;author&quot;: string// End of list of possible types for union field _author.// Union field _content can be only one of the following:&quot;content&quot;: {object (Content)}// End of list of possible types for union field _content.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`eventTime`

` string ( Timestamp  ` format)

Optional. The timestamp when the event occurred.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`stateDelta`

` object ( Struct  ` format)

Optional. The change in the session state caused by this event. This is a key-value map of fields that were modified or added by the event.

`activeTools[]`

` object ( Tool  ` )

Optional. The list of tools that were active/available to the agent at the time of this event. This overrides the `AgentConfig.tools` if set.

Union field `_author` .

`_author` can be only one of the following:

`author`

`string`

Required. The ID of the agent or entity that generated this event. Use "user" to denote events generated by the end-user.

Union field `_content` .

`_content` can be only one of the following:

`content`

` object ( Content  ` )

Required. The content of the event (e.g., text response, tool call, tool response).

### NullValue

Represents a JSON `null` .

`NullValue` is a sentinel, using an enum with only one value to represent the null value for the `Value` type union.

A field of type `NullValue` with any value other than `0` is considered invalid. Most ProtoJSON serializers will emit a `Value` with a `null_value` set as a JSON `null` regardless of the integer value, and so will round trip to a `0` value.

Enums

`NULL_VALUE`

Null value.

### Language

Supported programming languages for the generated code.

Enums

`LANGUAGE_UNSPECIFIED`

Unspecified language. This value should not be used.

`PYTHON`

Python \>= 3.10, with numpy and simpy available.

### Outcome

Enumeration of possible outcomes of the code execution.

Enums

`OUTCOME_UNSPECIFIED`

Unspecified status. This value should not be used.

`OUTCOME_OK`

Code execution completed successfully. `output` contains the stdout, if any.

`OUTCOME_FAILED`

Code execution failed. `output` contains the stderr and stdout, if any.

`OUTCOME_DEADLINE_EXCEEDED`

Code execution ran for too long, and was cancelled. There may or may not be a partial `output` present.

### Level

The media resolution level.

Enums

`MEDIA_RESOLUTION_UNSPECIFIED`

Media resolution has not been set.

`MEDIA_RESOLUTION_LOW`

Media resolution set to low.

`MEDIA_RESOLUTION_MEDIUM`

Media resolution set to medium.

`MEDIA_RESOLUTION_HIGH`

Media resolution set to high.

`MEDIA_RESOLUTION_ULTRA_HIGH`

Media resolution set to ultra high. This is for image only.

### CometVersion

Comet version options.

Enums

`COMET_VERSION_UNSPECIFIED`

Comet version unspecified.

`COMET_22_SRC_REF`

Comet 22 for translation + source + reference (source-reference-combined).

### MetricxVersion

MetricX Version options.

Enums

`METRICX_VERSION_UNSPECIFIED`

MetricX version unspecified.

`METRICX_24_REF`

MetricX 2024 (2.6) for translation + reference (reference-based).

`METRICX_24_SRC`

MetricX 2024 (2.6) for translation + source (QE).

`METRICX_24_SRC_REF`

MetricX 2024 (2.6) for translation + source + reference (source-reference-combined).

### ComputationBasedMetricType

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

### Type

Type contains the list of OpenAPI data types as defined by <https://swagger.io/docs/specification/data-models/data-types/>

Enums

`TYPE_UNSPECIFIED`

Not specified, should not be used.

`STRING`

OpenAPI string type

`NUMBER`

OpenAPI number type

`INTEGER`

OpenAPI integer type

`BOOLEAN`

OpenAPI boolean type

`ARRAY`

OpenAPI array type

`OBJECT`

OpenAPI object type

`NULL`

Null type

### ModelRoutingPreference

The model routing preference.

Enums

`UNKNOWN`

Unspecified model routing preference.

`PRIORITIZE_QUALITY`

The model will be selected to prioritize the quality of the response.

`BALANCED`

The model will be selected to balance quality and cost.

`PRIORITIZE_COST`

The model will be selected to prioritize the cost of the request.

### Modality

The modalities of the response.

Enums

`MODALITY_UNSPECIFIED`

Unspecified modality. Will be processed as text.

`TEXT`

Text modality.

`IMAGE`

Image modality.

`AUDIO`

Audio modality.

`VIDEO`

Video modality.

### MediaResolution

Media resolution for the input media.

Enums

`MEDIA_RESOLUTION_UNSPECIFIED`

Media resolution has not been set.

`MEDIA_RESOLUTION_LOW`

Media resolution set to low (64 tokens).

`MEDIA_RESOLUTION_MEDIUM`

Media resolution set to medium (256 tokens).

`MEDIA_RESOLUTION_HIGH`

Media resolution set to high (zoomed reframing with 256 tokens).

### ThinkingLevel

The thinking level for the model.

Enums

`THINKING_LEVEL_UNSPECIFIED`

Unspecified thinking level.

`LOW`

Low thinking level.

`MEDIUM`

Medium thinking level.

`HIGH`

High thinking level.

`MINIMAL`

MINIMAL thinking level.

### FeatureSelectionPreference

Options for feature selection preference.

Enums

`FEATURE_SELECTION_PREFERENCE_UNSPECIFIED`

Unspecified feature selection preference.

`PRIORITIZE_QUALITY`

Prefer higher quality over lower cost.

`BALANCED`

Balanced feature selection preference.

`PRIORITIZE_COST`

Prefer lower cost over higher quality.

### PersonGeneration

Enum for controlling the generation of people in images.

Enums

`PERSON_GENERATION_UNSPECIFIED`

The default behavior is unspecified. The model will decide whether to generate images of people.

`ALLOW_ALL`

Allows the model to generate images of people, including adults and children.

`ALLOW_ADULT`

Allows the model to generate images of adults, but not children.

`ALLOW_NONE`

Prevents the model from generating images of people.

### MimeType

Supported MIME types for text output.

Enums

`MIME_TYPE_UNSPECIFIED`

Default value. This value is unused.

`APPLICATION_JSON`

JSON output format.

`TEXT_PLAIN`

Plain text output format.

### MimeType

Supported MIME types for audio output.

Enums

`MIME_TYPE_UNSPECIFIED`

Default value. This value is unused.

`AUDIO_MP3`

MP3 audio format.

`AUDIO_OGG_OPUS`

OGG Opus audio format.

`AUDIO_L16`

Raw PCM (L16) audio format.

`AUDIO_WAV`

WAV audio format.

`AUDIO_ALAW`

A-law audio format.

`AUDIO_MULAW`

Mu-law audio format.

### DeliveryMode

The delivery mode for the output content.

Enums

`DELIVERY_UNSPECIFIED`

Default value. This value is unused.

`INLINE`

Generated bytes are returned inline in the response.

`URI`

Generated content is stored and a URI is returned.

### MimeType

Supported MIME types for image output.

Enums

`MIME_TYPE_UNSPECIFIED`

Default value. This value is unused.

`IMAGE_JPEG`

JPEG image format.

### AspectRatio

Supported aspect ratios for image output.

Enums

`ASPECT_RATIO_UNSPECIFIED`

Default value. This value is unused.

`ASPECT_RATIO_ONE_BY_ONE`

1:1 aspect ratio.

`ASPECT_RATIO_TWO_BY_THREE`

2:3 aspect ratio.

`ASPECT_RATIO_THREE_BY_TWO`

3:2 aspect ratio.

`ASPECT_RATIO_THREE_BY_FOUR`

3:4 aspect ratio.

`ASPECT_RATIO_FOUR_BY_THREE`

4:3 aspect ratio.

`ASPECT_RATIO_FOUR_BY_FIVE`

4:5 aspect ratio.

`ASPECT_RATIO_FIVE_BY_FOUR`

5:4 aspect ratio.

`ASPECT_RATIO_NINE_BY_SIXTEEN`

9:16 aspect ratio.

`ASPECT_RATIO_SIXTEEN_BY_NINE`

16:9 aspect ratio.

`ASPECT_RATIO_TWENTY_ONE_BY_NINE`

21:9 aspect ratio.

`ASPECT_RATIO_ONE_BY_EIGHT`

1:8 aspect ratio.

`ASPECT_RATIO_EIGHT_BY_ONE`

8:1 aspect ratio.

`ASPECT_RATIO_ONE_BY_FOUR`

1:4 aspect ratio.

`ASPECT_RATIO_FOUR_BY_ONE`

4:1 aspect ratio.

### ImageSize

Supported image sizes for image output.

Enums

`IMAGE_SIZE_UNSPECIFIED`

Default value. This value is unused.

`IMAGE_SIZE_FIVE_TWELVE`

512px image size.

`IMAGE_SIZE_ONE_K`

1K image size.

`IMAGE_SIZE_TWO_K`

2K image size.

`IMAGE_SIZE_FOUR_K`

4K image size.

### AspectRatio

Supported aspect ratios for video output.

Enums

`ASPECT_RATIO_UNSPECIFIED`

Default value. This value is unused.

`ASPECT_RATIO_SIXTEEN_BY_NINE`

16:9 aspect ratio.

`ASPECT_RATIO_NINE_BY_SIXTEEN`

9:16 aspect ratio.

### RubricContentType

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

### AggregationMetric

The per-metric statistics on evaluation results supported by `EvaluationService.EvaluateDataset` .

Enums

`AGGREGATION_METRIC_UNSPECIFIED`

Unspecified aggregation metric.

`AVERAGE`

Average aggregation metric. Not supported for Pairwise metric.

`MODE`

Mode aggregation metric.

`STANDARD_DEVIATION`

Standard deviation aggregation metric. Not supported for pairwise metric.

`VARIANCE`

Variance aggregation metric. Not supported for pairwise metric.

`MINIMUM`

Minimum aggregation metric. Not supported for pairwise metric.

`MAXIMUM`

Maximum aggregation metric. Not supported for pairwise metric.

`MEDIAN`

Median aggregation metric. Not supported for pairwise metric.

`PERCENTILE_P90`

90th percentile aggregation metric. Not supported for pairwise metric.

`PERCENTILE_P95`

95th percentile aggregation metric. Not supported for pairwise metric.

`PERCENTILE_P99`

99th percentile aggregation metric. Not supported for pairwise metric.

### Importance

Importance level of the rubric.

Enums

`IMPORTANCE_UNSPECIFIED`

Importance is not specified.

`HIGH`

High importance.

`MEDIUM`

Medium importance.

`LOW`

Low importance.

### PhishBlockThreshold

These are available confidence level user can set to block malicious urls with chosen confidence and above. For understanding different confidence of webrisk, please refer to <https://cloud.google.com/web-risk/docs/reference/rpc/google.cloud.webrisk.v1eap1#confidencelevel>

Enums

`PHISH_BLOCK_THRESHOLD_UNSPECIFIED`

Defaults to unspecified.

`BLOCK_LOW_AND_ABOVE`

Blocks Low and above confidence URL that is risky.

`BLOCK_MEDIUM_AND_ABOVE`

Blocks Medium and above confidence URL that is risky.

`BLOCK_HIGH_AND_ABOVE`

Blocks High and above confidence URL that is risky.

`BLOCK_HIGHER_AND_ABOVE`

Blocks Higher and above confidence URL that is risky.

`BLOCK_VERY_HIGH_AND_ABOVE`

Blocks Very high and above confidence URL that is risky.

`BLOCK_ONLY_EXTREMELY_HIGH`

Blocks Extremely high confidence URL that is risky.

### Mode

The mode of the predictor to be used in dynamic retrieval.

Enums

`MODE_UNSPECIFIED`

Always trigger retrieval.

`MODE_DYNAMIC`

Run retrieval only when system decides it is necessary.

### Environment

Represents the environment being operated, such as a web browser.

Enums

`ENVIRONMENT_UNSPECIFIED`

Defaults to browser.

`ENVIRONMENT_BROWSER`

Operates in a web browser.

## Output Schema

Response message for EvaluationService.EvaluateInstances.

### EvaluateInstancesResponse

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;metricResults&quot;: [{object (MetricResult)}],// Union field evaluation_results can be only one of the following:&quot;exactMatchResults&quot;: {object (ExactMatchResults)},&quot;bleuResults&quot;: {object (BleuResults)},&quot;rougeResults&quot;: {object (RougeResults)},&quot;fluencyResult&quot;: {object (FluencyResult)},&quot;coherenceResult&quot;: {object (CoherenceResult)},&quot;safetyResult&quot;: {object (SafetyResult)},&quot;groundednessResult&quot;: {object (GroundednessResult)},&quot;fulfillmentResult&quot;: {object (FulfillmentResult)},&quot;summarizationQualityResult&quot;: {object (SummarizationQualityResult)},&quot;pairwiseSummarizationQualityResult&quot;: {object (PairwiseSummarizationQualityResult)},&quot;summarizationHelpfulnessResult&quot;: {object (SummarizationHelpfulnessResult)},&quot;summarizationVerbosityResult&quot;: {object (SummarizationVerbosityResult)},&quot;questionAnsweringQualityResult&quot;: {object (QuestionAnsweringQualityResult)},&quot;pairwiseQuestionAnsweringQualityResult&quot;: {object (PairwiseQuestionAnsweringQualityResult)},&quot;questionAnsweringRelevanceResult&quot;: {object (QuestionAnsweringRelevanceResult)},&quot;questionAnsweringHelpfulnessResult&quot;: {object (QuestionAnsweringHelpfulnessResult)},&quot;questionAnsweringCorrectnessResult&quot;: {object (QuestionAnsweringCorrectnessResult)},&quot;pointwiseMetricResult&quot;: {object (PointwiseMetricResult)},&quot;pairwiseMetricResult&quot;: {object (PairwiseMetricResult)},&quot;toolCallValidResults&quot;: {object (ToolCallValidResults)},&quot;toolNameMatchResults&quot;: {object (ToolNameMatchResults)},&quot;toolParameterKeyMatchResults&quot;: {object (ToolParameterKeyMatchResults)},&quot;toolParameterKvMatchResults&quot;: {object (ToolParameterKVMatchResults)},&quot;cometResult&quot;: {object (CometResult)},&quot;metricxResult&quot;: {object (MetricxResult)},&quot;trajectoryExactMatchResults&quot;: {object (TrajectoryExactMatchResults)},&quot;trajectoryInOrderMatchResults&quot;: {object (TrajectoryInOrderMatchResults)},&quot;trajectoryAnyOrderMatchResults&quot;: {object (TrajectoryAnyOrderMatchResults)},&quot;trajectoryPrecisionResults&quot;: {object (TrajectoryPrecisionResults)},&quot;trajectoryRecallResults&quot;: {object (TrajectoryRecallResults)},&quot;trajectorySingleToolUseResults&quot;: {object (TrajectorySingleToolUseResults)},&quot;rubricBasedInstructionFollowingResult&quot;: {object (RubricBasedInstructionFollowingResult)}// End of list of possible types for union field evaluation_results.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`metricResults[]`

` object ( MetricResult  ` )

Metric results for each instance. The order of the metric results is guaranteed to be the same as the order of the instances in the request.

Union field `evaluation_results` . Evaluation results will be served in the same order as presented in EvaluationRequest.instances. `evaluation_results` can be only one of the following:

`exactMatchResults`

` object ( ExactMatchResults  ` )

Auto metric evaluation results. Results for exact match metric.

`bleuResults`

` object ( BleuResults  ` )

Results for bleu metric.

`rougeResults`

` object ( RougeResults  ` )

Results for rouge metric.

`fluencyResult`

` object ( FluencyResult  ` )

LLM-based metric evaluation result. General text generation metrics, applicable to other categories. Result for fluency metric.

`coherenceResult`

` object ( CoherenceResult  ` )

Result for coherence metric.

`safetyResult`

` object ( SafetyResult  ` )

Result for safety metric.

`groundednessResult`

` object ( GroundednessResult  ` )

Result for groundedness metric.

`fulfillmentResult`

` object ( FulfillmentResult  ` )

Result for fulfillment metric.

`summarizationQualityResult`

` object ( SummarizationQualityResult  ` )

Summarization only metrics. Result for summarization quality metric.

`pairwiseSummarizationQualityResult`

` object ( PairwiseSummarizationQualityResult  ` )

Result for pairwise summarization quality metric.

`summarizationHelpfulnessResult`

` object ( SummarizationHelpfulnessResult  ` )

Result for summarization helpfulness metric.

`summarizationVerbosityResult`

` object ( SummarizationVerbosityResult  ` )

Result for summarization verbosity metric.

`questionAnsweringQualityResult`

` object ( QuestionAnsweringQualityResult  ` )

Question answering only metrics. Result for question answering quality metric.

`pairwiseQuestionAnsweringQualityResult`

` object ( PairwiseQuestionAnsweringQualityResult  ` )

Result for pairwise question answering quality metric.

`questionAnsweringRelevanceResult`

` object ( QuestionAnsweringRelevanceResult  ` )

Result for question answering relevance metric.

`questionAnsweringHelpfulnessResult`

` object ( QuestionAnsweringHelpfulnessResult  ` )

Result for question answering helpfulness metric.

`questionAnsweringCorrectnessResult`

` object ( QuestionAnsweringCorrectnessResult  ` )

Result for question answering correctness metric.

`pointwiseMetricResult`

` object ( PointwiseMetricResult  ` )

Generic metrics. Result for pointwise metric.

`pairwiseMetricResult`

` object ( PairwiseMetricResult  ` )

Result for pairwise metric.

`toolCallValidResults`

` object ( ToolCallValidResults  ` )

Tool call metrics. Results for tool call valid metric.

`toolNameMatchResults`

` object ( ToolNameMatchResults  ` )

Results for tool name match metric.

`toolParameterKeyMatchResults`

` object ( ToolParameterKeyMatchResults  ` )

Results for tool parameter key match metric.

`toolParameterKvMatchResults`

` object ( ToolParameterKVMatchResults  ` )

Results for tool parameter key value match metric.

`cometResult`

` object ( CometResult  ` )

Translation metrics. Result for Comet metric.

`metricxResult`

` object ( MetricxResult  ` )

Result for Metricx metric.

`trajectoryExactMatchResults`

` object ( TrajectoryExactMatchResults  ` )

Result for trajectory exact match metric.

`trajectoryInOrderMatchResults`

` object ( TrajectoryInOrderMatchResults  ` )

Result for trajectory in order match metric.

`trajectoryAnyOrderMatchResults`

` object ( TrajectoryAnyOrderMatchResults  ` )

Result for trajectory any order match metric.

`trajectoryPrecisionResults`

` object ( TrajectoryPrecisionResults  ` )

Result for trajectory precision metric.

`trajectoryRecallResults`

` object ( TrajectoryRecallResults  ` )

Results for trajectory recall metric.

`trajectorySingleToolUseResults`

` object ( TrajectorySingleToolUseResults  ` )

Results for trajectory single tool use metric.

`rubricBasedInstructionFollowingResult`

` object ( RubricBasedInstructionFollowingResult  ` )

Result for rubric based instruction following metric.

### ExactMatchResults

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

Fields

`exactMatchMetricValues[]`

` object ( ExactMatchMetricValue  ` )

Output only. Exact match metric values.

### ExactMatchMetricValue

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{// Union field _score can be only one of the following:&quot;score&quot;: number// End of list of possible types for union field _score.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

Union field `_score` .

`_score` can be only one of the following:

`score`

`number`

Output only. Exact match score.

### BleuResults

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

Fields

`bleuMetricValues[]`

` object ( BleuMetricValue  ` )

Output only. Bleu metric values.

### BleuMetricValue

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{// Union field _score can be only one of the following:&quot;score&quot;: number// End of list of possible types for union field _score.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

Union field `_score` .

`_score` can be only one of the following:

`score`

`number`

Output only. Bleu score.

### RougeResults

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

Fields

`rougeMetricValues[]`

` object ( RougeMetricValue  ` )

Output only. Rouge metric values.

### RougeMetricValue

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{// Union field _score can be only one of the following:&quot;score&quot;: number// End of list of possible types for union field _score.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

Union field `_score` .

`_score` can be only one of the following:

`score`

`number`

Output only. Rouge score.

### FluencyResult

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;explanation&quot;: string,// Union field _score can be only one of the following:&quot;score&quot;: number// End of list of possible types for union field _score.// Union field _confidence can be only one of the following:&quot;confidence&quot;: number// End of list of possible types for union field _confidence.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`explanation`

`string`

Output only. Explanation for fluency score.

Union field `_score` .

`_score` can be only one of the following:

`score`

`number`

Output only. Fluency score.

Union field `_confidence` .

`_confidence` can be only one of the following:

`confidence`

`number`

Output only. Confidence for fluency score.

### CoherenceResult

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;explanation&quot;: string,// Union field _score can be only one of the following:&quot;score&quot;: number// End of list of possible types for union field _score.// Union field _confidence can be only one of the following:&quot;confidence&quot;: number// End of list of possible types for union field _confidence.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`explanation`

`string`

Output only. Explanation for coherence score.

Union field `_score` .

`_score` can be only one of the following:

`score`

`number`

Output only. Coherence score.

Union field `_confidence` .

`_confidence` can be only one of the following:

`confidence`

`number`

Output only. Confidence for coherence score.

### SafetyResult

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;explanation&quot;: string,// Union field _score can be only one of the following:&quot;score&quot;: number// End of list of possible types for union field _score.// Union field _confidence can be only one of the following:&quot;confidence&quot;: number// End of list of possible types for union field _confidence.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`explanation`

`string`

Output only. Explanation for safety score.

Union field `_score` .

`_score` can be only one of the following:

`score`

`number`

Output only. Safety score.

Union field `_confidence` .

`_confidence` can be only one of the following:

`confidence`

`number`

Output only. Confidence for safety score.

### GroundednessResult

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;explanation&quot;: string,// Union field _score can be only one of the following:&quot;score&quot;: number// End of list of possible types for union field _score.// Union field _confidence can be only one of the following:&quot;confidence&quot;: number// End of list of possible types for union field _confidence.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`explanation`

`string`

Output only. Explanation for groundedness score.

Union field `_score` .

`_score` can be only one of the following:

`score`

`number`

Output only. Groundedness score.

Union field `_confidence` .

`_confidence` can be only one of the following:

`confidence`

`number`

Output only. Confidence for groundedness score.

### FulfillmentResult

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;explanation&quot;: string,// Union field _score can be only one of the following:&quot;score&quot;: number// End of list of possible types for union field _score.// Union field _confidence can be only one of the following:&quot;confidence&quot;: number// End of list of possible types for union field _confidence.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`explanation`

`string`

Output only. Explanation for fulfillment score.

Union field `_score` .

`_score` can be only one of the following:

`score`

`number`

Output only. Fulfillment score.

Union field `_confidence` .

`_confidence` can be only one of the following:

`confidence`

`number`

Output only. Confidence for fulfillment score.

### SummarizationQualityResult

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;explanation&quot;: string,// Union field _score can be only one of the following:&quot;score&quot;: number// End of list of possible types for union field _score.// Union field _confidence can be only one of the following:&quot;confidence&quot;: number// End of list of possible types for union field _confidence.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`explanation`

`string`

Output only. Explanation for summarization quality score.

Union field `_score` .

`_score` can be only one of the following:

`score`

`number`

Output only. Summarization Quality score.

Union field `_confidence` .

`_confidence` can be only one of the following:

`confidence`

`number`

Output only. Confidence for summarization quality score.

### PairwiseSummarizationQualityResult

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;pairwiseChoice&quot;: enum (PairwiseChoice),&quot;explanation&quot;: string,// Union field _confidence can be only one of the following:&quot;confidence&quot;: number// End of list of possible types for union field _confidence.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`pairwiseChoice`

` enum ( PairwiseChoice  ` )

Output only. Pairwise summarization prediction choice.

`explanation`

`string`

Output only. Explanation for summarization quality score.

Union field `_confidence` .

`_confidence` can be only one of the following:

`confidence`

`number`

Output only. Confidence for summarization quality score.

### SummarizationHelpfulnessResult

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;explanation&quot;: string,// Union field _score can be only one of the following:&quot;score&quot;: number// End of list of possible types for union field _score.// Union field _confidence can be only one of the following:&quot;confidence&quot;: number// End of list of possible types for union field _confidence.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`explanation`

`string`

Output only. Explanation for summarization helpfulness score.

Union field `_score` .

`_score` can be only one of the following:

`score`

`number`

Output only. Summarization Helpfulness score.

Union field `_confidence` .

`_confidence` can be only one of the following:

`confidence`

`number`

Output only. Confidence for summarization helpfulness score.

### SummarizationVerbosityResult

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;explanation&quot;: string,// Union field _score can be only one of the following:&quot;score&quot;: number// End of list of possible types for union field _score.// Union field _confidence can be only one of the following:&quot;confidence&quot;: number// End of list of possible types for union field _confidence.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`explanation`

`string`

Output only. Explanation for summarization verbosity score.

Union field `_score` .

`_score` can be only one of the following:

`score`

`number`

Output only. Summarization Verbosity score.

Union field `_confidence` .

`_confidence` can be only one of the following:

`confidence`

`number`

Output only. Confidence for summarization verbosity score.

### QuestionAnsweringQualityResult

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;explanation&quot;: string,// Union field _score can be only one of the following:&quot;score&quot;: number// End of list of possible types for union field _score.// Union field _confidence can be only one of the following:&quot;confidence&quot;: number// End of list of possible types for union field _confidence.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`explanation`

`string`

Output only. Explanation for question answering quality score.

Union field `_score` .

`_score` can be only one of the following:

`score`

`number`

Output only. Question Answering Quality score.

Union field `_confidence` .

`_confidence` can be only one of the following:

`confidence`

`number`

Output only. Confidence for question answering quality score.

### PairwiseQuestionAnsweringQualityResult

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;pairwiseChoice&quot;: enum (PairwiseChoice),&quot;explanation&quot;: string,// Union field _confidence can be only one of the following:&quot;confidence&quot;: number// End of list of possible types for union field _confidence.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`pairwiseChoice`

` enum ( PairwiseChoice  ` )

Output only. Pairwise question answering prediction choice.

`explanation`

`string`

Output only. Explanation for question answering quality score.

Union field `_confidence` .

`_confidence` can be only one of the following:

`confidence`

`number`

Output only. Confidence for question answering quality score.

### QuestionAnsweringRelevanceResult

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;explanation&quot;: string,// Union field _score can be only one of the following:&quot;score&quot;: number// End of list of possible types for union field _score.// Union field _confidence can be only one of the following:&quot;confidence&quot;: number// End of list of possible types for union field _confidence.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`explanation`

`string`

Output only. Explanation for question answering relevance score.

Union field `_score` .

`_score` can be only one of the following:

`score`

`number`

Output only. Question Answering Relevance score.

Union field `_confidence` .

`_confidence` can be only one of the following:

`confidence`

`number`

Output only. Confidence for question answering relevance score.

### QuestionAnsweringHelpfulnessResult

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;explanation&quot;: string,// Union field _score can be only one of the following:&quot;score&quot;: number// End of list of possible types for union field _score.// Union field _confidence can be only one of the following:&quot;confidence&quot;: number// End of list of possible types for union field _confidence.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`explanation`

`string`

Output only. Explanation for question answering helpfulness score.

Union field `_score` .

`_score` can be only one of the following:

`score`

`number`

Output only. Question Answering Helpfulness score.

Union field `_confidence` .

`_confidence` can be only one of the following:

`confidence`

`number`

Output only. Confidence for question answering helpfulness score.

### QuestionAnsweringCorrectnessResult

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;explanation&quot;: string,// Union field _score can be only one of the following:&quot;score&quot;: number// End of list of possible types for union field _score.// Union field _confidence can be only one of the following:&quot;confidence&quot;: number// End of list of possible types for union field _confidence.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`explanation`

`string`

Output only. Explanation for question answering correctness score.

Union field `_score` .

`_score` can be only one of the following:

`score`

`number`

Output only. Question Answering Correctness score.

Union field `_confidence` .

`_confidence` can be only one of the following:

`confidence`

`number`

Output only. Confidence for question answering correctness score.

### PointwiseMetricResult

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;explanation&quot;: string,&quot;customOutput&quot;: {object (CustomOutput)},// Union field _score can be only one of the following:&quot;score&quot;: number// End of list of possible types for union field _score.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`explanation`

`string`

Output only. Explanation for pointwise metric score.

`customOutput`

` object ( CustomOutput  ` )

Output only. Spec for custom output.

Union field `_score` .

`_score` can be only one of the following:

`score`

`number`

Output only. Pointwise metric score.

### CustomOutput

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{// Union field custom_output can be only one of the following:&quot;rawOutputs&quot;: {object (RawOutput)}// End of list of possible types for union field custom_output.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

Union field `custom_output` . Custom output. `custom_output` can be only one of the following:

`rawOutputs`

` object ( RawOutput  ` )

Output only. List of raw output strings.

### RawOutput

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
  &quot;rawOutput&quot;: [
    string
  ]
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`rawOutput[]`

`string`

Output only. Raw output string.

### PairwiseMetricResult

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;pairwiseChoice&quot;: enum (PairwiseChoice),&quot;explanation&quot;: string,&quot;customOutput&quot;: {object (CustomOutput)}}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`pairwiseChoice`

` enum ( PairwiseChoice  ` )

Output only. Pairwise metric choice.

`explanation`

`string`

Output only. Explanation for pairwise metric score.

`customOutput`

` object ( CustomOutput  ` )

Output only. Spec for custom output.

### ToolCallValidResults

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

Fields

`toolCallValidMetricValues[]`

` object ( ToolCallValidMetricValue  ` )

Output only. Tool call valid metric values.

### ToolCallValidMetricValue

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{// Union field _score can be only one of the following:&quot;score&quot;: number// End of list of possible types for union field _score.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

Union field `_score` .

`_score` can be only one of the following:

`score`

`number`

Output only. Tool call valid score.

### ToolNameMatchResults

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

Fields

`toolNameMatchMetricValues[]`

` object ( ToolNameMatchMetricValue  ` )

Output only. Tool name match metric values.

### ToolNameMatchMetricValue

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{// Union field _score can be only one of the following:&quot;score&quot;: number// End of list of possible types for union field _score.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

Union field `_score` .

`_score` can be only one of the following:

`score`

`number`

Output only. Tool name match score.

### ToolParameterKeyMatchResults

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

Fields

`toolParameterKeyMatchMetricValues[]`

` object ( ToolParameterKeyMatchMetricValue  ` )

Output only. Tool parameter key match metric values.

### ToolParameterKeyMatchMetricValue

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{// Union field _score can be only one of the following:&quot;score&quot;: number// End of list of possible types for union field _score.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

Union field `_score` .

`_score` can be only one of the following:

`score`

`number`

Output only. Tool parameter key match score.

### ToolParameterKVMatchResults

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

Fields

`toolParameterKvMatchMetricValues[]`

` object ( ToolParameterKVMatchMetricValue  ` )

Output only. Tool parameter key value match metric values.

### ToolParameterKVMatchMetricValue

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{// Union field _score can be only one of the following:&quot;score&quot;: number// End of list of possible types for union field _score.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

Union field `_score` .

`_score` can be only one of the following:

`score`

`number`

Output only. Tool parameter key value match score.

### CometResult

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{// Union field _score can be only one of the following:&quot;score&quot;: number// End of list of possible types for union field _score.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

Union field `_score` .

`_score` can be only one of the following:

`score`

`number`

Output only. Comet score. Range depends on version.

### MetricxResult

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{// Union field _score can be only one of the following:&quot;score&quot;: number// End of list of possible types for union field _score.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

Union field `_score` .

`_score` can be only one of the following:

`score`

`number`

Output only. MetricX score. Range depends on version.

### TrajectoryExactMatchResults

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

Fields

`trajectoryExactMatchMetricValues[]`

` object ( TrajectoryExactMatchMetricValue  ` )

Output only. TrajectoryExactMatch metric values.

### TrajectoryExactMatchMetricValue

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{// Union field _score can be only one of the following:&quot;score&quot;: number// End of list of possible types for union field _score.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

Union field `_score` .

`_score` can be only one of the following:

`score`

`number`

Output only. TrajectoryExactMatch score.

### TrajectoryInOrderMatchResults

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

Fields

`trajectoryInOrderMatchMetricValues[]`

` object ( TrajectoryInOrderMatchMetricValue  ` )

Output only. TrajectoryInOrderMatch metric values.

### TrajectoryInOrderMatchMetricValue

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{// Union field _score can be only one of the following:&quot;score&quot;: number// End of list of possible types for union field _score.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

Union field `_score` .

`_score` can be only one of the following:

`score`

`number`

Output only. TrajectoryInOrderMatch score.

### TrajectoryAnyOrderMatchResults

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

Fields

`trajectoryAnyOrderMatchMetricValues[]`

` object ( TrajectoryAnyOrderMatchMetricValue  ` )

Output only. TrajectoryAnyOrderMatch metric values.

### TrajectoryAnyOrderMatchMetricValue

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{// Union field _score can be only one of the following:&quot;score&quot;: number// End of list of possible types for union field _score.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

Union field `_score` .

`_score` can be only one of the following:

`score`

`number`

Output only. TrajectoryAnyOrderMatch score.

### TrajectoryPrecisionResults

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

Fields

`trajectoryPrecisionMetricValues[]`

` object ( TrajectoryPrecisionMetricValue  ` )

Output only. TrajectoryPrecision metric values.

### TrajectoryPrecisionMetricValue

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{// Union field _score can be only one of the following:&quot;score&quot;: number// End of list of possible types for union field _score.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

Union field `_score` .

`_score` can be only one of the following:

`score`

`number`

Output only. TrajectoryPrecision score.

### TrajectoryRecallResults

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

Fields

`trajectoryRecallMetricValues[]`

` object ( TrajectoryRecallMetricValue  ` )

Output only. TrajectoryRecall metric values.

### TrajectoryRecallMetricValue

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{// Union field _score can be only one of the following:&quot;score&quot;: number// End of list of possible types for union field _score.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

Union field `_score` .

`_score` can be only one of the following:

`score`

`number`

Output only. TrajectoryRecall score.

### TrajectorySingleToolUseResults

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

Fields

`trajectorySingleToolUseMetricValues[]`

` object ( TrajectorySingleToolUseMetricValue  ` )

Output only. TrajectorySingleToolUse metric values.

### TrajectorySingleToolUseMetricValue

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{// Union field _score can be only one of the following:&quot;score&quot;: number// End of list of possible types for union field _score.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

Union field `_score` .

`_score` can be only one of the following:

`score`

`number`

Output only. TrajectorySingleToolUse score.

### RubricBasedInstructionFollowingResult

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;rubricCritiqueResults&quot;: [{object (RubricCritiqueResult)}],// Union field _score can be only one of the following:&quot;score&quot;: number// End of list of possible types for union field _score.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`rubricCritiqueResults[]`

` object ( RubricCritiqueResult  ` )

Output only. List of per rubric critique results.

Union field `_score` .

`_score` can be only one of the following:

`score`

`number`

Output only. Overall score for the instruction following.

### RubricCritiqueResult

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
  &quot;rubric&quot;: string,
  &quot;verdict&quot;: boolean
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`rubric`

`string`

Output only. Rubric to be evaluated.

`verdict`

`boolean`

Output only. Verdict for the rubric - true if the rubric is met, false otherwise.

### MetricResult

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;rubricVerdicts&quot;: [{object (RubricVerdict)}],// Union field _score can be only one of the following:&quot;score&quot;: number// End of list of possible types for union field _score.// Union field _explanation can be only one of the following:&quot;explanation&quot;: string// End of list of possible types for union field _explanation.// Union field _error can be only one of the following:&quot;error&quot;: {object (Status)}// End of list of possible types for union field _error.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`rubricVerdicts[]`

` object ( RubricVerdict  ` )

Output only. For rubric-based metrics, the verdicts for each rubric.

Union field `_score` .

`_score` can be only one of the following:

`score`

`number`

Output only. The score for the metric. Please refer to each metric's documentation for the meaning of the score.

Union field `_explanation` .

`_explanation` can be only one of the following:

`explanation`

`string`

Output only. The explanation for the metric result.

Union field `_error` .

`_error` can be only one of the following:

`error`

` object ( Status  ` )

Output only. The error status for the metric result.

### RubricVerdict

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;evaluatedRubric&quot;: {object (Rubric)},&quot;verdict&quot;: boolean,// Union field _reasoning can be only one of the following:&quot;reasoning&quot;: string// End of list of possible types for union field _reasoning.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`evaluatedRubric`

` object ( Rubric  ` )

Required. The full rubric definition that was evaluated. Storing this ensures the verdict is self-contained and understandable, especially if the original rubric definition changes or was dynamically generated.

`verdict`

`boolean`

Required. Outcome of the evaluation against the rubric, represented as a boolean. `true` indicates a "Pass", `false` indicates a "Fail".

Union field `_reasoning` .

`_reasoning` can be only one of the following:

`reasoning`

`string`

Optional. Human-readable reasoning or explanation for the verdict. This can include specific examples or details from the evaluated content that justify the given verdict.

### Rubric

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;rubricId&quot;: string,&quot;content&quot;: {object (Content)},// Union field _type can be only one of the following:&quot;type&quot;: string// End of list of possible types for union field _type.// Union field _importance can be only one of the following:&quot;importance&quot;: enum (Importance)// End of list of possible types for union field _importance.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`rubricId`

`string`

Unique identifier for the rubric. This ID is used to refer to this rubric, e.g., in RubricVerdict.

`content`

` object ( Content  ` )

Required. The actual testable criteria for the rubric.

Union field `_type` .

`_type` can be only one of the following:

`type`

`string`

Optional. A type designator for the rubric, which can inform how it's evaluated or interpreted by systems or users. It's recommended to use consistent, well-defined, upper snake\_case strings. Examples: "SUMMARIZATION\_QUALITY", "SAFETY\_HARMFUL\_CONTENT", "INSTRUCTION\_ADHERENCE".

Union field `_importance` .

`_importance` can be only one of the following:

`importance`

` enum ( Importance  ` )

Optional. The relative importance of this rubric.

### Content

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{// Union field content_type can be only one of the following:&quot;property&quot;: {object (Property)}// End of list of possible types for union field content_type.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

Union field `content_type` .

`content_type` can be only one of the following:

`property`

` object ( Property  ` )

Evaluation criteria based on a specific property.

### Property

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
  &quot;description&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`description`

`string`

Description of the property being evaluated. Example: "The model's response is grammatically correct."

### Status

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
  &quot;code&quot;: integer,
  &quot;message&quot;: string,
  &quot;details&quot;: [
    {
      &quot;@type&quot;: string,
      field1: ...,
      ...
    }
  ]
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`code`

`integer`

The status code, which should be an enum value of `google.rpc.Code` .

`message`

`string`

A developer-facing error message, which should be in English. Any user-facing error message should be localized and sent in the `google.rpc.Status.details` field, or localized by the client.

`details[]`

`object`

A list of messages that carry the error details. There is a common set of message types for APIs to use.

An object containing fields of an arbitrary type. An additional field `"@type"` contains a URI identifying the type. Example: `{ "id": 1234, "@type": "types.example.com/standard/id" }` .

### Any

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
  &quot;typeUrl&quot;: string,
  &quot;value&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`typeUrl`

`string`

Identifies the type of the serialized Protobuf message with a URI reference consisting of a prefix ending in a slash and the fully-qualified type name.

Example: type.googleapis.com/google.protobuf.StringValue

This string must contain at least one `/` character, and the content after the last `/` must be the fully-qualified name of the type in canonical form, without a leading dot. Do not write a scheme on these URI references so that clients do not attempt to contact them.

The prefix is arbitrary and Protobuf implementations are expected to simply strip off everything up to and including the last `/` to identify the type. `type.googleapis.com/` is a common default prefix that some legacy implementations require. This prefix does not indicate the origin of the type, and URIs containing it are not expected to respond to any requests.

All type URL strings must be legal URI references with the additional restriction (for the text format) that the content of the reference must consist only of alphanumeric characters, percent-encoded escapes, and characters in the following set (not including the outer backticks): `/-.~_!$&()*+,;=` . Despite our allowing percent encodings, implementations should not unescape them to prevent confusion with existing parsers. For example, `type.googleapis.com%2FFoo` should be rejected.

In the original design of `Any` , the possibility of launching a type resolution service at these type URLs was considered but Protobuf never implemented one and considers contacting these URLs to be problematic and a potential security issue. Do not attempt to contact type URLs.

`value`

`string ( bytes format)`

Holds a Protobuf serialization of the type described by type\_url.

A base64-encoded string.

### PairwiseChoice

Pairwise prediction autorater preference.

Enums

`PAIRWISE_CHOICE_UNSPECIFIED`

Unspecified prediction choice.

`BASELINE`

Baseline prediction wins

`CANDIDATE`

Candidate prediction wins

`TIE`

Winner cannot be determined

### Importance

Importance level of the rubric.

Enums

`IMPORTANCE_UNSPECIFIED`

Importance is not specified.

`HIGH`

High importance.

`MEDIUM`

Medium importance.

`LOW`

Low importance.

### Tool Annotations

Destructive Hint: ❌ | Idempotent Hint: ❌ | Read Only Hint: ❌ | Open World Hint: ❌
