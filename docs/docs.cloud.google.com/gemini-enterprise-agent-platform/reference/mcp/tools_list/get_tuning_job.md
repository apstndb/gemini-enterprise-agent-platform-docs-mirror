---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/get_tuning_job
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/get_tuning_job
title: 'MCP Tools Reference: aiplatform.googleapis.com'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

## Tool: `get_tuning_job`

Retrieves the full metadata and current status for a specific GenAI tuning job. This includes details about the base model being tuned, the tuning dataset, hyperparameters, and the resulting tuned model if the job has completed successfully. Use this to check if a model has finished fine-tuning and is ready for deployment. Format: 'projects/{project\_id}/locations/{region}'. CRITICAL: For {region}, use the region specified in the current context window. If no region is specified, prompt the user to provide one. Do not use 'global'. IMPORTANT: This parameter requires the 19-digit numeric ID returned by the list tool. If a shorter ID is provided, clarify the resource type or request the full ID before attempting discovery across other service types.

The following sample demonstrate how to use `curl` to invoke the `get_tuning_job` MCP tool.

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
    &quot;name&quot;: &quot;get_tuning_job&quot;,
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

Request message for `GenAiTuningService.GetTuningJob` .

### GetTuningJobRequest

<table>
<colgroup>
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
  &quot;name&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`name`

`string`

Required. The name of the tuning job to retrieve. Format: `projects/{project}/locations/{location}/tuningJobs/{tuning_job}`

## Output Schema

Represents a TuningJob that runs with Google owned models.

### TuningJob

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;name&quot;: string,&quot;tunedModelDisplayName&quot;: string,&quot;description&quot;: string,&quot;state&quot;: enum (JobState),&quot;createTime&quot;: string,&quot;startTime&quot;: string,&quot;endTime&quot;: string,&quot;updateTime&quot;: string,&quot;error&quot;: {object (Status)},&quot;labels&quot;: {string: string,...},&quot;experiment&quot;: string,&quot;tunedModel&quot;: {object (TunedModel)},&quot;tuningDataStats&quot;: {object (TuningDataStats)},&quot;encryptionSpec&quot;: {object (EncryptionSpec)},&quot;serviceAccount&quot;: string,&quot;evaluateDatasetRuns&quot;: [{object (EvaluateDatasetRun)}],// Union field source_model can be only one of the following:&quot;baseModel&quot;: string,&quot;preTunedModel&quot;: {object (PreTunedModel)}// End of list of possible types for union field source_model.// Union field tuning_spec can be only one of the following:&quot;supervisedTuningSpec&quot;: {object (SupervisedTuningSpec)}// End of list of possible types for union field tuning_spec.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`name`

`string`

Output only. Identifier. Resource name of a TuningJob. Format: `projects/{project}/locations/{location}/tuningJobs/{tuning_job}`

`tunedModelDisplayName`

`string`

Optional. The display name of the `  TunedModel  ` . The name can be up to 128 characters long and can consist of any UTF-8 characters. For continuous tuning, tuned\_model\_display\_name will by default use the same display name as the pre-tuned model. If a new display name is provided, the tuning job will create a new model instead of a new version.

`description`

`string`

Optional. The description of the `  TuningJob  ` .

`state`

` enum ( JobState  ` )

Output only. The detailed state of the job.

`createTime`

` string ( Timestamp  ` format)

Output only. Time when the `  TuningJob  ` was created.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`startTime`

` string ( Timestamp  ` format)

Output only. Time when the `  TuningJob  ` for the first time entered the `JOB_STATE_RUNNING` state.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`endTime`

` string ( Timestamp  ` format)

Output only. Time when the TuningJob entered any of the following `  JobStates  ` : `JOB_STATE_SUCCEEDED` , `JOB_STATE_FAILED` , `JOB_STATE_CANCELLED` , `JOB_STATE_EXPIRED` .

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`updateTime`

` string ( Timestamp  ` format)

Output only. Time when the `  TuningJob  ` was most recently updated.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`error`

` object ( Status  ` )

Output only. Only populated when job's state is `JOB_STATE_FAILED` or `JOB_STATE_CANCELLED` .

`labels`

`map (key: string, value: string)`

Optional. The labels with user-defined metadata to organize `  TuningJob  ` and generated resources such as `  Model  ` and `Endpoint` .

Label keys and values can be no longer than 64 characters (Unicode codepoints), can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed.

See <https://goo.gl/xmQnxf> for more information and examples of labels.

An object containing a list of `"key": value` pairs. Example: `{ "name": "wrench", "mass": "1.3kg", "count": "3" }` .

`experiment`

`string`

Output only. The Experiment associated with this `  TuningJob  ` .

`tunedModel`

` object ( TunedModel  ` )

Output only. The tuned model resources associated with this `  TuningJob  ` .

`tuningDataStats`

` object ( TuningDataStats  ` )

Output only. The tuning data statistics associated with this `  TuningJob  ` .

`encryptionSpec`

` object ( EncryptionSpec  ` )

Customer-managed encryption key options for a TuningJob. If this is set, then all resources created by the TuningJob will be encrypted with the provided encryption key.

`serviceAccount`

`string`

The service account that the tuningJob workload runs as. If not specified, the Agent Platform Secure Fine-Tuned Service Agent in the project will be used. See <https://cloud.google.com/iam/docs/service-agents#vertex-ai-secure-fine-tuning-service-agent>

Users starting the pipeline must have the `iam.serviceAccounts.actAs` permission on this service account.

`evaluateDatasetRuns[]`

` object ( EvaluateDatasetRun  ` )

Output only. Evaluation runs for the Tuning Job.

Union field `source_model` .

`source_model` can be only one of the following:

`baseModel`

`string`

The base model that is being tuned. See [Supported models](https://cloud.google.com/vertex-ai/generative-ai/docs/model-reference/tuning#supported_models) .

`preTunedModel`

` object ( PreTunedModel  ` )

The pre-tuned model for continuous tuning.

Union field `tuning_spec` .

`tuning_spec` can be only one of the following:

`supervisedTuningSpec`

` object ( SupervisedTuningSpec  ` )

Tuning Spec for Supervised Fine Tuning.

### PreTunedModel

<table>
<colgroup>
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

Fields

`tunedModelName`

`string`

The resource name of the Model. E.g., a model resource name with a specified version id or alias:

`projects/{project}/locations/{location}/models/{model}@{version_id}`

`projects/{project}/locations/{location}/models/{model}@{alias}`

Or, omit the version id to use the default version:

`projects/{project}/locations/{location}/models/{model}`

`checkpointId`

`string`

Optional. The source checkpoint id. If not specified, the default checkpoint will be used.

`baseModel`

`string`

Output only. The name of the base model this `  PreTunedModel  ` was tuned from.

### SupervisedTuningSpec

<table>
<colgroup>
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

Fields

`trainingDatasetUri`

`string`

Required. Training dataset used for tuning. The dataset can be specified as either a Cloud Storage path to a JSONL file or as the resource name of a Vertex Multimodal Dataset.

`validationDatasetUri`

`string`

Optional. Validation dataset used for tuning. The dataset can be specified as either a Cloud Storage path to a JSONL file or as the resource name of a Vertex Multimodal Dataset.

`hyperParameters`

` object ( SupervisedHyperParameters  ` )

Optional. Hyperparameters for SFT.

`exportLastCheckpointOnly`

`boolean`

Optional. If set to true, disable intermediate checkpoints for SFT and only the last checkpoint will be exported. Otherwise, enable intermediate checkpoints for SFT. Default is false.

`evaluationConfig`

` object ( EvaluationConfig  ` )

Optional. Evaluation Config for Tuning Job.

### SupervisedHyperParameters

<table>
<colgroup>
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

Fields

`epochCount`

`string ( int64 format)`

Optional. Number of complete passes the model makes over the entire training dataset during training.

`learningRateMultiplier`

`number`

Optional. Multiplier for adjusting the default learning rate. Mutually exclusive with `learning_rate` . This feature is only available for 1P models.

`adapterSize`

` enum ( AdapterSize  ` )

Optional. Adapter size for tuning.

### EvaluationConfig

<table>
<colgroup>
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

Fields

`metrics[]`

` object ( Metric  ` )

Required. The metrics used for evaluation.

`outputConfig`

` object ( OutputConfig  ` )

Required. Config for evaluation output.

`autoraterConfig`

` object ( AutoraterConfig  ` )

Optional. Autorater config for evaluation.

`inferenceGenerationConfig`

` object ( GenerationConfig  ` )

Optional. Configuration options for inference generation and outputs. If not set, default generation parameters are used.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;aggregationMetrics&quot;: [enum (AggregationMetric)],// Union field metric_spec can be only one of the following:&quot;predefinedMetricSpec&quot;: {object (PredefinedMetricSpec)},&quot;computationBasedMetricSpec&quot;: {object (ComputationBasedMetricSpec)},&quot;llmBasedMetricSpec&quot;: {object (LLMBasedMetricSpec)},&quot;pointwiseMetricSpec&quot;: {object (PointwiseMetricSpec)},&quot;pairwiseMetricSpec&quot;: {object (PairwiseMetricSpec)},&quot;exactMatchSpec&quot;: {object (ExactMatchSpec)},&quot;bleuSpec&quot;: {object (BleuSpec)},&quot;rougeSpec&quot;: {object (RougeSpec)}// End of list of possible types for union field metric_spec.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`aggregationMetrics[]`

` enum ( AggregationMetric  ` )

Optional. The aggregation metrics to use.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;resultParserConfig&quot;: {object (EvaluationParserConfig)},// Union field rubrics_source can be only one of the following:&quot;rubricGroupKey&quot;: string,&quot;predefinedRubricGenerationSpec&quot;: {object (PredefinedMetricSpec)}// End of list of possible types for union field rubrics_source.// Union field _metric_prompt_template can be only one of the following:&quot;metricPromptTemplate&quot;: string// End of list of possible types for union field _metric_prompt_template.// Union field _system_instruction can be only one of the following:&quot;systemInstruction&quot;: string// End of list of possible types for union field _system_instruction.// Union field _judge_autorater_config can be only one of the following:&quot;judgeAutoraterConfig&quot;: {object (AutoraterConfig)}// End of list of possible types for union field _judge_autorater_config.// Union field _additional_config can be only one of the following:&quot;additionalConfig&quot;: {object}// End of list of possible types for union field _additional_config.}</code></pre></td>
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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;stopSequences&quot;: [string],&quot;responseMimeType&quot;: string,&quot;responseModalities&quot;: [enum (Modality)],&quot;thinkingConfig&quot;: {object (ThinkingConfig)},&quot;responseFormat&quot;: [{object (ResponseFormat)}],// Union field _temperature can be only one of the following:&quot;temperature&quot;: number// End of list of possible types for union field _temperature.// Union field _top_p can be only one of the following:&quot;topP&quot;: number// End of list of possible types for union field _top_p.// Union field _top_k can be only one of the following:&quot;topK&quot;: number// End of list of possible types for union field _top_k.// Union field _candidate_count can be only one of the following:&quot;candidateCount&quot;: integer// End of list of possible types for union field _candidate_count.// Union field _max_output_tokens can be only one of the following:&quot;maxOutputTokens&quot;: integer// End of list of possible types for union field _max_output_tokens.// Union field _response_logprobs can be only one of the following:&quot;responseLogprobs&quot;: boolean// End of list of possible types for union field _response_logprobs.// Union field _logprobs can be only one of the following:&quot;logprobs&quot;: integer// End of list of possible types for union field _logprobs.// Union field _presence_penalty can be only one of the following:&quot;presencePenalty&quot;: number// End of list of possible types for union field _presence_penalty.// Union field _frequency_penalty can be only one of the following:&quot;frequencyPenalty&quot;: number// End of list of possible types for union field _frequency_penalty.// Union field _seed can be only one of the following:&quot;seed&quot;: integer// End of list of possible types for union field _seed.// Union field _response_schema can be only one of the following:&quot;responseSchema&quot;: {object (Schema)}// End of list of possible types for union field _response_schema.// Union field _response_json_schema can be only one of the following:&quot;responseJsonSchema&quot;: value// End of list of possible types for union field _response_json_schema.// Union field _routing_config can be only one of the following:&quot;routingConfig&quot;: {object (RoutingConfig)}// End of list of possible types for union field _routing_config.// Union field _audio_timestamp can be only one of the following:&quot;audioTimestamp&quot;: boolean// End of list of possible types for union field _audio_timestamp.// Union field _media_resolution can be only one of the following:&quot;mediaResolution&quot;: enum (MediaResolution)// End of list of possible types for union field _media_resolution.// Union field _speech_config can be only one of the following:&quot;speechConfig&quot;: {object (SpeechConfig)}// End of list of possible types for union field _speech_config.// Union field _enable_affective_dialog can be only one of the following:&quot;enableAffectiveDialog&quot;: boolean// End of list of possible types for union field _enable_affective_dialog.// Union field _image_config can be only one of the following:&quot;imageConfig&quot;: {object (ImageConfig)}// End of list of possible types for union field _image_config.// Union field _audio_transcription_config can be only one of the following:&quot;audioTranscriptionConfig&quot;: {object (AudioTranscriptionConfig)}// End of list of possible types for union field _audio_transcription_config.}</code></pre></td>
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

### OutputConfig

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{// Union field destination can be only one of the following:&quot;gcsDestination&quot;: {object (GcsDestination)}// End of list of possible types for union field destination.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

Union field `destination` . The destination for evaluation output. `destination` can be only one of the following:

`gcsDestination`

` object ( GcsDestination  ` )

Cloud storage destination for evaluation output.

### GcsDestination

<table>
<colgroup>
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
  &quot;outputUriPrefix&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`outputUriPrefix`

`string`

Required. Google Cloud Storage URI to output directory. If the uri doesn't end with '/', a '/' will be automatically appended. The directory is created if it doesn't exist.

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

### LabelsEntry

<table>
<colgroup>
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
  &quot;value&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`key`

`string`

`value`

`string`

### TunedModel

<table>
<colgroup>
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

Fields

`model`

`string`

Output only. The resource name of the TunedModel. Format:

`projects/{project}/locations/{location}/models/{model}@{version_id}`

When tuning from a base model, the version ID will be 1.

For continuous tuning, if the provided tuned\_model\_display\_name is set and different from parent model's display name, the tuned model will have a new parent model with version 1. Otherwise the version id will be incremented by 1 from the last version ID in the parent model. E.g.,

`projects/{project}/locations/{location}/models/{model}@{last_version_id + 1}`

`endpoint`

`string`

Output only. A resource name of an Endpoint. Format: `projects/{project}/locations/{location}/endpoints/{endpoint}` .

`checkpoints[]`

` object ( TunedModelCheckpoint  ` )

Output only. The checkpoints associated with this TunedModel. This field is only populated for tuning jobs that enable intermediate checkpoints.

### TunedModelCheckpoint

<table>
<colgroup>
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

Fields

`checkpointId`

`string`

The ID of the checkpoint.

`epoch`

`string ( int64 format)`

The epoch of the checkpoint.

`step`

`string ( int64 format)`

The step of the checkpoint.

`endpoint`

`string`

The Endpoint resource name that the checkpoint is deployed to. Format: `projects/{project}/locations/{location}/endpoints/{endpoint}` .

### TuningDataStats

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{// Union field tuning_data_stats can be only one of the following:&quot;supervisedTuningDataStats&quot;: {object (SupervisedTuningDataStats)}// End of list of possible types for union field tuning_data_stats.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

Union field `tuning_data_stats` .

`tuning_data_stats` can be only one of the following:

`supervisedTuningDataStats`

` object ( SupervisedTuningDataStats  ` )

The SFT Tuning data stats.

### SupervisedTuningDataStats

<table>
<colgroup>
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

Fields

`tuningDatasetExampleCount`

`string ( int64 format)`

Output only. Number of examples in the tuning dataset.

`totalTuningCharacterCount`

`string ( int64 format)`

Output only. Number of tuning characters in the tuning dataset.

` totalBillableCharacterCount (deprecated)  `

`string ( int64 format)`

> This item is deprecated\!

Output only. Number of billable characters in the tuning dataset.

`totalBillableTokenCount`

`string ( int64 format)`

Output only. Number of billable tokens in the tuning dataset.

`tuningStepCount`

`string ( int64 format)`

Output only. Number of tuning steps for this Tuning Job.

`userInputTokenDistribution`

` object ( SupervisedTuningDatasetDistribution  ` )

Output only. Dataset distributions for the user input tokens.

`userOutputTokenDistribution`

` object ( SupervisedTuningDatasetDistribution  ` )

Output only. Dataset distributions for the user output tokens.

`userMessagePerExampleDistribution`

` object ( SupervisedTuningDatasetDistribution  ` )

Output only. Dataset distributions for the messages per example.

`userDatasetExamples[]`

` object ( Content  ` )

Output only. Sample user messages in the training dataset uri.

`totalTruncatedExampleCount`

`string ( int64 format)`

Output only. The number of examples in the dataset that have been dropped. An example can be dropped for reasons including: too many tokens, contains an invalid image, contains too many images, etc.

`truncatedExampleIndices[]`

`string ( int64 format)`

Output only. A partial sample of the indices (starting from 1) of the dropped examples.

`droppedExampleReasons[]`

`string`

Output only. For each index in `truncated_example_indices` , the user-facing reason why the example was dropped.

### SupervisedTuningDatasetDistribution

<table>
<colgroup>
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

Fields

`sum`

`string ( int64 format)`

Output only. Sum of a given population of values.

`billableSum`

`string ( int64 format)`

Output only. Sum of a given population of values that are billable.

`min`

`number`

Output only. The minimum of the population values.

`max`

`number`

Output only. The maximum of the population values.

`mean`

`number`

Output only. The arithmetic mean of the values in the population.

`median`

`number`

Output only. The median of the values in the population.

`p5`

`number`

Output only. The 5th percentile of the values in the population.

`p95`

`number`

Output only. The 95th percentile of the values in the population.

`buckets[]`

` object ( DatasetBucket  ` )

Output only. Defines the histogram bucket.

### DatasetBucket

<table>
<colgroup>
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

Fields

`count`

`number`

Output only. Number of values in the bucket.

`left`

`number`

Output only. Left bound of the bucket.

`right`

`number`

Output only. Right bound of the bucket.

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

### EncryptionSpec

<table>
<colgroup>
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
  &quot;kmsKeyName&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`kmsKeyName`

`string`

Required. Resource name of the Cloud KMS key used to protect the resource.

The Cloud KMS key must be in the same region as the resource. It must have the format `projects/{project}/locations/{location}/keyRings/{key_ring}/cryptoKeys/{crypto_key}` .

### EvaluateDatasetRun

<table>
<colgroup>
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

Fields

` operationName (deprecated)  `

`string`

> This item is deprecated\!

Output only. Deprecated: The updated architecture uses evaluation\_run instead.

`evaluationRun`

`string`

Output only. The resource name of the evaluation run. Format: `projects/{project}/locations/{location}/evaluationRuns/{evaluation_run_id}` .

`checkpointId`

`string`

Output only. The checkpoint id used in the evaluation run. Only populated when evaluating checkpoints.

`evaluateDatasetResponse`

` object ( EvaluateDatasetResponse  ` )

Output only. Results for EvaluationService.

`error`

` object ( Status  ` )

Output only. The error of the evaluation run if any.

### EvaluateDatasetResponse

<table>
<colgroup>
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

Fields

`aggregationOutput`

` object ( AggregationOutput  ` )

Output only. Aggregation statistics derived from results of EvaluationService.

`outputInfo`

` object ( OutputInfo  ` )

Output only. Output info for EvaluationService.

### AggregationOutput

<table>
<colgroup>
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

Fields

`dataset`

` object ( EvaluationDataset  ` )

The dataset used for evaluation & aggregation.

`aggregationResults[]`

` object ( AggregationResult  ` )

One AggregationResult per metric.

### EvaluationDataset

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{// Union field source can be only one of the following:&quot;gcsSource&quot;: {object (GcsSource)},&quot;bigquerySource&quot;: {object (BigQuerySource)}// End of list of possible types for union field source.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

Union field `source` . The source of the dataset. `source` can be only one of the following:

`gcsSource`

` object ( GcsSource  ` )

Cloud storage source holds the dataset. Currently only one Cloud Storage file path is supported.

`bigquerySource`

` object ( BigQuerySource  ` )

BigQuery source holds the dataset.

### GcsSource

<table>
<colgroup>
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
  &quot;uris&quot;: [
    string
  ]
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`uris[]`

`string`

Required. Google Cloud Storage URI(-s) to the input file(s). May contain wildcards. For more information on wildcards, see <https://cloud.google.com/storage/docs/wildcards> .

### BigQuerySource

<table>
<colgroup>
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
  &quot;inputUri&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`inputUri`

`string`

Required. BigQuery URI to a table, up to 2000 characters long. Accepted forms:

  - BigQuery path. For example: `bq://projectId.bqDatasetId.bqTableId` .

### AggregationResult

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{// Union field aggregation_result can be only one of the following:&quot;pointwiseMetricResult&quot;: {object (PointwiseMetricResult)},&quot;pairwiseMetricResult&quot;: {object (PairwiseMetricResult)},&quot;exactMatchMetricValue&quot;: {object (ExactMatchMetricValue)},&quot;bleuMetricValue&quot;: {object (BleuMetricValue)},&quot;rougeMetricValue&quot;: {object (RougeMetricValue)}// End of list of possible types for union field aggregation_result.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

Union field `aggregation_result` . The aggregation result. `aggregation_result` can be only one of the following:

`pointwiseMetricResult`

` object ( PointwiseMetricResult  ` )

Result for pointwise metric.

`pairwiseMetricResult`

` object ( PairwiseMetricResult  ` )

Result for pairwise metric.

`exactMatchMetricValue`

` object ( ExactMatchMetricValue  ` )

Results for exact match metric.

`bleuMetricValue`

` object ( BleuMetricValue  ` )

Results for bleu metric.

`rougeMetricValue`

` object ( RougeMetricValue  ` )

Results for rouge metric.

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

### OutputInfo

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{// Union field output_location can be only one of the following:&quot;gcsOutputDirectory&quot;: string// End of list of possible types for union field output_location.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

Union field `output_location` . The output location into which evaluation output is written. `output_location` can be only one of the following:

`gcsOutputDirectory`

`string`

Output only. The full path of the Cloud Storage directory created, into which the evaluation results and aggregation results are written.

### AdapterSize

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

### NullValue

Represents a JSON `null` .

`NullValue` is a sentinel, using an enum with only one value to represent the null value for the `Value` type union.

A field of type `NullValue` with any value other than `0` is considered invalid. Most ProtoJSON serializers will emit a `Value` with a `null_value` set as a JSON `null` regardless of the integer value, and so will round trip to a `0` value.

Enums

`NULL_VALUE`

Null value.

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

### JobState

Describes the state of a job.

Enums

`JOB_STATE_UNSPECIFIED`

The job state is unspecified.

`JOB_STATE_QUEUED`

The job has been just created or resumed and processing has not yet begun.

`JOB_STATE_PENDING`

The service is preparing to run the job.

`JOB_STATE_RUNNING`

The job is in progress.

`JOB_STATE_SUCCEEDED`

The job completed successfully.

`JOB_STATE_FAILED`

The job failed.

`JOB_STATE_CANCELLING`

The job is being cancelled. From this state the job may only go to either `JOB_STATE_SUCCEEDED` , `JOB_STATE_FAILED` or `JOB_STATE_CANCELLED` .

`JOB_STATE_CANCELLED`

The job has been cancelled.

`JOB_STATE_PAUSED`

The job has been stopped, and can be resumed.

`JOB_STATE_EXPIRED`

The job has expired.

`JOB_STATE_UPDATING`

The job is being updated. Only jobs in the `RUNNING` state can be updated. After updating, the job goes back to the `RUNNING` state.

`JOB_STATE_PARTIALLY_SUCCEEDED`

The job is partially succeeded, some results may be missing due to errors.

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

### Tool Annotations

Destructive Hint: ❌ | Idempotent Hint: ✅ | Read Only Hint: ✅ | Open World Hint: ❌
