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

Optional. The display name of the [`TunedModel`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.models#Model) . The name can be up to 128 characters long and can consist of any UTF-8 characters. For continuous tuning, tunedModelDisplayName will by default use the same display name as the pre-tuned model. If a new display name is provided, the tuning job will create a new model instead of a new version.

`description` `string`

Optional. The description of the [`TuningJob`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.tuningJobs#TuningJob) .

`customBaseModel` `string`

Optional. The user-provided path to custom model weights. Set this field to tune a custom model. The path must be a Cloud Storage directory that contains the model weights in .safetensors format along with associated model metadata files. If this field is set, the baseModel field must still be set to indicate which base model the custom model is derived from. This feature is only available for open source models.

`state` `enum ( `[`JobState`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/JobState)` )`

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

`tunedModel` `object ( `[`TunedModel`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.tuningJobs#TunedModel)` )`

Output only. The tuned model resources associated with this [`TuningJob`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.tuningJobs#TuningJob) .

`tuningDataStats` `object ( `[`TuningDataStats`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.tuningJobs#TuningDataStats)` )`

Output only. The tuning data statistics associated with this [`TuningJob`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.tuningJobs#TuningJob) .

`pipelineJob `**`(deprecated)`** `string`

> This item is deprecated!

Output only. The resource name of the PipelineJob associated with the [`TuningJob`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.tuningJobs#TuningJob) . Format: `projects/{project}/locations/{location}/pipelineJobs/{pipelineJob}` .

`encryptionSpec` `object ( `[`EncryptionSpec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/EncryptionSpec)` )`

Customer-managed encryption key options for a TuningJob. If this is set, then all resources created by the TuningJob will be encrypted with the provided encryption key.

`serviceAccount` `string`

The service account that the tuningJob workload runs as. If not specified, the Agent Platform Secure Fine-Tuned service Agent in the project will be used. See <https://cloud.google.com/iam/docs/service-agents#vertex-ai-secure-fine-tuning-service-agent>

Users starting the pipeline must have the `iam.serviceAccounts.actAs` permission on this service account.

`outputUri` `string`

Optional. Cloud Storage path to the directory where tuning job outputs are written to. This field is only available and required for open source models.

`evaluateDatasetRuns[]` `object ( `[`EvaluateDatasetRun`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.tuningJobs#EvaluateDatasetRun)` )`

Output only. Evaluation runs for the Tuning Job.

`satisfiesPzs` `boolean`

Output only. reserved for future use.

`satisfiesPzi` `boolean`

Output only. reserved for future use.

`source_model` `Union type`

The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:

`baseModel` `string`

The base model that is being tuned. See [Supported models](https://cloud.google.com/vertex-ai/generative-ai/docs/model-reference/tuning#supported_models) .

`preTunedModel` `object ( `[`PreTunedModel`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.tuningJobs#PreTunedModel)` )`

The pre-tuned model for continuous tuning.

End of mutually exclusive fields.

`tuning_spec` `Union type`

The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:

`supervisedTuningSpec` `object ( `[`SupervisedTuningSpec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.tuningJobs#SupervisedTuningSpec)` )`

Tuning Spec for Supervised Fine Tuning.

`distillationSpec` `object ( `[`DistillationSpec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.tuningJobs#DistillationSpec)` )`

Tuning Spec for Distillation.

`partnerModelTuningSpec` `object ( `[`PartnerModelTuningSpec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.tuningJobs#PartnerModelTuningSpec)` )`

Tuning Spec for open sourced and third party Partner models.

`reinforcementTuningSpec` `object ( `[`ReinforcementTuningSpec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.tuningJobs#ReinforcementTuningSpec)` )`

Tuning Spec for Reinforcement Tuning.

`veoTuningSpec` `object ( `[`VeoTuningSpec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.tuningJobs#VeoTuningSpec)` )`

Tuning Spec for Veo Tuning.

`veoLoraTuningSpec` `object ( `[`VeoLoraTuningSpec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.tuningJobs#VeoLoraTuningSpec)` )`

Tuning Spec for Veo LoRA Tuning.

End of mutually exclusive fields.

**JSON representation**

```
{
  "name": string,
  "tunedModelDisplayName": string,
  "description": string,
  "customBaseModel": string,
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
  "pipelineJob": string,
  "encryptionSpec": {
    object (EncryptionSpec)
  },
  "serviceAccount": string,
  "outputUri": string,
  "evaluateDatasetRuns": [
    {
      object (EvaluateDatasetRun)
    }
  ],
  "satisfiesPzs": boolean,
  "satisfiesPzi": boolean,

  // source_model
  "baseModel": string,
  "preTunedModel": {
    object (PreTunedModel)
  }
  // Union type

  // tuning_spec
  "supervisedTuningSpec": {
    object (SupervisedTuningSpec)
  },
  "distillationSpec": {
    object (DistillationSpec)
  },
  "partnerModelTuningSpec": {
    object (PartnerModelTuningSpec)
  },
  "reinforcementTuningSpec": {
    object (ReinforcementTuningSpec)
  },
  "veoTuningSpec": {
    object (VeoTuningSpec)
  },
  "veoLoraTuningSpec": {
    object (VeoLoraTuningSpec)
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

Output only. The name of the base model this [`PreTunedModel`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.tuningJobs#PreTunedModel) was tuned from.

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

`hyperParameters` `object ( `[`SupervisedHyperParameters`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.tuningJobs#SupervisedHyperParameters)` )`

Optional. Hyperparameters for SFT.

`exportLastCheckpointOnly` `boolean`

Optional. If set to true, disable intermediate checkpoints for SFT and only the last checkpoint will be exported. Otherwise, enable intermediate checkpoints for SFT. Default is false.

`evaluationConfig` `object ( `[`EvaluationConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.tuningJobs#EvaluationConfig)` )`

Optional. Evaluation Config for Tuning Job.

`tuningMode` `enum ( `[`TuningMode`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.tuningJobs#TuningMode)` )`

Tuning mode.

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
  },
  "tuningMode": enum (TuningMode)
}
```

## SupervisedHyperParameters

Hyperparameters for SFT.

Fields

`epochCount` `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)`

Optional. Number of complete passes the model makes over the entire training dataset during training.

`learningRateMultiplier` `number`

Optional. Multiplier for adjusting the default learning rate. Mutually exclusive with `learningRate` . This feature is only available for 1P models.

`learningRate` `number`

Optional. Learning rate for tuning. Mutually exclusive with `learningRateMultiplier` . This feature is only available for open source models.

`adapterSize` `enum ( `[`AdapterSize`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.tuningJobs#AdapterSize)` )`

Optional. Adapter size for tuning.

`batchSize` `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)`

Optional. Batch size for tuning. This feature is only available for open source models.

**JSON representation**

```
{
  "epochCount": string,
  "learningRateMultiplier": number,
  "learningRate": number,
  "adapterSize": enum (AdapterSize),
  "batchSize": string
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

`metrics[]` `object ( `[`Metric`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/Metric)` )`

Required. The metrics used for evaluation.

`outputConfig` `object ( `[`OutputConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.tuningJobs#OutputConfig)` )`

Required. Config for evaluation output.

`autoraterConfig` `object ( `[`AutoraterConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/AutoraterConfig)` )`

Optional. Autorater config for evaluation.

`inferenceGenerationConfig` `object ( `[`GenerationConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/GeminiExample#GenerationConfig)` )`

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

## OutputConfig

Config for evaluation output.

Fields

`destination` `Union type`

The destination for evaluation output. The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:

`gcsDestination` `object ( ``GcsDestination`` )`

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

## TuningMode

Supported tuning modes.

| Enums                      |                             |
|----------------------------|-----------------------------|
| `TUNING_MODE_UNSPECIFIED`  | Tuning mode is unspecified. |
| `TUNING_MODE_FULL`         | Full fine-tuning mode.      |
| `TUNING_MODE_PEFT_ADAPTER` | PEFT adapter tuning mode.   |

## DistillationSpec

Tuning Spec for Distillation.

Fields

`trainingDatasetUri `**`(deprecated)`** `string`

> This item is deprecated!

Deprecated. Cloud Storage path to file containing training dataset for tuning. The dataset must be formatted as a JSONL file.

`promptDatasetUri` `string`

Optional. Cloud Storage path to file containing prompt dataset for distillation. The dataset must be formatted as a JSONL file.

`hyperParameters` `object ( `[`DistillationHyperParameters`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.tuningJobs#DistillationHyperParameters)` )`

Optional. Hyperparameters for Distillation.

`studentModel `**`(deprecated)`** `string`

> This item is deprecated!

The student model that is being tuned, e.g., "google/gemma-2b-1.1-it". Deprecated. Use baseModel instead.

`pipelineRootDirectory `**`(deprecated)`** `string`

> This item is deprecated!

Deprecated. A path in a Cloud Storage bucket, which will be treated as the root output directory of the distillation pipeline. It is used by the system to generate the paths of output artifacts.

`tuningMode` `enum ( `[`TuningMode`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.tuningJobs#TuningMode)` )`

Optional. Specifies the tuning mode for distillation (sft part). This feature is only available for open source models.

`teacher_model` `Union type`

The teacher model that is being distilled from. See [Supported models](https://cloud.google.com/vertex-ai/generative-ai/docs/model-reference/tuning#supported_models) . The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:

`baseTeacherModel` `string`

The base teacher model that is being distilled. See [Supported models](https://cloud.google.com/vertex-ai/generative-ai/docs/model-reference/tuning#supported_models) .

`tunedTeacherModelSource` `string`

The resource name of the Tuned teacher model. Format: `projects/{project}/locations/{location}/models/{model}` .

End of mutually exclusive fields.

`validationDatasetUri` `string`

Optional. Cloud Storage path to file containing validation dataset for tuning. The dataset must be formatted as a JSONL file.

**JSON representation**

```
{
  "trainingDatasetUri": string,
  "promptDatasetUri": string,
  "hyperParameters": {
    object (DistillationHyperParameters)
  },
  "studentModel": string,
  "pipelineRootDirectory": string,
  "tuningMode": enum (TuningMode),

  // teacher_model
  "baseTeacherModel": string,
  "tunedTeacherModelSource": string
  // Union type
  "validationDatasetUri": string
}
```

## DistillationHyperParameters

Hyperparameters for Distillation.

Fields

`adapterSize` `enum ( `[`AdapterSize`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.tuningJobs#AdapterSize)` )`

Optional. Adapter size for distillation.

`learningRate` `number`

Optional. Specifies the learning rate for tuning. Mutually exclusive with `learningRateMultiplier` . This feature is only available for open source models.

`batchSize` `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)`

Optional. Batch size for tuning. This feature is only available for open source models.

`epochCount` `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)`

Optional. Number of complete passes the model makes over the entire training dataset during training.

`learningRateMultiplier` `number`

Optional. Multiplier for adjusting the default learning rate.

**JSON representation**

```
{
  "adapterSize": enum (AdapterSize),
  "learningRate": number,
  "batchSize": string,
  "epochCount": string,
  "learningRateMultiplier": number
}
```

## PartnerModelTuningSpec

Tuning spec for Partner models.

Fields

`trainingDatasetUri` `string`

Required. Cloud Storage path to file containing training dataset for tuning. The dataset must be formatted as a JSONL file.

`validationDatasetUri` `string`

Optional. Cloud Storage path to file containing validation dataset for tuning. The dataset must be formatted as a JSONL file.

`hyperParameters` `map (key: string, value: value ( `[`Value`](https://protobuf.dev/reference/protobuf/google.protobuf/#value)` format))`

Hyperparameters for tuning. The accepted hyperParameters and their valid range of values will differ depending on the base model.

**JSON representation**

```
{
  "trainingDatasetUri": string,
  "validationDatasetUri": string,
  "hyperParameters": {
    string: value,
    ...
  }
}
```

## ReinforcementTuningSpec

Tuning spec for Reinforcement Tuning.

Fields

`hyperParameters` `object ( `[`ReinforcementTuningHyperParameters`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.tuningJobs#ReinforcementTuningHyperParameters)` )`

Optional. Hyper-parameters for reinforcement tuning.

`training_dataset` `Union type`

The dataset to use for training. The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:

`trainingDatasetUri` `string`

Cloud Storage path to the file containing training dataset for tuning. The dataset must be formatted as a JSONL file.

End of mutually exclusive fields.

`validation_dataset` `Union type`

The dataset to use for validation. The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:

`validationDatasetUri` `string`

Cloud Storage path to the file containing validation dataset for tuning. The dataset must be formatted as a JSONL file.

End of mutually exclusive fields.

`reward_config` `Union type`

Reward function configuration for reinforcement tuning. The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:

`singleRewardConfig` `object ( `[`SingleReinforcementTuningRewardConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.tuningJobs#SingleReinforcementTuningRewardConfig)` )`

Single Reward function configuration for reinforcement tuning.

`compositeRewardConfig` `object ( `[`CompositeReinforcementTuningRewardConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.tuningJobs#CompositeReinforcementTuningRewardConfig)` )`

Composite reward function configuration for reinforcement tuning.

End of mutually exclusive fields.

**JSON representation**

```
{
  "hyperParameters": {
    object (ReinforcementTuningHyperParameters)
  },

  // training_dataset
  "trainingDatasetUri": string
  // Union type

  // validation_dataset
  "validationDatasetUri": string
  // Union type

  // reward_config
  "singleRewardConfig": {
    object (SingleReinforcementTuningRewardConfig)
  },
  "compositeRewardConfig": {
    object (CompositeReinforcementTuningRewardConfig)
  }
  // Union type
}
```

## SingleReinforcementTuningRewardConfig

[`SingleReinforcementTuningRewardConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.tuningJobs#SingleReinforcementTuningRewardConfig) defines a single reward function configuration for RL tuning. Each reward calculation/evaluation consists of two stages:

1.  Stage 1: Parses the part of information important from sample response via regex extract, or simply takes the sample response unmodified.
2.  Stage 2: Calls the configured reward scorer to compute the reward.

Fields

`rewardName` `string`

A unique reward name for identifying each single reinforcement tuning reward.

`parseResponseConfig` `object ( `[`ReinforcementTuningParseResponseConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.tuningJobs#ReinforcementTuningParseResponseConfig)` )`

Defines how to parse sample response.

For example, given a sample response for evaluating the reward, users might want to extract the text only between `<ans>` and `</ans>` in the sample response, and keeps only the last one in case there are multiple such tags. To achieve such a purpose, they can define a regex `".*<ans>(.*?)</ans>"` using the [`ReinforcementTuningParseResponseConfig.ResponseParseType.REGEX_EXTRACT`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.tuningJobs#ResponseParseType.ENUM_VALUES.REGEX_EXTRACT) parse type.

`reward_scorer` `Union type`

After parsing the sample response, the RL Tuning passes the original training/validation data `example` and the parsed response to the configured reward scorer for evaluating a reward. The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:

`codeExecutionRewardScorer` `object ( `[`ReinforcementTuningCodeExecutionRewardScorer`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.tuningJobs#ReinforcementTuningCodeExecutionRewardScorer)` )`

[`ReinforcementTuningCodeExecutionRewardScorer`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.tuningJobs#ReinforcementTuningCodeExecutionRewardScorer) is used to score parsed responses for code execution use cases.

`stringMatchRewardScorer` `object ( `[`ReinforcementTuningStringMatchRewardScorer`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.tuningJobs#ReinforcementTuningStringMatchRewardScorer)` )`

[`ReinforcementTuningStringMatchRewardScorer`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.tuningJobs#ReinforcementTuningStringMatchRewardScorer) is used to score parsed responses for simple string matching use cases against reference answers.

`autoraterScorer` `object ( `[`ReinforcementTuningAutoraterScorer`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.tuningJobs#ReinforcementTuningAutoraterScorer)` )`

[`ReinforcementTuningAutoraterScorer`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.tuningJobs#ReinforcementTuningAutoraterScorer) is used to score parsed responses based on score computed by an autorater.

`cloudRunRewardScorer` `object ( `[`ReinforcementTuningCloudRunRewardScorer`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.tuningJobs#ReinforcementTuningCloudRunRewardScorer)` )`

[`ReinforcementTuningCloudRunRewardScorer`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.tuningJobs#ReinforcementTuningCloudRunRewardScorer) is used to score parsed responses by calling a Cloud Run service.

End of mutually exclusive fields.

**JSON representation**

```
{
  "rewardName": string,
  "parseResponseConfig": {
    object (ReinforcementTuningParseResponseConfig)
  },

  // reward_scorer
  "codeExecutionRewardScorer": {
    object (ReinforcementTuningCodeExecutionRewardScorer)
  },
  "stringMatchRewardScorer": {
    object (ReinforcementTuningStringMatchRewardScorer)
  },
  "autoraterScorer": {
    object (ReinforcementTuningAutoraterScorer)
  },
  "cloudRunRewardScorer": {
    object (ReinforcementTuningCloudRunRewardScorer)
  }
  // Union type
}
```

## ReinforcementTuningCodeExecutionRewardScorer

[`ReinforcementTuningCodeExecutionRewardScorer`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.tuningJobs#ReinforcementTuningCodeExecutionRewardScorer) allows users to implement a function to evaluate rewards for the sample response. The function signature is as follows:

```
def evaluate(example: dict[str, Any], response: dict[str, Any]) -> float:
  ...
```

`example` is a [`ReinforcementTuningExample`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.tuningJobs#ReinforcementTuningExample) in ProtoJSON format, (i.e., the format is the same as as one line in the training/validation dataset except that the keys must be in camel case). System instructions (i.e., `example.get("systemInstruction")` ) and references (i.e., `example.get("references")` ) are also included in the `example` provided that they are set in the training/validation dataset.

`response` is a [`Content`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/Content) in ProtoJSON format (i.e., keys must be in camel case), which is the same as the Online Prediction response for Gemini models.

Note: Reward output by the `evaluate` function is clipped to be within `[-1, 1]` , i.e., `reward = max(min(reward, 1.0), -1.0)` .

Fields

`pythonCodeSnippet` `string`

The python code snippet as a string for evaluating rewards.

The following is an example python code snippet that returns a reward `1.0` for a parsed response matching the user-provided reference answer in per prompt references map.

```
def evaluate(example, response) -> float:
  response_str = response.get("parts", [])[0]["text"]
  references = example.get("references", {})

  if response_str == references.get("concise_answer"):
    return 1.0
  return -1.0
```

Note: Reward output by the evaluate function is clipped to be within `[-1, 1]` , i.e., `reward = max(min(reward, 1.0), -1.0)` .

**JSON representation**

```
{
  "pythonCodeSnippet": string
}
```

## ReinforcementTuningStringMatchRewardScorer

[`ReinforcementTuningStringMatchRewardScorer`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.tuningJobs#ReinforcementTuningStringMatchRewardScorer) is used to score parsed responses for string matching use cases. For example, for math problems, users can use string match scorer to check if the correct exact answer is generated.

Note: Reward returned by the string match reward function is clipped to be within `[-1, 1]` if [`wrongAnswerReward`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.tuningJobs#ReinforcementTuningStringMatchRewardScorer.FIELDS.wrong_answer_reward) or [`correctAnswerReward`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.tuningJobs#ReinforcementTuningStringMatchRewardScorer.FIELDS.correct_answer_reward) are beyond the range, i.e., `reward = max(min(reward, 1.0), -1.0)` .

Fields

`expression` `Union type`

Evaluates parsed response using either string match expression or json match expression. The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:

`stringMatchExpression` `object ( `[`StringMatchExpression`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.tuningJobs#StringMatchExpression)` )`

uses string match expression to evaluate parsed response.

`jsonMatchExpression` `object ( `[`JsonMatchExpression`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.tuningJobs#JsonMatchExpression)` )`

uses json match expression to evaluate parsed response.

End of mutually exclusive fields.

`wrongAnswerReward` `number`

Wrong answer reward is returned if the parsed response is evaluated as `false` . All wrong answers get the same reward.

`correctAnswerReward` `number`

Correct answer rewawrd is returned if the parsed response is evaluated as `true` . All correct answers get the same reward.

**JSON representation**

```
{

  // expression
  "stringMatchExpression": {
    object (StringMatchExpression)
  },
  "jsonMatchExpression": {
    object (JsonMatchExpression)
  }
  // Union type
  "wrongAnswerReward": number,
  "correctAnswerReward": number
}
```

## StringMatchExpression

Evaluates parsed response using match type against the expression. Returns `true` if `MatchOperation(target, expression)` evaluates to `true` , and `false` otherwise.

Fields

`matchOperation` `enum ( `[`MatchOperation`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.tuningJobs#MatchOperation)` )`

Match operation to use for evaluating rewards.

`expression` `string`

A string or a regular expression to match against for evaluating rewards.

Users can also provide a references map of `{key: value}` whose `value` will be used to replace the placeholder {{references.key}} in the [`expression`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.tuningJobs#StringMatchExpression.FIELDS.expression) .

For example, if the following `references` are defined in the training / validation dataset:

```
{
  "systemInstruction": ...,
  "contents": ...,
  "references": {
    "concise_answer": "Yes",
    "verbose_answer": "The answer is <ans>Yes</ans>"
  }
}
```

and if users define the following [`StringMatchExpression`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.tuningJobs#StringMatchExpression) :

```
{
  "matchOperation": "REGEX_CONTAINS",
  "expression":
    ".*{{references.concise_answer}}.*"
}
```

On evaluating the reward for each sample response, this [`StringMatchExpression`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.tuningJobs#StringMatchExpression) will be substituted as:

```
{
  "matchOperation": "REGEX_CONTAINS",
  "expression": ".*Yes.*"
}
```

**JSON representation**

```
{
  "matchOperation": enum (MatchOperation),
  "expression": string
}
```

## MatchOperation

Match operation to use for evaluating rewards.

| Enums                         |                                                                                                                                                                                                                                                 |
|-------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `MATCH_OPERATION_UNSPECIFIED` | Default value. A user error will be returned if not set.                                                                                                                                                                                        |
| `REGEX_CONTAINS`              | Equivalent to [GoogleSQL](https://cloud.google.com/bigquery/docs/reference/standard-sql/string_functions#regexp_contains) `REGEX_CONTAINS(target, expression)` .                                                                                |
| `PARTIAL_MATCH`               | The match operation returns `true` if [`expression`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.tuningJobs#StringMatchExpression.FIELDS.expression) is a substring of the target. |
| `EXACT_MATCH`                 | The match operation returns `true` [`expression`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.tuningJobs#StringMatchExpression.FIELDS.expression) is an exact match of the target. |

## JsonMatchExpression

[`JsonMatchExpression`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.tuningJobs#JsonMatchExpression) supports converting the parsed responses to JSON format, finding the value in the JSON response that matches the [`keyName`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.tuningJobs#JsonMatchExpression.FIELDS.key_name) in the first level, and performing [`StringMatchExpression`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.tuningJobs#StringMatchExpression) operation on the matched JSON value.

Fields

`valueStringMatchExpression` `object ( `[`StringMatchExpression`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.tuningJobs#StringMatchExpression)` )`

String match expression to match against the extracted value from the JSON representation of the parsed response.

`keyName` `string`

The key name to find the value in the parsed response that's in JSON format. Only first-level key matching is supported.

**JSON representation**

```
{
  "valueStringMatchExpression": {
    object (StringMatchExpression)
  },
  "keyName": string
}
```

## ReinforcementTuningAutoraterScorer

[`ReinforcementTuningAutoraterScorer`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.tuningJobs#ReinforcementTuningAutoraterScorer) is used to score parsed responses for classification based autorater use cases. For example, for math problems, users can use classification based autorater to calculate rewards based on the autorater parsed response against a reference answer.

Fields

`autoraterPrompt` `string`

The prompt for an autorater to scorer the parsed sample response. This field supports the following placeholders that will be replaced before scoring:

- `{{prompt}}`
- `{{response}}`
- `{{system_instruction}}`
- `{{references.key}}`

`autoraterConfig` `object ( `[`AutoraterConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/AutoraterConfig)` )`

Autorater config for classification based autorater

`autoraterResponseParseConfig` `object ( `[`ReinforcementTuningParseResponseConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.tuningJobs#ReinforcementTuningParseResponseConfig)` )`

Parses autorater returned response for scoring. For example, if the autorater response has reward stored in the `<ans>2.0</ans>` block, defining a parsing response config using regex `".*<ans>(.*?)</ans>"` will return a score `"2.0"` .

`autorater_scorer` `Union type`

Scorer to be used for scoring autorater responses. The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:

`parsedResponseConversionScorer` `object ( `[`ParsedResponseConversionScorer`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.tuningJobs#ParsedResponseConversionScorer)` )`

Scores autorater responses by directly converting parsed autorater response to a float reward.

Note: Reward is clipped to be within `[-1, 1]` , i.e., `reward = max(min(reward, 1.0), -1.0)` .

`exactMatchScorer` `object ( `[`ExactMatchScorer`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.tuningJobs#ExactMatchScorer)` )`

Scores autorater responses by using string match reward scorer.

End of mutually exclusive fields.

**JSON representation**

```
{
  "autoraterPrompt": string,
  "autoraterConfig": {
    object (AutoraterConfig)
  },
  "autoraterResponseParseConfig": {
    object (ReinforcementTuningParseResponseConfig)
  },

  // autorater_scorer
  "parsedResponseConversionScorer": {
    object (ParsedResponseConversionScorer)
  },
  "exactMatchScorer": {
    object (ExactMatchScorer)
  }
  // Union type
}
```

## ParsedResponseConversionScorer

This type has no fields.

Scores responses by directly converting the parsed autorater response to a float reward.

Note: Reward is clipped to be within `[-1, 1]` , i.e., `reward = max(min(reward, 1.0), -1.0)` .

## ExactMatchScorer

Scores autorater responses by using exact string match reward scorer.

Fields

`correctAnswerReward` `number`

Assigns this reward score if the parsed response string equals the expression.

`wrongAnswerReward` `number`

Assigns this reward score if the parsed reward value does not equal the expression.

`expression` `string`

The string expression to match against for scoring. This field supports placeholders in the format of {{references.key}} that will be replaced before matching. Regex is not supported for this [`expression`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.tuningJobs#ExactMatchScorer.FIELDS.expression) .

For example, users can define an [`ExactMatchScorer`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.tuningJobs#ExactMatchScorer) as follows:

```
{
  "correctAnswerReward": 1.0,
  "wrongAnswerReward": -1.0,
  "expression":
    "{{references.concise_answer}}"
}
```

When evaluating the reward for each parsed autorater response, if the prompt references in the training/validation dataset has the following fields:

```
{
  "example": ...,
  "references": {
    "concise_ansser": "Yes",
    "verbose_answer": "The answer is <ans>Yes</ans>"
  }
}
```

The above [`ExactMatchScorer`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.tuningJobs#ExactMatchScorer) will be replaced as follows for scoring:

```
{
  "correctAnswerReward": 1.0,
  "wrongAnswerReward": -1.0,
  "expression": "Yes"
}
```

If the *parsed* autorater response is equal to the string `"Yes"` , then the reward is `1.0` , otherwise the reward is `-1.0` .

**JSON representation**

```
{
  "correctAnswerReward": number,
  "wrongAnswerReward": number,
  "expression": string
}
```

## ReinforcementTuningParseResponseConfig

Defines how to parse sample response config for reinforcement tuning. The parsed response (i.e., substring) will be passed to the reward functions.

For example, the input prompt might be:

> "Perform step-by-step thoughts first to problem A, finally output answer in the \<ans\> \</ans\> block."

The sample response from the model under tuning might look like:

> "\<ans\>Yes\</ans\>"

Here, users can define the following parse config:

```
{
  "parseType": "REGEX_EXTRACT",
  "regexExtractExpression": ".*<ans>(.*?)</ans>"
}
```

The resulting parsed response would be `"Yes"` and will be passed to the reward functions for evaluating rewards.

Fields

`parseType` `enum ( `[`ResponseParseType`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.tuningJobs#ResponseParseType)` )`

Defines the type for parsing sample response.

`regexExtractExpression` `string`

Defines the regex for extracting the important part of sample response. This field is only used when [`parseType`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.tuningJobs#ReinforcementTuningParseResponseConfig.FIELDS.parse_type) is [`ResponseParseType.REGEX_EXTRACT`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.tuningJobs#ResponseParseType.ENUM_VALUES.REGEX_EXTRACT) .

**JSON representation**

```
{
  "parseType": enum (ResponseParseType),
  "regexExtractExpression": string
}
```

## ResponseParseType

Defines the type for parsing sample response.

| Enums                             |                                                                                                                                                                                                                                                                                                                              |
|-----------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `RESPONSE_PARSE_TYPE_UNSPECIFIED` | Default value. Fallback to [`IDENTITY`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.tuningJobs#ResponseParseType.ENUM_VALUES.IDENTITY)                                                                                                                          |
| `IDENTITY`                        | Returns the sample response as is.                                                                                                                                                                                                                                                                                           |
| `REGEX_EXTRACT`                   | uses regex to extract the important part of sample response. Similar to [GoogleSQL](https://cloud.google.com/bigquery/docs/reference/standard-sql/string_functions#regexp_extract) `REGEX_EXTRACT(response, regexExtractExpression)` , but different in that if there are multiple matches, the last match will be returned. |

## ReinforcementTuningCloudRunRewardScorer

[`ReinforcementTuningCloudRunRewardScorer`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.tuningJobs#ReinforcementTuningCloudRunRewardScorer) allows users to implement a reward function through GCP Cloud Run. Comparing with [`ReinforcementTuningCodeExecutionRewardScorer`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.tuningJobs#ReinforcementTuningCodeExecutionRewardScorer) that runs in a Sandbox and has no internet access, Cloud Run reward scorer is fully controlled by users.

The Cloud Run service should implement the following HTTP API:

HTTP method: `POST`

HTTP request body:

```
{
  "example": ReinforcementTuningExample,
  "response": Content,
  "metadata": {
    "step": int
    "tuning_job_id": int64
  }
}
```

- `example` is a [`ReinforcementTuningExample`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.tuningJobs#ReinforcementTuningExample) in ProtoJSON format, (i.e., the format is the same as as one line in the training/validation dataset except that the keys must be in camel case). System instructions (i.e., `example.get("systemInstruction")` ) and references (i.e., `example.get("references")` ) are also included in the `example` provided that they are set in the training/validation dataset.
- `response` is a [`Content`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/Content) in ProtoJSON format (i.e., keys must be in camel case), which is the same as the Online Prediction response for Gemini models.

HTTP response body:

```
{
  "reward": float,
  "user_requested_aux_info": str // Optional
}
```

where the field "user_requested_aux_info" is any (optional) string provided by users for assisting debugging. It's in snake case. This field is mostly useful when calling the [`GenAiTuningService.ValidateReinforcementTuningReward`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.tuningJobs/validateReinforcementTuningReward#google.cloud.aiplatform.v1beta1.GenAiTuningService.ValidateReinforcementTuningReward) API, where the proto field (not Cloud Run HTTP response body) [`userRequestedAuxInfo`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.tuningJobs/validateReinforcementTuningReward#ReinforcementTuningRewardInfo.FIELDS.user_requested_aux_info) will be populated if the Cloud Run reward function sets this field in the HTTP response.

The following are examples for the HTTP request and response body.

Example HTTP request body:

```
{
  "example": {
    "contents": [
      {
        "role": "user",
        "parts": [
          {
            "text": "What is the capital of France?"
          }
        ]
      }
    ],
    "references": {
      "answer": "Paris"
    }
  },
  "response": {
    "parts": [
      {
        "text": "London"
      }
    ]
  },
  "metadata": {
    "step": 1,
    "tuning_job_id": 123456789
  }
}
```

Example HTTP response body:

```
{
  "reward": -1.0
}
```

Note: Reward output by Cloud Run reward function is clipped to be within `[-1, 1]` , i.e., `reward = max(min(reward, 1.0), -1.0)` .

Fields

`cloudRunUri` `string`

URI of the Cloud Run service that will be used to compute the reward. The [Agent Platform Secure Fine Tuning service Agent](https://docs.cloud.google.com/iam/docs/service-agents#vertex-ai-secure-fine-tuning-service-agent) ( `service-<PROJECT_NUMBER>@gcp-sa-vertex-tune.iam.gserviceaccount.com` ) must be granted the permission (e.g. by granting `roles/run.invoker` in IAM) to invoke the Cloud Run service.

**JSON representation**

```
{
  "cloudRunUri": string
}
```

## CompositeReinforcementTuningRewardConfig

Composite reward function configuration for reinforcement tuning.

Fields

`weightedRewardConfigs[]` `object ( `[`WeightedRewardConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.tuningJobs#WeightedRewardConfig)` )`

List of reward function configurations with weights.

**JSON representation**

```
{
  "weightedRewardConfigs": [
    {
      object (WeightedRewardConfig)
    }
  ]
}
```

## WeightedRewardConfig

Reward function configuration with a weight. The weight is used to combine the reward with other rewards.

Fields

`rewardConfig` `object ( `[`SingleReinforcementTuningRewardConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.tuningJobs#SingleReinforcementTuningRewardConfig)` )`

Single reward configuration.

`weight` `number`

How much this single reward contributes to the total overall reward.

Total reward is a linear combination of single rewards with their corresponding weights, i.e.,

```
total_reward = (
    weight_a * reward_a + weight_b * reward_b + ...
) / (weight_a + weight_b + ...)
```

**JSON representation**

```
{
  "rewardConfig": {
    object (SingleReinforcementTuningRewardConfig)
  },
  "weight": number
}
```

## ReinforcementTuningHyperParameters

Hyperparameters for Reinforcement Tuning.

Fields

`adapterSize` `enum ( `[`AdapterSize`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.tuningJobs#AdapterSize)` )`

Optional. Adapter size for Reinforcement Tuning.

`checkpoint_config` `Union type`

Configurations of checkpointing during training. The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:

`checkpointInterval` `integer`

Optional. How often at steps to save checkpoints during training. If not set, one checkpoint per epoch will be set.

`totalSteps = epochCount * samplesPerPrompt / total_prompts_in_dataset`

End of mutually exclusive fields.

`epochCount` `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)`

Optional. Number of training epoches for the tuning job.

`stepCount` `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)`

Optional. Number of steps for the tuning job (mutually exclusive with [`epochCount`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.tuningJobs#ReinforcementTuningHyperParameters.FIELDS.epoch_count) ).

`learningRateMultiplier` `number`

Optional. Learning rate multiplier for Reinforcement Tuning.

`samplesPerPrompt` `integer`

Optional. Number of different responses to generate per prompt during tuning.

`thinkingBudget` `integer`

Optional. The thinking budget for the tuning job to optimize for (Gemini 2.5 only).

- -1 means dynamic thinking
- 0 means no thinking
- \> 0 means thinking budget in tokens

If not set, default to -1 (dynamic thinking).

`batchSize` `integer`

Optional. Batch size for the tuning job. How many prompts to process at a train step. If not set, the batch size will be determined automatically.

`evaluateInterval` `integer`

Optional. How often at steps to evaluate the tuning job during training. If not set, evel will be run per epoch. `totalSteps = epochCount * samplesPerPrompt / total_prompts_in_dataset`

`maxOutputTokens` `integer`

Optional. The maximum number of tokens to generate per prompt. Default to 32768.

`thinkingLevel` `enum ( `[`ReinforcementTuningThinkingLevel`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.tuningJobs#ReinforcementTuningThinkingLevel)` )`

Indicates the maximum thinking depth during tuning. Starting from Gemini 3.5 models, the old [`thinkingBudget`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.tuningJobs#ReinforcementTuningHyperParameters.FIELDS.thinking_budget) will no longer be supported and will result in a user error if set. Instead, users should use the [`thinkingLevel`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.tuningJobs#ReinforcementTuningHyperParameters.FIELDS.thinking_level) parameter to control the maximum thinking depth.

**JSON representation**

```
{
  "adapterSize": enum (AdapterSize),

  // checkpoint_config
  "checkpointInterval": integer
  // Union type
  "epochCount": string,
  "stepCount": string,
  "learningRateMultiplier": number,
  "samplesPerPrompt": integer,
  "thinkingBudget": integer,
  "batchSize": integer,
  "evaluateInterval": integer,
  "maxOutputTokens": integer,
  "thinkingLevel": enum (ReinforcementTuningThinkingLevel)
}
```

## ReinforcementTuningThinkingLevel

Represents how much to think for the tuning job.

| Enums                                             |                             |
|---------------------------------------------------|-----------------------------|
| `REINFORCEMENT_TUNING_THINKING_LEVEL_UNSPECIFIED` | Unspecified thinking level. |
| `MINIMAL`                                         | Little to no thinking.      |
| `LOW`                                             | Low thinking level.         |
| `MEDIUM`                                          | Medium thinking level.      |
| `HIGH`                                            | High thinking level.        |

## VeoTuningSpec

Tuning Spec for Veo Model Tuning.

Fields

`trainingDatasetUri` `string`

Required. Training dataset used for tuning. The dataset can be specified as either a Cloud Storage path to a JSONL file or as the resource name of a Vertex Multimodal Dataset.

`validationDatasetUri` `string`

Optional. Validation dataset used for tuning. The dataset can be specified as either a Cloud Storage path to a JSONL file or as the resource name of a Vertex Multimodal Dataset.

`hyperParameters` `object ( `[`VeoHyperParameters`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.tuningJobs#VeoHyperParameters)` )`

Optional. Hyperparameters for Veo.

**JSON representation**

```
{
  "trainingDatasetUri": string,
  "validationDatasetUri": string,
  "hyperParameters": {
    object (VeoHyperParameters)
  }
}
```

## VeoHyperParameters

Hyperparameters for Veo.

Fields

`epochCount` `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)`

Optional. Number of complete passes the model makes over the entire training dataset during training.

`learningRateMultiplier` `number`

Optional. Multiplier for adjusting the default learning rate.

`tuningTask` `enum ( `[`TuningTask`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.tuningJobs#TuningTask)` )`

The tuning task for Veo.

`adapterSize` `enum ( `[`AdapterSize`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.tuningJobs#AdapterSize_1)` )`

Optional. The adapter size for LoRA tuning.

`veoDataMixtureRatio` `number`

Optional. The ratio of Google internal dataset to use in the training mixture, in range of `[0, 1)` . If `0.2` , it means 20% of Google internal dataset and 80% of user dataset will be used for training. If not set, the default value is 0.1.

`tuningSpeed` `enum ( `[`TuningSpeed`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.tuningJobs#TuningSpeed)` )`

The speed of the tuning job. Only supported for Veo 3.0 models.

**JSON representation**

```
{
  "epochCount": string,
  "learningRateMultiplier": number,
  "tuningTask": enum (TuningTask),
  "adapterSize": enum (AdapterSize),
  "veoDataMixtureRatio": number,
  "tuningSpeed": enum (TuningSpeed)
}
```

## TuningTask

An enum defining the tuning task used for Veo.

| Enums                     |                                      |
|---------------------------|--------------------------------------|
| `TUNING_TASK_UNSPECIFIED` | Default value. This value is unused. |
| `TUNING_TASK_I2V`         | Tuning task for image to video.      |
| `TUNING_TASK_T2V`         | Tuning task for text to video.       |
| `TUNING_TASK_R2V`         | Tuning task for reference to video.  |

## TuningSpeed

The speed of the tuning job. Only supported for Veo 3.0 models.

| Enums                      |                                                                       |
|----------------------------|-----------------------------------------------------------------------|
| `TUNING_SPEED_UNSPECIFIED` | The default / unset value. For Veo 3.0 models, this defaults to FAST. |
| `REGULAR`                  | Regular tuning speed.                                                 |
| `FAST`                     | Fast tuning speed.                                                    |

## AdapterSize

Adapter size for LoRA tuning.

| Enums                      |                                                                       |
|----------------------------|-----------------------------------------------------------------------|
| `ADAPTER_SIZE_UNSPECIFIED` | Adapter size is unspecified.                                          |
| `ADAPTER_SIZE_EIGHT`       | Adapter size 8. This is the default adapter size for Veo LoRA tuning. |
| `ADAPTER_SIZE_SIXTEEN`     | Adapter size 16.                                                      |
| `ADAPTER_SIZE_THIRTY_TWO`  | Adapter size 32.                                                      |

## VeoLoraTuningSpec

Tuning Spec for Veo LoRA Model Tuning.

Fields

`trainingDatasetUri` `string`

Required. Training dataset used for tuning. The dataset can be specified as either a Cloud Storage path to a JSONL file or as the resource name of a Vertex Multimodal Dataset.

`validationDatasetUri` `string`

Optional. Validation dataset used for tuning. The dataset can be specified as either a Cloud Storage path to a JSONL file or as the resource name of a Vertex Multimodal Dataset.

`hyperParameters` `object ( `[`VeoHyperParameters`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.tuningJobs#VeoHyperParameters)` )`

Optional. Hyperparameters for Veo LoRA.

**JSON representation**

```
{
  "trainingDatasetUri": string,
  "validationDatasetUri": string,
  "hyperParameters": {
    object (VeoHyperParameters)
  }
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

`checkpoints[]` `object ( `[`TunedModelCheckpoint`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.tuningJobs#TunedModelCheckpoint)` )`

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

`supervisedTuningDataStats` `object ( `[`SupervisedTuningDataStats`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.tuningJobs#SupervisedTuningDataStats)` )`

The SFT Tuning data stats.

`distillationDataStats` `object ( `[`DistillationDataStats`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.tuningJobs#DistillationDataStats)` )`

Output only. Statistics for distillation prompt dataset. These statistics do not include the responses sampled from the teacher model.

End of mutually exclusive fields.

**JSON representation**

```
{

  // tuning_data_stats
  "supervisedTuningDataStats": {
    object (SupervisedTuningDataStats)
  },
  "distillationDataStats": {
    object (DistillationDataStats)
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

`userInputTokenDistribution` `object ( `[`SupervisedTuningDatasetDistribution`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.tuningJobs#SupervisedTuningDatasetDistribution)` )`

Output only. Dataset distributions for the user input tokens.

`userOutputTokenDistribution` `object ( `[`SupervisedTuningDatasetDistribution`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.tuningJobs#SupervisedTuningDatasetDistribution)` )`

Output only. Dataset distributions for the user output tokens.

`userMessagePerExampleDistribution` `object ( `[`SupervisedTuningDatasetDistribution`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.tuningJobs#SupervisedTuningDatasetDistribution)` )`

Output only. Dataset distributions for the messages per example.

`userDatasetExamples[]` `object ( `[`Content`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/Content)` )`

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

`buckets[]` `object ( `[`DatasetBucket`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.tuningJobs#DatasetBucket)` )`

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

## DistillationDataStats

Statistics for distillation prompt dataset. These statistics do not include the responses sampled from the teacher model.

Fields

`trainingDatasetStats` `object ( `[`DatasetStats`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.tuningJobs#DatasetStats)` )`

Output only. Statistics computed for the training dataset.

**JSON representation**

```
{
  "trainingDatasetStats": {
    object (DatasetStats)
  }
}
```

## DatasetStats

Statistics computed over a tuning dataset.

Fields

`tuningDatasetExampleCount` `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)`

Output only. Number of examples in the tuning dataset.

`totalBillableTokenCount` `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)`

Output only. Number of billable tokens in the tuning dataset.

`totalTuningCharacterCount` `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)`

Output only. Number of tuning characters in the tuning dataset.

`totalBillableCharacterCount` `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)`

Output only. Number of billable characters in the tuning dataset.

`tuningStepCount` `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)`

Output only. Number of tuning steps for this Tuning Job.

`userInputTokenDistribution` `object ( `[`DatasetDistribution`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.tuningJobs#DatasetDistribution)` )`

Output only. Dataset distributions for the user input tokens.

`userMessagePerExampleDistribution` `object ( `[`DatasetDistribution`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.tuningJobs#DatasetDistribution)` )`

Output only. Dataset distributions for the messages per example.

`userDatasetExamples[]` `object ( `[`Content`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/Content)` )`

Output only. Sample user messages in the training dataset uri.

`droppedExampleIndices[]` `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)`

Output only. A partial sample of the indices (starting from 1) of the dropped examples.

`droppedExampleReasons[]` `string`

Output only. For each index in `droppedExampleIndices` , the user-facing reason why the example was dropped.

`dataset_examples` `Union type`

Sample user dataset examples in the training dataset uri. This will replace the old `user_dataset_examples` field. The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:

`reinforcementTuningUserDatasetExamples` `object ( `[`ReinforcementTuningUserDatasetExamples`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.tuningJobs#ReinforcementTuningUserDatasetExamples)` )`

Output only. Sample user dataset examples in the training dataset uri for Reinforcement Tuning.

End of mutually exclusive fields.

`userOutputTokenDistribution` `object ( `[`DatasetDistribution`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.tuningJobs#DatasetDistribution)` )`

Output only. Dataset distributions for the user output tokens.

**JSON representation**

```
{
  "tuningDatasetExampleCount": string,
  "totalBillableTokenCount": string,
  "totalTuningCharacterCount": string,
  "totalBillableCharacterCount": string,
  "tuningStepCount": string,
  "userInputTokenDistribution": {
    object (DatasetDistribution)
  },
  "userMessagePerExampleDistribution": {
    object (DatasetDistribution)
  },
  "userDatasetExamples": [
    {
      object (Content)
    }
  ],
  "droppedExampleIndices": [
    string
  ],
  "droppedExampleReasons": [
    string
  ],

  // dataset_examples
  "reinforcementTuningUserDatasetExamples": {
    object (ReinforcementTuningUserDatasetExamples)
  }
  // Union type
  "userOutputTokenDistribution": {
    object (DatasetDistribution)
  }
}
```

## ReinforcementTuningUserDatasetExamples

Sample reinforcement tuning user data in the training dataset. The contents are truncated for better UI showing.

Fields

`userDatasetExamples[]` `object ( `[`ReinforcementTuningExample`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.tuningJobs#ReinforcementTuningExample)` )`

List of user datasset examples showing to user.

**JSON representation**

```
{
  "userDatasetExamples": [
    {
      object (ReinforcementTuningExample)
    }
  ]
}
```

## ReinforcementTuningExample

user-facing format for Gemini Reinforcement Tuning examples on Vertex.

Fields

`contents[]` `object ( `[`Content`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/Content)` )`

Multi-turn contents that represents the Prompt.

`references` `map (key: string, value: string)`

References for the given prompt. The key is the name of the reference, and the value is the reference itself. Users can use this field together with the reward configurations to calculate rewards for reinforcement tuning. For example, users can set the following references:

```
{
  "concise_answer": "Yes",
  "verbose_answer": "The answer is <ans>Yes</ans>"
}
```

Then in a [`ReinforcementTuningCodeExecutionRewardScorer`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.tuningJobs#ReinforcementTuningCodeExecutionRewardScorer) reward function config, for example, they can define a python code snippet as follows:

```
def evaluate(example, response) -> float:
  response_str = response.get("parts", [])[0]["text"]
  references = example.get("references", {})

  if response_str == references.get("concise_answer"):
    return 1.0
  return -1.0
```

In this case, [`references`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.tuningJobs#ReinforcementTuningExample.FIELDS.references) can serve the purpose of holding the ground truth of this example in the training/validation dataset.

`systemInstruction` `object ( `[`Content`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/Content)` )`

Corresponds to [`systemInstruction`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.tuningJobs#ReinforcementTuningExample.FIELDS.system_instruction) in user-facing `GenerateContentRequest` .

**JSON representation**

```
{
  "contents": [
    {
      object (Content)
    }
  ],
  "references": {
    string: string,
    ...
  },
  "systemInstruction": {
    object (Content)
  }
}
```

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

`buckets[]` `object ( `[`DistributionBucket`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.tuningJobs#DistributionBucket)` )`

Output only. Defines the histogram bucket.

**JSON representation**

```
{
  "sum": number,
  "min": number,
  "max": number,
  "mean": number,
  "median": number,
  "p5": number,
  "p95": number,
  "buckets": [
    {
      object (DistributionBucket)
    }
  ]
}
```

## DistributionBucket

Dataset bucket used to create a histogram for the distribution given a population of values.

Fields

`count` `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)`

Output only. Number of values in the bucket.

`left` `number`

Output only. left bound of the bucket.

`right` `number`

Output only. Right bound of the bucket.

**JSON representation**

```
{
  "count": string,
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

`evaluateDatasetResponse` `object ( `[`EvaluateDatasetResponse`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.tuningJobs#EvaluateDatasetResponse)` )`

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

`aggregationOutput` `object ( `[`AggregationOutput`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.tuningJobs#AggregationOutput)` )`

Output only. Aggregation statistics derived from results of EvaluationService.

`outputInfo` `object ( `[`OutputInfo`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.tuningJobs#OutputInfo)` )`

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

`dataset` `object ( `[`EvaluationDataset`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.tuningJobs#EvaluationDataset)` )`

The dataset used for evaluation & aggregation.

`aggregationResults[]` `object ( `[`AggregationResult`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.tuningJobs#AggregationResult)` )`

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

`gcsSource` `object ( `[`GcsSource`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/GcsSource)` )`

Cloud storage source holds the dataset. Currently only one Cloud Storage file path is supported.

`bigquerySource` `object ( `[`BigQuerySource`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/BigQuerySource)` )`

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

`aggregationMetric` `enum ( `[`AggregationMetric`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/AggregationMetric)` )`

Aggregation metric.

`aggregation_result` `Union type`

The aggregation result. The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:

`pointwiseMetricResult` `object ( `[`PointwiseMetricResult`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.tuningJobs#PointwiseMetricResult)` )`

result for pointwise metric.

`pairwiseMetricResult` `object ( `[`PairwiseMetricResult`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.tuningJobs#PairwiseMetricResult)` )`

result for pairwise metric.

`exactMatchMetricValue` `object ( `[`ExactMatchMetricValue`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.tuningJobs#ExactMatchMetricValue)` )`

Results for exact match metric.

`bleuMetricValue` `object ( `[`BleuMetricValue`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.tuningJobs#BleuMetricValue)` )`

Results for bleu metric.

`rougeMetricValue` `object ( `[`RougeMetricValue`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.tuningJobs#RougeMetricValue)` )`

Results for rouge metric.

`customCodeExecutionResult` `object ( `[`CustomCodeExecutionResult`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.tuningJobs#CustomCodeExecutionResult)` )`

result for code execution metric.

End of mutually exclusive fields.

**JSON representation**

```
{
  "aggregationMetric": enum (AggregationMetric),

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
  },
  "customCodeExecutionResult": {
    object (CustomCodeExecutionResult)
  }
  // Union type
}
```

## PointwiseMetricResult

Spec for pointwise metric result.

Fields

`explanation` `string`

Output only. Explanation for pointwise metric score.

`customOutput` `object ( `[`CustomOutput`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.tuningJobs#CustomOutput)` )`

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

`rawOutputs` `object ( `[`RawOutput`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.tuningJobs#RawOutput)` )`

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

`pairwiseChoice` `enum ( `[`PairwiseChoice`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.tuningJobs#PairwiseChoice)` )`

Output only. Pairwise metric choice.

`explanation` `string`

Output only. Explanation for pairwise metric score.

`customOutput` `object ( `[`CustomOutput`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.tuningJobs#CustomOutput)` )`

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

## CustomCodeExecutionResult

result for custom code execution metric.

Fields

`score` `number`

Output only. Custom code execution score.

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

| Methods                                                                                                                                                                                      |                                        |
|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------------------------------|
| [`cancel`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.tuningJobs/cancel)                                                       | Cancels a tuning job.                  |
| [`create`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.tuningJobs/create)                                                       | Creates a tuning job.                  |
| [`get`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.tuningJobs/get)                                                             | Gets a tuning job.                     |
| [`list`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.tuningJobs/list)                                                           | Lists tuning jobs in a location.       |
| [`rebaseTunedModel`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.tuningJobs/rebaseTunedModel)                                   | Rebase a tuned model.                  |
| [`validateReinforcementTuningReward`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.tuningJobs/validateReinforcementTuningReward) | Validates a reward on a given example. |
