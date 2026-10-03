---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/VideoClassificationPredictionResult
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/VideoClassificationPredictionResult
title: VideoClassificationPredictionResult
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Prediction output format for Video Classification.

Fields

`id` `string`

The resource id of the AnnotationSpec that had been identified.

`displayName` `string`

The display name of the AnnotationSpec that had been identified.

`type` `string`

The type of the prediction. The requested types can be configured via parameters. This will be one of - segment-classification - shot-classification - one-sec-interval-classification

`timeSegmentStart` `string ( `[`Duration`](https://protobuf.dev/reference/protobuf/google.protobuf/#duration)` format)`

The beginning, inclusive, of the video's time segment in which the AnnotationSpec has been identified. Expressed as a number of seconds as measured from the start of the video, with fractions up to a microsecond precision, and with "s" appended at the end. Note that for 'segment-classification' prediction type, this equals the original 'timeSegmentStart' from the input instance, for other types it is the start of a shot or a 1 second interval respectively.

A duration in seconds with up to nine fractional digits, ending with ' `s` '. Example: `"3.5s"` .

`timeSegmentEnd` `string ( `[`Duration`](https://protobuf.dev/reference/protobuf/google.protobuf/#duration)` format)`

The end, exclusive, of the video's time segment in which the AnnotationSpec has been identified. Expressed as a number of seconds as measured from the start of the video, with fractions up to a microsecond precision, and with "s" appended at the end. Note that for 'segment-classification' prediction type, this equals the original 'timeSegmentEnd' from the input instance, for other types it is the end of a shot or a 1 second interval respectively.

A duration in seconds with up to nine fractional digits, ending with ' `s` '. Example: `"3.5s"` .

`confidence` `number`

The Model's confidence in correction of this prediction, higher value means higher confidence.

**JSON representation**

```
{
  "id": string,
  "displayName": string,
  "type": string,
  "timeSegmentStart": string,
  "timeSegmentEnd": string,
  "confidence": number
}
```
