---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.featureGroups.featureMonitors.featureMonitorJobs
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.featureGroups.featureMonitors.featureMonitorJobs
title: 'REST Resource: projects.locations.featureGroups.featureMonitors.featureMonitorJobs'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

## Resource: FeatureMonitorJob

Agent Platform feature Monitor Job.

Fields

`name` `string`

Identifier. name of the FeatureMonitorJob. Format: `projects/{project}/locations/{location}/featureGroups/{featureGroup}/featureMonitors/{featureMonitor}/featureMonitorJobs/{featureMonitorJob}` .

`createTime` ` string ( Timestamp  ` format)

Output only. timestamp when this FeatureMonitorJob was created. Creation of a FeatureMonitorJob means that the job is pending / waiting for sufficient resources but may not have started running yet.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`finalStatus` ` object ( Status  ` )

Output only. Final status of the FeatureMonitorJob.

`jobSummary` ` object ( JobSummary  ` )

Output only. Summary from the FeatureMonitorJob.

`labels` `map (key: string, value: string)`

Optional. The labels with user-defined metadata to organize your FeatureMonitorJob.

label keys and values can be no longer than 64 characters (Unicode codepoints), can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed.

See <https://goo.gl/xmQnxf> for more information on and examples of labels. No more than 64 user labels can be associated with one FeatureMonitor(System labels are excluded)." System reserved label keys are prefixed with "aiplatform.googleapis.com/" and are immutable.

`description` `string`

Optional. description of the FeatureMonitor.

`driftBaseFeatureMonitorJobId` `string ( int64 format)`

Output only. FeatureMonitorJob id comparing to which the drift is calculated.

`driftBaseSnapshotTime` ` string ( Timestamp  ` format)

Output only. data snapshot time comparing to which the drift is calculated.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`featureSelectionConfig` ` object ( FeatureSelectionConfig  ` )

Output only. feature selection config used when creating FeatureMonitorJob.

`triggerType` ` enum ( FeatureMonitorJobTrigger  ` )

Output only. Trigger type of the feature Monitor Job.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;name&quot;: string,&quot;createTime&quot;: string,&quot;finalStatus&quot;: {object (Status)},&quot;jobSummary&quot;: {object (JobSummary)},&quot;labels&quot;: {string: string,...},&quot;description&quot;: string,&quot;driftBaseFeatureMonitorJobId&quot;: string,&quot;driftBaseSnapshotTime&quot;: string,&quot;featureSelectionConfig&quot;: {object (FeatureSelectionConfig)},&quot;triggerType&quot;: enum (FeatureMonitorJobTrigger)}</code></pre></td>
</tr>
</tbody>
</table>

## JobSummary

Summary from the FeatureMonitorJob.

Fields

`totalSlotMs` `string ( int64 format)`

Output only. BigQuery slot milliseconds consumed.

`featureStatsAndAnomalies[]` ` object ( FeatureStatsAndAnomaly  ` )

Output only. Features and their stats and anomalies

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;totalSlotMs&quot;: string,&quot;featureStatsAndAnomalies&quot;: [{object (FeatureStatsAndAnomaly)}]}</code></pre></td>
</tr>
</tbody>
</table>

## FeatureMonitorJobTrigger

Choices of the trigger type.

Enums

`FEATURE_MONITOR_JOB_TRIGGER_UNSPECIFIED`

Trigger type unspecified.

`FEATURE_MONITOR_JOB_TRIGGER_PERIODIC`

Triggered by periodic schedule.

`FEATURE_MONITOR_JOB_TRIGGER_ON_DEMAND`

Triggered on demand by featureMonitorJobs.create request.

## Methods

### `            create           `

Creates a new feature monitor job.

### `            get           `

Get a feature monitor job.

### `            list           `

List feature monitor jobs.
