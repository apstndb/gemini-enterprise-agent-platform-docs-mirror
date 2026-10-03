---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/TimeSeriesForecastingPredictionResult
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/TimeSeriesForecastingPredictionResult
title: TimeSeriesForecastingPredictionResult
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Prediction output format for time Series Forecasting.

Fields

`value` `number`

The regression value.

`quantileValues[]` `number`

Quantile values.

`quantilePredictions[]` `number`

Quantile predictions, in 1-1 correspondence with quantileValues.

`tftFeatureImportance` `object ( `[`TftFeatureImportance`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/TftFeatureImportance)` )`

Only use these if TFt is enabled.

**JSON representation**

```
{
  "value": number,
  "quantileValues": [
    number
  ],
  "quantilePredictions": [
    number
  ],
  "tftFeatureImportance": {
    object (TftFeatureImportance)
  }
}
```
