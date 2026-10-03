---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/VideoActionMetrics
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/VideoActionMetrics
title: VideoActionMetrics
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

The Evaluation metrics given a specific [`precisionWindowLength`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/VideoActionMetrics#FIELDS.precision_window_length) .

Fields

`confidenceMetrics[]` `object ( `[`ConfidenceMetrics`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/VideoActionMetrics#ConfidenceMetrics)` )`

Metrics for each label-match confidenceThreshold from 0.05,0.10,...,0.95,0.96,0.97,0.98,0.99.

`precisionWindowLength` `string ( `[`Duration`](https://protobuf.dev/reference/protobuf/google.protobuf/#duration)` format)`

This [`VideoActionMetrics`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/VideoActionMetrics) is calculated based on this prediction window length. If the predicted action's timestamp is inside the time window whose center is the ground truth action's timestamp with this specific length, the prediction result is treated as a true positive.

A duration in seconds with up to nine fractional digits, ending with ' `s` '. Example: `"3.5s"` .

`meanAveragePrecision` `number`

The mean average precision.

**JSON representation**

```
{
  "confidenceMetrics": [
    {
      object (ConfidenceMetrics)
    }
  ],
  "precisionWindowLength": string,
  "meanAveragePrecision": number
}
```

## ConfidenceMetrics

Metrics for a single confidence threshold.

Fields

`confidenceThreshold` `number`

Output only. The confidence threshold value used to compute the metrics.

`recall` `number`

Output only. Recall for the given confidence threshold.

`precision` `number`

Output only. Precision for the given confidence threshold.

`f1Score` `number`

Output only. The harmonic mean of recall and precision.

**JSON representation**

```
{
  "confidenceThreshold": number,
  "recall": number,
  "precision": number,
  "f1Score": number
}
```
