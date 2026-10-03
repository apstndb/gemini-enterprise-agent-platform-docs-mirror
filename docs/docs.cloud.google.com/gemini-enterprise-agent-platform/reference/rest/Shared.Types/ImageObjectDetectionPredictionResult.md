---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/ImageObjectDetectionPredictionResult
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/ImageObjectDetectionPredictionResult
title: ImageObjectDetectionPredictionResult
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Prediction output format for Image Object Detection.

Fields

`ids[]` `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)`

The resource IDs of the AnnotationSpecs that had been identified, ordered by the confidence score descendingly.

`displayNames[]` `string`

The display names of the AnnotationSpecs that had been identified, order matches the IDs.

`confidences[]` `number`

The Model's confidences in correctness of the predicted IDs, higher value means higher confidence. Order matches the Ids.

`bboxes[]` `array ( `[`ListValue`](https://protobuf.dev/reference/protobuf/google.protobuf/#list-value)` format)`

Bounding boxes, i.e. the rectangles over the image, that pinpoint the found AnnotationSpecs. Given in order that matches the IDs. Each bounding box is an array of 4 numbers `xMin` , `xMax` , `yMin` , and `yMax` , which represent the extremal coordinates of the box. They are relative to the image size, and the point 0,0 is in the top left of the image.

**JSON representation**

```
{
  "ids": [
    string
  ],
  "displayNames": [
    string
  ],
  "confidences": [
    number
  ],
  "bboxes": [
    array
  ]
}
```
