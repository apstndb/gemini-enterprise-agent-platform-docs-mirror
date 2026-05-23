---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/Measurement
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/Measurement
title: Measurement
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

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

## Metric

A message representing a metric in the measurement.

Fields

`metricId` `string`

Output only. The id of the Metric. The Metric should be defined in `  StudySpec's Metrics  ` .

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
