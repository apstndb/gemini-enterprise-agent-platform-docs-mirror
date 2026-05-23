---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v1/projects.locations.schedules
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v1/projects.locations.schedules
title: 'REST Resource: projects.locations.schedules'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

## Resource: Schedule

The definition of a schedule.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;name&quot;: string,&quot;displayName&quot;: string,&quot;description&quot;: string,&quot;state&quot;: enum (State),&quot;cronSchedule&quot;: string,&quot;timeZone&quot;: string,&quot;createTime&quot;: string,&quot;updateTime&quot;: string,&quot;executionTemplate&quot;: {object (ExecutionTemplate)},&quot;recentExecutions&quot;: [{object (Execution)}]}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`name`

`string`

Output only. The name of this schedule. Format: `projects/{projectId}/locations/{location}/schedules/{scheduleId}`

`displayName`

`string`

Output only. Display name used for UI purposes. Name can only contain alphanumeric characters, hyphens `-` , and underscores `_` .

`description`

`string`

A brief description of this environment.

`state`

` enum ( State  ` )

`cronSchedule`

`string`

Cron-tab formatted schedule by which the job will execute. Format: minute, hour, day of month, month, day of week, e.g. `0 0 * * WED` = every Wednesday More examples: <https://crontab.guru/examples.html>

`timeZone`

`string`

Timezone on which the cronSchedule. The value of this field must be a time zone name from the tz database. TZ Database: <https://en.wikipedia.org/wiki/List_of_tz_database_time_zones>

Note that some time zones include a provision for daylight savings time. The rules for daylight saving time are determined by the chosen tz. For UTC use the string "utc". If a time zone is not specified, the default will be in UTC (also known as GMT).

`createTime`

` string ( Timestamp  ` format)

Output only. Time the schedule was created.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`updateTime`

` string ( Timestamp  ` format)

Output only. Time the schedule was last updated.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`executionTemplate`

` object ( ExecutionTemplate  ` )

Notebook Execution Template corresponding to this schedule.

`recentExecutions[]`

` object ( Execution  ` )

Output only. The most recent execution names triggered from this schedule and their corresponding states.

## State

State of the job.

Enums

`STATE_UNSPECIFIED`

Unspecified state.

`ENABLED`

The job is executing normally.

`PAUSED`

The job is paused by the user. It will not execute. A user can intentionally pause the job using [Cloud Scheduler](https://cloud.google.com/scheduler/docs/creating#pause) .

`DISABLED`

The job is disabled by the system due to error. The user cannot directly set a job to be disabled.

`UPDATE_FAILED`

The job state resulting from a failed [CloudScheduler.UpdateJob](https://cloud.google.com/scheduler/docs/creating#edit) operation. To recover a job from this state, retry [CloudScheduler.UpdateJob](https://cloud.google.com/scheduler/docs/creating#edit) until a successful response is received.

`INITIALIZING`

The schedule resource is being created.

`DELETING`

The schedule resource is being deleted.

## Methods

### `            create           `

Creates a new Scheduled Notebook in a given project and location.

### `            delete           `

Deletes schedule and all underlying jobs

### `            get           `

Gets details of schedule

### `            list           `

Lists schedules in a given project and location.
