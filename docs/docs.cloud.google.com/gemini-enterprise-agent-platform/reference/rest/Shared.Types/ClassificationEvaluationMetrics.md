---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/ClassificationEvaluationMetrics
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/ClassificationEvaluationMetrics
title: ClassificationEvaluationMetrics
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Metrics for classification evaluation results.

Fields

`confidenceMetrics[]` `object ( `[`ConfidenceMetrics`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/ClassificationEvaluationMetrics#ConfidenceMetrics)` )`

Metrics for each `confidenceThreshold` in 0.00,0.05,0.10,...,0.95,0.96,0.97,0.98,0.99 and `positionThreshold` = INT32_MAX_VALUE.

ROC and precision-recall curves, and other aggregated metrics are derived from them. The confidence metrics entries may also be supplied for additional values of `positionThreshold` , but from these no aggregated metrics are computed.

`confusionMatrix` `object ( `[`ConfusionMatrix`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/ConfusionMatrix)` )`

Confusion matrix of the evaluation.

`auPrc` `number`

The Area Under Precision-Recall Curve metric. Micro-averaged for the overall evaluation.

`auRoc` `number`

The Area Under Receiver Operating Characteristic curve metric. Micro-averaged for the overall evaluation.

`logLoss` `number`

The log Loss metric.

**JSON representation**

```
{
  "confidenceMetrics": [
    {
      object (ConfidenceMetrics)
    }
  ],
  "confusionMatrix": {
    object (ConfusionMatrix)
  },
  "auPrc": number,
  "auRoc": number,
  "logLoss": number
}
```

## ConfidenceMetrics

Fields

`confusionMatrix` `object ( `[`ConfusionMatrix`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/ConfusionMatrix)` )`

Confusion matrix of the evaluation for this confidenceThreshold.

`confidenceThreshold` `number`

Metrics are computed with an assumption that the Model never returns predictions with score lower than this value.

`maxPredictions` `integer`

Metrics are computed with an assumption that the Model always returns at most this many predictions (ordered by their score, descendingly), but they all still need to meet the `confidenceThreshold` .

`recall` `number`

Recall (True Positive Rate) for the given confidence threshold.

`precision` `number`

Precision for the given confidence threshold.

`falsePositiveRate` `number`

False Positive Rate for the given confidence threshold.

`f1Score` `number`

The harmonic mean of recall and precision. For summary metrics, it computes the micro-averaged F1 score.

`f1ScoreMicro` `number`

Micro-averaged F1 Score.

`f1ScoreMacro` `number`

Macro-averaged F1 Score.

`recallAt1` `number`

The Recall (True Positive Rate) when only considering the label that has the highest prediction score and not below the confidence threshold for each DataItem.

`precisionAt1` `number`

The precision when only considering the label that has the highest prediction score and not below the confidence threshold for each DataItem.

`falsePositiveRateAt1` `number`

The False Positive Rate when only considering the label that has the highest prediction score and not below the confidence threshold for each DataItem.

`f1ScoreAt1` `number`

The harmonic mean of recallAt1 and precisionAt1.

`truePositiveCount` `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)`

The number of Model created labels that match a ground truth label.

`falsePositiveCount` `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)`

The number of Model created labels that do not match a ground truth label.

`falseNegativeCount` `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)`

The number of ground truth labels that are not matched by a Model created label.

`trueNegativeCount` `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)`

The number of labels that were not created by the Model, but if they would, they would not match a ground truth label.

**JSON representation**

```
{
  "confusionMatrix": {
    object (ConfusionMatrix)
  },
  "confidenceThreshold": number,
  "maxPredictions": integer,
  "recall": number,
  "precision": number,
  "falsePositiveRate": number,
  "f1Score": number,
  "f1ScoreMicro": number,
  "f1ScoreMacro": number,
  "recallAt1": number,
  "precisionAt1": number,
  "falsePositiveRateAt1": number,
  "f1ScoreAt1": number,
  "truePositiveCount": string,
  "falsePositiveCount": string,
  "falseNegativeCount": string,
  "trueNegativeCount": string
}
```
