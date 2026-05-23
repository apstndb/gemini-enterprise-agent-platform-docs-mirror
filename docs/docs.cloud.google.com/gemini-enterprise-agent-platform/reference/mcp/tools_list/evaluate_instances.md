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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;location&quot;: string,&quot;autoraterConfig&quot;: {object (AutoraterConfig)},// Union field metric_inputs can be only one of the following:&quot;exactMatchInput&quot;: {object (ExactMatchInput)},&quot;bleuInput&quot;: {object (BleuInput)},&quot;rougeInput&quot;: {object (RougeInput)},&quot;fluencyInput&quot;: {object (FluencyInput)},&quot;coherenceInput&quot;: {object (CoherenceInput)},&quot;safetyInput&quot;: {object (SafetyInput)},&quot;groundednessInput&quot;: {object (GroundednessInput)},&quot;fulfillmentInput&quot;: {object (FulfillmentInput)},&quot;summarizationQualityInput&quot;: {object (SummarizationQualityInput)},&quot;pairwiseSummarizationQualityInput&quot;: {object (PairwiseSummarizationQualityInput)},&quot;summarizationHelpfulnessInput&quot;: {object (SummarizationHelpfulnessInput)},&quot;summarizationVerbosityInput&quot;: {object (SummarizationVerbosityInput)},&quot;questionAnsweringQualityInput&quot;: {object (QuestionAnsweringQualityInput)},&quot;pairwiseQuestionAnsweringQualityInput&quot;: {object (PairwiseQuestionAnsweringQualityInput)},&quot;questionAnsweringRelevanceInput&quot;: {object (QuestionAnsweringRelevanceInput)},&quot;questionAnsweringHelpfulnessInput&quot;: {object (QuestionAnsweringHelpfulnessInput)},&quot;questionAnsweringCorrectnessInput&quot;: {object (QuestionAnsweringCorrectnessInput)},&quot;pointwiseMetricInput&quot;: {object (PointwiseMetricInput)},&quot;pairwiseMetricInput&quot;: {object (PairwiseMetricInput)},&quot;toolCallValidInput&quot;: {object (ToolCallValidInput)},&quot;toolNameMatchInput&quot;: {object (ToolNameMatchInput)},&quot;toolParameterKeyMatchInput&quot;: {object (ToolParameterKeyMatchInput)},&quot;toolParameterKvMatchInput&quot;: {object (ToolParameterKVMatchInput)},&quot;cometInput&quot;: {object (CometInput)},&quot;metricxInput&quot;: {object (MetricxInput)},&quot;trajectoryExactMatchInput&quot;: {object (TrajectoryExactMatchInput)},&quot;trajectoryInOrderMatchInput&quot;: {object (TrajectoryInOrderMatchInput)},&quot;trajectoryAnyOrderMatchInput&quot;: {object (TrajectoryAnyOrderMatchInput)},&quot;trajectoryPrecisionInput&quot;: {object (TrajectoryPrecisionInput)},&quot;trajectoryRecallInput&quot;: {object (TrajectoryRecallInput)},&quot;trajectorySingleToolUseInput&quot;: {object (TrajectorySingleToolUseInput)},&quot;rubricBasedInstructionFollowingInput&quot;: {object (RubricBasedInstructionFollowingInput)}// End of list of possible types for union field metric_inputs.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`location`

`string`

Required. The resource name of the Location to evaluate the instances. Format: `projects/{project}/locations/{location}`

`autoraterConfig`

` object ( AutoraterConfig  ` )

Optional. Autorater config used for evaluation.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;thought&quot;: boolean,&quot;thoughtSignature&quot;: string,&quot;mediaResolution&quot;: {object (MediaResolution)},// Union field data can be only one of the following:&quot;text&quot;: string,&quot;inlineData&quot;: {object (Blob)},&quot;fileData&quot;: {object (FileData)},&quot;functionCall&quot;: {object (FunctionCall)},&quot;functionResponse&quot;: {object (FunctionResponse)},&quot;executableCode&quot;: {object (ExecutableCode)},&quot;codeExecutionResult&quot;: {object (CodeExecutionResult)}// End of list of possible types for union field data.// Union field metadata can be only one of the following:&quot;videoMetadata&quot;: {object (VideoMetadata)}// End of list of possible types for union field metadata.}</code></pre></td>
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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;language&quot;: enum (Language),&quot;code&quot;: string}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`language`

`enum ( Language` )

Required. Programming language of the `code` .

`code`

`string`

Required. The code to be executed.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;outcome&quot;: enum (Outcome),&quot;output&quot;: string}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`outcome`

`enum ( Outcome` )

Required. Outcome of the code execution.

`output`

`string`

Optional. Contains stdout when code execution is successful, stderr or other description otherwise.

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

`enum ( Level` )

The tokenization quality used for given media.

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

`enum ( CometVersion` )

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

`enum ( MetricxVersion` )

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;stopSequences&quot;: [string],&quot;responseMimeType&quot;: string,&quot;responseModalities&quot;: [enum (Modality)],&quot;thinkingConfig&quot;: {object (ThinkingConfig)},&quot;modelConfig&quot;: {object (ModelConfig)},// Union field _temperature can be only one of the following:&quot;temperature&quot;: number// End of list of possible types for union field _temperature.// Union field _top_p can be only one of the following:&quot;topP&quot;: number// End of list of possible types for union field _top_p.// Union field _top_k can be only one of the following:&quot;topK&quot;: number// End of list of possible types for union field _top_k.// Union field _candidate_count can be only one of the following:&quot;candidateCount&quot;: integer// End of list of possible types for union field _candidate_count.// Union field _max_output_tokens can be only one of the following:&quot;maxOutputTokens&quot;: integer// End of list of possible types for union field _max_output_tokens.// Union field _response_logprobs can be only one of the following:&quot;responseLogprobs&quot;: boolean// End of list of possible types for union field _response_logprobs.// Union field _logprobs can be only one of the following:&quot;logprobs&quot;: integer// End of list of possible types for union field _logprobs.// Union field _presence_penalty can be only one of the following:&quot;presencePenalty&quot;: number// End of list of possible types for union field _presence_penalty.// Union field _frequency_penalty can be only one of the following:&quot;frequencyPenalty&quot;: number// End of list of possible types for union field _frequency_penalty.// Union field _seed can be only one of the following:&quot;seed&quot;: integer// End of list of possible types for union field _seed.// Union field _response_schema can be only one of the following:&quot;responseSchema&quot;: {object (Schema)}// End of list of possible types for union field _response_schema.// Union field _response_json_schema can be only one of the following:&quot;responseJsonSchema&quot;: value// End of list of possible types for union field _response_json_schema.// Union field _routing_config can be only one of the following:&quot;routingConfig&quot;: {object (RoutingConfig)}// End of list of possible types for union field _routing_config.// Union field _audio_timestamp can be only one of the following:&quot;audioTimestamp&quot;: boolean// End of list of possible types for union field _audio_timestamp.// Union field _media_resolution can be only one of the following:&quot;mediaResolution&quot;: enum (MediaResolution)// End of list of possible types for union field _media_resolution.// Union field _speech_config can be only one of the following:&quot;speechConfig&quot;: {object (SpeechConfig)}// End of list of possible types for union field _speech_config.// Union field _enable_affective_dialog can be only one of the following:&quot;enableAffectiveDialog&quot;: boolean// End of list of possible types for union field _enable_affective_dialog.// Union field _image_config can be only one of the following:&quot;imageConfig&quot;: {object (ImageConfig)}// End of list of possible types for union field _image_config.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`stopSequences[]`

`string`

Optional. A list of character sequences that will stop the model from generating further tokens. If a stop sequence is generated, the output will end at that point. This is useful for controlling the length and structure of the output. For example, you can use \["\\n", "\#\#\#"\] to stop generation at a new line or a specific marker.

`responseMimeType`

`string`

Optional. The IANA standard MIME type of the response. The model will generate output that conforms to this MIME type. Supported values include 'text/plain' (default) and 'application/json'. The model needs to be prompted to output the appropriate response type, otherwise the behavior is undefined.

`responseModalities[]`

`enum ( Modality` )

Optional. The modalities of the response. The model will generate a response that includes all the specified modalities. For example, if this is set to `[TEXT, IMAGE]` , the response will include both text and an image.

`thinkingConfig`

` object ( ThinkingConfig  ` )

Optional. Configuration for thinking features. An error will be returned if this field is set for models that don't support thinking.

` modelConfig (deprecated)  `

` object ( ModelConfig  ` )

> Optional. The `model_config` field is deprecated and is not supported anymore. Use `routing_config` instead.

Optional. Config for model selection.

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

`responseSchema`

` object ( Schema  ` )

Optional. Lets you to specify a schema for the model's response, ensuring that the output conforms to a particular structure. This is useful for generating structured data such as JSON. The schema is a subset of the [OpenAPI 3.0 schema object](https://spec.openapis.org/oas/v3.0.3#schema) object.

When this field is set, you must also set the `response_mime_type` to `application/json` .

Union field `_response_json_schema` .

`_response_json_schema` can be only one of the following:

`responseJsonSchema`

` value ( Value  ` format)

Optional. When this field is set, `response_schema` must be omitted and `response_mime_type` must be set to `application/json` .

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

`enum ( MediaResolution` )

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

`imageConfig`

` object ( ImageConfig  ` )

Optional. Config for image generation features.

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

`enum ( Type` )

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

`enum ( ModelRoutingPreference` )

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

`enum ( ThinkingLevel` )

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

`enum ( FeatureSelectionPreference` )

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

`enum ( PersonGeneration` )

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

`enum ( PairwiseChoice` )

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

`enum ( PairwiseChoice` )

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

`enum ( PairwiseChoice` )

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{// Union field _score can be only one of the following:&quot;score&quot;: number// End of list of possible types for union field _score.// Union field _explanation can be only one of the following:&quot;explanation&quot;: string// End of list of possible types for union field _explanation.// Union field _error can be only one of the following:&quot;error&quot;: {object (Status)}// End of list of possible types for union field _error.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

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

### Tool Annotations

Destructive Hint: ❌ | Idempotent Hint: ❌ | Read Only Hint: ❌ | Open World Hint: ❌
