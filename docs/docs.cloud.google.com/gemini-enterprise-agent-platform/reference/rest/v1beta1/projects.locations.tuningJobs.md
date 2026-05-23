---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.tuningJobs
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.tuningJobs
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

`customBaseModel` `string`

Optional. The user-provided path to custom model weights. Set this field to tune a custom model. The path must be a Cloud Storage directory that contains the model weights in .safetensors format along with associated model metadata files. If this field is set, the baseModel field must still be set to indicate which base model the custom model is derived from. This feature is only available for open source models.

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

` pipelineJob (deprecated)  ` `string`

> This item is deprecated\!

Output only. The resource name of the PipelineJob associated with the `  TuningJob  ` . Format: `projects/{project}/locations/{location}/pipelineJobs/{pipelineJob}` .

`encryptionSpec` ` object ( EncryptionSpec  ` )

Customer-managed encryption key options for a TuningJob. If this is set, then all resources created by the TuningJob will be encrypted with the provided encryption key.

`serviceAccount` `string`

The service account that the tuningJob workload runs as. If not specified, the Agent Platform Secure Fine-Tuned service Agent in the project will be used. See <https://cloud.google.com/iam/docs/service-agents#vertex-ai-secure-fine-tuning-service-agent>

Users starting the pipeline must have the `iam.serviceAccounts.actAs` permission on this service account.

`outputUri` `string`

Optional. Cloud Storage path to the directory where tuning job outputs are written to. This field is only available and required for open source models.

`evaluateDatasetRuns[]` ` object ( EvaluateDatasetRun  ` )

Output only. Evaluation runs for the Tuning Job.

`satisfiesPzs` `boolean`

Output only. reserved for future use.

`satisfiesPzi` `boolean`

Output only. reserved for future use.

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

`distillationSpec` ` object ( DistillationSpec  ` )

Tuning Spec for Distillation.

`partnerModelTuningSpec` ` object ( PartnerModelTuningSpec  ` )

Tuning Spec for open sourced and third party Partner models.

`veoTuningSpec` ` object ( VeoTuningSpec  ` )

Tuning Spec for Veo Tuning.

`veoLoraTuningSpec` ` object ( VeoLoraTuningSpec  ` )

Tuning Spec for Veo LoRA Tuning.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;name&quot;: string,&quot;tunedModelDisplayName&quot;: string,&quot;description&quot;: string,&quot;customBaseModel&quot;: string,&quot;state&quot;: enum (JobState),&quot;createTime&quot;: string,&quot;startTime&quot;: string,&quot;endTime&quot;: string,&quot;updateTime&quot;: string,&quot;error&quot;: {object (Status)},&quot;labels&quot;: {string: string,...},&quot;experiment&quot;: string,&quot;tunedModel&quot;: {object (TunedModel)},&quot;tuningDataStats&quot;: {object (TuningDataStats)},&quot;pipelineJob&quot;: string,&quot;encryptionSpec&quot;: {object (EncryptionSpec)},&quot;serviceAccount&quot;: string,&quot;outputUri&quot;: string,&quot;evaluateDatasetRuns&quot;: [{object (EvaluateDatasetRun)}],&quot;satisfiesPzs&quot;: boolean,&quot;satisfiesPzi&quot;: boolean,// source_model&quot;baseModel&quot;: string,&quot;preTunedModel&quot;: {object (PreTunedModel)}// Union type// tuning_spec&quot;supervisedTuningSpec&quot;: {object (SupervisedTuningSpec)},&quot;distillationSpec&quot;: {object (DistillationSpec)},&quot;partnerModelTuningSpec&quot;: {object (PartnerModelTuningSpec)},&quot;veoTuningSpec&quot;: {object (VeoTuningSpec)},&quot;veoLoraTuningSpec&quot;: {object (VeoLoraTuningSpec)}// Union type}</code></pre></td>
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

`tuningMode` ` enum ( TuningMode  ` )

Tuning mode.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;trainingDatasetUri&quot;: string,&quot;validationDatasetUri&quot;: string,&quot;hyperParameters&quot;: {object (SupervisedHyperParameters)},&quot;exportLastCheckpointOnly&quot;: boolean,&quot;evaluationConfig&quot;: {object (EvaluationConfig)},&quot;tuningMode&quot;: enum (TuningMode)}</code></pre></td>
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

`learningRate` `number`

Optional. Learning rate for tuning. Mutually exclusive with `learningRateMultiplier` . This feature is only available for open source models.

`adapterSize` ` enum ( AdapterSize  ` )

Optional. Adapter size for tuning.

`batchSize` `string ( int64 format)`

Optional. Batch size for tuning. This feature is only available for open source models.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;epochCount&quot;: string,&quot;learningRateMultiplier&quot;: number,&quot;learningRate&quot;: number,&quot;adapterSize&quot;: enum (AdapterSize),&quot;batchSize&quot;: string}</code></pre></td>
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

## OutputConfig

Config for evaluation output.

Fields

`destination` `Union type`

The destination for evaluation output. `destination` can be only one of the following:

`gcsDestination` `object ( GcsDestination` )

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

## TuningMode

Supported tuning modes.

Enums

`TUNING_MODE_UNSPECIFIED`

Tuning mode is unspecified.

`TUNING_MODE_FULL`

Full fine-tuning mode.

`TUNING_MODE_PEFT_ADAPTER`

PEFT adapter tuning mode.

## DistillationSpec

Tuning Spec for Distillation.

Fields

` trainingDatasetUri (deprecated)  ` `string`

> This item is deprecated\!

Deprecated. Cloud Storage path to file containing training dataset for tuning. The dataset must be formatted as a JSONL file.

`promptDatasetUri` `string`

Optional. Cloud Storage path to file containing prompt dataset for distillation. The dataset must be formatted as a JSONL file.

`hyperParameters` ` object ( DistillationHyperParameters  ` )

Optional. Hyperparameters for Distillation.

` studentModel (deprecated)  ` `string`

> This item is deprecated\!

The student model that is being tuned, e.g., "google/gemma-2b-1.1-it". Deprecated. Use baseModel instead.

` pipelineRootDirectory (deprecated)  ` `string`

> This item is deprecated\!

Deprecated. A path in a Cloud Storage bucket, which will be treated as the root output directory of the distillation pipeline. It is used by the system to generate the paths of output artifacts.

`tuningMode` ` enum ( TuningMode  ` )

Optional. Specifies the tuning mode for distillation (sft part). This feature is only available for open source models.

`teacher_model` `Union type`

The teacher model that is being distilled from. See [Supported models](https://cloud.google.com/vertex-ai/generative-ai/docs/model-reference/tuning#supported_models) . `teacher_model` can be only one of the following:

`baseTeacherModel` `string`

The base teacher model that is being distilled. See [Supported models](https://cloud.google.com/vertex-ai/generative-ai/docs/model-reference/tuning#supported_models) .

`tunedTeacherModelSource` `string`

The resource name of the Tuned teacher model. Format: `projects/{project}/locations/{location}/models/{model}` .

`validationDatasetUri` `string`

Optional. Cloud Storage path to file containing validation dataset for tuning. The dataset must be formatted as a JSONL file.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;trainingDatasetUri&quot;: string,&quot;promptDatasetUri&quot;: string,&quot;hyperParameters&quot;: {object (DistillationHyperParameters)},&quot;studentModel&quot;: string,&quot;pipelineRootDirectory&quot;: string,&quot;tuningMode&quot;: enum (TuningMode),// teacher_model&quot;baseTeacherModel&quot;: string,&quot;tunedTeacherModelSource&quot;: string// Union type&quot;validationDatasetUri&quot;: string}</code></pre></td>
</tr>
</tbody>
</table>

## DistillationHyperParameters

Hyperparameters for Distillation.

Fields

`adapterSize` ` enum ( AdapterSize  ` )

Optional. Adapter size for distillation.

`learningRate` `number`

Optional. Specifies the learning rate for tuning. Mutually exclusive with `learningRateMultiplier` . This feature is only available for open source models.

`batchSize` `string ( int64 format)`

Optional. Batch size for tuning. This feature is only available for open source models.

`epochCount` `string ( int64 format)`

Optional. Number of complete passes the model makes over the entire training dataset during training.

`learningRateMultiplier` `number`

Optional. Multiplier for adjusting the default learning rate.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;adapterSize&quot;: enum (AdapterSize),&quot;learningRate&quot;: number,&quot;batchSize&quot;: string,&quot;epochCount&quot;: string,&quot;learningRateMultiplier&quot;: number}</code></pre></td>
</tr>
</tbody>
</table>

## PartnerModelTuningSpec

Tuning spec for Partner models.

Fields

`trainingDatasetUri` `string`

Required. Cloud Storage path to file containing training dataset for tuning. The dataset must be formatted as a JSONL file.

`validationDatasetUri` `string`

Optional. Cloud Storage path to file containing validation dataset for tuning. The dataset must be formatted as a JSONL file.

`hyperParameters` ` map (key: string, value: value ( Value  ` format))

Hyperparameters for tuning. The accepted hyperParameters and their valid range of values will differ depending on the base model.

<table>
<colgroup>
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
  &quot;trainingDatasetUri&quot;: string,
  &quot;validationDatasetUri&quot;: string,
  &quot;hyperParameters&quot;: {
    string: value,
    ...
  }
}</code></pre></td>
</tr>
</tbody>
</table>

## VeoTuningSpec

Tuning Spec for Veo Model Tuning.

Fields

`trainingDatasetUri` `string`

Required. Training dataset used for tuning. The dataset can be specified as either a Cloud Storage path to a JSONL file or as the resource name of a Vertex Multimodal Dataset.

`validationDatasetUri` `string`

Optional. Validation dataset used for tuning. The dataset can be specified as either a Cloud Storage path to a JSONL file or as the resource name of a Vertex Multimodal Dataset.

`hyperParameters` ` object ( VeoHyperParameters  ` )

Optional. Hyperparameters for Veo.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;trainingDatasetUri&quot;: string,&quot;validationDatasetUri&quot;: string,&quot;hyperParameters&quot;: {object (VeoHyperParameters)}}</code></pre></td>
</tr>
</tbody>
</table>

## VeoHyperParameters

Hyperparameters for Veo.

Fields

`epochCount` `string ( int64 format)`

Optional. Number of complete passes the model makes over the entire training dataset during training.

`learningRateMultiplier` `number`

Optional. Multiplier for adjusting the default learning rate.

`tuningTask` ` enum ( TuningTask  ` )

The tuning task for Veo.

`adapterSize` ` enum ( AdapterSize  ` )

Optional. The adapter size for LoRA tuning.

`veoDataMixtureRatio` `number`

Optional. The ratio of Google internal dataset to use in the training mixture, in range of `[0, 1)` . If `0.2` , it means 20% of Google internal dataset and 80% of user dataset will be used for training. If not set, the default value is 0.1.

`tuningSpeed` ` enum ( TuningSpeed  ` )

The speed of the tuning job. Only supported for Veo 3.0 models.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;epochCount&quot;: string,&quot;learningRateMultiplier&quot;: number,&quot;tuningTask&quot;: enum (TuningTask),&quot;adapterSize&quot;: enum (AdapterSize),&quot;veoDataMixtureRatio&quot;: number,&quot;tuningSpeed&quot;: enum (TuningSpeed)}</code></pre></td>
</tr>
</tbody>
</table>

## TuningTask

An enum defining the tuning task used for Veo.

Enums

`TUNING_TASK_UNSPECIFIED`

Default value. This value is unused.

`TUNING_TASK_I2V`

Tuning task for image to video.

`TUNING_TASK_T2V`

Tuning task for text to video.

`TUNING_TASK_R2V`

Tuning task for reference to video.

## TuningSpeed

The speed of the tuning job. Only supported for Veo 3.0 models.

Enums

`TUNING_SPEED_UNSPECIFIED`

The default / unset value. For Veo 3.0 models, this defaults to FAST.

`REGULAR`

Regular tuning speed.

`FAST`

Fast tuning speed.

## AdapterSize

Adapter size for LoRA tuning.

Enums

`ADAPTER_SIZE_UNSPECIFIED`

Adapter size is unspecified.

`ADAPTER_SIZE_EIGHT`

Adapter size 8. This is the default adapter size for Veo LoRA tuning.

`ADAPTER_SIZE_SIXTEEN`

Adapter size 16.

`ADAPTER_SIZE_THIRTY_TWO`

Adapter size 32.

## VeoLoraTuningSpec

Tuning Spec for Veo LoRA Model Tuning.

Fields

`trainingDatasetUri` `string`

Required. Training dataset used for tuning. The dataset can be specified as either a Cloud Storage path to a JSONL file or as the resource name of a Vertex Multimodal Dataset.

`validationDatasetUri` `string`

Optional. Validation dataset used for tuning. The dataset can be specified as either a Cloud Storage path to a JSONL file or as the resource name of a Vertex Multimodal Dataset.

`hyperParameters` ` object ( VeoHyperParameters  ` )

Optional. Hyperparameters for Veo LoRA.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;trainingDatasetUri&quot;: string,&quot;validationDatasetUri&quot;: string,&quot;hyperParameters&quot;: {object (VeoHyperParameters)}}</code></pre></td>
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

`distillationDataStats` ` object ( DistillationDataStats  ` )

Output only. Statistics for distillation prompt dataset. These statistics do not include the responses sampled from the teacher model.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{// tuning_data_stats&quot;supervisedTuningDataStats&quot;: {object (SupervisedTuningDataStats)},&quot;distillationDataStats&quot;: {object (DistillationDataStats)}// Union type}</code></pre></td>
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

## DistillationDataStats

Statistics for distillation prompt dataset. These statistics do not include the responses sampled from the teacher model.

Fields

`trainingDatasetStats` ` object ( DatasetStats  ` )

Output only. Statistics computed for the training dataset.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;trainingDatasetStats&quot;: {object (DatasetStats)}}</code></pre></td>
</tr>
</tbody>
</table>

## DatasetStats

Statistics computed over a tuning dataset.

Fields

`tuningDatasetExampleCount` `string ( int64 format)`

Output only. Number of examples in the tuning dataset.

`totalTuningCharacterCount` `string ( int64 format)`

Output only. Number of tuning characters in the tuning dataset.

`totalBillableCharacterCount` `string ( int64 format)`

Output only. Number of billable characters in the tuning dataset.

`tuningStepCount` `string ( int64 format)`

Output only. Number of tuning steps for this Tuning Job.

`userInputTokenDistribution` ` object ( DatasetDistribution  ` )

Output only. Dataset distributions for the user input tokens.

`userMessagePerExampleDistribution` ` object ( DatasetDistribution  ` )

Output only. Dataset distributions for the messages per example.

`userDatasetExamples[]` ` object ( Content  ` )

Output only. Sample user messages in the training dataset uri.

`droppedExampleIndices[]` `string ( int64 format)`

Output only. A partial sample of the indices (starting from 1) of the dropped examples.

`droppedExampleReasons[]` `string`

Output only. For each index in `droppedExampleIndices` , the user-facing reason why the example was dropped.

`userOutputTokenDistribution` ` object ( DatasetDistribution  ` )

Output only. Dataset distributions for the user output tokens.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;tuningDatasetExampleCount&quot;: string,&quot;totalTuningCharacterCount&quot;: string,&quot;totalBillableCharacterCount&quot;: string,&quot;tuningStepCount&quot;: string,&quot;userInputTokenDistribution&quot;: {object (DatasetDistribution)},&quot;userMessagePerExampleDistribution&quot;: {object (DatasetDistribution)},&quot;userDatasetExamples&quot;: [{object (Content)}],&quot;droppedExampleIndices&quot;: [string],&quot;droppedExampleReasons&quot;: [string],&quot;userOutputTokenDistribution&quot;: {object (DatasetDistribution)}}</code></pre></td>
</tr>
</tbody>
</table>

## DatasetDistribution

Distribution computed over a tuning dataset.

Fields

`sum` `number`

Output only. Sum of a given population of values.

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

`buckets[]` ` object ( DistributionBucket  ` )

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;sum&quot;: number,&quot;min&quot;: number,&quot;max&quot;: number,&quot;mean&quot;: number,&quot;median&quot;: number,&quot;p5&quot;: number,&quot;p95&quot;: number,&quot;buckets&quot;: [{object (DistributionBucket)}]}</code></pre></td>
</tr>
</tbody>
</table>

## DistributionBucket

Dataset bucket used to create a histogram for the distribution given a population of values.

Fields

`count` `string ( int64 format)`

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
  &quot;count&quot;: string,
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

`aggregationMetric` ` enum ( AggregationMetric  ` )

Aggregation metric.

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

`customCodeExecutionResult` ` object ( CustomCodeExecutionResult  ` )

result for code execution metric.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;aggregationMetric&quot;: enum (AggregationMetric),// aggregation_result&quot;pointwiseMetricResult&quot;: {object (PointwiseMetricResult)},&quot;pairwiseMetricResult&quot;: {object (PairwiseMetricResult)},&quot;exactMatchMetricValue&quot;: {object (ExactMatchMetricValue)},&quot;bleuMetricValue&quot;: {object (BleuMetricValue)},&quot;rougeMetricValue&quot;: {object (RougeMetricValue)},&quot;customCodeExecutionResult&quot;: {object (CustomCodeExecutionResult)}// Union type}</code></pre></td>
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

## CustomCodeExecutionResult

result for custom code execution metric.

Fields

`score` `number`

Output only. Custom code execution score.

<table>
<colgroup>
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
