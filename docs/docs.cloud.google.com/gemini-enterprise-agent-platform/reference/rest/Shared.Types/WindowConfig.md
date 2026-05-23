---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/WindowConfig
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/WindowConfig
title: WindowConfig
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Config that contains the strategy used to generate sliding windows in time series training. A window is a series of rows that comprise the context up to the time of prediction, and the horizon following. The corresponding row for each window marks the start of the forecast horizon. Each window is used as an input example for training/evaluation.

Fields

`strategy` `Union type`

`strategy` can be only one of the following:

`column` `string`

name of the column that should be used to generate sliding windows. The column should contain either booleans or string booleans; if the value of the row is True, generate a sliding window with the horizon starting at that row. The column will not be used as a feature in training.

`strideLength` `string ( int64 format)`

Stride length used to generate input examples. Within one time series, every {$STRIDE\_LENGTH} rows will be used to generate a sliding window.

`maxCount` `string ( int64 format)`

Maximum number of windows that should be generated across all time series.

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

  // strategy
  &quot;column&quot;: string,
  &quot;strideLength&quot;: string,
  &quot;maxCount&quot;: string
  // Union type
}</code></pre></td>
</tr>
</tbody>
</table>
