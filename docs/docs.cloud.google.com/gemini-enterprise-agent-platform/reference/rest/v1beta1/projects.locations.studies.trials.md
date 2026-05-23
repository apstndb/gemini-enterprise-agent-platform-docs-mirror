---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.studies.trials
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.studies.trials
title: 'REST Resource: projects.locations.studies.trials'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

## Resource: Trial

A message representing a Trial. A Trial contains a unique set of Parameters that has been or will be evaluated, along with the objective metrics got by running the Trial.

Fields

`name` `string`

Output only. Resource name of the Trial assigned by the service.

`id` `string`

Output only. The identifier of the Trial assigned by the service.

`state` ` enum ( State  ` )

Output only. The detailed state of the Trial.

`parameters[]` ` object ( Parameter  ` )

Output only. The parameters of the Trial.

`finalMeasurement` ` object ( Measurement  ` )

Output only. The final measurement containing the objective value.

`measurements[]` ` object ( Measurement  ` )

Output only. A list of measurements that are strictly lexicographically ordered by their induced tuples (steps, elapsedDuration). These are used for early stopping computations.

`startTime` ` string ( Timestamp  ` format)

Output only. time when the Trial was started.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`endTime` ` string ( Timestamp  ` format)

Output only. time when the Trial's status changed to `SUCCEEDED` or `INFEASIBLE` .

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`clientId` `string`

Output only. The identifier of the client that originally requested this Trial. Each client is identified by a unique clientId. When a client asks for a suggestion, Agent Platform Vizier will assign it a Trial. The client should evaluate the Trial, complete it, and report back to Agent Platform Vizier. If suggestion is asked again by same clientId before the Trial is completed, the same Trial will be returned. Multiple clients with different client\_ids can ask for suggestions simultaneously, each of them will get their own Trial.

`infeasibleReason` `string`

Output only. A human readable string describing why the Trial is infeasible. This is set only if Trial state is `INFEASIBLE` .

`customJob` `string`

Output only. The CustomJob name linked to the Trial. It's set for a HyperparameterTuningJob's Trial.

`webAccessUris` `map (key: string, value: string)`

Output only. URIs for accessing [interactive shells](https://cloud.google.com/vertex-ai/docs/training/monitor-debug-interactive-shell) (one URI for each training node). Only available if this trial is part of a `  HyperparameterTuningJob  ` and the job's `trialJobSpec.enable_web_access` field is `true` .

The keys are names of each node used for the trial; for example, `workerpool0-0` for the primary node, `workerpool1-0` for the first node in the second worker pool, and `workerpool1-1` for the second node in the second worker pool.

The values are the URIs for each node's interactive shell.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;name&quot;: string,&quot;id&quot;: string,&quot;state&quot;: enum (State),&quot;parameters&quot;: [{object (Parameter)}],&quot;finalMeasurement&quot;: {object (Measurement)},&quot;measurements&quot;: [{object (Measurement)}],&quot;startTime&quot;: string,&quot;endTime&quot;: string,&quot;clientId&quot;: string,&quot;infeasibleReason&quot;: string,&quot;customJob&quot;: string,&quot;webAccessUris&quot;: {string: string,...}}</code></pre></td>
</tr>
</tbody>
</table>

### State

Describes a Trial state.

Enums

`STATE_UNSPECIFIED`

The Trial state is unspecified.

`REQUESTED`

Indicates that a specific Trial has been requested, but it has not yet been suggested by the service.

`ACTIVE`

Indicates that the Trial has been suggested.

`STOPPING`

Indicates that the Trial should stop according to the service.

`SUCCEEDED`

Indicates that the Trial is completed successfully.

`INFEASIBLE`

Indicates that the Trial should not be attempted again. The service will set a Trial to INFEASIBLE when it's done but missing the finalMeasurement.

### Parameter

A message representing a parameter to be tuned.

Fields

`parameterId` `string`

Output only. The id of the parameter. The parameter should be defined in `StudySpec's Parameters` .

`value` ` value ( Value  ` format)

Output only. The value of the parameter. `numberValue` will be set if a parameter defined in StudySpec is in type 'INTEGER', 'DOUBLE' or 'DISCRETE'. `stringValue` will be set if a parameter defined in StudySpec is in type 'CATEGORICAL'.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;parameterId&quot;: string,
  &quot;value&quot;: value
}</code></pre></td>
</tr>
</tbody>
</table>

### Measurement

A message representing a Measurement of a Trial. A Measurement contains the Metrics got by executing a Trial using suggested hyperparameter values.

Fields

`elapsedDuration` ` string ( Duration  ` format)

Output only. time that the Trial has been running at the point of this Measurement.

A duration in seconds with up to nine fractional digits, ending with ' `s` '. Example: `"3.5s"` .

`stepCount` `string ( int64 format)`

Output only. The number of steps the machine learning model has been trained for. Must be non-negative.

`metrics[]` ` object ( Metric  ` )

Output only. A list of metrics got by evaluating the objective functions using suggested Parameter values.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;elapsedDuration&quot;: string,&quot;stepCount&quot;: string,&quot;metrics&quot;: [{object (Metric)}]}</code></pre></td>
</tr>
</tbody>
</table>

### Metric

A message representing a metric in the measurement.

Fields

`metricId` `string`

Output only. The id of the Metric. The Metric should be defined in `StudySpec's Metrics` .

`value` `number`

Output only. The value for this metric.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;metricId&quot;: string,
  &quot;value&quot;: number
}</code></pre></td>
</tr>
</tbody>
</table>

## Methods

### `            addTrialMeasurement           `

Adds a measurement of the objective metrics to a Trial.

### `            checkTrialEarlyStoppingState           `

Checks whether a Trial should stop or not.

### `            complete           `

Marks a Trial as complete.

### `            create           `

Adds a user provided Trial to a Study.

### `            delete           `

Deletes a Trial.

### `            get           `

Gets a Trial.

### `            list           `

Lists the Trials associated with a Study.

### `            listOptimalTrials           `

Lists the pareto-optimal Trials for multi-objective Study or the optimal Trials for single-objective Study.

### `            stop           `

Stops a Trial.

### `            suggest           `

Adds one or more Trials to a Study, with parameter values suggested by Agent Platform Vizier.
