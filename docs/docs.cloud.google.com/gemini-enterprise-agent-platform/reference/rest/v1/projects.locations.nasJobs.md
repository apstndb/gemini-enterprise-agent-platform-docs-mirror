---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.nasJobs
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.nasJobs
title: 'REST Resource: projects.locations.nasJobs'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

## Resource: NasJob

Represents a Neural Architecture Search (NAS) job.

Fields

`name` `string`

Output only. Resource name of the NasJob.

`displayName` `string`

Required. The display name of the NasJob. The name can be up to 128 characters long and can consist of any UTF-8 characters.

`nasJobSpec` `object ( `[`NasJobSpec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.nasJobs#NasJobSpec)` )`

Required. The specification of a NasJob.

`nasJobOutput` `object ( `[`NasJobOutput`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.nasJobs#NasJobOutput)` )`

Output only. Output of the NasJob.

`state` `enum ( `[`JobState`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/JobState)` )`

Output only. The detailed state of the job.

`createTime` `string ( `[`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp)` format)`

Output only. time when the NasJob was created.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`startTime` `string ( `[`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp)` format)`

Output only. time when the NasJob for the first time entered the `JOB_STATE_RUNNING` state.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`endTime` `string ( `[`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp)` format)`

Output only. time when the NasJob entered any of the following states: `JOB_STATE_SUCCEEDED` , `JOB_STATE_FAILED` , `JOB_STATE_CANCELLED` .

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`updateTime` `string ( `[`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp)` format)`

Output only. time when the NasJob was most recently updated.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`error` `object ( `[`Status`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/ListOperationsResponse#Status)` )`

Output only. Only populated when job's state is JOB_STATE_FAILED or JOB_STATE_CANCELLED.

`labels` `map (key: string, value: string)`

The labels with user-defined metadata to organize NasJobs.

label keys and values can be no longer than 64 characters (Unicode codepoints), can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed.

See <https://goo.gl/xmQnxf> for more information and examples of labels.

`encryptionSpec` `object ( `[`EncryptionSpec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/EncryptionSpec)` )`

Customer-managed encryption key options for a NasJob. If this is set, then all resources created by the NasJob will be encrypted with the provided encryption key.

`enableRestrictedImageTraining `**`(deprecated)`** `boolean`

> This item is deprecated!

Optional. Enable a separation of Custom model training and restricted image training for tenant project.

`satisfiesPzs` `boolean`

Output only. reserved for future use.

`satisfiesPzi` `boolean`

Output only. reserved for future use.

**JSON representation**

```
{
  "name": string,
  "displayName": string,
  "nasJobSpec": {
    object (NasJobSpec)
  },
  "nasJobOutput": {
    object (NasJobOutput)
  },
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
  "encryptionSpec": {
    object (EncryptionSpec)
  },
  "enableRestrictedImageTraining": boolean,
  "satisfiesPzs": boolean,
  "satisfiesPzi": boolean
}
```

## NasJobSpec

Represents the spec of a NasJob.

Fields

`resumeNasJobId` `string`

The id of the existing NasJob in the same Project and Location which will be used to resume search. searchSpaceSpec and nas_algorithm_spec are obtained from previous NasJob hence should not provide them again for this NasJob.

`searchSpaceSpec` `string`

It defines the search space for Neural Architecture Search (NAS).

`nas_algorithm_spec` `Union type`

The Neural Architecture Search (NAS) algorithm specification. The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:

`multiTrialAlgorithmSpec` `object ( `[`MultiTrialAlgorithmSpec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.nasJobs#MultiTrialAlgorithmSpec)` )`

The spec of multi-trial algorithms.

End of mutually exclusive fields.

**JSON representation**

```
{
  "resumeNasJobId": string,
  "searchSpaceSpec": string,

  // nas_algorithm_spec
  "multiTrialAlgorithmSpec": {
    object (MultiTrialAlgorithmSpec)
  }
  // Union type
}
```

## MultiTrialAlgorithmSpec

The spec of multi-trial Neural Architecture Search (NAS).

Fields

`multiTrialAlgorithm` `enum ( `[`MultiTrialAlgorithm`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.nasJobs#MultiTrialAlgorithm)` )`

The multi-trial Neural Architecture Search (NAS) algorithm type. Defaults to `REINFORCEMENT_LEARNING` .

`metric` `object ( `[`MetricSpec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.nasJobs#MetricSpec)` )`

Metric specs for the NAS job. Validation for this field is done at `multiTrialAlgorithmSpec` field.

`searchTrialSpec` `object ( `[`SearchTrialSpec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.nasJobs#SearchTrialSpec)` )`

Required. Spec for search trials.

`trainTrialSpec` `object ( `[`TrainTrialSpec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.nasJobs#TrainTrialSpec)` )`

Spec for train trials. top N \[TrainTrialSpec.max_parallel_trial_count\] search trials will be trained for every M \[TrainTrialSpec.frequency\] trials searched.

**JSON representation**

```
{
  "multiTrialAlgorithm": enum (MultiTrialAlgorithm),
  "metric": {
    object (MetricSpec)
  },
  "searchTrialSpec": {
    object (SearchTrialSpec)
  },
  "trainTrialSpec": {
    object (TrainTrialSpec)
  }
}
```

## MultiTrialAlgorithm

The available types of multi-trial algorithms.

| Enums                               |                                                                                        |
|-------------------------------------|----------------------------------------------------------------------------------------|
| `MULTI_TRIAL_ALGORITHM_UNSPECIFIED` | Defaults to `REINFORCEMENT_LEARNING` .                                                 |
| `REINFORCEMENT_LEARNING`            | The Reinforcement Learning algorithm for Multi-trial Neural Architecture Search (NAS). |
| `GRID_SEARCH`                       | The Grid Search algorithm for Multi-trial Neural Architecture Search (NAS).            |

## MetricSpec

Represents a metric to optimize.

Fields

`metricId` `string`

Required. The id of the metric. Must not contain whitespaces.

`goal` `enum ( `[`GoalType`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.nasJobs#GoalType)` )`

Required. The optimization goal of the metric.

**JSON representation**

```
{
  "metricId": string,
  "goal": enum (GoalType)
}
```

## GoalType

The available types of optimization goals.

| Enums                   |                                     |
|-------------------------|-------------------------------------|
| `GOAL_TYPE_UNSPECIFIED` | Goal type will default to maximize. |
| `MAXIMIZE`              | Maximize the goal metric.           |
| `MINIMIZE`              | Minimize the goal metric.           |

## SearchTrialSpec

Represent spec for search trials.

Fields

`searchTrialJobSpec` `object ( `[`CustomJobSpec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/CustomJobSpec)` )`

Required. The spec of a search trial job. The same spec applies to all search trials.

`maxTrialCount` `integer`

Required. The maximum number of Neural Architecture Search (NAS) trials to run.

`maxParallelTrialCount` `integer`

Required. The maximum number of trials to run in parallel.

`maxFailedTrialCount` `integer`

The number of failed trials that need to be seen before failing the NasJob.

If set to 0, Agent Platform decides how many trials must fail before the whole job fails.

**JSON representation**

```
{
  "searchTrialJobSpec": {
    object (CustomJobSpec)
  },
  "maxTrialCount": integer,
  "maxParallelTrialCount": integer,
  "maxFailedTrialCount": integer
}
```

## TrainTrialSpec

Represent spec for train trials.

Fields

`trainTrialJobSpec` `object ( `[`CustomJobSpec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/CustomJobSpec)` )`

Required. The spec of a train trial job. The same spec applies to all train trials.

`maxParallelTrialCount` `integer`

Required. The maximum number of trials to run in parallel.

`frequency` `integer`

Required. Frequency of search trials to start train stage. top N \[TrainTrialSpec.max_parallel_trial_count\] search trials will be trained for every M \[TrainTrialSpec.frequency\] trials searched.

**JSON representation**

```
{
  "trainTrialJobSpec": {
    object (CustomJobSpec)
  },
  "maxParallelTrialCount": integer,
  "frequency": integer
}
```

## NasJobOutput

Represents a uCAIP NasJob output.

Fields

`output` `Union type`

The output of this Neural Architecture Search (NAS) job. The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:

`multiTrialJobOutput` `object ( `[`MultiTrialJobOutput`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.nasJobs#MultiTrialJobOutput)` )`

Output only. The output of this multi-trial Neural Architecture Search (NAS) job.

End of mutually exclusive fields.

**JSON representation**

```
{

  // output
  "multiTrialJobOutput": {
    object (MultiTrialJobOutput)
  }
  // Union type
}
```

## MultiTrialJobOutput

The output of a multi-trial Neural Architecture Search (NAS) jobs.

Fields

`searchTrials[]` `object ( `[`NasTrial`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/NasTrial)` )`

Output only. List of NasTrials that were started as part of search stage.

`trainTrials[]` `object ( `[`NasTrial`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/NasTrial)` )`

Output only. List of NasTrials that were started as part of train stage.

**JSON representation**

```
{
  "searchTrials": [
    {
      object (NasTrial)
    }
  ],
  "trainTrials": [
    {
      object (NasTrial)
    }
  ]
}
```

| Methods                                                                                                                        |                              |
|--------------------------------------------------------------------------------------------------------------------------------|------------------------------|
| [`cancel`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.nasJobs/cancel) | Cancels a NasJob.            |
| [`create`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.nasJobs/create) | Creates a NasJob             |
| [`delete`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.nasJobs/delete) | Deletes a NasJob.            |
| [`get`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.nasJobs/get)       | Gets a NasJob                |
| [`list`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.nasJobs/list)     | Lists NasJobs in a Location. |
