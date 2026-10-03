---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/VideoObjectTrackingAnnotation
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/VideoObjectTrackingAnnotation
title: VideoObjectTrackingAnnotation
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Annotation details specific to video object tracking.

Fields

`timeOffset` `string ( `[`Duration`](https://protobuf.dev/reference/protobuf/google.protobuf/#duration)` format)`

A time (frame) of a video to which this annotation pertains. Represented as the duration since the video's start.

A duration in seconds with up to nine fractional digits, ending with ' `s` '. Example: `"3.5s"` .

`xMin` `number`

The leftmost coordinate of the bounding box.

`xMax` `number`

The rightmost coordinate of the bounding box.

`yMin` `number`

The topmost coordinate of the bounding box.

`yMax` `number`

The bottommost coordinate of the bounding box.

`instanceId` `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)`

The instance of the object, expressed as a positive integer. Used to track the same object across different frames.

`annotationSpecId` `string`

The resource id of the AnnotationSpec that this Annotation pertains to.

`displayName` `string`

The display name of the AnnotationSpec that this Annotation pertains to.

**JSON representation**

```
{
  "timeOffset": string,
  "xMin": number,
  "xMax": number,
  "yMin": number,
  "yMax": number,
  "instanceId": string,
  "annotationSpecId": string,
  "displayName": string
}
```
