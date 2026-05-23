---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/ForecastingEvaluationMetrics
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/ForecastingEvaluationMetrics
title: ForecastingEvaluationMetrics
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Metrics for forecasting evaluation results.

Fields

`quantileMetrics[]` ` object ( QuantileMetricsEntry  ` )

The quantile metrics entries for each quantile.

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

`weightedAbsolutePercentageError` `number`

Weighted Absolute Percentage Error. Does not use weights, this is just what the metric is called. Undefined if actual values sum to zero. Will be very large if actual values sum to a very small number.

`rootMeanSquaredPercentageError` `number`

Root Mean Square Percentage Error. Square root of MSPE. Undefined/imaginary when MSPE is negative.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;quantileMetrics&quot;: [{object (QuantileMetricsEntry)}],&quot;rootMeanSquaredError&quot;: number,&quot;meanAbsoluteError&quot;: number,&quot;meanAbsolutePercentageError&quot;: number,&quot;rSquared&quot;: number,&quot;rootMeanSquaredLogError&quot;: number,&quot;weightedAbsolutePercentageError&quot;: number,&quot;rootMeanSquaredPercentageError&quot;: number}</code></pre></td>
</tr>
</tbody>
</table>

## QuantileMetricsEntry

Entry for the Quantiles loss type optimization objective.

Fields

`quantile` `number`

The quantile for this entry.

`scaledPinballLoss` `number`

The scaled pinball loss of this quantile.

`observedQuantile` `number`

This is a custom metric that calculates the percentage of true values that were less than the predicted value for that quantile. Only populated when \[optimizationObjective\]\[google.cloud.aiplatform.publicfiles.trainingjob.definition.AutoMlForecastingInputs.optimization\_objective\] is minimize-quantile-loss and each entry corresponds to an entry in \[quantiles\]\[google.cloud.aiplatform.publicfiles.trainingjob.definition.AutoMlForecastingInputs.quantiles\] The percent value can be used to compare with the quantile value, which is the target value.

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
  &quot;quantile&quot;: number,
  &quot;scaledPinballLoss&quot;: number,
  &quot;observedQuantile&quot;: number
}</code></pre></td>
</tr>
</tbody>
</table>
