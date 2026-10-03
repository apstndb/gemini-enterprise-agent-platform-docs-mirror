---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/PairwiseTextGenerationEvaluationMetrics
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/PairwiseTextGenerationEvaluationMetrics
title: PairwiseTextGenerationEvaluationMetrics
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Metrics for general pairwise text generation evaluation results.

Fields

`modelWinRate` `number`

Percentage of time the autorater decided the model had the better response.

`baselineModelWinRate` `number`

Percentage of time the autorater decided the baseline model had the better response.

`humanPreferenceModelWinRate` `number`

Percentage of time humans decided the model had the better response.

`humanPreferenceBaselineModelWinRate` `number`

Percentage of time humans decided the baseline model had the better response.

`truePositiveCount` `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)`

Number of examples where both the autorater and humans decided that the model had the better response.

`falsePositiveCount` `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)`

Number of examples where the autorater chose the model, but humans preferred the baseline model.

`falseNegativeCount` `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)`

Number of examples where the autorater chose the baseline model, but humans preferred the model.

`trueNegativeCount` `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)`

Number of examples where both the autorater and humans decided that the model had the worse response.

`accuracy` `number`

Fraction of cases where the autorater agreed with the human raters.

`precision` `number`

Fraction of cases where the autorater and humans thought the model had a better response out of all cases where the autorater thought the model had a better response. True positive divided by all positive.

`recall` `number`

Fraction of cases where the autorater and humans thought the model had a better response out of all cases where the humans thought the model had a better response.

`f1Score` `number`

Harmonic mean of precision and recall.

`cohensKappa` `number`

A measurement of agreement between the autorater and human raters that takes the likelihood of random agreement into account.

**JSON representation**

```
{
  "modelWinRate": number,
  "baselineModelWinRate": number,
  "humanPreferenceModelWinRate": number,
  "humanPreferenceBaselineModelWinRate": number,
  "truePositiveCount": string,
  "falsePositiveCount": string,
  "falseNegativeCount": string,
  "trueNegativeCount": string,
  "accuracy": number,
  "precision": number,
  "recall": number,
  "f1Score": number,
  "cohensKappa": number
}
```
