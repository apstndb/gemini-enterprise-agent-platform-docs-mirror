---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/VideoObjectTrackingPredictionParams
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/VideoObjectTrackingPredictionParams
title: VideoObjectTrackingPredictionParams
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Prediction model parameters for Video Object Tracking.

Fields

`confidenceThreshold` `number`

The Model only returns predictions with at least this confidence score. Default value is 0.0

`maxPredictions` `integer`

The model only returns up to that many top, by confidence score, predictions per frame of the video. If this number is very high, the Model may return fewer predictions per frame. Default value is 50.

`minBoundingBoxSize` `number`

Only bounding boxes with shortest edge at least that long as a relative value of video frame size are returned. Default value is 0.0.

**JSON representation**

```
{
  "confidenceThreshold": number,
  "maxPredictions": integer,
  "minBoundingBoxSize": number
}
```
