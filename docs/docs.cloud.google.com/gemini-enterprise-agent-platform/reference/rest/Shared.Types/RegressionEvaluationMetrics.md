---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/RegressionEvaluationMetrics
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/RegressionEvaluationMetrics
title: RegressionEvaluationMetrics
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Metrics for regression evaluation results.

Fields

`rootMeanSquaredError` `number`

Root Mean Squared Error (RMSE).

`meanAbsoluteError` `number`

Mean Absolute Error (MAE).

`meanAbsolutePercentageError` `number`

Mean absolute percentage error. Infinity when there are zeros in the ground truth.

`rSquared` `number`

Coefficient of determination as Pearson correlation coefficient. Undefined when ground truth or predictions are constant or near constant.

`rootMeanSquaredLogError` `number`

Root mean squared log error. Undefined when there are negative ground truth values or predictions.

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
  &quot;rootMeanSquaredError&quot;: number,
  &quot;meanAbsoluteError&quot;: number,
  &quot;meanAbsolutePercentageError&quot;: number,
  &quot;rSquared&quot;: number,
  &quot;rootMeanSquaredLogError&quot;: number
}</code></pre></td>
</tr>
</tbody>
</table>
