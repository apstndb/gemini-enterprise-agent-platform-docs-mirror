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

`nasJobSpec` ` object ( NasJobSpec  ` )

Required. The specification of a NasJob.

`nasJobOutput` ` object ( NasJobOutput  ` )

Output only. Output of the NasJob.

`state` ` enum ( JobState  ` )

Output only. The detailed state of the job.

`createTime` ` string ( Timestamp  ` format)

Output only. time when the NasJob was created.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`startTime` ` string ( Timestamp  ` format)

Output only. time when the NasJob for the first time entered the `JOB_STATE_RUNNING` state.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`endTime` ` string ( Timestamp  ` format)

Output only. time when the NasJob entered any of the following states: `JOB_STATE_SUCCEEDED` , `JOB_STATE_FAILED` , `JOB_STATE_CANCELLED` .

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`updateTime` ` string ( Timestamp  ` format)

Output only. time when the NasJob was most recently updated.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`error` ` object ( Status  ` )

Output only. Only populated when job's state is JOB\_STATE\_FAILED or JOB\_STATE\_CANCELLED.

`labels` `map (key: string, value: string)`

The labels with user-defined metadata to organize NasJobs.

label keys and values can be no longer than 64 characters (Unicode codepoints), can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed.

See <https://goo.gl/xmQnxf> for more information and examples of labels.

`encryptionSpec` ` object ( EncryptionSpec  ` )

Customer-managed encryption key options for a NasJob. If this is set, then all resources created by the NasJob will be encrypted with the provided encryption key.

` enableRestrictedImageTraining (deprecated)  ` `boolean`

> This item is deprecated\!

Optional. Enable a separation of Custom model training and restricted image training for tenant project.

`satisfiesPzs` `boolean`

Output only. reserved for future use.

`satisfiesPzi` `boolean`

Output only. reserved for future use.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;name&quot;: string,&quot;displayName&quot;: string,&quot;nasJobSpec&quot;: {object (NasJobSpec)},&quot;nasJobOutput&quot;: {object (NasJobOutput)},&quot;state&quot;: enum (JobState),&quot;createTime&quot;: string,&quot;startTime&quot;: string,&quot;endTime&quot;: string,&quot;updateTime&quot;: string,&quot;error&quot;: {object (Status)},&quot;labels&quot;: {string: string,...},&quot;encryptionSpec&quot;: {object (EncryptionSpec)},&quot;enableRestrictedImageTraining&quot;: boolean,&quot;satisfiesPzs&quot;: boolean,&quot;satisfiesPzi&quot;: boolean}</code></pre></td>
</tr>
</tbody>
</table>

## NasJobSpec

Represents the spec of a NasJob.

Fields

`resumeNasJobId` `string`

The id of the existing NasJob in the same Project and Location which will be used to resume search. searchSpaceSpec and nas\_algorithm\_spec are obtained from previous NasJob hence should not provide them again for this NasJob.

`searchSpaceSpec` `string`

It defines the search space for Neural Architecture Search (NAS).

`nas_algorithm_spec` `Union type`

The Neural Architecture Search (NAS) algorithm specification. `nas_algorithm_spec` can be only one of the following:

`multiTrialAlgorithmSpec` ` object ( MultiTrialAlgorithmSpec  ` )

The spec of multi-trial algorithms.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;resumeNasJobId&quot;: string,&quot;searchSpaceSpec&quot;: string,// nas_algorithm_spec&quot;multiTrialAlgorithmSpec&quot;: {object (MultiTrialAlgorithmSpec)}// Union type}</code></pre></td>
</tr>
</tbody>
</table>

## MultiTrialAlgorithmSpec

The spec of multi-trial Neural Architecture Search (NAS).

Fields

`multiTrialAlgorithm` ` enum ( MultiTrialAlgorithm  ` )

The multi-trial Neural Architecture Search (NAS) algorithm type. Defaults to `REINFORCEMENT_LEARNING` .

`metric` ` object ( MetricSpec  ` )

Metric specs for the NAS job. Validation for this field is done at `multiTrialAlgorithmSpec` field.

`searchTrialSpec` ` object ( SearchTrialSpec  ` )

Required. Spec for search trials.

`trainTrialSpec` ` object ( TrainTrialSpec  ` )

Spec for train trials. top N \[TrainTrialSpec.max\_parallel\_trial\_count\] search trials will be trained for every M \[TrainTrialSpec.frequency\] trials searched.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;multiTrialAlgorithm&quot;: enum (MultiTrialAlgorithm),&quot;metric&quot;: {object (MetricSpec)},&quot;searchTrialSpec&quot;: {object (SearchTrialSpec)},&quot;trainTrialSpec&quot;: {object (TrainTrialSpec)}}</code></pre></td>
</tr>
</tbody>
</table>

## MultiTrialAlgorithm

The available types of multi-trial algorithms.

Enums

`MULTI_TRIAL_ALGORITHM_UNSPECIFIED`

Defaults to `REINFORCEMENT_LEARNING` .

`REINFORCEMENT_LEARNING`

The Reinforcement Learning algorithm for Multi-trial Neural Architecture Search (NAS).

`GRID_SEARCH`

The Grid Search algorithm for Multi-trial Neural Architecture Search (NAS).

## MetricSpec

Represents a metric to optimize.

Fields

`metricId` `string`

Required. The id of the metric. Must not contain whitespaces.

`goal` ` enum ( GoalType  ` )

Required. The optimization goal of the metric.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;metricId&quot;: string,&quot;goal&quot;: enum (GoalType)}</code></pre></td>
</tr>
</tbody>
</table>

## GoalType

The available types of optimization goals.

Enums

`GOAL_TYPE_UNSPECIFIED`

Goal type will default to maximize.

`MAXIMIZE`

Maximize the goal metric.

`MINIMIZE`

Minimize the goal metric.

## SearchTrialSpec

Represent spec for search trials.

Fields

`searchTrialJobSpec` ` object ( CustomJobSpec  ` )

Required. The spec of a search trial job. The same spec applies to all search trials.

`maxTrialCount` `integer`

Required. The maximum number of Neural Architecture Search (NAS) trials to run.

`maxParallelTrialCount` `integer`

Required. The maximum number of trials to run in parallel.

`maxFailedTrialCount` `integer`

The number of failed trials that need to be seen before failing the NasJob.

If set to 0, Agent Platform decides how many trials must fail before the whole job fails.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;searchTrialJobSpec&quot;: {object (CustomJobSpec)},&quot;maxTrialCount&quot;: integer,&quot;maxParallelTrialCount&quot;: integer,&quot;maxFailedTrialCount&quot;: integer}</code></pre></td>
</tr>
</tbody>
</table>

## TrainTrialSpec

Represent spec for train trials.

Fields

`trainTrialJobSpec` ` object ( CustomJobSpec  ` )

Required. The spec of a train trial job. The same spec applies to all train trials.

`maxParallelTrialCount` `integer`

Required. The maximum number of trials to run in parallel.

`frequency` `integer`

Required. Frequency of search trials to start train stage. top N \[TrainTrialSpec.max\_parallel\_trial\_count\] search trials will be trained for every M \[TrainTrialSpec.frequency\] trials searched.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;trainTrialJobSpec&quot;: {object (CustomJobSpec)},&quot;maxParallelTrialCount&quot;: integer,&quot;frequency&quot;: integer}</code></pre></td>
</tr>
</tbody>
</table>

## NasJobOutput

Represents a uCAIP NasJob output.

Fields

`output` `Union type`

The output of this Neural Architecture Search (NAS) job. `output` can be only one of the following:

`multiTrialJobOutput` ` object ( MultiTrialJobOutput  ` )

Output only. The output of this multi-trial Neural Architecture Search (NAS) job.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{// output&quot;multiTrialJobOutput&quot;: {object (MultiTrialJobOutput)}// Union type}</code></pre></td>
</tr>
</tbody>
</table>

## MultiTrialJobOutput

The output of a multi-trial Neural Architecture Search (NAS) jobs.

Fields

`searchTrials[]` ` object ( NasTrial  ` )

Output only. List of NasTrials that were started as part of search stage.

`trainTrials[]` ` object ( NasTrial  ` )

Output only. List of NasTrials that were started as part of train stage.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;searchTrials&quot;: [{object (NasTrial)}],&quot;trainTrials&quot;: [{object (NasTrial)}]}</code></pre></td>
</tr>
</tbody>
</table>

## Methods

### `            cancel           `

Cancels a NasJob.

### `            create           `

Creates a NasJob

### `            delete           `

Deletes a NasJob.

### `            get           `

Gets a NasJob

### `            list           `

Lists NasJobs in a Location.
