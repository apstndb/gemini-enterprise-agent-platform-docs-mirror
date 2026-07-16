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

Optional. The display name of the `  TunedModel  ` . The name can be up to 128 characters long and can consist of any UTF-8 characters. For continuous tuning, tunedModelDisplayName will by default use the same display name as the pre-tuned model. If a new display name is provided, the tuning job will create a new model instead of a new version.

`description` `string`

Optional. The description of the `  TuningJob  ` .

`state` ` enum ( JobState  ` )

Output only. The detailed state of the job.

`createTime` ` string ( Timestamp  ` format)

Output only. time when the `  TuningJob  ` was created.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`startTime` ` string ( Timestamp  ` format)

Output only. time when the `  TuningJob  ` for the first time entered the `JOB_STATE_RUNNING` state.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`endTime` ` string ( Timestamp  ` format)

Output only. time when the TuningJob entered any of the following `  JobStates  ` : `JOB_STATE_SUCCEEDED` , `JOB_STATE_FAILED` , `JOB_STATE_CANCELLED` , `JOB_STATE_EXPIRED` .

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`updateTime` ` string ( Timestamp  ` format)

Output only. time when the `  TuningJob  ` was most recently updated.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`error` ` object ( Status  ` )

Output only. Only populated when job's state is `JOB_STATE_FAILED` or `JOB_STATE_CANCELLED` .

`labels` `map (key: string, value: string)`

Optional. The labels with user-defined metadata to organize `  TuningJob  ` and generated resources such as `  Model  ` and `  Endpoint  ` .

label keys and values can be no longer than 64 characters (Unicode codepoints), can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed.

See <https://goo.gl/xmQnxf> for more information and examples of labels.

`experiment` `string`

Output only. The Experiment associated with this `  TuningJob  ` .

`tunedModel` ` object ( TunedModel  ` )

Output only. The tuned model resources associated with this `  TuningJob  ` .

`tuningDataStats` ` object ( TuningDataStats  ` )

Output only. The tuning data statistics associated with this `  TuningJob  ` .

`encryptionSpec` ` object ( EncryptionSpec  ` )

Customer-managed encryption key options for a TuningJob. If this is set, then all resources created by the TuningJob will be encrypted with the provided encryption key.

`serviceAccount` `string`

The service account that the tuningJob workload runs as. If not specified, the Agent Platform Secure Fine-Tuned service Agent in the project will be used. See <https://cloud.google.com/iam/docs/service-agents#vertex-ai-secure-fine-tuning-service-agent>

Users starting the pipeline must have the `iam.serviceAccounts.actAs` permission on this service account.

`evaluateDatasetRuns[]` ` object ( EvaluateDatasetRun  ` )

Output only. Evaluation runs for the Tuning Job.

`source_model` `Union type`

`source_model` can be only one of the following:

`baseModel` `string`

The base model that is being tuned. See [Supported models](https://cloud.google.com/vertex-ai/generative-ai/docs/model-reference/tuning#supported_models) .

`preTunedModel` ` object ( PreTunedModel  ` )

The pre-tuned model for continuous tuning.

`tuning_spec` `Union type`

`tuning_spec` can be only one of the following:

`supervisedTuningSpec` ` object ( SupervisedTuningSpec  ` )

Tuning Spec for Supervised Fine Tuning.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;name&quot;: string,&quot;tunedModelDisplayName&quot;: string,&quot;description&quot;: string,&quot;state&quot;: enum (JobState),&quot;createTime&quot;: string,&quot;startTime&quot;: string,&quot;endTime&quot;: string,&quot;updateTime&quot;: string,&quot;error&quot;: {object (Status)},&quot;labels&quot;: {string: string,...},&quot;experiment&quot;: string,&quot;tunedModel&quot;: {object (TunedModel)},&quot;tuningDataStats&quot;: {object (TuningDataStats)},&quot;encryptionSpec&quot;: {object (EncryptionSpec)},&quot;serviceAccount&quot;: string,&quot;evaluateDatasetRuns&quot;: [{object (EvaluateDatasetRun)}],// source_model&quot;baseModel&quot;: string,&quot;preTunedModel&quot;: {object (PreTunedModel)}// Union type// tuning_spec&quot;supervisedTuningSpec&quot;: {object (SupervisedTuningSpec)}// Union type}</code></pre></td>
</tr>
</tbody>
</table>

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

Output only. The name of the base model this `  PreTunedModel  ` was tuned from.

<table>
<colgroup>
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
  &quot;tunedModelName&quot;: string,
  &quot;checkpointId&quot;: string,
  &quot;baseModel&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

## SupervisedTuningSpec

Tuning Spec for Supervised Tuning for first party models.

Fields

`trainingDatasetUri` `string`

Required. Training dataset used for tuning. The dataset can be specified as either a Cloud Storage path to a JSONL file or as the resource name of a Vertex Multimodal Dataset.

`validationDatasetUri` `string`

Optional. Validation dataset used for tuning. The dataset can be specified as either a Cloud Storage path to a JSONL file or as the resource name of a Vertex Multimodal Dataset.

`hyperParameters` ` object ( SupervisedHyperParameters  ` )

Optional. Hyperparameters for SFT.

`exportLastCheckpointOnly` `boolean`

Optional. If set to true, disable intermediate checkpoints for SFT and only the last checkpoint will be exported. Otherwise, enable intermediate checkpoints for SFT. Default is false.

`evaluationConfig` ` object ( EvaluationConfig  ` )

Optional. Evaluation Config for Tuning Job.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;trainingDatasetUri&quot;: string,&quot;validationDatasetUri&quot;: string,&quot;hyperParameters&quot;: {object (SupervisedHyperParameters)},&quot;exportLastCheckpointOnly&quot;: boolean,&quot;evaluationConfig&quot;: {object (EvaluationConfig)}}</code></pre></td>
</tr>
</tbody>
</table>

## SupervisedHyperParameters

Hyperparameters for SFT.

Fields

`epochCount` `string ( int64 format)`

Optional. Number of complete passes the model makes over the entire training dataset during training.

`learningRateMultiplier` `number`

Optional. Multiplier for adjusting the default learning rate. Mutually exclusive with `learningRate` . This feature is only available for 1P models.

`adapterSize` ` enum ( AdapterSize  ` )

Optional. Adapter size for tuning.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;epochCount&quot;: string,&quot;learningRateMultiplier&quot;: number,&quot;adapterSize&quot;: enum (AdapterSize)}</code></pre></td>
</tr>
</tbody>
</table>

## AdapterSize

Supported adapter sizes for tuning.

Enums

`ADAPTER_SIZE_UNSPECIFIED`

Adapter size is unspecified.

`ADAPTER_SIZE_ONE`

Adapter size 1.

`ADAPTER_SIZE_TWO`

Adapter size 2.

`ADAPTER_SIZE_FOUR`

Adapter size 4.

`ADAPTER_SIZE_EIGHT`

Adapter size 8.

`ADAPTER_SIZE_SIXTEEN`

Adapter size 16.

`ADAPTER_SIZE_THIRTY_TWO`

Adapter size 32.

## EvaluationConfig

Evaluation Config for Tuning Job.

Fields

`metrics[]` ` object ( Metric  ` )

Required. The metrics used for evaluation.

`outputConfig` ` object ( OutputConfig  ` )

Required. Config for evaluation output.

`autoraterConfig` ` object ( AutoraterConfig  ` )

Optional. Autorater config for evaluation.

`inferenceGenerationConfig` ` object ( GenerationConfig  ` )

Optional. Configuration options for inference generation and outputs. If not set, default generation parameters are used.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;metrics&quot;: [{object (Metric)}],&quot;outputConfig&quot;: {object (OutputConfig)},&quot;autoraterConfig&quot;: {object (AutoraterConfig)},&quot;inferenceGenerationConfig&quot;: {object (GenerationConfig)}}</code></pre></td>
</tr>
</tbody>
</table>

## Metric

The metric used for running evaluations.

Fields

`aggregationMetrics[]` ` enum ( AggregationMetric  ` )

Optional. The aggregation metrics to use.

`metric_spec` `Union type`

The spec for the metric. It would be either a pre-defined metric, or a inline metric spec. `metric_spec` can be only one of the following:

`predefinedMetricSpec` ` object ( PredefinedMetricSpec  ` )

The spec for a pre-defined metric.

`computationBasedMetricSpec` ` object ( ComputationBasedMetricSpec  ` )

Spec for a computation based metric.

`llmBasedMetricSpec` ` object ( LLMBasedMetricSpec  ` )

Spec for an LLM based metric.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;aggregationMetrics&quot;: [enum (AggregationMetric)],// metric_spec&quot;predefinedMetricSpec&quot;: {object (PredefinedMetricSpec)},&quot;computationBasedMetricSpec&quot;: {object (ComputationBasedMetricSpec)},&quot;llmBasedMetricSpec&quot;: {object (LLMBasedMetricSpec)},&quot;pointwiseMetricSpec&quot;: {object (PointwiseMetricSpec)},&quot;pairwiseMetricSpec&quot;: {object (PairwiseMetricSpec)},&quot;exactMatchSpec&quot;: {object (ExactMatchSpec)},&quot;bleuSpec&quot;: {object (BleuSpec)},&quot;rougeSpec&quot;: {object (RougeSpec)}// Union type}</code></pre></td>
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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;resultParserConfig&quot;: {object (EvaluationParserConfig)},// rubrics_source&quot;rubricGroupKey&quot;: string,&quot;predefinedRubricGenerationSpec&quot;: {object (PredefinedMetricSpec)}// Union type&quot;metricPromptTemplate&quot;: string,&quot;systemInstruction&quot;: string,&quot;judgeAutoraterConfig&quot;: {object (AutoraterConfig)},&quot;additionalConfig&quot;: {object}}</code></pre></td>
</tr>
</tbody>
</table>

## AutoraterConfig

The configs for autorater. This is applicable to both EvaluateInstances and EvaluateDataset.

Fields

`autoraterModel` `string`

Optional. The fully qualified name of the publisher model or tuned autorater endpoint to use.

Publisher model format: `projects/{project}/locations/{location}/publishers/*/models/*`

Tuned model endpoint format: `projects/{project}/locations/{location}/endpoints/{endpoint}`

`generationConfig` ` object ( GenerationConfig  ` )

Optional. Configuration options for model generation and outputs.

`samplingCount` `integer`

Optional. Number of samples for each instance in the dataset. If not specified, the default is 4. Minimum value is 1, maximum value is 32.

`flipEnabled` `boolean`

Optional. Default is true. Whether to flip the candidate and baseline responses. This is only applicable to the pairwise metric. If enabled, also provide PairwiseMetricSpec.candidate\_response\_field\_name and PairwiseMetricSpec.baseline\_response\_field\_name. When rendering PairwiseMetricSpec.metric\_prompt\_template, the candidate and baseline fields will be flipped for half of the samples to reduce bias.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;autoraterModel&quot;: string,&quot;generationConfig&quot;: {object (GenerationConfig)},&quot;samplingCount&quot;: integer,&quot;flipEnabled&quot;: boolean}</code></pre></td>
</tr>
</tbody>
</table>

## GenerationConfig

Configuration for content generation.

This message contains all the parameters that control how the model generates content. It allows you to influence the randomness, length, and structure of the output.

Fields

`stopSequences[]` `string`

Optional. A list of character sequences that will stop the model from generating further tokens. If a stop sequence is generated, the output will end at that point. This is useful for controlling the length and structure of the output. For example, you can use \["\\n", "\#\#\#"\] to stop generation at a new line or a specific marker.

` responseMimeType (deprecated)  ` `string`

> This item is deprecated\!

Optional. The IANA standard MIME type of the response. The model will generate output that conforms to this MIME type. Supported values include 'text/plain' (default) and 'application/json'. The model needs to be prompted to output the appropriate response type, otherwise the behavior is undefined. Deprecated: Use `responseFormat` instead.

`responseModalities[]` ` enum ( Modality  ` )

Optional. The modalities of the response. The model will generate a response that includes all the specified modalities. For example, if this is set to `[TEXT, IMAGE]` , the response will include both text and an image.

`thinkingConfig` ` object ( ThinkingConfig  ` )

Optional. Configuration for thinking features. An error will be returned if this field is set for models that don't support thinking.

`responseFormat[]` ` object ( ResponseFormat  ` )

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

` responseSchema (deprecated)  ` ` object ( Schema  ` )

> This item is deprecated\!

Optional. Lets you to specify a schema for the model's response, ensuring that the output conforms to a particular structure. This is useful for generating structured data such as JSON. The schema is a subset of the [OpenAPI 3.0 schema object](https://spec.openapis.org/oas/v3.0.3#schema) object.

When this field is set, you must also set the `responseMimeType` to `application/json` . Deprecated: Use `responseFormat` instead.

` responseJsonSchema (deprecated)  ` ` value ( Value  ` format)

> This item is deprecated\!

Optional. When this field is set, `responseSchema` must be omitted and `responseMimeType` must be set to `application/json` . Deprecated: Use `responseFormat` instead.

`routingConfig` ` object ( RoutingConfig  ` )

Optional. Routing configuration.

`audioTimestamp` `boolean`

Optional. If enabled, audio timestamps will be included in the request to the model. This can be useful for synchronizing audio with other modalities in the response.

`mediaResolution` ` enum ( MediaResolution  ` )

Optional. The token resolution at which input media content is sampled. This is used to control the trade-off between the quality of the response and the number of tokens used to represent the media. A higher resolution allows the model to perceive more detail, which can lead to a more nuanced response, but it will also use more tokens. This does not affect the image dimensions sent to the model.

`speechConfig` ` object ( SpeechConfig  ` )

Optional. The speech generation config.

`enableAffectiveDialog` `boolean`

Optional. If enabled, the model will detect emotions and adapt its responses accordingly. For example, if the model detects that the user is frustrated, it may provide a more empathetic response.

` imageConfig (deprecated)  ` ` object ( ImageConfig  ` )

> This item is deprecated\!

Optional. Config for image generation features. Deprecated: Use `responseFormat.image` instead.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;stopSequences&quot;: [string],&quot;responseMimeType&quot;: string,&quot;responseModalities&quot;: [enum (Modality)],&quot;thinkingConfig&quot;: {object (ThinkingConfig)},&quot;responseFormat&quot;: [{object (ResponseFormat)}],&quot;temperature&quot;: number,&quot;topP&quot;: number,&quot;topK&quot;: number,&quot;candidateCount&quot;: integer,&quot;maxOutputTokens&quot;: integer,&quot;responseLogprobs&quot;: boolean,&quot;logprobs&quot;: integer,&quot;presencePenalty&quot;: number,&quot;frequencyPenalty&quot;: number,&quot;seed&quot;: integer,&quot;responseSchema&quot;: {object (Schema)},&quot;responseJsonSchema&quot;: value,&quot;routingConfig&quot;: {object (RoutingConfig)},&quot;audioTimestamp&quot;: boolean,&quot;mediaResolution&quot;: enum (MediaResolution),&quot;speechConfig&quot;: {object (SpeechConfig)},&quot;enableAffectiveDialog&quot;: boolean,&quot;imageConfig&quot;: {object (ImageConfig)}}</code></pre></td>
</tr>
</tbody>
</table>

## RoutingConfig

The configuration for routing the request to a specific model. This can be used to control which model is used for the generation, either automatically or by specifying a model name.

Fields

`routing_config` `Union type`

The routing mode for the request. `routing_config` can be only one of the following:

`autoMode` ` object ( AutoRoutingMode  ` )

In this mode, the model is selected automatically based on the content of the request.

`manualMode` ` object ( ManualRoutingMode  ` )

In this mode, the model is specified manually.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{// routing_config&quot;autoMode&quot;: {object (AutoRoutingMode)},&quot;manualMode&quot;: {object (ManualRoutingMode)}// Union type}</code></pre></td>
</tr>
</tbody>
</table>

## AutoRoutingMode

The configuration for automated routing.

When automated routing is specified, the routing will be determined by the pretrained routing model and customer provided model routing preference.

Fields

`modelRoutingPreference` ` enum ( ModelRoutingPreference  ` )

The model routing preference.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;modelRoutingPreference&quot;: enum (ModelRoutingPreference)}</code></pre></td>
</tr>
</tbody>
</table>

## ModelRoutingPreference

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

## ManualRoutingMode

The configuration for manual routing.

When manual routing is specified, the model will be selected based on the model name provided.

Fields

`modelName` `string`

The name of the model to use. Only public LLM models are accepted.

<table>
<colgroup>
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
  &quot;modelName&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

## Modality

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

## MediaResolution

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

## SpeechConfig

Configuration for speech generation.

Fields

`voiceConfig` ` object ( VoiceConfig  ` )

The configuration for the voice to use.

`languageCode` `string`

Optional. The language code (ISO 639-1) for the speech synthesis.

`multiSpeakerVoiceConfig` ` object ( MultiSpeakerVoiceConfig  ` )

The configuration for a multi-speaker text-to-speech request. This field is mutually exclusive with `voiceConfig` .

<table>
<colgroup>
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

## VoiceConfig

Configuration for a voice.

Fields

`voice_config` `Union type`

The configuration for the speaker to use. `voice_config` can be only one of the following:

`prebuiltVoiceConfig` ` object ( PrebuiltVoiceConfig  ` )

The configuration for a prebuilt voice.

`replicatedVoiceConfig` ` object ( ReplicatedVoiceConfig  ` )

Optional. The configuration for a replicated voice. This enables users to replicate a voice from an audio sample.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{// voice_config&quot;prebuiltVoiceConfig&quot;: {object (PrebuiltVoiceConfig)},&quot;replicatedVoiceConfig&quot;: {object (ReplicatedVoiceConfig)}// Union type}</code></pre></td>
</tr>
</tbody>
</table>

## PrebuiltVoiceConfig

Configuration for a prebuilt voice.

Fields

`voiceName` `string`

The name of the prebuilt voice to use.

<table>
<colgroup>
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
  &quot;voiceName&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

## ReplicatedVoiceConfig

The configuration for the replicated voice to use.

Fields

`mimeType` `string`

Optional. The mimetype of the voice sample. The only currently supported value is `audio/wav` . This represents 16-bit signed little-endian wav data, with a 24kHz sampling rate. `mimeType` will default to `audio/wav` if not set.

`voiceSampleAudio` `string ( bytes format)`

Optional. The sample of the custom voice.

A base64-encoded string.

<table>
<colgroup>
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

## MultiSpeakerVoiceConfig

Configuration for a multi-speaker text-to-speech request.

Fields

`speakerVoiceConfigs[]` ` object ( SpeakerVoiceConfig  ` )

Required. A list of configurations for the voices of the speakers. Exactly two speaker voice configurations must be provided.

<table>
<colgroup>
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

## SpeakerVoiceConfig

Configuration for a single speaker in a multi-speaker setup.

Fields

`speaker` `string`

Required. The name of the speaker. This should be the same as the speaker name used in the prompt.

`voiceConfig` ` object ( VoiceConfig  ` )

Required. The configuration for the voice of this speaker.

<table>
<colgroup>
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

## ThinkingConfig

Configuration for the model's thinking features.

"Thinking" is a process where the model breaks down a complex task into smaller, manageable steps. This allows the model to reason about the task, plan its approach, and execute the plan to generate a high-quality response.

Fields

`includeThoughts` `boolean`

Optional. If true, the model will include its thoughts in the response. "Thoughts" are the intermediate steps the model takes to arrive at the final response. They can provide insights into the model's reasoning process and help with debugging. If this is true, thoughts are returned only when available.

`thinkingBudget` `integer`

Optional. The token budget for the model's thinking process. The model will make a best effort to stay within this budget. This can be used to control the trade-off between response quality and latency.

`thinkingLevel` ` enum ( ThinkingLevel  ` )

Optional. The number of thoughts tokens that the model should generate.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;includeThoughts&quot;: boolean,&quot;thinkingBudget&quot;: integer,&quot;thinkingLevel&quot;: enum (ThinkingLevel)}</code></pre></td>
</tr>
</tbody>
</table>

## ThinkingLevel

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

## ImageConfig

Configuration for image generation.

This message allows you to control various aspects of image generation, such as the output format, aspect ratio, and whether the model can generate images of people.

Fields

`imageOutputOptions` ` object ( ImageOutputOptions  ` )

Optional. The image output format for generated images.

`aspectRatio` `string`

Optional. The desired aspect ratio for the generated images. The following aspect ratios are supported:

"1:1" "2:3", "3:2" "3:4", "4:3" "4:5", "5:4" "9:16", "16:9" "21:9"

`personGeneration` ` enum ( PersonGeneration  ` )

Optional. Controls whether the model can generate people.

`imageSize` `string`

Optional. Specifies the size of generated images. Supported values are `1K` , `2K` , `4K` . If not specified, the model will use default value `1K` .

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;imageOutputOptions&quot;: {object (ImageOutputOptions)},&quot;aspectRatio&quot;: string,&quot;personGeneration&quot;: enum (PersonGeneration),&quot;imageSize&quot;: string}</code></pre></td>
</tr>
</tbody>
</table>

## ImageOutputOptions

The image output format for generated images.

Fields

`mimeType` `string`

Optional. The image format that the output should be saved as.

`compressionQuality` `integer`

Optional. The compression quality of the output image.

<table>
<colgroup>
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
  &quot;compressionQuality&quot;: integer
}</code></pre></td>
</tr>
</tbody>
</table>

## PersonGeneration

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

## ResponseFormat

Configuration for the model to configure output formatting and delivery.

Fields

`format` `Union type`

The format of the output content. `format` can be only one of the following:

`text` ` object ( TextResponseFormat  ` )

Text output format.

`audio` ` object ( AudioResponseFormat  ` )

Audio output format.

`image` ` object ( ImageResponseFormat  ` )

Image output format.

`video` ` object ( VideoResponseFormat  ` )

Video output format.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{// format&quot;text&quot;: {object (TextResponseFormat)},&quot;audio&quot;: {object (AudioResponseFormat)},&quot;image&quot;: {object (ImageResponseFormat)},&quot;video&quot;: {object (VideoResponseFormat)}// Union type}</code></pre></td>
</tr>
</tbody>
</table>

## TextResponseFormat

Configuration for text-specific output formatting.

Fields

`mimeType` ` enum ( MimeType  ` )

Optional. The IANA standard MIME type of the response.

`schema` ` value ( Value  ` format)

Optional. The JSON schema that the output should conform to. Only applicable when mimeType is APPLICATION\_JSON.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;mimeType&quot;: enum (MimeType),&quot;schema&quot;: value}</code></pre></td>
</tr>
</tbody>
</table>

## MimeType

Supported MIME types for text output.

Enums

`MIME_TYPE_UNSPECIFIED`

Default value. This value is unused.

`APPLICATION_JSON`

JSON output format.

`TEXT_PLAIN`

Plain text output format.

## AudioResponseFormat

Configuration for audio-specific output formatting.

Fields

`delivery` ` enum ( DeliveryMode  ` )

Optional. Delivery mode for the generated content.

`mimeType` ` enum ( MimeType  ` )

Optional. The MIME type of the audio output.

`sampleRate` `integer`

Optional. Sample rate for the generated audio in Hertz.

`bitRate` `integer`

Optional. Bit rate in bits per second (bps). Only applicable for compressed formats (MP3, Opus).

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;delivery&quot;: enum (DeliveryMode),&quot;mimeType&quot;: enum (MimeType),&quot;sampleRate&quot;: integer,&quot;bitRate&quot;: integer}</code></pre></td>
</tr>
</tbody>
</table>

## MimeType

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

## DeliveryMode

The delivery mode for the output content.

Enums

`DELIVERY_UNSPECIFIED`

Default value. This value is unused.

`INLINE`

Generated bytes are returned inline in the response.

`URI`

Generated content is stored and a URI is returned.

## ImageResponseFormat

Configuration for image-specific output formatting.

Fields

`delivery` ` enum ( DeliveryMode  ` )

Optional. Delivery mode for the generated content.

`mimeType` ` enum ( MimeType  ` )

Optional. The MIME type of the image output.

`aspectRatio` ` enum ( AspectRatio  ` )

Optional. The aspect ratio for the image output.

`imageSize` ` enum ( ImageSize  ` )

Optional. The size of the image output.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;delivery&quot;: enum (DeliveryMode),&quot;mimeType&quot;: enum (MimeType),&quot;aspectRatio&quot;: enum (AspectRatio),&quot;imageSize&quot;: enum (ImageSize)}</code></pre></td>
</tr>
</tbody>
</table>

## MimeType

Supported MIME types for image output.

Enums

`MIME_TYPE_UNSPECIFIED`

Default value. This value is unused.

`IMAGE_JPEG`

JPEG image format.

## AspectRatio

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

## ImageSize

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

## VideoResponseFormat

Configuration for video-specific output formatting.

Fields

`delivery` ` enum ( DeliveryMode  ` )

Optional. Delivery mode for the generated content.

`gcsUri` `string`

Optional. The Google Cloud Storage URI to store the video output. Required for Vertex if delivery is URI.

`aspectRatio` ` enum ( AspectRatio  ` )

The aspect ratio for the video output.

`duration` ` string ( Duration  ` format)

Optional. The duration for the video output.

A duration in seconds with up to nine fractional digits, ending with ' `s` '. Example: `"3.5s"` .

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;delivery&quot;: enum (DeliveryMode),&quot;gcsUri&quot;: string,&quot;aspectRatio&quot;: enum (AspectRatio),&quot;duration&quot;: string}</code></pre></td>
</tr>
</tbody>
</table>

## AspectRatio

Supported aspect ratios for video output.

Enums

`ASPECT_RATIO_UNSPECIFIED`

Default value. This value is unused.

`ASPECT_RATIO_SIXTEEN_BY_NINE`

16:9 aspect ratio.

`ASPECT_RATIO_NINE_BY_SIXTEEN`

9:16 aspect ratio.

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

## AggregationMetric

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

## OutputConfig

Config for evaluation output.

Fields

`destination` `Union type`

The destination for evaluation output. `destination` can be only one of the following:

`gcsDestination` ` object ( GcsDestination  ` )

Cloud storage destination for evaluation output.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{// destination&quot;gcsDestination&quot;: {object (GcsDestination)}// Union type}</code></pre></td>
</tr>
</tbody>
</table>

## TunedModel

The Model Registry Model and Online Prediction Endpoint associated with this `  TuningJob  ` .

Fields

`model` `string`

Output only. The resource name of the TunedModel. Format:

`projects/{project}/locations/{location}/models/{model}@{versionId}`

When tuning from a base model, the version id will be 1.

For continuous tuning, if the provided tunedModelDisplayName is set and different from parent model's display name, the tuned model will have a new parent model with version 1. Otherwise the version id will be incremented by 1 from the last version id in the parent model. E.g.,

`projects/{project}/locations/{location}/models/{model}@{last_version_id + 1}`

`endpoint` `string`

Output only. A resource name of an Endpoint. Format: `projects/{project}/locations/{location}/endpoints/{endpoint}` .

`checkpoints[]` ` object ( TunedModelCheckpoint  ` )

Output only. The checkpoints associated with this TunedModel. This field is only populated for tuning jobs that enable intermediate checkpoints.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;model&quot;: string,&quot;endpoint&quot;: string,&quot;checkpoints&quot;: [{object (TunedModelCheckpoint)}]}</code></pre></td>
</tr>
</tbody>
</table>

## TunedModelCheckpoint

TunedModelCheckpoint for the Tuned Model of a Tuning Job.

Fields

`checkpointId` `string`

The id of the checkpoint.

`epoch` `string ( int64 format)`

The epoch of the checkpoint.

`step` `string ( int64 format)`

The step of the checkpoint.

`endpoint` `string`

The Endpoint resource name that the checkpoint is deployed to. Format: `projects/{project}/locations/{location}/endpoints/{endpoint}` .

<table>
<colgroup>
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
  &quot;checkpointId&quot;: string,
  &quot;epoch&quot;: string,
  &quot;step&quot;: string,
  &quot;endpoint&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

## TuningDataStats

The tuning data statistic values for `  TuningJob  ` .

Fields

`tuning_data_stats` `Union type`

`tuning_data_stats` can be only one of the following:

`supervisedTuningDataStats` ` object ( SupervisedTuningDataStats  ` )

The SFT Tuning data stats.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{// tuning_data_stats&quot;supervisedTuningDataStats&quot;: {object (SupervisedTuningDataStats)}// Union type}</code></pre></td>
</tr>
</tbody>
</table>

## SupervisedTuningDataStats

Tuning data statistics for Supervised Tuning.

Fields

`tuningDatasetExampleCount` `string ( int64 format)`

Output only. Number of examples in the tuning dataset.

`totalTuningCharacterCount` `string ( int64 format)`

Output only. Number of tuning characters in the tuning dataset.

` totalBillableCharacterCount (deprecated)  ` `string ( int64 format)`

> This item is deprecated\!

Output only. Number of billable characters in the tuning dataset.

`totalBillableTokenCount` `string ( int64 format)`

Output only. Number of billable tokens in the tuning dataset.

`tuningStepCount` `string ( int64 format)`

Output only. Number of tuning steps for this Tuning Job.

`userInputTokenDistribution` ` object ( SupervisedTuningDatasetDistribution  ` )

Output only. Dataset distributions for the user input tokens.

`userOutputTokenDistribution` ` object ( SupervisedTuningDatasetDistribution  ` )

Output only. Dataset distributions for the user output tokens.

`userMessagePerExampleDistribution` ` object ( SupervisedTuningDatasetDistribution  ` )

Output only. Dataset distributions for the messages per example.

`userDatasetExamples[]` ` object ( Content  ` )

Output only. Sample user messages in the training dataset uri.

`totalTruncatedExampleCount` `string ( int64 format)`

Output only. The number of examples in the dataset that have been dropped. An example can be dropped for reasons including: too many tokens, contains an invalid image, contains too many images, etc.

`truncatedExampleIndices[]` `string ( int64 format)`

Output only. A partial sample of the indices (starting from 1) of the dropped examples.

`droppedExampleReasons[]` `string`

Output only. For each index in `truncatedExampleIndices` , the user-facing reason why the example was dropped.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;tuningDatasetExampleCount&quot;: string,&quot;totalTuningCharacterCount&quot;: string,&quot;totalBillableCharacterCount&quot;: string,&quot;totalBillableTokenCount&quot;: string,&quot;tuningStepCount&quot;: string,&quot;userInputTokenDistribution&quot;: {object (SupervisedTuningDatasetDistribution)},&quot;userOutputTokenDistribution&quot;: {object (SupervisedTuningDatasetDistribution)},&quot;userMessagePerExampleDistribution&quot;: {object (SupervisedTuningDatasetDistribution)},&quot;userDatasetExamples&quot;: [{object (Content)}],&quot;totalTruncatedExampleCount&quot;: string,&quot;truncatedExampleIndices&quot;: [string],&quot;droppedExampleReasons&quot;: [string]}</code></pre></td>
</tr>
</tbody>
</table>

## SupervisedTuningDatasetDistribution

Dataset distribution for Supervised Tuning.

Fields

`sum` `string ( int64 format)`

Output only. Sum of a given population of values.

`billableSum` `string ( int64 format)`

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

`buckets[]` ` object ( DatasetBucket  ` )

Output only. Defines the histogram bucket.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;sum&quot;: string,&quot;billableSum&quot;: string,&quot;min&quot;: number,&quot;max&quot;: number,&quot;mean&quot;: number,&quot;median&quot;: number,&quot;p5&quot;: number,&quot;p95&quot;: number,&quot;buckets&quot;: [{object (DatasetBucket)}]}</code></pre></td>
</tr>
</tbody>
</table>

## DatasetBucket

Dataset bucket used to create a histogram for the distribution given a population of values.

Fields

`count` `number`

Output only. Number of values in the bucket.

`left` `number`

Output only. left bound of the bucket.

`right` `number`

Output only. Right bound of the bucket.

<table>
<colgroup>
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
  &quot;count&quot;: number,
  &quot;left&quot;: number,
  &quot;right&quot;: number
}</code></pre></td>
</tr>
</tbody>
</table>

## EvaluateDatasetRun

Evaluate Dataset Run result for Tuning Job.

Fields

` operationName (deprecated)  ` `string`

> This item is deprecated\!

Output only. Deprecated: The updated architecture uses evaluationRun instead.

`evaluationRun` `string`

Output only. The resource name of the evaluation run. Format: `projects/{project}/locations/{location}/evaluationRuns/{evaluation_run_id}` .

`checkpointId` `string`

Output only. The checkpoint id used in the evaluation run. Only populated when evaluating checkpoints.

`evaluateDatasetResponse` ` object ( EvaluateDatasetResponse  ` )

Output only. Results for EvaluationService.

`error` ` object ( Status  ` )

Output only. The error of the evaluation run if any.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;operationName&quot;: string,&quot;evaluationRun&quot;: string,&quot;checkpointId&quot;: string,&quot;evaluateDatasetResponse&quot;: {object (EvaluateDatasetResponse)},&quot;error&quot;: {object (Status)}}</code></pre></td>
</tr>
</tbody>
</table>

## EvaluateDatasetResponse

The results from an evaluation run performed by the EvaluationService.

Fields

`aggregationOutput` ` object ( AggregationOutput  ` )

Output only. Aggregation statistics derived from results of EvaluationService.

`outputInfo` ` object ( OutputInfo  ` )

Output only. Output info for EvaluationService.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;aggregationOutput&quot;: {object (AggregationOutput)},&quot;outputInfo&quot;: {object (OutputInfo)}}</code></pre></td>
</tr>
</tbody>
</table>

## AggregationOutput

The aggregation result for the entire dataset and all metrics.

Fields

`dataset` ` object ( EvaluationDataset  ` )

The dataset used for evaluation & aggregation.

`aggregationResults[]` ` object ( AggregationResult  ` )

One AggregationResult per metric.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;dataset&quot;: {object (EvaluationDataset)},&quot;aggregationResults&quot;: [{object (AggregationResult)}]}</code></pre></td>
</tr>
</tbody>
</table>

## EvaluationDataset

The dataset used for evaluation.

Fields

`source` `Union type`

The source of the dataset. `source` can be only one of the following:

`gcsSource` ` object ( GcsSource  ` )

Cloud storage source holds the dataset. Currently only one Cloud Storage file path is supported.

`bigquerySource` ` object ( BigQuerySource  ` )

BigQuery source holds the dataset.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{// source&quot;gcsSource&quot;: {object (GcsSource)},&quot;bigquerySource&quot;: {object (BigQuerySource)}// Union type}</code></pre></td>
</tr>
</tbody>
</table>

## AggregationResult

The aggregation result for a single metric.

Fields

`aggregation_result` `Union type`

The aggregation result. `aggregation_result` can be only one of the following:

`pointwiseMetricResult` ` object ( PointwiseMetricResult  ` )

result for pointwise metric.

`pairwiseMetricResult` ` object ( PairwiseMetricResult  ` )

result for pairwise metric.

`exactMatchMetricValue` ` object ( ExactMatchMetricValue  ` )

Results for exact match metric.

`bleuMetricValue` ` object ( BleuMetricValue  ` )

Results for bleu metric.

`rougeMetricValue` ` object ( RougeMetricValue  ` )

Results for rouge metric.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{// aggregation_result&quot;pointwiseMetricResult&quot;: {object (PointwiseMetricResult)},&quot;pairwiseMetricResult&quot;: {object (PairwiseMetricResult)},&quot;exactMatchMetricValue&quot;: {object (ExactMatchMetricValue)},&quot;bleuMetricValue&quot;: {object (BleuMetricValue)},&quot;rougeMetricValue&quot;: {object (RougeMetricValue)}// Union type}</code></pre></td>
</tr>
</tbody>
</table>

## PointwiseMetricResult

Spec for pointwise metric result.

Fields

`explanation` `string`

Output only. Explanation for pointwise metric score.

`customOutput` ` object ( CustomOutput  ` )

Output only. Spec for custom output.

`score` `number`

Output only. Pointwise metric score.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;explanation&quot;: string,&quot;customOutput&quot;: {object (CustomOutput)},&quot;score&quot;: number}</code></pre></td>
</tr>
</tbody>
</table>

## CustomOutput

Spec for custom output.

Fields

`custom_output` `Union type`

Custom output. `custom_output` can be only one of the following:

`rawOutputs` ` object ( RawOutput  ` )

Output only. List of raw output strings.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{// custom_output&quot;rawOutputs&quot;: {object (RawOutput)}// Union type}</code></pre></td>
</tr>
</tbody>
</table>

## RawOutput

Raw output.

Fields

`rawOutput[]` `string`

Output only. Raw output string.

<table>
<colgroup>
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

## PairwiseMetricResult

Spec for pairwise metric result.

Fields

`pairwiseChoice` ` enum ( PairwiseChoice  ` )

Output only. Pairwise metric choice.

`explanation` `string`

Output only. Explanation for pairwise metric score.

`customOutput` ` object ( CustomOutput  ` )

Output only. Spec for custom output.

<table>
<colgroup>
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

## PairwiseChoice

Pairwise prediction autorater preference.

Enums

`PAIRWISE_CHOICE_UNSPECIFIED`

Unspecified prediction choice.

`BASELINE`

baseline prediction wins

`CANDIDATE`

Candidate prediction wins

`TIE`

Winner cannot be determined

## ExactMatchMetricValue

Exact match metric value for an instance.

Fields

`score` `number`

Output only. Exact match score.

<table>
<colgroup>
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

## BleuMetricValue

Bleu metric value for an instance.

Fields

`score` `number`

Output only. Bleu score.

<table>
<colgroup>
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

## RougeMetricValue

Rouge metric value for an instance.

Fields

`score` `number`

Output only. Rouge score.

<table>
<colgroup>
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

## OutputInfo

Describes the info for output of EvaluationService.

Fields

`output_location` `Union type`

The output location into which evaluation output is written. `output_location` can be only one of the following:

`gcsOutputDirectory` `string`

Output only. The full path of the Cloud Storage directory created, into which the evaluation results and aggregation results are written.

<table>
<colgroup>
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

  // output_location
  &quot;gcsOutputDirectory&quot;: string
  // Union type
}</code></pre></td>
</tr>
</tbody>
</table>

## Methods

### `            cancel           `

Cancels a tuning job.

### `            create           `

Creates a tuning job.

### `            get           `

Gets a tuning job.

### `            list           `

Lists tuning jobs in a location.

### `            rebaseTunedModel           `

Rebase a tuned model.
