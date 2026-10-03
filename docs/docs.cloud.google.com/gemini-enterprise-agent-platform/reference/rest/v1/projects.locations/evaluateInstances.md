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

`autoraterConfig` `object ( `[`AutoraterConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.tuningJobs#AutoraterConfig)` )`

Optional. Autorater config used for evaluation. Not applicable for predefined metrics (PredefinedMetricSpec); the server uses its own model configuration for predefined metrics and this field is ignored.

`metric_inputs` `Union type`

Instances and specs for evaluation The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:

`exactMatchInput` `object ( `[`ExactMatchInput`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations/evaluateInstances#ExactMatchInput)` )`

Auto metric instances. Instances and metric spec for exact match metric.

`bleuInput` `object ( `[`BleuInput`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations/evaluateInstances#BleuInput)` )`

Instances and metric spec for bleu metric.

`rougeInput` `object ( `[`RougeInput`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations/evaluateInstances#RougeInput)` )`

Instances and metric spec for rouge metric.

`fluencyInput` `object ( `[`FluencyInput`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations/evaluateInstances#FluencyInput)` )`

LLM-based metric instance. General text generation metrics, applicable to other categories. Input for fluency metric.

`coherenceInput` `object ( `[`CoherenceInput`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations/evaluateInstances#CoherenceInput)` )`

Input for coherence metric.

`safetyInput` `object ( `[`SafetyInput`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations/evaluateInstances#SafetyInput)` )`

Input for safety metric.

`groundednessInput` `object ( `[`GroundednessInput`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations/evaluateInstances#GroundednessInput)` )`

Input for groundedness metric.

`fulfillmentInput` `object ( `[`FulfillmentInput`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations/evaluateInstances#FulfillmentInput)` )`

Input for fulfillment metric.

`summarizationQualityInput` `object ( `[`SummarizationQualityInput`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations/evaluateInstances#SummarizationQualityInput)` )`

Input for summarization quality metric.

`pairwiseSummarizationQualityInput` `object ( `[`PairwiseSummarizationQualityInput`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations/evaluateInstances#PairwiseSummarizationQualityInput)` )`

Input for pairwise summarization quality metric.

`summarizationHelpfulnessInput` `object ( `[`SummarizationHelpfulnessInput`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations/evaluateInstances#SummarizationHelpfulnessInput)` )`

Input for summarization helpfulness metric.

`summarizationVerbosityInput` `object ( `[`SummarizationVerbosityInput`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations/evaluateInstances#SummarizationVerbosityInput)` )`

Input for summarization verbosity metric.

`questionAnsweringQualityInput` `object ( `[`QuestionAnsweringQualityInput`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations/evaluateInstances#QuestionAnsweringQualityInput)` )`

Input for question answering quality metric.

`pairwiseQuestionAnsweringQualityInput` `object ( `[`PairwiseQuestionAnsweringQualityInput`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations/evaluateInstances#PairwiseQuestionAnsweringQualityInput)` )`

Input for pairwise question answering quality metric.

`questionAnsweringRelevanceInput` `object ( `[`QuestionAnsweringRelevanceInput`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations/evaluateInstances#QuestionAnsweringRelevanceInput)` )`

Input for question answering relevance metric.

`questionAnsweringHelpfulnessInput` `object ( `[`QuestionAnsweringHelpfulnessInput`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations/evaluateInstances#QuestionAnsweringHelpfulnessInput)` )`

Input for question answering helpfulness metric.

`questionAnsweringCorrectnessInput` `object ( `[`QuestionAnsweringCorrectnessInput`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations/evaluateInstances#QuestionAnsweringCorrectnessInput)` )`

Input for question answering correctness metric.

`pointwiseMetricInput` `object ( `[`PointwiseMetricInput`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations/evaluateInstances#PointwiseMetricInput)` )`

Input for pointwise metric.

`pairwiseMetricInput` `object ( `[`PairwiseMetricInput`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations/evaluateInstances#PairwiseMetricInput)` )`

Input for pairwise metric.

`toolCallValidInput` `object ( `[`ToolCallValidInput`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations/evaluateInstances#ToolCallValidInput)` )`

Tool call metric instances. Input for tool call valid metric.

`toolNameMatchInput` `object ( `[`ToolNameMatchInput`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations/evaluateInstances#ToolNameMatchInput)` )`

Input for tool name match metric.

`toolParameterKeyMatchInput` `object ( `[`ToolParameterKeyMatchInput`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations/evaluateInstances#ToolParameterKeyMatchInput)` )`

Input for tool parameter key match metric.

`toolParameterKvMatchInput` `object ( `[`ToolParameterKVMatchInput`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations/evaluateInstances#ToolParameterKVMatchInput)` )`

Input for tool parameter key value match metric.

`cometInput` `object ( `[`CometInput`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations/evaluateInstances#CometInput)` )`

Translation metrics. Input for Comet metric.

`metricxInput` `object ( `[`MetricxInput`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations/evaluateInstances#MetricxInput)` )`

Input for Metricx metric.

`trajectoryExactMatchInput` `object ( `[`TrajectoryExactMatchInput`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations/evaluateInstances#TrajectoryExactMatchInput)` )`

Input for trajectory exact match metric.

`trajectoryInOrderMatchInput` `object ( `[`TrajectoryInOrderMatchInput`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations/evaluateInstances#TrajectoryInOrderMatchInput)` )`

Input for trajectory in order match metric.

`trajectoryAnyOrderMatchInput` `object ( `[`TrajectoryAnyOrderMatchInput`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations/evaluateInstances#TrajectoryAnyOrderMatchInput)` )`

Input for trajectory match any order metric.

`trajectoryPrecisionInput` `object ( `[`TrajectoryPrecisionInput`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations/evaluateInstances#TrajectoryPrecisionInput)` )`

Input for trajectory precision metric.

`trajectoryRecallInput` `object ( `[`TrajectoryRecallInput`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations/evaluateInstances#TrajectoryRecallInput)` )`

Input for trajectory recall metric.

`trajectorySingleToolUseInput` `object ( `[`TrajectorySingleToolUseInput`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations/evaluateInstances#TrajectorySingleToolUseInput)` )`

Input for trajectory single tool use metric.

End of mutually exclusive fields.

### Response body

Response message for EvaluationService.EvaluateInstances.

If successful, the response body contains data with the following structure:

Fields

`metricResults[]` `object ( `[`MetricResult`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations/evaluateInstances#MetricResult)` )`

Metric results for each instance. The order of the metric results is guaranteed to be the same as the order of the instances in the request.

`evaluation_results` `Union type`

Evaluation results will be served in the same order as presented in EvaluationRequest.instances. The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:

`exactMatchResults` `object ( `[`ExactMatchResults`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations/evaluateInstances#ExactMatchResults)` )`

Auto metric evaluation results. Results for exact match metric.

`bleuResults` `object ( `[`BleuResults`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations/evaluateInstances#BleuResults)` )`

Results for bleu metric.

`rougeResults` `object ( `[`RougeResults`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations/evaluateInstances#RougeResults)` )`

Results for rouge metric.

`fluencyResult` `object ( `[`FluencyResult`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations/evaluateInstances#FluencyResult)` )`

LLM-based metric evaluation result. General text generation metrics, applicable to other categories. result for fluency metric.

`coherenceResult` `object ( `[`CoherenceResult`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations/evaluateInstances#CoherenceResult)` )`

result for coherence metric.

`safetyResult` `object ( `[`SafetyResult`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations/evaluateInstances#SafetyResult)` )`

result for safety metric.

`groundednessResult` `object ( `[`GroundednessResult`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations/evaluateInstances#GroundednessResult)` )`

result for groundedness metric.

`fulfillmentResult` `object ( `[`FulfillmentResult`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations/evaluateInstances#FulfillmentResult)` )`

result for fulfillment metric.

`summarizationQualityResult` `object ( `[`SummarizationQualityResult`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations/evaluateInstances#SummarizationQualityResult)` )`

Summarization only metrics. result for summarization quality metric.

`pairwiseSummarizationQualityResult` `object ( `[`PairwiseSummarizationQualityResult`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations/evaluateInstances#PairwiseSummarizationQualityResult)` )`

result for pairwise summarization quality metric.

`summarizationHelpfulnessResult` `object ( `[`SummarizationHelpfulnessResult`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations/evaluateInstances#SummarizationHelpfulnessResult)` )`

result for summarization helpfulness metric.

`summarizationVerbosityResult` `object ( `[`SummarizationVerbosityResult`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations/evaluateInstances#SummarizationVerbosityResult)` )`

result for summarization verbosity metric.

`questionAnsweringQualityResult` `object ( `[`QuestionAnsweringQualityResult`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations/evaluateInstances#QuestionAnsweringQualityResult)` )`

Question answering only metrics. result for question answering quality metric.

`pairwiseQuestionAnsweringQualityResult` `object ( `[`PairwiseQuestionAnsweringQualityResult`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations/evaluateInstances#PairwiseQuestionAnsweringQualityResult)` )`

result for pairwise question answering quality metric.

`questionAnsweringRelevanceResult` `object ( `[`QuestionAnsweringRelevanceResult`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations/evaluateInstances#QuestionAnsweringRelevanceResult)` )`

result for question answering relevance metric.

`questionAnsweringHelpfulnessResult` `object ( `[`QuestionAnsweringHelpfulnessResult`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations/evaluateInstances#QuestionAnsweringHelpfulnessResult)` )`

result for question answering helpfulness metric.

`questionAnsweringCorrectnessResult` `object ( `[`QuestionAnsweringCorrectnessResult`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations/evaluateInstances#QuestionAnsweringCorrectnessResult)` )`

result for question answering correctness metric.

`pointwiseMetricResult` `object ( `[`PointwiseMetricResult`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.tuningJobs#PointwiseMetricResult)` )`

Generic metrics. result for pointwise metric.

`pairwiseMetricResult` `object ( `[`PairwiseMetricResult`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.tuningJobs#PairwiseMetricResult)` )`

result for pairwise metric.

`toolCallValidResults` `object ( `[`ToolCallValidResults`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations/evaluateInstances#ToolCallValidResults)` )`

Tool call metrics. Results for tool call valid metric.

`toolNameMatchResults` `object ( `[`ToolNameMatchResults`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations/evaluateInstances#ToolNameMatchResults)` )`

Results for tool name match metric.

`toolParameterKeyMatchResults` `object ( `[`ToolParameterKeyMatchResults`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations/evaluateInstances#ToolParameterKeyMatchResults)` )`

Results for tool parameter key match metric.

`toolParameterKvMatchResults` `object ( `[`ToolParameterKVMatchResults`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations/evaluateInstances#ToolParameterKVMatchResults)` )`

Results for tool parameter key value match metric.

`cometResult` `object ( `[`CometResult`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations/evaluateInstances#CometResult)` )`

Translation metrics. result for Comet metric.

`metricxResult` `object ( `[`MetricxResult`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations/evaluateInstances#MetricxResult)` )`

result for Metricx metric.

`trajectoryExactMatchResults` `object ( `[`TrajectoryExactMatchResults`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations/evaluateInstances#TrajectoryExactMatchResults)` )`

result for trajectory exact match metric.

`trajectoryInOrderMatchResults` `object ( `[`TrajectoryInOrderMatchResults`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations/evaluateInstances#TrajectoryInOrderMatchResults)` )`

result for trajectory in order match metric.

`trajectoryAnyOrderMatchResults` `object ( `[`TrajectoryAnyOrderMatchResults`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations/evaluateInstances#TrajectoryAnyOrderMatchResults)` )`

result for trajectory any order match metric.

`trajectoryPrecisionResults` `object ( `[`TrajectoryPrecisionResults`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations/evaluateInstances#TrajectoryPrecisionResults)` )`

result for trajectory precision metric.

`trajectoryRecallResults` `object ( `[`TrajectoryRecallResults`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations/evaluateInstances#TrajectoryRecallResults)` )`

Results for trajectory recall metric.

`trajectorySingleToolUseResults` `object ( `[`TrajectorySingleToolUseResults`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations/evaluateInstances#TrajectorySingleToolUseResults)` )`

Results for trajectory single tool use metric.

End of mutually exclusive fields.

**JSON representation**

```
{
  "metricResults": [
    {
      object (MetricResult)
    }
  ],

  // evaluation_results
  "exactMatchResults": {
    object (ExactMatchResults)
  },
  "bleuResults": {
    object (BleuResults)
  },
  "rougeResults": {
    object (RougeResults)
  },
  "fluencyResult": {
    object (FluencyResult)
  },
  "coherenceResult": {
    object (CoherenceResult)
  },
  "safetyResult": {
    object (SafetyResult)
  },
  "groundednessResult": {
    object (GroundednessResult)
  },
  "fulfillmentResult": {
    object (FulfillmentResult)
  },
  "summarizationQualityResult": {
    object (SummarizationQualityResult)
  },
  "pairwiseSummarizationQualityResult": {
    object (PairwiseSummarizationQualityResult)
  },
  "summarizationHelpfulnessResult": {
    object (SummarizationHelpfulnessResult)
  },
  "summarizationVerbosityResult": {
    object (SummarizationVerbosityResult)
  },
  "questionAnsweringQualityResult": {
    object (QuestionAnsweringQualityResult)
  },
  "pairwiseQuestionAnsweringQualityResult": {
    object (PairwiseQuestionAnsweringQualityResult)
  },
  "questionAnsweringRelevanceResult": {
    object (QuestionAnsweringRelevanceResult)
  },
  "questionAnsweringHelpfulnessResult": {
    object (QuestionAnsweringHelpfulnessResult)
  },
  "questionAnsweringCorrectnessResult": {
    object (QuestionAnsweringCorrectnessResult)
  },
  "pointwiseMetricResult": {
    object (PointwiseMetricResult)
  },
  "pairwiseMetricResult": {
    object (PairwiseMetricResult)
  },
  "toolCallValidResults": {
    object (ToolCallValidResults)
  },
  "toolNameMatchResults": {
    object (ToolNameMatchResults)
  },
  "toolParameterKeyMatchResults": {
    object (ToolParameterKeyMatchResults)
  },
  "toolParameterKvMatchResults": {
    object (ToolParameterKVMatchResults)
  },
  "cometResult": {
    object (CometResult)
  },
  "metricxResult": {
    object (MetricxResult)
  },
  "trajectoryExactMatchResults": {
    object (TrajectoryExactMatchResults)
  },
  "trajectoryInOrderMatchResults": {
    object (TrajectoryInOrderMatchResults)
  },
  "trajectoryAnyOrderMatchResults": {
    object (TrajectoryAnyOrderMatchResults)
  },
  "trajectoryPrecisionResults": {
    object (TrajectoryPrecisionResults)
  },
  "trajectoryRecallResults": {
    object (TrajectoryRecallResults)
  },
  "trajectorySingleToolUseResults": {
    object (TrajectorySingleToolUseResults)
  }
  // Union type
}
```

## ExactMatchInput

Input for exact match metric.

Fields

`metricSpec` `object ( `[`ExactMatchSpec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.tuningJobs#ExactMatchSpec)` )`

Required. Spec for exact match metric.

`instances[]` `object ( `[`ExactMatchInstance`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations/evaluateInstances#ExactMatchInstance)` )`

Required. Repeated exact match instances.

**JSON representation**

```
{
  "metricSpec": {
    object (ExactMatchSpec)
  },
  "instances": [
    {
      object (ExactMatchInstance)
    }
  ]
}
```

## ExactMatchInstance

Spec for exact match instance.

Fields

`prediction` `string`

Required. Output of the evaluated model.

`reference` `string`

Required. Ground truth used to compare against the prediction.

**JSON representation**

```
{
  "prediction": string,
  "reference": string
}
```

## BleuInput

Input for bleu metric.

Fields

`metricSpec` `object ( `[`BleuSpec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.tuningJobs#BleuSpec)` )`

Required. Spec for bleu score metric.

`instances[]` `object ( `[`BleuInstance`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations/evaluateInstances#BleuInstance)` )`

Required. Repeated bleu instances.

**JSON representation**

```
{
  "metricSpec": {
    object (BleuSpec)
  },
  "instances": [
    {
      object (BleuInstance)
    }
  ]
}
```

## BleuInstance

Spec for bleu instance.

Fields

`prediction` `string`

Required. Output of the evaluated model.

`reference` `string`

Required. Ground truth used to compare against the prediction.

**JSON representation**

```
{
  "prediction": string,
  "reference": string
}
```

## RougeInput

Input for rouge metric.

Fields

`metricSpec` `object ( `[`RougeSpec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.tuningJobs#RougeSpec)` )`

Required. Spec for rouge score metric.

`instances[]` `object ( `[`RougeInstance`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations/evaluateInstances#RougeInstance)` )`

Required. Repeated rouge instances.

**JSON representation**

```
{
  "metricSpec": {
    object (RougeSpec)
  },
  "instances": [
    {
      object (RougeInstance)
    }
  ]
}
```

## RougeInstance

Spec for rouge instance.

Fields

`prediction` `string`

Required. Output of the evaluated model.

`reference` `string`

Required. Ground truth used to compare against the prediction.

**JSON representation**

```
{
  "prediction": string,
  "reference": string
}
```

## FluencyInput

Input for fluency metric.

Fields

`metricSpec` `object ( `[`FluencySpec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations/evaluateInstances#FluencySpec)` )`

Required. Spec for fluency score metric.

`instance` `object ( `[`FluencyInstance`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations/evaluateInstances#FluencyInstance)` )`

Required. Fluency instance.

**JSON representation**

```
{
  "metricSpec": {
    object (FluencySpec)
  },
  "instance": {
    object (FluencyInstance)
  }
}
```

## FluencySpec

Spec for fluency score metric.

Fields

`version` `integer`

Optional. Which version to use for evaluation.

**JSON representation**

```
{
  "version": integer
}
```

## FluencyInstance

Spec for fluency instance.

Fields

`prediction` `string`

Required. Output of the evaluated model.

**JSON representation**

```
{
  "prediction": string
}
```

## CoherenceInput

Input for coherence metric.

Fields

`metricSpec` `object ( `[`CoherenceSpec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations/evaluateInstances#CoherenceSpec)` )`

Required. Spec for coherence score metric.

`instance` `object ( `[`CoherenceInstance`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations/evaluateInstances#CoherenceInstance)` )`

Required. Coherence instance.

**JSON representation**

```
{
  "metricSpec": {
    object (CoherenceSpec)
  },
  "instance": {
    object (CoherenceInstance)
  }
}
```

## CoherenceSpec

Spec for coherence score metric.

Fields

`version` `integer`

Optional. Which version to use for evaluation.

**JSON representation**

```
{
  "version": integer
}
```

## CoherenceInstance

Spec for coherence instance.

Fields

`prediction` `string`

Required. Output of the evaluated model.

**JSON representation**

```
{
  "prediction": string
}
```

## SafetyInput

Input for safety metric.

Fields

`metricSpec` `object ( `[`SafetySpec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations/evaluateInstances#SafetySpec)` )`

Required. Spec for safety metric.

`instance` `object ( `[`SafetyInstance`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations/evaluateInstances#SafetyInstance)` )`

Required. Safety instance.

**JSON representation**

```
{
  "metricSpec": {
    object (SafetySpec)
  },
  "instance": {
    object (SafetyInstance)
  }
}
```

## SafetySpec

Spec for safety metric.

Fields

`version` `integer`

Optional. Which version to use for evaluation.

**JSON representation**

```
{
  "version": integer
}
```

## SafetyInstance

Spec for safety instance.

Fields

`prediction` `string`

Required. Output of the evaluated model.

**JSON representation**

```
{
  "prediction": string
}
```

## GroundednessInput

Input for groundedness metric.

Fields

`metricSpec` `object ( `[`GroundednessSpec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations/evaluateInstances#GroundednessSpec)` )`

Required. Spec for groundedness metric.

`instance` `object ( `[`GroundednessInstance`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations/evaluateInstances#GroundednessInstance)` )`

Required. Groundedness instance.

**JSON representation**

```
{
  "metricSpec": {
    object (GroundednessSpec)
  },
  "instance": {
    object (GroundednessInstance)
  }
}
```

## GroundednessSpec

Spec for groundedness metric.

Fields

`version` `integer`

Optional. Which version to use for evaluation.

**JSON representation**

```
{
  "version": integer
}
```

## GroundednessInstance

Spec for groundedness instance.

Fields

`prediction` `string`

Required. Output of the evaluated model.

`context` `string`

Required. Background information provided in context used to compare against the prediction.

**JSON representation**

```
{
  "prediction": string,
  "context": string
}
```

## FulfillmentInput

Input for fulfillment metric.

Fields

`metricSpec` `object ( `[`FulfillmentSpec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations/evaluateInstances#FulfillmentSpec)` )`

Required. Spec for fulfillment score metric.

`instance` `object ( `[`FulfillmentInstance`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations/evaluateInstances#FulfillmentInstance)` )`

Required. Fulfillment instance.

**JSON representation**

```
{
  "metricSpec": {
    object (FulfillmentSpec)
  },
  "instance": {
    object (FulfillmentInstance)
  }
}
```

## FulfillmentSpec

Spec for fulfillment metric.

Fields

`version` `integer`

Optional. Which version to use for evaluation.

**JSON representation**

```
{
  "version": integer
}
```

## FulfillmentInstance

Spec for fulfillment instance.

Fields

`prediction` `string`

Required. Output of the evaluated model.

`instruction` `string`

Required. Inference instruction prompt to compare prediction with.

**JSON representation**

```
{
  "prediction": string,
  "instruction": string
}
```

## SummarizationQualityInput

Input for summarization quality metric.

Fields

`metricSpec` `object ( `[`SummarizationQualitySpec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations/evaluateInstances#SummarizationQualitySpec)` )`

Required. Spec for summarization quality score metric.

`instance` `object ( `[`SummarizationQualityInstance`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations/evaluateInstances#SummarizationQualityInstance)` )`

Required. Summarization quality instance.

**JSON representation**

```
{
  "metricSpec": {
    object (SummarizationQualitySpec)
  },
  "instance": {
    object (SummarizationQualityInstance)
  }
}
```

## SummarizationQualitySpec

Spec for summarization quality score metric.

Fields

`useReference` `boolean`

Optional. Whether to use instance.reference to compute summarization quality.

`version` `integer`

Optional. Which version to use for evaluation.

**JSON representation**

```
{
  "useReference": boolean,
  "version": integer
}
```

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

**JSON representation**

```
{
  "prediction": string,
  "reference": string,
  "context": string,
  "instruction": string
}
```

## PairwiseSummarizationQualityInput

Input for pairwise summarization quality metric.

Fields

`metricSpec` `object ( `[`PairwiseSummarizationQualitySpec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations/evaluateInstances#PairwiseSummarizationQualitySpec)` )`

Required. Spec for pairwise summarization quality score metric.

`instance` `object ( `[`PairwiseSummarizationQualityInstance`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations/evaluateInstances#PairwiseSummarizationQualityInstance)` )`

Required. Pairwise summarization quality instance.

**JSON representation**

```
{
  "metricSpec": {
    object (PairwiseSummarizationQualitySpec)
  },
  "instance": {
    object (PairwiseSummarizationQualityInstance)
  }
}
```

## PairwiseSummarizationQualitySpec

Spec for pairwise summarization quality score metric.

Fields

`useReference` `boolean`

Optional. Whether to use instance.reference to compute pairwise summarization quality.

`version` `integer`

Optional. Which version to use for evaluation.

**JSON representation**

```
{
  "useReference": boolean,
  "version": integer
}
```

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

**JSON representation**

```
{
  "prediction": string,
  "baselinePrediction": string,
  "reference": string,
  "context": string,
  "instruction": string
}
```

## SummarizationHelpfulnessInput

Input for summarization helpfulness metric.

Fields

`metricSpec` `object ( `[`SummarizationHelpfulnessSpec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations/evaluateInstances#SummarizationHelpfulnessSpec)` )`

Required. Spec for summarization helpfulness score metric.

`instance` `object ( `[`SummarizationHelpfulnessInstance`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations/evaluateInstances#SummarizationHelpfulnessInstance)` )`

Required. Summarization helpfulness instance.

**JSON representation**

```
{
  "metricSpec": {
    object (SummarizationHelpfulnessSpec)
  },
  "instance": {
    object (SummarizationHelpfulnessInstance)
  }
}
```

## SummarizationHelpfulnessSpec

Spec for summarization helpfulness score metric.

Fields

`useReference` `boolean`

Optional. Whether to use instance.reference to compute summarization helpfulness.

`version` `integer`

Optional. Which version to use for evaluation.

**JSON representation**

```
{
  "useReference": boolean,
  "version": integer
}
```

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

**JSON representation**

```
{
  "prediction": string,
  "reference": string,
  "context": string,
  "instruction": string
}
```

## SummarizationVerbosityInput

Input for summarization verbosity metric.

Fields

`metricSpec` `object ( `[`SummarizationVerbositySpec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations/evaluateInstances#SummarizationVerbositySpec)` )`

Required. Spec for summarization verbosity score metric.

`instance` `object ( `[`SummarizationVerbosityInstance`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations/evaluateInstances#SummarizationVerbosityInstance)` )`

Required. Summarization verbosity instance.

**JSON representation**

```
{
  "metricSpec": {
    object (SummarizationVerbositySpec)
  },
  "instance": {
    object (SummarizationVerbosityInstance)
  }
}
```

## SummarizationVerbositySpec

Spec for summarization verbosity score metric.

Fields

`useReference` `boolean`

Optional. Whether to use instance.reference to compute summarization verbosity.

`version` `integer`

Optional. Which version to use for evaluation.

**JSON representation**

```
{
  "useReference": boolean,
  "version": integer
}
```

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

**JSON representation**

```
{
  "prediction": string,
  "reference": string,
  "context": string,
  "instruction": string
}
```

## QuestionAnsweringQualityInput

Input for question answering quality metric.

Fields

`metricSpec` `object ( `[`QuestionAnsweringQualitySpec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations/evaluateInstances#QuestionAnsweringQualitySpec)` )`

Required. Spec for question answering quality score metric.

`instance` `object ( `[`QuestionAnsweringQualityInstance`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations/evaluateInstances#QuestionAnsweringQualityInstance)` )`

Required. Question answering quality instance.

**JSON representation**

```
{
  "metricSpec": {
    object (QuestionAnsweringQualitySpec)
  },
  "instance": {
    object (QuestionAnsweringQualityInstance)
  }
}
```

## QuestionAnsweringQualitySpec

Spec for question answering quality score metric.

Fields

`useReference` `boolean`

Optional. Whether to use instance.reference to compute question answering quality.

`version` `integer`

Optional. Which version to use for evaluation.

**JSON representation**

```
{
  "useReference": boolean,
  "version": integer
}
```

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

**JSON representation**

```
{
  "prediction": string,
  "reference": string,
  "context": string,
  "instruction": string
}
```

## PairwiseQuestionAnsweringQualityInput

Input for pairwise question answering quality metric.

Fields

`metricSpec` `object ( `[`PairwiseQuestionAnsweringQualitySpec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations/evaluateInstances#PairwiseQuestionAnsweringQualitySpec)` )`

Required. Spec for pairwise question answering quality score metric.

`instance` `object ( `[`PairwiseQuestionAnsweringQualityInstance`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations/evaluateInstances#PairwiseQuestionAnsweringQualityInstance)` )`

Required. Pairwise question answering quality instance.

**JSON representation**

```
{
  "metricSpec": {
    object (PairwiseQuestionAnsweringQualitySpec)
  },
  "instance": {
    object (PairwiseQuestionAnsweringQualityInstance)
  }
}
```

## PairwiseQuestionAnsweringQualitySpec

Spec for pairwise question answering quality score metric.

Fields

`useReference` `boolean`

Optional. Whether to use instance.reference to compute question answering quality.

`version` `integer`

Optional. Which version to use for evaluation.

**JSON representation**

```
{
  "useReference": boolean,
  "version": integer
}
```

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

**JSON representation**

```
{
  "prediction": string,
  "baselinePrediction": string,
  "reference": string,
  "context": string,
  "instruction": string
}
```

## QuestionAnsweringRelevanceInput

Input for question answering relevance metric.

Fields

`metricSpec` `object ( `[`QuestionAnsweringRelevanceSpec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations/evaluateInstances#QuestionAnsweringRelevanceSpec)` )`

Required. Spec for question answering relevance score metric.

`instance` `object ( `[`QuestionAnsweringRelevanceInstance`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations/evaluateInstances#QuestionAnsweringRelevanceInstance)` )`

Required. Question answering relevance instance.

**JSON representation**

```
{
  "metricSpec": {
    object (QuestionAnsweringRelevanceSpec)
  },
  "instance": {
    object (QuestionAnsweringRelevanceInstance)
  }
}
```

## QuestionAnsweringRelevanceSpec

Spec for question answering relevance metric.

Fields

`useReference` `boolean`

Optional. Whether to use instance.reference to compute question answering relevance.

`version` `integer`

Optional. Which version to use for evaluation.

**JSON representation**

```
{
  "useReference": boolean,
  "version": integer
}
```

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

**JSON representation**

```
{
  "prediction": string,
  "reference": string,
  "context": string,
  "instruction": string
}
```

## QuestionAnsweringHelpfulnessInput

Input for question answering helpfulness metric.

Fields

`metricSpec` `object ( `[`QuestionAnsweringHelpfulnessSpec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations/evaluateInstances#QuestionAnsweringHelpfulnessSpec)` )`

Required. Spec for question answering helpfulness score metric.

`instance` `object ( `[`QuestionAnsweringHelpfulnessInstance`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations/evaluateInstances#QuestionAnsweringHelpfulnessInstance)` )`

Required. Question answering helpfulness instance.

**JSON representation**

```
{
  "metricSpec": {
    object (QuestionAnsweringHelpfulnessSpec)
  },
  "instance": {
    object (QuestionAnsweringHelpfulnessInstance)
  }
}
```

## QuestionAnsweringHelpfulnessSpec

Spec for question answering helpfulness metric.

Fields

`useReference` `boolean`

Optional. Whether to use instance.reference to compute question answering helpfulness.

`version` `integer`

Optional. Which version to use for evaluation.

**JSON representation**

```
{
  "useReference": boolean,
  "version": integer
}
```

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

**JSON representation**

```
{
  "prediction": string,
  "reference": string,
  "context": string,
  "instruction": string
}
```

## QuestionAnsweringCorrectnessInput

Input for question answering correctness metric.

Fields

`metricSpec` `object ( `[`QuestionAnsweringCorrectnessSpec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations/evaluateInstances#QuestionAnsweringCorrectnessSpec)` )`

Required. Spec for question answering correctness score metric.

`instance` `object ( `[`QuestionAnsweringCorrectnessInstance`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations/evaluateInstances#QuestionAnsweringCorrectnessInstance)` )`

Required. Question answering correctness instance.

**JSON representation**

```
{
  "metricSpec": {
    object (QuestionAnsweringCorrectnessSpec)
  },
  "instance": {
    object (QuestionAnsweringCorrectnessInstance)
  }
}
```

## QuestionAnsweringCorrectnessSpec

Spec for question answering correctness metric.

Fields

`useReference` `boolean`

Optional. Whether to use instance.reference to compute question answering correctness.

`version` `integer`

Optional. Which version to use for evaluation.

**JSON representation**

```
{
  "useReference": boolean,
  "version": integer
}
```

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

**JSON representation**

```
{
  "prediction": string,
  "reference": string,
  "context": string,
  "instruction": string
}
```

## PointwiseMetricInput

Input for pointwise metric.

Fields

`metricSpec` `object ( `[`PointwiseMetricSpec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.tuningJobs#PointwiseMetricSpec)` )`

Required. Spec for pointwise metric.

`instance` `object ( `[`PointwiseMetricInstance`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations/evaluateInstances#PointwiseMetricInstance)` )`

Required. Pointwise metric instance.

**JSON representation**

```
{
  "metricSpec": {
    object (PointwiseMetricSpec)
  },
  "instance": {
    object (PointwiseMetricInstance)
  }
}
```

## PointwiseMetricInstance

Pointwise metric instance. Usually one instance corresponds to one row in an evaluation dataset.

Fields

`instance` `Union type`

Instance for pointwise metric. The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:

`jsonInstance` `string`

Instance specified as a json string. String key-value pairs are expected in the jsonInstance to render PointwiseMetricSpec.instance_prompt_template.

`contentMapInstance` `object ( `[`ContentMap`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations/evaluateInstances#ContentMap)` )`

Key-value contents for the mutlimodality input, including text, image, video, audio, and pdf, etc. The key is placeholder in metric prompt template, and the value is the multimodal content.

End of mutually exclusive fields.

**JSON representation**

```
{

  // instance
  "jsonInstance": string,
  "contentMapInstance": {
    object (ContentMap)
  }
  // Union type
}
```

## ContentMap

Map of placeholder in metric prompt template to contents of model input.

Fields

`values` `map (key: string, value: object ( `[`Contents`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations/evaluateInstances#Contents)` ))`

Optional. Map of placeholder to contents.

**JSON representation**

```
{
  "values": {
    string: {
      object (Contents)
    },
    ...
  }
}
```

## Contents

Repeated Content type.

Fields

`contents[]` `object ( `[`Content`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/Content)` )`

Optional. Repeated contents.

**JSON representation**

```
{
  "contents": [
    {
      object (Content)
    }
  ]
}
```

## PairwiseMetricInput

Input for pairwise metric.

Fields

`metricSpec` `object ( `[`PairwiseMetricSpec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.tuningJobs#PairwiseMetricSpec)` )`

Required. Spec for pairwise metric.

`instance` `object ( `[`PairwiseMetricInstance`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations/evaluateInstances#PairwiseMetricInstance)` )`

Required. Pairwise metric instance.

**JSON representation**

```
{
  "metricSpec": {
    object (PairwiseMetricSpec)
  },
  "instance": {
    object (PairwiseMetricInstance)
  }
}
```

## PairwiseMetricInstance

Pairwise metric instance. Usually one instance corresponds to one row in an evaluation dataset.

Fields

`instance` `Union type`

Instance for pairwise metric. The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:

`jsonInstance` `string`

Instance specified as a json string. String key-value pairs are expected in the jsonInstance to render PairwiseMetricSpec.instance_prompt_template.

`contentMapInstance` `object ( `[`ContentMap`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations/evaluateInstances#ContentMap)` )`

Key-value contents for the mutlimodality input, including text, image, video, audio, and pdf, etc. The key is placeholder in metric prompt template, and the value is the multimodal content.

End of mutually exclusive fields.

**JSON representation**

```
{

  // instance
  "jsonInstance": string,
  "contentMapInstance": {
    object (ContentMap)
  }
  // Union type
}
```

## ToolCallValidInput

Input for tool call valid metric.

Fields

`metricSpec` `object ( `[`ToolCallValidSpec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations/evaluateInstances#ToolCallValidSpec)` )`

Required. Spec for tool call valid metric.

`instances[]` `object ( `[`ToolCallValidInstance`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations/evaluateInstances#ToolCallValidInstance)` )`

Required. Repeated tool call valid instances.

**JSON representation**

```
{
  "metricSpec": {
    object (ToolCallValidSpec)
  },
  "instances": [
    {
      object (ToolCallValidInstance)
    }
  ]
}
```

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

**JSON representation**

```
{
  "prediction": string,
  "reference": string
}
```

## ToolNameMatchInput

Input for tool name match metric.

Fields

`metricSpec` `object ( `[`ToolNameMatchSpec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations/evaluateInstances#ToolNameMatchSpec)` )`

Required. Spec for tool name match metric.

`instances[]` `object ( `[`ToolNameMatchInstance`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations/evaluateInstances#ToolNameMatchInstance)` )`

Required. Repeated tool name match instances.

**JSON representation**

```
{
  "metricSpec": {
    object (ToolNameMatchSpec)
  },
  "instances": [
    {
      object (ToolNameMatchInstance)
    }
  ]
}
```

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

**JSON representation**

```
{
  "prediction": string,
  "reference": string
}
```

## ToolParameterKeyMatchInput

Input for tool parameter key match metric.

Fields

`metricSpec` `object ( `[`ToolParameterKeyMatchSpec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations/evaluateInstances#ToolParameterKeyMatchSpec)` )`

Required. Spec for tool parameter key match metric.

`instances[]` `object ( `[`ToolParameterKeyMatchInstance`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations/evaluateInstances#ToolParameterKeyMatchInstance)` )`

Required. Repeated tool parameter key match instances.

**JSON representation**

```
{
  "metricSpec": {
    object (ToolParameterKeyMatchSpec)
  },
  "instances": [
    {
      object (ToolParameterKeyMatchInstance)
    }
  ]
}
```

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

**JSON representation**

```
{
  "prediction": string,
  "reference": string
}
```

## ToolParameterKVMatchInput

Input for tool parameter key value match metric.

Fields

`metricSpec` `object ( `[`ToolParameterKVMatchSpec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations/evaluateInstances#ToolParameterKVMatchSpec)` )`

Required. Spec for tool parameter key value match metric.

`instances[]` `object ( `[`ToolParameterKVMatchInstance`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations/evaluateInstances#ToolParameterKVMatchInstance)` )`

Required. Repeated tool parameter key value match instances.

**JSON representation**

```
{
  "metricSpec": {
    object (ToolParameterKVMatchSpec)
  },
  "instances": [
    {
      object (ToolParameterKVMatchInstance)
    }
  ]
}
```

## ToolParameterKVMatchSpec

Spec for tool parameter key value match metric.

Fields

`useStrictStringMatch` `boolean`

Optional. Whether to use STRICT string match on parameter values.

**JSON representation**

```
{
  "useStrictStringMatch": boolean
}
```

## ToolParameterKVMatchInstance

Spec for tool parameter key value match instance.

Fields

`prediction` `string`

Required. Output of the evaluated model.

`reference` `string`

Required. Ground truth used to compare against the prediction.

**JSON representation**

```
{
  "prediction": string,
  "reference": string
}
```

## CometInput

Input for Comet metric.

Fields

`metricSpec` `object ( `[`CometSpec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations/evaluateInstances#CometSpec)` )`

Required. Spec for comet metric.

`instance` `object ( `[`CometInstance`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations/evaluateInstances#CometInstance)` )`

Required. Comet instance.

**JSON representation**

```
{
  "metricSpec": {
    object (CometSpec)
  },
  "instance": {
    object (CometInstance)
  }
}
```

## CometSpec

Spec for Comet metric.

Fields

`sourceLanguage` `string`

Optional. Source language in BCP-47 format.

`targetLanguage` `string`

Optional. Target language in BCP-47 format. Covers both prediction and reference.

`version` `enum ( `[`CometVersion`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations/evaluateInstances#CometVersion)` )`

Required. Which version to use for evaluation.

**JSON representation**

```
{
  "sourceLanguage": string,
  "targetLanguage": string,
  "version": enum (CometVersion)
}
```

## CometVersion

Comet version options.

| Enums                       |                                                                            |
|-----------------------------|----------------------------------------------------------------------------|
| `COMET_VERSION_UNSPECIFIED` | Comet version unspecified.                                                 |
| `COMET_22_SRC_REF`          | Comet 22 for translation + source + reference (source-reference-combined). |

## CometInstance

Spec for Comet instance - The fields used for evaluation are dependent on the comet version.

Fields

`prediction` `string`

Required. Output of the evaluated model.

`reference` `string`

Optional. Ground truth used to compare against the prediction.

`source` `string`

Optional. Source text in original language.

**JSON representation**

```
{
  "prediction": string,
  "reference": string,
  "source": string
}
```

## MetricxInput

Input for MetricX metric.

Fields

`metricSpec` `object ( `[`MetricxSpec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations/evaluateInstances#MetricxSpec)` )`

Required. Spec for Metricx metric.

`instance` `object ( `[`MetricxInstance`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations/evaluateInstances#MetricxInstance)` )`

Required. Metricx instance.

**JSON representation**

```
{
  "metricSpec": {
    object (MetricxSpec)
  },
  "instance": {
    object (MetricxInstance)
  }
}
```

## MetricxSpec

Spec for MetricX metric.

Fields

`sourceLanguage` `string`

Optional. Source language in BCP-47 format.

`targetLanguage` `string`

Optional. Target language in BCP-47 format. Covers both prediction and reference.

`version` `enum ( `[`MetricxVersion`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations/evaluateInstances#MetricxVersion)` )`

Required. Which version to use for evaluation.

**JSON representation**

```
{
  "sourceLanguage": string,
  "targetLanguage": string,
  "version": enum (MetricxVersion)
}
```

## MetricxVersion

MetricX version options.

| Enums                         |                                                                                      |
|-------------------------------|--------------------------------------------------------------------------------------|
| `METRICX_VERSION_UNSPECIFIED` | MetricX version unspecified.                                                         |
| `METRICX_24_REF`              | MetricX 2024 (2.6) for translation + reference (reference-based).                    |
| `METRICX_24_SRC`              | MetricX 2024 (2.6) for translation + source (QE).                                    |
| `METRICX_24_SRC_REF`          | MetricX 2024 (2.6) for translation + source + reference (source-reference-combined). |

## MetricxInstance

Spec for MetricX instance - The fields used for evaluation are dependent on the MetricX version.

Fields

`prediction` `string`

Required. Output of the evaluated model.

`reference` `string`

Optional. Ground truth used to compare against the prediction.

`source` `string`

Optional. Source text in original language.

**JSON representation**

```
{
  "prediction": string,
  "reference": string,
  "source": string
}
```

## TrajectoryExactMatchInput

Instances and metric spec for TrajectoryExactMatch metric.

Fields

`metricSpec` `object ( `[`TrajectoryExactMatchSpec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations/evaluateInstances#TrajectoryExactMatchSpec)` )`

Required. Spec for TrajectoryExactMatch metric.

`instances[]` `object ( `[`TrajectoryExactMatchInstance`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations/evaluateInstances#TrajectoryExactMatchInstance)` )`

Required. Repeated TrajectoryExactMatch instance.

**JSON representation**

```
{
  "metricSpec": {
    object (TrajectoryExactMatchSpec)
  },
  "instances": [
    {
      object (TrajectoryExactMatchInstance)
    }
  ]
}
```

## TrajectoryExactMatchSpec

This type has no fields.

Spec for TrajectoryExactMatch metric - returns 1 if tool calls in the reference trajectory exactly match the predicted trajectory, else 0.

## TrajectoryExactMatchInstance

Spec for TrajectoryExactMatch instance.

Fields

`predictedTrajectory` `object ( `[`Trajectory`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations/evaluateInstances#Trajectory)` )`

Required. Spec for predicted tool call trajectory.

`referenceTrajectory` `object ( `[`Trajectory`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations/evaluateInstances#Trajectory)` )`

Required. Spec for reference tool call trajectory.

**JSON representation**

```
{
  "predictedTrajectory": {
    object (Trajectory)
  },
  "referenceTrajectory": {
    object (Trajectory)
  }
}
```

## Trajectory

Spec for trajectory.

Fields

`toolCalls[]` `object ( `[`ToolCall`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations/evaluateInstances#ToolCall)` )`

Required. Tool calls in the trajectory.

**JSON representation**

```
{
  "toolCalls": [
    {
      object (ToolCall)
    }
  ]
}
```

## ToolCall

Spec for tool call.

Fields

`toolName` `string`

Required. Spec for tool name

`toolInput` `string`

Optional. Spec for tool input

**JSON representation**

```
{
  "toolName": string,
  "toolInput": string
}
```

## TrajectoryInOrderMatchInput

Instances and metric spec for TrajectoryInOrderMatch metric.

Fields

`metricSpec` `object ( `[`TrajectoryInOrderMatchSpec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations/evaluateInstances#TrajectoryInOrderMatchSpec)` )`

Required. Spec for TrajectoryInOrderMatch metric.

`instances[]` `object ( `[`TrajectoryInOrderMatchInstance`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations/evaluateInstances#TrajectoryInOrderMatchInstance)` )`

Required. Repeated TrajectoryInOrderMatch instance.

**JSON representation**

```
{
  "metricSpec": {
    object (TrajectoryInOrderMatchSpec)
  },
  "instances": [
    {
      object (TrajectoryInOrderMatchInstance)
    }
  ]
}
```

## TrajectoryInOrderMatchSpec

This type has no fields.

Spec for TrajectoryInOrderMatch metric - returns 1 if tool calls in the reference trajectory appear in the predicted trajectory in the same order, else 0.

## TrajectoryInOrderMatchInstance

Spec for TrajectoryInOrderMatch instance.

Fields

`predictedTrajectory` `object ( `[`Trajectory`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations/evaluateInstances#Trajectory)` )`

Required. Spec for predicted tool call trajectory.

`referenceTrajectory` `object ( `[`Trajectory`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations/evaluateInstances#Trajectory)` )`

Required. Spec for reference tool call trajectory.

**JSON representation**

```
{
  "predictedTrajectory": {
    object (Trajectory)
  },
  "referenceTrajectory": {
    object (Trajectory)
  }
}
```

## TrajectoryAnyOrderMatchInput

Instances and metric spec for TrajectoryAnyOrderMatch metric.

Fields

`metricSpec` `object ( `[`TrajectoryAnyOrderMatchSpec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations/evaluateInstances#TrajectoryAnyOrderMatchSpec)` )`

Required. Spec for TrajectoryAnyOrderMatch metric.

`instances[]` `object ( `[`TrajectoryAnyOrderMatchInstance`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations/evaluateInstances#TrajectoryAnyOrderMatchInstance)` )`

Required. Repeated TrajectoryAnyOrderMatch instance.

**JSON representation**

```
{
  "metricSpec": {
    object (TrajectoryAnyOrderMatchSpec)
  },
  "instances": [
    {
      object (TrajectoryAnyOrderMatchInstance)
    }
  ]
}
```

## TrajectoryAnyOrderMatchSpec

This type has no fields.

Spec for TrajectoryAnyOrderMatch metric - returns 1 if all tool calls in the reference trajectory appear in the predicted trajectory in any order, else 0.

## TrajectoryAnyOrderMatchInstance

Spec for TrajectoryAnyOrderMatch instance.

Fields

`predictedTrajectory` `object ( `[`Trajectory`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations/evaluateInstances#Trajectory)` )`

Required. Spec for predicted tool call trajectory.

`referenceTrajectory` `object ( `[`Trajectory`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations/evaluateInstances#Trajectory)` )`

Required. Spec for reference tool call trajectory.

**JSON representation**

```
{
  "predictedTrajectory": {
    object (Trajectory)
  },
  "referenceTrajectory": {
    object (Trajectory)
  }
}
```

## TrajectoryPrecisionInput

Instances and metric spec for TrajectoryPrecision metric.

Fields

`metricSpec` `object ( `[`TrajectoryPrecisionSpec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations/evaluateInstances#TrajectoryPrecisionSpec)` )`

Required. Spec for TrajectoryPrecision metric.

`instances[]` `object ( `[`TrajectoryPrecisionInstance`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations/evaluateInstances#TrajectoryPrecisionInstance)` )`

Required. Repeated TrajectoryPrecision instance.

**JSON representation**

```
{
  "metricSpec": {
    object (TrajectoryPrecisionSpec)
  },
  "instances": [
    {
      object (TrajectoryPrecisionInstance)
    }
  ]
}
```

## TrajectoryPrecisionSpec

This type has no fields.

Spec for TrajectoryPrecision metric - returns a float score based on average precision of individual tool calls.

## TrajectoryPrecisionInstance

Spec for TrajectoryPrecision instance.

Fields

`predictedTrajectory` `object ( `[`Trajectory`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations/evaluateInstances#Trajectory)` )`

Required. Spec for predicted tool call trajectory.

`referenceTrajectory` `object ( `[`Trajectory`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations/evaluateInstances#Trajectory)` )`

Required. Spec for reference tool call trajectory.

**JSON representation**

```
{
  "predictedTrajectory": {
    object (Trajectory)
  },
  "referenceTrajectory": {
    object (Trajectory)
  }
}
```

## TrajectoryRecallInput

Instances and metric spec for TrajectoryRecall metric.

Fields

`metricSpec` `object ( `[`TrajectoryRecallSpec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations/evaluateInstances#TrajectoryRecallSpec)` )`

Required. Spec for TrajectoryRecall metric.

`instances[]` `object ( `[`TrajectoryRecallInstance`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations/evaluateInstances#TrajectoryRecallInstance)` )`

Required. Repeated TrajectoryRecall instance.

**JSON representation**

```
{
  "metricSpec": {
    object (TrajectoryRecallSpec)
  },
  "instances": [
    {
      object (TrajectoryRecallInstance)
    }
  ]
}
```

## TrajectoryRecallSpec

This type has no fields.

Spec for TrajectoryRecall metric - returns a float score based on average recall of individual tool calls.

## TrajectoryRecallInstance

Spec for TrajectoryRecall instance.

Fields

`predictedTrajectory` `object ( `[`Trajectory`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations/evaluateInstances#Trajectory)` )`

Required. Spec for predicted tool call trajectory.

`referenceTrajectory` `object ( `[`Trajectory`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations/evaluateInstances#Trajectory)` )`

Required. Spec for reference tool call trajectory.

**JSON representation**

```
{
  "predictedTrajectory": {
    object (Trajectory)
  },
  "referenceTrajectory": {
    object (Trajectory)
  }
}
```

## TrajectorySingleToolUseInput

Instances and metric spec for TrajectorySingleToolUse metric.

Fields

`metricSpec` `object ( `[`TrajectorySingleToolUseSpec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations/evaluateInstances#TrajectorySingleToolUseSpec)` )`

Required. Spec for TrajectorySingleToolUse metric.

`instances[]` `object ( `[`TrajectorySingleToolUseInstance`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations/evaluateInstances#TrajectorySingleToolUseInstance)` )`

Required. Repeated TrajectorySingleToolUse instance.

**JSON representation**

```
{
  "metricSpec": {
    object (TrajectorySingleToolUseSpec)
  },
  "instances": [
    {
      object (TrajectorySingleToolUseInstance)
    }
  ]
}
```

## TrajectorySingleToolUseSpec

Spec for TrajectorySingleToolUse metric - returns 1 if tool is present in the predicted trajectory, else 0.

Fields

`toolName` `string`

Required. Spec for tool name to be checked for in the predicted trajectory.

**JSON representation**

```
{
  "toolName": string
}
```

## TrajectorySingleToolUseInstance

Spec for TrajectorySingleToolUse instance.

Fields

`predictedTrajectory` `object ( `[`Trajectory`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations/evaluateInstances#Trajectory)` )`

Required. Spec for predicted tool call trajectory.

**JSON representation**

```
{
  "predictedTrajectory": {
    object (Trajectory)
  }
}
```

## ExactMatchResults

Results for exact match metric.

Fields

`exactMatchMetricValues[]` `object ( `[`ExactMatchMetricValue`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.tuningJobs#ExactMatchMetricValue)` )`

Output only. Exact match metric values.

**JSON representation**

```
{
  "exactMatchMetricValues": [
    {
      object (ExactMatchMetricValue)
    }
  ]
}
```

## BleuResults

Results for bleu metric.

Fields

`bleuMetricValues[]` `object ( `[`BleuMetricValue`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.tuningJobs#BleuMetricValue)` )`

Output only. Bleu metric values.

**JSON representation**

```
{
  "bleuMetricValues": [
    {
      object (BleuMetricValue)
    }
  ]
}
```

## RougeResults

Results for rouge metric.

Fields

`rougeMetricValues[]` `object ( `[`RougeMetricValue`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.tuningJobs#RougeMetricValue)` )`

Output only. Rouge metric values.

**JSON representation**

```
{
  "rougeMetricValues": [
    {
      object (RougeMetricValue)
    }
  ]
}
```

## FluencyResult

Spec for fluency result.

Fields

`explanation` `string`

Output only. Explanation for fluency score.

`score` `number`

Output only. Fluency score.

`confidence` `number`

Output only. confidence for fluency score.

**JSON representation**

```
{
  "explanation": string,
  "score": number,
  "confidence": number
}
```

## CoherenceResult

Spec for coherence result.

Fields

`explanation` `string`

Output only. Explanation for coherence score.

`score` `number`

Output only. Coherence score.

`confidence` `number`

Output only. confidence for coherence score.

**JSON representation**

```
{
  "explanation": string,
  "score": number,
  "confidence": number
}
```

## SafetyResult

Spec for safety result.

Fields

`explanation` `string`

Output only. Explanation for safety score.

`score` `number`

Output only. Safety score.

`confidence` `number`

Output only. confidence for safety score.

**JSON representation**

```
{
  "explanation": string,
  "score": number,
  "confidence": number
}
```

## GroundednessResult

Spec for groundedness result.

Fields

`explanation` `string`

Output only. Explanation for groundedness score.

`score` `number`

Output only. Groundedness score.

`confidence` `number`

Output only. confidence for groundedness score.

**JSON representation**

```
{
  "explanation": string,
  "score": number,
  "confidence": number
}
```

## FulfillmentResult

Spec for fulfillment result.

Fields

`explanation` `string`

Output only. Explanation for fulfillment score.

`score` `number`

Output only. Fulfillment score.

`confidence` `number`

Output only. confidence for fulfillment score.

**JSON representation**

```
{
  "explanation": string,
  "score": number,
  "confidence": number
}
```

## SummarizationQualityResult

Spec for summarization quality result.

Fields

`explanation` `string`

Output only. Explanation for summarization quality score.

`score` `number`

Output only. Summarization Quality score.

`confidence` `number`

Output only. confidence for summarization quality score.

**JSON representation**

```
{
  "explanation": string,
  "score": number,
  "confidence": number
}
```

## PairwiseSummarizationQualityResult

Spec for pairwise summarization quality result.

Fields

`pairwiseChoice` `enum ( `[`PairwiseChoice`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.tuningJobs#PairwiseChoice)` )`

Output only. Pairwise summarization prediction choice.

`explanation` `string`

Output only. Explanation for summarization quality score.

`confidence` `number`

Output only. confidence for summarization quality score.

**JSON representation**

```
{
  "pairwiseChoice": enum (PairwiseChoice),
  "explanation": string,
  "confidence": number
}
```

## SummarizationHelpfulnessResult

Spec for summarization helpfulness result.

Fields

`explanation` `string`

Output only. Explanation for summarization helpfulness score.

`score` `number`

Output only. Summarization Helpfulness score.

`confidence` `number`

Output only. confidence for summarization helpfulness score.

**JSON representation**

```
{
  "explanation": string,
  "score": number,
  "confidence": number
}
```

## SummarizationVerbosityResult

Spec for summarization verbosity result.

Fields

`explanation` `string`

Output only. Explanation for summarization verbosity score.

`score` `number`

Output only. Summarization Verbosity score.

`confidence` `number`

Output only. confidence for summarization verbosity score.

**JSON representation**

```
{
  "explanation": string,
  "score": number,
  "confidence": number
}
```

## QuestionAnsweringQualityResult

Spec for question answering quality result.

Fields

`explanation` `string`

Output only. Explanation for question answering quality score.

`score` `number`

Output only. Question Answering Quality score.

`confidence` `number`

Output only. confidence for question answering quality score.

**JSON representation**

```
{
  "explanation": string,
  "score": number,
  "confidence": number
}
```

## PairwiseQuestionAnsweringQualityResult

Spec for pairwise question answering quality result.

Fields

`pairwiseChoice` `enum ( `[`PairwiseChoice`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.tuningJobs#PairwiseChoice)` )`

Output only. Pairwise question answering prediction choice.

`explanation` `string`

Output only. Explanation for question answering quality score.

`confidence` `number`

Output only. confidence for question answering quality score.

**JSON representation**

```
{
  "pairwiseChoice": enum (PairwiseChoice),
  "explanation": string,
  "confidence": number
}
```

## QuestionAnsweringRelevanceResult

Spec for question answering relevance result.

Fields

`explanation` `string`

Output only. Explanation for question answering relevance score.

`score` `number`

Output only. Question Answering Relevance score.

`confidence` `number`

Output only. confidence for question answering relevance score.

**JSON representation**

```
{
  "explanation": string,
  "score": number,
  "confidence": number
}
```

## QuestionAnsweringHelpfulnessResult

Spec for question answering helpfulness result.

Fields

`explanation` `string`

Output only. Explanation for question answering helpfulness score.

`score` `number`

Output only. Question Answering Helpfulness score.

`confidence` `number`

Output only. confidence for question answering helpfulness score.

**JSON representation**

```
{
  "explanation": string,
  "score": number,
  "confidence": number
}
```

## QuestionAnsweringCorrectnessResult

Spec for question answering correctness result.

Fields

`explanation` `string`

Output only. Explanation for question answering correctness score.

`score` `number`

Output only. Question Answering Correctness score.

`confidence` `number`

Output only. confidence for question answering correctness score.

**JSON representation**

```
{
  "explanation": string,
  "score": number,
  "confidence": number
}
```

## ToolCallValidResults

Results for tool call valid metric.

Fields

`toolCallValidMetricValues[]` `object ( `[`ToolCallValidMetricValue`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations/evaluateInstances#ToolCallValidMetricValue)` )`

Output only. Tool call valid metric values.

**JSON representation**

```
{
  "toolCallValidMetricValues": [
    {
      object (ToolCallValidMetricValue)
    }
  ]
}
```

## ToolCallValidMetricValue

Tool call valid metric value for an instance.

Fields

`score` `number`

Output only. Tool call valid score.

**JSON representation**

```
{
  "score": number
}
```

## ToolNameMatchResults

Results for tool name match metric.

Fields

`toolNameMatchMetricValues[]` `object ( `[`ToolNameMatchMetricValue`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations/evaluateInstances#ToolNameMatchMetricValue)` )`

Output only. Tool name match metric values.

**JSON representation**

```
{
  "toolNameMatchMetricValues": [
    {
      object (ToolNameMatchMetricValue)
    }
  ]
}
```

## ToolNameMatchMetricValue

Tool name match metric value for an instance.

Fields

`score` `number`

Output only. Tool name match score.

**JSON representation**

```
{
  "score": number
}
```

## ToolParameterKeyMatchResults

Results for tool parameter key match metric.

Fields

`toolParameterKeyMatchMetricValues[]` `object ( `[`ToolParameterKeyMatchMetricValue`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations/evaluateInstances#ToolParameterKeyMatchMetricValue)` )`

Output only. Tool parameter key match metric values.

**JSON representation**

```
{
  "toolParameterKeyMatchMetricValues": [
    {
      object (ToolParameterKeyMatchMetricValue)
    }
  ]
}
```

## ToolParameterKeyMatchMetricValue

Tool parameter key match metric value for an instance.

Fields

`score` `number`

Output only. Tool parameter key match score.

**JSON representation**

```
{
  "score": number
}
```

## ToolParameterKVMatchResults

Results for tool parameter key value match metric.

Fields

`toolParameterKvMatchMetricValues[]` `object ( `[`ToolParameterKVMatchMetricValue`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations/evaluateInstances#ToolParameterKVMatchMetricValue)` )`

Output only. Tool parameter key value match metric values.

**JSON representation**

```
{
  "toolParameterKvMatchMetricValues": [
    {
      object (ToolParameterKVMatchMetricValue)
    }
  ]
}
```

## ToolParameterKVMatchMetricValue

Tool parameter key value match metric value for an instance.

Fields

`score` `number`

Output only. Tool parameter key value match score.

**JSON representation**

```
{
  "score": number
}
```

## CometResult

Spec for Comet result - calculates the comet score for the given instance using the version specified in the spec.

Fields

`score` `number`

Output only. Comet score. Range depends on version.

**JSON representation**

```
{
  "score": number
}
```

## MetricxResult

Spec for MetricX result - calculates the MetricX score for the given instance using the version specified in the spec.

Fields

`score` `number`

Output only. MetricX score. Range depends on version.

**JSON representation**

```
{
  "score": number
}
```

## TrajectoryExactMatchResults

Results for TrajectoryExactMatch metric.

Fields

`trajectoryExactMatchMetricValues[]` `object ( `[`TrajectoryExactMatchMetricValue`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations/evaluateInstances#TrajectoryExactMatchMetricValue)` )`

Output only. TrajectoryExactMatch metric values.

**JSON representation**

```
{
  "trajectoryExactMatchMetricValues": [
    {
      object (TrajectoryExactMatchMetricValue)
    }
  ]
}
```

## TrajectoryExactMatchMetricValue

TrajectoryExactMatch metric value for an instance.

Fields

`score` `number`

Output only. TrajectoryExactMatch score.

**JSON representation**

```
{
  "score": number
}
```

## TrajectoryInOrderMatchResults

Results for TrajectoryInOrderMatch metric.

Fields

`trajectoryInOrderMatchMetricValues[]` `object ( `[`TrajectoryInOrderMatchMetricValue`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations/evaluateInstances#TrajectoryInOrderMatchMetricValue)` )`

Output only. TrajectoryInOrderMatch metric values.

**JSON representation**

```
{
  "trajectoryInOrderMatchMetricValues": [
    {
      object (TrajectoryInOrderMatchMetricValue)
    }
  ]
}
```

## TrajectoryInOrderMatchMetricValue

TrajectoryInOrderMatch metric value for an instance.

Fields

`score` `number`

Output only. TrajectoryInOrderMatch score.

**JSON representation**

```
{
  "score": number
}
```

## TrajectoryAnyOrderMatchResults

Results for TrajectoryAnyOrderMatch metric.

Fields

`trajectoryAnyOrderMatchMetricValues[]` `object ( `[`TrajectoryAnyOrderMatchMetricValue`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations/evaluateInstances#TrajectoryAnyOrderMatchMetricValue)` )`

Output only. TrajectoryAnyOrderMatch metric values.

**JSON representation**

```
{
  "trajectoryAnyOrderMatchMetricValues": [
    {
      object (TrajectoryAnyOrderMatchMetricValue)
    }
  ]
}
```

## TrajectoryAnyOrderMatchMetricValue

TrajectoryAnyOrderMatch metric value for an instance.

Fields

`score` `number`

Output only. TrajectoryAnyOrderMatch score.

**JSON representation**

```
{
  "score": number
}
```

## TrajectoryPrecisionResults

Results for TrajectoryPrecision metric.

Fields

`trajectoryPrecisionMetricValues[]` `object ( `[`TrajectoryPrecisionMetricValue`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations/evaluateInstances#TrajectoryPrecisionMetricValue)` )`

Output only. TrajectoryPrecision metric values.

**JSON representation**

```
{
  "trajectoryPrecisionMetricValues": [
    {
      object (TrajectoryPrecisionMetricValue)
    }
  ]
}
```

## TrajectoryPrecisionMetricValue

TrajectoryPrecision metric value for an instance.

Fields

`score` `number`

Output only. TrajectoryPrecision score.

**JSON representation**

```
{
  "score": number
}
```

## TrajectoryRecallResults

Results for TrajectoryRecall metric.

Fields

`trajectoryRecallMetricValues[]` `object ( `[`TrajectoryRecallMetricValue`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations/evaluateInstances#TrajectoryRecallMetricValue)` )`

Output only. TrajectoryRecall metric values.

**JSON representation**

```
{
  "trajectoryRecallMetricValues": [
    {
      object (TrajectoryRecallMetricValue)
    }
  ]
}
```

## TrajectoryRecallMetricValue

TrajectoryRecall metric value for an instance.

Fields

`score` `number`

Output only. TrajectoryRecall score.

**JSON representation**

```
{
  "score": number
}
```

## TrajectorySingleToolUseResults

Results for TrajectorySingleToolUse metric.

Fields

`trajectorySingleToolUseMetricValues[]` `object ( `[`TrajectorySingleToolUseMetricValue`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations/evaluateInstances#TrajectorySingleToolUseMetricValue)` )`

Output only. TrajectorySingleToolUse metric values.

**JSON representation**

```
{
  "trajectorySingleToolUseMetricValues": [
    {
      object (TrajectorySingleToolUseMetricValue)
    }
  ]
}
```

## TrajectorySingleToolUseMetricValue

TrajectorySingleToolUse metric value for an instance.

Fields

`score` `number`

Output only. TrajectorySingleToolUse score.

**JSON representation**

```
{
  "score": number
}
```

## MetricResult

result for a single metric on a single instance.

Fields

`score` `number`

Output only. The score for the metric. Please refer to each metric's documentation for the meaning of the score.

`explanation` `string`

Output only. The explanation for the metric result.

`error` `object ( `[`Status`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/ListOperationsResponse#Status)` )`

Output only. The error status for the metric result.

**JSON representation**

```
{
  "score": number,
  "explanation": string,
  "error": {
    object (Status)
  }
}
```
