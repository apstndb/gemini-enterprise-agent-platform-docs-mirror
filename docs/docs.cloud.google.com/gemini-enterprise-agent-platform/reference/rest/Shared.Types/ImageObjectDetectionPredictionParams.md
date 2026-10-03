---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/ImageObjectDetectionPredictionParams
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/ImageObjectDetectionPredictionParams
title: ImageObjectDetectionPredictionParams
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Prediction model parameters for Image Object Detection.

Fields

`confidenceThreshold` `number`

The Model only returns predictions with at least this confidence score. Default value is 0.0

`maxPredictions` `integer`

The Model only returns up to that many top, by confidence score, predictions per instance. Note that number of returned predictions is also limited by metadata's predictionsLimit. Default value is 10.

**JSON representation**

```
{
  "confidenceThreshold": number,
  "maxPredictions": integer
}
```
