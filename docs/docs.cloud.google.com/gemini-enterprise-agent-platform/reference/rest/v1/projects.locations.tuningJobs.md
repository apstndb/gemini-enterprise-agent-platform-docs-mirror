---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.tuningJobs
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.tuningJobs
title: 'REST Resource: projects.locations.tuningJobs'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

## Resource: TuningJob

Represents a TuningJob that runs with Google owned models.

Fields

`name` `string`

Output only. Identifier. Resource name of a TuningJob. Format: `projects/{project}/locations/{location}/tuningJobs/{tuningJob}`

`tunedModelDisplayName` `string`

Optional. The display name of the [`TunedModel`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.models#Model) . The name can be up to 128 characters long and can consist of any UTF-8 characters. For continuous tuning, tunedModelDisplayName will by default use the same display name as the pre-tuned model. If a new display name is provided, the tuning job will create a new model instead of a new version.

`description` `string`

Optional. The description of the [`TuningJob`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.tuningJobs#TuningJob) .

`state` `enum ( `[`JobState`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/JobState)` )`

Output only. The detailed state of the job.

`createTime` `string ( `[`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp)` format)`

Output only. time when the [`TuningJob`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.tuningJobs#TuningJob) was created.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`startTime` `string ( `[`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp)` format)`

Output only. time when the [`TuningJob`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.tuningJobs#TuningJob) for the first time entered the `JOB_STATE_RUNNING` state.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`endTime` `string ( `[`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp)` format)`

Output only. time when the TuningJob entered any of the following [`JobStates`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/JobState) : `JOB_STATE_SUCCEEDED` , `JOB_STATE_FAILED` , `JOB_STATE_CANCELLED` , `JOB_STATE_EXPIRED` .

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`updateTime` `string ( `[`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp)` format)`

Output only. time when the [`TuningJob`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.tuningJobs#TuningJob) was most recently updated.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`error` `object ( `[`Status`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/ListOperationsResponse#Status)` )`

Output only. Only populated when job's state is `JOB_STATE_FAILED` or `JOB_STATE_CANCELLED` .

`labels` `map (key: string, value: string)`

Optional. The labels with user-defined metadata to organize [`TuningJob`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.tuningJobs#TuningJob) and generated resources such as [`Model`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.models#Model) and [`Endpoint`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.endpoints#Endpoint) .

label keys and values can be no longer than 64 characters (Unicode codepoints), can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed.

See <https://goo.gl/xmQnxf> for more information and examples of labels.

`experiment` `string`

Output only. The Experiment associated with this [`TuningJob`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.tuningJobs#TuningJob) .

`gcsMetricsUri` `string`

Output only. The Cloud Storage metrics URI associated with this [`TuningJob`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.tuningJobs#TuningJob) .

`tunedModel` `object ( `[`TunedModel`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.tuningJobs#TunedModel)` )`

Output only. The tuned model resources associated with this [`TuningJob`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.tuningJobs#TuningJob) .

`tuningDataStats` `object ( `[`TuningDataStats`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.tuningJobs#TuningDataStats)` )`

Output only. The tuning data statistics associated with this [`TuningJob`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.tuningJobs#TuningJob) .

`encryptionSpec` `object ( `[`EncryptionSpec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/EncryptionSpec)` )`

Customer-managed encryption key options for a TuningJob. If this is set, then all resources created by the TuningJob will be encrypted with the provided encryption key.

`serviceAccount` `string`

The service account that the tuningJob workload runs as. If not specified, the Agent Platform Secure Fine-Tuned service Agent in the project will be used. See <https://cloud.google.com/iam/docs/service-agents#vertex-ai-secure-fine-tuning-service-agent>

Users starting the pipeline must have the `iam.serviceAccounts.actAs` permission on this service account.

`evaluateDatasetRuns[]` `object ( `[`EvaluateDatasetRun`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.tuningJobs#EvaluateDatasetRun)` )`

Output only. Evaluation runs for the Tuning Job.

`source_model` `Union type`

The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:

`baseModel` `string`

The base model that is being tuned. See [Supported models](https://cloud.google.com/vertex-ai/generative-ai/docs/model-reference/tuning#supported_models) .

`preTunedModel` `object ( `[`PreTunedModel`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.tuningJobs#PreTunedModel)` )`

The pre-tuned model for continuous tuning.

End of mutually exclusive fields.

`tuning_spec` `Union type`

The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:

`supervisedTuningSpec` `object ( `[`SupervisedTuningSpec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.tuningJobs#SupervisedTuningSpec)` )`

Tuning Spec for Supervised Fine Tuning.

End of mutually exclusive fields.

**JSON representation**

```
{
  "name": string,
  "tunedModelDisplayName": string,
  "description": string,
  "state": enum (JobState),
  "createTime": string,
  "startTime": string,
  "endTime": string,
  "updateTime": string,
  "error": {
    object (Status)
  },
  "labels": {
    string: string,
    ...
  },
  "experiment": string,
  "gcsMetricsUri": string,
  "tunedModel": {
    object (TunedModel)
  },
  "tuningDataStats": {
    object (TuningDataStats)
  },
  "encryptionSpec": {
    object (EncryptionSpec)
  },
  "serviceAccount": string,
  "evaluateDatasetRuns": [
    {
      object (EvaluateDatasetRun)
    }
  ],

  // source_model
  "baseModel": string,
  "preTunedModel": {
    object (PreTunedModel)
  }
  // Union type

  // tuning_spec
  "supervisedTuningSpec": {
    object (SupervisedTuningSpec)
  }
  // Union type
}
```

## PreTunedModel

A pre-tuned model for continuous tuning.

Fields

`tunedModelName` `string`

The resource name of the Model. E.g., a model resource name with a specified version id or alias:

`projects/{project}/locations/{location}/models/{model}@{versionId}`

`projects/{project}/locations/{location}/models/{model}@{alias}`

Or, omit the version id to use the default version:

`projects/{project}/locations/{location}/models/{model}`

`checkpointId` `string`

Optional. The source checkpoint id. If not specified, the default checkpoint will be used.

`baseModel` `string`

Output only. The name of the base model this [`PreTunedModel`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.tuningJobs#PreTunedModel) was tuned from.

**JSON representation**

```
{
  "tunedModelName": string,
  "checkpointId": string,
  "baseModel": string
}
```

## SupervisedTuningSpec

Tuning Spec for Supervised Tuning for first party models.

Fields

`trainingDatasetUri` `string`

Required. Training dataset used for tuning. The dataset can be specified as either a Cloud Storage path to a JSONL file or as the resource name of a Vertex Multimodal Dataset.

`validationDatasetUri` `string`

Optional. Validation dataset used for tuning. The dataset can be specified as either a Cloud Storage path to a JSONL file or as the resource name of a Vertex Multimodal Dataset.

`hyperParameters` `object ( `[`SupervisedHyperParameters`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.tuningJobs#SupervisedHyperParameters)` )`

Optional. Hyperparameters for SFT.

`exportLastCheckpointOnly` `boolean`

Optional. If set to true, disable intermediate checkpoints for SFT and only the last checkpoint will be exported. Otherwise, enable intermediate checkpoints for SFT. Default is false.

`evaluationConfig` `object ( `[`EvaluationConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.tuningJobs#EvaluationConfig)` )`

Optional. Evaluation Config for Tuning Job.

**JSON representation**

```
{
  "trainingDatasetUri": string,
  "validationDatasetUri": string,
  "hyperParameters": {
    object (SupervisedHyperParameters)
  },
  "exportLastCheckpointOnly": boolean,
  "evaluationConfig": {
    object (EvaluationConfig)
  }
}
```

## SupervisedHyperParameters

Hyperparameters for SFT.

Fields

`epochCount` `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)`

Optional. Number of complete passes the model makes over the entire training dataset during training.

`learningRateMultiplier` `number`

Optional. Multiplier for adjusting the default learning rate. Mutually exclusive with `learningRate` . This feature is only available for 1P models.

`adapterSize` `enum ( `[`AdapterSize`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.tuningJobs#AdapterSize)` )`

Optional. Adapter size for tuning.

**JSON representation**

```
{
  "epochCount": string,
  "learningRateMultiplier": number,
  "adapterSize": enum (AdapterSize)
}
```

## AdapterSize

Supported adapter sizes for tuning.

| Enums                      |                              |
|----------------------------|------------------------------|
| `ADAPTER_SIZE_UNSPECIFIED` | Adapter size is unspecified. |
| `ADAPTER_SIZE_ONE`         | Adapter size 1.              |
| `ADAPTER_SIZE_TWO`         | Adapter size 2.              |
| `ADAPTER_SIZE_FOUR`        | Adapter size 4.              |
| `ADAPTER_SIZE_EIGHT`       | Adapter size 8.              |
| `ADAPTER_SIZE_SIXTEEN`     | Adapter size 16.             |
| `ADAPTER_SIZE_THIRTY_TWO`  | Adapter size 32.             |

## EvaluationConfig

Evaluation Config for Tuning Job.

Fields

`metrics[]` `object ( `[`Metric`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.tuningJobs#Metric)` )`

Required. The metrics used for evaluation.

`outputConfig` `object ( `[`OutputConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.tuningJobs#OutputConfig)` )`

Required. Config for evaluation output.

`autoraterConfig` `object ( `[`AutoraterConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.tuningJobs#AutoraterConfig)` )`

Optional. Autorater config for evaluation.

`inferenceGenerationConfig` `object ( `[`GenerationConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.tuningJobs#GenerationConfig)` )`

Optional. Configuration options for inference generation and outputs. If not set, default generation parameters are used.

**JSON representation**

```
{
  "metrics": [
    {
      object (Metric)
    }
  ],
  "outputConfig": {
    object (OutputConfig)
  },
  "autoraterConfig": {
    object (AutoraterConfig)
  },
  "inferenceGenerationConfig": {
    object (GenerationConfig)
  }
}
```

## Metric

The metric used for running evaluations.

Fields

`aggregationMetrics[]` `enum ( `[`AggregationMetric`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.tuningJobs#AggregationMetric)` )`

Optional. The aggregation metrics to use.

`metric_spec` `Union type`

The spec for the metric. It would be either a pre-defined metric, or a inline metric spec. The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:

`predefinedMetricSpec` `object ( `[`PredefinedMetricSpec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.tuningJobs#PredefinedMetricSpec)` )`

The spec for a pre-defined metric.

`computationBasedMetricSpec` `object ( `[`ComputationBasedMetricSpec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.tuningJobs#ComputationBasedMetricSpec)` )`

Spec for a computation based metric.

`llmBasedMetricSpec` `object ( `[`LLMBasedMetricSpec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.tuningJobs#LLMBasedMetricSpec)` )`

Spec for an LLM based metric.

`pointwiseMetricSpec` `object ( `[`PointwiseMetricSpec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.tuningJobs#PointwiseMetricSpec)` )`

Spec for pointwise metric.

`pairwiseMetricSpec` `object ( `[`PairwiseMetricSpec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.tuningJobs#PairwiseMetricSpec)` )`

Spec for pairwise metric.

`exactMatchSpec` `object ( `[`ExactMatchSpec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.tuningJobs#ExactMatchSpec)` )`

Spec for exact match metric.

`bleuSpec` `object ( `[`BleuSpec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.tuningJobs#BleuSpec)` )`

Spec for bleu metric.

`rougeSpec` `object ( `[`RougeSpec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.tuningJobs#RougeSpec)` )`

Spec for rouge metric.

End of mutually exclusive fields.

**JSON representation**

```
{
  "aggregationMetrics": [
    enum (AggregationMetric)
  ],

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

`type` `enum ( `[`ComputationBasedMetricType`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.tuningJobs#ComputationBasedMetricType)` )`

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

`resultParserConfig` `object ( `[`EvaluationParserConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.tuningJobs#EvaluationParserConfig)` )`

Optional. The parser config for the metric result.

`rubrics_source` `Union type`

Source of the rubrics to be used for evaluation. The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:

`rubricGroupKey` `string`

Use a pre-defined group of rubrics associated with the input. Refers to a key in the rubricGroups map of EvaluationInstance.

`predefinedRubricGenerationSpec` `object ( `[`PredefinedMetricSpec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.tuningJobs#PredefinedMetricSpec)` )`

Dynamically generate rubrics using a predefined spec.

End of mutually exclusive fields.

`metricPromptTemplate` `string`

Required. Template for the prompt sent to the judge model.

`systemInstruction` `string`

Optional. System instructions for the judge model.

`judgeAutoraterConfig` `object ( `[`AutoraterConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.tuningJobs#AutoraterConfig)` )`

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

## AutoraterConfig

The configs for autorater. This is applicable to both EvaluateInstances and EvaluateDataset.

Fields

`autoraterModel` `string`

Optional. The fully qualified name of the publisher model or tuned autorater endpoint to use.

Publisher model format: `projects/{project}/locations/{location}/publishers/*/models/*`

Tuned model endpoint format: `projects/{project}/locations/{location}/endpoints/{endpoint}`

`generationConfig` `object ( `[`GenerationConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.tuningJobs#GenerationConfig)` )`

Optional. Configuration options for model generation and outputs.

`samplingCount` `integer`

Optional. Number of samples for each instance in the dataset. If not specified, the default is 4. Minimum value is 1, maximum value is 32.

`flipEnabled` `boolean`

Optional. Default is true. Whether to flip the candidate and baseline responses. This is only applicable to the pairwise metric. If enabled, also provide PairwiseMetricSpec.candidate_response_field_name and PairwiseMetricSpec.baseline_response_field_name. When rendering PairwiseMetricSpec.metric_prompt_template, the candidate and baseline fields will be flipped for half of the samples to reduce bias.

**JSON representation**

```
{
  "autoraterModel": string,
  "generationConfig": {
    object (GenerationConfig)
  },
  "samplingCount": integer,
  "flipEnabled": boolean
}
```

## GenerationConfig

Configuration for content generation.

This message contains all the parameters that control how the model generates content. It allows you to influence the randomness, length, and structure of the output.

Fields

`stopSequences[]` `string`

Optional. A list of character sequences that will stop the model from generating further tokens. If a stop sequence is generated, the output will end at that point. This is useful for controlling the length and structure of the output. For example, you can use \["\n", "###"\] to stop generation at a new line or a specific marker.

`responseMimeType `**`(deprecated)`** `string`

> This item is deprecated!

Optional. The IANA standard MIME type of the response. The model will generate output that conforms to this MIME type. Supported values include 'text/plain' (default) and 'application/json'. The model needs to be prompted to output the appropriate response type, otherwise the behavior is undefined. Deprecated: Use `responseFormat` instead.

`responseModalities[]` `enum ( `[`Modality`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.tuningJobs#Modality)` )`

Optional. The modalities of the response. The model will generate a response that includes all the specified modalities. For example, if this is set to `[TEXT, IMAGE]` , the response will include both text and an image.

`thinkingConfig` `object ( `[`ThinkingConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.tuningJobs#ThinkingConfig)` )`

Optional. Configuration for thinking features. An error will be returned if this field is set for models that don't support thinking.

`responseFormat[]` `object ( `[`ResponseFormat`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.tuningJobs#ResponseFormat)` )`

Optional. New response format field for the model to configure output formatting and delivery.

`temperature` `number`

Optional. Controls the randomness of the output. A higher temperature results in more creative and diverse responses, while a lower temperature makes the output more predictable and focused. The valid range is (0.0, 2.0\].

`topP` `number`

Optional. Specifies the nucleus sampling threshold. The model considers only the smallest set of tokens whose cumulative probability is at least `topP` . This helps generate more diverse and less repetitive responses. For example, a `topP` of 0.9 means the model considers tokens until the cumulative probability of the tokens to select from reaches 0.9. It's recommended to adjust either temperature or `topP` , but not both.

`topK` `number`

Optional. Specifies the top-k sampling threshold. The model considers only the top k most probable tokens for the next token. This can be useful for generating more coherent and less random text. For example, a `topK` of 40 means the model will choose the next word from the 40 most likely words.

`candidateCount` `integer`

Optional. The number of candidate responses to generate.

A higher `candidateCount` can provide more options to choose from, but it also consumes more resources. This can be useful for generating a variety of responses and selecting the best one.

`maxOutputTokens` `integer`

Optional. The maximum number of tokens to generate in the response.

A token is approximately four characters. The default value varies by model. This parameter can be used to control the length of the generated text and prevent overly long responses.

`responseLogprobs` `boolean`

Optional. If set to true, the log probabilities of the output tokens are returned.

log probabilities are the logarithm of the probability of a token appearing in the output. A higher log probability means the token is more likely to be generated. This can be useful for analyzing the model's confidence in its own output and for debugging.

`logprobs` `integer`

Optional. The number of top log probabilities to return for each token.

This can be used to see which other tokens were considered likely candidates for a given position. A higher value will return more options, but it will also increase the size of the response.

`presencePenalty` `number`

Optional. Penalizes tokens that have already appeared in the generated text. A positive value encourages the model to generate more diverse and less repetitive text. Valid values can range from \[-2.0, 2.0\].

`frequencyPenalty` `number`

Optional. Penalizes tokens based on their frequency in the generated text. A positive value helps to reduce the repetition of words and phrases. Valid values can range from \[-2.0, 2.0\].

`seed` `integer`

Optional. A seed for the random number generator.

By setting a seed, you can make the model's output mostly deterministic. For a given prompt and parameters (like temperature, topP, etc.), the model will produce the same response every time. However, it's not a guaranteed absolute deterministic behavior. This is different from parameters like `temperature` , which control the *level* of randomness. `seed` ensures that the "random" choices the model makes are the same on every run, making it essential for testing and ensuring reproducible results.

`responseSchema `**`(deprecated)`** `object ( `[`Schema`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/Schema)` )`

> This item is deprecated!

Optional. Lets you to specify a schema for the model's response, ensuring that the output conforms to a particular structure. This is useful for generating structured data such as JSON. The schema is a subset of the [OpenAPI 3.0 schema object](https://spec.openapis.org/oas/v3.0.3#schema) object.

When this field is set, you must also set the `responseMimeType` to `application/json` . Deprecated: Use `responseFormat` instead.

`responseJsonSchema `**`(deprecated)`** `value ( `[`Value`](https://protobuf.dev/reference/protobuf/google.protobuf/#value)` format)`

> This item is deprecated!

Optional. When this field is set, `responseSchema` must be omitted and `responseMimeType` must be set to `application/json` . Deprecated: Use `responseFormat` instead.

`routingConfig` `object ( `[`RoutingConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.tuningJobs#RoutingConfig)` )`

Optional. Routing configuration.

`audioTimestamp` `boolean`

Optional. If enabled, audio timestamps will be included in the request to the model. This can be useful for synchronizing audio with other modalities in the response.

`mediaResolution` `enum ( `[`MediaResolution`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.tuningJobs#MediaResolution)` )`

Optional. The token resolution at which input media content is sampled. This is used to control the trade-off between the quality of the response and the number of tokens used to represent the media. A higher resolution allows the model to perceive more detail, which can lead to a more nuanced response, but it will also use more tokens. This does not affect the image dimensions sent to the model.

`speechConfig` `object ( `[`SpeechConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.tuningJobs#SpeechConfig)` )`

Optional. The speech generation config.

`enableAffectiveDialog` `boolean`

Optional. If enabled, the model will detect emotions and adapt its responses accordingly. For example, if the model detects that the user is frustrated, it may provide a more empathetic response.

`imageConfig `**`(deprecated)`** `object ( `[`ImageConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.tuningJobs#ImageConfig)` )`

> This item is deprecated!

Optional. Config for image generation features. Deprecated: Use `responseFormat.image` instead.

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
  "responseFormat": [
    {
      object (ResponseFormat)
    }
  ],
  "temperature": number,
  "topP": number,
  "topK": number,
  "candidateCount": integer,
  "maxOutputTokens": integer,
  "responseLogprobs": boolean,
  "logprobs": integer,
  "presencePenalty": number,
  "frequencyPenalty": number,
  "seed": integer,
  "responseSchema": {
    object (Schema)
  },
  "responseJsonSchema": value,
  "routingConfig": {
    object (RoutingConfig)
  },
  "audioTimestamp": boolean,
  "mediaResolution": enum (MediaResolution),
  "speechConfig": {
    object (SpeechConfig)
  },
  "enableAffectiveDialog": boolean,
  "imageConfig": {
    object (ImageConfig)
  }
}
```

## RoutingConfig

The configuration for routing the request to a specific model. This can be used to control which model is used for the generation, either automatically or by specifying a model name.

Fields

`routing_config` `Union type`

The routing mode for the request. The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:

`autoMode` `object ( `[`AutoRoutingMode`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.tuningJobs#AutoRoutingMode)` )`

In this mode, the model is selected automatically based on the content of the request.

`manualMode` `object ( `[`ManualRoutingMode`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.tuningJobs#ManualRoutingMode)` )`

In this mode, the model is specified manually.

End of mutually exclusive fields.

**JSON representation**

```
{

  // routing_config
  "autoMode": {
    object (AutoRoutingMode)
  },
  "manualMode": {
    object (ManualRoutingMode)
  }
  // Union type
}
```

## AutoRoutingMode

The configuration for automated routing.

When automated routing is specified, the routing will be determined by the pretrained routing model and customer provided model routing preference.

Fields

`modelRoutingPreference` `enum ( `[`ModelRoutingPreference`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.tuningJobs#ModelRoutingPreference)` )`

The model routing preference.

**JSON representation**

```
{
  "modelRoutingPreference": enum (ModelRoutingPreference)
}
```

## ModelRoutingPreference

The model routing preference.

| Enums                |                                                                       |
|----------------------|-----------------------------------------------------------------------|
| `UNKNOWN`            | Unspecified model routing preference.                                 |
| `PRIORITIZE_QUALITY` | The model will be selected to prioritize the quality of the response. |
| `BALANCED`           | The model will be selected to balance quality and cost.               |
| `PRIORITIZE_COST`    | The model will be selected to prioritize the cost of the request.     |

## ManualRoutingMode

The configuration for manual routing.

When manual routing is specified, the model will be selected based on the model name provided.

Fields

`modelName` `string`

The name of the model to use. Only public LLM models are accepted.

**JSON representation**

```
{
  "modelName": string
}
```

## Modality

The modalities of the response.

| Enums                  |                                                  |
|------------------------|--------------------------------------------------|
| `MODALITY_UNSPECIFIED` | Unspecified modality. Will be processed as text. |
| `TEXT`                 | Text modality.                                   |
| `IMAGE`                | Image modality.                                  |
| `AUDIO`                | Audio modality.                                  |
| `VIDEO`                | Video modality.                                  |

## MediaResolution

Media resolution for the input media.

| Enums                          |                                                                  |
|--------------------------------|------------------------------------------------------------------|
| `MEDIA_RESOLUTION_UNSPECIFIED` | Media resolution has not been set.                               |
| `MEDIA_RESOLUTION_LOW`         | Media resolution set to low (64 tokens).                         |
| `MEDIA_RESOLUTION_MEDIUM`      | Media resolution set to medium (256 tokens).                     |
| `MEDIA_RESOLUTION_HIGH`        | Media resolution set to high (zoomed reframing with 256 tokens). |

## SpeechConfig

Configuration for speech generation.

Fields

`voiceConfig` `object ( `[`VoiceConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.tuningJobs#VoiceConfig)` )`

The configuration for the voice to use.

`languageCode` `string`

Optional. The language code (ISO 639-1) for the speech synthesis.

`multiSpeakerVoiceConfig` `object ( `[`MultiSpeakerVoiceConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.tuningJobs#MultiSpeakerVoiceConfig)` )`

The configuration for a multi-speaker text-to-speech request. This field is mutually exclusive with `voiceConfig` .

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

## VoiceConfig

Configuration for a voice.

Fields

`voice_config` `Union type`

The configuration for the speaker to use. The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:

`prebuiltVoiceConfig` `object ( `[`PrebuiltVoiceConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.tuningJobs#PrebuiltVoiceConfig)` )`

The configuration for a prebuilt voice.

`replicatedVoiceConfig` `object ( `[`ReplicatedVoiceConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.tuningJobs#ReplicatedVoiceConfig)` )`

Optional. The configuration for a replicated voice. This enables users to replicate a voice from an audio sample.

End of mutually exclusive fields.

**JSON representation**

```
{

  // voice_config
  "prebuiltVoiceConfig": {
    object (PrebuiltVoiceConfig)
  },
  "replicatedVoiceConfig": {
    object (ReplicatedVoiceConfig)
  }
  // Union type
}
```

## PrebuiltVoiceConfig

Configuration for a prebuilt voice.

Fields

`voiceName` `string`

The name of the prebuilt voice to use.

**JSON representation**

```
{
  "voiceName": string
}
```

## ReplicatedVoiceConfig

The configuration for the replicated voice to use.

Fields

`mimeType` `string`

Optional. The mimetype of the voice sample. The only currently supported value is `audio/wav` . This represents 16-bit signed little-endian wav data, with a 24kHz sampling rate. `mimeType` will default to `audio/wav` if not set.

`voiceSampleAudio` `string ( `[`bytes`](https://developers.google.com/discovery/v1/type-format)` format)`

Optional. The sample of the custom voice.

A base64-encoded string.

**JSON representation**

```
{
  "mimeType": string,
  "voiceSampleAudio": string
}
```

## MultiSpeakerVoiceConfig

Configuration for a multi-speaker text-to-speech request.

Fields

`speakerVoiceConfigs[]` `object ( `[`SpeakerVoiceConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.tuningJobs#SpeakerVoiceConfig)` )`

Required. A list of configurations for the voices of the speakers. Exactly two speaker voice configurations must be provided.

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

## SpeakerVoiceConfig

Configuration for a single speaker in a multi-speaker setup.

Fields

`speaker` `string`

Required. The name of the speaker. This should be the same as the speaker name used in the prompt.

`voiceConfig` `object ( `[`VoiceConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.tuningJobs#VoiceConfig)` )`

Required. The configuration for the voice of this speaker.

**JSON representation**

```
{
  "speaker": string,
  "voiceConfig": {
    object (VoiceConfig)
  }
}
```

## ThinkingConfig

Configuration for the model's thinking features.

"Thinking" is a process where the model breaks down a complex task into smaller, manageable steps. This allows the model to reason about the task, plan its approach, and execute the plan to generate a high-quality response.

Fields

`includeThoughts` `boolean`

Optional. If true, the model will include its thoughts in the response. "Thoughts" are the intermediate steps the model takes to arrive at the final response. They can provide insights into the model's reasoning process and help with debugging. If this is true, thoughts are returned only when available.

`thinkingBudget` `integer`

Optional. The token budget for the model's thinking process. The model will make a best effort to stay within this budget. This can be used to control the trade-off between response quality and latency.

`thinkingLevel` `enum ( `[`ThinkingLevel`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.tuningJobs#ThinkingLevel)` )`

Optional. The number of thoughts tokens that the model should generate.

**JSON representation**

```
{
  "includeThoughts": boolean,
  "thinkingBudget": integer,
  "thinkingLevel": enum (ThinkingLevel)
}
```

## ThinkingLevel

The thinking level for the model.

| Enums                        |                             |
|------------------------------|-----------------------------|
| `THINKING_LEVEL_UNSPECIFIED` | Unspecified thinking level. |
| `LOW`                        | Low thinking level.         |
| `MEDIUM`                     | Medium thinking level.      |
| `HIGH`                       | High thinking level.        |
| `MINIMAL`                    | MINIMAL thinking level.     |

## ImageConfig

Configuration for image generation.

This message allows you to control various aspects of image generation, such as the output format, aspect ratio, and whether the model can generate images of people.

Fields

`prominentPeople` `enum ( `[`ProminentPeople`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.tuningJobs#ProminentPeople)` )`

Optional. Controls whether prominent people (celebrities) generation is allowed. If used with personGeneration, personGeneration enum would take precedence. For instance, if ALLOW_NONE is set, all person generation would be blocked. If this field is unspecified, the default behavior is to allow prominent people.

`imageOutputOptions` `object ( `[`ImageOutputOptions`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.tuningJobs#ImageOutputOptions)` )`

Optional. The image output format for generated images.

`aspectRatio` `string`

Optional. The desired aspect ratio for the generated images. The following aspect ratios are supported:

"1:1" "2:3", "3:2" "3:4", "4:3" "4:5", "5:4" "9:16", "16:9" "21:9"

`personGeneration` `enum ( `[`PersonGeneration`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.tuningJobs#PersonGeneration)` )`

Optional. Controls whether the model can generate people.

`imageSize` `string`

Optional. Specifies the size of generated images. Supported values are `1K` , `2K` , `4K` . If not specified, the model will use default value `1K` .

**JSON representation**

```
{
  "prominentPeople": enum (ProminentPeople),
  "imageOutputOptions": {
    object (ImageOutputOptions)
  },
  "aspectRatio": string,
  "personGeneration": enum (PersonGeneration),
  "imageSize": string
}
```

## ImageOutputOptions

The image output format for generated images.

Fields

`mimeType` `string`

Optional. The image format that the output should be saved as.

`compressionQuality` `integer`

Optional. The compression quality of the output image.

**JSON representation**

```
{
  "mimeType": string,
  "compressionQuality": integer
}
```

## PersonGeneration

Enum for controlling the generation of people in images.

| Enums                           |                                                                                                  |
|---------------------------------|--------------------------------------------------------------------------------------------------|
| `PERSON_GENERATION_UNSPECIFIED` | The default behavior is unspecified. The model will decide whether to generate images of people. |
| `ALLOW_ALL`                     | Allows the model to generate images of people, including adults and children.                    |
| `ALLOW_ADULT`                   | Allows the model to generate images of adults, but not children.                                 |
| `ALLOW_NONE`                    | Prevents the model from generating images of people.                                             |

## ProminentPeople

Enum for controlling whether the model can generate images of prominent people (celebrities).

| Enums                          |                                                                                                                        |
|--------------------------------|------------------------------------------------------------------------------------------------------------------------|
| `PROMINENT_PEOPLE_UNSPECIFIED` | Unspecified value. The model will proceed with the default behavior, which is to allow generation of prominent people. |
| `ALLOW_PROMINENT_PEOPLE`       | Allows the model to generate images of prominent people.                                                               |
| `BLOCK_PROMINENT_PEOPLE`       | Prevents the model from generating images of prominent people.                                                         |

## ResponseFormat

Configuration for the model to configure output formatting and delivery.

Fields

`format` `Union type`

The format of the output content. The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:

`text` `object ( `[`TextResponseFormat`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.tuningJobs#TextResponseFormat)` )`

Text output format.

`audio` `object ( `[`AudioResponseFormat`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.tuningJobs#AudioResponseFormat)` )`

Audio output format.

`image` `object ( `[`ImageResponseFormat`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.tuningJobs#ImageResponseFormat)` )`

Image output format.

`video` `object ( `[`VideoResponseFormat`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.tuningJobs#VideoResponseFormat)` )`

Video output format.

End of mutually exclusive fields.

**JSON representation**

```
{

  // format
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
  // Union type
}
```

## TextResponseFormat

Configuration for text-specific output formatting.

Fields

`mimeType` `enum ( `[`MimeType`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.tuningJobs#MimeType)` )`

Optional. The IANA standard MIME type of the response.

`schema` `value ( `[`Value`](https://protobuf.dev/reference/protobuf/google.protobuf/#value)` format)`

Optional. The JSON schema that the output should conform to. Only applicable when mimeType is APPLICATION_JSON.

**JSON representation**

```
{
  "mimeType": enum (MimeType),
  "schema": value
}
```

## MimeType

Supported MIME types for text output.

| Enums                   |                                      |
|-------------------------|--------------------------------------|
| `MIME_TYPE_UNSPECIFIED` | Default value. This value is unused. |
| `APPLICATION_JSON`      | JSON output format.                  |
| `TEXT_PLAIN`            | Plain text output format.            |

## AudioResponseFormat

Configuration for audio-specific output formatting.

Fields

`delivery` `enum ( `[`DeliveryMode`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.tuningJobs#DeliveryMode)` )`

Optional. Delivery mode for the generated content.

`mimeType` `enum ( `[`MimeType`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.tuningJobs#MimeType_1)` )`

Optional. The MIME type of the audio output.

`sampleRate` `integer`

Optional. Sample rate for the generated audio in Hertz.

`bitRate` `integer`

Optional. Bit rate in bits per second (bps). Only applicable for compressed formats (MP3, Opus).

**JSON representation**

```
{
  "delivery": enum (DeliveryMode),
  "mimeType": enum (MimeType),
  "sampleRate": integer,
  "bitRate": integer
}
```

## MimeType

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

## DeliveryMode

The delivery mode for the output content.

| Enums                  |                                                      |
|------------------------|------------------------------------------------------|
| `DELIVERY_UNSPECIFIED` | Default value. This value is unused.                 |
| `INLINE`               | Generated bytes are returned inline in the response. |
| `URI`                  | Generated content is stored and a URI is returned.   |

## ImageResponseFormat

Configuration for image-specific output formatting.

Fields

`delivery` `enum ( `[`DeliveryMode`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.tuningJobs#DeliveryMode)` )`

Optional. Delivery mode for the generated content.

`mimeType` `enum ( `[`MimeType`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.tuningJobs#MimeType_2)` )`

Optional. The MIME type of the image output.

`aspectRatio` `enum ( `[`AspectRatio`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.tuningJobs#AspectRatio)` )`

Optional. The aspect ratio for the image output.

`imageSize` `enum ( `[`ImageSize`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.tuningJobs#ImageSize)` )`

Optional. The size of the image output.

**JSON representation**

```
{
  "delivery": enum (DeliveryMode),
  "mimeType": enum (MimeType),
  "aspectRatio": enum (AspectRatio),
  "imageSize": enum (ImageSize)
}
```

## MimeType

Supported MIME types for image output.

| Enums                   |                                      |
|-------------------------|--------------------------------------|
| `MIME_TYPE_UNSPECIFIED` | Default value. This value is unused. |
| `IMAGE_JPEG`            | JPEG image format.                   |

## AspectRatio

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

## ImageSize

Supported image sizes for image output.

| Enums                    |                                      |
|--------------------------|--------------------------------------|
| `IMAGE_SIZE_UNSPECIFIED` | Default value. This value is unused. |
| `IMAGE_SIZE_FIVE_TWELVE` | 512px image size.                    |
| `IMAGE_SIZE_ONE_K`       | 1K image size.                       |
| `IMAGE_SIZE_TWO_K`       | 2K image size.                       |
| `IMAGE_SIZE_FOUR_K`      | 4K image size.                       |

## VideoResponseFormat

Configuration for video-specific output formatting.

Fields

`delivery` `enum ( `[`DeliveryMode`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.tuningJobs#DeliveryMode)` )`

Optional. Delivery mode for the generated content.

`gcsUri` `string`

Optional. The Google Cloud Storage URI to store the video output. Required for Vertex if delivery is URI.

`aspectRatio` `enum ( `[`AspectRatio`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.tuningJobs#AspectRatio_1)` )`

The aspect ratio for the video output.

`resolution` `string`

Optional. The video output resolution. Supported values: "360p", "720p", "1080p", "4k".

`duration` `string ( `[`Duration`](https://protobuf.dev/reference/protobuf/google.protobuf/#duration)` format)`

Optional. The duration for the video output.

A duration in seconds with up to nine fractional digits, ending with ' `s` '. Example: `"3.5s"` .

**JSON representation**

```
{
  "delivery": enum (DeliveryMode),
  "gcsUri": string,
  "aspectRatio": enum (AspectRatio),
  "resolution": string,
  "duration": string
}
```

## AspectRatio

Supported aspect ratios for video output.

| Enums                          |                                      |
|--------------------------------|--------------------------------------|
| `ASPECT_RATIO_UNSPECIFIED`     | Default value. This value is unused. |
| `ASPECT_RATIO_SIXTEEN_BY_NINE` | 16:9 aspect ratio.                   |
| `ASPECT_RATIO_NINE_BY_SIXTEEN` | 9:16 aspect ratio.                   |

## EvaluationParserConfig

Config for parsing LLM responses. It can be used to parse the LLM response to be evaluated, or the LLM response from LLM-based metrics/Autoraters.

Fields

`parser` `Union type`

The parser to use. The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:

`customCodeParserConfig` `object ( `[`CustomCodeParserConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.tuningJobs#CustomCodeParserConfig)` )`

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
  "parsingFunction": string
}
```

## PointwiseMetricSpec

Spec for pointwise metric.

Fields

`customOutputFormatConfig` `object ( `[`CustomOutputFormatConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.tuningJobs#CustomOutputFormatConfig)` )`

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

`customOutputFormatConfig` `object ( `[`CustomOutputFormatConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.tuningJobs#CustomOutputFormatConfig)` )`

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

## AggregationMetric

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

## OutputConfig

Config for evaluation output.

Fields

`destination` `Union type`

The destination for evaluation output. The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:

`gcsDestination` `object ( `[`GcsDestination`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/CustomJobSpec#GcsDestination)` )`

Cloud storage destination for evaluation output.

End of mutually exclusive fields.

**JSON representation**

```
{

  // destination
  "gcsDestination": {
    object (GcsDestination)
  }
  // Union type
}
```

## TunedModel

The Model Registry Model and Online Prediction Endpoint associated with this [`TuningJob`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.tuningJobs#TuningJob) .

Fields

`model` `string`

Output only. The resource name of the TunedModel. Format:

`projects/{project}/locations/{location}/models/{model}@{versionId}`

When tuning from a base model, the version id will be 1.

For continuous tuning, if the provided tunedModelDisplayName is set and different from parent model's display name, the tuned model will have a new parent model with version 1. Otherwise the version id will be incremented by 1 from the last version id in the parent model. E.g.,

`projects/{project}/locations/{location}/models/{model}@{last_version_id + 1}`

`endpoint` `string`

Output only. A resource name of an Endpoint. Format: `projects/{project}/locations/{location}/endpoints/{endpoint}` .

`checkpoints[]` `object ( `[`TunedModelCheckpoint`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.tuningJobs#TunedModelCheckpoint)` )`

Output only. The checkpoints associated with this TunedModel. This field is only populated for tuning jobs that enable intermediate checkpoints.

**JSON representation**

```
{
  "model": string,
  "endpoint": string,
  "checkpoints": [
    {
      object (TunedModelCheckpoint)
    }
  ]
}
```

## TunedModelCheckpoint

TunedModelCheckpoint for the Tuned Model of a Tuning Job.

Fields

`checkpointId` `string`

The id of the checkpoint.

`epoch` `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)`

The epoch of the checkpoint.

`step` `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)`

The step of the checkpoint.

`endpoint` `string`

The Endpoint resource name that the checkpoint is deployed to. Format: `projects/{project}/locations/{location}/endpoints/{endpoint}` .

**JSON representation**

```
{
  "checkpointId": string,
  "epoch": string,
  "step": string,
  "endpoint": string
}
```

## TuningDataStats

The tuning data statistic values for [`TuningJob`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.tuningJobs#TuningJob) .

Fields

`tuning_data_stats` `Union type`

The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:

`supervisedTuningDataStats` `object ( `[`SupervisedTuningDataStats`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.tuningJobs#SupervisedTuningDataStats)` )`

The SFT Tuning data stats.

End of mutually exclusive fields.

**JSON representation**

```
{

  // tuning_data_stats
  "supervisedTuningDataStats": {
    object (SupervisedTuningDataStats)
  }
  // Union type
}
```

## SupervisedTuningDataStats

Tuning data statistics for Supervised Tuning.

Fields

`tuningDatasetExampleCount` `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)`

Output only. Number of examples in the tuning dataset.

`totalTuningCharacterCount` `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)`

Output only. Number of tuning characters in the tuning dataset.

`totalBillableCharacterCount `**`(deprecated)`** `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)`

> This item is deprecated!

Output only. Number of billable characters in the tuning dataset.

`totalBillableTokenCount` `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)`

Output only. Number of billable tokens in the tuning dataset.

`tuningStepCount` `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)`

Output only. Number of tuning steps for this Tuning Job.

`userInputTokenDistribution` `object ( `[`SupervisedTuningDatasetDistribution`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.tuningJobs#SupervisedTuningDatasetDistribution)` )`

Output only. Dataset distributions for the user input tokens.

`userOutputTokenDistribution` `object ( `[`SupervisedTuningDatasetDistribution`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.tuningJobs#SupervisedTuningDatasetDistribution)` )`

Output only. Dataset distributions for the user output tokens.

`userMessagePerExampleDistribution` `object ( `[`SupervisedTuningDatasetDistribution`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.tuningJobs#SupervisedTuningDatasetDistribution)` )`

Output only. Dataset distributions for the messages per example.

`userDatasetExamples[]` `object ( `[`Content`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/Content)` )`

Output only. Sample user messages in the training dataset uri.

`totalTruncatedExampleCount` `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)`

Output only. The number of examples in the dataset that have been dropped. An example can be dropped for reasons including: too many tokens, contains an invalid image, contains too many images, etc.

`truncatedExampleIndices[]` `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)`

Output only. A partial sample of the indices (starting from 1) of the dropped examples.

`droppedExampleReasons[]` `string`

Output only. For each index in `truncatedExampleIndices` , the user-facing reason why the example was dropped.

**JSON representation**

```
{
  "tuningDatasetExampleCount": string,
  "totalTuningCharacterCount": string,
  "totalBillableCharacterCount": string,
  "totalBillableTokenCount": string,
  "tuningStepCount": string,
  "userInputTokenDistribution": {
    object (SupervisedTuningDatasetDistribution)
  },
  "userOutputTokenDistribution": {
    object (SupervisedTuningDatasetDistribution)
  },
  "userMessagePerExampleDistribution": {
    object (SupervisedTuningDatasetDistribution)
  },
  "userDatasetExamples": [
    {
      object (Content)
    }
  ],
  "totalTruncatedExampleCount": string,
  "truncatedExampleIndices": [
    string
  ],
  "droppedExampleReasons": [
    string
  ]
}
```

## SupervisedTuningDatasetDistribution

Dataset distribution for Supervised Tuning.

Fields

`sum` `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)`

Output only. Sum of a given population of values.

`billableSum` `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)`

Output only. Sum of a given population of values that are billable.

`min` `number`

Output only. The minimum of the population values.

`max` `number`

Output only. The maximum of the population values.

`mean` `number`

Output only. The arithmetic mean of the values in the population.

`median` `number`

Output only. The median of the values in the population.

`p5` `number`

Output only. The 5th percentile of the values in the population.

`p95` `number`

Output only. The 95th percentile of the values in the population.

`buckets[]` `object ( `[`DatasetBucket`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.tuningJobs#DatasetBucket)` )`

Output only. Defines the histogram bucket.

**JSON representation**

```
{
  "sum": string,
  "billableSum": string,
  "min": number,
  "max": number,
  "mean": number,
  "median": number,
  "p5": number,
  "p95": number,
  "buckets": [
    {
      object (DatasetBucket)
    }
  ]
}
```

## DatasetBucket

Dataset bucket used to create a histogram for the distribution given a population of values.

Fields

`count` `number`

Output only. Number of values in the bucket.

`left` `number`

Output only. left bound of the bucket.

`right` `number`

Output only. Right bound of the bucket.

**JSON representation**

```
{
  "count": number,
  "left": number,
  "right": number
}
```

## EvaluateDatasetRun

Evaluate Dataset Run result for Tuning Job.

Fields

`operationName `**`(deprecated)`** `string`

> This item is deprecated!

Output only. Deprecated: The updated architecture uses evaluationRun instead.

`evaluationRun` `string`

Output only. The resource name of the evaluation run. Format: `projects/{project}/locations/{location}/evaluationRuns/{evaluation_run_id}` .

`checkpointId` `string`

Output only. The checkpoint id used in the evaluation run. Only populated when evaluating checkpoints.

`evaluateDatasetResponse` `object ( `[`EvaluateDatasetResponse`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.tuningJobs#EvaluateDatasetResponse)` )`

Output only. Results for EvaluationService.

`error` `object ( `[`Status`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/ListOperationsResponse#Status)` )`

Output only. The error of the evaluation run if any.

**JSON representation**

```
{
  "operationName": string,
  "evaluationRun": string,
  "checkpointId": string,
  "evaluateDatasetResponse": {
    object (EvaluateDatasetResponse)
  },
  "error": {
    object (Status)
  }
}
```

## EvaluateDatasetResponse

The results from an evaluation run performed by the EvaluationService.

Fields

`aggregationOutput` `object ( `[`AggregationOutput`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.tuningJobs#AggregationOutput)` )`

Output only. Aggregation statistics derived from results of EvaluationService.

`outputInfo` `object ( `[`OutputInfo`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.tuningJobs#OutputInfo)` )`

Output only. Output info for EvaluationService.

**JSON representation**

```
{
  "aggregationOutput": {
    object (AggregationOutput)
  },
  "outputInfo": {
    object (OutputInfo)
  }
}
```

## AggregationOutput

The aggregation result for the entire dataset and all metrics.

Fields

`dataset` `object ( `[`EvaluationDataset`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.tuningJobs#EvaluationDataset)` )`

The dataset used for evaluation & aggregation.

`aggregationResults[]` `object ( `[`AggregationResult`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.tuningJobs#AggregationResult)` )`

One AggregationResult per metric.

**JSON representation**

```
{
  "dataset": {
    object (EvaluationDataset)
  },
  "aggregationResults": [
    {
      object (AggregationResult)
    }
  ]
}
```

## EvaluationDataset

The dataset used for evaluation.

Fields

`source` `Union type`

The source of the dataset. The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:

`gcsSource` `object ( `[`GcsSource`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/GcsSource)` )`

Cloud storage source holds the dataset. Currently only one Cloud Storage file path is supported.

`bigquerySource` `object ( `[`BigQuerySource`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/BigQuerySource)` )`

BigQuery source holds the dataset.

End of mutually exclusive fields.

**JSON representation**

```
{

  // source
  "gcsSource": {
    object (GcsSource)
  },
  "bigquerySource": {
    object (BigQuerySource)
  }
  // Union type
}
```

## AggregationResult

The aggregation result for a single metric.

Fields

`aggregation_result` `Union type`

The aggregation result. The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:

`pointwiseMetricResult` `object ( `[`PointwiseMetricResult`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.tuningJobs#PointwiseMetricResult)` )`

result for pointwise metric.

`pairwiseMetricResult` `object ( `[`PairwiseMetricResult`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.tuningJobs#PairwiseMetricResult)` )`

result for pairwise metric.

`exactMatchMetricValue` `object ( `[`ExactMatchMetricValue`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.tuningJobs#ExactMatchMetricValue)` )`

Results for exact match metric.

`bleuMetricValue` `object ( `[`BleuMetricValue`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.tuningJobs#BleuMetricValue)` )`

Results for bleu metric.

`rougeMetricValue` `object ( `[`RougeMetricValue`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.tuningJobs#RougeMetricValue)` )`

Results for rouge metric.

End of mutually exclusive fields.

**JSON representation**

```
{

  // aggregation_result
  "pointwiseMetricResult": {
    object (PointwiseMetricResult)
  },
  "pairwiseMetricResult": {
    object (PairwiseMetricResult)
  },
  "exactMatchMetricValue": {
    object (ExactMatchMetricValue)
  },
  "bleuMetricValue": {
    object (BleuMetricValue)
  },
  "rougeMetricValue": {
    object (RougeMetricValue)
  }
  // Union type
}
```

## PointwiseMetricResult

Spec for pointwise metric result.

Fields

`explanation` `string`

Output only. Explanation for pointwise metric score.

`customOutput` `object ( `[`CustomOutput`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.tuningJobs#CustomOutput)` )`

Output only. Spec for custom output.

`score` `number`

Output only. Pointwise metric score.

**JSON representation**

```
{
  "explanation": string,
  "customOutput": {
    object (CustomOutput)
  },
  "score": number
}
```

## CustomOutput

Spec for custom output.

Fields

`custom_output` `Union type`

Custom output. The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:

`rawOutputs` `object ( `[`RawOutput`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.tuningJobs#RawOutput)` )`

Output only. List of raw output strings.

End of mutually exclusive fields.

**JSON representation**

```
{

  // custom_output
  "rawOutputs": {
    object (RawOutput)
  }
  // Union type
}
```

## RawOutput

Raw output.

Fields

`rawOutput[]` `string`

Output only. Raw output string.

**JSON representation**

```
{
  "rawOutput": [
    string
  ]
}
```

## PairwiseMetricResult

Spec for pairwise metric result.

Fields

`pairwiseChoice` `enum ( `[`PairwiseChoice`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.tuningJobs#PairwiseChoice)` )`

Output only. Pairwise metric choice.

`explanation` `string`

Output only. Explanation for pairwise metric score.

`customOutput` `object ( `[`CustomOutput`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.tuningJobs#CustomOutput)` )`

Output only. Spec for custom output.

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

## PairwiseChoice

Pairwise prediction autorater preference.

| Enums                         |                                |
|-------------------------------|--------------------------------|
| `PAIRWISE_CHOICE_UNSPECIFIED` | Unspecified prediction choice. |
| `BASELINE`                    | baseline prediction wins       |
| `CANDIDATE`                   | Candidate prediction wins      |
| `TIE`                         | Winner cannot be determined    |

## ExactMatchMetricValue

Exact match metric value for an instance.

Fields

`score` `number`

Output only. Exact match score.

**JSON representation**

```
{
  "score": number
}
```

## BleuMetricValue

Bleu metric value for an instance.

Fields

`score` `number`

Output only. Bleu score.

**JSON representation**

```
{
  "score": number
}
```

## RougeMetricValue

Rouge metric value for an instance.

Fields

`score` `number`

Output only. Rouge score.

**JSON representation**

```
{
  "score": number
}
```

## OutputInfo

Describes the info for output of EvaluationService.

Fields

`output_location` `Union type`

The output location into which evaluation output is written. The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:

`gcsOutputDirectory` `string`

Output only. The full path of the Cloud Storage directory created, into which the evaluation results and aggregation results are written.

End of mutually exclusive fields.

**JSON representation**

```
{

  // output_location
  "gcsOutputDirectory": string
  // Union type
}
```

| Methods                                                                                                                                               |                                  |
|-------------------------------------------------------------------------------------------------------------------------------------------------------|----------------------------------|
| [`cancel`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.tuningJobs/cancel)                     | Cancels a tuning job.            |
| [`create`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.tuningJobs/create)                     | Creates a tuning job.            |
| [`get`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.tuningJobs/get)                           | Gets a tuning job.               |
| [`list`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.tuningJobs/list)                         | Lists tuning jobs in a location. |
| [`rebaseTunedModel`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.tuningJobs/rebaseTunedModel) | Rebase a tuned model.            |
