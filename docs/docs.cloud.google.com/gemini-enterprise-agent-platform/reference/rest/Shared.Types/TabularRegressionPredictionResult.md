---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/TabularRegressionPredictionResult
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/TabularRegressionPredictionResult
title: TabularRegressionPredictionResult
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Prediction output format for Tabular Regression.

Fields

`value` `number`

The regression value.

`lowerBound` `number`

The lower bound of the prediction interval.

`upperBound` `number`

The upper bound of the prediction interval.

`quantileValues[]` `number`

Quantile values.

`quantilePredictions[]` `number`

Quantile predictions, in 1-1 correspondence with quantileValues.

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
  &quot;value&quot;: number,
  &quot;lowerBound&quot;: number,
  &quot;upperBound&quot;: number,
  &quot;quantileValues&quot;: [
    number
  ],
  &quot;quantilePredictions&quot;: [
    number
  ]
}</code></pre></td>
</tr>
</tbody>
</table>
