---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/ImageSegmentationPredictionInstance
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/ImageSegmentationPredictionInstance
title: ImageSegmentationPredictionInstance
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Prediction input format for Image Segmentation.

Fields

`content` `string`

The image bytes to make the predictions on.

`mimeType` `string`

The MIME type of the content of the image. Only the images in below listed MIME types are supported. - image/jpeg - image/png

**JSON representation**

```
{
  "content": string,
  "mimeType": string
}
```
