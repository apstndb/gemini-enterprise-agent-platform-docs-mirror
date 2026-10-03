---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/TrackMetrics
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/TrackMetrics
title: TrackMetrics
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

UNIMPLEMENTED. Track matching model metrics for a single track match threshold and multiple label match confidence thresholds.

Fields

`confidenceMetrics[]` `object ( `[`ConfidenceMetrics`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/TrackMetrics#ConfidenceMetrics)` )`

Metrics for each label-match `confidenceThreshold` from 0.05,0.10,...,0.95,0.96,0.97,0.98,0.99. Precision-recall curve is derived from them.

`iouThreshold` `number`

The intersection-over-union threshold value between bounding boxes across frames used to compute this metric entry.

`meanTrackingAveragePrecision` `number`

The mean average precision over all confidence thresholds.

`meanBoundingBoxIou` `number`

The mean bounding box iou over all confidence thresholds.

`meanMismatchRate` `number`

The mean mismatch rate over all confidence thresholds.

**JSON representation**

```
{
  "confidenceMetrics": [
    {
      object (ConfidenceMetrics)
    }
  ],
  "iouThreshold": number,
  "meanTrackingAveragePrecision": number,
  "meanBoundingBoxIou": number,
  "meanMismatchRate": number
}
```

## ConfidenceMetrics

Metrics for a single confidence threshold.

Fields

`confidenceThreshold` `number`

The confidence threshold value used to compute the metrics.

`trackingPrecision` `number`

Tracking precision.

`trackingRecall` `number`

Tracking recall.

`boundingBoxIou` `number`

Bounding box intersection-over-union precision. Measures how well the bounding boxes overlap between each other (e.g. complete overlap or just barely above iouThreshold).

`mismatchRate` `number`

Mismatch rate, which measures the tracking consistency, i.e. correctness of instance id continuity.

**JSON representation**

```
{
  "confidenceThreshold": number,
  "trackingPrecision": number,
  "trackingRecall": number,
  "boundingBoxIou": number,
  "mismatchRate": number
}
```
