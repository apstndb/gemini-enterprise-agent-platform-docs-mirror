---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/list_tuning_jobs
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/list_tuning_jobs
title: 'MCP Tools Reference: aiplatform.googleapis.com'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

## Tool: `list_tuning_jobs`

Lists all GenAI tuning jobs within a specified Google Cloud location. Tuning jobs are used to adapt base models (like Gemini) to perform better on specific tasks by training them on user-provided datasets. Use this tool to monitor the status and progress of various fine-tuning efforts in your project. Format: 'projects/{project_id}/locations/{region}'. CRITICAL: For {region}, use the region specified in the current context window. If no region is specified, prompt the user to provide one. Do not use 'global'.

The following sample demonstrate how to use `curl` to invoke the `list_tuning_jobs` MCP tool.

**Curl Request**

```
curl --location 'https://aiplatform.googleapis.com/mcp/generate' \
--header 'content-type: application/json' \
--header 'accept: application/json, text/event-stream' \
--data '{
  "method": "tools/call",
  "params": {
    "name": "list_tuning_jobs",
    "arguments": {
      // provide these details according to the tool's MCP specification
    }
  },
  "jsonrpc": "2.0",
  "id": 1
}'
```

## Input Schema

Request message for `GenAiTuningService.ListTuningJobs` .

### ListTuningJobsRequest

**JSON representation**

```
{
  "parent": string,
  "filter": string,
  "pageSize": integer,
  "pageToken": string
}
```

| Fields      |                                                                                                                                                                             |
|-------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `parent`    | `string` Required. The resource name of the location to list the tuning jobs from. Format: `projects/{project}/locations/{location}`                                        |
| `filter`    | `string` Optional. The standard list filter.                                                                                                                                |
| `pageSize`  | `integer` Optional. The standard list page size.                                                                                                                            |
| `pageToken` | `string` Optional. The standard list page token. Typically obtained from `ListTuningJobsResponse.next_page_token` of the previous `GenAiTuningService.ListTuningJobs` call. |

## Output Schema

Response message for `GenAiTuningService.ListTuningJobs`

### ListTuningJobsResponse

**JSON representation**

```
{
  "tuningJobs": [
    {
      object (TuningJob)
    }
  ],
  "nextPageToken": string
}
```

| Fields          |                                                                                                                                                                                                        |
|-----------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `tuningJobs[]`  | `object ( `[`TuningJob`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/list_tuning_jobs#Output.Schema.TuningJob)` )` The tuning jobs that match the request. |
| `nextPageToken` | `string` A token to retrieve the next page of results. Pass this token in a subsequent \[GenAiTuningService.ListTuningJobs\] call to retrieve the next page of results.                                |

### TuningJob

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

  // Union field source_model can be only one of the following:
  "baseModel": string,
  "preTunedModel": {
    object (PreTunedModel)
  }
  // End of list of possible types for union field source_model.

  // Union field tuning_spec can be only one of the following:
  "supervisedTuningSpec": {
    object (SupervisedTuningSpec)
  }
  // End of list of possible types for union field tuning_spec.
}
```

| Fields                                                                        |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
|-------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `name`                                                                        | `string` Output only. Identifier. Resource name of a TuningJob. Format: `projects/{project}/locations/{location}/tuningJobs/{tuning_job}`                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| `tunedModelDisplayName`                                                       | `string` Optional. The display name of the [`TunedModel`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/upload_model#Input.Schema.Model) . The name can be up to 128 characters long and can consist of any UTF-8 characters. For continuous tuning, tuned_model_display_name will by default use the same display name as the pre-tuned model. If a new display name is provided, the tuning job will create a new model instead of a new version.                                                                                                                                                                                                                                                                                                                                           |
| `description`                                                                 | `string` Optional. The description of the [`TuningJob`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/list_tuning_jobs#Output.Schema.TuningJob) .                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| `state`                                                                       | `enum ( `[`JobState`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/list_tuning_jobs#Output.Schema.JobState)` )` Output only. The detailed state of the job.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| `createTime`                                                                  | `string ( `[`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp)` format)` Output only. Time when the [`TuningJob`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/list_tuning_jobs#Output.Schema.TuningJob) was created. Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .                                                                                                                                                                                                                                                                           |
| `startTime`                                                                   | `string ( `[`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp)` format)` Output only. Time when the [`TuningJob`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/list_tuning_jobs#Output.Schema.TuningJob) for the first time entered the `JOB_STATE_RUNNING` state. Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .                                                                                                                                                                                                                              |
| `endTime`                                                                     | `string ( `[`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp)` format)` Output only. Time when the TuningJob entered any of the following [`JobStates`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/list_tuning_jobs#Output.Schema.JobState) : `JOB_STATE_SUCCEEDED` , `JOB_STATE_FAILED` , `JOB_STATE_CANCELLED` , `JOB_STATE_EXPIRED` . Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .                                                                                                                                                     |
| `updateTime`                                                                  | `string ( `[`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp)` format)` Output only. Time when the [`TuningJob`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/list_tuning_jobs#Output.Schema.TuningJob) was most recently updated. Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .                                                                                                                                                                                                                                                             |
| `error`                                                                       | `object ( `[`Status`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/create_endpoint#Output.Schema.Status)` )` Output only. Only populated when job's state is `JOB_STATE_FAILED` or `JOB_STATE_CANCELLED` .                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| `labels`                                                                      | `map (key: string, value: string)` Optional. The labels with user-defined metadata to organize [`TuningJob`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/list_tuning_jobs#Output.Schema.TuningJob) and generated resources such as [`Model`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/upload_model#Input.Schema.Model) and `Endpoint` . Label keys and values can be no longer than 64 characters (Unicode codepoints), can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed. See <https://goo.gl/xmQnxf> for more information and examples of labels. An object containing a list of `"key": value` pairs. Example: `{ "name": "wrench", "mass": "1.3kg", "count": "3" }` . |
| `experiment`                                                                  | `string` Output only. The Experiment associated with this [`TuningJob`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/list_tuning_jobs#Output.Schema.TuningJob) .                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| `tunedModel`                                                                  | `object ( `[`TunedModel`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/list_tuning_jobs#Output.Schema.TunedModel)` )` Output only. The tuned model resources associated with this [`TuningJob`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/list_tuning_jobs#Output.Schema.TuningJob) .                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
| `tuningDataStats`                                                             | `object ( `[`TuningDataStats`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/list_tuning_jobs#Output.Schema.TuningDataStats)` )` Output only. The tuning data statistics associated with this [`TuningJob`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/list_tuning_jobs#Output.Schema.TuningJob) .                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| `encryptionSpec`                                                              | `object ( `[`EncryptionSpec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/upload_model#Input.Schema.EncryptionSpec)` )` Customer-managed encryption key options for a TuningJob. If this is set, then all resources created by the TuningJob will be encrypted with the provided encryption key.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| `serviceAccount`                                                              | `string` The service account that the tuningJob workload runs as. If not specified, the Agent Platform Secure Fine-Tuned Service Agent in the project will be used. See <https://cloud.google.com/iam/docs/service-agents#vertex-ai-secure-fine-tuning-service-agent> Users starting the pipeline must have the `iam.serviceAccounts.actAs` permission on this service account.                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
| `evaluateDatasetRuns[]`                                                       | `object ( `[`EvaluateDatasetRun`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/list_tuning_jobs#Output.Schema.EvaluateDatasetRun)` )` Output only. Evaluation runs for the Tuning Job.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| Union field `source_model` . `source_model` can be only one of the following: |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
| `baseModel`                                                                   | `string` The base model that is being tuned. See [Supported models](https://cloud.google.com/vertex-ai/generative-ai/docs/model-reference/tuning#supported_models) .                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| `preTunedModel`                                                               | `object ( `[`PreTunedModel`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/list_tuning_jobs#Output.Schema.PreTunedModel)` )` The pre-tuned model for continuous tuning.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| Union field `tuning_spec` . `tuning_spec` can be only one of the following:   |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
| `supervisedTuningSpec`                                                        | `object ( `[`SupervisedTuningSpec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/list_tuning_jobs#Output.Schema.SupervisedTuningSpec)` )` Tuning Spec for Supervised Fine Tuning.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |

### PreTunedModel

**JSON representation**

```
{
  "tunedModelName": string,
  "checkpointId": string,
  "baseModel": string
}
```

| Fields           |                                                                                                                                                                                                                                                                                                                                                                |
|------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `tunedModelName` | `string` The resource name of the Model. E.g., a model resource name with a specified version id or alias: `projects/{project}/locations/{location}/models/{model}@{version_id}` `projects/{project}/locations/{location}/models/{model}@{alias}` Or, omit the version id to use the default version: `projects/{project}/locations/{location}/models/{model}` |
| `checkpointId`   | `string` Optional. The source checkpoint id. If not specified, the default checkpoint will be used.                                                                                                                                                                                                                                                            |
| `baseModel`      | `string` Output only. The name of the base model this [`PreTunedModel`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/list_tuning_jobs#Output.Schema.PreTunedModel) was tuned from.                                                                                                                                  |

### SupervisedTuningSpec

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

| Fields                     |                                                                                                                                                                                                                                   |
|----------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `trainingDatasetUri`       | `string` Required. Training dataset used for tuning. The dataset can be specified as either a Cloud Storage path to a JSONL file or as the resource name of a Vertex Multimodal Dataset.                                          |
| `validationDatasetUri`     | `string` Optional. Validation dataset used for tuning. The dataset can be specified as either a Cloud Storage path to a JSONL file or as the resource name of a Vertex Multimodal Dataset.                                        |
| `hyperParameters`          | `object ( `[`SupervisedHyperParameters`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/list_tuning_jobs#Output.Schema.SupervisedHyperParameters)` )` Optional. Hyperparameters for SFT. |
| `exportLastCheckpointOnly` | `boolean` Optional. If set to true, disable intermediate checkpoints for SFT and only the last checkpoint will be exported. Otherwise, enable intermediate checkpoints for SFT. Default is false.                                 |
| `evaluationConfig`         | `object ( `[`EvaluationConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/list_tuning_jobs#Output.Schema.EvaluationConfig)` )` Optional. Evaluation Config for Tuning Job.          |

### SupervisedHyperParameters

**JSON representation**

```
{
  "epochCount": string,
  "learningRateMultiplier": number,
  "adapterSize": enum (AdapterSize)
}
```

| Fields                   |                                                                                                                                                                                                     |
|--------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `epochCount`             | `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)` Optional. Number of complete passes the model makes over the entire training dataset during training.        |
| `learningRateMultiplier` | `number` Optional. Multiplier for adjusting the default learning rate. Mutually exclusive with `learning_rate` . This feature is only available for 1P models.                                      |
| `adapterSize`            | `enum ( `[`AdapterSize`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/list_tuning_jobs#Output.Schema.AdapterSize)` )` Optional. Adapter size for tuning. |

### EvaluationConfig

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

| Fields                      |                                                                                                                                                                                                                                                                                                        |
|-----------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `metrics[]`                 | `object ( `[`Metric`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/list_tuning_jobs#Output.Schema.Metric)` )` Required. The metrics used for evaluation.                                                                                                    |
| `outputConfig`              | `object ( `[`OutputConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/list_tuning_jobs#Output.Schema.OutputConfig)` )` Required. Config for evaluation output.                                                                                           |
| `autoraterConfig`           | `object ( `[`AutoraterConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/list_tuning_jobs#Output.Schema.AutoraterConfig)` )` Optional. Autorater config for evaluation.                                                                                  |
| `inferenceGenerationConfig` | `object ( `[`GenerationConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/list_tuning_jobs#Output.Schema.GenerationConfig)` )` Optional. Configuration options for inference generation and outputs. If not set, default generation parameters are used. |

### Metric

**JSON representation**

```
{
  "aggregationMetrics": [
    enum (AggregationMetric)
  ],

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

| Fields                                                                                                                                                                 |                                                                                                                                                                                                                                       |
|------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `aggregationMetrics[]`                                                                                                                                                 | `enum ( `[`AggregationMetric`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/list_tuning_jobs#Output.Schema.AggregationMetric)` )` Optional. The aggregation metrics to use.                |
| Union field `metric_spec` . The spec for the metric. It would be either a pre-defined metric, or a inline metric spec. `metric_spec` can be only one of the following: |                                                                                                                                                                                                                                       |
| `predefinedMetricSpec`                                                                                                                                                 | `object ( `[`PredefinedMetricSpec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/list_tuning_jobs#Output.Schema.PredefinedMetricSpec)` )` The spec for a pre-defined metric.               |
| `computationBasedMetricSpec`                                                                                                                                           | `object ( `[`ComputationBasedMetricSpec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/list_tuning_jobs#Output.Schema.ComputationBasedMetricSpec)` )` Spec for a computation based metric. |
| `llmBasedMetricSpec`                                                                                                                                                   | `object ( `[`LLMBasedMetricSpec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/list_tuning_jobs#Output.Schema.LLMBasedMetricSpec)` )` Spec for an LLM based metric.                        |
| `pointwiseMetricSpec`                                                                                                                                                  | `object ( `[`PointwiseMetricSpec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/list_tuning_jobs#Output.Schema.PointwiseMetricSpec)` )` Spec for pointwise metric.                         |
| `pairwiseMetricSpec`                                                                                                                                                   | `object ( `[`PairwiseMetricSpec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/list_tuning_jobs#Output.Schema.PairwiseMetricSpec)` )` Spec for pairwise metric.                            |
| `exactMatchSpec`                                                                                                                                                       | `object ( ``ExactMatchSpec`` )` Spec for exact match metric.                                                                                                                                                                          |
| `bleuSpec`                                                                                                                                                             | `object ( `[`BleuSpec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/list_tuning_jobs#Output.Schema.BleuSpec)` )` Spec for bleu metric.                                                    |
| `rougeSpec`                                                                                                                                                            | `object ( `[`RougeSpec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/list_tuning_jobs#Output.Schema.RougeSpec)` )` Spec for rouge metric.                                                 |

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

| Fields                                                                      |                                                                                                                                                                                                                                                    |
|-----------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Union field `_type` . `_type` can be only one of the following:             |                                                                                                                                                                                                                                                    |
| `type`                                                                      | `enum ( `[`ComputationBasedMetricType`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/list_tuning_jobs#Output.Schema.ComputationBasedMetricType)` )` Required. The type of the computation based metric. |
| Union field `_parameters` . `_parameters` can be only one of the following: |                                                                                                                                                                                                                                                    |
| `parameters`                                                                | `object ( `[`Struct`](https://protobuf.dev/reference/protobuf/google.protobuf/#struct)` format)` Optional. A map of parameters for the metric, e.g. {"rouge_type": "rougeL"}.                                                                      |

### LLMBasedMetricSpec

**JSON representation**

```
{
  "resultParserConfig": {
    object (EvaluationParserConfig)
  },

  // Union field rubrics_source can be only one of the following:
  "rubricGroupKey": string,
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

| Fields                                                                                                                             |                                                                                                                                                                                                                                             |
|------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `resultParserConfig`                                                                                                               | `object ( `[`EvaluationParserConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/list_tuning_jobs#Output.Schema.EvaluationParserConfig)` )` Optional. The parser config for the metric result. |
| Union field `rubrics_source` . Source of the rubrics to be used for evaluation. `rubrics_source` can be only one of the following: |                                                                                                                                                                                                                                             |
| `rubricGroupKey`                                                                                                                   | `string` Use a pre-defined group of rubrics associated with the input. Refers to a key in the rubric_groups map of EvaluationInstance.                                                                                                      |
| `predefinedRubricGenerationSpec`                                                                                                   | `object ( `[`PredefinedMetricSpec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/list_tuning_jobs#Output.Schema.PredefinedMetricSpec)` )` Dynamically generate rubrics using a predefined spec.  |
| Union field `_metric_prompt_template` . `_metric_prompt_template` can be only one of the following:                                |                                                                                                                                                                                                                                             |
| `metricPromptTemplate`                                                                                                             | `string` Required. Template for the prompt sent to the judge model.                                                                                                                                                                         |
| Union field `_system_instruction` . `_system_instruction` can be only one of the following:                                        |                                                                                                                                                                                                                                             |
| `systemInstruction`                                                                                                                | `string` Optional. System instructions for the judge model.                                                                                                                                                                                 |
| Union field `_judge_autorater_config` . `_judge_autorater_config` can be only one of the following:                                |                                                                                                                                                                                                                                             |
| `judgeAutoraterConfig`                                                                                                             | `object ( `[`AutoraterConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/list_tuning_jobs#Output.Schema.AutoraterConfig)` )` Optional. Optional configuration for the judge LLM (Autorater).  |
| Union field `_additional_config` . `_additional_config` can be only one of the following:                                          |                                                                                                                                                                                                                                             |
| `additionalConfig`                                                                                                                 | `object ( `[`Struct`](https://protobuf.dev/reference/protobuf/google.protobuf/#struct)` format)` Optional. Optional additional configuration for the metric.                                                                                |

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
| `generationConfig`                                                                  | `object ( `[`GenerationConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/list_tuning_jobs#Output.Schema.GenerationConfig)` )` Optional. Configuration options for model generation and outputs.                                                                                                                                                                                |
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
<td><p><code>enum ( </code><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/list_tuning_jobs#Output.Schema.Modality"><code>Modality</code></a><code> )</code></p>
<p>Optional. The modalities of the response. The model will generate a response that includes all the specified modalities. For example, if this is set to <code>[TEXT, IMAGE]</code> , the response will include both text and an image.</p></td>
</tr>
<tr class="even">
<td><code>thinkingConfig</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/list_tuning_jobs#Output.Schema.ThinkingConfig"><code>ThinkingConfig</code></a><code> )</code></p>
<p>Optional. Configuration for thinking features. An error will be returned if this field is set for models that don't support thinking.</p></td>
</tr>
<tr class="odd">
<td><code>responseFormat[]</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/list_tuning_jobs#Output.Schema.ResponseFormat"><code>ResponseFormat</code></a><code> )</code></p>
<p>Optional. New response format field for the model to configure output formatting and delivery.</p></td>
</tr>
<tr class="even">
<td><p>Union field <code>_temperature</code> .</p>
<p><code>_temperature</code> can be only one of the following:</p></td>
<td></td>
</tr>
<tr class="odd">
<td><code>temperature</code></td>
<td><p><code>number</code></p>
<p>Optional. Controls the randomness of the output. A higher temperature results in more creative and diverse responses, while a lower temperature makes the output more predictable and focused. The valid range is (0.0, 2.0].</p></td>
</tr>
<tr class="even">
<td><p>Union field <code>_top_p</code> .</p>
<p><code>_top_p</code> can be only one of the following:</p></td>
<td></td>
</tr>
<tr class="odd">
<td><code>topP</code></td>
<td><p><code>number</code></p>
<p>Optional. Specifies the nucleus sampling threshold. The model considers only the smallest set of tokens whose cumulative probability is at least <code>top_p</code> . This helps generate more diverse and less repetitive responses. For example, a <code>top_p</code> of 0.9 means the model considers tokens until the cumulative probability of the tokens to select from reaches 0.9. It's recommended to adjust either temperature or <code>top_p</code> , but not both.</p></td>
</tr>
<tr class="even">
<td><p>Union field <code>_top_k</code> .</p>
<p><code>_top_k</code> can be only one of the following:</p></td>
<td></td>
</tr>
<tr class="odd">
<td><code>topK</code></td>
<td><p><code>number</code></p>
<p>Optional. Specifies the top-k sampling threshold. The model considers only the top k most probable tokens for the next token. This can be useful for generating more coherent and less random text. For example, a <code>top_k</code> of 40 means the model will choose the next word from the 40 most likely words.</p></td>
</tr>
<tr class="even">
<td><p>Union field <code>_candidate_count</code> .</p>
<p><code>_candidate_count</code> can be only one of the following:</p></td>
<td></td>
</tr>
<tr class="odd">
<td><code>candidateCount</code></td>
<td><p><code>integer</code></p>
<p>Optional. The number of candidate responses to generate.</p>
<p>A higher <code>candidate_count</code> can provide more options to choose from, but it also consumes more resources. This can be useful for generating a variety of responses and selecting the best one.</p></td>
</tr>
<tr class="even">
<td><p>Union field <code>_max_output_tokens</code> .</p>
<p><code>_max_output_tokens</code> can be only one of the following:</p></td>
<td></td>
</tr>
<tr class="odd">
<td><code>maxOutputTokens</code></td>
<td><p><code>integer</code></p>
<p>Optional. The maximum number of tokens to generate in the response.</p>
<p>A token is approximately four characters. The default value varies by model. This parameter can be used to control the length of the generated text and prevent overly long responses.</p></td>
</tr>
<tr class="even">
<td><p>Union field <code>_response_logprobs</code> .</p>
<p><code>_response_logprobs</code> can be only one of the following:</p></td>
<td></td>
</tr>
<tr class="odd">
<td><code>responseLogprobs</code></td>
<td><p><code>boolean</code></p>
<p>Optional. If set to true, the log probabilities of the output tokens are returned.</p>
<p>Log probabilities are the logarithm of the probability of a token appearing in the output. A higher log probability means the token is more likely to be generated. This can be useful for analyzing the model's confidence in its own output and for debugging.</p></td>
</tr>
<tr class="even">
<td><p>Union field <code>_logprobs</code> .</p>
<p><code>_logprobs</code> can be only one of the following:</p></td>
<td></td>
</tr>
<tr class="odd">
<td><code>logprobs</code></td>
<td><p><code>integer</code></p>
<p>Optional. The number of top log probabilities to return for each token.</p>
<p>This can be used to see which other tokens were considered likely candidates for a given position. A higher value will return more options, but it will also increase the size of the response.</p></td>
</tr>
<tr class="even">
<td><p>Union field <code>_presence_penalty</code> .</p>
<p><code>_presence_penalty</code> can be only one of the following:</p></td>
<td></td>
</tr>
<tr class="odd">
<td><code>presencePenalty</code></td>
<td><p><code>number</code></p>
<p>Optional. Penalizes tokens that have already appeared in the generated text. A positive value encourages the model to generate more diverse and less repetitive text. Valid values can range from [-2.0, 2.0].</p></td>
</tr>
<tr class="even">
<td><p>Union field <code>_frequency_penalty</code> .</p>
<p><code>_frequency_penalty</code> can be only one of the following:</p></td>
<td></td>
</tr>
<tr class="odd">
<td><code>frequencyPenalty</code></td>
<td><p><code>number</code></p>
<p>Optional. Penalizes tokens based on their frequency in the generated text. A positive value helps to reduce the repetition of words and phrases. Valid values can range from [-2.0, 2.0].</p></td>
</tr>
<tr class="even">
<td><p>Union field <code>_seed</code> .</p>
<p><code>_seed</code> can be only one of the following:</p></td>
<td></td>
</tr>
<tr class="odd">
<td><code>seed</code></td>
<td><p><code>integer</code></p>
<p>Optional. A seed for the random number generator.</p>
<p>By setting a seed, you can make the model's output mostly deterministic. For a given prompt and parameters (like temperature, top_p, etc.), the model will produce the same response every time. However, it's not a guaranteed absolute deterministic behavior. This is different from parameters like <code>temperature</code> , which control the <em>level</em> of randomness. <code>seed</code> ensures that the "random" choices the model makes are the same on every run, making it essential for testing and ensuring reproducible results.</p></td>
</tr>
<tr class="even">
<td><p>Union field <code>_response_schema</code> .</p>
<p><code>_response_schema</code> can be only one of the following:</p></td>
<td></td>
</tr>
<tr class="odd">
<td><code>responseSchema </code><strong><code>(deprecated)</code></strong></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/list_tuning_jobs#Output.Schema.Schema"><code>Schema</code></a><code> )</code></p>
<blockquote>
<p>This item is deprecated!</p>
</blockquote>
<p>Optional. Lets you to specify a schema for the model's response, ensuring that the output conforms to a particular structure. This is useful for generating structured data such as JSON. The schema is a subset of the <a href="https://spec.openapis.org/oas/v3.0.3#schema">OpenAPI 3.0 schema object</a> object.</p>
<p>When this field is set, you must also set the <code>response_mime_type</code> to <code>application/json</code> . Deprecated: Use <code>response_format</code> instead.</p></td>
</tr>
<tr class="even">
<td><p>Union field <code>_response_json_schema</code> .</p>
<p><code>_response_json_schema</code> can be only one of the following:</p></td>
<td></td>
</tr>
<tr class="odd">
<td><code>responseJsonSchema </code><strong><code>(deprecated)</code></strong></td>
<td><p><code>value ( </code><a href="https://protobuf.dev/reference/protobuf/google.protobuf/#value"><code>Value</code></a><code> format)</code></p>
<blockquote>
<p>This item is deprecated!</p>
</blockquote>
<p>Optional. When this field is set, <code>response_schema</code> must be omitted and <code>response_mime_type</code> must be set to <code>application/json</code> . Deprecated: Use <code>response_format</code> instead.</p></td>
</tr>
<tr class="even">
<td><p>Union field <code>_routing_config</code> .</p>
<p><code>_routing_config</code> can be only one of the following:</p></td>
<td></td>
</tr>
<tr class="odd">
<td><code>routingConfig</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/list_tuning_jobs#Output.Schema.RoutingConfig"><code>RoutingConfig</code></a><code> )</code></p>
<p>Optional. Routing configuration.</p></td>
</tr>
<tr class="even">
<td><p>Union field <code>_audio_timestamp</code> .</p>
<p><code>_audio_timestamp</code> can be only one of the following:</p></td>
<td></td>
</tr>
<tr class="odd">
<td><code>audioTimestamp</code></td>
<td><p><code>boolean</code></p>
<p>Optional. If enabled, audio timestamps will be included in the request to the model. This can be useful for synchronizing audio with other modalities in the response.</p></td>
</tr>
<tr class="even">
<td><p>Union field <code>_media_resolution</code> .</p>
<p><code>_media_resolution</code> can be only one of the following:</p></td>
<td></td>
</tr>
<tr class="odd">
<td><code>mediaResolution</code></td>
<td><p><code>enum ( </code><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/list_tuning_jobs#Output.Schema.MediaResolution_1"><code>MediaResolution</code></a><code> )</code></p>
<p>Optional. The token resolution at which input media content is sampled. This is used to control the trade-off between the quality of the response and the number of tokens used to represent the media. A higher resolution allows the model to perceive more detail, which can lead to a more nuanced response, but it will also use more tokens. This does not affect the image dimensions sent to the model.</p></td>
</tr>
<tr class="even">
<td><p>Union field <code>_speech_config</code> .</p>
<p><code>_speech_config</code> can be only one of the following:</p></td>
<td></td>
</tr>
<tr class="odd">
<td><code>speechConfig</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/list_tuning_jobs#Output.Schema.SpeechConfig"><code>SpeechConfig</code></a><code> )</code></p>
<p>Optional. The speech generation config.</p></td>
</tr>
<tr class="even">
<td><p>Union field <code>_enable_affective_dialog</code> .</p>
<p><code>_enable_affective_dialog</code> can be only one of the following:</p></td>
<td></td>
</tr>
<tr class="odd">
<td><code>enableAffectiveDialog</code></td>
<td><p><code>boolean</code></p>
<p>Optional. If enabled, the model will detect emotions and adapt its responses accordingly. For example, if the model detects that the user is frustrated, it may provide a more empathetic response.</p></td>
</tr>
<tr class="even">
<td><p>Union field <code>_image_config</code> .</p>
<p><code>_image_config</code> can be only one of the following:</p></td>
<td></td>
</tr>
<tr class="odd">
<td><code>imageConfig </code><strong><code>(deprecated)</code></strong></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/list_tuning_jobs#Output.Schema.ImageConfig"><code>ImageConfig</code></a><code> )</code></p>
<blockquote>
<p>This item is deprecated!</p>
</blockquote>
<p>Optional. Config for image generation features. Deprecated: Use <code>response_format.image</code> instead.</p></td>
</tr>
<tr class="even">
<td><p>Union field <code>_audio_transcription_config</code> .</p>
<p><code>_audio_transcription_config</code> can be only one of the following:</p></td>
<td></td>
</tr>
<tr class="odd">
<td><code>audioTranscriptionConfig</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/list_tuning_jobs#Output.Schema.AudioTranscriptionConfig"><code>AudioTranscriptionConfig</code></a><code> )</code></p>
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
| `type`                 | `enum ( `[`Type`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/list_tuning_jobs#Output.Schema.Type)` )` Optional. Data type of the schema field.                                                                                                                                                                                                                                                                                                                         |
| `format`               | `string` Optional. The format of the data. For `NUMBER` type, format can be `float` or `double` . For `INTEGER` type, format can be `int32` or `int64` . For `STRING` type, format can be `email` , `byte` , `date` , `date-time` , `password` , and other formats to further refine the data type.                                                                                                                                                                                                                 |
| `title`                | `string` Optional. Title for the schema.                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| `description`          | `string` Optional. Describes the data. The model uses this field to understand the purpose of the schema and how to use it. It is a best practice to provide a clear and descriptive explanation for the schema and its properties here, rather than in the prompt.                                                                                                                                                                                                                                                 |
| `nullable`             | `boolean` Optional. Indicates if the value of this field can be null.                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| `default`              | `value ( `[`Value`](https://protobuf.dev/reference/protobuf/google.protobuf/#value)` format)` Optional. Default value to use if the field is not specified.                                                                                                                                                                                                                                                                                                                                                         |
| `items`                | `object ( `[`Schema`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/list_tuning_jobs#Output.Schema.Schema)` )` Optional. If type is `ARRAY` , `items` specifies the schema of elements in the array.                                                                                                                                                                                                                                                                      |
| `minItems`             | `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)` Optional. If type is `ARRAY` , `min_items` specifies the minimum number of items in an array.                                                                                                                                                                                                                                                                                                                                |
| `maxItems`             | `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)` Optional. If type is `ARRAY` , `max_items` specifies the maximum number of items in an array.                                                                                                                                                                                                                                                                                                                                |
| `enum[]`               | `string` Optional. Possible values of the field. This field can be used to restrict a value to a fixed set of values. To mark a field as an enum, set `format` to `enum` and provide the list of possible values in `enum` . For example: 1. To define directions: `{type:STRING, format:enum, enum:["EAST", "NORTH", "SOUTH", "WEST"]}` 2. To define apartment numbers: `{type:INTEGER, format:enum, enum:["101", "201", "301"]}`                                                                                  |
| `properties`           | `map (key: string, value: object ( `[`Schema`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/list_tuning_jobs#Output.Schema.Schema)` ))` Optional. If type is `OBJECT` , `properties` is a map of property names to schema definitions for each property of the object. An object containing a list of `"key": value` pairs. Example: `{ "name": "wrench", "mass": "1.3kg", "count": "3" }` .                                                                             |
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
| `anyOf[]`              | `object ( `[`Schema`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/list_tuning_jobs#Output.Schema.Schema)` )` Optional. The instance must be valid against any (one or more) of the subschemas listed in `any_of` .                                                                                                                                                                                                                                                      |
| `additionalProperties` | `value ( `[`Value`](https://protobuf.dev/reference/protobuf/google.protobuf/#value)` format)` Optional. If `type` is `OBJECT` , specifies how to handle properties not defined in `properties` . If it is a boolean `false` , no additional properties are allowed. If it is a schema, additional properties are allowed if they conform to the schema.                                                                                                                                                             |
| `ref`                  | `string` Optional. Allows referencing another schema definition to use in place of this schema. The value must be a valid reference to a schema in `defs` . For example, the following schema defines a reference to a schema node named "Pet": type: object properties: pet: ref: \#/defs/Pet defs: Pet: type: object properties: name: type: string The value of the "pet" property is a reference to the schema node named "Pet". See details in <https://json-schema.org/understanding-json-schema/structuring> |
| `defs`                 | `map (key: string, value: object ( `[`Schema`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/list_tuning_jobs#Output.Schema.Schema)` ))` Optional. `defs` provides a map of schema definitions that can be reused by `ref` elsewhere in the schema. Only allowed at root level of the schema. An object containing a list of `"key": value` pairs. Example: `{ "name": "wrench", "mass": "1.3kg", "count": "3" }` .                                                       |

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

| Fields  |                                                                                                                                                          |
|---------|----------------------------------------------------------------------------------------------------------------------------------------------------------|
| `key`   | `string`                                                                                                                                                 |
| `value` | `object ( `[`Schema`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/list_tuning_jobs#Output.Schema.Schema)` )` |

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

| Fields  |                                                                                                                                                          |
|---------|----------------------------------------------------------------------------------------------------------------------------------------------------------|
| `key`   | `string`                                                                                                                                                 |
| `value` | `object ( `[`Schema`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/list_tuning_jobs#Output.Schema.Schema)` )` |

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

| Fields                                                                                                              |                                                                                                                                                                                                                                                                   |
|---------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Union field `routing_config` . The routing mode for the request. `routing_config` can be only one of the following: |                                                                                                                                                                                                                                                                   |
| `autoMode`                                                                                                          | `object ( `[`AutoRoutingMode`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/list_tuning_jobs#Output.Schema.AutoRoutingMode)` )` In this mode, the model is selected automatically based on the content of the request. |
| `manualMode`                                                                                                        | `object ( `[`ManualRoutingMode`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/list_tuning_jobs#Output.Schema.ManualRoutingMode)` )` In this mode, the model is specified manually.                                     |

### AutoRoutingMode

**JSON representation**

```
{

  // Union field _model_routing_preference can be only one of the following:
  "modelRoutingPreference": enum (ModelRoutingPreference)
  // End of list of possible types for union field _model_routing_preference.
}
```

| Fields                                                                                                  |                                                                                                                                                                                                                      |
|---------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Union field `_model_routing_preference` . `_model_routing_preference` can be only one of the following: |                                                                                                                                                                                                                      |
| `modelRoutingPreference`                                                                                | `enum ( `[`ModelRoutingPreference`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/list_tuning_jobs#Output.Schema.ModelRoutingPreference)` )` The model routing preference. |

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

| Fields                    |                                                                                                                                                                                                                                                                                                                 |
|---------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `voiceConfig`             | `object ( `[`VoiceConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/list_tuning_jobs#Output.Schema.VoiceConfig)` )` The configuration for the voice to use.                                                                                                      |
| `languageCode`            | `string` Optional. The language code (ISO 639-1) for the speech synthesis.                                                                                                                                                                                                                                      |
| `multiSpeakerVoiceConfig` | `object ( `[`MultiSpeakerVoiceConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/list_tuning_jobs#Output.Schema.MultiSpeakerVoiceConfig)` )` The configuration for a multi-speaker text-to-speech request. This field is mutually exclusive with `voice_config` . |

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

| Fields                                                                                                                  |                                                                                                                                                                                                                                                                                                          |
|-------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Union field `voice_config` . The configuration for the speaker to use. `voice_config` can be only one of the following: |                                                                                                                                                                                                                                                                                                          |
| `prebuiltVoiceConfig`                                                                                                   | `object ( `[`PrebuiltVoiceConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/list_tuning_jobs#Output.Schema.PrebuiltVoiceConfig)` )` The configuration for a prebuilt voice.                                                                               |
| `replicatedVoiceConfig`                                                                                                 | `object ( `[`ReplicatedVoiceConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/list_tuning_jobs#Output.Schema.ReplicatedVoiceConfig)` )` Optional. The configuration for a replicated voice. This enables users to replicate a voice from an audio sample. |

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

| Fields                  |                                                                                                                                                                                                                                                                                                                |
|-------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `speakerVoiceConfigs[]` | `object ( `[`SpeakerVoiceConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/list_tuning_jobs#Output.Schema.SpeakerVoiceConfig)` )` Required. A list of configurations for the voices of the speakers. Exactly two speaker voice configurations must be provided. |

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

| Fields        |                                                                                                                                                                                                                               |
|---------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `speaker`     | `string` Required. The name of the speaker. This should be the same as the speaker name used in the prompt.                                                                                                                   |
| `voiceConfig` | `object ( `[`VoiceConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/list_tuning_jobs#Output.Schema.VoiceConfig)` )` Required. The configuration for the voice of this speaker. |

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
| `thinkingLevel`                                                                         | `enum ( `[`ThinkingLevel`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/list_tuning_jobs#Output.Schema.ThinkingLevel)` )` Optional. The number of thoughts tokens that the model should generate.                                                                               |

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

| Fields                                                                                          |                                                                                                                                                                                                                                          |
|-------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Union field `_image_output_options` . `_image_output_options` can be only one of the following: |                                                                                                                                                                                                                                          |
| `imageOutputOptions`                                                                            | `object ( `[`ImageOutputOptions`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/list_tuning_jobs#Output.Schema.ImageOutputOptions)` )` Optional. The image output format for generated images. |
| Union field `_aspect_ratio` . `_aspect_ratio` can be only one of the following:                 |                                                                                                                                                                                                                                          |
| `aspectRatio`                                                                                   | `string` Optional. The desired aspect ratio for the generated images. The following aspect ratios are supported: "1:1" "2:3", "3:2" "3:4", "4:3" "4:5", "5:4" "9:16", "16:9" "21:9"                                                      |
| Union field `_person_generation` . `_person_generation` can be only one of the following:       |                                                                                                                                                                                                                                          |
| `personGeneration`                                                                              | `enum ( `[`PersonGeneration`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/list_tuning_jobs#Output.Schema.PersonGeneration)` )` Optional. Controls whether the model can generate people.     |
| Union field `_image_size` . `_image_size` can be only one of the following:                     |                                                                                                                                                                                                                                          |
| `imageSize`                                                                                     | `string` Optional. Specifies the size of generated images. Supported values are `1K` , `2K` , `4K` . If not specified, the model will use default value `1K` .                                                                           |

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

| Fields                                                                                              |                                                                                                                                                                                                         |
|-----------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Union field `format` . The format of the output content. `format` can be only one of the following: |                                                                                                                                                                                                         |
| `text`                                                                                              | `object ( `[`TextResponseFormat`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/list_tuning_jobs#Output.Schema.TextResponseFormat)` )` Text output format.    |
| `audio`                                                                                             | `object ( `[`AudioResponseFormat`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/list_tuning_jobs#Output.Schema.AudioResponseFormat)` )` Audio output format. |
| `image`                                                                                             | `object ( `[`ImageResponseFormat`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/list_tuning_jobs#Output.Schema.ImageResponseFormat)` )` Image output format. |
| `video`                                                                                             | `object ( `[`VideoResponseFormat`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/list_tuning_jobs#Output.Schema.VideoResponseFormat)` )` Video output format. |

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

| Fields                                                                    |                                                                                                                                                                                                                   |
|---------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Union field `_mime_type` . `_mime_type` can be only one of the following: |                                                                                                                                                                                                                   |
| `mimeType`                                                                | `enum ( `[`MimeType`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/list_tuning_jobs#Output.Schema.MimeType)` )` Optional. The IANA standard MIME type of the response. |
| Union field `_schema` . `_schema` can be only one of the following:       |                                                                                                                                                                                                                   |
| `schema`                                                                  | `value ( `[`Value`](https://protobuf.dev/reference/protobuf/google.protobuf/#value)` format)` Optional. The JSON schema that the output should conform to. Only applicable when mime_type is APPLICATION_JSON.    |

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

| Fields                                                                        |                                                                                                                                                                                                                       |
|-------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `delivery`                                                                    | `enum ( `[`DeliveryMode`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/list_tuning_jobs#Output.Schema.DeliveryMode)` )` Optional. Delivery mode for the generated content. |
| Union field `_mime_type` . `_mime_type` can be only one of the following:     |                                                                                                                                                                                                                       |
| `mimeType`                                                                    | `enum ( `[`MimeType`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/list_tuning_jobs#Output.Schema.MimeType_1)` )` Optional. The MIME type of the audio output.             |
| Union field `_sample_rate` . `_sample_rate` can be only one of the following: |                                                                                                                                                                                                                       |
| `sampleRate`                                                                  | `integer` Optional. Sample rate for the generated audio in Hertz.                                                                                                                                                     |
| Union field `_bit_rate` . `_bit_rate` can be only one of the following:       |                                                                                                                                                                                                                       |
| `bitRate`                                                                     | `integer` Optional. Bit rate in bits per second (bps). Only applicable for compressed formats (MP3, Opus).                                                                                                            |

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

| Fields                                                                          |                                                                                                                                                                                                                       |
|---------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `delivery`                                                                      | `enum ( `[`DeliveryMode`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/list_tuning_jobs#Output.Schema.DeliveryMode)` )` Optional. Delivery mode for the generated content. |
| Union field `_mime_type` . `_mime_type` can be only one of the following:       |                                                                                                                                                                                                                       |
| `mimeType`                                                                      | `enum ( `[`MimeType`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/list_tuning_jobs#Output.Schema.MimeType_2)` )` Optional. The MIME type of the image output.             |
| Union field `_aspect_ratio` . `_aspect_ratio` can be only one of the following: |                                                                                                                                                                                                                       |
| `aspectRatio`                                                                   | `enum ( `[`AspectRatio`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/list_tuning_jobs#Output.Schema.AspectRatio)` )` Optional. The aspect ratio for the image output.     |
| Union field `_image_size` . `_image_size` can be only one of the following:     |                                                                                                                                                                                                                       |
| `imageSize`                                                                     | `enum ( `[`ImageSize`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/list_tuning_jobs#Output.Schema.ImageSize)` )` Optional. The size of the image output.                  |

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
| `delivery`                                                              | `enum ( `[`DeliveryMode`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/list_tuning_jobs#Output.Schema.DeliveryMode)` )` Optional. Delivery mode for the generated content.                               |
| `gcsUri`                                                                | `string` Optional. The Google Cloud Storage URI to store the video output. Required for Vertex if delivery is URI.                                                                                                                                  |
| `aspectRatio`                                                           | `enum ( `[`AspectRatio`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/list_tuning_jobs#Output.Schema.AspectRatio_1)` )` The aspect ratio for the video output.                                           |
| Union field `_duration` . `_duration` can be only one of the following: |                                                                                                                                                                                                                                                     |
| `duration`                                                              | `string ( `[`Duration`](https://protobuf.dev/reference/protobuf/google.protobuf/#duration)` format)` Optional. The duration for the video output. A duration in seconds with up to nine fractional digits, ending with ' `s` '. Example: `"3.5s"` . |

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
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/list_tuning_jobs#Output.Schema.LanguageHints"><code>LanguageHints</code></a><code> )</code></p>
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

| Fields                                                            |                                                                                                                                                                                                                                               |
|-------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Union field `parser` . `parser` can be only one of the following: |                                                                                                                                                                                                                                               |
| `customCodeParserConfig`                                          | `object ( `[`CustomCodeParserConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/list_tuning_jobs#Output.Schema.CustomCodeParserConfig)` )` Optional. Use custom code to parse the LLM response. |

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

| Fields                                                                                              |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
|-----------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `customOutputFormatConfig`                                                                          | `object ( `[`CustomOutputFormatConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/list_tuning_jobs#Output.Schema.CustomOutputFormatConfig)` )` Optional. CustomOutputFormatConfig allows customization of metric output. By default, metrics return a score and explanation. When this config is set, the default output is replaced with either: - The raw output string. - A parsed output based on a user-defined schema. If a custom format is chosen, the `score` and `explanation` fields in the corresponding metric result will be empty. |
| Union field `_metric_prompt_template` . `_metric_prompt_template` can be only one of the following: |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| `metricPromptTemplate`                                                                              | `string` Required. Metric prompt template for pointwise metric.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| Union field `_system_instruction` . `_system_instruction` can be only one of the following:         |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| `systemInstruction`                                                                                 | `string` Optional. System instructions for pointwise metric.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |

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

| Fields                                                                                              |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
|-----------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `candidateResponseFieldName`                                                                        | `string` Optional. The field name of the candidate response.                                                                                                                                                                                                                                                                                                                                                                                                                              |
| `baselineResponseFieldName`                                                                         | `string` Optional. The field name of the baseline response.                                                                                                                                                                                                                                                                                                                                                                                                                               |
| `customOutputFormatConfig`                                                                          | `object ( `[`CustomOutputFormatConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/list_tuning_jobs#Output.Schema.CustomOutputFormatConfig)` )` Optional. CustomOutputFormatConfig allows customization of metric output. When this config is set, the default output is replaced with the raw output string. If a custom format is chosen, the `pairwise_choice` and `explanation` fields in the corresponding metric result will be empty. |
| Union field `_metric_prompt_template` . `_metric_prompt_template` can be only one of the following: |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| `metricPromptTemplate`                                                                              | `string` Required. Metric prompt template for pairwise metric.                                                                                                                                                                                                                                                                                                                                                                                                                            |
| Union field `_system_instruction` . `_system_instruction` can be only one of the following:         |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| `systemInstruction`                                                                                 | `string` Optional. System instructions for pairwise metric.                                                                                                                                                                                                                                                                                                                                                                                                                               |

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

### OutputConfig

**JSON representation**

```
{

  // Union field destination can be only one of the following:
  "gcsDestination": {
    object (GcsDestination)
  }
  // End of list of possible types for union field destination.
}
```

| Fields                                                                                                             |                                                                                                                                                                                                                           |
|--------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Union field `destination` . The destination for evaluation output. `destination` can be only one of the following: |                                                                                                                                                                                                                           |
| `gcsDestination`                                                                                                   | `object ( `[`GcsDestination`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/list_tuning_jobs#Output.Schema.GcsDestination)` )` Cloud storage destination for evaluation output. |

### GcsDestination

**JSON representation**

```
{
  "outputUriPrefix": string
}
```

| Fields            |                                                                                                                                                                                       |
|-------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `outputUriPrefix` | `string` Required. Google Cloud Storage URI to output directory. If the uri doesn't end with '/', a '/' will be automatically appended. The directory is created if it doesn't exist. |

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

### LabelsEntry

**JSON representation**

```
{
  "key": string,
  "value": string
}
```

| Fields  |          |
|---------|----------|
| `key`   | `string` |
| `value` | `string` |

### TunedModel

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

| Fields          |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
|-----------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `model`         | `string` Output only. The resource name of the TunedModel. Format: `projects/{project}/locations/{location}/models/{model}@{version_id}` When tuning from a base model, the version ID will be 1. For continuous tuning, if the provided tuned_model_display_name is set and different from parent model's display name, the tuned model will have a new parent model with version 1. Otherwise the version id will be incremented by 1 from the last version ID in the parent model. E.g., `projects/{project}/locations/{location}/models/{model}@{last_version_id + 1}` |
| `endpoint`      | `string` Output only. A resource name of an Endpoint. Format: `projects/{project}/locations/{location}/endpoints/{endpoint}` .                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| `checkpoints[]` | `object ( `[`TunedModelCheckpoint`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/list_tuning_jobs#Output.Schema.TunedModelCheckpoint)` )` Output only. The checkpoints associated with this TunedModel. This field is only populated for tuning jobs that enable intermediate checkpoints.                                                                                                                                                                                                                                      |

### TunedModelCheckpoint

**JSON representation**

```
{
  "checkpointId": string,
  "epoch": string,
  "step": string,
  "endpoint": string
}
```

| Fields         |                                                                                                                                                  |
|----------------|--------------------------------------------------------------------------------------------------------------------------------------------------|
| `checkpointId` | `string` The ID of the checkpoint.                                                                                                               |
| `epoch`        | `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)` The epoch of the checkpoint.                              |
| `step`         | `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)` The step of the checkpoint.                               |
| `endpoint`     | `string` The Endpoint resource name that the checkpoint is deployed to. Format: `projects/{project}/locations/{location}/endpoints/{endpoint}` . |

### TuningDataStats

**JSON representation**

```
{

  // Union field tuning_data_stats can be only one of the following:
  "supervisedTuningDataStats": {
    object (SupervisedTuningDataStats)
  }
  // End of list of possible types for union field tuning_data_stats.
}
```

| Fields                                                                                  |                                                                                                                                                                                                                           |
|-----------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Union field `tuning_data_stats` . `tuning_data_stats` can be only one of the following: |                                                                                                                                                                                                                           |
| `supervisedTuningDataStats`                                                             | `object ( `[`SupervisedTuningDataStats`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/list_tuning_jobs#Output.Schema.SupervisedTuningDataStats)` )` The SFT Tuning data stats. |

### SupervisedTuningDataStats

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
<td><code>tuningDatasetExampleCount</code></td>
<td><p><code>string ( </code><a href="https://developers.google.com/discovery/v1/type-format"><code>int64</code></a><code> format)</code></p>
<p>Output only. Number of examples in the tuning dataset.</p></td>
</tr>
<tr class="even">
<td><code>totalTuningCharacterCount</code></td>
<td><p><code>string ( </code><a href="https://developers.google.com/discovery/v1/type-format"><code>int64</code></a><code> format)</code></p>
<p>Output only. Number of tuning characters in the tuning dataset.</p></td>
</tr>
<tr class="odd">
<td><code>totalBillableCharacterCount </code><strong><code>(deprecated)</code></strong></td>
<td><p><code>string ( </code><a href="https://developers.google.com/discovery/v1/type-format"><code>int64</code></a><code> format)</code></p>
<blockquote>
<p>This item is deprecated!</p>
</blockquote>
<p>Output only. Number of billable characters in the tuning dataset.</p></td>
</tr>
<tr class="even">
<td><code>totalBillableTokenCount</code></td>
<td><p><code>string ( </code><a href="https://developers.google.com/discovery/v1/type-format"><code>int64</code></a><code> format)</code></p>
<p>Output only. Number of billable tokens in the tuning dataset.</p></td>
</tr>
<tr class="odd">
<td><code>tuningStepCount</code></td>
<td><p><code>string ( </code><a href="https://developers.google.com/discovery/v1/type-format"><code>int64</code></a><code> format)</code></p>
<p>Output only. Number of tuning steps for this Tuning Job.</p></td>
</tr>
<tr class="even">
<td><code>userInputTokenDistribution</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/list_tuning_jobs#Output.Schema.SupervisedTuningDatasetDistribution"><code>SupervisedTuningDatasetDistribution</code></a><code> )</code></p>
<p>Output only. Dataset distributions for the user input tokens.</p></td>
</tr>
<tr class="odd">
<td><code>userOutputTokenDistribution</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/list_tuning_jobs#Output.Schema.SupervisedTuningDatasetDistribution"><code>SupervisedTuningDatasetDistribution</code></a><code> )</code></p>
<p>Output only. Dataset distributions for the user output tokens.</p></td>
</tr>
<tr class="even">
<td><code>userMessagePerExampleDistribution</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/list_tuning_jobs#Output.Schema.SupervisedTuningDatasetDistribution"><code>SupervisedTuningDatasetDistribution</code></a><code> )</code></p>
<p>Output only. Dataset distributions for the messages per example.</p></td>
</tr>
<tr class="odd">
<td><code>userDatasetExamples[]</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/list_tuning_jobs#Output.Schema.Content"><code>Content</code></a><code> )</code></p>
<p>Output only. Sample user messages in the training dataset uri.</p></td>
</tr>
<tr class="even">
<td><code>totalTruncatedExampleCount</code></td>
<td><p><code>string ( </code><a href="https://developers.google.com/discovery/v1/type-format"><code>int64</code></a><code> format)</code></p>
<p>Output only. The number of examples in the dataset that have been dropped. An example can be dropped for reasons including: too many tokens, contains an invalid image, contains too many images, etc.</p></td>
</tr>
<tr class="odd">
<td><code>truncatedExampleIndices[]</code></td>
<td><p><code>string ( </code><a href="https://developers.google.com/discovery/v1/type-format"><code>int64</code></a><code> format)</code></p>
<p>Output only. A partial sample of the indices (starting from 1) of the dropped examples.</p></td>
</tr>
<tr class="even">
<td><code>droppedExampleReasons[]</code></td>
<td><p><code>string</code></p>
<p>Output only. For each index in <code>truncated_example_indices</code> , the user-facing reason why the example was dropped.</p></td>
</tr>
</tbody>
</table>

### SupervisedTuningDatasetDistribution

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

| Fields        |                                                                                                                                                                                                                   |
|---------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `sum`         | `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)` Output only. Sum of a given population of values.                                                                          |
| `billableSum` | `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)` Output only. Sum of a given population of values that are billable.                                                        |
| `min`         | `number` Output only. The minimum of the population values.                                                                                                                                                       |
| `max`         | `number` Output only. The maximum of the population values.                                                                                                                                                       |
| `mean`        | `number` Output only. The arithmetic mean of the values in the population.                                                                                                                                        |
| `median`      | `number` Output only. The median of the values in the population.                                                                                                                                                 |
| `p5`          | `number` Output only. The 5th percentile of the values in the population.                                                                                                                                         |
| `p95`         | `number` Output only. The 95th percentile of the values in the population.                                                                                                                                        |
| `buckets[]`   | `object ( `[`DatasetBucket`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/list_tuning_jobs#Output.Schema.DatasetBucket)` )` Output only. Defines the histogram bucket. |

### DatasetBucket

**JSON representation**

```
{
  "count": number,
  "left": number,
  "right": number
}
```

| Fields  |                                                       |
|---------|-------------------------------------------------------|
| `count` | `number` Output only. Number of values in the bucket. |
| `left`  | `number` Output only. Left bound of the bucket.       |
| `right` | `number` Output only. Right bound of the bucket.      |

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

| Fields    |                                                                                                                                                                                                                                                                                                                              |
|-----------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `role`    | `string` Optional. The producer of the content. Must be either 'user' or 'model'. If not set, the service will default to 'user'.                                                                                                                                                                                            |
| `parts[]` | `object ( `[`Part`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/list_tuning_jobs#Output.Schema.Part)` )` Required. A list of `Part` objects that make up a single message. Parts of a message can have different MIME types. A `Content` message must have at least one `Part` . |

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

| Fields                                                                |                                                                                                                                                                                                                                                                                                                             |
|-----------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `thought`                                                             | `boolean` Optional. Indicates whether the `part` represents the model's thought process or reasoning.                                                                                                                                                                                                                       |
| `thoughtSignature`                                                    | `string ( `[`bytes`](https://developers.google.com/discovery/v1/type-format)` format)` Optional. An opaque signature for the thought so it can be reused in subsequent requests. A base64-encoded string.                                                                                                                   |
| `mediaResolution`                                                     | `object ( `[`MediaResolution`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/list_tuning_jobs#Output.Schema.MediaResolution)` )` per part media resolution. Media resolution for the input media.                                                                                 |
| `audioTranscription`                                                  | `object ( `[`AudioTranscription`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/list_tuning_jobs#Output.Schema.AudioTranscription)` )` Optional. Audio (input or output) transcription. This is only set when this Part contains audio data.                                      |
| Union field `data` . `data` can be only one of the following:         |                                                                                                                                                                                                                                                                                                                             |
| `text`                                                                | `string` Optional. The text content of the part. When sent from the VSCode Gemini Code Assist extension, references to @mentioned items will be converted to markdown boldface text. For example `@my-repo` will be converted to and sent as `**my-repo**` by the IDE agent.                                                |
| `inlineData`                                                          | `object ( `[`Blob`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/list_tuning_jobs#Output.Schema.Blob)` )` Optional. The inline data content of the part. This can be used to include images, audio, or video in a request.                                                       |
| `fileData`                                                            | `object ( `[`FileData`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/list_tuning_jobs#Output.Schema.FileData)` )` Optional. The URI-based data of the part. This can be used to include files from Google Cloud Storage.                                                         |
| `functionCall`                                                        | `object ( `[`FunctionCall`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/list_tuning_jobs#Output.Schema.FunctionCall)` )` Optional. A predicted function call returned from the model. This contains the name of the function to call and the arguments to pass to the function. |
| `functionResponse`                                                    | `object ( `[`FunctionResponse`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/list_tuning_jobs#Output.Schema.FunctionResponse)` )` Optional. The result of a function call. This is used to provide the model with the result of a function call that it predicted.               |
| `executableCode`                                                      | `object ( `[`ExecutableCode`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/list_tuning_jobs#Output.Schema.ExecutableCode)` )` Optional. Code generated by the model that is intended to be executed.                                                                             |
| `codeExecutionResult`                                                 | `object ( `[`CodeExecutionResult`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/list_tuning_jobs#Output.Schema.CodeExecutionResult)` )` Optional. The result of executing the `ExecutableCode` .                                                                                 |
| Union field `metadata` . `metadata` can be only one of the following: |                                                                                                                                                                                                                                                                                                                             |
| `videoMetadata`                                                       | `object ( `[`VideoMetadata`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/list_tuning_jobs#Output.Schema.VideoMetadata)` )` Optional. Video metadata. The metadata should only be specified while the video data is presented in inline_data or file_data.                       |

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

| Fields          |                                                                                                                                                                                                                                                                                                           |
|-----------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `id`            | `string` Optional. The unique id of the function call. If populated, the client to execute the `function_call` and return the response with the matching `id` .                                                                                                                                           |
| `name`          | `string` Optional. The name of the function to call. Matches `FunctionDeclaration.name` .                                                                                                                                                                                                                 |
| `args`          | `object ( `[`Struct`](https://protobuf.dev/reference/protobuf/google.protobuf/#struct)` format)` Optional. The function parameters and values in JSON object format. See `FunctionDeclaration.parameters` for parameter details.                                                                          |
| `partialArgs[]` | `object ( `[`PartialArg`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/list_tuning_jobs#Output.Schema.PartialArg)` )` Optional. The partial argument value of the function call. If provided, represents the arguments/fields that are streamed incrementally. |
| `willContinue`  | `boolean` Optional. Whether this is the last part of the FunctionCall. If true, another partial message for the current FunctionCall is expected to follow.                                                                                                                                               |

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
| `parts[]`  | `object ( `[`FunctionResponsePart`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/list_tuning_jobs#Output.Schema.FunctionResponsePart)` )` Optional. Ordered `Parts` that constitute a function response. Parts may have different IANA MIME types.                                                               |

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

| Fields                                                                                                |                                                                                                                                                                                                              |
|-------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Union field `data` . The data of the function response part. `data` can be only one of the following: |                                                                                                                                                                                                              |
| `inlineData`                                                                                          | `object ( `[`FunctionResponseBlob`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/list_tuning_jobs#Output.Schema.FunctionResponseBlob)` )` Inline media bytes.     |
| `fileData`                                                                                            | `object ( `[`FunctionResponseFileData`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/list_tuning_jobs#Output.Schema.FunctionResponseFileData)` )` URI based data. |

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

| Fields                                                      |                                                                                                                                                                                                           |
|-------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `language`                                                  | `enum ( `[`Language`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/list_tuning_jobs#Output.Schema.Language)` )` Required. Programming language of the `code` . |
| `code`                                                      | `string` Required. The code to be executed.                                                                                                                                                               |
| Union field `_id` . `_id` can be only one of the following: |                                                                                                                                                                                                           |
| `id`                                                        | `string` Optional. Unique identifier of the `ExecutableCode` part. The server returns the `CodeExecutionResult` with the matching `id` .                                                                  |

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

| Fields                                                      |                                                                                                                                                                                                   |
|-------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `outcome`                                                   | `enum ( `[`Outcome`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/list_tuning_jobs#Output.Schema.Outcome)` )` Required. Outcome of the code execution. |
| `output`                                                    | `string` Optional. Contains stdout when code execution is successful, stderr or other description otherwise.                                                                                      |
| Union field `_id` . `_id` can be only one of the following: |                                                                                                                                                                                                   |
| `id`                                                        | `string` Optional. The identifier of the `ExecutableCode` part this result is for. Only populated if the corresponding `ExecutableCode` has an id.                                                |

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

### MediaResolution

**JSON representation**

```
{

  // Union field value can be only one of the following:
  "level": enum (Level)
  // End of list of possible types for union field value.
}
```

| Fields                                                          |                                                                                                                                                                                                     |
|-----------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Union field `value` . `value` can be only one of the following: |                                                                                                                                                                                                     |
| `level`                                                         | `enum ( `[`Level`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/list_tuning_jobs#Output.Schema.Level)` )` The tokenization quality used for given media. |

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

| Fields         |                                                                                                                                                                                                                                                                   |
|----------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `text`         | `string` Required. The transcription text of this audio segment.                                                                                                                                                                                                  |
| `speakerLabel` | `string` Optional. A label identifying the speaker of this audio segment (e.g. "spk_1", "spk_2"). Present when diarization is set.                                                                                                                                |
| `words[]`      | `object ( `[`WordInfo`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/list_tuning_jobs#Output.Schema.WordInfo)` )` Optional. Detailed word-level transcriptions and timing details. Present when word_timestamp is set. |

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

### EncryptionSpec

**JSON representation**

```
{
  "kmsKeyName": string
}
```

| Fields       |                                                                                                                                                                                                                                                                   |
|--------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `kmsKeyName` | `string` Required. Resource name of the Cloud KMS key used to protect the resource. The Cloud KMS key must be in the same region as the resource. It must have the format `projects/{project}/locations/{location}/keyRings/{key_ring}/cryptoKeys/{crypto_key}` . |

### EvaluateDatasetRun

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
<td><code>operationName </code><strong><code>(deprecated)</code></strong></td>
<td><p><code>string</code></p>
<blockquote>
<p>This item is deprecated!</p>
</blockquote>
<p>Output only. Deprecated: The updated architecture uses evaluation_run instead.</p></td>
</tr>
<tr class="even">
<td><code>evaluationRun</code></td>
<td><p><code>string</code></p>
<p>Output only. The resource name of the evaluation run. Format: <code>projects/{project}/locations/{location}/evaluationRuns/{evaluation_run_id}</code> .</p></td>
</tr>
<tr class="odd">
<td><code>checkpointId</code></td>
<td><p><code>string</code></p>
<p>Output only. The checkpoint id used in the evaluation run. Only populated when evaluating checkpoints.</p></td>
</tr>
<tr class="even">
<td><code>evaluateDatasetResponse</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/list_tuning_jobs#Output.Schema.EvaluateDatasetResponse"><code>EvaluateDatasetResponse</code></a><code> )</code></p>
<p>Output only. Results for EvaluationService.</p></td>
</tr>
<tr class="odd">
<td><code>error</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/create_endpoint#Output.Schema.Status"><code>Status</code></a><code> )</code></p>
<p>Output only. The error of the evaluation run if any.</p></td>
</tr>
</tbody>
</table>

### EvaluateDatasetResponse

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

| Fields              |                                                                                                                                                                                                                                                               |
|---------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `aggregationOutput` | `object ( `[`AggregationOutput`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/list_tuning_jobs#Output.Schema.AggregationOutput)` )` Output only. Aggregation statistics derived from results of EvaluationService. |
| `outputInfo`        | `object ( `[`OutputInfo`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/list_tuning_jobs#Output.Schema.OutputInfo)` )` Output only. Output info for EvaluationService.                                              |

### AggregationOutput

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

| Fields                 |                                                                                                                                                                                                                               |
|------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `dataset`              | `object ( `[`EvaluationDataset`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/list_tuning_jobs#Output.Schema.EvaluationDataset)` )` The dataset used for evaluation & aggregation. |
| `aggregationResults[]` | `object ( `[`AggregationResult`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/list_tuning_jobs#Output.Schema.AggregationResult)` )` One AggregationResult per metric.              |

### EvaluationDataset

**JSON representation**

```
{

  // Union field source can be only one of the following:
  "gcsSource": {
    object (GcsSource)
  },
  "bigquerySource": {
    object (BigQuerySource)
  }
  // End of list of possible types for union field source.
}
```

| Fields                                                                                       |                                                                                                                                                                                                                                                            |
|----------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Union field `source` . The source of the dataset. `source` can be only one of the following: |                                                                                                                                                                                                                                                            |
| `gcsSource`                                                                                  | `object ( `[`GcsSource`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/upload_model#Input.Schema.GcsSource)` )` Cloud storage source holds the dataset. Currently only one Cloud Storage file path is supported. |
| `bigquerySource`                                                                             | `object ( `[`BigQuerySource`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/list_tuning_jobs#Output.Schema.BigQuerySource)` )` BigQuery source holds the dataset.                                                |

### GcsSource

**JSON representation**

```
{
  "uris": [
    string
  ]
}
```

| Fields   |                                                                                                                                                                                         |
|----------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `uris[]` | `string` Required. Google Cloud Storage URI(-s) to the input file(s). May contain wildcards. For more information on wildcards, see <https://cloud.google.com/storage/docs/wildcards> . |

### BigQuerySource

**JSON representation**

```
{
  "inputUri": string
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
<td><code>inputUri</code></td>
<td><p><code>string</code></p>
<p>Required. BigQuery URI to a table, up to 2000 characters long. Accepted forms:</p>
<ul>
<li>BigQuery path. For example: <code>bq://projectId.bqDatasetId.bqTableId</code> .</li>
</ul></td>
</tr>
</tbody>
</table>

### AggregationResult

**JSON representation**

```
{

  // Union field aggregation_result can be only one of the following:
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
  // End of list of possible types for union field aggregation_result.
}
```

| Fields                                                                                                            |                                                                                                                                                                                                                        |
|-------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Union field `aggregation_result` . The aggregation result. `aggregation_result` can be only one of the following: |                                                                                                                                                                                                                        |
| `pointwiseMetricResult`                                                                                           | `object ( `[`PointwiseMetricResult`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/list_tuning_jobs#Output.Schema.PointwiseMetricResult)` )` Result for pointwise metric.    |
| `pairwiseMetricResult`                                                                                            | `object ( `[`PairwiseMetricResult`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/list_tuning_jobs#Output.Schema.PairwiseMetricResult)` )` Result for pairwise metric.       |
| `exactMatchMetricValue`                                                                                           | `object ( `[`ExactMatchMetricValue`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/list_tuning_jobs#Output.Schema.ExactMatchMetricValue)` )` Results for exact match metric. |
| `bleuMetricValue`                                                                                                 | `object ( `[`BleuMetricValue`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/list_tuning_jobs#Output.Schema.BleuMetricValue)` )` Results for bleu metric.                    |
| `rougeMetricValue`                                                                                                | `object ( `[`RougeMetricValue`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/list_tuning_jobs#Output.Schema.RougeMetricValue)` )` Results for rouge metric.                 |

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

| Fields                                                            |                                                                                                                                                                                                           |
|-------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `explanation`                                                     | `string` Output only. Explanation for pointwise metric score.                                                                                                                                             |
| `customOutput`                                                    | `object ( `[`CustomOutput`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/list_tuning_jobs#Output.Schema.CustomOutput)` )` Output only. Spec for custom output. |
| Union field `_score` . `_score` can be only one of the following: |                                                                                                                                                                                                           |
| `score`                                                           | `number` Output only. Pointwise metric score.                                                                                                                                                             |

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

| Fields                                                                                         |                                                                                                                                                                                                         |
|------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Union field `custom_output` . Custom output. `custom_output` can be only one of the following: |                                                                                                                                                                                                         |
| `rawOutputs`                                                                                   | `object ( `[`RawOutput`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/list_tuning_jobs#Output.Schema.RawOutput)` )` Output only. List of raw output strings. |

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

| Fields           |                                                                                                                                                                                                             |
|------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `pairwiseChoice` | `enum ( `[`PairwiseChoice`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/list_tuning_jobs#Output.Schema.PairwiseChoice)` )` Output only. Pairwise metric choice. |
| `explanation`    | `string` Output only. Explanation for pairwise metric score.                                                                                                                                                |
| `customOutput`   | `object ( `[`CustomOutput`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/mcp/tools_list/list_tuning_jobs#Output.Schema.CustomOutput)` )` Output only. Spec for custom output.   |

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

### OutputInfo

**JSON representation**

```
{

  // Union field output_location can be only one of the following:
  "gcsOutputDirectory": string
  // End of list of possible types for union field output_location.
}
```

| Fields                                                                                                                                           |                                                                                                                                                    |
|--------------------------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------|
| Union field `output_location` . The output location into which evaluation output is written. `output_location` can be only one of the following: |                                                                                                                                                    |
| `gcsOutputDirectory`                                                                                                                             | `string` Output only. The full path of the Cloud Storage directory created, into which the evaluation results and aggregation results are written. |

### AdapterSize

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

### NullValue

Represents a JSON `null` .

`NullValue` is a sentinel, using an enum with only one value to represent the null value for the `Value` type union.

A field of type `NullValue` with any value other than `0` is considered invalid. Most ProtoJSON serializers will emit a `Value` with a `null_value` set as a JSON `null` regardless of the integer value, and so will round trip to a `0` value.

| Enums        |             |
|--------------|-------------|
| `NULL_VALUE` | Null value. |

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

### JobState

Describes the state of a job.

| Enums                           |                                                                                                                                                 |
|---------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------|
| `JOB_STATE_UNSPECIFIED`         | The job state is unspecified.                                                                                                                   |
| `JOB_STATE_QUEUED`              | The job has been just created or resumed and processing has not yet begun.                                                                      |
| `JOB_STATE_PENDING`             | The service is preparing to run the job.                                                                                                        |
| `JOB_STATE_RUNNING`             | The job is in progress.                                                                                                                         |
| `JOB_STATE_SUCCEEDED`           | The job completed successfully.                                                                                                                 |
| `JOB_STATE_FAILED`              | The job failed.                                                                                                                                 |
| `JOB_STATE_CANCELLING`          | The job is being cancelled. From this state the job may only go to either `JOB_STATE_SUCCEEDED` , `JOB_STATE_FAILED` or `JOB_STATE_CANCELLED` . |
| `JOB_STATE_CANCELLED`           | The job has been cancelled.                                                                                                                     |
| `JOB_STATE_PAUSED`              | The job has been stopped, and can be resumed.                                                                                                   |
| `JOB_STATE_EXPIRED`             | The job has expired.                                                                                                                            |
| `JOB_STATE_UPDATING`            | The job is being updated. Only jobs in the `RUNNING` state can be updated. After updating, the job goes back to the `RUNNING` state.            |
| `JOB_STATE_PARTIALLY_SUCCEEDED` | The job is partially succeeded, some results may be missing due to errors.                                                                      |

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

### PairwiseChoice

Pairwise prediction autorater preference.

| Enums                         |                                |
|-------------------------------|--------------------------------|
| `PAIRWISE_CHOICE_UNSPECIFIED` | Unspecified prediction choice. |
| `BASELINE`                    | Baseline prediction wins       |
| `CANDIDATE`                   | Candidate prediction wins      |
| `TIE`                         | Winner cannot be determined    |

### Tool Annotations

Destructive Hint: ❌ \| Idempotent Hint: ✅ \| Read Only Hint: ✅ \| Open World Hint: ❌
