---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/VideoObjectTrackingPredictionResult
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/VideoObjectTrackingPredictionResult
title: VideoObjectTrackingPredictionResult
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Prediction output format for Video Object Tracking.

Fields

`id` `string`

The resource id of the AnnotationSpec that had been identified.

`displayName` `string`

The display name of the AnnotationSpec that had been identified.

`timeSegmentStart` `string ( `[`Duration`](https://protobuf.dev/reference/protobuf/google.protobuf/#duration)` format)`

The beginning, inclusive, of the video's time segment in which the object instance has been detected. Expressed as a number of seconds as measured from the start of the video, with fractions up to a microsecond precision, and with "s" appended at the end.

A duration in seconds with up to nine fractional digits, ending with ' `s` '. Example: `"3.5s"` .

`timeSegmentEnd` `string ( `[`Duration`](https://protobuf.dev/reference/protobuf/google.protobuf/#duration)` format)`

The end, inclusive, of the video's time segment in which the object instance has been detected. Expressed as a number of seconds as measured from the start of the video, with fractions up to a microsecond precision, and with "s" appended at the end.

A duration in seconds with up to nine fractional digits, ending with ' `s` '. Example: `"3.5s"` .

`confidence` `number`

The Model's confidence in correction of this prediction, higher value means higher confidence.

`frames[]` `object ( `[`Frame`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/VideoObjectTrackingPredictionResult#Frame)` )`

All of the frames of the video in which a single object instance has been detected. The bounding boxes in the frames identify the same object.

**JSON representation**

```
{
  "id": string,
  "displayName": string,
  "timeSegmentStart": string,
  "timeSegmentEnd": string,
  "confidence": number,
  "frames": [
    {
      object (Frame)
    }
  ]
}
```

## Frame

The fields `xMin` , `xMax` , `yMin` , and `yMax` refer to a bounding box, i.e. the rectangle over the video frame pinpointing the found AnnotationSpec. The coordinates are relative to the frame size, and the point 0,0 is in the top left of the frame.

Fields

`timeOffset` `string ( `[`Duration`](https://protobuf.dev/reference/protobuf/google.protobuf/#duration)` format)`

A time (frame) of a video in which the object has been detected. Expressed as a number of seconds as measured from the start of the video, with fractions up to a microsecond precision, and with "s" appended at the end.

A duration in seconds with up to nine fractional digits, ending with ' `s` '. Example: `"3.5s"` .

`xMin` `number`

The leftmost coordinate of the bounding box.

`xMax` `number`

The rightmost coordinate of the bounding box.

`yMin` `number`

The topmost coordinate of the bounding box.

`yMax` `number`

The bottommost coordinate of the bounding box.

**JSON representation**

```
{
  "timeOffset": string,
  "xMin": number,
  "xMax": number,
  "yMin": number,
  "yMax": number
}
```
