---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.modelMonitors.modelMonitoringJobs
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.modelMonitors.modelMonitoringJobs
title: 'REST Resource: projects.locations.modelMonitors.modelMonitoringJobs'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

## Resource: ModelMonitoringJob

Represents a model monitoring job that analyze dataset using different monitoring algorithm.

Fields

`name` `string`

Output only. Resource name of a ModelMonitoringJob. Format: `projects/{projectId}/locations/{locationId}/modelMonitors/{modelMonitorId}/modelMonitoringJobs/{modelMonitoringJobId}`

`displayName` `string`

The display name of the ModelMonitoringJob. The name can be up to 128 characters long and can consist of any UTF-8.

`modelMonitoringSpec` `object ( `[`ModelMonitoringSpec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.modelMonitors.modelMonitoringJobs#ModelMonitoringJob.ModelMonitoringSpec)` )`

Monitoring monitoring job spec. It outlines the specifications for monitoring objectives, notifications, and result exports. If left blank, the default monitoring specifications from the top-level resource 'ModelMonitor' will be applied. If provided, we will use the specification defined here rather than the default one.

`createTime` `string ( `[`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp)` format)`

Output only. timestamp when this ModelMonitoringJob was created.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`updateTime` `string ( `[`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp)` format)`

Output only. timestamp when this ModelMonitoringJob was updated most recently.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`state` `enum ( `[`JobState`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/JobState)` )`

Output only. The state of the monitoring job. \* When the job is still creating, the state will be 'JOB_STATE_PENDING'. \* Once the job is successfully created, the state will be 'JOB_STATE_RUNNING'. \* Once the job is finished, the state will be one of 'JOB_STATE_FAILED', 'JOB_STATE_SUCCEEDED', 'JOB_STATE_PARTIALLY_SUCCEEDED'.

`schedule` `string`

Output only. Schedule resource name. It will only appear when this job is triggered by a schedule.

`jobExecutionDetail` `object ( `[`ModelMonitoringJobExecutionDetail`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.modelMonitors.modelMonitoringJobs#ModelMonitoringJob.ModelMonitoringJobExecutionDetail)` )`

Output only. Execution results for all the monitoring objectives.

`scheduleTime` `string ( `[`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp)` format)`

Output only. timestamp when this ModelMonitoringJob was scheduled. It will only appear when this job is triggered by a schedule.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

**JSON representation**

```
{
  "name": string,
  "displayName": string,
  "modelMonitoringSpec": {
    object (ModelMonitoringSpec)
  },
  "createTime": string,
  "updateTime": string,
  "state": enum (JobState),
  "schedule": string,
  "jobExecutionDetail": {
    object (ModelMonitoringJobExecutionDetail)
  },
  "scheduleTime": string
}
```

### ModelMonitoringSpec

Monitoring monitoring job spec. It outlines the specifications for monitoring objectives, notifications, and result exports.

Fields

`objectiveSpec` `object ( `[`ModelMonitoringObjectiveSpec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.modelMonitors.modelMonitoringJobs#ModelMonitoringJob.ModelMonitoringObjectiveSpec)` )`

The monitoring objective spec.

`notificationSpec` `object ( `[`ModelMonitoringNotificationSpec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/ModelMonitoringNotificationSpec)` )`

The model monitoring notification spec.

`outputSpec` `object ( `[`ModelMonitoringOutputSpec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/ModelMonitoringOutputSpec)` )`

The Output destination spec for metrics, error logs, etc.

**JSON representation**

```
{
  "objectiveSpec": {
    object (ModelMonitoringObjectiveSpec)
  },
  "notificationSpec": {
    object (ModelMonitoringNotificationSpec)
  },
  "outputSpec": {
    object (ModelMonitoringOutputSpec)
  }
}
```

### ModelMonitoringObjectiveSpec

Monitoring objectives spec.

Fields

`explanationSpec` `object ( `[`ExplanationSpec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/ExplanationSpec)` )`

The explanation spec. This spec is required when the objectives spec includes feature attribution objectives.

`baselineDataset` `object ( `[`ModelMonitoringInput`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/ModelMonitoringInput)` )`

baseline dataset. It could be the training dataset or production serving dataset from a previous period.

`targetDataset` `object ( `[`ModelMonitoringInput`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/ModelMonitoringInput)` )`

Target dataset.

`objective` `Union type`

The monitoring objective. The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:

`tabularObjective` `object ( `[`TabularObjective`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/TabularObjective)` )`

Tabular monitoring objective.

End of mutually exclusive fields.

**JSON representation**

```
{
  "explanationSpec": {
    object (ExplanationSpec)
  },
  "baselineDataset": {
    object (ModelMonitoringInput)
  },
  "targetDataset": {
    object (ModelMonitoringInput)
  },

  // objective
  "tabularObjective": {
    object (TabularObjective)
  }
  // Union type
}
```

### ModelMonitoringJobExecutionDetail

Represent the execution details of the job.

Fields

`baselineDatasets[]` `object ( `[`ProcessedDataset`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.modelMonitors.modelMonitoringJobs#ModelMonitoringJob.ProcessedDataset)` )`

Processed baseline datasets.

`targetDatasets[]` `object ( `[`ProcessedDataset`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.modelMonitors.modelMonitoringJobs#ModelMonitoringJob.ProcessedDataset)` )`

Processed target datasets.

`objectiveStatus` `map (key: string, value: object ( `[`Status`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/ListOperationsResponse#Status)` ))`

status of data processing for each monitoring objective. Key is the objective.

`error` `object ( `[`Status`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/ListOperationsResponse#Status)` )`

Additional job error status.

**JSON representation**

```
{
  "baselineDatasets": [
    {
      object (ProcessedDataset)
    }
  ],
  "targetDatasets": [
    {
      object (ProcessedDataset)
    }
  ],
  "objectiveStatus": {
    string: {
      object (Status)
    },
    ...
  },
  "error": {
    object (Status)
  }
}
```

### ProcessedDataset

Processed dataset information.

Fields

`location` `string`

Actual data location of the processed dataset.

`timeRange` `object ( `[`Interval`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/Interval)` )`

Dataset time range information if any.

**JSON representation**

```
{
  "location": string,
  "timeRange": {
    object (Interval)
  }
}
```

| Methods                                                                                                                                                       |                               |
|---------------------------------------------------------------------------------------------------------------------------------------------------------------|-------------------------------|
| [`create`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.modelMonitors.modelMonitoringJobs/create) | Creates a ModelMonitoringJob. |
| [`delete`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.modelMonitors.modelMonitoringJobs/delete) | Deletes a ModelMonitoringJob. |
| [`get`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.modelMonitors.modelMonitoringJobs/get)       | Gets a ModelMonitoringJob.    |
| [`list`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.modelMonitors.modelMonitoringJobs/list)     | Lists ModelMonitoringJobs.    |
