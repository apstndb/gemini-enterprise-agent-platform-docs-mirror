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

`modelMonitoringSpec` ` object ( ModelMonitoringSpec  ` )

Monitoring monitoring job spec. It outlines the specifications for monitoring objectives, notifications, and result exports. If left blank, the default monitoring specifications from the top-level resource 'ModelMonitor' will be applied. If provided, we will use the specification defined here rather than the default one.

`createTime` ` string ( Timestamp  ` format)

Output only. timestamp when this ModelMonitoringJob was created.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`updateTime` ` string ( Timestamp  ` format)

Output only. timestamp when this ModelMonitoringJob was updated most recently.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`state` ` enum ( JobState  ` )

Output only. The state of the monitoring job. \* When the job is still creating, the state will be 'JOB\_STATE\_PENDING'. \* Once the job is successfully created, the state will be 'JOB\_STATE\_RUNNING'. \* Once the job is finished, the state will be one of 'JOB\_STATE\_FAILED', 'JOB\_STATE\_SUCCEEDED', 'JOB\_STATE\_PARTIALLY\_SUCCEEDED'.

`schedule` `string`

Output only. Schedule resource name. It will only appear when this job is triggered by a schedule.

`jobExecutionDetail` ` object ( ModelMonitoringJobExecutionDetail  ` )

Output only. Execution results for all the monitoring objectives.

`scheduleTime` ` string ( Timestamp  ` format)

Output only. timestamp when this ModelMonitoringJob was scheduled. It will only appear when this job is triggered by a schedule.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;name&quot;: string,&quot;displayName&quot;: string,&quot;modelMonitoringSpec&quot;: {object (ModelMonitoringSpec)},&quot;createTime&quot;: string,&quot;updateTime&quot;: string,&quot;state&quot;: enum (JobState),&quot;schedule&quot;: string,&quot;jobExecutionDetail&quot;: {object (ModelMonitoringJobExecutionDetail)},&quot;scheduleTime&quot;: string}</code></pre></td>
</tr>
</tbody>
</table>

### ModelMonitoringSpec

Monitoring monitoring job spec. It outlines the specifications for monitoring objectives, notifications, and result exports.

Fields

`objectiveSpec` ` object ( ModelMonitoringObjectiveSpec  ` )

The monitoring objective spec.

`notificationSpec` ` object ( ModelMonitoringNotificationSpec  ` )

The model monitoring notification spec.

`outputSpec` ` object ( ModelMonitoringOutputSpec  ` )

The Output destination spec for metrics, error logs, etc.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;objectiveSpec&quot;: {object (ModelMonitoringObjectiveSpec)},&quot;notificationSpec&quot;: {object (ModelMonitoringNotificationSpec)},&quot;outputSpec&quot;: {object (ModelMonitoringOutputSpec)}}</code></pre></td>
</tr>
</tbody>
</table>

### ModelMonitoringObjectiveSpec

Monitoring objectives spec.

Fields

`explanationSpec` ` object ( ExplanationSpec  ` )

The explanation spec. This spec is required when the objectives spec includes feature attribution objectives.

`baselineDataset` ` object ( ModelMonitoringInput  ` )

baseline dataset. It could be the training dataset or production serving dataset from a previous period.

`targetDataset` ` object ( ModelMonitoringInput  ` )

Target dataset.

`objective` `Union type`

The monitoring objective. `objective` can be only one of the following:

`tabularObjective` ` object ( TabularObjective  ` )

Tabular monitoring objective.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;explanationSpec&quot;: {object (ExplanationSpec)},&quot;baselineDataset&quot;: {object (ModelMonitoringInput)},&quot;targetDataset&quot;: {object (ModelMonitoringInput)},// objective&quot;tabularObjective&quot;: {object (TabularObjective)}// Union type}</code></pre></td>
</tr>
</tbody>
</table>

### ModelMonitoringJobExecutionDetail

Represent the execution details of the job.

Fields

`baselineDatasets[]` ` object ( ProcessedDataset  ` )

Processed baseline datasets.

`targetDatasets[]` ` object ( ProcessedDataset  ` )

Processed target datasets.

`objectiveStatus` ` map (key: string, value: object ( Status  ` ))

status of data processing for each monitoring objective. Key is the objective.

`error` ` object ( Status  ` )

Additional job error status.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;baselineDatasets&quot;: [{object (ProcessedDataset)}],&quot;targetDatasets&quot;: [{object (ProcessedDataset)}],&quot;objectiveStatus&quot;: {string: {object (Status)},...},&quot;error&quot;: {object (Status)}}</code></pre></td>
</tr>
</tbody>
</table>

### ProcessedDataset

Processed dataset information.

Fields

`location` `string`

Actual data location of the processed dataset.

`timeRange` ` object ( Interval  ` )

Dataset time range information if any.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;location&quot;: string,&quot;timeRange&quot;: {object (Interval)}}</code></pre></td>
</tr>
</tbody>
</table>

## Methods

### `            create           `

Creates a ModelMonitoringJob.

### `            delete           `

Deletes a ModelMonitoringJob.

### `            get           `

Gets a ModelMonitoringJob.

### `            list           `

Lists ModelMonitoringJobs.
