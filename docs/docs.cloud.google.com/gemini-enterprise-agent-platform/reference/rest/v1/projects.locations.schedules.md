---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.schedules
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.schedules
title: 'REST Resource: projects.locations.schedules'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

## Resource: Schedule

An instance of a Schedule periodically schedules runs to make API calls based on user specified time specification and API request type.

Fields

`name` `string`

Immutable. The resource name of the Schedule.

`displayName` `string`

Required. user provided name of the Schedule. The name can be up to 128 characters long and can consist of any UTF-8 characters.

`startTime` `string ( `[`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp)` format)`

Optional. timestamp after which the first run can be scheduled. Default to Schedule create time if not specified.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`endTime` `string ( `[`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp)` format)`

Optional. timestamp after which no new runs can be scheduled. If specified, The schedule will be completed when either endTime is reached or when scheduled_run_count \>= maxRunCount. If not specified, new runs will keep getting scheduled until this Schedule is paused or deleted. Already scheduled runs will be allowed to complete. Unset if not specified.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`maxRunCount` `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)`

Optional. Maximum run count of the schedule. If specified, The schedule will be completed when either startedRunCount \>= maxRunCount or when endTime is reached. If not specified, new runs will keep getting scheduled until this Schedule is paused or deleted. Already scheduled runs will be allowed to complete. Unset if not specified.

`startedRunCount` `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)`

Output only. The number of runs started by this schedule.

`state` `enum ( `[`State`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.schedules#State)` )`

Output only. The state of this Schedule.

`createTime` `string ( `[`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp)` format)`

Output only. timestamp when this Schedule was created.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`updateTime` `string ( `[`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp)` format)`

Output only. timestamp when this Schedule was updated.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`nextRunTime` `string ( `[`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp)` format)`

Output only. timestamp when this Schedule should schedule the next run. Having a nextRunTime in the past means the runs are being started behind schedule.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`lastPauseTime` `string ( `[`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp)` format)`

Output only. timestamp when this Schedule was last paused. Unset if never paused.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`lastResumeTime` `string ( `[`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp)` format)`

Output only. timestamp when this Schedule was last resumed. Unset if never resumed from pause.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`maxConcurrentRunCount` `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)`

Required. Maximum number of runs that can be started concurrently for this Schedule. This is the limit for starting the scheduled requests and not the execution of the operations/jobs created by the requests (if applicable).

`maxConcurrentActiveRunCount` `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)`

Optional. Specifies the maximum number of active runs that can be executed concurrently for this Schedule. This limits the number of runs that can be in a non-terminal state at the same time. Currently, this field is only supported for requests of type CreatePipelineJobRequest.

`allowQueueing` `boolean`

Optional. Whether new scheduled runs can be queued when max_concurrent_runs limit is reached. If set to true, new runs will be queued instead of skipped. Default to false.

`catchUp` `boolean`

Output only. Whether to backfill missed runs when the schedule is resumed from PAUSED state. If set to true, all missed runs will be scheduled. New runs will be scheduled after the backfill is complete. Default to false.

`lastScheduledRunResponse` `object ( `[`RunResponse`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.schedules#RunResponse)` )`

Output only. Response of the last scheduled run. This is the response for starting the scheduled requests and not the execution of the operations/jobs created by the requests (if applicable). Unset if no run has been scheduled yet.

`time_specification` `Union type`

Required. The time specification to launch scheduled runs. The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:

`cron` `string`

Cron schedule ( <https://en.wikipedia.org/wiki/Cron> ) to launch scheduled runs. To explicitly set a timezone to the cron tab, apply a prefix in the cron tab: "CRON_TZ=\${IANA_TIME_ZONE}" or "TZ=\${IANA_TIME_ZONE}". The \${IANA_TIME_ZONE} may only be a valid string from IANA time zone database. For example, "CRON_TZ=America/New_York 1 \* \* \* \*", or "TZ=America/New_York 1 \* \* \* \*".

End of mutually exclusive fields.

`request` `Union type`

Required. The API request template to launch the scheduled runs. User-specified ID is not supported in the request template. The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:

`createPipelineJobRequest` `object ( `[`CreatePipelineJobRequest`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.schedules#CreatePipelineJobRequest)` )`

Request for [`PipelineService.CreatePipelineJob`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.pipelineJobs/create#google.cloud.aiplatform.v1.PipelineService.CreatePipelineJob) . CreatePipelineJobRequest.parent field is required (format: projects/{project}/locations/{location}).

`createNotebookExecutionJobRequest` `object ( `[`CreateNotebookExecutionJobRequest`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.schedules#CreateNotebookExecutionJobRequest)` )`

Request for [`NotebookService.CreateNotebookExecutionJob`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.notebookExecutionJobs/create#google.cloud.aiplatform.v1.NotebookService.CreateNotebookExecutionJob) .

End of mutually exclusive fields.

**JSON representation**

```
{
  "name": string,
  "displayName": string,
  "startTime": string,
  "endTime": string,
  "maxRunCount": string,
  "startedRunCount": string,
  "state": enum (State),
  "createTime": string,
  "updateTime": string,
  "nextRunTime": string,
  "lastPauseTime": string,
  "lastResumeTime": string,
  "maxConcurrentRunCount": string,
  "maxConcurrentActiveRunCount": string,
  "allowQueueing": boolean,
  "catchUp": boolean,
  "lastScheduledRunResponse": {
    object (RunResponse)
  },

  // time_specification
  "cron": string
  // Union type

  // request
  "createPipelineJobRequest": {
    object (CreatePipelineJobRequest)
  },
  "createNotebookExecutionJobRequest": {
    object (CreateNotebookExecutionJobRequest)
  }
  // Union type
}
```

## CreatePipelineJobRequest

Request message for [`PipelineService.CreatePipelineJob`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.pipelineJobs/create#google.cloud.aiplatform.v1.PipelineService.CreatePipelineJob) .

Fields

`parent` `string`

Required. The resource name of the Location to create the PipelineJob in. Format: `projects/{project}/locations/{location}`

`pipelineJob` `object ( `[`PipelineJob`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.pipelineJobs#PipelineJob)` )`

Required. The PipelineJob to create.

`pipelineJobId` `string`

The id to use for the PipelineJob, which will become the final component of the PipelineJob name. If not provided, an id will be automatically generated.

This value should be less than 128 characters, and valid characters are `/[a-z][0-9]-/` .

**JSON representation**

```
{
  "parent": string,
  "pipelineJob": {
    object (PipelineJob)
  },
  "pipelineJobId": string
}
```

## CreateNotebookExecutionJobRequest

Request message for \[NotebookService.CreateNotebookExecutionJob\]

Fields

`parent` `string`

Required. The resource name of the Location to create the NotebookExecutionJob. Format: `projects/{project}/locations/{location}`

`notebookExecutionJob` `object ( `[`NotebookExecutionJob`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.notebookExecutionJobs#NotebookExecutionJob)` )`

Required. The NotebookExecutionJob to create.

`notebookExecutionJobId` `string`

Optional. user specified id for the NotebookExecutionJob.

**JSON representation**

```
{
  "parent": string,
  "notebookExecutionJob": {
    object (NotebookExecutionJob)
  },
  "notebookExecutionJobId": string
}
```

## State

Possible state of the schedule.

| Enums               |                                                                                                                                                                       |
|---------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `STATE_UNSPECIFIED` | Unspecified.                                                                                                                                                          |
| `ACTIVE`            | The Schedule is active. Runs are being scheduled on the user-specified timespec.                                                                                      |
| `PAUSED`            | The schedule is paused. No new runs will be created until the schedule is resumed. Already started runs will be allowed to complete.                                  |
| `COMPLETED`         | The Schedule is completed. No new runs will be scheduled. Already started runs will be allowed to complete. Schedules in completed state cannot be paused or resumed. |

## RunResponse

status of a scheduled run.

Fields

`scheduledRunTime` `string ( `[`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp)` format)`

The scheduled run time based on the user-specified schedule.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`runResponse` `string`

The response of the scheduled run.

**JSON representation**

```
{
  "scheduledRunTime": string,
  "runResponse": string
}
```

| Methods                                                                                                                          |                                                         |
|----------------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------|
| [`create`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.schedules/create) | Creates a Schedule.                                     |
| [`delete`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.schedules/delete) | Deletes a Schedule.                                     |
| [`get`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.schedules/get)       | Gets a Schedule.                                        |
| [`list`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.schedules/list)     | Lists Schedules in a Location.                          |
| [`patch`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.schedules/patch)   | Updates an active or paused Schedule.                   |
| [`pause`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.schedules/pause)   | Pauses a Schedule.                                      |
| [`resume`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.schedules/resume) | Resumes a paused Schedule to start scheduling new runs. |
