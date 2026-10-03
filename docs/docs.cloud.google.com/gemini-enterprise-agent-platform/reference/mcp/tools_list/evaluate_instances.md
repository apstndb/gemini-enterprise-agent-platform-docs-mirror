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

**Curl Request**

```
curl --location 'https://aiplatform.googleapis.com/mcp/generate' \
--header 'content-type: application/json' \
--header 'accept: application/json, text/event-stream' \
--data '{
  "method": "tools/call",
  "params": {
    "name": "evaluate_instances",
    "arguments": {
      // provide these details according to the tool's MCP specification
    }
  },
  "jsonrpc": "2.0",
  "id": 1
}'
```

## Input Schema

Request message for EvaluationService.EvaluateInstances.

### EvaluateInstancesRequest

**JSON representation**

```
{
  "location": string,
  "metrics": [
    {
      object (Metric)
    }
  ],
  "metricSources": [
    {
      object (MetricSource)
    }
  ],
  "instance": {
    object (EvaluationInstance)
  },
  "autoraterConfig": {
    object (AutoraterConfig)
  },

  // Union field metric_inputs can be only one of the following:
  "exactMatchInput": {
    object (ExactMatchInput)
  },
  "bleuInput": {
    object (BleuInput)
  },
  "rougeInput": {
    object (RougeInput)
  },
  "fluencyInput": {
    object (FluencyInput)
  },
  "coherenceInput": {
    object (CoherenceInput)
  },
  "safetyInput": {
    object (SafetyInput)
  },
  "groundednessInput": {
    object (GroundednessInput)
  },
  "fulfillmentInput": {
    object (FulfillmentInput)
  },
  "summarizationQualityInput": {
    object (SummarizationQualityInput)
  },
  "pairwiseSummarizationQualityInput": {
    object (PairwiseSummarizationQualityInput)
  },
  "summarizationHelpfulnessInput": {
    object (SummarizationHelpfulnessInput)
  },
  "summarizationVerbosityInput": {
    object (SummarizationVerbosityInput)
  },
  "questionAnsweringQualityInput": {
    object (QuestionAnsweringQualityInput)
  },
  "pairwiseQuestionAnsweringQualityInput": {
    object (PairwiseQuestionAnsweringQualityInput)
  },
  "questionAnsweringRelevanceInput": {
    object (QuestionAnsweringRelevanceInput)
  },
  "questionAnsweringHelpfulnessInput": {
    object (QuestionAnsweringHelpfulnessInput)
  },
  "questionAnsweringCorrectnessInput": {
    object (QuestionAnsweringCorrectnessInput)
  },
  "pointwiseMetricInput": {
    object (PointwiseMetricInput)
  },
  "pairwiseMetricInput": {
    object (PairwiseMetricInput)
  },
  "toolCallValidInput": {
    object (ToolCallValidInput)
  },
  "toolNameMatchInput": {
    object (ToolNameMatchInput)
  },
  "toolParameterKeyMatchInput": {
    object (ToolParameterKeyMatchInput)
  },
  "toolParameterKvMatchInput": {
    object (ToolParameterKVMatchInput)
  },
  "cometInput": {
    object (CometInput)
  },
  "metricxInput": {
    object (MetricxInput)
  },
  "trajectoryExactMatchInput": {
    object (TrajectoryExactMatchInput)
  },
  "trajectoryInOrderMatchInput": {
    object (TrajectoryInOrderMatchInput)
  },
  "trajectoryAnyOrderMatchInput": {
    object (TrajectoryAnyOrderMatchInput)
  },
  "trajectoryPrecisionInput": {
    object (TrajectoryPrecisionInput)
  },
  "trajectoryRecallInput": {
    object (TrajectoryRecallInput)
  },
  "trajectorySingleToolUseInput": {
    object (TrajectorySingleToolUseInput)
  },
  "rubricBasedInstructionFollowingInput": {
    object (RubricBasedInstructionFollowingInput)
  }
  // End of list of possible types for union field metric_inputs.
}
```

| Fields                                                                                                             |                                                                                                                                                                                                                                                                                                                                                                                         |
|--------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `location`                                                                                                         | `string` Required. The resource name of the Location to evaluate the instances. Format: `projects/{project}/locations/{location}`                                                                                                                                                                                                                                                       |
| `metrics[]`                                                                                                        | `object ( `[`Metric`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.Metric)` )` The metrics used for evaluation. Currently, we only support evaluating a single metric. If multiple metrics are provided, only the first one will be evaluated.                                                               |
| `metricSources[]`                                                                                                  | `object ( `[`MetricSource`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.MetricSource)` )` Optional. The metrics (either inline or registered) used for evaluation. Currently, we only support evaluating a single metric. If multiple metrics are provided, only the first one will be evaluated.           |
| `instance`                                                                                                         | `object ( `[`EvaluationInstance`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.EvaluationInstance)` )` The instance to be evaluated.                                                                                                                                                                         |
| `autoraterConfig`                                                                                                  | `object ( `[`AutoraterConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.AutoraterConfig)` )` Optional. Autorater config used for evaluation. Not applicable for predefined metrics (PredefinedMetricSpec); the server uses its own model configuration for predefined metrics and this field is ignored. |
| Union field `metric_inputs` . Instances and specs for evaluation `metric_inputs` can be only one of the following: |                                                                                                                                                                                                                                                                                                                                                                                         |
| `exactMatchInput`                                                                                                  | `object ( `[`ExactMatchInput`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.ExactMatchInput)` )` Auto metric instances. Instances and metric spec for exact match metric.                                                                                                                                    |
| `bleuInput`                                                                                                        | `object ( `[`BleuInput`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.BleuInput)` )` Instances and metric spec for bleu metric.                                                                                                                                                                              |
| `rougeInput`                                                                                                       | `object ( `[`RougeInput`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.RougeInput)` )` Instances and metric spec for rouge metric.                                                                                                                                                                           |
| `fluencyInput`                                                                                                     | `object ( `[`FluencyInput`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.FluencyInput)` )` LLM-based metric instance. General text generation metrics, applicable to other categories. Input for fluency metric.                                                                                             |
| `coherenceInput`                                                                                                   | `object ( `[`CoherenceInput`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.CoherenceInput)` )` Input for coherence metric.                                                                                                                                                                                   |
| `safetyInput`                                                                                                      | `object ( `[`SafetyInput`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.SafetyInput)` )` Input for safety metric.                                                                                                                                                                                            |
| `groundednessInput`                                                                                                | `object ( `[`GroundednessInput`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.GroundednessInput)` )` Input for groundedness metric.                                                                                                                                                                          |
| `fulfillmentInput`                                                                                                 | `object ( `[`FulfillmentInput`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.FulfillmentInput)` )` Input for fulfillment metric.                                                                                                                                                                             |
| `summarizationQualityInput`                                                                                        | `object ( `[`SummarizationQualityInput`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.SummarizationQualityInput)` )` Input for summarization quality metric.                                                                                                                                                 |
| `pairwiseSummarizationQualityInput`                                                                                | `object ( `[`PairwiseSummarizationQualityInput`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.PairwiseSummarizationQualityInput)` )` Input for pairwise summarization quality metric.                                                                                                                        |
| `summarizationHelpfulnessInput`                                                                                    | `object ( `[`SummarizationHelpfulnessInput`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.SummarizationHelpfulnessInput)` )` Input for summarization helpfulness metric.                                                                                                                                     |
| `summarizationVerbosityInput`                                                                                      | `object ( `[`SummarizationVerbosityInput`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.SummarizationVerbosityInput)` )` Input for summarization verbosity metric.                                                                                                                                           |
| `questionAnsweringQualityInput`                                                                                    | `object ( `[`QuestionAnsweringQualityInput`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.QuestionAnsweringQualityInput)` )` Input for question answering quality metric.                                                                                                                                    |
| `pairwiseQuestionAnsweringQualityInput`                                                                            | `object ( `[`PairwiseQuestionAnsweringQualityInput`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.PairwiseQuestionAnsweringQualityInput)` )` Input for pairwise question answering quality metric.                                                                                                           |
| `questionAnsweringRelevanceInput`                                                                                  | `object ( `[`QuestionAnsweringRelevanceInput`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.QuestionAnsweringRelevanceInput)` )` Input for question answering relevance metric.                                                                                                                              |
| `questionAnsweringHelpfulnessInput`                                                                                | `object ( `[`QuestionAnsweringHelpfulnessInput`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.QuestionAnsweringHelpfulnessInput)` )` Input for question answering helpfulness metric.                                                                                                                        |
| `questionAnsweringCorrectnessInput`                                                                                | `object ( `[`QuestionAnsweringCorrectnessInput`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.QuestionAnsweringCorrectnessInput)` )` Input for question answering correctness metric.                                                                                                                        |
| `pointwiseMetricInput`                                                                                             | `object ( `[`PointwiseMetricInput`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.PointwiseMetricInput)` )` Input for pointwise metric.                                                                                                                                                                       |
| `pairwiseMetricInput`                                                                                              | `object ( `[`PairwiseMetricInput`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.PairwiseMetricInput)` )` Input for pairwise metric.                                                                                                                                                                          |
| `toolCallValidInput`                                                                                               | `object ( `[`ToolCallValidInput`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.ToolCallValidInput)` )` Tool call metric instances. Input for tool call valid metric.                                                                                                                                         |
| `toolNameMatchInput`                                                                                               | `object ( `[`ToolNameMatchInput`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.ToolNameMatchInput)` )` Input for tool name match metric.                                                                                                                                                                     |
| `toolParameterKeyMatchInput`                                                                                       | `object ( `[`ToolParameterKeyMatchInput`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.ToolParameterKeyMatchInput)` )` Input for tool parameter key match metric.                                                                                                                                            |
| `toolParameterKvMatchInput`                                                                                        | `object ( `[`ToolParameterKVMatchInput`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.ToolParameterKVMatchInput)` )` Input for tool parameter key value match metric.                                                                                                                                        |
| `cometInput`                                                                                                       | `object ( `[`CometInput`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.CometInput)` )` Translation metrics. Input for Comet metric.                                                                                                                                                                          |
| `metricxInput`                                                                                                     | `object ( `[`MetricxInput`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.MetricxInput)` )` Input for Metricx metric.                                                                                                                                                                                         |
| `trajectoryExactMatchInput`                                                                                        | `object ( `[`TrajectoryExactMatchInput`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.TrajectoryExactMatchInput)` )` Input for trajectory exact match metric.                                                                                                                                                |
| `trajectoryInOrderMatchInput`                                                                                      | `object ( `[`TrajectoryInOrderMatchInput`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.TrajectoryInOrderMatchInput)` )` Input for trajectory in order match metric.                                                                                                                                         |
| `trajectoryAnyOrderMatchInput`                                                                                     | `object ( `[`TrajectoryAnyOrderMatchInput`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.TrajectoryAnyOrderMatchInput)` )` Input for trajectory match any order metric.                                                                                                                                      |
| `trajectoryPrecisionInput`                                                                                         | `object ( `[`TrajectoryPrecisionInput`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.TrajectoryPrecisionInput)` )` Input for trajectory precision metric.                                                                                                                                                    |
| `trajectoryRecallInput`                                                                                            | `object ( `[`TrajectoryRecallInput`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.TrajectoryRecallInput)` )` Input for trajectory recall metric.                                                                                                                                                             |
| `trajectorySingleToolUseInput`                                                                                     | `object ( `[`TrajectorySingleToolUseInput`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.TrajectorySingleToolUseInput)` )` Input for trajectory single tool use metric.                                                                                                                                      |
| `rubricBasedInstructionFollowingInput`                                                                             | `object ( `[`RubricBasedInstructionFollowingInput`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.RubricBasedInstructionFollowingInput)` )` Rubric Based Instruction Following metric.                                                                                                                        |

### ExactMatchInput

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

| Fields        |                                                                                                                                                                                                                             |
|---------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `metricSpec`  | `object ( ``ExactMatchSpec`` )` Required. Spec for exact match metric.                                                                                                                                                      |
| `instances[]` | `object ( `[`ExactMatchInstance`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.ExactMatchInstance)` )` Required. Repeated exact match instances. |

### ExactMatchInstance

**JSON representation**

```
{

  // Union field _prediction can be only one of the following:
  "prediction": string
  // End of list of possible types for union field _prediction.

  // Union field _reference can be only one of the following:
  "reference": string
  // End of list of possible types for union field _reference.
}
```

| Fields                                                                      |                                                                         |
|-----------------------------------------------------------------------------|-------------------------------------------------------------------------|
| Union field `_prediction` . `_prediction` can be only one of the following: |                                                                         |
| `prediction`                                                                | `string` Required. Output of the evaluated model.                       |
| Union field `_reference` . `_reference` can be only one of the following:   |                                                                         |
| `reference`                                                                 | `string` Required. Ground truth used to compare against the prediction. |

### BleuInput

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

| Fields        |                                                                                                                                                                                                          |
|---------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `metricSpec`  | `object ( `[`BleuSpec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.BleuSpec)` )` Required. Spec for bleu score metric.      |
| `instances[]` | `object ( `[`BleuInstance`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.BleuInstance)` )` Required. Repeated bleu instances. |

### BleuSpec

**JSON representation**

```
{
  "useEffectiveOrder": boolean
}
```

| Fields              |                                                                           |
|---------------------|---------------------------------------------------------------------------|
| `useEffectiveOrder` | `boolean` Optional. Whether to use_effective_order to compute bleu score. |

### BleuInstance

**JSON representation**

```
{

  // Union field _prediction can be only one of the following:
  "prediction": string
  // End of list of possible types for union field _prediction.

  // Union field _reference can be only one of the following:
  "reference": string
  // End of list of possible types for union field _reference.
}
```

| Fields                                                                      |                                                                         |
|-----------------------------------------------------------------------------|-------------------------------------------------------------------------|
| Union field `_prediction` . `_prediction` can be only one of the following: |                                                                         |
| `prediction`                                                                | `string` Required. Output of the evaluated model.                       |
| Union field `_reference` . `_reference` can be only one of the following:   |                                                                         |
| `reference`                                                                 | `string` Required. Ground truth used to compare against the prediction. |

### RougeInput

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

| Fields        |                                                                                                                                                                                                             |
|---------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `metricSpec`  | `object ( `[`RougeSpec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.RougeSpec)` )` Required. Spec for rouge score metric.      |
| `instances[]` | `object ( `[`RougeInstance`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.RougeInstance)` )` Required. Repeated rouge instances. |

### RougeSpec

**JSON representation**

```
{
  "rougeType": string,
  "useStemmer": boolean,
  "splitSummaries": boolean
}
```

| Fields           |                                                                                    |
|------------------|------------------------------------------------------------------------------------|
| `rougeType`      | `string` Optional. Supported rouge types are rougen\[1-9\], rougeL, and rougeLsum. |
| `useStemmer`     | `boolean` Optional. Whether to use stemmer to compute rouge score.                 |
| `splitSummaries` | `boolean` Optional. Whether to split summaries while using rougeLsum.              |

### RougeInstance

**JSON representation**

```
{

  // Union field _prediction can be only one of the following:
  "prediction": string
  // End of list of possible types for union field _prediction.

  // Union field _reference can be only one of the following:
  "reference": string
  // End of list of possible types for union field _reference.
}
```

| Fields                                                                      |                                                                         |
|-----------------------------------------------------------------------------|-------------------------------------------------------------------------|
| Union field `_prediction` . `_prediction` can be only one of the following: |                                                                         |
| `prediction`                                                                | `string` Required. Output of the evaluated model.                       |
| Union field `_reference` . `_reference` can be only one of the following:   |                                                                         |
| `reference`                                                                 | `string` Required. Ground truth used to compare against the prediction. |

### FluencyInput

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

| Fields       |                                                                                                                                                                                                              |
|--------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `metricSpec` | `object ( `[`FluencySpec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.FluencySpec)` )` Required. Spec for fluency score metric. |
| `instance`   | `object ( `[`FluencyInstance`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.FluencyInstance)` )` Required. Fluency instance.      |

### FluencySpec

**JSON representation**

```
{
  "version": integer
}
```

| Fields    |                                                          |
|-----------|----------------------------------------------------------|
| `version` | `integer` Optional. Which version to use for evaluation. |

### FluencyInstance

**JSON representation**

```
{

  // Union field _prediction can be only one of the following:
  "prediction": string
  // End of list of possible types for union field _prediction.
}
```

| Fields                                                                      |                                                   |
|-----------------------------------------------------------------------------|---------------------------------------------------|
| Union field `_prediction` . `_prediction` can be only one of the following: |                                                   |
| `prediction`                                                                | `string` Required. Output of the evaluated model. |

### CoherenceInput

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

| Fields       |                                                                                                                                                                                                                    |
|--------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `metricSpec` | `object ( `[`CoherenceSpec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.CoherenceSpec)` )` Required. Spec for coherence score metric. |
| `instance`   | `object ( `[`CoherenceInstance`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.CoherenceInstance)` )` Required. Coherence instance.      |

### CoherenceSpec

**JSON representation**

```
{
  "version": integer
}
```

| Fields    |                                                          |
|-----------|----------------------------------------------------------|
| `version` | `integer` Optional. Which version to use for evaluation. |

### CoherenceInstance

**JSON representation**

```
{

  // Union field _prediction can be only one of the following:
  "prediction": string
  // End of list of possible types for union field _prediction.
}
```

| Fields                                                                      |                                                   |
|-----------------------------------------------------------------------------|---------------------------------------------------|
| Union field `_prediction` . `_prediction` can be only one of the following: |                                                   |
| `prediction`                                                                | `string` Required. Output of the evaluated model. |

### SafetyInput

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

| Fields       |                                                                                                                                                                                                      |
|--------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `metricSpec` | `object ( `[`SafetySpec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.SafetySpec)` )` Required. Spec for safety metric.  |
| `instance`   | `object ( `[`SafetyInstance`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.SafetyInstance)` )` Required. Safety instance. |

### SafetySpec

**JSON representation**

```
{
  "version": integer
}
```

| Fields    |                                                          |
|-----------|----------------------------------------------------------|
| `version` | `integer` Optional. Which version to use for evaluation. |

### SafetyInstance

**JSON representation**

```
{

  // Union field _prediction can be only one of the following:
  "prediction": string
  // End of list of possible types for union field _prediction.
}
```

| Fields                                                                      |                                                   |
|-----------------------------------------------------------------------------|---------------------------------------------------|
| Union field `_prediction` . `_prediction` can be only one of the following: |                                                   |
| `prediction`                                                                | `string` Required. Output of the evaluated model. |

### GroundednessInput

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

| Fields       |                                                                                                                                                                                                                        |
|--------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `metricSpec` | `object ( `[`GroundednessSpec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.GroundednessSpec)` )` Required. Spec for groundedness metric.  |
| `instance`   | `object ( `[`GroundednessInstance`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.GroundednessInstance)` )` Required. Groundedness instance. |

### GroundednessSpec

**JSON representation**

```
{
  "version": integer
}
```

| Fields    |                                                          |
|-----------|----------------------------------------------------------|
| `version` | `integer` Optional. Which version to use for evaluation. |

### GroundednessInstance

**JSON representation**

```
{

  // Union field _prediction can be only one of the following:
  "prediction": string
  // End of list of possible types for union field _prediction.

  // Union field _context can be only one of the following:
  "context": string
  // End of list of possible types for union field _context.
}
```

| Fields                                                                      |                                                                                                       |
|-----------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------|
| Union field `_prediction` . `_prediction` can be only one of the following: |                                                                                                       |
| `prediction`                                                                | `string` Required. Output of the evaluated model.                                                     |
| Union field `_context` . `_context` can be only one of the following:       |                                                                                                       |
| `context`                                                                   | `string` Required. Background information provided in context used to compare against the prediction. |

### FulfillmentInput

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

| Fields       |                                                                                                                                                                                                                          |
|--------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `metricSpec` | `object ( `[`FulfillmentSpec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.FulfillmentSpec)` )` Required. Spec for fulfillment score metric. |
| `instance`   | `object ( `[`FulfillmentInstance`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.FulfillmentInstance)` )` Required. Fulfillment instance.      |

### FulfillmentSpec

**JSON representation**

```
{
  "version": integer
}
```

| Fields    |                                                          |
|-----------|----------------------------------------------------------|
| `version` | `integer` Optional. Which version to use for evaluation. |

### FulfillmentInstance

**JSON representation**

```
{

  // Union field _prediction can be only one of the following:
  "prediction": string
  // End of list of possible types for union field _prediction.

  // Union field _instruction can be only one of the following:
  "instruction": string
  // End of list of possible types for union field _instruction.
}
```

| Fields                                                                        |                                                                             |
|-------------------------------------------------------------------------------|-----------------------------------------------------------------------------|
| Union field `_prediction` . `_prediction` can be only one of the following:   |                                                                             |
| `prediction`                                                                  | `string` Required. Output of the evaluated model.                           |
| Union field `_instruction` . `_instruction` can be only one of the following: |                                                                             |
| `instruction`                                                                 | `string` Required. Inference instruction prompt to compare prediction with. |

### SummarizationQualityInput

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

| Fields       |                                                                                                                                                                                                                                                      |
|--------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `metricSpec` | `object ( `[`SummarizationQualitySpec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.SummarizationQualitySpec)` )` Required. Spec for summarization quality score metric. |
| `instance`   | `object ( `[`SummarizationQualityInstance`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.SummarizationQualityInstance)` )` Required. Summarization quality instance.      |

### SummarizationQualitySpec

**JSON representation**

```
{
  "useReference": boolean,
  "version": integer
}
```

| Fields         |                                                                                         |
|----------------|-----------------------------------------------------------------------------------------|
| `useReference` | `boolean` Optional. Whether to use instance.reference to compute summarization quality. |
| `version`      | `integer` Optional. Which version to use for evaluation.                                |

### SummarizationQualityInstance

**JSON representation**

```
{

  // Union field _prediction can be only one of the following:
  "prediction": string
  // End of list of possible types for union field _prediction.

  // Union field _reference can be only one of the following:
  "reference": string
  // End of list of possible types for union field _reference.

  // Union field _context can be only one of the following:
  "context": string
  // End of list of possible types for union field _context.

  // Union field _instruction can be only one of the following:
  "instruction": string
  // End of list of possible types for union field _instruction.
}
```

| Fields                                                                        |                                                                         |
|-------------------------------------------------------------------------------|-------------------------------------------------------------------------|
| Union field `_prediction` . `_prediction` can be only one of the following:   |                                                                         |
| `prediction`                                                                  | `string` Required. Output of the evaluated model.                       |
| Union field `_reference` . `_reference` can be only one of the following:     |                                                                         |
| `reference`                                                                   | `string` Optional. Ground truth used to compare against the prediction. |
| Union field `_context` . `_context` can be only one of the following:         |                                                                         |
| `context`                                                                     | `string` Required. Text to be summarized.                               |
| Union field `_instruction` . `_instruction` can be only one of the following: |                                                                         |
| `instruction`                                                                 | `string` Required. Summarization prompt for LLM.                        |

### PairwiseSummarizationQualityInput

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

| Fields       |                                                                                                                                                                                                                                                                               |
|--------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `metricSpec` | `object ( `[`PairwiseSummarizationQualitySpec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.PairwiseSummarizationQualitySpec)` )` Required. Spec for pairwise summarization quality score metric. |
| `instance`   | `object ( `[`PairwiseSummarizationQualityInstance`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.PairwiseSummarizationQualityInstance)` )` Required. Pairwise summarization quality instance.      |

### PairwiseSummarizationQualitySpec

**JSON representation**

```
{
  "useReference": boolean,
  "version": integer
}
```

| Fields         |                                                                                                  |
|----------------|--------------------------------------------------------------------------------------------------|
| `useReference` | `boolean` Optional. Whether to use instance.reference to compute pairwise summarization quality. |
| `version`      | `integer` Optional. Which version to use for evaluation.                                         |

### PairwiseSummarizationQualityInstance

**JSON representation**

```
{

  // Union field _prediction can be only one of the following:
  "prediction": string
  // End of list of possible types for union field _prediction.

  // Union field _baseline_prediction can be only one of the following:
  "baselinePrediction": string
  // End of list of possible types for union field _baseline_prediction.

  // Union field _reference can be only one of the following:
  "reference": string
  // End of list of possible types for union field _reference.

  // Union field _context can be only one of the following:
  "context": string
  // End of list of possible types for union field _context.

  // Union field _instruction can be only one of the following:
  "instruction": string
  // End of list of possible types for union field _instruction.
}
```

| Fields                                                                                        |                                                                         |
|-----------------------------------------------------------------------------------------------|-------------------------------------------------------------------------|
| Union field `_prediction` . `_prediction` can be only one of the following:                   |                                                                         |
| `prediction`                                                                                  | `string` Required. Output of the candidate model.                       |
| Union field `_baseline_prediction` . `_baseline_prediction` can be only one of the following: |                                                                         |
| `baselinePrediction`                                                                          | `string` Required. Output of the baseline model.                        |
| Union field `_reference` . `_reference` can be only one of the following:                     |                                                                         |
| `reference`                                                                                   | `string` Optional. Ground truth used to compare against the prediction. |
| Union field `_context` . `_context` can be only one of the following:                         |                                                                         |
| `context`                                                                                     | `string` Required. Text to be summarized.                               |
| Union field `_instruction` . `_instruction` can be only one of the following:                 |                                                                         |
| `instruction`                                                                                 | `string` Required. Summarization prompt for LLM.                        |

### SummarizationHelpfulnessInput

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

| Fields       |                                                                                                                                                                                                                                                                  |
|--------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `metricSpec` | `object ( `[`SummarizationHelpfulnessSpec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.SummarizationHelpfulnessSpec)` )` Required. Spec for summarization helpfulness score metric. |
| `instance`   | `object ( `[`SummarizationHelpfulnessInstance`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.SummarizationHelpfulnessInstance)` )` Required. Summarization helpfulness instance.      |

### SummarizationHelpfulnessSpec

**JSON representation**

```
{
  "useReference": boolean,
  "version": integer
}
```

| Fields         |                                                                                             |
|----------------|---------------------------------------------------------------------------------------------|
| `useReference` | `boolean` Optional. Whether to use instance.reference to compute summarization helpfulness. |
| `version`      | `integer` Optional. Which version to use for evaluation.                                    |

### SummarizationHelpfulnessInstance

**JSON representation**

```
{

  // Union field _prediction can be only one of the following:
  "prediction": string
  // End of list of possible types for union field _prediction.

  // Union field _reference can be only one of the following:
  "reference": string
  // End of list of possible types for union field _reference.

  // Union field _context can be only one of the following:
  "context": string
  // End of list of possible types for union field _context.

  // Union field _instruction can be only one of the following:
  "instruction": string
  // End of list of possible types for union field _instruction.
}
```

| Fields                                                                        |                                                                         |
|-------------------------------------------------------------------------------|-------------------------------------------------------------------------|
| Union field `_prediction` . `_prediction` can be only one of the following:   |                                                                         |
| `prediction`                                                                  | `string` Required. Output of the evaluated model.                       |
| Union field `_reference` . `_reference` can be only one of the following:     |                                                                         |
| `reference`                                                                   | `string` Optional. Ground truth used to compare against the prediction. |
| Union field `_context` . `_context` can be only one of the following:         |                                                                         |
| `context`                                                                     | `string` Required. Text to be summarized.                               |
| Union field `_instruction` . `_instruction` can be only one of the following: |                                                                         |
| `instruction`                                                                 | `string` Optional. Summarization prompt for LLM.                        |

### SummarizationVerbosityInput

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

| Fields       |                                                                                                                                                                                                                                                            |
|--------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `metricSpec` | `object ( `[`SummarizationVerbositySpec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.SummarizationVerbositySpec)` )` Required. Spec for summarization verbosity score metric. |
| `instance`   | `object ( `[`SummarizationVerbosityInstance`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.SummarizationVerbosityInstance)` )` Required. Summarization verbosity instance.      |

### SummarizationVerbositySpec

**JSON representation**

```
{
  "useReference": boolean,
  "version": integer
}
```

| Fields         |                                                                                           |
|----------------|-------------------------------------------------------------------------------------------|
| `useReference` | `boolean` Optional. Whether to use instance.reference to compute summarization verbosity. |
| `version`      | `integer` Optional. Which version to use for evaluation.                                  |

### SummarizationVerbosityInstance

**JSON representation**

```
{

  // Union field _prediction can be only one of the following:
  "prediction": string
  // End of list of possible types for union field _prediction.

  // Union field _reference can be only one of the following:
  "reference": string
  // End of list of possible types for union field _reference.

  // Union field _context can be only one of the following:
  "context": string
  // End of list of possible types for union field _context.

  // Union field _instruction can be only one of the following:
  "instruction": string
  // End of list of possible types for union field _instruction.
}
```

| Fields                                                                        |                                                                         |
|-------------------------------------------------------------------------------|-------------------------------------------------------------------------|
| Union field `_prediction` . `_prediction` can be only one of the following:   |                                                                         |
| `prediction`                                                                  | `string` Required. Output of the evaluated model.                       |
| Union field `_reference` . `_reference` can be only one of the following:     |                                                                         |
| `reference`                                                                   | `string` Optional. Ground truth used to compare against the prediction. |
| Union field `_context` . `_context` can be only one of the following:         |                                                                         |
| `context`                                                                     | `string` Required. Text to be summarized.                               |
| Union field `_instruction` . `_instruction` can be only one of the following: |                                                                         |
| `instruction`                                                                 | `string` Optional. Summarization prompt for LLM.                        |

### QuestionAnsweringQualityInput

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

| Fields       |                                                                                                                                                                                                                                                                   |
|--------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `metricSpec` | `object ( `[`QuestionAnsweringQualitySpec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.QuestionAnsweringQualitySpec)` )` Required. Spec for question answering quality score metric. |
| `instance`   | `object ( `[`QuestionAnsweringQualityInstance`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.QuestionAnsweringQualityInstance)` )` Required. Question answering quality instance.      |

### QuestionAnsweringQualitySpec

**JSON representation**

```
{
  "useReference": boolean,
  "version": integer
}
```

| Fields         |                                                                                              |
|----------------|----------------------------------------------------------------------------------------------|
| `useReference` | `boolean` Optional. Whether to use instance.reference to compute question answering quality. |
| `version`      | `integer` Optional. Which version to use for evaluation.                                     |

### QuestionAnsweringQualityInstance

**JSON representation**

```
{

  // Union field _prediction can be only one of the following:
  "prediction": string
  // End of list of possible types for union field _prediction.

  // Union field _reference can be only one of the following:
  "reference": string
  // End of list of possible types for union field _reference.

  // Union field _context can be only one of the following:
  "context": string
  // End of list of possible types for union field _context.

  // Union field _instruction can be only one of the following:
  "instruction": string
  // End of list of possible types for union field _instruction.
}
```

| Fields                                                                        |                                                                         |
|-------------------------------------------------------------------------------|-------------------------------------------------------------------------|
| Union field `_prediction` . `_prediction` can be only one of the following:   |                                                                         |
| `prediction`                                                                  | `string` Required. Output of the evaluated model.                       |
| Union field `_reference` . `_reference` can be only one of the following:     |                                                                         |
| `reference`                                                                   | `string` Optional. Ground truth used to compare against the prediction. |
| Union field `_context` . `_context` can be only one of the following:         |                                                                         |
| `context`                                                                     | `string` Required. Text to answer the question.                         |
| Union field `_instruction` . `_instruction` can be only one of the following: |                                                                         |
| `instruction`                                                                 | `string` Required. Question Answering prompt for LLM.                   |

### PairwiseQuestionAnsweringQualityInput

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

| Fields       |                                                                                                                                                                                                                                                                                            |
|--------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `metricSpec` | `object ( `[`PairwiseQuestionAnsweringQualitySpec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.PairwiseQuestionAnsweringQualitySpec)` )` Required. Spec for pairwise question answering quality score metric. |
| `instance`   | `object ( `[`PairwiseQuestionAnsweringQualityInstance`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.PairwiseQuestionAnsweringQualityInstance)` )` Required. Pairwise question answering quality instance.      |

### PairwiseQuestionAnsweringQualitySpec

**JSON representation**

```
{
  "useReference": boolean,
  "version": integer
}
```

| Fields         |                                                                                              |
|----------------|----------------------------------------------------------------------------------------------|
| `useReference` | `boolean` Optional. Whether to use instance.reference to compute question answering quality. |
| `version`      | `integer` Optional. Which version to use for evaluation.                                     |

### PairwiseQuestionAnsweringQualityInstance

**JSON representation**

```
{

  // Union field _prediction can be only one of the following:
  "prediction": string
  // End of list of possible types for union field _prediction.

  // Union field _baseline_prediction can be only one of the following:
  "baselinePrediction": string
  // End of list of possible types for union field _baseline_prediction.

  // Union field _reference can be only one of the following:
  "reference": string
  // End of list of possible types for union field _reference.

  // Union field _context can be only one of the following:
  "context": string
  // End of list of possible types for union field _context.

  // Union field _instruction can be only one of the following:
  "instruction": string
  // End of list of possible types for union field _instruction.
}
```

| Fields                                                                                        |                                                                         |
|-----------------------------------------------------------------------------------------------|-------------------------------------------------------------------------|
| Union field `_prediction` . `_prediction` can be only one of the following:                   |                                                                         |
| `prediction`                                                                                  | `string` Required. Output of the candidate model.                       |
| Union field `_baseline_prediction` . `_baseline_prediction` can be only one of the following: |                                                                         |
| `baselinePrediction`                                                                          | `string` Required. Output of the baseline model.                        |
| Union field `_reference` . `_reference` can be only one of the following:                     |                                                                         |
| `reference`                                                                                   | `string` Optional. Ground truth used to compare against the prediction. |
| Union field `_context` . `_context` can be only one of the following:                         |                                                                         |
| `context`                                                                                     | `string` Required. Text to answer the question.                         |
| Union field `_instruction` . `_instruction` can be only one of the following:                 |                                                                         |
| `instruction`                                                                                 | `string` Required. Question Answering prompt for LLM.                   |

### QuestionAnsweringRelevanceInput

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

| Fields       |                                                                                                                                                                                                                                                                         |
|--------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `metricSpec` | `object ( `[`QuestionAnsweringRelevanceSpec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.QuestionAnsweringRelevanceSpec)` )` Required. Spec for question answering relevance score metric. |
| `instance`   | `object ( `[`QuestionAnsweringRelevanceInstance`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.QuestionAnsweringRelevanceInstance)` )` Required. Question answering relevance instance.      |

### QuestionAnsweringRelevanceSpec

**JSON representation**

```
{
  "useReference": boolean,
  "version": integer
}
```

| Fields         |                                                                                                |
|----------------|------------------------------------------------------------------------------------------------|
| `useReference` | `boolean` Optional. Whether to use instance.reference to compute question answering relevance. |
| `version`      | `integer` Optional. Which version to use for evaluation.                                       |

### QuestionAnsweringRelevanceInstance

**JSON representation**

```
{

  // Union field _prediction can be only one of the following:
  "prediction": string
  // End of list of possible types for union field _prediction.

  // Union field _reference can be only one of the following:
  "reference": string
  // End of list of possible types for union field _reference.

  // Union field _context can be only one of the following:
  "context": string
  // End of list of possible types for union field _context.

  // Union field _instruction can be only one of the following:
  "instruction": string
  // End of list of possible types for union field _instruction.
}
```

| Fields                                                                        |                                                                                      |
|-------------------------------------------------------------------------------|--------------------------------------------------------------------------------------|
| Union field `_prediction` . `_prediction` can be only one of the following:   |                                                                                      |
| `prediction`                                                                  | `string` Required. Output of the evaluated model.                                    |
| Union field `_reference` . `_reference` can be only one of the following:     |                                                                                      |
| `reference`                                                                   | `string` Optional. Ground truth used to compare against the prediction.              |
| Union field `_context` . `_context` can be only one of the following:         |                                                                                      |
| `context`                                                                     | `string` Optional. Text provided as context to answer the question.                  |
| Union field `_instruction` . `_instruction` can be only one of the following: |                                                                                      |
| `instruction`                                                                 | `string` Required. The question asked and other instruction in the inference prompt. |

### QuestionAnsweringHelpfulnessInput

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

| Fields       |                                                                                                                                                                                                                                                                               |
|--------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `metricSpec` | `object ( `[`QuestionAnsweringHelpfulnessSpec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.QuestionAnsweringHelpfulnessSpec)` )` Required. Spec for question answering helpfulness score metric. |
| `instance`   | `object ( `[`QuestionAnsweringHelpfulnessInstance`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.QuestionAnsweringHelpfulnessInstance)` )` Required. Question answering helpfulness instance.      |

### QuestionAnsweringHelpfulnessSpec

**JSON representation**

```
{
  "useReference": boolean,
  "version": integer
}
```

| Fields         |                                                                                                  |
|----------------|--------------------------------------------------------------------------------------------------|
| `useReference` | `boolean` Optional. Whether to use instance.reference to compute question answering helpfulness. |
| `version`      | `integer` Optional. Which version to use for evaluation.                                         |

### QuestionAnsweringHelpfulnessInstance

**JSON representation**

```
{

  // Union field _prediction can be only one of the following:
  "prediction": string
  // End of list of possible types for union field _prediction.

  // Union field _reference can be only one of the following:
  "reference": string
  // End of list of possible types for union field _reference.

  // Union field _context can be only one of the following:
  "context": string
  // End of list of possible types for union field _context.

  // Union field _instruction can be only one of the following:
  "instruction": string
  // End of list of possible types for union field _instruction.
}
```

| Fields                                                                        |                                                                                      |
|-------------------------------------------------------------------------------|--------------------------------------------------------------------------------------|
| Union field `_prediction` . `_prediction` can be only one of the following:   |                                                                                      |
| `prediction`                                                                  | `string` Required. Output of the evaluated model.                                    |
| Union field `_reference` . `_reference` can be only one of the following:     |                                                                                      |
| `reference`                                                                   | `string` Optional. Ground truth used to compare against the prediction.              |
| Union field `_context` . `_context` can be only one of the following:         |                                                                                      |
| `context`                                                                     | `string` Optional. Text provided as context to answer the question.                  |
| Union field `_instruction` . `_instruction` can be only one of the following: |                                                                                      |
| `instruction`                                                                 | `string` Required. The question asked and other instruction in the inference prompt. |

### QuestionAnsweringCorrectnessInput

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

| Fields       |                                                                                                                                                                                                                                                                               |
|--------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `metricSpec` | `object ( `[`QuestionAnsweringCorrectnessSpec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.QuestionAnsweringCorrectnessSpec)` )` Required. Spec for question answering correctness score metric. |
| `instance`   | `object ( `[`QuestionAnsweringCorrectnessInstance`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.QuestionAnsweringCorrectnessInstance)` )` Required. Question answering correctness instance.      |

### QuestionAnsweringCorrectnessSpec

**JSON representation**

```
{
  "useReference": boolean,
  "version": integer
}
```

| Fields         |                                                                                                  |
|----------------|--------------------------------------------------------------------------------------------------|
| `useReference` | `boolean` Optional. Whether to use instance.reference to compute question answering correctness. |
| `version`      | `integer` Optional. Which version to use for evaluation.                                         |

### QuestionAnsweringCorrectnessInstance

**JSON representation**

```
{

  // Union field _prediction can be only one of the following:
  "prediction": string
  // End of list of possible types for union field _prediction.

  // Union field _reference can be only one of the following:
  "reference": string
  // End of list of possible types for union field _reference.

  // Union field _context can be only one of the following:
  "context": string
  // End of list of possible types for union field _context.

  // Union field _instruction can be only one of the following:
  "instruction": string
  // End of list of possible types for union field _instruction.
}
```

| Fields                                                                        |                                                                                      |
|-------------------------------------------------------------------------------|--------------------------------------------------------------------------------------|
| Union field `_prediction` . `_prediction` can be only one of the following:   |                                                                                      |
| `prediction`                                                                  | `string` Required. Output of the evaluated model.                                    |
| Union field `_reference` . `_reference` can be only one of the following:     |                                                                                      |
| `reference`                                                                   | `string` Optional. Ground truth used to compare against the prediction.              |
| Union field `_context` . `_context` can be only one of the following:         |                                                                                      |
| `context`                                                                     | `string` Optional. Text provided as context to answer the question.                  |
| Union field `_instruction` . `_instruction` can be only one of the following: |                                                                                      |
| `instruction`                                                                 | `string` Required. The question asked and other instruction in the inference prompt. |

### PointwiseMetricInput

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

| Fields       |                                                                                                                                                                                                                                  |
|--------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `metricSpec` | `object ( `[`PointwiseMetricSpec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.PointwiseMetricSpec)` )` Required. Spec for pointwise metric.         |
| `instance`   | `object ( `[`PointwiseMetricInstance`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.PointwiseMetricInstance)` )` Required. Pointwise metric instance. |

### PointwiseMetricSpec

**JSON representation**

```
{
  "customOutputFormatConfig": {
    object (CustomOutputFormatConfig)
  },

  // Union field _metric_prompt_template can be only one of the following:
  "metricPromptTemplate": string
  // End of list of possible types for union field _metric_prompt_template.

  // Union field _system_instruction can be only one of the following:
  "systemInstruction": string
  // End of list of possible types for union field _system_instruction.
}
```

| Fields                                                                                              |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
|-----------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `customOutputFormatConfig`                                                                          | `object ( `[`CustomOutputFormatConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.CustomOutputFormatConfig)` )` Optional. CustomOutputFormatConfig allows customization of metric output. By default, metrics return a score and explanation. When this config is set, the default output is replaced with either: - The raw output string. - A parsed output based on a user-defined schema. If a custom format is chosen, the `score` and `explanation` fields in the corresponding metric result will be empty. |
| Union field `_metric_prompt_template` . `_metric_prompt_template` can be only one of the following: |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| `metricPromptTemplate`                                                                              | `string` Required. Metric prompt template for pointwise metric.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| Union field `_system_instruction` . `_system_instruction` can be only one of the following:         |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| `systemInstruction`                                                                                 | `string` Optional. System instructions for pointwise metric.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |

### CustomOutputFormatConfig

**JSON representation**

```
{

  // Union field custom_output_format_config can be only one of the following:
  "returnRawOutput": boolean
  // End of list of possible types for union field custom_output_format_config.
}
```

| Fields                                                                                                                                          |                                                   |
|-------------------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------|
| Union field `custom_output_format_config` . Custom output format configuration. `custom_output_format_config` can be only one of the following: |                                                   |
| `returnRawOutput`                                                                                                                               | `boolean` Optional. Whether to return raw output. |

### PointwiseMetricInstance

**JSON representation**

```
{

  // Union field instance can be only one of the following:
  "jsonInstance": string,
  "contentMapInstance": {
    object (ContentMap)
  }
  // End of list of possible types for union field instance.
}
```

| Fields                                                                                               |                                                                                                                                                                                                                                                                                                                                                                 |
|------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Union field `instance` . Instance for pointwise metric. `instance` can be only one of the following: |                                                                                                                                                                                                                                                                                                                                                                 |
| `jsonInstance`                                                                                       | `string` Instance specified as a json string. String key-value pairs are expected in the json_instance to render PointwiseMetricSpec.instance_prompt_template.                                                                                                                                                                                                  |
| `contentMapInstance`                                                                                 | `object ( `[`ContentMap`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.ContentMap)` )` Key-value contents for the mutlimodality input, including text, image, video, audio, and pdf, etc. The key is placeholder in metric prompt template, and the value is the multimodal content. |

### ContentMap

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

| Fields   |                                                                                                                                                                                                                                                                                                                                                         |
|----------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `values` | `map (key: string, value: object ( `[`Contents`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.Contents)` ))` Optional. Map of placeholder to contents. An object containing a list of `"key": value` pairs. Example: `{ "name": "wrench", "mass": "1.3kg", "count": "3" }` . |

### ValuesEntry

**JSON representation**

```
{
  "key": string,
  "value": {
    object (Contents)
  }
}
```

| Fields  |                                                                                                                                                               |
|---------|---------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `key`   | `string`                                                                                                                                                      |
| `value` | `object ( `[`Contents`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.Contents)` )` |

### Contents

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

| Fields       |                                                                                                                                                                                          |
|--------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `contents[]` | `object ( `[`Content`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.Content)` )` Optional. Repeated contents. |

### Content

**JSON representation**

```
{
  "role": string,
  "parts": [
    {
      object (Part)
    }
  ]
}
```

| Fields    |                                                                                                                                                                                                                                                                                                                               |
|-----------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `role`    | `string` Optional. The producer of the content. Must be either 'user' or 'model'. If not set, the service will default to 'user'.                                                                                                                                                                                             |
| `parts[]` | `object ( `[`Part`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.Part)` )` Required. A list of `Part` objects that make up a single message. Parts of a message can have different MIME types. A `Content` message must have at least one `Part` . |

### Part

**JSON representation**

```
{
  "thought": boolean,
  "thoughtSignature": string,
  "mediaResolution": {
    object (MediaResolution)
  },
  "audioTranscription": {
    object (AudioTranscription)
  },

  // Union field data can be only one of the following:
  "text": string,
  "inlineData": {
    object (Blob)
  },
  "fileData": {
    object (FileData)
  },
  "functionCall": {
    object (FunctionCall)
  },
  "functionResponse": {
    object (FunctionResponse)
  },
  "executableCode": {
    object (ExecutableCode)
  },
  "codeExecutionResult": {
    object (CodeExecutionResult)
  }
  // End of list of possible types for union field data.

  // Union field metadata can be only one of the following:
  "videoMetadata": {
    object (VideoMetadata)
  }
  // End of list of possible types for union field metadata.
}
```

| Fields                                                                |                                                                                                                                                                                                                                                                                                                              |
|-----------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `thought`                                                             | `boolean` Optional. Indicates whether the `part` represents the model's thought process or reasoning.                                                                                                                                                                                                                        |
| `thoughtSignature`                                                    | `string ( `[`bytes`](https://developers.google.com/discovery/v1/type-format)` format)` Optional. An opaque signature for the thought so it can be reused in subsequent requests. A base64-encoded string.                                                                                                                    |
| `mediaResolution`                                                     | `object ( `[`MediaResolution`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.MediaResolution)` )` per part media resolution. Media resolution for the input media.                                                                                 |
| `audioTranscription`                                                  | `object ( `[`AudioTranscription`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.AudioTranscription)` )` Optional. Audio (input or output) transcription. This is only set when this Part contains audio data.                                      |
| Union field `data` . `data` can be only one of the following:         |                                                                                                                                                                                                                                                                                                                              |
| `text`                                                                | `string` Optional. The text content of the part. When sent from the VSCode Gemini Code Assist extension, references to @mentioned items will be converted to markdown boldface text. For example `@my-repo` will be converted to and sent as `**my-repo**` by the IDE agent.                                                 |
| `inlineData`                                                          | `object ( `[`Blob`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.Blob)` )` Optional. The inline data content of the part. This can be used to include images, audio, or video in a request.                                                       |
| `fileData`                                                            | `object ( `[`FileData`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.FileData)` )` Optional. The URI-based data of the part. This can be used to include files from Google Cloud Storage.                                                         |
| `functionCall`                                                        | `object ( `[`FunctionCall`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.FunctionCall)` )` Optional. A predicted function call returned from the model. This contains the name of the function to call and the arguments to pass to the function. |
| `functionResponse`                                                    | `object ( `[`FunctionResponse`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.FunctionResponse)` )` Optional. The result of a function call. This is used to provide the model with the result of a function call that it predicted.               |
| `executableCode`                                                      | `object ( `[`ExecutableCode`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.ExecutableCode)` )` Optional. Code generated by the model that is intended to be executed.                                                                             |
| `codeExecutionResult`                                                 | `object ( `[`CodeExecutionResult`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.CodeExecutionResult)` )` Optional. The result of executing the `ExecutableCode` .                                                                                 |
| Union field `metadata` . `metadata` can be only one of the following: |                                                                                                                                                                                                                                                                                                                              |
| `videoMetadata`                                                       | `object ( `[`VideoMetadata`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.VideoMetadata)` )` Optional. Video metadata. The metadata should only be specified while the video data is presented in inline_data or file_data.                       |

### Blob

**JSON representation**

```
{
  "mimeType": string,
  "data": string,
  "displayName": string
}
```

| Fields        |                                                                                                                                                                                                                                                                                                                     |
|---------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `mimeType`    | `string` Required. The IANA standard MIME type of the source data.                                                                                                                                                                                                                                                  |
| `data`        | `string ( `[`bytes`](https://developers.google.com/discovery/v1/type-format)` format)` Required. The raw bytes of the data. A base64-encoded string.                                                                                                                                                                |
| `displayName` | `string` Optional. The display name of the blob. Used to provide a label or filename to distinguish blobs. This field is only returned in `PromptMessage` for prompt management. It is used in the Gemini calls only when server-side tools ( `code_execution` , `google_search` , and `url_context` ) are enabled. |

### FileData

**JSON representation**

```
{
  "mimeType": string,
  "fileUri": string,
  "displayName": string
}
```

| Fields        |                                                                                                                                                                                                                                                                                                                     |
|---------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `mimeType`    | `string` Required. The IANA standard MIME type of the source data.                                                                                                                                                                                                                                                  |
| `fileUri`     | `string` Required. The URI of the file in Google Cloud Storage.                                                                                                                                                                                                                                                     |
| `displayName` | `string` Optional. The display name of the file. Used to provide a label or filename to distinguish files. This field is only returned in `PromptMessage` for prompt management. It is used in the Gemini calls only when server side tools ( `code_execution` , `google_search` , and `url_context` ) are enabled. |

### FunctionCall

**JSON representation**

```
{
  "id": string,
  "name": string,
  "args": {
    object
  },
  "partialArgs": [
    {
      object (PartialArg)
    }
  ],
  "willContinue": boolean
}
```

| Fields          |                                                                                                                                                                                                                                                                                                            |
|-----------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `id`            | `string` Optional. The unique id of the function call. If populated, the client to execute the `function_call` and return the response with the matching `id` .                                                                                                                                            |
| `name`          | `string` Optional. The name of the function to call. Matches `FunctionDeclaration.name` .                                                                                                                                                                                                                  |
| `args`          | `object ( `[`Struct`](https://protobuf.dev/reference/protobuf/google.protobuf/#struct)` format)` Optional. The function parameters and values in JSON object format. See `FunctionDeclaration.parameters` for parameter details.                                                                           |
| `partialArgs[]` | `object ( `[`PartialArg`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.PartialArg)` )` Optional. The partial argument value of the function call. If provided, represents the arguments/fields that are streamed incrementally. |
| `willContinue`  | `boolean` Optional. Whether this is the last part of the FunctionCall. If true, another partial message for the current FunctionCall is expected to follow.                                                                                                                                                |

### Struct

**JSON representation**

```
{
  "fields": {
    string: value,
    ...
  }
}
```

| Fields   |                                                                                                                                                                                                                                                                                          |
|----------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `fields` | `map (key: string, value: value ( `[`Value`](https://protobuf.dev/reference/protobuf/google.protobuf/#value)` format))` Unordered map of dynamically typed values. An object containing a list of `"key": value` pairs. Example: `{ "name": "wrench", "mass": "1.3kg", "count": "3" }` . |

### FieldsEntry

**JSON representation**

```
{
  "key": string,
  "value": value
}
```

| Fields  |                                                                                               |
|---------|-----------------------------------------------------------------------------------------------|
| `key`   | `string`                                                                                      |
| `value` | `value ( `[`Value`](https://protobuf.dev/reference/protobuf/google.protobuf/#value)` format)` |

### Value

**JSON representation**

```
{

  // Union field kind can be only one of the following:
  "nullValue": null,
  "numberValue": number,
  "stringValue": string,
  "boolValue": boolean,
  "structValue": {
    object
  },
  "listValue": array
  // End of list of possible types for union field kind.
}
```

| Fields                                                                           |                                                                                                                                                                                                                                                |
|----------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Union field `kind` . The kind of value. `kind` can be only one of the following: |                                                                                                                                                                                                                                                |
| `nullValue`                                                                      | `null` Represents a JSON `null` .                                                                                                                                                                                                              |
| `numberValue`                                                                    | `number` Represents a JSON number. Must not be `NaN` , `Infinity` or `-Infinity` , since those are not supported in JSON. This also cannot represent large Int64 values, since JSON format generally does not support them in its number type. |
| `stringValue`                                                                    | `string` Represents a JSON string.                                                                                                                                                                                                             |
| `boolValue`                                                                      | `boolean` Represents a JSON boolean ( `true` or `false` literal in JSON).                                                                                                                                                                      |
| `structValue`                                                                    | `object ( `[`Struct`](https://protobuf.dev/reference/protobuf/google.protobuf/#struct)` format)` Represents a JSON object.                                                                                                                     |
| `listValue`                                                                      | `array ( `[`ListValue`](https://protobuf.dev/reference/protobuf/google.protobuf/#list-value)` format)` Represents a JSON array.                                                                                                                |

### ListValue

**JSON representation**

```
{
  "values": [
    value
  ]
}
```

| Fields     |                                                                                                                                           |
|------------|-------------------------------------------------------------------------------------------------------------------------------------------|
| `values[]` | `value ( `[`Value`](https://protobuf.dev/reference/protobuf/google.protobuf/#value)` format)` Repeated field of dynamically typed values. |

### PartialArg

**JSON representation**

```
{
  "jsonPath": string,
  "willContinue": boolean,

  // Union field delta can be only one of the following:
  "nullValue": null,
  "numberValue": number,
  "stringValue": string,
  "boolValue": boolean
  // End of list of possible types for union field delta.
}
```

| Fields                                                                                                   |                                                                                                                                                                   |
|----------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `jsonPath`                                                                                               | `string` Required. A JSON Path (RFC 9535) to the argument being streamed. <https://datatracker.ietf.org/doc/html/rfc9535> . e.g. "\$.foo.bar\[0\].data".          |
| `willContinue`                                                                                           | `boolean` Optional. Whether this is not the last part of the same json_path. If true, another PartialArg message for the current json_path is expected to follow. |
| Union field `delta` . The delta of field value being streamed. `delta` can be only one of the following: |                                                                                                                                                                   |
| `nullValue`                                                                                              | `null` Optional. Represents a null value.                                                                                                                         |
| `numberValue`                                                                                            | `number` Optional. Represents a double value.                                                                                                                     |
| `stringValue`                                                                                            | `string` Optional. Represents a string value.                                                                                                                     |
| `boolValue`                                                                                              | `boolean` Optional. Represents a boolean value.                                                                                                                   |

### FunctionResponse

**JSON representation**

```
{
  "id": string,
  "name": string,
  "response": {
    object
  },
  "parts": [
    {
      object (FunctionResponsePart)
    }
  ]
}
```

| Fields     |                                                                                                                                                                                                                                                                                                                                                             |
|------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `id`       | `string` Optional. The id of the function call this response is for. Populated by the client to match the corresponding function call `id` .                                                                                                                                                                                                                |
| `name`     | `string` Required. The name of the function to call. Matches `FunctionDeclaration.name` and `FunctionCall.name` .                                                                                                                                                                                                                                           |
| `response` | `object ( `[`Struct`](https://protobuf.dev/reference/protobuf/google.protobuf/#struct)` format)` Required. The function response in JSON object format. Use "output" key to specify function output and "error" key to specify error details (if any). If "output" and "error" keys are not specified, then whole "response" is treated as function output. |
| `parts[]`  | `object ( `[`FunctionResponsePart`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.FunctionResponsePart)` )` Optional. Ordered `Parts` that constitute a function response. Parts may have different IANA MIME types.                                                              |

### FunctionResponsePart

**JSON representation**

```
{

  // Union field data can be only one of the following:
  "inlineData": {
    object (FunctionResponseBlob)
  },
  "fileData": {
    object (FunctionResponseFileData)
  }
  // End of list of possible types for union field data.
}
```

| Fields                                                                                                |                                                                                                                                                                                                               |
|-------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Union field `data` . The data of the function response part. `data` can be only one of the following: |                                                                                                                                                                                                               |
| `inlineData`                                                                                          | `object ( `[`FunctionResponseBlob`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.FunctionResponseBlob)` )` Inline media bytes.     |
| `fileData`                                                                                            | `object ( `[`FunctionResponseFileData`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.FunctionResponseFileData)` )` URI based data. |

### FunctionResponseBlob

**JSON representation**

```
{
  "mimeType": string,
  "data": string,
  "displayName": string
}
```

| Fields        |                                                                                                                                                                                                                                                                                                                               |
|---------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `mimeType`    | `string` Required. The IANA standard MIME type of the source data.                                                                                                                                                                                                                                                            |
| `data`        | `string ( `[`bytes`](https://developers.google.com/discovery/v1/type-format)` format)` Required. Raw bytes. A base64-encoded string.                                                                                                                                                                                          |
| `displayName` | `string` Optional. Display name of the blob. Used to provide a label or filename to distinguish blobs. This field is only returned in PromptMessage for prompt management. It is currently used in the Gemini GenerateContent calls only when server side tools (code_execution, google_search, and url_context) are enabled. |

### FunctionResponseFileData

**JSON representation**

```
{
  "mimeType": string,
  "fileUri": string,
  "displayName": string
}
```

| Fields        |                                                                                                                                                                                                                                                                                                                                         |
|---------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `mimeType`    | `string` Required. The IANA standard MIME type of the source data.                                                                                                                                                                                                                                                                      |
| `fileUri`     | `string` Required. URI.                                                                                                                                                                                                                                                                                                                 |
| `displayName` | `string` Optional. Display name of the file data. Used to provide a label or filename to distinguish file datas. This field is only returned in PromptMessage for prompt management. It is currently used in the Gemini GenerateContent calls only when server side tools (code_execution, google_search, and url_context) are enabled. |

### ExecutableCode

**JSON representation**

```
{
  "language": enum (Language),
  "code": string,

  // Union field _id can be only one of the following:
  "id": string
  // End of list of possible types for union field _id.
}
```

| Fields                                                      |                                                                                                                                                                                                            |
|-------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `language`                                                  | `enum ( `[`Language`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.Language)` )` Required. Programming language of the `code` . |
| `code`                                                      | `string` Required. The code to be executed.                                                                                                                                                                |
| Union field `_id` . `_id` can be only one of the following: |                                                                                                                                                                                                            |
| `id`                                                        | `string` Optional. Unique identifier of the `ExecutableCode` part. The server returns the `CodeExecutionResult` with the matching `id` .                                                                   |

### CodeExecutionResult

**JSON representation**

```
{
  "outcome": enum (Outcome),
  "output": string,

  // Union field _id can be only one of the following:
  "id": string
  // End of list of possible types for union field _id.
}
```

| Fields                                                      |                                                                                                                                                                                                    |
|-------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `outcome`                                                   | `enum ( `[`Outcome`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.Outcome)` )` Required. Outcome of the code execution. |
| `output`                                                    | `string` Optional. Contains stdout when code execution is successful, stderr or other description otherwise.                                                                                       |
| Union field `_id` . `_id` can be only one of the following: |                                                                                                                                                                                                    |
| `id`                                                        | `string` Optional. The identifier of the `ExecutableCode` part this result is for. Only populated if the corresponding `ExecutableCode` has an id.                                                 |

### VideoMetadata

**JSON representation**

```
{
  "startOffset": string,
  "endOffset": string,
  "fps": number
}
```

| Fields        |                                                                                                                                                                                                                                                 |
|---------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `startOffset` | `string ( `[`Duration`](https://protobuf.dev/reference/protobuf/google.protobuf/#duration)` format)` Optional. The start offset of the video. A duration in seconds with up to nine fractional digits, ending with ' `s` '. Example: `"3.5s"` . |
| `endOffset`   | `string ( `[`Duration`](https://protobuf.dev/reference/protobuf/google.protobuf/#duration)` format)` Optional. The end offset of the video. A duration in seconds with up to nine fractional digits, ending with ' `s` '. Example: `"3.5s"` .   |
| `fps`         | `number` Optional. The frame rate of the video sent to the model. If not specified, the default value is 1.0. The valid range is (0.0, 24.0\].                                                                                                  |

### Duration

**JSON representation**

```
{
  "seconds": string,
  "nanos": integer
}
```

| Fields    |                                                                                                                                                                                                                                                                                                                                                                                          |
|-----------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `seconds` | `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)` Signed seconds of the span of time. Must be from -315,576,000,000 to +315,576,000,000 inclusive. Note: these bounds are computed from: 60 sec/min \* 60 min/hr \* 24 hr/day \* 365.25 days/year \* 10000 years                                                                                    |
| `nanos`   | `integer` Signed fractions of a second at nanosecond resolution of the span of time. Durations less than one second are represented with a 0 `seconds` field and a positive or negative `nanos` field. For durations of one second or more, a non-zero value for the `nanos` field must be of the same sign as the `seconds` field. Must be from -999,999,999 to +999,999,999 inclusive. |

### MediaResolution

**JSON representation**

```
{

  // Union field value can be only one of the following:
  "level": enum (Level)
  // End of list of possible types for union field value.
}
```

| Fields                                                          |                                                                                                                                                                                                      |
|-----------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Union field `value` . `value` can be only one of the following: |                                                                                                                                                                                                      |
| `level`                                                         | `enum ( `[`Level`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.Level)` )` The tokenization quality used for given media. |

### AudioTranscription

**JSON representation**

```
{
  "text": string,
  "speakerLabel": string,
  "words": [
    {
      object (WordInfo)
    }
  ]
}
```

| Fields         |                                                                                                                                                                                                                                                                    |
|----------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `text`         | `string` Required. The transcription text of this audio segment.                                                                                                                                                                                                   |
| `speakerLabel` | `string` Optional. A label identifying the speaker of this audio segment (e.g. "spk_1", "spk_2"). Present when diarization is set.                                                                                                                                 |
| `words[]`      | `object ( `[`WordInfo`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.WordInfo)` )` Optional. Detailed word-level transcriptions and timing details. Present when word_timestamp is set. |

### WordInfo

**JSON representation**

```
{
  "word": string,
  "startOffset": string,
  "endOffset": string
}
```

| Fields        |                                                                                                                                                                                                                                                                                       |
|---------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `word`        | `string` Required. Transcript of the word.                                                                                                                                                                                                                                            |
| `startOffset` | `string ( `[`Duration`](https://protobuf.dev/reference/protobuf/google.protobuf/#duration)` format)` Optional. Start offset in time of the word relative to the start of the audio. A duration in seconds with up to nine fractional digits, ending with ' `s` '. Example: `"3.5s"` . |
| `endOffset`   | `string ( `[`Duration`](https://protobuf.dev/reference/protobuf/google.protobuf/#duration)` format)` Optional. End offset in time of the word relative to the start of the audio. A duration in seconds with up to nine fractional digits, ending with ' `s` '. Example: `"3.5s"` .   |

### PairwiseMetricInput

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

| Fields       |                                                                                                                                                                                                                               |
|--------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `metricSpec` | `object ( `[`PairwiseMetricSpec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.PairwiseMetricSpec)` )` Required. Spec for pairwise metric.         |
| `instance`   | `object ( `[`PairwiseMetricInstance`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.PairwiseMetricInstance)` )` Required. Pairwise metric instance. |

### PairwiseMetricSpec

**JSON representation**

```
{
  "candidateResponseFieldName": string,
  "baselineResponseFieldName": string,
  "customOutputFormatConfig": {
    object (CustomOutputFormatConfig)
  },

  // Union field _metric_prompt_template can be only one of the following:
  "metricPromptTemplate": string
  // End of list of possible types for union field _metric_prompt_template.

  // Union field _system_instruction can be only one of the following:
  "systemInstruction": string
  // End of list of possible types for union field _system_instruction.
}
```

| Fields                                                                                              |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
|-----------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `candidateResponseFieldName`                                                                        | `string` Optional. The field name of the candidate response.                                                                                                                                                                                                                                                                                                                                                                                                                               |
| `baselineResponseFieldName`                                                                         | `string` Optional. The field name of the baseline response.                                                                                                                                                                                                                                                                                                                                                                                                                                |
| `customOutputFormatConfig`                                                                          | `object ( `[`CustomOutputFormatConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.CustomOutputFormatConfig)` )` Optional. CustomOutputFormatConfig allows customization of metric output. When this config is set, the default output is replaced with the raw output string. If a custom format is chosen, the `pairwise_choice` and `explanation` fields in the corresponding metric result will be empty. |
| Union field `_metric_prompt_template` . `_metric_prompt_template` can be only one of the following: |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| `metricPromptTemplate`                                                                              | `string` Required. Metric prompt template for pairwise metric.                                                                                                                                                                                                                                                                                                                                                                                                                             |
| Union field `_system_instruction` . `_system_instruction` can be only one of the following:         |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| `systemInstruction`                                                                                 | `string` Optional. System instructions for pairwise metric.                                                                                                                                                                                                                                                                                                                                                                                                                                |

### PairwiseMetricInstance

**JSON representation**

```
{

  // Union field instance can be only one of the following:
  "jsonInstance": string,
  "contentMapInstance": {
    object (ContentMap)
  }
  // End of list of possible types for union field instance.
}
```

| Fields                                                                                              |                                                                                                                                                                                                                                                                                                                                                                 |
|-----------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Union field `instance` . Instance for pairwise metric. `instance` can be only one of the following: |                                                                                                                                                                                                                                                                                                                                                                 |
| `jsonInstance`                                                                                      | `string` Instance specified as a json string. String key-value pairs are expected in the json_instance to render PairwiseMetricSpec.instance_prompt_template.                                                                                                                                                                                                   |
| `contentMapInstance`                                                                                | `object ( `[`ContentMap`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.ContentMap)` )` Key-value contents for the mutlimodality input, including text, image, video, audio, and pdf, etc. The key is placeholder in metric prompt template, and the value is the multimodal content. |

### ToolCallValidInput

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

| Fields        |                                                                                                                                                                                                                                       |
|---------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `metricSpec`  | `object ( ``ToolCallValidSpec`` )` Required. Spec for tool call valid metric.                                                                                                                                                         |
| `instances[]` | `object ( `[`ToolCallValidInstance`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.ToolCallValidInstance)` )` Required. Repeated tool call valid instances. |

### ToolCallValidInstance

**JSON representation**

```
{

  // Union field _prediction can be only one of the following:
  "prediction": string
  // End of list of possible types for union field _prediction.

  // Union field _reference can be only one of the following:
  "reference": string
  // End of list of possible types for union field _reference.
}
```

| Fields                                                                      |                                                                         |
|-----------------------------------------------------------------------------|-------------------------------------------------------------------------|
| Union field `_prediction` . `_prediction` can be only one of the following: |                                                                         |
| `prediction`                                                                | `string` Required. Output of the evaluated model.                       |
| Union field `_reference` . `_reference` can be only one of the following:   |                                                                         |
| `reference`                                                                 | `string` Required. Ground truth used to compare against the prediction. |

### ToolNameMatchInput

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

| Fields        |                                                                                                                                                                                                                                       |
|---------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `metricSpec`  | `object ( ``ToolNameMatchSpec`` )` Required. Spec for tool name match metric.                                                                                                                                                         |
| `instances[]` | `object ( `[`ToolNameMatchInstance`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.ToolNameMatchInstance)` )` Required. Repeated tool name match instances. |

### ToolNameMatchInstance

**JSON representation**

```
{

  // Union field _prediction can be only one of the following:
  "prediction": string
  // End of list of possible types for union field _prediction.

  // Union field _reference can be only one of the following:
  "reference": string
  // End of list of possible types for union field _reference.
}
```

| Fields                                                                      |                                                                         |
|-----------------------------------------------------------------------------|-------------------------------------------------------------------------|
| Union field `_prediction` . `_prediction` can be only one of the following: |                                                                         |
| `prediction`                                                                | `string` Required. Output of the evaluated model.                       |
| Union field `_reference` . `_reference` can be only one of the following:   |                                                                         |
| `reference`                                                                 | `string` Required. Ground truth used to compare against the prediction. |

### ToolParameterKeyMatchInput

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

| Fields        |                                                                                                                                                                                                                                                                |
|---------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `metricSpec`  | `object ( ``ToolParameterKeyMatchSpec`` )` Required. Spec for tool parameter key match metric.                                                                                                                                                                 |
| `instances[]` | `object ( `[`ToolParameterKeyMatchInstance`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.ToolParameterKeyMatchInstance)` )` Required. Repeated tool parameter key match instances. |

### ToolParameterKeyMatchInstance

**JSON representation**

```
{

  // Union field _prediction can be only one of the following:
  "prediction": string
  // End of list of possible types for union field _prediction.

  // Union field _reference can be only one of the following:
  "reference": string
  // End of list of possible types for union field _reference.
}
```

| Fields                                                                      |                                                                         |
|-----------------------------------------------------------------------------|-------------------------------------------------------------------------|
| Union field `_prediction` . `_prediction` can be only one of the following: |                                                                         |
| `prediction`                                                                | `string` Required. Output of the evaluated model.                       |
| Union field `_reference` . `_reference` can be only one of the following:   |                                                                         |
| `reference`                                                                 | `string` Required. Ground truth used to compare against the prediction. |

### ToolParameterKVMatchInput

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

| Fields        |                                                                                                                                                                                                                                                                    |
|---------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `metricSpec`  | `object ( `[`ToolParameterKVMatchSpec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.ToolParameterKVMatchSpec)` )` Required. Spec for tool parameter key value match metric.            |
| `instances[]` | `object ( `[`ToolParameterKVMatchInstance`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.ToolParameterKVMatchInstance)` )` Required. Repeated tool parameter key value match instances. |

### ToolParameterKVMatchSpec

**JSON representation**

```
{
  "useStrictStringMatch": boolean
}
```

| Fields                 |                                                                             |
|------------------------|-----------------------------------------------------------------------------|
| `useStrictStringMatch` | `boolean` Optional. Whether to use STRICT string match on parameter values. |

### ToolParameterKVMatchInstance

**JSON representation**

```
{

  // Union field _prediction can be only one of the following:
  "prediction": string
  // End of list of possible types for union field _prediction.

  // Union field _reference can be only one of the following:
  "reference": string
  // End of list of possible types for union field _reference.
}
```

| Fields                                                                      |                                                                         |
|-----------------------------------------------------------------------------|-------------------------------------------------------------------------|
| Union field `_prediction` . `_prediction` can be only one of the following: |                                                                         |
| `prediction`                                                                | `string` Required. Output of the evaluated model.                       |
| Union field `_reference` . `_reference` can be only one of the following:   |                                                                         |
| `reference`                                                                 | `string` Required. Ground truth used to compare against the prediction. |

### CometInput

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

| Fields       |                                                                                                                                                                                                   |
|--------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `metricSpec` | `object ( `[`CometSpec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.CometSpec)` )` Required. Spec for comet metric.  |
| `instance`   | `object ( `[`CometInstance`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.CometInstance)` )` Required. Comet instance. |

### CometSpec

**JSON representation**

```
{
  "sourceLanguage": string,
  "targetLanguage": string,

  // Union field _version can be only one of the following:
  "version": enum (CometVersion)
  // End of list of possible types for union field _version.
}
```

| Fields                                                                |                                                                                                                                                                                                                    |
|-----------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `sourceLanguage`                                                      | `string` Optional. Source language in BCP-47 format.                                                                                                                                                               |
| `targetLanguage`                                                      | `string` Optional. Target language in BCP-47 format. Covers both prediction and reference.                                                                                                                         |
| Union field `_version` . `_version` can be only one of the following: |                                                                                                                                                                                                                    |
| `version`                                                             | `enum ( `[`CometVersion`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.CometVersion)` )` Required. Which version to use for evaluation. |

### CometInstance

**JSON representation**

```
{

  // Union field _prediction can be only one of the following:
  "prediction": string
  // End of list of possible types for union field _prediction.

  // Union field _reference can be only one of the following:
  "reference": string
  // End of list of possible types for union field _reference.

  // Union field _source can be only one of the following:
  "source": string
  // End of list of possible types for union field _source.
}
```

| Fields                                                                      |                                                                         |
|-----------------------------------------------------------------------------|-------------------------------------------------------------------------|
| Union field `_prediction` . `_prediction` can be only one of the following: |                                                                         |
| `prediction`                                                                | `string` Required. Output of the evaluated model.                       |
| Union field `_reference` . `_reference` can be only one of the following:   |                                                                         |
| `reference`                                                                 | `string` Optional. Ground truth used to compare against the prediction. |
| Union field `_source` . `_source` can be only one of the following:         |                                                                         |
| `source`                                                                    | `string` Optional. Source text in original language.                    |

### MetricxInput

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

| Fields       |                                                                                                                                                                                                         |
|--------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `metricSpec` | `object ( `[`MetricxSpec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.MetricxSpec)` )` Required. Spec for Metricx metric.  |
| `instance`   | `object ( `[`MetricxInstance`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.MetricxInstance)` )` Required. Metricx instance. |

### MetricxSpec

**JSON representation**

```
{
  "sourceLanguage": string,
  "targetLanguage": string,

  // Union field _version can be only one of the following:
  "version": enum (MetricxVersion)
  // End of list of possible types for union field _version.
}
```

| Fields                                                                |                                                                                                                                                                                                                        |
|-----------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `sourceLanguage`                                                      | `string` Optional. Source language in BCP-47 format.                                                                                                                                                                   |
| `targetLanguage`                                                      | `string` Optional. Target language in BCP-47 format. Covers both prediction and reference.                                                                                                                             |
| Union field `_version` . `_version` can be only one of the following: |                                                                                                                                                                                                                        |
| `version`                                                             | `enum ( `[`MetricxVersion`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.MetricxVersion)` )` Required. Which version to use for evaluation. |

### MetricxInstance

**JSON representation**

```
{

  // Union field _prediction can be only one of the following:
  "prediction": string
  // End of list of possible types for union field _prediction.

  // Union field _reference can be only one of the following:
  "reference": string
  // End of list of possible types for union field _reference.

  // Union field _source can be only one of the following:
  "source": string
  // End of list of possible types for union field _source.
}
```

| Fields                                                                      |                                                                         |
|-----------------------------------------------------------------------------|-------------------------------------------------------------------------|
| Union field `_prediction` . `_prediction` can be only one of the following: |                                                                         |
| `prediction`                                                                | `string` Required. Output of the evaluated model.                       |
| Union field `_reference` . `_reference` can be only one of the following:   |                                                                         |
| `reference`                                                                 | `string` Optional. Ground truth used to compare against the prediction. |
| Union field `_source` . `_source` can be only one of the following:         |                                                                         |
| `source`                                                                    | `string` Optional. Source text in original language.                    |

### TrajectoryExactMatchInput

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

| Fields        |                                                                                                                                                                                                                                                         |
|---------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `metricSpec`  | `object ( ``TrajectoryExactMatchSpec`` )` Required. Spec for TrajectoryExactMatch metric.                                                                                                                                                               |
| `instances[]` | `object ( `[`TrajectoryExactMatchInstance`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.TrajectoryExactMatchInstance)` )` Required. Repeated TrajectoryExactMatch instance. |

### TrajectoryExactMatchInstance

**JSON representation**

```
{

  // Union field _predicted_trajectory can be only one of the following:
  "predictedTrajectory": {
    object (Trajectory)
  }
  // End of list of possible types for union field _predicted_trajectory.

  // Union field _reference_trajectory can be only one of the following:
  "referenceTrajectory": {
    object (Trajectory)
  }
  // End of list of possible types for union field _reference_trajectory.
}
```

| Fields                                                                                          |                                                                                                                                                                                                                      |
|-------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Union field `_predicted_trajectory` . `_predicted_trajectory` can be only one of the following: |                                                                                                                                                                                                                      |
| `predictedTrajectory`                                                                           | `object ( `[`Trajectory`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.Trajectory)` )` Required. Spec for predicted tool call trajectory. |
| Union field `_reference_trajectory` . `_reference_trajectory` can be only one of the following: |                                                                                                                                                                                                                      |
| `referenceTrajectory`                                                                           | `object ( `[`Trajectory`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.Trajectory)` )` Required. Spec for reference tool call trajectory. |

### Trajectory

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

| Fields        |                                                                                                                                                                                                       |
|---------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `toolCalls[]` | `object ( `[`ToolCall`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.ToolCall)` )` Required. Tool calls in the trajectory. |

### ToolCall

**JSON representation**

```
{

  // Union field _tool_name can be only one of the following:
  "toolName": string
  // End of list of possible types for union field _tool_name.

  // Union field _tool_input can be only one of the following:
  "toolInput": string
  // End of list of possible types for union field _tool_input.
}
```

| Fields                                                                      |                                        |
|-----------------------------------------------------------------------------|----------------------------------------|
| Union field `_tool_name` . `_tool_name` can be only one of the following:   |                                        |
| `toolName`                                                                  | `string` Required. Spec for tool name  |
| Union field `_tool_input` . `_tool_input` can be only one of the following: |                                        |
| `toolInput`                                                                 | `string` Optional. Spec for tool input |

### TrajectoryInOrderMatchInput

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

| Fields        |                                                                                                                                                                                                                                                               |
|---------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `metricSpec`  | `object ( ``TrajectoryInOrderMatchSpec`` )` Required. Spec for TrajectoryInOrderMatch metric.                                                                                                                                                                 |
| `instances[]` | `object ( `[`TrajectoryInOrderMatchInstance`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.TrajectoryInOrderMatchInstance)` )` Required. Repeated TrajectoryInOrderMatch instance. |

### TrajectoryInOrderMatchInstance

**JSON representation**

```
{

  // Union field _predicted_trajectory can be only one of the following:
  "predictedTrajectory": {
    object (Trajectory)
  }
  // End of list of possible types for union field _predicted_trajectory.

  // Union field _reference_trajectory can be only one of the following:
  "referenceTrajectory": {
    object (Trajectory)
  }
  // End of list of possible types for union field _reference_trajectory.
}
```

| Fields                                                                                          |                                                                                                                                                                                                                      |
|-------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Union field `_predicted_trajectory` . `_predicted_trajectory` can be only one of the following: |                                                                                                                                                                                                                      |
| `predictedTrajectory`                                                                           | `object ( `[`Trajectory`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.Trajectory)` )` Required. Spec for predicted tool call trajectory. |
| Union field `_reference_trajectory` . `_reference_trajectory` can be only one of the following: |                                                                                                                                                                                                                      |
| `referenceTrajectory`                                                                           | `object ( `[`Trajectory`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.Trajectory)` )` Required. Spec for reference tool call trajectory. |

### TrajectoryAnyOrderMatchInput

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

| Fields        |                                                                                                                                                                                                                                                                  |
|---------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `metricSpec`  | `object ( ``TrajectoryAnyOrderMatchSpec`` )` Required. Spec for TrajectoryAnyOrderMatch metric.                                                                                                                                                                  |
| `instances[]` | `object ( `[`TrajectoryAnyOrderMatchInstance`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.TrajectoryAnyOrderMatchInstance)` )` Required. Repeated TrajectoryAnyOrderMatch instance. |

### TrajectoryAnyOrderMatchInstance

**JSON representation**

```
{

  // Union field _predicted_trajectory can be only one of the following:
  "predictedTrajectory": {
    object (Trajectory)
  }
  // End of list of possible types for union field _predicted_trajectory.

  // Union field _reference_trajectory can be only one of the following:
  "referenceTrajectory": {
    object (Trajectory)
  }
  // End of list of possible types for union field _reference_trajectory.
}
```

| Fields                                                                                          |                                                                                                                                                                                                                      |
|-------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Union field `_predicted_trajectory` . `_predicted_trajectory` can be only one of the following: |                                                                                                                                                                                                                      |
| `predictedTrajectory`                                                                           | `object ( `[`Trajectory`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.Trajectory)` )` Required. Spec for predicted tool call trajectory. |
| Union field `_reference_trajectory` . `_reference_trajectory` can be only one of the following: |                                                                                                                                                                                                                      |
| `referenceTrajectory`                                                                           | `object ( `[`Trajectory`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.Trajectory)` )` Required. Spec for reference tool call trajectory. |

### TrajectoryPrecisionInput

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

| Fields        |                                                                                                                                                                                                                                                      |
|---------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `metricSpec`  | `object ( ``TrajectoryPrecisionSpec`` )` Required. Spec for TrajectoryPrecision metric.                                                                                                                                                              |
| `instances[]` | `object ( `[`TrajectoryPrecisionInstance`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.TrajectoryPrecisionInstance)` )` Required. Repeated TrajectoryPrecision instance. |

### TrajectoryPrecisionInstance

**JSON representation**

```
{

  // Union field _predicted_trajectory can be only one of the following:
  "predictedTrajectory": {
    object (Trajectory)
  }
  // End of list of possible types for union field _predicted_trajectory.

  // Union field _reference_trajectory can be only one of the following:
  "referenceTrajectory": {
    object (Trajectory)
  }
  // End of list of possible types for union field _reference_trajectory.
}
```

| Fields                                                                                          |                                                                                                                                                                                                                      |
|-------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Union field `_predicted_trajectory` . `_predicted_trajectory` can be only one of the following: |                                                                                                                                                                                                                      |
| `predictedTrajectory`                                                                           | `object ( `[`Trajectory`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.Trajectory)` )` Required. Spec for predicted tool call trajectory. |
| Union field `_reference_trajectory` . `_reference_trajectory` can be only one of the following: |                                                                                                                                                                                                                      |
| `referenceTrajectory`                                                                           | `object ( `[`Trajectory`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.Trajectory)` )` Required. Spec for reference tool call trajectory. |

### TrajectoryRecallInput

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

| Fields        |                                                                                                                                                                                                                                             |
|---------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `metricSpec`  | `object ( ``TrajectoryRecallSpec`` )` Required. Spec for TrajectoryRecall metric.                                                                                                                                                           |
| `instances[]` | `object ( `[`TrajectoryRecallInstance`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.TrajectoryRecallInstance)` )` Required. Repeated TrajectoryRecall instance. |

### TrajectoryRecallInstance

**JSON representation**

```
{

  // Union field _predicted_trajectory can be only one of the following:
  "predictedTrajectory": {
    object (Trajectory)
  }
  // End of list of possible types for union field _predicted_trajectory.

  // Union field _reference_trajectory can be only one of the following:
  "referenceTrajectory": {
    object (Trajectory)
  }
  // End of list of possible types for union field _reference_trajectory.
}
```

| Fields                                                                                          |                                                                                                                                                                                                                      |
|-------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Union field `_predicted_trajectory` . `_predicted_trajectory` can be only one of the following: |                                                                                                                                                                                                                      |
| `predictedTrajectory`                                                                           | `object ( `[`Trajectory`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.Trajectory)` )` Required. Spec for predicted tool call trajectory. |
| Union field `_reference_trajectory` . `_reference_trajectory` can be only one of the following: |                                                                                                                                                                                                                      |
| `referenceTrajectory`                                                                           | `object ( `[`Trajectory`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.Trajectory)` )` Required. Spec for reference tool call trajectory. |

### TrajectorySingleToolUseInput

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

| Fields        |                                                                                                                                                                                                                                                                  |
|---------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `metricSpec`  | `object ( `[`TrajectorySingleToolUseSpec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.TrajectorySingleToolUseSpec)` )` Required. Spec for TrajectorySingleToolUse metric.           |
| `instances[]` | `object ( `[`TrajectorySingleToolUseInstance`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.TrajectorySingleToolUseInstance)` )` Required. Repeated TrajectorySingleToolUse instance. |

### TrajectorySingleToolUseSpec

**JSON representation**

```
{

  // Union field _tool_name can be only one of the following:
  "toolName": string
  // End of list of possible types for union field _tool_name.
}
```

| Fields                                                                    |                                                                                      |
|---------------------------------------------------------------------------|--------------------------------------------------------------------------------------|
| Union field `_tool_name` . `_tool_name` can be only one of the following: |                                                                                      |
| `toolName`                                                                | `string` Required. Spec for tool name to be checked for in the predicted trajectory. |

### TrajectorySingleToolUseInstance

**JSON representation**

```
{

  // Union field _predicted_trajectory can be only one of the following:
  "predictedTrajectory": {
    object (Trajectory)
  }
  // End of list of possible types for union field _predicted_trajectory.
}
```

| Fields                                                                                          |                                                                                                                                                                                                                      |
|-------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Union field `_predicted_trajectory` . `_predicted_trajectory` can be only one of the following: |                                                                                                                                                                                                                      |
| `predictedTrajectory`                                                                           | `object ( `[`Trajectory`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.Trajectory)` )` Required. Spec for predicted tool call trajectory. |

### RubricBasedInstructionFollowingInput

**JSON representation**

```
{
  "metricSpec": {
    object (RubricBasedInstructionFollowingSpec)
  },
  "instance": {
    object (RubricBasedInstructionFollowingInstance)
  }
}
```

| Fields       |                                                                                                                                                                                                                                                                                            |
|--------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `metricSpec` | `object ( ``RubricBasedInstructionFollowingSpec`` )` Required. Spec for RubricBasedInstructionFollowing metric.                                                                                                                                                                            |
| `instance`   | `object ( `[`RubricBasedInstructionFollowingInstance`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.RubricBasedInstructionFollowingInstance)` )` Required. Instance for RubricBasedInstructionFollowing metric. |

### RubricBasedInstructionFollowingInstance

**JSON representation**

```
{

  // Union field instance can be only one of the following:
  "jsonInstance": string
  // End of list of possible types for union field instance.
}
```

| Fields                                                                                                                     |                                                                                                                                                                              |
|----------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Union field `instance` . Instance for RubricBasedInstructionFollowing metric. `instance` can be only one of the following: |                                                                                                                                                                              |
| `jsonInstance`                                                                                                             | `string` Required. Instance specified as a json string. String key-value pairs are expected in the json_instance to render RubricBasedInstructionFollowing prompt templates. |

### Metric

**JSON representation**

```
{
  "aggregationMetrics": [
    enum (AggregationMetric)
  ],
  "metadata": {
    object (MetricMetadata)
  },

  // Union field metric_spec can be only one of the following:
  "predefinedMetricSpec": {
    object (PredefinedMetricSpec)
  },
  "computationBasedMetricSpec": {
    object (ComputationBasedMetricSpec)
  },
  "llmBasedMetricSpec": {
    object (LLMBasedMetricSpec)
  },
  "customCodeExecutionSpec": {
    object (CustomCodeExecutionSpec)
  },
  "pointwiseMetricSpec": {
    object (PointwiseMetricSpec)
  },
  "pairwiseMetricSpec": {
    object (PairwiseMetricSpec)
  },
  "exactMatchSpec": {
    object (ExactMatchSpec)
  },
  "bleuSpec": {
    object (BleuSpec)
  },
  "rougeSpec": {
    object (RougeSpec)
  }
  // End of list of possible types for union field metric_spec.
}
```

| Fields                                                                                                                                                                 |                                                                                                                                                                                                                                                         |
|------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `aggregationMetrics[]`                                                                                                                                                 | `enum ( `[`AggregationMetric`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.AggregationMetric)` )` Optional. The aggregation metrics to use.                                 |
| `metadata`                                                                                                                                                             | `object ( `[`MetricMetadata`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.MetricMetadata)` )` Optional. Metadata about the metric, used for visualization and organization. |
| Union field `metric_spec` . The spec for the metric. It would be either a pre-defined metric, or a inline metric spec. `metric_spec` can be only one of the following: |                                                                                                                                                                                                                                                         |
| `predefinedMetricSpec`                                                                                                                                                 | `object ( `[`PredefinedMetricSpec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.PredefinedMetricSpec)` )` The spec for a pre-defined metric.                                |
| `computationBasedMetricSpec`                                                                                                                                           | `object ( `[`ComputationBasedMetricSpec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.ComputationBasedMetricSpec)` )` Spec for a computation based metric.                  |
| `llmBasedMetricSpec`                                                                                                                                                   | `object ( `[`LLMBasedMetricSpec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.LLMBasedMetricSpec)` )` Spec for an LLM based metric.                                         |
| `customCodeExecutionSpec`                                                                                                                                              | `object ( `[`CustomCodeExecutionSpec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.CustomCodeExecutionSpec)` )` Spec for Custom Code Execution metric.                      |
| `pointwiseMetricSpec`                                                                                                                                                  | `object ( `[`PointwiseMetricSpec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.PointwiseMetricSpec)` )` Spec for pointwise metric.                                          |
| `pairwiseMetricSpec`                                                                                                                                                   | `object ( `[`PairwiseMetricSpec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.PairwiseMetricSpec)` )` Spec for pairwise metric.                                             |
| `exactMatchSpec`                                                                                                                                                       | `object ( ``ExactMatchSpec`` )` Spec for exact match metric.                                                                                                                                                                                            |
| `bleuSpec`                                                                                                                                                             | `object ( `[`BleuSpec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.BleuSpec)` )` Spec for bleu metric.                                                                     |
| `rougeSpec`                                                                                                                                                            | `object ( `[`RougeSpec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.RougeSpec)` )` Spec for rouge metric.                                                                  |

### PredefinedMetricSpec

**JSON representation**

```
{
  "metricSpecName": string,
  "metricSpecParameters": {
    object
  }
}
```

| Fields                 |                                                                                                                                                                 |
|------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `metricSpecName`       | `string` Required. The name of a pre-defined metric, such as "instruction_following_v1" or "text_quality_v1".                                                   |
| `metricSpecParameters` | `object ( `[`Struct`](https://protobuf.dev/reference/protobuf/google.protobuf/#struct)` format)` Optional. The parameters needed to run the pre-defined metric. |

### ComputationBasedMetricSpec

**JSON representation**

```
{

  // Union field _type can be only one of the following:
  "type": enum (ComputationBasedMetricType)
  // End of list of possible types for union field _type.

  // Union field _parameters can be only one of the following:
  "parameters": {
    object
  }
  // End of list of possible types for union field _parameters.
}
```

| Fields                                                                      |                                                                                                                                                                                                                                                     |
|-----------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Union field `_type` . `_type` can be only one of the following:             |                                                                                                                                                                                                                                                     |
| `type`                                                                      | `enum ( `[`ComputationBasedMetricType`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.ComputationBasedMetricType)` )` Required. The type of the computation based metric. |
| Union field `_parameters` . `_parameters` can be only one of the following: |                                                                                                                                                                                                                                                     |
| `parameters`                                                                | `object ( `[`Struct`](https://protobuf.dev/reference/protobuf/google.protobuf/#struct)` format)` Optional. A map of parameters for the metric, e.g. {"rouge_type": "rougeL"}.                                                                       |

### LLMBasedMetricSpec

**JSON representation**

```
{
  "resultParserConfig": {
    object (EvaluationParserConfig)
  },

  // Union field rubrics_source can be only one of the following:
  "rubricGroupKey": string,
  "rubricGenerationSpec": {
    object (RubricGenerationSpec)
  },
  "predefinedRubricGenerationSpec": {
    object (PredefinedMetricSpec)
  }
  // End of list of possible types for union field rubrics_source.

  // Union field _metric_prompt_template can be only one of the following:
  "metricPromptTemplate": string
  // End of list of possible types for union field _metric_prompt_template.

  // Union field _system_instruction can be only one of the following:
  "systemInstruction": string
  // End of list of possible types for union field _system_instruction.

  // Union field _judge_autorater_config can be only one of the following:
  "judgeAutoraterConfig": {
    object (AutoraterConfig)
  }
  // End of list of possible types for union field _judge_autorater_config.

  // Union field _additional_config can be only one of the following:
  "additionalConfig": {
    object
  }
  // End of list of possible types for union field _additional_config.
}
```

| Fields                                                                                                                             |                                                                                                                                                                                                                                              |
|------------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `resultParserConfig`                                                                                                               | `object ( `[`EvaluationParserConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.EvaluationParserConfig)` )` Optional. The parser config for the metric result. |
| Union field `rubrics_source` . Source of the rubrics to be used for evaluation. `rubrics_source` can be only one of the following: |                                                                                                                                                                                                                                              |
| `rubricGroupKey`                                                                                                                   | `string` Use a pre-defined group of rubrics associated with the input. Refers to a key in the rubric_groups map of EvaluationInstance.                                                                                                       |
| `rubricGenerationSpec`                                                                                                             | `object ( `[`RubricGenerationSpec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.RubricGenerationSpec)` )` Dynamically generate rubrics using this specification. |
| `predefinedRubricGenerationSpec`                                                                                                   | `object ( `[`PredefinedMetricSpec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.PredefinedMetricSpec)` )` Dynamically generate rubrics using a predefined spec.  |
| Union field `_metric_prompt_template` . `_metric_prompt_template` can be only one of the following:                                |                                                                                                                                                                                                                                              |
| `metricPromptTemplate`                                                                                                             | `string` Required. Template for the prompt sent to the judge model.                                                                                                                                                                          |
| Union field `_system_instruction` . `_system_instruction` can be only one of the following:                                        |                                                                                                                                                                                                                                              |
| `systemInstruction`                                                                                                                | `string` Optional. System instructions for the judge model.                                                                                                                                                                                  |
| Union field `_judge_autorater_config` . `_judge_autorater_config` can be only one of the following:                                |                                                                                                                                                                                                                                              |
| `judgeAutoraterConfig`                                                                                                             | `object ( `[`AutoraterConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.AutoraterConfig)` )` Optional. Optional configuration for the judge LLM (Autorater).  |
| Union field `_additional_config` . `_additional_config` can be only one of the following:                                          |                                                                                                                                                                                                                                              |
| `additionalConfig`                                                                                                                 | `object ( `[`Struct`](https://protobuf.dev/reference/protobuf/google.protobuf/#struct)` format)` Optional. Optional additional configuration for the metric.                                                                                 |

### RubricGenerationSpec

**JSON representation**

```
{
  "promptTemplate": string,
  "rubricContentType": enum (RubricContentType),
  "rubricTypeOntology": [
    string
  ],

  // Union field _model_config can be only one of the following:
  "modelConfig": {
    object (AutoraterConfig)
  }
  // End of list of possible types for union field _model_config.
}
```

| Fields                                                                          |                                                                                                                                                                                                                                                                                                                                                            |
|---------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `promptTemplate`                                                                | `string` Template for the prompt used to generate rubrics. The details should be updated based on the most-recent recipe requirements.                                                                                                                                                                                                                     |
| `rubricContentType`                                                             | `enum ( `[`RubricContentType`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.RubricContentType)` )` The type of rubric content to be generated.                                                                                                                                  |
| `rubricTypeOntology[]`                                                          | `string` Optional. An optional, pre-defined list of allowed types for generated rubrics. If this field is provided, it implies `include_rubric_type` should be true, and the generated rubric types should be chosen from this ontology.                                                                                                                   |
| Union field `_model_config` . `_model_config` can be only one of the following: |                                                                                                                                                                                                                                                                                                                                                            |
| `modelConfig`                                                                   | `object ( `[`AutoraterConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.AutoraterConfig)` )` Configuration for the model used in rubric generation. Configs including sampling count and base model can be specified here. Flipping is not supported for rubric generation. |

### AutoraterConfig

**JSON representation**

```
{
  "autoraterModel": string,
  "generationConfig": {
    object (GenerationConfig)
  },

  // Union field _sampling_count can be only one of the following:
  "samplingCount": integer
  // End of list of possible types for union field _sampling_count.

  // Union field _flip_enabled can be only one of the following:
  "flipEnabled": boolean
  // End of list of possible types for union field _flip_enabled.
}
```

| Fields                                                                              |                                                                                                                                                                                                                                                                                                                                                                                                                               |
|-------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `autoraterModel`                                                                    | `string` Optional. The fully qualified name of the publisher model or tuned autorater endpoint to use. Publisher model format: `projects/{project}/locations/{location}/publishers/*/models/*` Tuned model endpoint format: `projects/{project}/locations/{location}/endpoints/{endpoint}`                                                                                                                                    |
| `generationConfig`                                                                  | `object ( `[`GenerationConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.GenerationConfig)` )` Optional. Configuration options for model generation and outputs.                                                                                                                                                                               |
| Union field `_sampling_count` . `_sampling_count` can be only one of the following: |                                                                                                                                                                                                                                                                                                                                                                                                                               |
| `samplingCount`                                                                     | `integer` Optional. Number of samples for each instance in the dataset. If not specified, the default is 4. Minimum value is 1, maximum value is 32.                                                                                                                                                                                                                                                                          |
| Union field `_flip_enabled` . `_flip_enabled` can be only one of the following:     |                                                                                                                                                                                                                                                                                                                                                                                                                               |
| `flipEnabled`                                                                       | `boolean` Optional. Default is true. Whether to flip the candidate and baseline responses. This is only applicable to the pairwise metric. If enabled, also provide PairwiseMetricSpec.candidate_response_field_name and PairwiseMetricSpec.baseline_response_field_name. When rendering PairwiseMetricSpec.metric_prompt_template, the candidate and baseline fields will be flipped for half of the samples to reduce bias. |

### GenerationConfig

**JSON representation**

```
{
  "stopSequences": [
    string
  ],
  "responseMimeType": string,
  "responseModalities": [
    enum (Modality)
  ],
  "thinkingConfig": {
    object (ThinkingConfig)
  },
  "modelConfig": {
    object (ModelConfig)
  },
  "responseFormat": [
    {
      object (ResponseFormat)
    }
  ],

  // Union field _temperature can be only one of the following:
  "temperature": number
  // End of list of possible types for union field _temperature.

  // Union field _top_p can be only one of the following:
  "topP": number
  // End of list of possible types for union field _top_p.

  // Union field _top_k can be only one of the following:
  "topK": number
  // End of list of possible types for union field _top_k.

  // Union field _candidate_count can be only one of the following:
  "candidateCount": integer
  // End of list of possible types for union field _candidate_count.

  // Union field _max_output_tokens can be only one of the following:
  "maxOutputTokens": integer
  // End of list of possible types for union field _max_output_tokens.

  // Union field _response_logprobs can be only one of the following:
  "responseLogprobs": boolean
  // End of list of possible types for union field _response_logprobs.

  // Union field _logprobs can be only one of the following:
  "logprobs": integer
  // End of list of possible types for union field _logprobs.

  // Union field _presence_penalty can be only one of the following:
  "presencePenalty": number
  // End of list of possible types for union field _presence_penalty.

  // Union field _frequency_penalty can be only one of the following:
  "frequencyPenalty": number
  // End of list of possible types for union field _frequency_penalty.

  // Union field _seed can be only one of the following:
  "seed": integer
  // End of list of possible types for union field _seed.

  // Union field _response_schema can be only one of the following:
  "responseSchema": {
    object (Schema)
  }
  // End of list of possible types for union field _response_schema.

  // Union field _response_json_schema can be only one of the following:
  "responseJsonSchema": value
  // End of list of possible types for union field _response_json_schema.

  // Union field _routing_config can be only one of the following:
  "routingConfig": {
    object (RoutingConfig)
  }
  // End of list of possible types for union field _routing_config.

  // Union field _audio_timestamp can be only one of the following:
  "audioTimestamp": boolean
  // End of list of possible types for union field _audio_timestamp.

  // Union field _media_resolution can be only one of the following:
  "mediaResolution": enum (MediaResolution)
  // End of list of possible types for union field _media_resolution.

  // Union field _speech_config can be only one of the following:
  "speechConfig": {
    object (SpeechConfig)
  }
  // End of list of possible types for union field _speech_config.

  // Union field _enable_affective_dialog can be only one of the following:
  "enableAffectiveDialog": boolean
  // End of list of possible types for union field _enable_affective_dialog.

  // Union field _image_config can be only one of the following:
  "imageConfig": {
    object (ImageConfig)
  }
  // End of list of possible types for union field _image_config.

  // Union field _audio_transcription_config can be only one of the following:
  "audioTranscriptionConfig": {
    object (AudioTranscriptionConfig)
  }
  // End of list of possible types for union field _audio_transcription_config.
}
```

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Fields</th>
<th></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code>stopSequences[]</code></td>
<td><p><code>string</code></p>
<p>Optional. A list of character sequences that will stop the model from generating further tokens. If a stop sequence is generated, the output will end at that point. This is useful for controlling the length and structure of the output. For example, you can use ["\n", "###"] to stop generation at a new line or a specific marker.</p></td>
</tr>
<tr class="even">
<td><code>responseMimeType </code><strong><code>(deprecated)</code></strong></td>
<td><p><code>string</code></p>
<blockquote>
<p>This item is deprecated!</p>
</blockquote>
<p>Optional. The IANA standard MIME type of the response. The model will generate output that conforms to this MIME type. Supported values include 'text/plain' (default) and 'application/json'. The model needs to be prompted to output the appropriate response type, otherwise the behavior is undefined. Deprecated: Use <code>response_format</code> instead.</p></td>
</tr>
<tr class="odd">
<td><code>responseModalities[]</code></td>
<td><p><code>enum ( </code><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.Modality"><code>Modality</code></a><code> )</code></p>
<p>Optional. The modalities of the response. The model will generate a response that includes all the specified modalities. For example, if this is set to <code>[TEXT, IMAGE]</code> , the response will include both text and an image.</p></td>
</tr>
<tr class="even">
<td><code>thinkingConfig</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.ThinkingConfig"><code>ThinkingConfig</code></a><code> )</code></p>
<p>Optional. Configuration for thinking features. An error will be returned if this field is set for models that don't support thinking.</p></td>
</tr>
<tr class="odd">
<td><code>modelConfig </code><strong><code>(deprecated)</code></strong></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.ModelConfig"><code>ModelConfig</code></a><code> )</code></p>
<blockquote>
<p>Optional. The <code>model_config</code> field is deprecated and is not supported anymore. Use <code>routing_config</code> instead.</p>
</blockquote>
<p>Optional. Config for model selection.</p></td>
</tr>
<tr class="even">
<td><code>responseFormat[]</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.ResponseFormat"><code>ResponseFormat</code></a><code> )</code></p>
<p>Optional. New response format field for the model to configure output formatting and delivery.</p></td>
</tr>
<tr class="odd">
<td><p>Union field <code>_temperature</code> .</p>
<p><code>_temperature</code> can be only one of the following:</p></td>
<td></td>
</tr>
<tr class="even">
<td><code>temperature</code></td>
<td><p><code>number</code></p>
<p>Optional. Controls the randomness of the output. A higher temperature results in more creative and diverse responses, while a lower temperature makes the output more predictable and focused. The valid range is (0.0, 2.0].</p></td>
</tr>
<tr class="odd">
<td><p>Union field <code>_top_p</code> .</p>
<p><code>_top_p</code> can be only one of the following:</p></td>
<td></td>
</tr>
<tr class="even">
<td><code>topP</code></td>
<td><p><code>number</code></p>
<p>Optional. Specifies the nucleus sampling threshold. The model considers only the smallest set of tokens whose cumulative probability is at least <code>top_p</code> . This helps generate more diverse and less repetitive responses. For example, a <code>top_p</code> of 0.9 means the model considers tokens until the cumulative probability of the tokens to select from reaches 0.9. It's recommended to adjust either temperature or <code>top_p</code> , but not both.</p></td>
</tr>
<tr class="odd">
<td><p>Union field <code>_top_k</code> .</p>
<p><code>_top_k</code> can be only one of the following:</p></td>
<td></td>
</tr>
<tr class="even">
<td><code>topK</code></td>
<td><p><code>number</code></p>
<p>Optional. Specifies the top-k sampling threshold. The model considers only the top k most probable tokens for the next token. This can be useful for generating more coherent and less random text. For example, a <code>top_k</code> of 40 means the model will choose the next word from the 40 most likely words.</p></td>
</tr>
<tr class="odd">
<td><p>Union field <code>_candidate_count</code> .</p>
<p><code>_candidate_count</code> can be only one of the following:</p></td>
<td></td>
</tr>
<tr class="even">
<td><code>candidateCount</code></td>
<td><p><code>integer</code></p>
<p>Optional. The number of candidate responses to generate.</p>
<p>A higher <code>candidate_count</code> can provide more options to choose from, but it also consumes more resources. This can be useful for generating a variety of responses and selecting the best one.</p></td>
</tr>
<tr class="odd">
<td><p>Union field <code>_max_output_tokens</code> .</p>
<p><code>_max_output_tokens</code> can be only one of the following:</p></td>
<td></td>
</tr>
<tr class="even">
<td><code>maxOutputTokens</code></td>
<td><p><code>integer</code></p>
<p>Optional. The maximum number of tokens to generate in the response.</p>
<p>A token is approximately four characters. The default value varies by model. This parameter can be used to control the length of the generated text and prevent overly long responses.</p></td>
</tr>
<tr class="odd">
<td><p>Union field <code>_response_logprobs</code> .</p>
<p><code>_response_logprobs</code> can be only one of the following:</p></td>
<td></td>
</tr>
<tr class="even">
<td><code>responseLogprobs</code></td>
<td><p><code>boolean</code></p>
<p>Optional. If set to true, the log probabilities of the output tokens are returned.</p>
<p>Log probabilities are the logarithm of the probability of a token appearing in the output. A higher log probability means the token is more likely to be generated. This can be useful for analyzing the model's confidence in its own output and for debugging.</p></td>
</tr>
<tr class="odd">
<td><p>Union field <code>_logprobs</code> .</p>
<p><code>_logprobs</code> can be only one of the following:</p></td>
<td></td>
</tr>
<tr class="even">
<td><code>logprobs</code></td>
<td><p><code>integer</code></p>
<p>Optional. The number of top log probabilities to return for each token.</p>
<p>This can be used to see which other tokens were considered likely candidates for a given position. A higher value will return more options, but it will also increase the size of the response.</p></td>
</tr>
<tr class="odd">
<td><p>Union field <code>_presence_penalty</code> .</p>
<p><code>_presence_penalty</code> can be only one of the following:</p></td>
<td></td>
</tr>
<tr class="even">
<td><code>presencePenalty</code></td>
<td><p><code>number</code></p>
<p>Optional. Penalizes tokens that have already appeared in the generated text. A positive value encourages the model to generate more diverse and less repetitive text. Valid values can range from [-2.0, 2.0].</p></td>
</tr>
<tr class="odd">
<td><p>Union field <code>_frequency_penalty</code> .</p>
<p><code>_frequency_penalty</code> can be only one of the following:</p></td>
<td></td>
</tr>
<tr class="even">
<td><code>frequencyPenalty</code></td>
<td><p><code>number</code></p>
<p>Optional. Penalizes tokens based on their frequency in the generated text. A positive value helps to reduce the repetition of words and phrases. Valid values can range from [-2.0, 2.0].</p></td>
</tr>
<tr class="odd">
<td><p>Union field <code>_seed</code> .</p>
<p><code>_seed</code> can be only one of the following:</p></td>
<td></td>
</tr>
<tr class="even">
<td><code>seed</code></td>
<td><p><code>integer</code></p>
<p>Optional. A seed for the random number generator.</p>
<p>By setting a seed, you can make the model's output mostly deterministic. For a given prompt and parameters (like temperature, top_p, etc.), the model will produce the same response every time. However, it's not a guaranteed absolute deterministic behavior. This is different from parameters like <code>temperature</code> , which control the <em>level</em> of randomness. <code>seed</code> ensures that the "random" choices the model makes are the same on every run, making it essential for testing and ensuring reproducible results.</p></td>
</tr>
<tr class="odd">
<td><p>Union field <code>_response_schema</code> .</p>
<p><code>_response_schema</code> can be only one of the following:</p></td>
<td></td>
</tr>
<tr class="even">
<td><code>responseSchema </code><strong><code>(deprecated)</code></strong></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.Schema"><code>Schema</code></a><code> )</code></p>
<blockquote>
<p>This item is deprecated!</p>
</blockquote>
<p>Optional. Lets you to specify a schema for the model's response, ensuring that the output conforms to a particular structure. This is useful for generating structured data such as JSON. The schema is a subset of the <a href="https://spec.openapis.org/oas/v3.0.3#schema">OpenAPI 3.0 schema object</a> object.</p>
<p>When this field is set, you must also set the <code>response_mime_type</code> to <code>application/json</code> . Deprecated: Use <code>response_format</code> instead.</p></td>
</tr>
<tr class="odd">
<td><p>Union field <code>_response_json_schema</code> .</p>
<p><code>_response_json_schema</code> can be only one of the following:</p></td>
<td></td>
</tr>
<tr class="even">
<td><code>responseJsonSchema </code><strong><code>(deprecated)</code></strong></td>
<td><p><code>value ( </code><a href="https://protobuf.dev/reference/protobuf/google.protobuf/#value"><code>Value</code></a><code> format)</code></p>
<blockquote>
<p>This item is deprecated!</p>
</blockquote>
<p>Optional. When this field is set, <code>response_schema</code> must be omitted and <code>response_mime_type</code> must be set to <code>application/json</code> . Deprecated: Use <code>response_format</code> instead.</p></td>
</tr>
<tr class="odd">
<td><p>Union field <code>_routing_config</code> .</p>
<p><code>_routing_config</code> can be only one of the following:</p></td>
<td></td>
</tr>
<tr class="even">
<td><code>routingConfig</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.RoutingConfig"><code>RoutingConfig</code></a><code> )</code></p>
<p>Optional. Routing configuration.</p></td>
</tr>
<tr class="odd">
<td><p>Union field <code>_audio_timestamp</code> .</p>
<p><code>_audio_timestamp</code> can be only one of the following:</p></td>
<td></td>
</tr>
<tr class="even">
<td><code>audioTimestamp</code></td>
<td><p><code>boolean</code></p>
<p>Optional. If enabled, audio timestamps will be included in the request to the model. This can be useful for synchronizing audio with other modalities in the response.</p></td>
</tr>
<tr class="odd">
<td><p>Union field <code>_media_resolution</code> .</p>
<p><code>_media_resolution</code> can be only one of the following:</p></td>
<td></td>
</tr>
<tr class="even">
<td><code>mediaResolution</code></td>
<td><p><code>enum ( </code><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.MediaResolution_1"><code>MediaResolution</code></a><code> )</code></p>
<p>Optional. The token resolution at which input media content is sampled. This is used to control the trade-off between the quality of the response and the number of tokens used to represent the media. A higher resolution allows the model to perceive more detail, which can lead to a more nuanced response, but it will also use more tokens. This does not affect the image dimensions sent to the model.</p></td>
</tr>
<tr class="odd">
<td><p>Union field <code>_speech_config</code> .</p>
<p><code>_speech_config</code> can be only one of the following:</p></td>
<td></td>
</tr>
<tr class="even">
<td><code>speechConfig</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.SpeechConfig"><code>SpeechConfig</code></a><code> )</code></p>
<p>Optional. The speech generation config.</p></td>
</tr>
<tr class="odd">
<td><p>Union field <code>_enable_affective_dialog</code> .</p>
<p><code>_enable_affective_dialog</code> can be only one of the following:</p></td>
<td></td>
</tr>
<tr class="even">
<td><code>enableAffectiveDialog</code></td>
<td><p><code>boolean</code></p>
<p>Optional. If enabled, the model will detect emotions and adapt its responses accordingly. For example, if the model detects that the user is frustrated, it may provide a more empathetic response.</p></td>
</tr>
<tr class="odd">
<td><p>Union field <code>_image_config</code> .</p>
<p><code>_image_config</code> can be only one of the following:</p></td>
<td></td>
</tr>
<tr class="even">
<td><code>imageConfig </code><strong><code>(deprecated)</code></strong></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.ImageConfig"><code>ImageConfig</code></a><code> )</code></p>
<blockquote>
<p>This item is deprecated!</p>
</blockquote>
<p>Optional. Config for image generation features. Deprecated: Use <code>response_format.image</code> instead.</p></td>
</tr>
<tr class="odd">
<td><p>Union field <code>_audio_transcription_config</code> .</p>
<p><code>_audio_transcription_config</code> can be only one of the following:</p></td>
<td></td>
</tr>
<tr class="even">
<td><code>audioTranscriptionConfig</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.AudioTranscriptionConfig"><code>AudioTranscriptionConfig</code></a><code> )</code></p>
<p>Optional. Config for audio transcription (speech recognition).</p></td>
</tr>
</tbody>
</table>

### Schema

**JSON representation**

```
{
  "type": enum (Type),
  "format": string,
  "title": string,
  "description": string,
  "nullable": boolean,
  "default": value,
  "items": {
    object (Schema)
  },
  "minItems": string,
  "maxItems": string,
  "enum": [
    string
  ],
  "properties": {
    string: {
      object (Schema)
    },
    ...
  },
  "propertyOrdering": [
    string
  ],
  "required": [
    string
  ],
  "minProperties": string,
  "maxProperties": string,
  "minimum": number,
  "maximum": number,
  "minLength": string,
  "maxLength": string,
  "pattern": string,
  "example": value,
  "anyOf": [
    {
      object (Schema)
    }
  ],
  "additionalProperties": value,
  "ref": string,
  "defs": {
    string: {
      object (Schema)
    },
    ...
  }
}
```

| Fields                 |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
|------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `type`                 | `enum ( `[`Type`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.Type)` )` Optional. Data type of the schema field.                                                                                                                                                                                                                                                                                                                        |
| `format`               | `string` Optional. The format of the data. For `NUMBER` type, format can be `float` or `double` . For `INTEGER` type, format can be `int32` or `int64` . For `STRING` type, format can be `email` , `byte` , `date` , `date-time` , `password` , and other formats to further refine the data type.                                                                                                                                                                                                                 |
| `title`                | `string` Optional. Title for the schema.                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| `description`          | `string` Optional. Describes the data. The model uses this field to understand the purpose of the schema and how to use it. It is a best practice to provide a clear and descriptive explanation for the schema and its properties here, rather than in the prompt.                                                                                                                                                                                                                                                 |
| `nullable`             | `boolean` Optional. Indicates if the value of this field can be null.                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| `default`              | `value ( `[`Value`](https://protobuf.dev/reference/protobuf/google.protobuf/#value)` format)` Optional. Default value to use if the field is not specified.                                                                                                                                                                                                                                                                                                                                                         |
| `items`                | `object ( `[`Schema`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.Schema)` )` Optional. If type is `ARRAY` , `items` specifies the schema of elements in the array.                                                                                                                                                                                                                                                                     |
| `minItems`             | `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)` Optional. If type is `ARRAY` , `min_items` specifies the minimum number of items in an array.                                                                                                                                                                                                                                                                                                                                |
| `maxItems`             | `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)` Optional. If type is `ARRAY` , `max_items` specifies the maximum number of items in an array.                                                                                                                                                                                                                                                                                                                                |
| `enum[]`               | `string` Optional. Possible values of the field. This field can be used to restrict a value to a fixed set of values. To mark a field as an enum, set `format` to `enum` and provide the list of possible values in `enum` . For example: 1. To define directions: `{type:STRING, format:enum, enum:["EAST", "NORTH", "SOUTH", "WEST"]}` 2. To define apartment numbers: `{type:INTEGER, format:enum, enum:["101", "201", "301"]}`                                                                                  |
| `properties`           | `map (key: string, value: object ( `[`Schema`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.Schema)` ))` Optional. If type is `OBJECT` , `properties` is a map of property names to schema definitions for each property of the object. An object containing a list of `"key": value` pairs. Example: `{ "name": "wrench", "mass": "1.3kg", "count": "3" }` .                                                                            |
| `propertyOrdering[]`   | `string` Optional. Order of properties displayed or used where order matters. This is not a standard field in OpenAPI specification, but can be used to control the order of properties.                                                                                                                                                                                                                                                                                                                            |
| `required[]`           | `string` Optional. If type is `OBJECT` , `required` lists the names of properties that must be present.                                                                                                                                                                                                                                                                                                                                                                                                             |
| `minProperties`        | `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)` Optional. If type is `OBJECT` , `min_properties` specifies the minimum number of properties that can be provided.                                                                                                                                                                                                                                                                                                            |
| `maxProperties`        | `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)` Optional. If type is `OBJECT` , `max_properties` specifies the maximum number of properties that can be provided.                                                                                                                                                                                                                                                                                                            |
| `minimum`              | `number` Optional. If type is `INTEGER` or `NUMBER` , `minimum` specifies the minimum allowed value.                                                                                                                                                                                                                                                                                                                                                                                                                |
| `maximum`              | `number` Optional. If type is `INTEGER` or `NUMBER` , `maximum` specifies the maximum allowed value.                                                                                                                                                                                                                                                                                                                                                                                                                |
| `minLength`            | `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)` Optional. If type is `STRING` , `min_length` specifies the minimum length of the string.                                                                                                                                                                                                                                                                                                                                     |
| `maxLength`            | `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)` Optional. If type is `STRING` , `max_length` specifies the maximum length of the string.                                                                                                                                                                                                                                                                                                                                     |
| `pattern`              | `string` Optional. If type is `STRING` , `pattern` specifies a regular expression that the string must match.                                                                                                                                                                                                                                                                                                                                                                                                       |
| `example`              | `value ( `[`Value`](https://protobuf.dev/reference/protobuf/google.protobuf/#value)` format)` Optional. Example of an instance of this schema.                                                                                                                                                                                                                                                                                                                                                                      |
| `anyOf[]`              | `object ( `[`Schema`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.Schema)` )` Optional. The instance must be valid against any (one or more) of the subschemas listed in `any_of` .                                                                                                                                                                                                                                                     |
| `additionalProperties` | `value ( `[`Value`](https://protobuf.dev/reference/protobuf/google.protobuf/#value)` format)` Optional. If `type` is `OBJECT` , specifies how to handle properties not defined in `properties` . If it is a boolean `false` , no additional properties are allowed. If it is a schema, additional properties are allowed if they conform to the schema.                                                                                                                                                             |
| `ref`                  | `string` Optional. Allows referencing another schema definition to use in place of this schema. The value must be a valid reference to a schema in `defs` . For example, the following schema defines a reference to a schema node named "Pet": type: object properties: pet: ref: \#/defs/Pet defs: Pet: type: object properties: name: type: string The value of the "pet" property is a reference to the schema node named "Pet". See details in <https://json-schema.org/understanding-json-schema/structuring> |
| `defs`                 | `map (key: string, value: object ( `[`Schema`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.Schema)` ))` Optional. `defs` provides a map of schema definitions that can be reused by `ref` elsewhere in the schema. Only allowed at root level of the schema. An object containing a list of `"key": value` pairs. Example: `{ "name": "wrench", "mass": "1.3kg", "count": "3" }` .                                                      |

### PropertiesEntry

**JSON representation**

```
{
  "key": string,
  "value": {
    object (Schema)
  }
}
```

| Fields  |                                                                                                                                                           |
|---------|-----------------------------------------------------------------------------------------------------------------------------------------------------------|
| `key`   | `string`                                                                                                                                                  |
| `value` | `object ( `[`Schema`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.Schema)` )` |

### DefsEntry

**JSON representation**

```
{
  "key": string,
  "value": {
    object (Schema)
  }
}
```

| Fields  |                                                                                                                                                           |
|---------|-----------------------------------------------------------------------------------------------------------------------------------------------------------|
| `key`   | `string`                                                                                                                                                  |
| `value` | `object ( `[`Schema`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.Schema)` )` |

### RoutingConfig

**JSON representation**

```
{

  // Union field routing_config can be only one of the following:
  "autoMode": {
    object (AutoRoutingMode)
  },
  "manualMode": {
    object (ManualRoutingMode)
  }
  // End of list of possible types for union field routing_config.
}
```

| Fields                                                                                                              |                                                                                                                                                                                                                                                                    |
|---------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Union field `routing_config` . The routing mode for the request. `routing_config` can be only one of the following: |                                                                                                                                                                                                                                                                    |
| `autoMode`                                                                                                          | `object ( `[`AutoRoutingMode`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.AutoRoutingMode)` )` In this mode, the model is selected automatically based on the content of the request. |
| `manualMode`                                                                                                        | `object ( `[`ManualRoutingMode`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.ManualRoutingMode)` )` In this mode, the model is specified manually.                                     |

### AutoRoutingMode

**JSON representation**

```
{

  // Union field _model_routing_preference can be only one of the following:
  "modelRoutingPreference": enum (ModelRoutingPreference)
  // End of list of possible types for union field _model_routing_preference.
}
```

| Fields                                                                                                  |                                                                                                                                                                                                                       |
|---------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Union field `_model_routing_preference` . `_model_routing_preference` can be only one of the following: |                                                                                                                                                                                                                       |
| `modelRoutingPreference`                                                                                | `enum ( `[`ModelRoutingPreference`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.ModelRoutingPreference)` )` The model routing preference. |

### ManualRoutingMode

**JSON representation**

```
{

  // Union field _model_name can be only one of the following:
  "modelName": string
  // End of list of possible types for union field _model_name.
}
```

| Fields                                                                      |                                                                             |
|-----------------------------------------------------------------------------|-----------------------------------------------------------------------------|
| Union field `_model_name` . `_model_name` can be only one of the following: |                                                                             |
| `modelName`                                                                 | `string` The name of the model to use. Only public LLM models are accepted. |

### SpeechConfig

**JSON representation**

```
{
  "voiceConfig": {
    object (VoiceConfig)
  },
  "languageCode": string,
  "multiSpeakerVoiceConfig": {
    object (MultiSpeakerVoiceConfig)
  }
}
```

| Fields                    |                                                                                                                                                                                                                                                                                                                  |
|---------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `voiceConfig`             | `object ( `[`VoiceConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.VoiceConfig)` )` The configuration for the voice to use.                                                                                                      |
| `languageCode`            | `string` Optional. The language code (ISO 639-1) for the speech synthesis.                                                                                                                                                                                                                                       |
| `multiSpeakerVoiceConfig` | `object ( `[`MultiSpeakerVoiceConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.MultiSpeakerVoiceConfig)` )` The configuration for a multi-speaker text-to-speech request. This field is mutually exclusive with `voice_config` . |

### VoiceConfig

**JSON representation**

```
{

  // Union field voice_config can be only one of the following:
  "prebuiltVoiceConfig": {
    object (PrebuiltVoiceConfig)
  },
  "replicatedVoiceConfig": {
    object (ReplicatedVoiceConfig)
  }
  // End of list of possible types for union field voice_config.
}
```

| Fields                                                                                                                  |                                                                                                                                                                                                                                                                                                           |
|-------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Union field `voice_config` . The configuration for the speaker to use. `voice_config` can be only one of the following: |                                                                                                                                                                                                                                                                                                           |
| `prebuiltVoiceConfig`                                                                                                   | `object ( `[`PrebuiltVoiceConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.PrebuiltVoiceConfig)` )` The configuration for a prebuilt voice.                                                                               |
| `replicatedVoiceConfig`                                                                                                 | `object ( `[`ReplicatedVoiceConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.ReplicatedVoiceConfig)` )` Optional. The configuration for a replicated voice. This enables users to replicate a voice from an audio sample. |

### PrebuiltVoiceConfig

**JSON representation**

```
{

  // Union field _voice_name can be only one of the following:
  "voiceName": string
  // End of list of possible types for union field _voice_name.
}
```

| Fields                                                                      |                                                 |
|-----------------------------------------------------------------------------|-------------------------------------------------|
| Union field `_voice_name` . `_voice_name` can be only one of the following: |                                                 |
| `voiceName`                                                                 | `string` The name of the prebuilt voice to use. |

### ReplicatedVoiceConfig

**JSON representation**

```
{
  "mimeType": string,
  "voiceSampleAudio": string
}
```

| Fields             |                                                                                                                                                                                                                                                |
|--------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `mimeType`         | `string` Optional. The mimetype of the voice sample. The only currently supported value is `audio/wav` . This represents 16-bit signed little-endian wav data, with a 24kHz sampling rate. `mime_type` will default to `audio/wav` if not set. |
| `voiceSampleAudio` | `string ( `[`bytes`](https://developers.google.com/discovery/v1/type-format)` format)` Optional. The sample of the custom voice. A base64-encoded string.                                                                                      |

### MultiSpeakerVoiceConfig

**JSON representation**

```
{
  "speakerVoiceConfigs": [
    {
      object (SpeakerVoiceConfig)
    }
  ]
}
```

| Fields                  |                                                                                                                                                                                                                                                                                                                 |
|-------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `speakerVoiceConfigs[]` | `object ( `[`SpeakerVoiceConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.SpeakerVoiceConfig)` )` Required. A list of configurations for the voices of the speakers. Exactly two speaker voice configurations must be provided. |

### SpeakerVoiceConfig

**JSON representation**

```
{
  "speaker": string,
  "voiceConfig": {
    object (VoiceConfig)
  }
}
```

| Fields        |                                                                                                                                                                                                                                |
|---------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `speaker`     | `string` Required. The name of the speaker. This should be the same as the speaker name used in the prompt.                                                                                                                    |
| `voiceConfig` | `object ( `[`VoiceConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.VoiceConfig)` )` Required. The configuration for the voice of this speaker. |

### ThinkingConfig

**JSON representation**

```
{

  // Union field _include_thoughts can be only one of the following:
  "includeThoughts": boolean
  // End of list of possible types for union field _include_thoughts.

  // Union field _thinking_budget can be only one of the following:
  "thinkingBudget": integer
  // End of list of possible types for union field _thinking_budget.

  // Union field _thinking_level can be only one of the following:
  "thinkingLevel": enum (ThinkingLevel)
  // End of list of possible types for union field _thinking_level.
}
```

| Fields                                                                                  |                                                                                                                                                                                                                                                                                                                            |
|-----------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Union field `_include_thoughts` . `_include_thoughts` can be only one of the following: |                                                                                                                                                                                                                                                                                                                            |
| `includeThoughts`                                                                       | `boolean` Optional. If true, the model will include its thoughts in the response. "Thoughts" are the intermediate steps the model takes to arrive at the final response. They can provide insights into the model's reasoning process and help with debugging. If this is true, thoughts are returned only when available. |
| Union field `_thinking_budget` . `_thinking_budget` can be only one of the following:   |                                                                                                                                                                                                                                                                                                                            |
| `thinkingBudget`                                                                        | `integer` Optional. The token budget for the model's thinking process. The model will make a best effort to stay within this budget. This can be used to control the trade-off between response quality and latency.                                                                                                       |
| Union field `_thinking_level` . `_thinking_level` can be only one of the following:     |                                                                                                                                                                                                                                                                                                                            |
| `thinkingLevel`                                                                         | `enum ( `[`ThinkingLevel`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.ThinkingLevel)` )` Optional. The number of thoughts tokens that the model should generate.                                                                              |

### ModelConfig

**JSON representation**

```
{
  "featureSelectionPreference": enum (FeatureSelectionPreference)
}
```

| Fields                       |                                                                                                                                                                                                                                         |
|------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `featureSelectionPreference` | `enum ( `[`FeatureSelectionPreference`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.FeatureSelectionPreference)` )` Required. Feature selection preference. |

### ImageConfig

**JSON representation**

```
{

  // Union field _image_output_options can be only one of the following:
  "imageOutputOptions": {
    object (ImageOutputOptions)
  }
  // End of list of possible types for union field _image_output_options.

  // Union field _aspect_ratio can be only one of the following:
  "aspectRatio": string
  // End of list of possible types for union field _aspect_ratio.

  // Union field _person_generation can be only one of the following:
  "personGeneration": enum (PersonGeneration)
  // End of list of possible types for union field _person_generation.

  // Union field _image_size can be only one of the following:
  "imageSize": string
  // End of list of possible types for union field _image_size.
}
```

| Fields                                                                                          |                                                                                                                                                                                                                                           |
|-------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Union field `_image_output_options` . `_image_output_options` can be only one of the following: |                                                                                                                                                                                                                                           |
| `imageOutputOptions`                                                                            | `object ( `[`ImageOutputOptions`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.ImageOutputOptions)` )` Optional. The image output format for generated images. |
| Union field `_aspect_ratio` . `_aspect_ratio` can be only one of the following:                 |                                                                                                                                                                                                                                           |
| `aspectRatio`                                                                                   | `string` Optional. The desired aspect ratio for the generated images. The following aspect ratios are supported: "1:1" "2:3", "3:2" "3:4", "4:3" "4:5", "5:4" "9:16", "16:9" "21:9"                                                       |
| Union field `_person_generation` . `_person_generation` can be only one of the following:       |                                                                                                                                                                                                                                           |
| `personGeneration`                                                                              | `enum ( `[`PersonGeneration`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.PersonGeneration)` )` Optional. Controls whether the model can generate people.     |
| Union field `_image_size` . `_image_size` can be only one of the following:                     |                                                                                                                                                                                                                                           |
| `imageSize`                                                                                     | `string` Optional. Specifies the size of generated images. Supported values are `1K` , `2K` , `4K` . If not specified, the model will use default value `1K` .                                                                            |

### ImageOutputOptions

**JSON representation**

```
{

  // Union field _mime_type can be only one of the following:
  "mimeType": string
  // End of list of possible types for union field _mime_type.

  // Union field _compression_quality can be only one of the following:
  "compressionQuality": integer
  // End of list of possible types for union field _compression_quality.
}
```

| Fields                                                                                        |                                                                         |
|-----------------------------------------------------------------------------------------------|-------------------------------------------------------------------------|
| Union field `_mime_type` . `_mime_type` can be only one of the following:                     |                                                                         |
| `mimeType`                                                                                    | `string` Optional. The image format that the output should be saved as. |
| Union field `_compression_quality` . `_compression_quality` can be only one of the following: |                                                                         |
| `compressionQuality`                                                                          | `integer` Optional. The compression quality of the output image.        |

### ResponseFormat

**JSON representation**

```
{

  // Union field format can be only one of the following:
  "text": {
    object (TextResponseFormat)
  },
  "audio": {
    object (AudioResponseFormat)
  },
  "image": {
    object (ImageResponseFormat)
  },
  "video": {
    object (VideoResponseFormat)
  }
  // End of list of possible types for union field format.
}
```

| Fields                                                                                              |                                                                                                                                                                                                          |
|-----------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Union field `format` . The format of the output content. `format` can be only one of the following: |                                                                                                                                                                                                          |
| `text`                                                                                              | `object ( `[`TextResponseFormat`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.TextResponseFormat)` )` Text output format.    |
| `audio`                                                                                             | `object ( `[`AudioResponseFormat`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.AudioResponseFormat)` )` Audio output format. |
| `image`                                                                                             | `object ( `[`ImageResponseFormat`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.ImageResponseFormat)` )` Image output format. |
| `video`                                                                                             | `object ( `[`VideoResponseFormat`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.VideoResponseFormat)` )` Video output format. |

### TextResponseFormat

**JSON representation**

```
{

  // Union field _mime_type can be only one of the following:
  "mimeType": enum (MimeType)
  // End of list of possible types for union field _mime_type.

  // Union field _schema can be only one of the following:
  "schema": value
  // End of list of possible types for union field _schema.
}
```

| Fields                                                                    |                                                                                                                                                                                                                    |
|---------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Union field `_mime_type` . `_mime_type` can be only one of the following: |                                                                                                                                                                                                                    |
| `mimeType`                                                                | `enum ( `[`MimeType`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.MimeType)` )` Optional. The IANA standard MIME type of the response. |
| Union field `_schema` . `_schema` can be only one of the following:       |                                                                                                                                                                                                                    |
| `schema`                                                                  | `value ( `[`Value`](https://protobuf.dev/reference/protobuf/google.protobuf/#value)` format)` Optional. The JSON schema that the output should conform to. Only applicable when mime_type is APPLICATION_JSON.     |

### AudioResponseFormat

**JSON representation**

```
{
  "delivery": enum (DeliveryMode),

  // Union field _mime_type can be only one of the following:
  "mimeType": enum (MimeType)
  // End of list of possible types for union field _mime_type.

  // Union field _sample_rate can be only one of the following:
  "sampleRate": integer
  // End of list of possible types for union field _sample_rate.

  // Union field _bit_rate can be only one of the following:
  "bitRate": integer
  // End of list of possible types for union field _bit_rate.
}
```

| Fields                                                                        |                                                                                                                                                                                                                        |
|-------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `delivery`                                                                    | `enum ( `[`DeliveryMode`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.DeliveryMode)` )` Optional. Delivery mode for the generated content. |
| Union field `_mime_type` . `_mime_type` can be only one of the following:     |                                                                                                                                                                                                                        |
| `mimeType`                                                                    | `enum ( `[`MimeType`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.MimeType_1)` )` Optional. The MIME type of the audio output.             |
| Union field `_sample_rate` . `_sample_rate` can be only one of the following: |                                                                                                                                                                                                                        |
| `sampleRate`                                                                  | `integer` Optional. Sample rate for the generated audio in Hertz.                                                                                                                                                      |
| Union field `_bit_rate` . `_bit_rate` can be only one of the following:       |                                                                                                                                                                                                                        |
| `bitRate`                                                                     | `integer` Optional. Bit rate in bits per second (bps). Only applicable for compressed formats (MP3, Opus).                                                                                                             |

### ImageResponseFormat

**JSON representation**

```
{
  "delivery": enum (DeliveryMode),

  // Union field _mime_type can be only one of the following:
  "mimeType": enum (MimeType)
  // End of list of possible types for union field _mime_type.

  // Union field _aspect_ratio can be only one of the following:
  "aspectRatio": enum (AspectRatio)
  // End of list of possible types for union field _aspect_ratio.

  // Union field _image_size can be only one of the following:
  "imageSize": enum (ImageSize)
  // End of list of possible types for union field _image_size.
}
```

| Fields                                                                          |                                                                                                                                                                                                                        |
|---------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `delivery`                                                                      | `enum ( `[`DeliveryMode`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.DeliveryMode)` )` Optional. Delivery mode for the generated content. |
| Union field `_mime_type` . `_mime_type` can be only one of the following:       |                                                                                                                                                                                                                        |
| `mimeType`                                                                      | `enum ( `[`MimeType`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.MimeType_2)` )` Optional. The MIME type of the image output.             |
| Union field `_aspect_ratio` . `_aspect_ratio` can be only one of the following: |                                                                                                                                                                                                                        |
| `aspectRatio`                                                                   | `enum ( `[`AspectRatio`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.AspectRatio)` )` Optional. The aspect ratio for the image output.     |
| Union field `_image_size` . `_image_size` can be only one of the following:     |                                                                                                                                                                                                                        |
| `imageSize`                                                                     | `enum ( `[`ImageSize`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.ImageSize)` )` Optional. The size of the image output.                  |

### VideoResponseFormat

**JSON representation**

```
{
  "delivery": enum (DeliveryMode),
  "gcsUri": string,
  "aspectRatio": enum (AspectRatio),

  // Union field _duration can be only one of the following:
  "duration": string
  // End of list of possible types for union field _duration.
}
```

| Fields                                                                  |                                                                                                                                                                                                                                                     |
|-------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `delivery`                                                              | `enum ( `[`DeliveryMode`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.DeliveryMode)` )` Optional. Delivery mode for the generated content.                              |
| `gcsUri`                                                                | `string` Optional. The Google Cloud Storage URI to store the video output. Required for Vertex if delivery is URI.                                                                                                                                  |
| `aspectRatio`                                                           | `enum ( `[`AspectRatio`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.AspectRatio_1)` )` The aspect ratio for the video output.                                          |
| Union field `_duration` . `_duration` can be only one of the following: |                                                                                                                                                                                                                                                     |
| `duration`                                                              | `string ( `[`Duration`](https://protobuf.dev/reference/protobuf/google.protobuf/#duration)` format)` Optional. The duration for the video output. A duration in seconds with up to nine fractional digits, ending with ' `s` '. Example: `"3.5s"` . |

### AudioTranscriptionConfig

**JSON representation**

```
{
  "adaptationPhrases": [
    string
  ],
  "customVocabulary": [
    string
  ],
  "wordTimestamp": boolean,
  "diarization": boolean,

  // Union field language_config can be only one of the following:
  "languageAuto": {
    object (LanguageAuto)
  },
  "languageHints": {
    object (LanguageHints)
  }
  // End of list of possible types for union field language_config.
}
```

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Fields</th>
<th></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code>adaptationPhrases[] </code><strong><code>(deprecated)</code></strong></td>
<td><p><code>string</code></p>
<blockquote>
<p>This item is deprecated!</p>
</blockquote>
<p>Optional. A list of phrases to bias the ASR model towards.</p></td>
</tr>
<tr class="even">
<td><code>customVocabulary[]</code></td>
<td><p><code>string</code></p>
<p>Optional. A list of custom vocabulary phrases to bias the speech recognition model toward recognizing specific terms.</p></td>
</tr>
<tr class="odd">
<td><code>wordTimestamp</code></td>
<td><p><code>boolean</code></p>
<p>Optional. Configures word-level timestamp generation.</p></td>
</tr>
<tr class="even">
<td><code>diarization</code></td>
<td><p><code>boolean</code></p>
<p>Optional. Configures speaker diarization.</p></td>
</tr>
<tr class="odd">
<td>Union field <code>language_config</code> . Required. Specifies how to handle the languages in the audio. <code>language_config</code> can be only one of the following:</td>
<td></td>
</tr>
<tr class="even">
<td><code>languageAuto</code></td>
<td><p><code>object ( </code><code>LanguageAuto</code><code> )</code></p>
<p>Optional. The model will detect the language automatically.</p></td>
</tr>
<tr class="odd">
<td><code>languageHints</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.LanguageHints"><code>LanguageHints</code></a><code> )</code></p>
<p>Optional. Specifies one or more languages in the audio.</p></td>
</tr>
</tbody>
</table>

### LanguageHints

**JSON representation**

```
{
  "languageCodes": [
    string
  ]
}
```

| Fields            |                                                                           |
|-------------------|---------------------------------------------------------------------------|
| `languageCodes[]` | `string` Required. BCP-47 language codes. At least one must be specified. |

### EvaluationParserConfig

**JSON representation**

```
{

  // Union field parser can be only one of the following:
  "customCodeParserConfig": {
    object (CustomCodeParserConfig)
  }
  // End of list of possible types for union field parser.
}
```

| Fields                                                            |                                                                                                                                                                                                                                                |
|-------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Union field `parser` . `parser` can be only one of the following: |                                                                                                                                                                                                                                                |
| `customCodeParserConfig`                                          | `object ( `[`CustomCodeParserConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.CustomCodeParserConfig)` )` Optional. Use custom code to parse the LLM response. |

### CustomCodeParserConfig

**JSON representation**

```
{

  // Union field _parsing_function can be only one of the following:
  "parsingFunction": string
  // End of list of possible types for union field _parsing_function.
}
```

| Fields                                                                                  |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
|-----------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Union field `_parsing_function` . `_parsing_function` can be only one of the following: |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| `parsingFunction`                                                                       | `string` Required. Python function for parsing results. The function should be defined within this string. The function takes a list of strings (LLM responses) and should return either a list of dictionaries (for rubrics) or a single dictionary (for a metric result). Example function signature: def parse(responses: list\[str\]) -\> list\[dict\[str, Any\]\] \| dict\[str, Any\]: When parsing rubrics, return a list of dictionaries, where each dictionary represents a Rubric. Example for rubrics: \[ { "content": {"property": {"description": "The response is factual."}}, "type": "FACTUALITY", "importance": "HIGH" }, { "content": {"property": {"description": "The response is fluent."}}, "type": "FLUENCY", "importance": "MEDIUM" } \] When parsing critique results, return a dictionary representing a MetricResult. Example for a metric result: { "score": 0.8, "explanation": "The model followed most instructions.", "rubric_verdicts": \[...\] } ... code for result extraction and aggregation |

### CustomCodeExecutionSpec

**JSON representation**

```
{

  // Union field _evaluation_function can be only one of the following:
  "evaluationFunction": string
  // End of list of possible types for union field _evaluation_function.
}
```

| Fields                                                                                        |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
|-----------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Union field `_evaluation_function` . `_evaluation_function` can be only one of the following: |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| `evaluationFunction`                                                                          | `string` Required. Python function. Expected user to define the following function, e.g.: def evaluate(instance: dict\[str, Any\]) -\> float: Please include this function signature in the code snippet. Instance is the evaluation instance, any fields populated in the instance are available to the function as instance\[field_name\]. Example: Example input: `instance= EvaluationInstance( response=EvaluationInstance.InstanceData(text="The answer is 4."), reference=EvaluationInstance.InstanceData(text="4") )` Example converted input: `{ 'response': {'text': 'The answer is 4.'}, 'reference': {'text': '4'} }` Example python function: `def evaluate(instance: dict[str, Any]) -> float: if instance['response']['text'] == instance['reference']['text']: return 1.0 return 0.0` CustomCodeExecutionSpec is also supported in Batch Evaluation (EvalDataset RPC) and Tuning Evaluation. Each line in the input jsonl file will be converted to dict\[str, Any\] and passed to the evaluation function. |

### MetricMetadata

**JSON representation**

```
{
  "title": string,
  "scoreRange": {
    object (ScoreRange)
  },
  "otherMetadata": {
    object
  }
}
```

| Fields          |                                                                                                                                                                                                                                              |
|-----------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `title`         | `string` Optional. The user-friendly name for the metric. If not set for a registered metric, it will default to the metric's display name.                                                                                                  |
| `scoreRange`    | `object ( `[`ScoreRange`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.ScoreRange)` )` Optional. The range of possible scores for this metric, used for plotting. |
| `otherMetadata` | `object ( `[`Struct`](https://protobuf.dev/reference/protobuf/google.protobuf/#struct)` format)` Optional. Flexible metadata for user-defined attributes.                                                                                    |

### ScoreRange

**JSON representation**

```
{
  "description": string,

  // Union field _min can be only one of the following:
  "min": number
  // End of list of possible types for union field _min.

  // Union field _max can be only one of the following:
  "max": number
  // End of list of possible types for union field _max.

  // Union field _step can be only one of the following:
  "step": number
  // End of list of possible types for union field _step.
}
```

| Fields                                                          |                                                                                                                       |
|-----------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------|
| `description`                                                   | `string` Optional. The description of the score explaining the directionality etc.                                    |
| Union field `_min` . `_min` can be only one of the following:   |                                                                                                                       |
| `min`                                                           | `number` Required. The minimum value of the score range (inclusive).                                                  |
| Union field `_max` . `_max` can be only one of the following:   |                                                                                                                       |
| `max`                                                           | `number` Required. The maximum value of the score range (inclusive).                                                  |
| Union field `_step` . `_step` can be only one of the following: |                                                                                                                       |
| `step`                                                          | `number` Optional. The distance between discrete steps in the range. If unset, the range is assumed to be continuous. |

### MetricSource

**JSON representation**

```
{

  // Union field metric_source can be only one of the following:
  "metric": {
    object (Metric)
  },
  "metricResourceName": string
  // End of list of possible types for union field metric_source.
}
```

| Fields                                                                                                    |                                                                                                                                                                                 |
|-----------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Union field `metric_source` . The source of the metric. `metric_source` can be only one of the following: |                                                                                                                                                                                 |
| `metric`                                                                                                  | `object ( `[`Metric`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.Metric)` )` Inline metric config. |
| `metricResourceName`                                                                                      | `string` Optional. Resource name for registered metric.                                                                                                                         |

### EvaluationInstance

**JSON representation**

```
{
  "prompt": {
    object (InstanceData)
  },
  "rubricGroups": {
    string: {
      object (RubricGroup)
    },
    ...
  },
  "response": {
    object (InstanceData)
  },
  "reference": {
    object (InstanceData)
  },
  "otherData": {
    object (MapInstance)
  },
  "agentData": {
    object (DeprecatedAgentData)
  },
  "agentEvalData": {
    object (AgentData)
  }
}
```

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Fields</th>
<th></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code>prompt</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.InstanceData"><code>InstanceData</code></a><code> )</code></p>
<p>Optional. Data used to populate placeholder <code>prompt</code> in a metric prompt template.</p></td>
</tr>
<tr class="even">
<td><code>rubricGroups</code></td>
<td><p><code>map (key: string, value: object ( </code><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.RubricGroup"><code>RubricGroup</code></a><code> ))</code></p>
<p>Optional. Named groups of rubrics associated with the prompt. This is used for rubric-based evaluations where rubrics can be referenced by a key. The key could represent versions, associated metrics, etc.</p>
<p>An object containing a list of <code>"key": value</code> pairs. Example: <code>{ "name": "wrench", "mass": "1.3kg", "count": "3" }</code> .</p></td>
</tr>
<tr class="odd">
<td><code>response</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.InstanceData"><code>InstanceData</code></a><code> )</code></p>
<p>Optional. Data used to populate placeholder <code>response</code> in a metric prompt template.</p></td>
</tr>
<tr class="even">
<td><code>reference</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.InstanceData"><code>InstanceData</code></a><code> )</code></p>
<p>Optional. Data used to populate placeholder <code>reference</code> in a metric prompt template.</p></td>
</tr>
<tr class="odd">
<td><code>otherData</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.MapInstance"><code>MapInstance</code></a><code> )</code></p>
<p>Optional. Other data used to populate placeholders based on their key. If a key conflicts with a field in the EvaluationInstance (e.g. <code>prompt</code> ), the value of the field will take precedence over the value in other_data.</p></td>
</tr>
<tr class="even">
<td><code>agentData </code><strong><code>(deprecated)</code></strong></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.DeprecatedAgentData"><code>DeprecatedAgentData</code></a><code> )</code></p>
<blockquote>
<p>This item is deprecated!</p>
</blockquote>
<p>Optional. Deprecated: Use <code>agent_eval_data</code> instead. Data used for agent evaluation.</p></td>
</tr>
<tr class="odd">
<td><code>agentEvalData</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.AgentData"><code>AgentData</code></a><code> )</code></p>
<p>Optional. Data used for agent evaluation.</p></td>
</tr>
</tbody>
</table>

### InstanceData

**JSON representation**

```
{

  // Union field data can be only one of the following:
  "text": string,
  "contents": {
    object (Contents)
  }
  // End of list of possible types for union field data.
}
```

| Fields                                                                                             |                                                                                                                                                                                              |
|----------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Union field `data` . Supported formats for instance data. `data` can be only one of the following: |                                                                                                                                                                                              |
| `text`                                                                                             | `string` Text data.                                                                                                                                                                          |
| `contents`                                                                                         | `object ( `[`Contents`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.Contents_1)` )` List of Gemini content data. |

### Contents

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

| Fields       |                                                                                                                                                                                          |
|--------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `contents[]` | `object ( `[`Content`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.Content)` )` Optional. Repeated contents. |

### RubricGroupsEntry

**JSON representation**

```
{
  "key": string,
  "value": {
    object (RubricGroup)
  }
}
```

| Fields  |                                                                                                                                                                     |
|---------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `key`   | `string`                                                                                                                                                            |
| `value` | `object ( `[`RubricGroup`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.RubricGroup)` )` |

### RubricGroup

**JSON representation**

```
{
  "groupId": string,
  "displayName": string,
  "rubrics": [
    {
      object (Rubric)
    }
  ]
}
```

| Fields        |                                                                                                                                                                                                         |
|---------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `groupId`     | `string` Unique identifier for the group.                                                                                                                                                               |
| `displayName` | `string` Human-readable name for the group. This should be unique within a given context if used for display or selection. Example: "Instruction Following V1", "Content Quality - Summarization Task". |
| `rubrics[]`   | `object ( `[`Rubric`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.Rubric)` )` Rubrics that are part of this group.          |

### Rubric

**JSON representation**

```
{
  "rubricId": string,
  "content": {
    object (Content)
  },

  // Union field _type can be only one of the following:
  "type": string
  // End of list of possible types for union field _type.

  // Union field _importance can be only one of the following:
  "importance": enum (Importance)
  // End of list of possible types for union field _importance.
}
```

| Fields                                                                      |                                                                                                                                                                                                                                                                                                |
|-----------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `rubricId`                                                                  | `string` Unique identifier for the rubric. This ID is used to refer to this rubric, e.g., in RubricVerdict.                                                                                                                                                                                    |
| `content`                                                                   | `object ( `[`Content`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.Content_1)` )` Required. The actual testable criteria for the rubric.                                                                           |
| Union field `_type` . `_type` can be only one of the following:             |                                                                                                                                                                                                                                                                                                |
| `type`                                                                      | `string` Optional. A type designator for the rubric, which can inform how it's evaluated or interpreted by systems or users. It's recommended to use consistent, well-defined, upper snake_case strings. Examples: "SUMMARIZATION_QUALITY", "SAFETY_HARMFUL_CONTENT", "INSTRUCTION_ADHERENCE". |
| Union field `_importance` . `_importance` can be only one of the following: |                                                                                                                                                                                                                                                                                                |
| `importance`                                                                | `enum ( `[`Importance`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.Importance)` )` Optional. The relative importance of this rubric.                                                                              |

### Content

**JSON representation**

```
{

  // Union field content_type can be only one of the following:
  "property": {
    object (Property)
  }
  // End of list of possible types for union field content_type.
}
```

| Fields                                                                        |                                                                                                                                                                                                                 |
|-------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Union field `content_type` . `content_type` can be only one of the following: |                                                                                                                                                                                                                 |
| `property`                                                                    | `object ( `[`Property`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.Property)` )` Evaluation criteria based on a specific property. |

### Property

**JSON representation**

```
{
  "description": string
}
```

| Fields        |                                                                                                                 |
|---------------|-----------------------------------------------------------------------------------------------------------------|
| `description` | `string` Description of the property being evaluated. Example: "The model's response is grammatically correct." |

### MapInstance

**JSON representation**

```
{
  "mapInstance": {
    string: {
      object (InstanceData)
    },
    ...
  }
}
```

| Fields        |                                                                                                                                                                                                                                                                                                                                                       |
|---------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `mapInstance` | `map (key: string, value: object ( `[`InstanceData`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.InstanceData)` ))` Optional. Map of instance data. An object containing a list of `"key": value` pairs. Example: `{ "name": "wrench", "mass": "1.3kg", "count": "3" }` . |

### MapInstanceEntry

**JSON representation**

```
{
  "key": string,
  "value": {
    object (InstanceData)
  }
}
```

| Fields  |                                                                                                                                                                       |
|---------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `key`   | `string`                                                                                                                                                              |
| `value` | `object ( `[`InstanceData`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.InstanceData)` )` |

### DeprecatedAgentData

**JSON representation**

```
{
  "agents": {
    string: {
      object (DeprecatedAgentConfig)
    },
    ...
  },
  "turns": [
    {
      object (ConversationTurn)
    }
  ],
  "developerInstruction": {
    object (InstanceData)
  },
  "agentConfig": {
    object (DeprecatedAgentConfig)
  },

  // Union field tools_data can be only one of the following:
  "toolsText": string,
  "tools": {
    object (Tools)
  }
  // End of list of possible types for union field tools_data.

  // Union field events_data can be only one of the following:
  "events": {
    object (Events)
  }
  // End of list of possible types for union field events_data.
}
```

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Fields</th>
<th></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code>agents</code></td>
<td><p><code>map (key: string, value: object ( </code><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.DeprecatedAgentConfig"><code>DeprecatedAgentConfig</code></a><code> ))</code></p>
<p>Optional. The static Agent Configuration. This map defines the graph structure of the agent system. Key: agent_id (matches the <code>author</code> field in events). Value: The static configuration of the agent (tools, instructions, sub-agents).</p>
<p>An object containing a list of <code>"key": value</code> pairs. Example: <code>{ "name": "wrench", "mass": "1.3kg", "count": "3" }</code> .</p></td>
</tr>
<tr class="even">
<td><code>turns[]</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.ConversationTurn"><code>ConversationTurn</code></a><code> )</code></p>
<p>Optional. The chronological list of conversation turns. Each turn represents a logical execution cycle (e.g., User Input -&gt; Agent Response).</p></td>
</tr>
<tr class="odd">
<td><code>developerInstruction </code><strong><code>(deprecated)</code></strong></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.InstanceData"><code>InstanceData</code></a><code> )</code></p>
<blockquote>
<p>This item is deprecated!</p>
</blockquote>
<p>Optional. Deprecated: Use <code>agents.developer_instruction</code> or <code>turns.events.active_instruction</code> instead. A field containing instructions from the developer for the agent.</p></td>
</tr>
<tr class="even">
<td><code>agentConfig</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.DeprecatedAgentConfig"><code>DeprecatedAgentConfig</code></a><code> )</code></p>
<p>Optional. Deprecated: Use <code>agent_eval_data</code> instead. Agent configuration.</p></td>
</tr>
<tr class="odd">
<td>Union field <code>tools_data</code> . --- Legacy fields below. To be deprecated. --- Deprecated: Use <code>agents</code> instead. Data for the tools available to the agent. <code>tools_data</code> can be only one of the following:</td>
<td></td>
</tr>
<tr class="even">
<td><code>toolsText </code><strong><code>(deprecated)</code></strong></td>
<td><p><code>string</code></p>
<blockquote>
<p>This item is deprecated!</p>
</blockquote>
<p>A JSON string containing a list of tools available to an agent with info such as name, description, parameters and required parameters.</p></td>
</tr>
<tr class="odd">
<td><code>tools </code><strong><code>(deprecated)</code></strong></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.Tools"><code>Tools</code></a><code> )</code></p>
<blockquote>
<p>This item is deprecated!</p>
</blockquote>
<p>List of tools.</p></td>
</tr>
<tr class="even">
<td><p>Union field <code>events_data</code> .</p>
<p><code>events_data</code> can be only one of the following:</p></td>
<td></td>
</tr>
<tr class="odd">
<td><code>events</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.Events"><code>Events</code></a><code> )</code></p>
<p>A list of events.</p></td>
</tr>
</tbody>
</table>

### Tools

**JSON representation**

```
{
  "tool": [
    {
      object (Tool)
    }
  ]
}
```

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Fields</th>
<th></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code>tool[] </code><strong><code>(deprecated)</code></strong></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.Tool"><code>Tool</code></a><code> )</code></p>
<blockquote>
<p>This item is deprecated!</p>
</blockquote>
<p>Optional. List of tools: each tool can have multiple function declarations.</p></td>
</tr>
</tbody>
</table>

### Tool

**JSON representation**

```
{
  "functionDeclarations": [
    {
      object (FunctionDeclaration)
    }
  ],
  "retrieval": {
    object (Retrieval)
  },
  "googleSearch": {
    object (GoogleSearch)
  },
  "googleSearchRetrieval": {
    object (GoogleSearchRetrieval)
  },
  "googleMaps": {
    object (GoogleMaps)
  },
  "enterpriseWebSearch": {
    object (EnterpriseWebSearch)
  },
  "parallelAiSearch": {
    object (ParallelAiSearch)
  },
  "codeExecution": {
    object (CodeExecution)
  },
  "urlContext": {
    object (UrlContext)
  },
  "computerUse": {
    object (ComputerUse)
  }
}
```

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Fields</th>
<th></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code>functionDeclarations[]</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.FunctionDeclaration"><code>FunctionDeclaration</code></a><code> )</code></p>
<p>Optional. Function tool type. One or more function declarations to be passed to the model along with the current user query. Model may decide to call a subset of these functions by populating <code>FunctionCall</code> in the response. User should provide a <code>FunctionResponse</code> for each function call in the next turn. Based on the function responses, Model will generate the final response back to the user. Maximum 512 function declarations can be provided.</p></td>
</tr>
<tr class="even">
<td><code>retrieval</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.Retrieval"><code>Retrieval</code></a><code> )</code></p>
<p>Optional. Retrieval tool type. System will always execute the provided retrieval tool(s) to get external knowledge to answer the prompt. Retrieval results are presented to the model for generation.</p></td>
</tr>
<tr class="odd">
<td><code>googleSearch</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.GoogleSearch"><code>GoogleSearch</code></a><code> )</code></p>
<p>Optional. GoogleSearch tool type. Tool to support Google Search in Model. Powered by Google.</p></td>
</tr>
<tr class="even">
<td><code>googleSearchRetrieval </code><strong><code>(deprecated)</code></strong></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.GoogleSearchRetrieval"><code>GoogleSearchRetrieval</code></a><code> )</code></p>
<blockquote>
<p>Optional. The <code>google_search_retrieval</code> field is deprecated. Use <code>google_search</code> instead. This field is for use with Gemini 1.5 models; <code>google_search</code> is used for Gemini 2.0 and newer models.</p>
</blockquote>
<p>Optional. Specialized retrieval tool that is powered by Google Search.</p></td>
</tr>
<tr class="odd">
<td><code>googleMaps</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.GoogleMaps"><code>GoogleMaps</code></a><code> )</code></p>
<p>Optional. GoogleMaps tool type. Tool to support Google Maps in Model.</p></td>
</tr>
<tr class="even">
<td><code>enterpriseWebSearch</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.EnterpriseWebSearch"><code>EnterpriseWebSearch</code></a><code> )</code></p>
<p>Optional. Tool to support searching public web data, powered by Agent Platform Search and Sec4 compliance.</p></td>
</tr>
<tr class="odd">
<td><code>parallelAiSearch</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.ParallelAiSearch"><code>ParallelAiSearch</code></a><code> )</code></p>
<p>Optional. If specified, Agent Platform will use Parallel.ai to search for information to answer user queries. The search results will be grounded on Parallel.ai and presented to the model for response generation</p></td>
</tr>
<tr class="even">
<td><code>codeExecution</code></td>
<td><p><code>object ( </code><code>CodeExecution</code><code> )</code></p>
<p>Optional. CodeExecution tool type. Enables the model to execute code as part of generation.</p></td>
</tr>
<tr class="odd">
<td><code>urlContext</code></td>
<td><p><code>object ( </code><code>UrlContext</code><code> )</code></p>
<p>Optional. Tool to support URL context retrieval.</p></td>
</tr>
<tr class="even">
<td><code>computerUse</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.ComputerUse"><code>ComputerUse</code></a><code> )</code></p>
<p>Optional. Tool to support the model interacting directly with the computer. If enabled, it automatically populates computer-use specific Function Declarations.</p></td>
</tr>
</tbody>
</table>

### FunctionDeclaration

**JSON representation**

```
{
  "name": string,
  "description": string,
  "parameters": {
    object (Schema)
  },
  "parametersJsonSchema": value,
  "response": {
    object (Schema)
  },
  "responseJsonSchema": value
}
```

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Fields</th>
<th></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code>name</code></td>
<td><p><code>string</code></p>
<p>Required. The name of the function to call. Must start with a letter or an underscore. Must be a-z, A-Z, 0-9, or contain underscores, dots, colons and dashes, with a maximum length of 128.</p></td>
</tr>
<tr class="even">
<td><code>description</code></td>
<td><p><code>string</code></p>
<p>Optional. Description and purpose of the function. Model uses it to decide how and whether to call the function.</p></td>
</tr>
<tr class="odd">
<td><code>parameters</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.Schema"><code>Schema</code></a><code> )</code></p>
<p>Optional. Describes the parameters to this function in JSON Schema Object format. Reflects the Open API 3.03 Parameter Object. string Key: the name of the parameter. Parameter names are case sensitive. Schema Value: the Schema defining the type used for the parameter. For function with no parameters, this can be left unset. Parameter names must start with a letter or an underscore and must only contain chars a-z, A-Z, 0-9, or underscores with a maximum length of 64. Example with 1 required and 1 optional parameter: type: OBJECT properties: param1: type: STRING param2: type: INTEGER required: - param1</p></td>
</tr>
<tr class="even">
<td><code>parametersJsonSchema</code></td>
<td><p><code>value ( </code><a href="https://protobuf.dev/reference/protobuf/google.protobuf/#value"><code>Value</code></a><code> format)</code></p>
<p>Optional. Describes the parameters to the function in JSON Schema format. The schema must describe an object where the properties are the parameters to the function. For example:</p>
<pre data-fenced=""><code>{
  &quot;type&quot;: &quot;object&quot;,
  &quot;properties&quot;: {
    &quot;name&quot;: { &quot;type&quot;: &quot;string&quot; },
    &quot;age&quot;: { &quot;type&quot;: &quot;integer&quot; }
  },
  &quot;additionalProperties&quot;: false,
  &quot;required&quot;: [&quot;name&quot;, &quot;age&quot;],
  &quot;propertyOrdering&quot;: [&quot;name&quot;, &quot;age&quot;]
}</code></pre>
<p>This field is mutually exclusive with <code>parameters</code> .</p></td>
</tr>
<tr class="odd">
<td><code>response</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.Schema"><code>Schema</code></a><code> )</code></p>
<p>Optional. Describes the output from this function in JSON Schema format. Reflects the Open API 3.03 Response Object. The Schema defines the type used for the response value of the function.</p></td>
</tr>
<tr class="even">
<td><code>responseJsonSchema</code></td>
<td><p><code>value ( </code><a href="https://protobuf.dev/reference/protobuf/google.protobuf/#value"><code>Value</code></a><code> format)</code></p>
<p>Optional. Describes the output from this function in JSON Schema format. The value specified by the schema is the response value of the function.</p>
<p>This field is mutually exclusive with <code>response</code> .</p></td>
</tr>
</tbody>
</table>

### Retrieval

**JSON representation**

```
{
  "disableAttribution": boolean,

  // Union field source can be only one of the following:
  "vertexAiSearch": {
    object (VertexAISearch)
  },
  "vertexRagStore": {
    object (VertexRagStore)
  }
  // End of list of possible types for union field source.
}
```

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Fields</th>
<th></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code>disableAttribution </code><strong><code>(deprecated)</code></strong></td>
<td><p><code>boolean</code></p>
<blockquote>
<p>This item is deprecated!</p>
</blockquote>
<p>Optional. Deprecated. This option is no longer supported.</p></td>
</tr>
<tr class="even">
<td>Union field <code>source</code> . The source of the retrieval. <code>source</code> can be only one of the following:</td>
<td></td>
</tr>
<tr class="odd">
<td><code>vertexAiSearch</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.VertexAISearch"><code>VertexAISearch</code></a><code> )</code></p>
<p>Set to use data source powered by Agent Platform Search.</p></td>
</tr>
<tr class="even">
<td><code>vertexRagStore</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.VertexRagStore"><code>VertexRagStore</code></a><code> )</code></p>
<p>Set to use data source powered by Vertex RAG store. User data is uploaded via the VertexRagDataService.</p></td>
</tr>
</tbody>
</table>

### VertexAISearch

**JSON representation**

```
{
  "datastore": string,
  "engine": string,
  "maxResults": integer,
  "filter": string,
  "dataStoreSpecs": [
    {
      object (DataStoreSpec)
    }
  ]
}
```

| Fields             |                                                                                                                                                                                                                                                                                                                                                                                                     |
|--------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `datastore`        | `string` Optional. Fully-qualified Agent Platform Search data store resource ID. Format: `projects/{project}/locations/{location}/collections/{collection}/dataStores/{dataStore}`                                                                                                                                                                                                                  |
| `engine`           | `string` Optional. Fully-qualified Agent Platform Search engine resource ID. Format: `projects/{project}/locations/{location}/collections/{collection}/engines/{engine}`                                                                                                                                                                                                                            |
| `maxResults`       | `integer` Optional. Number of search results to return per query. The default value is 10. The maximumm allowed value is 10.                                                                                                                                                                                                                                                                        |
| `filter`           | `string` Optional. Filter strings to be passed to the search API.                                                                                                                                                                                                                                                                                                                                   |
| `dataStoreSpecs[]` | `object ( `[`DataStoreSpec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.DataStoreSpec)` )` Specifications that define the specific DataStores to be searched, along with configurations for those data stores. This is only considered for Engines with multiple data stores. It should only be set if engine is used. |

### DataStoreSpec

**JSON representation**

```
{
  "dataStore": string,
  "filter": string
}
```

| Fields      |                                                                                                                                                                                                                                                 |
|-------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `dataStore` | `string` Full resource name of DataStore, such as Format: `projects/{project}/locations/{location}/collections/{collection}/dataStores/{dataStore}`                                                                                             |
| `filter`    | `string` Optional. Filter specification to filter documents in the data store specified by data_store field. For more information on filtering, see [Filtering](https://cloud.google.com/generative-ai-app-builder/docs/filter-search-metadata) |

### VertexRagStore

**JSON representation**

```
{
  "ragCorpora": [
    string
  ],
  "ragResources": [
    {
      object (RagResource)
    }
  ],
  "ragRetrievalConfig": {
    object (RagRetrievalConfig)
  },
  "storeContext": boolean,

  // Union field _similarity_top_k can be only one of the following:
  "similarityTopK": integer
  // End of list of possible types for union field _similarity_top_k.

  // Union field _vector_distance_threshold can be only one of the following:
  "vectorDistanceThreshold": number
  // End of list of possible types for union field _vector_distance_threshold.
}
```

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Fields</th>
<th></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code>ragCorpora[] </code><strong><code>(deprecated)</code></strong></td>
<td><p><code>string</code></p>
<blockquote>
<p>This item is deprecated!</p>
</blockquote>
<p>Optional. Deprecated. Please use rag_resources instead.</p></td>
</tr>
<tr class="even">
<td><code>ragResources[]</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.RagResource"><code>RagResource</code></a><code> )</code></p>
<p>Optional. The representation of the rag source. It can be used to specify corpus only or ragfiles. Currently only support one corpus or multiple files from one corpus. In the future we may open up multiple corpora support.</p></td>
</tr>
<tr class="odd">
<td><code>ragRetrievalConfig</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.RagRetrievalConfig"><code>RagRetrievalConfig</code></a><code> )</code></p>
<p>Optional. The retrieval config for the Rag query.</p></td>
</tr>
<tr class="even">
<td><code>storeContext</code></td>
<td><p><code>boolean</code></p>
<p>Optional. Currently only supported for Gemini Multimodal Live API.</p>
<p>In Gemini Multimodal Live API, if <code>store_context</code> bool is specified, Gemini will leverage it to automatically memorize the interactions between the client and Gemini, and retrieve context when needed to augment the response generation for users' ongoing and future interactions.</p></td>
</tr>
<tr class="odd">
<td><p>Union field <code>_similarity_top_k</code> .</p>
<p><code>_similarity_top_k</code> can be only one of the following:</p></td>
<td></td>
</tr>
<tr class="even">
<td><code>similarityTopK </code><strong><code>(deprecated)</code></strong></td>
<td><p><code>integer</code></p>
<blockquote>
<p>This item is deprecated!</p>
</blockquote>
<p>Optional. Number of top k results to return from the selected corpora.</p></td>
</tr>
<tr class="odd">
<td><p>Union field <code>_vector_distance_threshold</code> .</p>
<p><code>_vector_distance_threshold</code> can be only one of the following:</p></td>
<td></td>
</tr>
<tr class="even">
<td><code>vectorDistanceThreshold </code><strong><code>(deprecated)</code></strong></td>
<td><p><code>number</code></p>
<blockquote>
<p>This item is deprecated!</p>
</blockquote>
<p>Optional. Only return results with vector distance smaller than the threshold.</p></td>
</tr>
</tbody>
</table>

### RagResource

**JSON representation**

```
{
  "ragCorpus": string,
  "ragFileIds": [
    string
  ]
}
```

| Fields         |                                                                                                                        |
|----------------|------------------------------------------------------------------------------------------------------------------------|
| `ragCorpus`    | `string` Optional. RagCorpora resource name. Format: `projects/{project}/locations/{location}/ragCorpora/{rag_corpus}` |
| `ragFileIds[]` | `string` Optional. rag_file_id. The files should be in the same rag_corpus set in rag_corpus field.                    |

### RagRetrievalConfig

**JSON representation**

```
{
  "topK": integer,
  "hybridSearch": {
    object (HybridSearch)
  },
  "filter": {
    object (Filter)
  },
  "ranking": {
    object (Ranking)
  }
}
```

| Fields         |                                                                                                                                                                                                           |
|----------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `topK`         | `integer` Optional. The number of contexts to retrieve.                                                                                                                                                   |
| `hybridSearch` | `object ( `[`HybridSearch`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.HybridSearch)` )` Optional. Config for Hybrid Search. |
| `filter`       | `object ( `[`Filter`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.Filter)` )` Optional. Config for filters.                   |
| `ranking`      | `object ( `[`Ranking`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.Ranking)` )` Optional. Config for ranking and reranking.   |

### HybridSearch

**JSON representation**

```
{

  // Union field _alpha can be only one of the following:
  "alpha": number
  // End of list of possible types for union field _alpha.
}
```

| Fields                                                            |                                                                                                                                                                                                                                                                                         |
|-------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Union field `_alpha` . `_alpha` can be only one of the following: |                                                                                                                                                                                                                                                                                         |
| `alpha`                                                           | `number` Optional. Alpha value controls the weight between dense and sparse vector search results. The range is \[0, 1\], while 0 means sparse vector search only and 1 means dense vector search only. The default value is 0.5 which balances sparse and dense vector search equally. |

### Filter

**JSON representation**

```
{
  "metadataFilter": string,

  // Union field vector_db_threshold can be only one of the following:
  "vectorDistanceThreshold": number,
  "vectorSimilarityThreshold": number
  // End of list of possible types for union field vector_db_threshold.
}
```

| Fields                                                                                                                                                                                         |                                                                                            |
|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------|
| `metadataFilter`                                                                                                                                                                               | `string` Optional. String for metadata filtering.                                          |
| Union field `vector_db_threshold` . Filter contexts retrieved from the vector DB based on either vector distance or vector similarity. `vector_db_threshold` can be only one of the following: |                                                                                            |
| `vectorDistanceThreshold`                                                                                                                                                                      | `number` Optional. Only returns contexts with vector distance smaller than the threshold.  |
| `vectorSimilarityThreshold`                                                                                                                                                                    | `number` Optional. Only returns contexts with vector similarity larger than the threshold. |

### Ranking

**JSON representation**

```
{

  // Union field ranking_config can be only one of the following:
  "rankService": {
    object (RankService)
  },
  "llmRanker": {
    object (LlmRanker)
  }
  // End of list of possible types for union field ranking_config.
}
```

| Fields                                                                                                                                                  |                                                                                                                                                                                                        |
|---------------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Union field `ranking_config` . Config options for ranking. Currently only Rank Service is supported. `ranking_config` can be only one of the following: |                                                                                                                                                                                                        |
| `rankService`                                                                                                                                           | `object ( `[`RankService`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.RankService)` )` Optional. Config for Rank Service. |
| `llmRanker`                                                                                                                                             | `object ( `[`LlmRanker`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.LlmRanker)` )` Optional. Config for LlmRanker.        |

### RankService

**JSON representation**

```
{

  // Union field _model_name can be only one of the following:
  "modelName": string
  // End of list of possible types for union field _model_name.
}
```

| Fields                                                                      |                                                                                             |
|-----------------------------------------------------------------------------|---------------------------------------------------------------------------------------------|
| Union field `_model_name` . `_model_name` can be only one of the following: |                                                                                             |
| `modelName`                                                                 | `string` Optional. The model name of the rank service. Format: `semantic-ranker-512@latest` |

### LlmRanker

**JSON representation**

```
{

  // Union field _model_name can be only one of the following:
  "modelName": string
  // End of list of possible types for union field _model_name.
}
```

| Fields                                                                      |                                                                                                                                                                                |
|-----------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Union field `_model_name` . `_model_name` can be only one of the following: |                                                                                                                                                                                |
| `modelName`                                                                 | `string` Optional. The model name used for ranking. See [Supported models](https://cloud.google.com/vertex-ai/generative-ai/docs/model-reference/inference#supported-models) . |

### GoogleSearch

**JSON representation**

```
{
  "excludeDomains": [
    string
  ],

  // Union field _blocking_confidence can be only one of the following:
  "blockingConfidence": enum (PhishBlockThreshold)
  // End of list of possible types for union field _blocking_confidence.
}
```

| Fields                                                                                        |                                                                                                                                                                                                                                                                                            |
|-----------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `excludeDomains[]`                                                                            | `string` Optional. List of domains to be excluded from the search results. The default limit is 2000 domains. Example: \["amazon.com", "facebook.com"\].                                                                                                                                   |
| Union field `_blocking_confidence` . `_blocking_confidence` can be only one of the following: |                                                                                                                                                                                                                                                                                            |
| `blockingConfidence`                                                                          | `enum ( `[`PhishBlockThreshold`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.PhishBlockThreshold)` )` Optional. Sites with confidence level chosen & above this value will be blocked from the search results. |

### GoogleSearchRetrieval

**JSON representation**

```
{
  "dynamicRetrievalConfig": {
    object (DynamicRetrievalConfig)
  }
}
```

| Fields                   |                                                                                                                                                                                                                                                               |
|--------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `dynamicRetrievalConfig` | `object ( `[`DynamicRetrievalConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.DynamicRetrievalConfig)` )` Specifies the dynamic retrieval configuration for the given source. |

### DynamicRetrievalConfig

**JSON representation**

```
{
  "mode": enum (Mode),

  // Union field _dynamic_threshold can be only one of the following:
  "dynamicThreshold": number
  // End of list of possible types for union field _dynamic_threshold.
}
```

| Fields                                                                                    |                                                                                                                                                                                                                |
|-------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `mode`                                                                                    | `enum ( `[`Mode`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.Mode)` )` The mode of the predictor to be used in dynamic retrieval. |
| Union field `_dynamic_threshold` . `_dynamic_threshold` can be only one of the following: |                                                                                                                                                                                                                |
| `dynamicThreshold`                                                                        | `number` Optional. The threshold to be used in dynamic retrieval. If not set, a system default value is used.                                                                                                  |

### GoogleMaps

**JSON representation**

```
{
  "enableWidget": boolean,
  "groundingTypes": {
    object (GroundingTypes)
  }
}
```

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Fields</th>
<th></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code>enableWidget </code><strong><code>(deprecated)</code></strong></td>
<td><p><code>boolean</code></p>
<blockquote>
<p>This item is deprecated!</p>
</blockquote>
<p>Optional. Deprecated: The Google Maps contextual widget behavior in Grounding with Google Maps is being deprecated; this field is planned for removal and no longer has any effect once removed.</p>
<p>If true, include the widget context token in the response.</p></td>
</tr>
<tr class="even">
<td><code>groundingTypes</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.GroundingTypes"><code>GroundingTypes</code></a><code> )</code></p>
<p>Optional. Specifies the types of Google Maps grounding to enable. Defaults to <code>places</code> when unset.</p></td>
</tr>
</tbody>
</table>

### GroundingTypes

**JSON representation**

```
{
  "places": {
    object (Places)
  },
  "routing": {
    object (Routing)
  }
}
```

| Fields    |                                                                                                                                                         |
|-----------|---------------------------------------------------------------------------------------------------------------------------------------------------------|
| `places`  | `object ( ``Places`` )` Optional. Enables grounding with Google Maps Places. This is the default grounding type when no `GroundingTypes` are specified. |
| `routing` | `object ( ``Routing`` )` Optional. Enables grounding with Google Maps Routing APIs (ComputeRoutes and SearchAlongRoute).                                |

### EnterpriseWebSearch

**JSON representation**

```
{
  "excludeDomains": [
    string
  ],

  // Union field _blocking_confidence can be only one of the following:
  "blockingConfidence": enum (PhishBlockThreshold)
  // End of list of possible types for union field _blocking_confidence.
}
```

| Fields                                                                                        |                                                                                                                                                                                                                                                                                            |
|-----------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `excludeDomains[]`                                                                            | `string` Optional. List of domains to be excluded from the search results. The default limit is 2000 domains.                                                                                                                                                                              |
| Union field `_blocking_confidence` . `_blocking_confidence` can be only one of the following: |                                                                                                                                                                                                                                                                                            |
| `blockingConfidence`                                                                          | `enum ( `[`PhishBlockThreshold`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.PhishBlockThreshold)` )` Optional. Sites with confidence level chosen & above this value will be blocked from the search results. |

### ParallelAiSearch

**JSON representation**

```
{
  "apiKey": string,
  "customConfigs": {
    object
  }
}
```

| Fields          |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
|-----------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `apiKey`        | `string` Optional. The API key for ParallelAiSearch. If an API key is not provided, the system will attempt to verify access by checking for an active Parallel.ai subscription through the Google Cloud Marketplace. See <https://docs.parallel.ai/search/search-quickstart> for more details.                                                                                                                                                                                                                                                                                                                                                                                       |
| `customConfigs` | `object ( `[`Struct`](https://protobuf.dev/reference/protobuf/google.protobuf/#struct)` format)` Optional. Custom configs for ParallelAiSearch. This field can be used to pass any parameter from the Parallel.ai Search API. See the Parallel.ai documentation for the full list of available parameters and their usage: <https://docs.parallel.ai/api-reference/search-beta/search> Currently only `source_policy` , `excerpts` , `max_results` , `mode` , `fetch_policy` can be set via this field. For example: { "source_policy": { "include_domains": \["google.com", "wikipedia.org"\], "exclude_domains": \["example.com"\] }, "fetch_policy": { "max_age_seconds": 3600 } } |

### ComputerUse

**JSON representation**

```
{
  "environment": enum (Environment),
  "excludedPredefinedFunctions": [
    string
  ]
}
```

| Fields                          |                                                                                                                                                                                                                                                                                                                                                                                                                     |
|---------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `environment`                   | `enum ( `[`Environment`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.Environment)` )` Required. The environment being operated.                                                                                                                                                                                                         |
| `excludedPredefinedFunctions[]` | `string` Optional. By default, [predefined functions](https://cloud.google.com/vertex-ai/generative-ai/docs/computer-use#supported-actions) are included in the final model call. Some of them can be explicitly excluded from being automatically included. This can serve two purposes: 1. Using a more restricted / different action space. 2. Improving the definitions / instructions of predefined functions. |

### Events

**JSON representation**

```
{
  "event": [
    {
      object (Content)
    }
  ]
}
```

| Fields    |                                                                                                                                                                                         |
|-----------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `event[]` | `object ( `[`Content`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.Content)` )` Optional. A list of events. |

### AgentsEntry

**JSON representation**

```
{
  "key": string,
  "value": {
    object (DeprecatedAgentConfig)
  }
}
```

| Fields  |                                                                                                                                                                                         |
|---------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `key`   | `string`                                                                                                                                                                                |
| `value` | `object ( `[`DeprecatedAgentConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.DeprecatedAgentConfig)` )` |

### DeprecatedAgentConfig

**JSON representation**

```
{
  "agentId": string,
  "agentType": string,
  "description": string,
  "subAgents": [
    string
  ],
  "developerInstruction": {
    object (InstanceData)
  },

  // Union field tools_data can be only one of the following:
  "toolsText": string,
  "tools": {
    object (Tools)
  }
  // End of list of possible types for union field tools_data.
}
```

| Fields                                                                                                               |                                                                                                                                                                                                                                                                                                                                  |
|----------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `agentId`                                                                                                            | `string` Optional. Unique identifier of the agent. This ID is used to refer to this agent, e.g., in AgentEvent.author, or in the `sub_agents` field. It must be unique within the `agents` map.                                                                                                                                  |
| `agentType`                                                                                                          | `string` Optional. The type or class of the agent (e.g., "LlmAgent", "RouterAgent", "ToolUseAgent"). Useful for the autorater to understand the expected behavior of the agent.                                                                                                                                                  |
| `description`                                                                                                        | `string` Optional. A high-level description of the agent's role and responsibilities. Critical for evaluating if the agent is routing tasks correctly.                                                                                                                                                                           |
| `subAgents[]`                                                                                                        | `string` Optional. The list of valid agent IDs (names) that this agent can delegate to. This defines the directed edges in the agent system graph topology.                                                                                                                                                                      |
| `developerInstruction`                                                                                               | `object ( `[`InstanceData`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.InstanceData)` )` Optional. Contains instructions from the developer for the agent. Can be static or a dynamic prompt template used with the `AgentEvent.state_delta` field. |
| Union field `tools_data` . Data for the tools available to the agent. `tools_data` can be only one of the following: |                                                                                                                                                                                                                                                                                                                                  |
| `toolsText`                                                                                                          | `string` A JSON string containing a list of tools available to an agent with info such as name, description, parameters and required parameters.                                                                                                                                                                                 |
| `tools`                                                                                                              | `object ( `[`Tools`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.Tools_1)` )` List of tools.                                                                                                                                                         |

### Tools

**JSON representation**

```
{
  "tool": [
    {
      object (Tool)
    }
  ]
}
```

| Fields   |                                                                                                                                                                                                                                   |
|----------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `tool[]` | `object ( `[`Tool`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.Tool)` )` Optional. List of tools: each tool can have multiple function declarations. |

### ConversationTurn

**JSON representation**

```
{
  "turnId": string,
  "events": [
    {
      object (AgentEvent)
    }
  ],

  // Union field _turn_index can be only one of the following:
  "turnIndex": integer
  // End of list of possible types for union field _turn_index.
}
```

| Fields                                                                      |                                                                                                                                                                                                                                |
|-----------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `turnId`                                                                    | `string` Optional. A unique identifier for the turn. Useful for referencing specific turns across systems.                                                                                                                     |
| `events[]`                                                                  | `object ( `[`AgentEvent`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.AgentEvent)` )` Optional. The list of events that occurred during this turn. |
| Union field `_turn_index` . `_turn_index` can be only one of the following: |                                                                                                                                                                                                                                |
| `turnIndex`                                                                 | `integer` Required. The 0-based index of the turn in the conversation sequence.                                                                                                                                                |

### AgentEvent

**JSON representation**

```
{
  "content": {
    object (Content)
  },
  "eventTime": string,
  "stateDelta": {
    object
  },
  "activeTools": [
    {
      object (Tool)
    }
  ],

  // Union field _author can be only one of the following:
  "author": string
  // End of list of possible types for union field _author.
}
```

| Fields                                                              |                                                                                                                                                                                                                                                                                                                                                                                                                        |
|---------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `content`                                                           | `object ( `[`Content`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.Content)` )` Required. The content of the event (e.g., text response, tool call, tool response).                                                                                                                                                                        |
| `eventTime`                                                         | `string ( `[`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp)` format)` Optional. The timestamp when the event occurred. Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` . |
| `stateDelta`                                                        | `object ( `[`Struct`](https://protobuf.dev/reference/protobuf/google.protobuf/#struct)` format)` Optional. The change in the session state caused by this event. This is a key-value map of fields that were modified or added by the event.                                                                                                                                                                           |
| `activeTools[]`                                                     | `object ( `[`Tool`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.Tool)` )` Optional. The list of tools that were active/available to the agent at the time of this event. This overrides the `AgentConfig.tools` if set.                                                                                                                    |
| Union field `_author` . `_author` can be only one of the following: |                                                                                                                                                                                                                                                                                                                                                                                                                        |
| `author`                                                            | `string` Required. The ID of the agent or entity that generated this event.                                                                                                                                                                                                                                                                                                                                            |

### Timestamp

**JSON representation**

```
{
  "seconds": string,
  "nanos": integer
}
```

| Fields    |                                                                                                                                                                                                                                                                                                                      |
|-----------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `seconds` | `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)` Represents seconds of UTC time since Unix epoch 1970-01-01T00:00:00Z. Must be between -62135596800 and 253402300799 inclusive (which corresponds to 0001-01-01T00:00:00Z to 9999-12-31T23:59:59Z).                            |
| `nanos`   | `integer` Non-negative fractions of a second at nanosecond resolution. This field is the nanosecond portion of the duration, not an alternative to seconds. Negative second values with fractions must still have non-negative nanos values that count forward in time. Must be between 0 and 999,999,999 inclusive. |

### AgentData

**JSON representation**

```
{
  "agents": {
    string: {
      object (AgentConfig)
    },
    ...
  },
  "turns": [
    {
      object (ConversationTurn)
    }
  ]
}
```

| Fields    |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
|-----------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `agents`  | `map (key: string, value: object ( `[`AgentConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.AgentConfig)` ))` Optional. A map containing the static configurations for each agent in the system. Key: agent_id (matches the `author` field in events). Value: The static configuration of the agent. An object containing a list of `"key": value` pairs. Example: `{ "name": "wrench", "mass": "1.3kg", "count": "3" }` . |
| `turns[]` | `object ( `[`ConversationTurn`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.ConversationTurn_1)` )` Optional. A chronological list of conversation turns. Each turn represents a logical execution cycle (e.g., User Input -\> Agent Response).                                                                                                                                                                                |

### AgentsEntry

**JSON representation**

```
{
  "key": string,
  "value": {
    object (AgentConfig)
  }
}
```

| Fields  |                                                                                                                                                                     |
|---------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `key`   | `string`                                                                                                                                                            |
| `value` | `object ( `[`AgentConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.AgentConfig)` )` |

### AgentConfig

**JSON representation**

```
{
  "agentType": string,
  "description": string,
  "instruction": string,
  "tools": [
    {
      object (Tool)
    }
  ],
  "subAgents": [
    string
  ],

  // Union field _agent_id can be only one of the following:
  "agentId": string
  // End of list of possible types for union field _agent_id.
}
```

| Fields                                                                  |                                                                                                                                                                                                                                                                   |
|-------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `agentType`                                                             | `string` Optional. The type or class of the agent (e.g., "LlmAgent", "RouterAgent", "ToolUseAgent"). Useful for the autorater to understand the expected behavior of the agent.                                                                                   |
| `description`                                                           | `string` Optional. A high-level description of the agent's role and responsibilities. Critical for evaluating if the agent is routing tasks correctly.                                                                                                            |
| `instruction`                                                           | `string` Optional. Provides instructions for the LLM model, guiding the agent's behavior. Can be static or dynamic. Dynamic instructions can contain placeholders like {variable_name} that will be resolved at runtime using the `AgentEvent.state_delta` field. |
| `tools[]`                                                               | `object ( `[`Tool`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.Tool)` )` Optional. The list of tools available to this agent.                                                        |
| `subAgents[]`                                                           | `string` Optional. The list of valid agent IDs that this agent can delegate to. This defines the directed edges in the multi-agent system graph topology.                                                                                                         |
| Union field `_agent_id` . `_agent_id` can be only one of the following: |                                                                                                                                                                                                                                                                   |
| `agentId`                                                               | `string` Required. Unique identifier of the agent. This ID is used to refer to this agent, e.g., in AgentEvent.author, or in the `sub_agents` field. It must be unique within the `agents` map.                                                                   |

### ConversationTurn

**JSON representation**

```
{
  "turnId": string,
  "events": [
    {
      object (AgentEvent)
    }
  ],

  // Union field _turn_index can be only one of the following:
  "turnIndex": integer
  // End of list of possible types for union field _turn_index.
}
```

| Fields                                                                      |                                                                                                                                                                                                                                  |
|-----------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `turnId`                                                                    | `string` Optional. A unique identifier for the turn. Useful for referencing specific turns across systems.                                                                                                                       |
| `events[]`                                                                  | `object ( `[`AgentEvent`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.AgentEvent_1)` )` Optional. The list of events that occurred during this turn. |
| Union field `_turn_index` . `_turn_index` can be only one of the following: |                                                                                                                                                                                                                                  |
| `turnIndex`                                                                 | `integer` Required. The 0-based index of the turn in the conversation sequence.                                                                                                                                                  |

### AgentEvent

**JSON representation**

```
{
  "eventTime": string,
  "stateDelta": {
    object
  },
  "activeTools": [
    {
      object (Tool)
    }
  ],

  // Union field _author can be only one of the following:
  "author": string
  // End of list of possible types for union field _author.

  // Union field _content can be only one of the following:
  "content": {
    object (Content)
  }
  // End of list of possible types for union field _content.
}
```

| Fields                                                                |                                                                                                                                                                                                                                                                                                                                                                                                                        |
|-----------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `eventTime`                                                           | `string ( `[`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp)` format)` Optional. The timestamp when the event occurred. Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` . |
| `stateDelta`                                                          | `object ( `[`Struct`](https://protobuf.dev/reference/protobuf/google.protobuf/#struct)` format)` Optional. The change in the session state caused by this event. This is a key-value map of fields that were modified or added by the event.                                                                                                                                                                           |
| `activeTools[]`                                                       | `object ( `[`Tool`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.Tool)` )` Optional. The list of tools that were active/available to the agent at the time of this event. This overrides the `AgentConfig.tools` if set.                                                                                                                    |
| Union field `_author` . `_author` can be only one of the following:   |                                                                                                                                                                                                                                                                                                                                                                                                                        |
| `author`                                                              | `string` Required. The ID of the agent or entity that generated this event. Use "user" to denote events generated by the end-user.                                                                                                                                                                                                                                                                                     |
| Union field `_content` . `_content` can be only one of the following: |                                                                                                                                                                                                                                                                                                                                                                                                                        |
| `content`                                                             | `object ( `[`Content`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.Content)` )` Required. The content of the event (e.g., text response, tool call, tool response).                                                                                                                                                                        |

### NullValue

Represents a JSON `null` .

`NullValue` is a sentinel, using an enum with only one value to represent the null value for the `Value` type union.

A field of type `NullValue` with any value other than `0` is considered invalid. Most ProtoJSON serializers will emit a `Value` with a `null_value` set as a JSON `null` regardless of the integer value, and so will round trip to a `0` value.

| Enums        |             |
|--------------|-------------|
| `NULL_VALUE` | Null value. |

### Language

Supported programming languages for the generated code.

| Enums                  |                                                      |
|------------------------|------------------------------------------------------|
| `LANGUAGE_UNSPECIFIED` | Unspecified language. This value should not be used. |
| `PYTHON`               | Python \>= 3.10, with numpy and simpy available.     |

### Outcome

Enumeration of possible outcomes of the code execution.

| Enums                       |                                                                                                         |
|-----------------------------|---------------------------------------------------------------------------------------------------------|
| `OUTCOME_UNSPECIFIED`       | Unspecified status. This value should not be used.                                                      |
| `OUTCOME_OK`                | Code execution completed successfully. `output` contains the stdout, if any.                            |
| `OUTCOME_FAILED`            | Code execution failed. `output` contains the stderr and stdout, if any.                                 |
| `OUTCOME_DEADLINE_EXCEEDED` | Code execution ran for too long, and was cancelled. There may or may not be a partial `output` present. |

### Level

The media resolution level.

| Enums                          |                                                             |
|--------------------------------|-------------------------------------------------------------|
| `MEDIA_RESOLUTION_UNSPECIFIED` | Media resolution has not been set.                          |
| `MEDIA_RESOLUTION_LOW`         | Media resolution set to low.                                |
| `MEDIA_RESOLUTION_MEDIUM`      | Media resolution set to medium.                             |
| `MEDIA_RESOLUTION_HIGH`        | Media resolution set to high.                               |
| `MEDIA_RESOLUTION_ULTRA_HIGH`  | Media resolution set to ultra high. This is for image only. |

### CometVersion

Comet version options.

| Enums                       |                                                                            |
|-----------------------------|----------------------------------------------------------------------------|
| `COMET_VERSION_UNSPECIFIED` | Comet version unspecified.                                                 |
| `COMET_22_SRC_REF`          | Comet 22 for translation + source + reference (source-reference-combined). |

### MetricxVersion

MetricX Version options.

| Enums                         |                                                                                      |
|-------------------------------|--------------------------------------------------------------------------------------|
| `METRICX_VERSION_UNSPECIFIED` | MetricX version unspecified.                                                         |
| `METRICX_24_REF`              | MetricX 2024 (2.6) for translation + reference (reference-based).                    |
| `METRICX_24_SRC`              | MetricX 2024 (2.6) for translation + source (QE).                                    |
| `METRICX_24_SRC_REF`          | MetricX 2024 (2.6) for translation + source + reference (source-reference-combined). |

### ComputationBasedMetricType

Types of computation based metrics.

| Enums                                       |                                            |
|---------------------------------------------|--------------------------------------------|
| `COMPUTATION_BASED_METRIC_TYPE_UNSPECIFIED` | Unspecified computation based metric type. |
| `EXACT_MATCH`                               | Exact match metric.                        |
| `BLEU`                                      | BLEU metric.                               |
| `ROUGE`                                     | ROUGE metric.                              |

### Type

Type contains the list of OpenAPI data types as defined by <https://swagger.io/docs/specification/data-models/data-types/>

| Enums              |                                    |
|--------------------|------------------------------------|
| `TYPE_UNSPECIFIED` | Not specified, should not be used. |
| `STRING`           | OpenAPI string type                |
| `NUMBER`           | OpenAPI number type                |
| `INTEGER`          | OpenAPI integer type               |
| `BOOLEAN`          | OpenAPI boolean type               |
| `ARRAY`            | OpenAPI array type                 |
| `OBJECT`           | OpenAPI object type                |
| `NULL`             | Null type                          |

### ModelRoutingPreference

The model routing preference.

| Enums                |                                                                       |
|----------------------|-----------------------------------------------------------------------|
| `UNKNOWN`            | Unspecified model routing preference.                                 |
| `PRIORITIZE_QUALITY` | The model will be selected to prioritize the quality of the response. |
| `BALANCED`           | The model will be selected to balance quality and cost.               |
| `PRIORITIZE_COST`    | The model will be selected to prioritize the cost of the request.     |

### Modality

The modalities of the response.

| Enums                  |                                                  |
|------------------------|--------------------------------------------------|
| `MODALITY_UNSPECIFIED` | Unspecified modality. Will be processed as text. |
| `TEXT`                 | Text modality.                                   |
| `IMAGE`                | Image modality.                                  |
| `AUDIO`                | Audio modality.                                  |
| `VIDEO`                | Video modality.                                  |

### MediaResolution

Media resolution for the input media.

| Enums                          |                                                                  |
|--------------------------------|------------------------------------------------------------------|
| `MEDIA_RESOLUTION_UNSPECIFIED` | Media resolution has not been set.                               |
| `MEDIA_RESOLUTION_LOW`         | Media resolution set to low (64 tokens).                         |
| `MEDIA_RESOLUTION_MEDIUM`      | Media resolution set to medium (256 tokens).                     |
| `MEDIA_RESOLUTION_HIGH`        | Media resolution set to high (zoomed reframing with 256 tokens). |

### ThinkingLevel

The thinking level for the model.

| Enums                        |                             |
|------------------------------|-----------------------------|
| `THINKING_LEVEL_UNSPECIFIED` | Unspecified thinking level. |
| `LOW`                        | Low thinking level.         |
| `MEDIUM`                     | Medium thinking level.      |
| `HIGH`                       | High thinking level.        |
| `MINIMAL`                    | MINIMAL thinking level.     |

### FeatureSelectionPreference

Options for feature selection preference.

| Enums                                      |                                           |
|--------------------------------------------|-------------------------------------------|
| `FEATURE_SELECTION_PREFERENCE_UNSPECIFIED` | Unspecified feature selection preference. |
| `PRIORITIZE_QUALITY`                       | Prefer higher quality over lower cost.    |
| `BALANCED`                                 | Balanced feature selection preference.    |
| `PRIORITIZE_COST`                          | Prefer lower cost over higher quality.    |

### PersonGeneration

Enum for controlling the generation of people in images.

| Enums                           |                                                                                                  |
|---------------------------------|--------------------------------------------------------------------------------------------------|
| `PERSON_GENERATION_UNSPECIFIED` | The default behavior is unspecified. The model will decide whether to generate images of people. |
| `ALLOW_ALL`                     | Allows the model to generate images of people, including adults and children.                    |
| `ALLOW_ADULT`                   | Allows the model to generate images of adults, but not children.                                 |
| `ALLOW_NONE`                    | Prevents the model from generating images of people.                                             |

### MimeType

Supported MIME types for text output.

| Enums                   |                                      |
|-------------------------|--------------------------------------|
| `MIME_TYPE_UNSPECIFIED` | Default value. This value is unused. |
| `APPLICATION_JSON`      | JSON output format.                  |
| `TEXT_PLAIN`            | Plain text output format.            |

### MimeType

Supported MIME types for audio output.

| Enums                   |                                      |
|-------------------------|--------------------------------------|
| `MIME_TYPE_UNSPECIFIED` | Default value. This value is unused. |
| `AUDIO_MP3`             | MP3 audio format.                    |
| `AUDIO_OGG_OPUS`        | OGG Opus audio format.               |
| `AUDIO_L16`             | Raw PCM (L16) audio format.          |
| `AUDIO_WAV`             | WAV audio format.                    |
| `AUDIO_ALAW`            | A-law audio format.                  |
| `AUDIO_MULAW`           | Mu-law audio format.                 |

### DeliveryMode

The delivery mode for the output content.

| Enums                  |                                                      |
|------------------------|------------------------------------------------------|
| `DELIVERY_UNSPECIFIED` | Default value. This value is unused.                 |
| `INLINE`               | Generated bytes are returned inline in the response. |
| `URI`                  | Generated content is stored and a URI is returned.   |

### MimeType

Supported MIME types for image output.

| Enums                   |                                      |
|-------------------------|--------------------------------------|
| `MIME_TYPE_UNSPECIFIED` | Default value. This value is unused. |
| `IMAGE_JPEG`            | JPEG image format.                   |

### AspectRatio

Supported aspect ratios for image output.

| Enums                             |                                      |
|-----------------------------------|--------------------------------------|
| `ASPECT_RATIO_UNSPECIFIED`        | Default value. This value is unused. |
| `ASPECT_RATIO_ONE_BY_ONE`         | 1:1 aspect ratio.                    |
| `ASPECT_RATIO_TWO_BY_THREE`       | 2:3 aspect ratio.                    |
| `ASPECT_RATIO_THREE_BY_TWO`       | 3:2 aspect ratio.                    |
| `ASPECT_RATIO_THREE_BY_FOUR`      | 3:4 aspect ratio.                    |
| `ASPECT_RATIO_FOUR_BY_THREE`      | 4:3 aspect ratio.                    |
| `ASPECT_RATIO_FOUR_BY_FIVE`       | 4:5 aspect ratio.                    |
| `ASPECT_RATIO_FIVE_BY_FOUR`       | 5:4 aspect ratio.                    |
| `ASPECT_RATIO_NINE_BY_SIXTEEN`    | 9:16 aspect ratio.                   |
| `ASPECT_RATIO_SIXTEEN_BY_NINE`    | 16:9 aspect ratio.                   |
| `ASPECT_RATIO_TWENTY_ONE_BY_NINE` | 21:9 aspect ratio.                   |
| `ASPECT_RATIO_ONE_BY_EIGHT`       | 1:8 aspect ratio.                    |
| `ASPECT_RATIO_EIGHT_BY_ONE`       | 8:1 aspect ratio.                    |
| `ASPECT_RATIO_ONE_BY_FOUR`        | 1:4 aspect ratio.                    |
| `ASPECT_RATIO_FOUR_BY_ONE`        | 4:1 aspect ratio.                    |

### ImageSize

Supported image sizes for image output.

| Enums                    |                                      |
|--------------------------|--------------------------------------|
| `IMAGE_SIZE_UNSPECIFIED` | Default value. This value is unused. |
| `IMAGE_SIZE_FIVE_TWELVE` | 512px image size.                    |
| `IMAGE_SIZE_ONE_K`       | 1K image size.                       |
| `IMAGE_SIZE_TWO_K`       | 2K image size.                       |
| `IMAGE_SIZE_FOUR_K`      | 4K image size.                       |

### AspectRatio

Supported aspect ratios for video output.

| Enums                          |                                      |
|--------------------------------|--------------------------------------|
| `ASPECT_RATIO_UNSPECIFIED`     | Default value. This value is unused. |
| `ASPECT_RATIO_SIXTEEN_BY_NINE` | 16:9 aspect ratio.                   |
| `ASPECT_RATIO_NINE_BY_SIXTEEN` | 9:16 aspect ratio.                   |

### RubricContentType

Specifies the type of rubric content to generate.

| Enums                             |                                                   |
|-----------------------------------|---------------------------------------------------|
| `RUBRIC_CONTENT_TYPE_UNSPECIFIED` | The content type to generate is not specified.    |
| `PROPERTY`                        | Generate rubrics based on properties.             |
| `NL_QUESTION_ANSWER`              | Generate rubrics in an NL question answer format. |
| `PYTHON_CODE_ASSERTION`           | Generate rubrics in a unit test format.           |

### AggregationMetric

The per-metric statistics on evaluation results supported by `EvaluationService.EvaluateDataset` .

| Enums                            |                                                                           |
|----------------------------------|---------------------------------------------------------------------------|
| `AGGREGATION_METRIC_UNSPECIFIED` | Unspecified aggregation metric.                                           |
| `AVERAGE`                        | Average aggregation metric. Not supported for Pairwise metric.            |
| `MODE`                           | Mode aggregation metric.                                                  |
| `STANDARD_DEVIATION`             | Standard deviation aggregation metric. Not supported for pairwise metric. |
| `VARIANCE`                       | Variance aggregation metric. Not supported for pairwise metric.           |
| `MINIMUM`                        | Minimum aggregation metric. Not supported for pairwise metric.            |
| `MAXIMUM`                        | Maximum aggregation metric. Not supported for pairwise metric.            |
| `MEDIAN`                         | Median aggregation metric. Not supported for pairwise metric.             |
| `PERCENTILE_P90`                 | 90th percentile aggregation metric. Not supported for pairwise metric.    |
| `PERCENTILE_P95`                 | 95th percentile aggregation metric. Not supported for pairwise metric.    |
| `PERCENTILE_P99`                 | 99th percentile aggregation metric. Not supported for pairwise metric.    |

### Importance

Importance level of the rubric.

| Enums                    |                              |
|--------------------------|------------------------------|
| `IMPORTANCE_UNSPECIFIED` | Importance is not specified. |
| `HIGH`                   | High importance.             |
| `MEDIUM`                 | Medium importance.           |
| `LOW`                    | Low importance.              |

### PhishBlockThreshold

These are available confidence level user can set to block malicious urls with chosen confidence and above. For understanding different confidence of webrisk, please refer to <https://cloud.google.com/web-risk/docs/reference/rpc/google.cloud.webrisk.v1eap1#confidencelevel>

| Enums                               |                                                          |
|-------------------------------------|----------------------------------------------------------|
| `PHISH_BLOCK_THRESHOLD_UNSPECIFIED` | Defaults to unspecified.                                 |
| `BLOCK_LOW_AND_ABOVE`               | Blocks Low and above confidence URL that is risky.       |
| `BLOCK_MEDIUM_AND_ABOVE`            | Blocks Medium and above confidence URL that is risky.    |
| `BLOCK_HIGH_AND_ABOVE`              | Blocks High and above confidence URL that is risky.      |
| `BLOCK_HIGHER_AND_ABOVE`            | Blocks Higher and above confidence URL that is risky.    |
| `BLOCK_VERY_HIGH_AND_ABOVE`         | Blocks Very high and above confidence URL that is risky. |
| `BLOCK_ONLY_EXTREMELY_HIGH`         | Blocks Extremely high confidence URL that is risky.      |

### Mode

The mode of the predictor to be used in dynamic retrieval.

| Enums              |                                                         |
|--------------------|---------------------------------------------------------|
| `MODE_UNSPECIFIED` | Always trigger retrieval.                               |
| `MODE_DYNAMIC`     | Run retrieval only when system decides it is necessary. |

### Environment

Represents the environment being operated, such as a web browser.

| Enums                     |                            |
|---------------------------|----------------------------|
| `ENVIRONMENT_UNSPECIFIED` | Defaults to browser.       |
| `ENVIRONMENT_BROWSER`     | Operates in a web browser. |

## Output Schema

Response message for EvaluationService.EvaluateInstances.

### EvaluateInstancesResponse

**JSON representation**

```
{
  "metricResults": [
    {
      object (MetricResult)
    }
  ],

  // Union field evaluation_results can be only one of the following:
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
  },
  "rubricBasedInstructionFollowingResult": {
    object (RubricBasedInstructionFollowingResult)
  }
  // End of list of possible types for union field evaluation_results.
}
```

| Fields                                                                                                                                                                                     |                                                                                                                                                                                                                                                                                                                     |
|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `metricResults[]`                                                                                                                                                                          | `object ( `[`MetricResult`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Output.Schema.MetricResult)` )` Metric results for each instance. The order of the metric results is guaranteed to be the same as the order of the instances in the request. |
| Union field `evaluation_results` . Evaluation results will be served in the same order as presented in EvaluationRequest.instances. `evaluation_results` can be only one of the following: |                                                                                                                                                                                                                                                                                                                     |
| `exactMatchResults`                                                                                                                                                                        | `object ( `[`ExactMatchResults`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Output.Schema.ExactMatchResults)` )` Auto metric evaluation results. Results for exact match metric.                                                                    |
| `bleuResults`                                                                                                                                                                              | `object ( `[`BleuResults`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Output.Schema.BleuResults)` )` Results for bleu metric.                                                                                                                       |
| `rougeResults`                                                                                                                                                                             | `object ( `[`RougeResults`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Output.Schema.RougeResults)` )` Results for rouge metric.                                                                                                                    |
| `fluencyResult`                                                                                                                                                                            | `object ( `[`FluencyResult`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Output.Schema.FluencyResult)` )` LLM-based metric evaluation result. General text generation metrics, applicable to other categories. Result for fluency metric.            |
| `coherenceResult`                                                                                                                                                                          | `object ( `[`CoherenceResult`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Output.Schema.CoherenceResult)` )` Result for coherence metric.                                                                                                           |
| `safetyResult`                                                                                                                                                                             | `object ( `[`SafetyResult`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Output.Schema.SafetyResult)` )` Result for safety metric.                                                                                                                    |
| `groundednessResult`                                                                                                                                                                       | `object ( `[`GroundednessResult`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Output.Schema.GroundednessResult)` )` Result for groundedness metric.                                                                                                  |
| `fulfillmentResult`                                                                                                                                                                        | `object ( `[`FulfillmentResult`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Output.Schema.FulfillmentResult)` )` Result for fulfillment metric.                                                                                                     |
| `summarizationQualityResult`                                                                                                                                                               | `object ( `[`SummarizationQualityResult`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Output.Schema.SummarizationQualityResult)` )` Summarization only metrics. Result for summarization quality metric.                                             |
| `pairwiseSummarizationQualityResult`                                                                                                                                                       | `object ( `[`PairwiseSummarizationQualityResult`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Output.Schema.PairwiseSummarizationQualityResult)` )` Result for pairwise summarization quality metric.                                                |
| `summarizationHelpfulnessResult`                                                                                                                                                           | `object ( `[`SummarizationHelpfulnessResult`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Output.Schema.SummarizationHelpfulnessResult)` )` Result for summarization helpfulness metric.                                                             |
| `summarizationVerbosityResult`                                                                                                                                                             | `object ( `[`SummarizationVerbosityResult`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Output.Schema.SummarizationVerbosityResult)` )` Result for summarization verbosity metric.                                                                   |
| `questionAnsweringQualityResult`                                                                                                                                                           | `object ( `[`QuestionAnsweringQualityResult`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Output.Schema.QuestionAnsweringQualityResult)` )` Question answering only metrics. Result for question answering quality metric.                           |
| `pairwiseQuestionAnsweringQualityResult`                                                                                                                                                   | `object ( `[`PairwiseQuestionAnsweringQualityResult`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Output.Schema.PairwiseQuestionAnsweringQualityResult)` )` Result for pairwise question answering quality metric.                                   |
| `questionAnsweringRelevanceResult`                                                                                                                                                         | `object ( `[`QuestionAnsweringRelevanceResult`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Output.Schema.QuestionAnsweringRelevanceResult)` )` Result for question answering relevance metric.                                                      |
| `questionAnsweringHelpfulnessResult`                                                                                                                                                       | `object ( `[`QuestionAnsweringHelpfulnessResult`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Output.Schema.QuestionAnsweringHelpfulnessResult)` )` Result for question answering helpfulness metric.                                                |
| `questionAnsweringCorrectnessResult`                                                                                                                                                       | `object ( `[`QuestionAnsweringCorrectnessResult`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Output.Schema.QuestionAnsweringCorrectnessResult)` )` Result for question answering correctness metric.                                                |
| `pointwiseMetricResult`                                                                                                                                                                    | `object ( `[`PointwiseMetricResult`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Output.Schema.PointwiseMetricResult)` )` Generic metrics. Result for pointwise metric.                                                                              |
| `pairwiseMetricResult`                                                                                                                                                                     | `object ( `[`PairwiseMetricResult`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Output.Schema.PairwiseMetricResult)` )` Result for pairwise metric.                                                                                                  |
| `toolCallValidResults`                                                                                                                                                                     | `object ( `[`ToolCallValidResults`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Output.Schema.ToolCallValidResults)` )` Tool call metrics. Results for tool call valid metric.                                                                       |
| `toolNameMatchResults`                                                                                                                                                                     | `object ( `[`ToolNameMatchResults`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Output.Schema.ToolNameMatchResults)` )` Results for tool name match metric.                                                                                          |
| `toolParameterKeyMatchResults`                                                                                                                                                             | `object ( `[`ToolParameterKeyMatchResults`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Output.Schema.ToolParameterKeyMatchResults)` )` Results for tool parameter key match metric.                                                                 |
| `toolParameterKvMatchResults`                                                                                                                                                              | `object ( `[`ToolParameterKVMatchResults`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Output.Schema.ToolParameterKVMatchResults)` )` Results for tool parameter key value match metric.                                                             |
| `cometResult`                                                                                                                                                                              | `object ( `[`CometResult`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Output.Schema.CometResult)` )` Translation metrics. Result for Comet metric.                                                                                                  |
| `metricxResult`                                                                                                                                                                            | `object ( `[`MetricxResult`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Output.Schema.MetricxResult)` )` Result for Metricx metric.                                                                                                                 |
| `trajectoryExactMatchResults`                                                                                                                                                              | `object ( `[`TrajectoryExactMatchResults`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Output.Schema.TrajectoryExactMatchResults)` )` Result for trajectory exact match metric.                                                                      |
| `trajectoryInOrderMatchResults`                                                                                                                                                            | `object ( `[`TrajectoryInOrderMatchResults`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Output.Schema.TrajectoryInOrderMatchResults)` )` Result for trajectory in order match metric.                                                               |
| `trajectoryAnyOrderMatchResults`                                                                                                                                                           | `object ( `[`TrajectoryAnyOrderMatchResults`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Output.Schema.TrajectoryAnyOrderMatchResults)` )` Result for trajectory any order match metric.                                                            |
| `trajectoryPrecisionResults`                                                                                                                                                               | `object ( `[`TrajectoryPrecisionResults`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Output.Schema.TrajectoryPrecisionResults)` )` Result for trajectory precision metric.                                                                          |
| `trajectoryRecallResults`                                                                                                                                                                  | `object ( `[`TrajectoryRecallResults`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Output.Schema.TrajectoryRecallResults)` )` Results for trajectory recall metric.                                                                                  |
| `trajectorySingleToolUseResults`                                                                                                                                                           | `object ( `[`TrajectorySingleToolUseResults`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Output.Schema.TrajectorySingleToolUseResults)` )` Results for trajectory single tool use metric.                                                           |
| `rubricBasedInstructionFollowingResult`                                                                                                                                                    | `object ( `[`RubricBasedInstructionFollowingResult`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Output.Schema.RubricBasedInstructionFollowingResult)` )` Result for rubric based instruction following metric.                                      |

### ExactMatchResults

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

| Fields                     |                                                                                                                                                                                                                                  |
|----------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `exactMatchMetricValues[]` | `object ( `[`ExactMatchMetricValue`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Output.Schema.ExactMatchMetricValue)` )` Output only. Exact match metric values. |

### ExactMatchMetricValue

**JSON representation**

```
{

  // Union field _score can be only one of the following:
  "score": number
  // End of list of possible types for union field _score.
}
```

| Fields                                                            |                                          |
|-------------------------------------------------------------------|------------------------------------------|
| Union field `_score` . `_score` can be only one of the following: |                                          |
| `score`                                                           | `number` Output only. Exact match score. |

### BleuResults

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

| Fields               |                                                                                                                                                                                                               |
|----------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `bleuMetricValues[]` | `object ( `[`BleuMetricValue`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Output.Schema.BleuMetricValue)` )` Output only. Bleu metric values. |

### BleuMetricValue

**JSON representation**

```
{

  // Union field _score can be only one of the following:
  "score": number
  // End of list of possible types for union field _score.
}
```

| Fields                                                            |                                   |
|-------------------------------------------------------------------|-----------------------------------|
| Union field `_score` . `_score` can be only one of the following: |                                   |
| `score`                                                           | `number` Output only. Bleu score. |

### RougeResults

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

| Fields                |                                                                                                                                                                                                                  |
|-----------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `rougeMetricValues[]` | `object ( `[`RougeMetricValue`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Output.Schema.RougeMetricValue)` )` Output only. Rouge metric values. |

### RougeMetricValue

**JSON representation**

```
{

  // Union field _score can be only one of the following:
  "score": number
  // End of list of possible types for union field _score.
}
```

| Fields                                                            |                                    |
|-------------------------------------------------------------------|------------------------------------|
| Union field `_score` . `_score` can be only one of the following: |                                    |
| `score`                                                           | `number` Output only. Rouge score. |

### FluencyResult

**JSON representation**

```
{
  "explanation": string,

  // Union field _score can be only one of the following:
  "score": number
  // End of list of possible types for union field _score.

  // Union field _confidence can be only one of the following:
  "confidence": number
  // End of list of possible types for union field _confidence.
}
```

| Fields                                                                      |                                                      |
|-----------------------------------------------------------------------------|------------------------------------------------------|
| `explanation`                                                               | `string` Output only. Explanation for fluency score. |
| Union field `_score` . `_score` can be only one of the following:           |                                                      |
| `score`                                                                     | `number` Output only. Fluency score.                 |
| Union field `_confidence` . `_confidence` can be only one of the following: |                                                      |
| `confidence`                                                                | `number` Output only. Confidence for fluency score.  |

### CoherenceResult

**JSON representation**

```
{
  "explanation": string,

  // Union field _score can be only one of the following:
  "score": number
  // End of list of possible types for union field _score.

  // Union field _confidence can be only one of the following:
  "confidence": number
  // End of list of possible types for union field _confidence.
}
```

| Fields                                                                      |                                                        |
|-----------------------------------------------------------------------------|--------------------------------------------------------|
| `explanation`                                                               | `string` Output only. Explanation for coherence score. |
| Union field `_score` . `_score` can be only one of the following:           |                                                        |
| `score`                                                                     | `number` Output only. Coherence score.                 |
| Union field `_confidence` . `_confidence` can be only one of the following: |                                                        |
| `confidence`                                                                | `number` Output only. Confidence for coherence score.  |

### SafetyResult

**JSON representation**

```
{
  "explanation": string,

  // Union field _score can be only one of the following:
  "score": number
  // End of list of possible types for union field _score.

  // Union field _confidence can be only one of the following:
  "confidence": number
  // End of list of possible types for union field _confidence.
}
```

| Fields                                                                      |                                                     |
|-----------------------------------------------------------------------------|-----------------------------------------------------|
| `explanation`                                                               | `string` Output only. Explanation for safety score. |
| Union field `_score` . `_score` can be only one of the following:           |                                                     |
| `score`                                                                     | `number` Output only. Safety score.                 |
| Union field `_confidence` . `_confidence` can be only one of the following: |                                                     |
| `confidence`                                                                | `number` Output only. Confidence for safety score.  |

### GroundednessResult

**JSON representation**

```
{
  "explanation": string,

  // Union field _score can be only one of the following:
  "score": number
  // End of list of possible types for union field _score.

  // Union field _confidence can be only one of the following:
  "confidence": number
  // End of list of possible types for union field _confidence.
}
```

| Fields                                                                      |                                                           |
|-----------------------------------------------------------------------------|-----------------------------------------------------------|
| `explanation`                                                               | `string` Output only. Explanation for groundedness score. |
| Union field `_score` . `_score` can be only one of the following:           |                                                           |
| `score`                                                                     | `number` Output only. Groundedness score.                 |
| Union field `_confidence` . `_confidence` can be only one of the following: |                                                           |
| `confidence`                                                                | `number` Output only. Confidence for groundedness score.  |

### FulfillmentResult

**JSON representation**

```
{
  "explanation": string,

  // Union field _score can be only one of the following:
  "score": number
  // End of list of possible types for union field _score.

  // Union field _confidence can be only one of the following:
  "confidence": number
  // End of list of possible types for union field _confidence.
}
```

| Fields                                                                      |                                                          |
|-----------------------------------------------------------------------------|----------------------------------------------------------|
| `explanation`                                                               | `string` Output only. Explanation for fulfillment score. |
| Union field `_score` . `_score` can be only one of the following:           |                                                          |
| `score`                                                                     | `number` Output only. Fulfillment score.                 |
| Union field `_confidence` . `_confidence` can be only one of the following: |                                                          |
| `confidence`                                                                | `number` Output only. Confidence for fulfillment score.  |

### SummarizationQualityResult

**JSON representation**

```
{
  "explanation": string,

  // Union field _score can be only one of the following:
  "score": number
  // End of list of possible types for union field _score.

  // Union field _confidence can be only one of the following:
  "confidence": number
  // End of list of possible types for union field _confidence.
}
```

| Fields                                                                      |                                                                    |
|-----------------------------------------------------------------------------|--------------------------------------------------------------------|
| `explanation`                                                               | `string` Output only. Explanation for summarization quality score. |
| Union field `_score` . `_score` can be only one of the following:           |                                                                    |
| `score`                                                                     | `number` Output only. Summarization Quality score.                 |
| Union field `_confidence` . `_confidence` can be only one of the following: |                                                                    |
| `confidence`                                                                | `number` Output only. Confidence for summarization quality score.  |

### PairwiseSummarizationQualityResult

**JSON representation**

```
{
  "pairwiseChoice": enum (PairwiseChoice),
  "explanation": string,

  // Union field _confidence can be only one of the following:
  "confidence": number
  // End of list of possible types for union field _confidence.
}
```

| Fields                                                                      |                                                                                                                                                                                                                                 |
|-----------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `pairwiseChoice`                                                            | `enum ( `[`PairwiseChoice`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Output.Schema.PairwiseChoice)` )` Output only. Pairwise summarization prediction choice. |
| `explanation`                                                               | `string` Output only. Explanation for summarization quality score.                                                                                                                                                              |
| Union field `_confidence` . `_confidence` can be only one of the following: |                                                                                                                                                                                                                                 |
| `confidence`                                                                | `number` Output only. Confidence for summarization quality score.                                                                                                                                                               |

### SummarizationHelpfulnessResult

**JSON representation**

```
{
  "explanation": string,

  // Union field _score can be only one of the following:
  "score": number
  // End of list of possible types for union field _score.

  // Union field _confidence can be only one of the following:
  "confidence": number
  // End of list of possible types for union field _confidence.
}
```

| Fields                                                                      |                                                                        |
|-----------------------------------------------------------------------------|------------------------------------------------------------------------|
| `explanation`                                                               | `string` Output only. Explanation for summarization helpfulness score. |
| Union field `_score` . `_score` can be only one of the following:           |                                                                        |
| `score`                                                                     | `number` Output only. Summarization Helpfulness score.                 |
| Union field `_confidence` . `_confidence` can be only one of the following: |                                                                        |
| `confidence`                                                                | `number` Output only. Confidence for summarization helpfulness score.  |

### SummarizationVerbosityResult

**JSON representation**

```
{
  "explanation": string,

  // Union field _score can be only one of the following:
  "score": number
  // End of list of possible types for union field _score.

  // Union field _confidence can be only one of the following:
  "confidence": number
  // End of list of possible types for union field _confidence.
}
```

| Fields                                                                      |                                                                      |
|-----------------------------------------------------------------------------|----------------------------------------------------------------------|
| `explanation`                                                               | `string` Output only. Explanation for summarization verbosity score. |
| Union field `_score` . `_score` can be only one of the following:           |                                                                      |
| `score`                                                                     | `number` Output only. Summarization Verbosity score.                 |
| Union field `_confidence` . `_confidence` can be only one of the following: |                                                                      |
| `confidence`                                                                | `number` Output only. Confidence for summarization verbosity score.  |

### QuestionAnsweringQualityResult

**JSON representation**

```
{
  "explanation": string,

  // Union field _score can be only one of the following:
  "score": number
  // End of list of possible types for union field _score.

  // Union field _confidence can be only one of the following:
  "confidence": number
  // End of list of possible types for union field _confidence.
}
```

| Fields                                                                      |                                                                         |
|-----------------------------------------------------------------------------|-------------------------------------------------------------------------|
| `explanation`                                                               | `string` Output only. Explanation for question answering quality score. |
| Union field `_score` . `_score` can be only one of the following:           |                                                                         |
| `score`                                                                     | `number` Output only. Question Answering Quality score.                 |
| Union field `_confidence` . `_confidence` can be only one of the following: |                                                                         |
| `confidence`                                                                | `number` Output only. Confidence for question answering quality score.  |

### PairwiseQuestionAnsweringQualityResult

**JSON representation**

```
{
  "pairwiseChoice": enum (PairwiseChoice),
  "explanation": string,

  // Union field _confidence can be only one of the following:
  "confidence": number
  // End of list of possible types for union field _confidence.
}
```

| Fields                                                                      |                                                                                                                                                                                                                                      |
|-----------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `pairwiseChoice`                                                            | `enum ( `[`PairwiseChoice`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Output.Schema.PairwiseChoice)` )` Output only. Pairwise question answering prediction choice. |
| `explanation`                                                               | `string` Output only. Explanation for question answering quality score.                                                                                                                                                              |
| Union field `_confidence` . `_confidence` can be only one of the following: |                                                                                                                                                                                                                                      |
| `confidence`                                                                | `number` Output only. Confidence for question answering quality score.                                                                                                                                                               |

### QuestionAnsweringRelevanceResult

**JSON representation**

```
{
  "explanation": string,

  // Union field _score can be only one of the following:
  "score": number
  // End of list of possible types for union field _score.

  // Union field _confidence can be only one of the following:
  "confidence": number
  // End of list of possible types for union field _confidence.
}
```

| Fields                                                                      |                                                                           |
|-----------------------------------------------------------------------------|---------------------------------------------------------------------------|
| `explanation`                                                               | `string` Output only. Explanation for question answering relevance score. |
| Union field `_score` . `_score` can be only one of the following:           |                                                                           |
| `score`                                                                     | `number` Output only. Question Answering Relevance score.                 |
| Union field `_confidence` . `_confidence` can be only one of the following: |                                                                           |
| `confidence`                                                                | `number` Output only. Confidence for question answering relevance score.  |

### QuestionAnsweringHelpfulnessResult

**JSON representation**

```
{
  "explanation": string,

  // Union field _score can be only one of the following:
  "score": number
  // End of list of possible types for union field _score.

  // Union field _confidence can be only one of the following:
  "confidence": number
  // End of list of possible types for union field _confidence.
}
```

| Fields                                                                      |                                                                             |
|-----------------------------------------------------------------------------|-----------------------------------------------------------------------------|
| `explanation`                                                               | `string` Output only. Explanation for question answering helpfulness score. |
| Union field `_score` . `_score` can be only one of the following:           |                                                                             |
| `score`                                                                     | `number` Output only. Question Answering Helpfulness score.                 |
| Union field `_confidence` . `_confidence` can be only one of the following: |                                                                             |
| `confidence`                                                                | `number` Output only. Confidence for question answering helpfulness score.  |

### QuestionAnsweringCorrectnessResult

**JSON representation**

```
{
  "explanation": string,

  // Union field _score can be only one of the following:
  "score": number
  // End of list of possible types for union field _score.

  // Union field _confidence can be only one of the following:
  "confidence": number
  // End of list of possible types for union field _confidence.
}
```

| Fields                                                                      |                                                                             |
|-----------------------------------------------------------------------------|-----------------------------------------------------------------------------|
| `explanation`                                                               | `string` Output only. Explanation for question answering correctness score. |
| Union field `_score` . `_score` can be only one of the following:           |                                                                             |
| `score`                                                                     | `number` Output only. Question Answering Correctness score.                 |
| Union field `_confidence` . `_confidence` can be only one of the following: |                                                                             |
| `confidence`                                                                | `number` Output only. Confidence for question answering correctness score.  |

### PointwiseMetricResult

**JSON representation**

```
{
  "explanation": string,
  "customOutput": {
    object (CustomOutput)
  },

  // Union field _score can be only one of the following:
  "score": number
  // End of list of possible types for union field _score.
}
```

| Fields                                                            |                                                                                                                                                                                                             |
|-------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `explanation`                                                     | `string` Output only. Explanation for pointwise metric score.                                                                                                                                               |
| `customOutput`                                                    | `object ( `[`CustomOutput`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Output.Schema.CustomOutput)` )` Output only. Spec for custom output. |
| Union field `_score` . `_score` can be only one of the following: |                                                                                                                                                                                                             |
| `score`                                                           | `number` Output only. Pointwise metric score.                                                                                                                                                               |

### CustomOutput

**JSON representation**

```
{

  // Union field custom_output can be only one of the following:
  "rawOutputs": {
    object (RawOutput)
  }
  // End of list of possible types for union field custom_output.
}
```

| Fields                                                                                         |                                                                                                                                                                                                           |
|------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Union field `custom_output` . Custom output. `custom_output` can be only one of the following: |                                                                                                                                                                                                           |
| `rawOutputs`                                                                                   | `object ( `[`RawOutput`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Output.Schema.RawOutput)` )` Output only. List of raw output strings. |

### RawOutput

**JSON representation**

```
{
  "rawOutput": [
    string
  ]
}
```

| Fields        |                                          |
|---------------|------------------------------------------|
| `rawOutput[]` | `string` Output only. Raw output string. |

### PairwiseMetricResult

**JSON representation**

```
{
  "pairwiseChoice": enum (PairwiseChoice),
  "explanation": string,
  "customOutput": {
    object (CustomOutput)
  }
}
```

| Fields           |                                                                                                                                                                                                               |
|------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `pairwiseChoice` | `enum ( `[`PairwiseChoice`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Output.Schema.PairwiseChoice)` )` Output only. Pairwise metric choice. |
| `explanation`    | `string` Output only. Explanation for pairwise metric score.                                                                                                                                                  |
| `customOutput`   | `object ( `[`CustomOutput`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Output.Schema.CustomOutput)` )` Output only. Spec for custom output.   |

### ToolCallValidResults

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

| Fields                        |                                                                                                                                                                                                                                            |
|-------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `toolCallValidMetricValues[]` | `object ( `[`ToolCallValidMetricValue`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Output.Schema.ToolCallValidMetricValue)` )` Output only. Tool call valid metric values. |

### ToolCallValidMetricValue

**JSON representation**

```
{

  // Union field _score can be only one of the following:
  "score": number
  // End of list of possible types for union field _score.
}
```

| Fields                                                            |                                              |
|-------------------------------------------------------------------|----------------------------------------------|
| Union field `_score` . `_score` can be only one of the following: |                                              |
| `score`                                                           | `number` Output only. Tool call valid score. |

### ToolNameMatchResults

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

| Fields                        |                                                                                                                                                                                                                                            |
|-------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `toolNameMatchMetricValues[]` | `object ( `[`ToolNameMatchMetricValue`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Output.Schema.ToolNameMatchMetricValue)` )` Output only. Tool name match metric values. |

### ToolNameMatchMetricValue

**JSON representation**

```
{

  // Union field _score can be only one of the following:
  "score": number
  // End of list of possible types for union field _score.
}
```

| Fields                                                            |                                              |
|-------------------------------------------------------------------|----------------------------------------------|
| Union field `_score` . `_score` can be only one of the following: |                                              |
| `score`                                                           | `number` Output only. Tool name match score. |

### ToolParameterKeyMatchResults

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

| Fields                                |                                                                                                                                                                                                                                                                     |
|---------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `toolParameterKeyMatchMetricValues[]` | `object ( `[`ToolParameterKeyMatchMetricValue`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Output.Schema.ToolParameterKeyMatchMetricValue)` )` Output only. Tool parameter key match metric values. |

### ToolParameterKeyMatchMetricValue

**JSON representation**

```
{

  // Union field _score can be only one of the following:
  "score": number
  // End of list of possible types for union field _score.
}
```

| Fields                                                            |                                                       |
|-------------------------------------------------------------------|-------------------------------------------------------|
| Union field `_score` . `_score` can be only one of the following: |                                                       |
| `score`                                                           | `number` Output only. Tool parameter key match score. |

### ToolParameterKVMatchResults

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

| Fields                               |                                                                                                                                                                                                                                                                         |
|--------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `toolParameterKvMatchMetricValues[]` | `object ( `[`ToolParameterKVMatchMetricValue`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Output.Schema.ToolParameterKVMatchMetricValue)` )` Output only. Tool parameter key value match metric values. |

### ToolParameterKVMatchMetricValue

**JSON representation**

```
{

  // Union field _score can be only one of the following:
  "score": number
  // End of list of possible types for union field _score.
}
```

| Fields                                                            |                                                             |
|-------------------------------------------------------------------|-------------------------------------------------------------|
| Union field `_score` . `_score` can be only one of the following: |                                                             |
| `score`                                                           | `number` Output only. Tool parameter key value match score. |

### CometResult

**JSON representation**

```
{

  // Union field _score can be only one of the following:
  "score": number
  // End of list of possible types for union field _score.
}
```

| Fields                                                            |                                                              |
|-------------------------------------------------------------------|--------------------------------------------------------------|
| Union field `_score` . `_score` can be only one of the following: |                                                              |
| `score`                                                           | `number` Output only. Comet score. Range depends on version. |

### MetricxResult

**JSON representation**

```
{

  // Union field _score can be only one of the following:
  "score": number
  // End of list of possible types for union field _score.
}
```

| Fields                                                            |                                                                |
|-------------------------------------------------------------------|----------------------------------------------------------------|
| Union field `_score` . `_score` can be only one of the following: |                                                                |
| `score`                                                           | `number` Output only. MetricX score. Range depends on version. |

### TrajectoryExactMatchResults

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

| Fields                               |                                                                                                                                                                                                                                                               |
|--------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `trajectoryExactMatchMetricValues[]` | `object ( `[`TrajectoryExactMatchMetricValue`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Output.Schema.TrajectoryExactMatchMetricValue)` )` Output only. TrajectoryExactMatch metric values. |

### TrajectoryExactMatchMetricValue

**JSON representation**

```
{

  // Union field _score can be only one of the following:
  "score": number
  // End of list of possible types for union field _score.
}
```

| Fields                                                            |                                                   |
|-------------------------------------------------------------------|---------------------------------------------------|
| Union field `_score` . `_score` can be only one of the following: |                                                   |
| `score`                                                           | `number` Output only. TrajectoryExactMatch score. |

### TrajectoryInOrderMatchResults

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

| Fields                                 |                                                                                                                                                                                                                                                                     |
|----------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `trajectoryInOrderMatchMetricValues[]` | `object ( `[`TrajectoryInOrderMatchMetricValue`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Output.Schema.TrajectoryInOrderMatchMetricValue)` )` Output only. TrajectoryInOrderMatch metric values. |

### TrajectoryInOrderMatchMetricValue

**JSON representation**

```
{

  // Union field _score can be only one of the following:
  "score": number
  // End of list of possible types for union field _score.
}
```

| Fields                                                            |                                                     |
|-------------------------------------------------------------------|-----------------------------------------------------|
| Union field `_score` . `_score` can be only one of the following: |                                                     |
| `score`                                                           | `number` Output only. TrajectoryInOrderMatch score. |

### TrajectoryAnyOrderMatchResults

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

| Fields                                  |                                                                                                                                                                                                                                                                        |
|-----------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `trajectoryAnyOrderMatchMetricValues[]` | `object ( `[`TrajectoryAnyOrderMatchMetricValue`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Output.Schema.TrajectoryAnyOrderMatchMetricValue)` )` Output only. TrajectoryAnyOrderMatch metric values. |

### TrajectoryAnyOrderMatchMetricValue

**JSON representation**

```
{

  // Union field _score can be only one of the following:
  "score": number
  // End of list of possible types for union field _score.
}
```

| Fields                                                            |                                                      |
|-------------------------------------------------------------------|------------------------------------------------------|
| Union field `_score` . `_score` can be only one of the following: |                                                      |
| `score`                                                           | `number` Output only. TrajectoryAnyOrderMatch score. |

### TrajectoryPrecisionResults

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

| Fields                              |                                                                                                                                                                                                                                                            |
|-------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `trajectoryPrecisionMetricValues[]` | `object ( `[`TrajectoryPrecisionMetricValue`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Output.Schema.TrajectoryPrecisionMetricValue)` )` Output only. TrajectoryPrecision metric values. |

### TrajectoryPrecisionMetricValue

**JSON representation**

```
{

  // Union field _score can be only one of the following:
  "score": number
  // End of list of possible types for union field _score.
}
```

| Fields                                                            |                                                  |
|-------------------------------------------------------------------|--------------------------------------------------|
| Union field `_score` . `_score` can be only one of the following: |                                                  |
| `score`                                                           | `number` Output only. TrajectoryPrecision score. |

### TrajectoryRecallResults

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

| Fields                           |                                                                                                                                                                                                                                                   |
|----------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `trajectoryRecallMetricValues[]` | `object ( `[`TrajectoryRecallMetricValue`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Output.Schema.TrajectoryRecallMetricValue)` )` Output only. TrajectoryRecall metric values. |

### TrajectoryRecallMetricValue

**JSON representation**

```
{

  // Union field _score can be only one of the following:
  "score": number
  // End of list of possible types for union field _score.
}
```

| Fields                                                            |                                               |
|-------------------------------------------------------------------|-----------------------------------------------|
| Union field `_score` . `_score` can be only one of the following: |                                               |
| `score`                                                           | `number` Output only. TrajectoryRecall score. |

### TrajectorySingleToolUseResults

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

| Fields                                  |                                                                                                                                                                                                                                                                        |
|-----------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `trajectorySingleToolUseMetricValues[]` | `object ( `[`TrajectorySingleToolUseMetricValue`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Output.Schema.TrajectorySingleToolUseMetricValue)` )` Output only. TrajectorySingleToolUse metric values. |

### TrajectorySingleToolUseMetricValue

**JSON representation**

```
{

  // Union field _score can be only one of the following:
  "score": number
  // End of list of possible types for union field _score.
}
```

| Fields                                                            |                                                      |
|-------------------------------------------------------------------|------------------------------------------------------|
| Union field `_score` . `_score` can be only one of the following: |                                                      |
| `score`                                                           | `number` Output only. TrajectorySingleToolUse score. |

### RubricBasedInstructionFollowingResult

**JSON representation**

```
{
  "rubricCritiqueResults": [
    {
      object (RubricCritiqueResult)
    }
  ],

  // Union field _score can be only one of the following:
  "score": number
  // End of list of possible types for union field _score.
}
```

| Fields                                                            |                                                                                                                                                                                                                                          |
|-------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `rubricCritiqueResults[]`                                         | `object ( `[`RubricCritiqueResult`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Output.Schema.RubricCritiqueResult)` )` Output only. List of per rubric critique results. |
| Union field `_score` . `_score` can be only one of the following: |                                                                                                                                                                                                                                          |
| `score`                                                           | `number` Output only. Overall score for the instruction following.                                                                                                                                                                       |

### RubricCritiqueResult

**JSON representation**

```
{
  "rubric": string,
  "verdict": boolean
}
```

| Fields    |                                                                                             |
|-----------|---------------------------------------------------------------------------------------------|
| `rubric`  | `string` Output only. Rubric to be evaluated.                                               |
| `verdict` | `boolean` Output only. Verdict for the rubric - true if the rubric is met, false otherwise. |

### MetricResult

**JSON representation**

```
{
  "rubricVerdicts": [
    {
      object (RubricVerdict)
    }
  ],

  // Union field _score can be only one of the following:
  "score": number
  // End of list of possible types for union field _score.

  // Union field _explanation can be only one of the following:
  "explanation": string
  // End of list of possible types for union field _explanation.

  // Union field _error can be only one of the following:
  "error": {
    object (Status)
  }
  // End of list of possible types for union field _error.
}
```

| Fields                                                                        |                                                                                                                                                                                                                                               |
|-------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `rubricVerdicts[]`                                                            | `object ( `[`RubricVerdict`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Output.Schema.RubricVerdict)` )` Output only. For rubric-based metrics, the verdicts for each rubric. |
| Union field `_score` . `_score` can be only one of the following:             |                                                                                                                                                                                                                                               |
| `score`                                                                       | `number` Output only. The score for the metric. Please refer to each metric's documentation for the meaning of the score.                                                                                                                     |
| Union field `_explanation` . `_explanation` can be only one of the following: |                                                                                                                                                                                                                                               |
| `explanation`                                                                 | `string` Output only. The explanation for the metric result.                                                                                                                                                                                  |
| Union field `_error` . `_error` can be only one of the following:             |                                                                                                                                                                                                                                               |
| `error`                                                                       | `object ( `[`Status`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/create_endpoint#Output.Schema.Status)` )` Output only. The error status for the metric result.                                  |

### RubricVerdict

**JSON representation**

```
{
  "evaluatedRubric": {
    object (Rubric)
  },
  "verdict": boolean,

  // Union field _reasoning can be only one of the following:
  "reasoning": string
  // End of list of possible types for union field _reasoning.
}
```

| Fields                                                                    |                                                                                                                                                                                                                                                                                                                                                                              |
|---------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `evaluatedRubric`                                                         | `object ( `[`Rubric`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.Rubric)` )` Required. The full rubric definition that was evaluated. Storing this ensures the verdict is self-contained and understandable, especially if the original rubric definition changes or was dynamically generated. |
| `verdict`                                                                 | `boolean` Required. Outcome of the evaluation against the rubric, represented as a boolean. `true` indicates a "Pass", `false` indicates a "Fail".                                                                                                                                                                                                                           |
| Union field `_reasoning` . `_reasoning` can be only one of the following: |                                                                                                                                                                                                                                                                                                                                                                              |
| `reasoning`                                                               | `string` Optional. Human-readable reasoning or explanation for the verdict. This can include specific examples or details from the evaluated content that justify the given verdict.                                                                                                                                                                                         |

### Rubric

**JSON representation**

```
{
  "rubricId": string,
  "content": {
    object (Content)
  },

  // Union field _type can be only one of the following:
  "type": string
  // End of list of possible types for union field _type.

  // Union field _importance can be only one of the following:
  "importance": enum (Importance)
  // End of list of possible types for union field _importance.
}
```

| Fields                                                                      |                                                                                                                                                                                                                                                                                                |
|-----------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `rubricId`                                                                  | `string` Unique identifier for the rubric. This ID is used to refer to this rubric, e.g., in RubricVerdict.                                                                                                                                                                                    |
| `content`                                                                   | `object ( `[`Content`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.Content_1)` )` Required. The actual testable criteria for the rubric.                                                                           |
| Union field `_type` . `_type` can be only one of the following:             |                                                                                                                                                                                                                                                                                                |
| `type`                                                                      | `string` Optional. A type designator for the rubric, which can inform how it's evaluated or interpreted by systems or users. It's recommended to use consistent, well-defined, upper snake_case strings. Examples: "SUMMARIZATION_QUALITY", "SAFETY_HARMFUL_CONTENT", "INSTRUCTION_ADHERENCE". |
| Union field `_importance` . `_importance` can be only one of the following: |                                                                                                                                                                                                                                                                                                |
| `importance`                                                                | `enum ( `[`Importance`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.Importance)` )` Optional. The relative importance of this rubric.                                                                              |

### Content

**JSON representation**

```
{

  // Union field content_type can be only one of the following:
  "property": {
    object (Property)
  }
  // End of list of possible types for union field content_type.
}
```

| Fields                                                                        |                                                                                                                                                                                                                 |
|-------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Union field `content_type` . `content_type` can be only one of the following: |                                                                                                                                                                                                                 |
| `property`                                                                    | `object ( `[`Property`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/evaluate_instances#Input.Schema.Property)` )` Evaluation criteria based on a specific property. |

### Property

**JSON representation**

```
{
  "description": string
}
```

| Fields        |                                                                                                                 |
|---------------|-----------------------------------------------------------------------------------------------------------------|
| `description` | `string` Description of the property being evaluated. Example: "The model's response is grammatically correct." |

### Status

**JSON representation**

```
{
  "code": integer,
  "message": string,
  "details": [
    {
      "@type": string,
      field1: ...,
      ...
    }
  ]
}
```

| Fields      |                                                                                                                                                                                                                                                                                                              |
|-------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `code`      | `integer` The status code, which should be an enum value of `google.rpc.Code` .                                                                                                                                                                                                                              |
| `message`   | `string` A developer-facing error message, which should be in English. Any user-facing error message should be localized and sent in the `google.rpc.Status.details` field, or localized by the client.                                                                                                      |
| `details[]` | `object` A list of messages that carry the error details. There is a common set of message types for APIs to use. An object containing fields of an arbitrary type. An additional field `"@type"` contains a URI identifying the type. Example: `{ "id": 1234, "@type": "types.example.com/standard/id" }` . |

### Any

**JSON representation**

```
{
  "typeUrl": string,
  "value": string
}
```

| Fields    |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
|-----------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `typeUrl` | `string` Identifies the type of the serialized Protobuf message with a URI reference consisting of a prefix ending in a slash and the fully-qualified type name. Example: type.googleapis.com/google.protobuf.StringValue This string must contain at least one `/` character, and the content after the last `/` must be the fully-qualified name of the type in canonical form, without a leading dot. Do not write a scheme on these URI references so that clients do not attempt to contact them. The prefix is arbitrary and Protobuf implementations are expected to simply strip off everything up to and including the last `/` to identify the type. `type.googleapis.com/` is a common default prefix that some legacy implementations require. This prefix does not indicate the origin of the type, and URIs containing it are not expected to respond to any requests. All type URL strings must be legal URI references with the additional restriction (for the text format) that the content of the reference must consist only of alphanumeric characters, percent-encoded escapes, and characters in the following set (not including the outer backticks): `/-.~_!$&()*+,;=` . Despite our allowing percent encodings, implementations should not unescape them to prevent confusion with existing parsers. For example, `type.googleapis.com%2FFoo` should be rejected. In the original design of `Any` , the possibility of launching a type resolution service at these type URLs was considered but Protobuf never implemented one and considers contacting these URLs to be problematic and a potential security issue. Do not attempt to contact type URLs. |
| `value`   | `string ( `[`bytes`](https://developers.google.com/discovery/v1/type-format)` format)` Holds a Protobuf serialization of the type described by type_url. A base64-encoded string.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |

### PairwiseChoice

Pairwise prediction autorater preference.

| Enums                         |                                |
|-------------------------------|--------------------------------|
| `PAIRWISE_CHOICE_UNSPECIFIED` | Unspecified prediction choice. |
| `BASELINE`                    | Baseline prediction wins       |
| `CANDIDATE`                   | Candidate prediction wins      |
| `TIE`                         | Winner cannot be determined    |

### Importance

Importance level of the rubric.

| Enums                    |                              |
|--------------------------|------------------------------|
| `IMPORTANCE_UNSPECIFIED` | Importance is not specified. |
| `HIGH`                   | High importance.             |
| `MEDIUM`                 | Medium importance.           |
| `LOW`                    | Low importance.              |

### Tool Annotations

Destructive Hint: ❌ \| Idempotent Hint: ❌ \| Read Only Hint: ❌ \| Open World Hint: ❌
