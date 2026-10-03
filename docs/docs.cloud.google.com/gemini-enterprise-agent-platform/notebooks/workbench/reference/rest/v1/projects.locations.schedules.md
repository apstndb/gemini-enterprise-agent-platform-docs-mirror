---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v1/projects.locations.schedules
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v1/projects.locations.schedules
title: 'REST Resource: projects.locations.schedules'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

## Resource: Schedule

The definition of a schedule.

**JSON representation**

```
{
  "name": string,
  "displayName": string,
  "description": string,
  "state": enum (State),
  "cronSchedule": string,
  "timeZone": string,
  "createTime": string,
  "updateTime": string,
  "executionTemplate": {
    object (ExecutionTemplate)
  },
  "recentExecutions": [
    {
      object (Execution)
    }
  ]
}
```

| Fields               |                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
|----------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `name`               | `string` Output only. The name of this schedule. Format: `projects/{projectId}/locations/{location}/schedules/{scheduleId}`                                                                                                                                                                                                                                                                                                                                 |
| `displayName`        | `string` Output only. Display name used for UI purposes. Name can only contain alphanumeric characters, hyphens `-` , and underscores `_` .                                                                                                                                                                                                                                                                                                                 |
| `description`        | `string` A brief description of this environment.                                                                                                                                                                                                                                                                                                                                                                                                           |
| `state`              | `enum ( `[`State`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v1/projects.locations.schedules#State)` )`                                                                                                                                                                                                                                                                                             |
| `cronSchedule`       | `string` Cron-tab formatted schedule by which the job will execute. Format: minute, hour, day of month, month, day of week, e.g. `0 0 * * WED` = every Wednesday More examples: <https://crontab.guru/examples.html>                                                                                                                                                                                                                                        |
| `timeZone`           | `string` Timezone on which the cronSchedule. The value of this field must be a time zone name from the tz database. TZ Database: <https://en.wikipedia.org/wiki/List_of_tz_database_time_zones> Note that some time zones include a provision for daylight savings time. The rules for daylight saving time are determined by the chosen tz. For UTC use the string "utc". If a time zone is not specified, the default will be in UTC (also known as GMT). |
| `createTime`         | `string ( `[`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp)` format)` Output only. Time the schedule was created. Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .                                           |
| `updateTime`         | `string ( `[`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp)` format)` Output only. Time the schedule was last updated. Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .                                      |
| `executionTemplate`  | `object ( `[`ExecutionTemplate`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v1/ExecutionTemplate)` )` Notebook Execution Template corresponding to this schedule.                                                                                                                                                                                                                                    |
| `recentExecutions[]` | `object ( `[`Execution`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v1/projects.locations.executions#Execution)` )` Output only. The most recent execution names triggered from this schedule and their corresponding states.                                                                                                                                                                        |

## State

State of the job.

| Enums               |                                                                                                                                                                                                                                                                                                       |
|---------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `STATE_UNSPECIFIED` | Unspecified state.                                                                                                                                                                                                                                                                                    |
| `ENABLED`           | The job is executing normally.                                                                                                                                                                                                                                                                        |
| `PAUSED`            | The job is paused by the user. It will not execute. A user can intentionally pause the job using [Cloud Scheduler](https://cloud.google.com/scheduler/docs/creating#pause) .                                                                                                                          |
| `DISABLED`          | The job is disabled by the system due to error. The user cannot directly set a job to be disabled.                                                                                                                                                                                                    |
| `UPDATE_FAILED`     | The job state resulting from a failed [CloudScheduler.UpdateJob](https://cloud.google.com/scheduler/docs/creating#edit) operation. To recover a job from this state, retry [CloudScheduler.UpdateJob](https://cloud.google.com/scheduler/docs/creating#edit) until a successful response is received. |
| `INITIALIZING`      | The schedule resource is being created.                                                                                                                                                                                                                                                               |
| `DELETING`          | The schedule resource is being deleted.                                                                                                                                                                                                                                                               |

| Methods                                                                                                                                              |                                                                   |
|------------------------------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------|
| [`create`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v1/projects.locations.schedules/create) | Creates a new Scheduled Notebook in a given project and location. |
| [`delete`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v1/projects.locations.schedules/delete) | Deletes schedule and all underlying jobs                          |
| [`get`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v1/projects.locations.schedules/get)       | Gets details of schedule                                          |
| [`list`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v1/projects.locations.schedules/list)     | Lists schedules in a given project and location.                  |
