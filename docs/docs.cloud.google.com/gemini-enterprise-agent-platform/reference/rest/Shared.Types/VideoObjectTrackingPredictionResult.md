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

`timeSegmentStart` ` string ( Duration  ` format)

The beginning, inclusive, of the video's time segment in which the object instance has been detected. Expressed as a number of seconds as measured from the start of the video, with fractions up to a microsecond precision, and with "s" appended at the end.

A duration in seconds with up to nine fractional digits, ending with ' `s` '. Example: `"3.5s"` .

`timeSegmentEnd` ` string ( Duration  ` format)

The end, inclusive, of the video's time segment in which the object instance has been detected. Expressed as a number of seconds as measured from the start of the video, with fractions up to a microsecond precision, and with "s" appended at the end.

A duration in seconds with up to nine fractional digits, ending with ' `s` '. Example: `"3.5s"` .

`confidence` `number`

The Model's confidence in correction of this prediction, higher value means higher confidence.

`frames[]` ` object ( Frame  ` )

All of the frames of the video in which a single object instance has been detected. The bounding boxes in the frames identify the same object.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;id&quot;: string,&quot;displayName&quot;: string,&quot;timeSegmentStart&quot;: string,&quot;timeSegmentEnd&quot;: string,&quot;confidence&quot;: number,&quot;frames&quot;: [{object (Frame)}]}</code></pre></td>
</tr>
</tbody>
</table>

## Frame

The fields `xMin` , `xMax` , `yMin` , and `yMax` refer to a bounding box, i.e. the rectangle over the video frame pinpointing the found AnnotationSpec. The coordinates are relative to the frame size, and the point 0,0 is in the top left of the frame.

Fields

`timeOffset` ` string ( Duration  ` format)

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

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;timeOffset&quot;: string,
  &quot;xMin&quot;: number,
  &quot;xMax&quot;: number,
  &quot;yMin&quot;: number,
  &quot;yMax&quot;: number
}</code></pre></td>
</tr>
</tbody>
</table>
