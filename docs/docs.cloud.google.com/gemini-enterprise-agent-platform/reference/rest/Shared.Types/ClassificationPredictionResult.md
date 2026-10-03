---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/ClassificationPredictionResult
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/ClassificationPredictionResult
title: ClassificationPredictionResult
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Prediction output format for Image and Text Classification.

Fields

`ids[]` `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)`

The resource IDs of the AnnotationSpecs that had been identified.

`displayNames[]` `string`

The display names of the AnnotationSpecs that had been identified, order matches the IDs.

`confidences[]` `number`

The Model's confidences in correctness of the predicted IDs, higher value means higher confidence. Order matches the Ids.

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
  ]
}
```
