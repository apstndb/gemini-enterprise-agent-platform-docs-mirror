---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/VideoActionRecognitionPredictionResult
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/VideoActionRecognitionPredictionResult
title: VideoActionRecognitionPredictionResult
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Prediction output format for Video Action Recognition.

Fields

`id` `string`

The resource id of the AnnotationSpec that had been identified.

`displayName` `string`

The display name of the AnnotationSpec that had been identified.

`timeSegmentStart` `string ( `[`Duration`](https://protobuf.dev/reference/protobuf/google.protobuf/#duration)` format)`

The beginning, inclusive, of the video's time segment in which the AnnotationSpec has been identified. Expressed as a number of seconds as measured from the start of the video, with fractions up to a microsecond precision, and with "s" appended at the end.

A duration in seconds with up to nine fractional digits, ending with ' `s` '. Example: `"3.5s"` .

`timeSegmentEnd` `string ( `[`Duration`](https://protobuf.dev/reference/protobuf/google.protobuf/#duration)` format)`

The end, exclusive, of the video's time segment in which the AnnotationSpec has been identified. Expressed as a number of seconds as measured from the start of the video, with fractions up to a microsecond precision, and with "s" appended at the end.

A duration in seconds with up to nine fractional digits, ending with ' `s` '. Example: `"3.5s"` .

`confidence` `number`

The Model's confidence in correction of this prediction, higher value means higher confidence.

**JSON representation**

```
{
  "id": string,
  "displayName": string,
  "timeSegmentStart": string,
  "timeSegmentEnd": string,
  "confidence": number
}
```
