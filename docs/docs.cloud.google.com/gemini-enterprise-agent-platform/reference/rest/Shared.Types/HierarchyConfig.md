---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/HierarchyConfig
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/HierarchyConfig
title: HierarchyConfig
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Configuration that defines the hierarchical relationship of time series and parameters for hierarchical forecasting strategies.

Fields

`groupColumns[]` `string`

A list of time series attribute column names that define the time series hierarchy. Only one level of hierarchy is supported, ex. 'region' for a hierarchy of stores or 'department' for a hierarchy of products. If multiple columns are specified, time series will be grouped by their combined values, ex. ('blue', 'large') for 'color' and 'size', up to 5 columns are accepted. If no group columns are specified, all time series are considered to be part of the same group.

`groupTotalWeight` `number`

The weight of the loss for predictions aggregated over time series in the same group.

`temporalTotalWeight` `number`

The weight of the loss for predictions aggregated over the horizon for a single time series.

`groupTemporalTotalWeight` `number`

The weight of the loss for predictions aggregated over both the horizon and time series in the same hierarchy group.

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
  &quot;groupColumns&quot;: [
    string
  ],
  &quot;groupTotalWeight&quot;: number,
  &quot;temporalTotalWeight&quot;: number,
  &quot;groupTemporalTotalWeight&quot;: number
}</code></pre></td>
</tr>
</tbody>
</table>
