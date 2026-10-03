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

**JSON representation**

```
{
  "rootMeanSquaredError": number,
  "meanAbsoluteError": number,
  "meanAbsolutePercentageError": number,
  "rSquared": number,
  "rootMeanSquaredLogError": number
}
```
