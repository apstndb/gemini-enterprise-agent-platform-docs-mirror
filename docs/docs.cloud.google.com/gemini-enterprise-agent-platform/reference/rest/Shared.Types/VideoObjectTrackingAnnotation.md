---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/VideoObjectTrackingAnnotation
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/VideoObjectTrackingAnnotation
title: VideoObjectTrackingAnnotation
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Annotation details specific to video object tracking.

Fields

`timeOffset` ` string ( Duration  ` format)

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

`instanceId` `string ( int64 format)`

The instance of the object, expressed as a positive integer. Used to track the same object across different frames.

`annotationSpecId` `string`

The resource id of the AnnotationSpec that this Annotation pertains to.

`displayName` `string`

The display name of the AnnotationSpec that this Annotation pertains to.

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
  &quot;yMax&quot;: number,
  &quot;instanceId&quot;: string,
  &quot;annotationSpecId&quot;: string,
  &quot;displayName&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>
