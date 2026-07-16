---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.onlineEvaluators
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.onlineEvaluators
title: 'REST Resource: projects.locations.onlineEvaluators'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

## Resource: OnlineEvaluator

An OnlineEvaluator contains the configuration for an Online Evaluation.

Fields

`name` `string`

Identifier. The resource name of the OnlineEvaluator. Format: projects/{project}/locations/{location}/onlineEvaluators/{id}.

`agentResource` `string`

Required. Immutable. The name of the agent that the OnlineEvaluator evaluates periodically. This value is used to filter the traces with a matching cloud.resource\_id and link the evaluation results with relevant dashboards/UIs.

This field is immutable. Once set, it cannot be changed.

`metricSources[]` ` object ( MetricSource  ` )

Required. A list of metric sources to be used for evaluating samples. At least one MetricSource must be provided. Right now, only predefined metrics and registered metrics are supported.

Every registered metric must have `displayName` (or `title` ) and `scoreRange` defined. Otherwise, the evaluations will fail.

The maximum number of `metricSources` is 25.

`config` ` object ( Config  ` )

Required. Configuration for the OnlineEvaluator.

`state` ` enum ( State  ` )

Output only. The state of the OnlineEvaluator.

`stateDetails[]` ` object ( StateDetails  ` )

Output only. Contains additional information about the state of the OnlineEvaluator. This is used to provide more details in the event of a failure.

`createTime` ` string ( Timestamp  ` format)

Output only. timestamp when the OnlineEvaluator was created.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`updateTime` ` string ( Timestamp  ` format)

Output only. timestamp when the OnlineEvaluator was last updated.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .

`displayName` `string`

Optional. Human-readable name for the OnlineEvaluator.

The name doesn't have to be unique.

The name can consist of any UTF-8 characters. The maximum length is `63` characters. If the display name exceeds max characters, an `INVALID_ARGUMENT` error is returned.

`data_source` `Union type`

Required. The data source used to query samples for evaluations. More data sources will be supported in the future.

This field is immutable. Once set, it cannot be changed. `data_source` can be only one of the following:

`cloudObservability` ` object ( CloudObservability  ` )

data source for the OnlineEvaluator, based on Google Cloud Observability stack (Cloud Trace & Cloud Logging).

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;name&quot;: string,&quot;agentResource&quot;: string,&quot;metricSources&quot;: [{object (MetricSource)}],&quot;config&quot;: {object (Config)},&quot;state&quot;: enum (State),&quot;stateDetails&quot;: [{object (StateDetails)}],&quot;createTime&quot;: string,&quot;updateTime&quot;: string,&quot;displayName&quot;: string,// data_source&quot;cloudObservability&quot;: {object (CloudObservability)}// Union type}</code></pre></td>
</tr>
</tbody>
</table>

## CloudObservability

data source for the OnlineEvaluator, based on Google Cloud Observability stack (Cloud Trace & Cloud Logging).

Fields

`logView` `string`

Optional. Optional log view that will be used to query logs. If empty, the `_Default` view will be used.

`traceView` `string`

Optional. Optional trace view that will be used to query traces. If empty, the `_Default` view will be used.

NOTE: This field is not supported yet and will be ignored if set.

`eval_scope` `Union type`

Required. Defines the scope of data to be evaluated. `eval_scope` can be only one of the following:

`traceScope` ` object ( TraceScope  ` )

scope online evaluation to single traces.

`convention` `Union type`

Required. Defines which convention the data source follows. `convention` can be only one of the following:

`openTelemetry` ` object ( OpenTelemetry  ` )

data source follows OpenTelemetry convention.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;logView&quot;: string,&quot;traceView&quot;: string,// eval_scope&quot;traceScope&quot;: {object (TraceScope)}// Union type// convention&quot;openTelemetry&quot;: {object (OpenTelemetry)}// Union type}</code></pre></td>
</tr>
</tbody>
</table>

## TraceScope

If chosen, the online evaluator will evaluate single traces matching specified `filter` .

Fields

`filter[]` ` object ( Predicate  ` )

Optional. A list of predicates to filter traces. Multiple predicates are combined using AND.

The maximum number of predicates is 10.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;filter&quot;: [{object (Predicate)}]}</code></pre></td>
</tr>
</tbody>
</table>

## Predicate

Defines a single filter predicate.

Fields

`predicate` `Union type`

The type of predicate. `predicate` can be only one of the following:

`duration` ` object ( NumericPredicate  ` )

Filter on the duration of a trace.

`totalTokenUsage` ` object ( NumericPredicate  ` )

Filter on the total token usage within a trace.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{// predicate&quot;duration&quot;: {object (NumericPredicate)},&quot;totalTokenUsage&quot;: {object (NumericPredicate)}// Union type}</code></pre></td>
</tr>
</tbody>
</table>

## NumericPredicate

Defines a predicate for filtering based on a numeric value.

Fields

`comparisonOperator` ` enum ( ComparisonOperator  ` )

Required. The comparison operator to apply.

`value` `number`

Required. The value to compare against.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;comparisonOperator&quot;: enum (ComparisonOperator),&quot;value&quot;: number}</code></pre></td>
</tr>
</tbody>
</table>

## ComparisonOperator

Comparison operators for numeric predicates.

Enums

`COMPARISON_OPERATOR_UNSPECIFIED`

Unspecified comparison operator. This value should not be used.

`LESS`

Less than.

`LESS_OR_EQUAL`

Less than or equal to.

`EQUAL`

Equal to.

`NOT_EQUAL`

Not equal to.

`GREATER_OR_EQUAL`

Greater than or equal to.

`GREATER`

Greater than.

## OpenTelemetry

Configuration for data source following OpenTelemetry.

Fields

`semconvVersion` `string`

Required. Defines which version OTel Semantic Convention the data follows. Can be "1.39.0" or newer.

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
  &quot;semconvVersion&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

## MetricSource

The metric source used for evaluation.

Fields

`metric_source` `Union type`

The source of the metric. `metric_source` can be only one of the following:

`metric` ` object ( Metric  ` )

Inline metric config.

`metricResourceName` `string`

Optional. Resource name for registered metric.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{// metric_source&quot;metric&quot;: {object (Metric)},&quot;metricResourceName&quot;: string// Union type}</code></pre></td>
</tr>
</tbody>
</table>

## Config

Configuration for sampling behavior of the OnlineEvaluator. The OnlineEvaluator runs at a fixed interval of 10 minutes.

Fields

`maxEvaluatedSamplesPerRun` `string ( int64 format)`

Optional. The maximum number of evaluations to perform per run. If set to 0, the number is unbounded.

`sampling_method` `Union type`

Required. The sampling method used to select traces for evaluation. `sampling_method` can be only one of the following:

`randomSampling` ` object ( RandomSampling  ` )

Random sampling method.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;maxEvaluatedSamplesPerRun&quot;: string,// sampling_method&quot;randomSampling&quot;: {object (RandomSampling)}// Union type}</code></pre></td>
</tr>
</tbody>
</table>

## RandomSampling

Configuration for random sampling.

Fields

`percentage` `integer`

Required. The percentage of traces to sample for evaluation. Must be an integer between `1` and `100` .

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
  &quot;percentage&quot;: integer
}</code></pre></td>
</tr>
</tbody>
</table>

## State

The state of the OnlineEvaluator.

Enums

`STATE_UNSPECIFIED`

Default value.

`ACTIVE`

Indicates that the OnlineEvaluator is active.

`SUSPENDED`

Indicates that the OnlineEvaluator is suspended. In this state, the OnlineEvaluator will not evaluate any samples.

`FAILED`

Indicates that the OnlineEvaluator is in a failed state.

This can happen if, for example, the `logView` or `traceView` set on the `CloudObservability` does not exist.

`WARNING`

Indicates that the OnlineEvaluator is in a warning state. This can happen if, for example, some of the metrics in the `metricSources` are invalid. Evaluation will still run with the remaining valid metrics.

## StateDetails

Contains additional information about the state of the OnlineEvaluator.

Fields

`message` `string`

Output only. Human-readable message describing the state of the OnlineEvaluator.

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
  &quot;message&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

## Methods

### `            activate           `

Activates an OnlineEvaluator.

### `            create           `

Creates an OnlineEvaluator in the given project and location.

### `            delete           `

Deletes an OnlineEvaluator.

### `            get           `

Gets details of an OnlineEvaluator.

### `            list           `

Lists the OnlineEvaluators for the given project and location.

### `            patch           `

Updates the fields of an OnlineEvaluator.

### `            suspend           `

Suspends an OnlineEvaluator.
