---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/TextExtractionPredictionResult
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/TextExtractionPredictionResult
title: TextExtractionPredictionResult
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Prediction output format for Text Extraction.

Fields

`ids[]` `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)`

The resource IDs of the AnnotationSpecs that had been identified, ordered by the confidence score descendingly.

`displayNames[]` `string`

The display names of the AnnotationSpecs that had been identified, order matches the IDs.

`textSegmentStartOffsets[]` `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)`

The start offsets, inclusive, of the text segment in which the AnnotationSpec has been identified. Expressed as a zero-based number of characters as measured from the start of the text snippet.

`textSegmentEndOffsets[]` `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)`

The end offsets, inclusive, of the text segment in which the AnnotationSpec has been identified. Expressed as a zero-based number of characters as measured from the start of the text snippet.

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
  "textSegmentStartOffsets": [
    string
  ],
  "textSegmentEndOffsets": [
    string
  ],
  "confidences": [
    number
  ]
}
```
