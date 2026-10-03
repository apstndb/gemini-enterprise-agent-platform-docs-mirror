---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/Metric
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/Metric
title: Metric
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

The metric used for running evaluations.

Fields

`aggregationMetrics[]` `enum ( `[`AggregationMetric`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/AggregationMetric)` )`

Optional. The aggregation metrics to use.

`metadata` `object ( `[`MetricMetadata`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/Metric#MetricMetadata)` )`

Optional. metadata about the metric, used for visualization and organization.

`metric_spec` `Union type`

The spec for the metric. It would be either a pre-defined metric, or a inline metric spec. The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:

`predefinedMetricSpec` `object ( `[`PredefinedMetricSpec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/Metric#PredefinedMetricSpec)` )`

The spec for a pre-defined metric.

`computationBasedMetricSpec` `object ( `[`ComputationBasedMetricSpec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/Metric#ComputationBasedMetricSpec)` )`

Spec for a computation based metric.

`llmBasedMetricSpec` `object ( `[`LLMBasedMetricSpec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/Metric#LLMBasedMetricSpec)` )`

Spec for an LLM based metric.

`customCodeExecutionSpec` `object ( `[`CustomCodeExecutionSpec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/Metric#CustomCodeExecutionSpec)` )`

Spec for Custom code Execution metric.

`pointwiseMetricSpec` `object ( `[`PointwiseMetricSpec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/Metric#PointwiseMetricSpec)` )`

Spec for pointwise metric.

`pairwiseMetricSpec` `object ( `[`PairwiseMetricSpec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/Metric#PairwiseMetricSpec)` )`

Spec for pairwise metric.

`exactMatchSpec` `object ( `[`ExactMatchSpec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/Metric#ExactMatchSpec)` )`

Spec for exact match metric.

`bleuSpec` `object ( `[`BleuSpec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/Metric#BleuSpec)` )`

Spec for bleu metric.

`rougeSpec` `object ( `[`RougeSpec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/Metric#RougeSpec)` )`

Spec for rouge metric.

End of mutually exclusive fields.

**JSON representation**

```
{
  "aggregationMetrics": [
    enum (AggregationMetric)
  ],
  "metadata": {
    object (MetricMetadata)
  },

  // metric_spec
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
  // Union type
}
```

## PredefinedMetricSpec

The spec for a pre-defined metric.

Fields

`metricSpecName` `string`

Required. The name of a pre-defined metric, such as "instruction_following_v1" or "text_quality_v1".

`metricSpecParameters` `object ( `[`Struct`](https://protobuf.dev/reference/protobuf/google.protobuf/#struct)` format)`

Optional. The parameters needed to run the pre-defined metric.

**JSON representation**

```
{
  "metricSpecName": string,
  "metricSpecParameters": {
    object
  }
}
```

## ComputationBasedMetricSpec

Specification for a computation based metric.

Fields

`type` `enum ( `[`ComputationBasedMetricType`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/Metric#ComputationBasedMetricType)` )`

Required. The type of the computation based metric.

`parameters` `object ( `[`Struct`](https://protobuf.dev/reference/protobuf/google.protobuf/#struct)` format)`

Optional. A map of parameters for the metric, e.g. {"rougeType": "rougeL"}.

**JSON representation**

```
{
  "type": enum (ComputationBasedMetricType),
  "parameters": {
    object
  }
}
```

## ComputationBasedMetricType

Types of computation based metrics.

| Enums                                       |                                            |
|---------------------------------------------|--------------------------------------------|
| `COMPUTATION_BASED_METRIC_TYPE_UNSPECIFIED` | Unspecified computation based metric type. |
| `EXACT_MATCH`                               | Exact match metric.                        |
| `BLEU`                                      | BLEU metric.                               |
| `ROUGE`                                     | ROUGE metric.                              |

## LLMBasedMetricSpec

Specification for an LLM based metric.

Fields

`resultParserConfig` `object ( `[`EvaluationParserConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/Metric#EvaluationParserConfig)` )`

Optional. The parser config for the metric result.

`rubrics_source` `Union type`

Source of the rubrics to be used for evaluation. The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:

`rubricGroupKey` `string`

Use a pre-defined group of rubrics associated with the input. Refers to a key in the rubricGroups map of EvaluationInstance.

`rubricGenerationSpec` `object ( `[`RubricGenerationSpec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/Metric#RubricGenerationSpec)` )`

Dynamically generate rubrics using this specification.

`predefinedRubricGenerationSpec` `object ( `[`PredefinedMetricSpec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/Metric#PredefinedMetricSpec)` )`

Dynamically generate rubrics using a predefined spec.

End of mutually exclusive fields.

`metricPromptTemplate` `string`

Required. Template for the prompt sent to the judge model.

`systemInstruction` `string`

Optional. System instructions for the judge model.

`judgeAutoraterConfig` `object ( `[`AutoraterConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/AutoraterConfig)` )`

Optional. Optional configuration for the judge LLM (Autorater).

`additionalConfig` `object ( `[`Struct`](https://protobuf.dev/reference/protobuf/google.protobuf/#struct)` format)`

Optional. Optional additional configuration for the metric.

**JSON representation**

```
{
  "resultParserConfig": {
    object (EvaluationParserConfig)
  },

  // rubrics_source
  "rubricGroupKey": string,
  "rubricGenerationSpec": {
    object (RubricGenerationSpec)
  },
  "predefinedRubricGenerationSpec": {
    object (PredefinedMetricSpec)
  }
  // Union type
  "metricPromptTemplate": string,
  "systemInstruction": string,
  "judgeAutoraterConfig": {
    object (AutoraterConfig)
  },
  "additionalConfig": {
    object
  }
}
```

## RubricGenerationSpec

Specification for how rubrics should be generated.

Fields

`promptTemplate` `string`

Template for the prompt used to generate rubrics. The details should be updated based on the most-recent recipe requirements.

`rubricContentType` `enum ( `[`RubricContentType`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/Metric#RubricContentType)` )`

The type of rubric content to be generated.

`rubricTypeOntology[]` `string`

Optional. An optional, pre-defined list of allowed types for generated rubrics. If this field is provided, it implies `include_rubric_type` should be true, and the generated rubric types should be chosen from this ontology.

`modelConfig` `object ( `[`AutoraterConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/AutoraterConfig)` )`

Configuration for the model used in rubric generation. Configs including sampling count and base model can be specified here. Flipping is not supported for rubric generation.

**JSON representation**

```
{
  "promptTemplate": string,
  "rubricContentType": enum (RubricContentType),
  "rubricTypeOntology": [
    string
  ],
  "modelConfig": {
    object (AutoraterConfig)
  }
}
```

## RubricContentType

Specifies the type of rubric content to generate.

| Enums                             |                                                   |
|-----------------------------------|---------------------------------------------------|
| `RUBRIC_CONTENT_TYPE_UNSPECIFIED` | The content type to generate is not specified.    |
| `PROPERTY`                        | Generate rubrics based on properties.             |
| `NL_QUESTION_ANSWER`              | Generate rubrics in an NL question answer format. |
| `PYTHON_CODE_ASSERTION`           | Generate rubrics in a unit test format.           |

## EvaluationParserConfig

Config for parsing LLM responses. It can be used to parse the LLM response to be evaluated, or the LLM response from LLM-based metrics/Autoraters.

Fields

`parser` `Union type`

The parser to use. The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:

`customCodeParserConfig` `object ( `[`CustomCodeParserConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/Metric#CustomCodeParserConfig)` )`

Optional. Use custom code to parse the LLM response.

End of mutually exclusive fields.

**JSON representation**

```
{

  // parser
  "customCodeParserConfig": {
    object (CustomCodeParserConfig)
  }
  // Union type
}
```

## CustomCodeParserConfig

Configuration for parsing the LLM response using custom code.

Fields

`codeExecutionRegion` `string`

Optional. The region to use for code execution. If set, the code Execution Sandbox will be invoked in the specified region regardless of the request's originating region. Must be a region where the code Execution Sandbox is available. For the current list of [supported regions](https://cloud.google.com/vertex-ai/generative-ai/docs/agent-engine/locations) . If unset, the request's originating region is used.

`parsingFunction` `string`

Required. Python function for parsing results. The function should be defined within this string.

The function takes a list of strings (LLM responses) and should return either a list of dictionaries (for rubrics) or a single dictionary (for a metric result).

Example function signature: def parse(responses: list\[str\]) -\> list\[dict\[str, Any\]\] \| dict\[str, Any\]:

When parsing rubrics, return a list of dictionaries, where each dictionary represents a Rubric. Example for rubrics: \[ { "content": {"property": {"description": "The response is factual."}}, "type": "FACTUALITY", "importance": "HIGH" }, { "content": {"property": {"description": "The response is fluent."}}, "type": "FLUENCY", "importance": "MEDIUM" } \]

When parsing critique results, return a dictionary representing a MetricResult. Example for a metric result: { "score": 0.8, "explanation": "The model followed most instructions.", "rubricVerdicts": \[...\] }

... code for result extraction and aggregation

**JSON representation**

```
{
  "codeExecutionRegion": string,
  "parsingFunction": string
}
```

## CustomCodeExecutionSpec

Specificies a metric that is populated by evaluating user-defined Python code.

Fields

`codeExecutionRegion` `string`

Optional. The region to use for code execution. If set, the code Execution Sandbox will be invoked in the specified region regardless of the request's originating region. Must be a region where the code Execution Sandbox is available. For the current list of [supported regions](https://cloud.google.com/vertex-ai/generative-ai/docs/agent-engine/locations) . If unset, the request's originating region is used; requests from regions where the sandbox is unavailable will fail with UNIMPLEMENTED.

`evaluationFunction` `string`

Required. Python function. Expected user to define the following function, e.g.: def evaluate(instance: dict\[str, Any\]) -\> float: Please include this function signature in the code snippet. Instance is the evaluation instance, any fields populated in the instance are available to the function as instance\[fieldName\].

Example: Example input:

`instance= EvaluationInstance( response=EvaluationInstance.InstanceData(text="The answer is 4."), reference=EvaluationInstance.InstanceData(text="4") )`

Example converted input:

`{ 'response': {'text': 'The answer is 4.'}, 'reference': {'text': '4'} }`

Example python function:

`def evaluate(instance: dict[str, Any]) -> float: if instance['response']['text'] == instance['reference']['text']: return 1.0 return 0.0`

CustomCodeExecutionSpec is also supported in Batch Evaluation (EvalDataset RPC) and Tuning Evaluation. Each line in the input jsonl file will be converted to dict\[str, Any\] and passed to the evaluation function.

**JSON representation**

```
{
  "codeExecutionRegion": string,
  "evaluationFunction": string
}
```

## PointwiseMetricSpec

Spec for pointwise metric.

Fields

`customOutputFormatConfig` `object ( `[`CustomOutputFormatConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/Metric#CustomOutputFormatConfig)` )`

Optional. CustomOutputFormatConfig allows customization of metric output. By default, metrics return a score and explanation. When this config is set, the default output is replaced with either: - The raw output string. - A parsed output based on a user-defined schema. If a custom format is chosen, the `score` and `explanation` fields in the corresponding metric result will be empty.

`metricPromptTemplate` `string`

Required. Metric prompt template for pointwise metric.

`systemInstruction` `string`

Optional. System instructions for pointwise metric.

**JSON representation**

```
{
  "customOutputFormatConfig": {
    object (CustomOutputFormatConfig)
  },
  "metricPromptTemplate": string,
  "systemInstruction": string
}
```

## CustomOutputFormatConfig

Spec for custom output format configuration.

Fields

`custom_output_format_config` `Union type`

Custom output format configuration. The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:

`returnRawOutput` `boolean`

Optional. Whether to return raw output.

End of mutually exclusive fields.

**JSON representation**

```
{

  // custom_output_format_config
  "returnRawOutput": boolean
  // Union type
}
```

## PairwiseMetricSpec

Spec for pairwise metric.

Fields

`candidateResponseFieldName` `string`

Optional. The field name of the candidate response.

`baselineResponseFieldName` `string`

Optional. The field name of the baseline response.

`customOutputFormatConfig` `object ( `[`CustomOutputFormatConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/Metric#CustomOutputFormatConfig)` )`

Optional. CustomOutputFormatConfig allows customization of metric output. When this config is set, the default output is replaced with the raw output string. If a custom format is chosen, the `pairwiseChoice` and `explanation` fields in the corresponding metric result will be empty.

`metricPromptTemplate` `string`

Required. Metric prompt template for pairwise metric.

`systemInstruction` `string`

Optional. System instructions for pairwise metric.

**JSON representation**

```
{
  "candidateResponseFieldName": string,
  "baselineResponseFieldName": string,
  "customOutputFormatConfig": {
    object (CustomOutputFormatConfig)
  },
  "metricPromptTemplate": string,
  "systemInstruction": string
}
```

## ExactMatchSpec

This type has no fields.

Spec for exact match metric - returns 1 if prediction and reference exactly matches, otherwise 0.

## BleuSpec

Spec for bleu score metric - calculates the precision of n-grams in the prediction as compared to reference - returns a score ranging between 0 to 1.

Fields

`useEffectiveOrder` `boolean`

Optional. Whether to useEffectiveOrder to compute bleu score.

**JSON representation**

```
{
  "useEffectiveOrder": boolean
}
```

## RougeSpec

Spec for rouge score metric - calculates the recall of n-grams in prediction as compared to reference - returns a score ranging between 0 and 1.

Fields

`rougeType` `string`

Optional. Supported rouge types are rougen\[1-9\], rougeL, and rougeLsum.

`useStemmer` `boolean`

Optional. Whether to use stemmer to compute rouge score.

`splitSummaries` `boolean`

Optional. Whether to split summaries while using rougeLsum.

**JSON representation**

```
{
  "rougeType": string,
  "useStemmer": boolean,
  "splitSummaries": boolean
}
```

## MetricMetadata

metadata about the metric, used for visualization and organization.

Fields

`title` `string`

Optional. The user-friendly name for the metric. If not set for a registered metric, it will default to the metric's display name.

`scoreRange` `object ( `[`ScoreRange`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/Metric#ScoreRange)` )`

Optional. The range of possible scores for this metric, used for plotting.

`otherMetadata` `object ( `[`Struct`](https://protobuf.dev/reference/protobuf/google.protobuf/#struct)` format)`

Optional. Flexible metadata for user-defined attributes.

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

**JSON representation**

```
{
  "description": string,
  "min": number,
  "max": number,
  "step": number
}
```
