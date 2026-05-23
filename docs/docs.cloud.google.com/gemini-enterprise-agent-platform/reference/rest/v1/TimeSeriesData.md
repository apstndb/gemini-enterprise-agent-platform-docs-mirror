---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/TimeSeriesData
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/TimeSeriesData
title: TimeSeriesData
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

All the data stored in a TensorboardTimeSeries.

Fields

`tensorboardTimeSeriesId` `string`

Required. The id of the TensorboardTimeSeries, which will become the final component of the TensorboardTimeSeries' resource name

`valueType` ` enum ( ValueType  ` )

Required. Immutable. The value type of this time series. All the values in this time series data must match this value type.

`values[]` ` object ( TimeSeriesDataPoint  ` )

Required. data points in this time series.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;tensorboardTimeSeriesId&quot;: string,&quot;valueType&quot;: enum (ValueType),&quot;values&quot;: [{object (TimeSeriesDataPoint)}]}</code></pre></td>
</tr>
</tbody>
</table>
