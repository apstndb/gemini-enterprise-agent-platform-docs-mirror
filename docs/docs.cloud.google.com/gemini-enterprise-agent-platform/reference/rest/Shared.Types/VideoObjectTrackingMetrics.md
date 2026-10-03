---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/VideoObjectTrackingMetrics
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/VideoObjectTrackingMetrics
title: VideoObjectTrackingMetrics
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Model evaluation metrics for video object tracking problems. Evaluates prediction quality of both labeled bounding boxes and labeled tracks (i.e. series of bounding boxes sharing same label and instance id).

Fields

`boundingBoxMetrics[]` `object ( `[`BoundingBoxMetrics`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/BoundingBoxMetrics)` )`

The bounding boxes match metrics for each intersection-over-union threshold 0.05,0.10,...,0.95,0.96,0.97,0.98,0.99 and each label confidence threshold 0.05,0.10,...,0.95,0.96,0.97,0.98,0.99 pair.

`trackMetrics[]` `object ( `[`TrackMetrics`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/TrackMetrics)` )`

UNIMPLEMENTED. The tracks match metrics for each intersection-over-union threshold 0.05,0.10,...,0.95,0.96,0.97,0.98,0.99 and each label confidence threshold 0.05,0.10,...,0.95,0.96,0.97,0.98,0.99 pair.

`evaluatedFrameCount` `integer`

UNIMPLEMENTED. The number of video frames used to create this evaluation.

`evaluatedBoundingBoxCount` `integer`

UNIMPLEMENTED. The total number of bounding boxes (i.e. summed over all frames) the ground truth used to create this evaluation had.

`evaluatedTrackCount` `integer`

UNIMPLEMENTED. The total number of tracks (i.e. as seen across all frames) the ground truth used to create this evaluation had.

`boundingBoxMeanAveragePrecision` `number`

The single metric for bounding boxes evaluation: the `meanAveragePrecision` averaged over all `boundingBoxMetrics` .

`trackMeanAveragePrecision` `number`

UNIMPLEMENTED. The single metric for tracks accuracy evaluation: the `meanAveragePrecision` averaged over all `trackMetrics` .

`trackMeanBoundingBoxIou` `number`

UNIMPLEMENTED. The single metric for tracks bounding box iou evaluation: the `meanBoundingBoxIou` averaged over all `trackMetrics` .

`trackMeanMismatchRate` `number`

UNIMPLEMENTED. The single metric for tracking consistency evaluation: the `meanMismatchRate` averaged over all `trackMetrics` .

**JSON representation**

```
{
  "boundingBoxMetrics": [
    {
      object (BoundingBoxMetrics)
    }
  ],
  "trackMetrics": [
    {
      object (TrackMetrics)
    }
  ],
  "evaluatedFrameCount": integer,
  "evaluatedBoundingBoxCount": integer,
  "evaluatedTrackCount": integer,
  "boundingBoxMeanAveragePrecision": number,
  "trackMeanAveragePrecision": number,
  "trackMeanBoundingBoxIou": number,
  "trackMeanMismatchRate": number
}
```
