---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/TextExtractionEvaluationMetrics
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/TextExtractionEvaluationMetrics
title: TextExtractionEvaluationMetrics
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Metrics for text extraction evaluation results.

Fields

`confidenceMetrics[]` `object ( `[`ConfidenceMetrics`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/TextExtractionEvaluationMetrics#ConfidenceMetrics)` )`

Metrics that have confidence thresholds. Precision-recall curve can be derived from them.

`confusionMatrix` `object ( `[`ConfusionMatrix`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/ConfusionMatrix)` )`

Confusion matrix of the evaluation. Only set for Models where number of AnnotationSpecs is no more than 10. Only set for ModelEvaluations, not for ModelEvaluationSlices.

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
  }
}
```

## ConfidenceMetrics

Fields

`confidenceThreshold` `number`

Metrics are computed with an assumption that the Model never returns predictions with score lower than this value.

`recall` `number`

Recall (True Positive Rate) for the given confidence threshold.

`precision` `number`

Precision for the given confidence threshold.

`f1Score` `number`

The harmonic mean of recall and precision.

**JSON representation**

```
{
  "confidenceThreshold": number,
  "recall": number,
  "precision": number,
  "f1Score": number
}
```
