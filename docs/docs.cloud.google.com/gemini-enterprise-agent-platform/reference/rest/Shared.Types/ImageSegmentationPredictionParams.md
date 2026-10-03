---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/ImageSegmentationPredictionParams
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/ImageSegmentationPredictionParams
title: ImageSegmentationPredictionParams
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Prediction model parameters for Image Segmentation.

Fields

`confidenceThreshold` `number`

When the model predicts category of pixels of the image, it will only provide predictions for pixels that it is at least this much confident about. All other pixels will be classified as background. Default value is 0.5.

**JSON representation**

```
{
  "confidenceThreshold": number
}
```
