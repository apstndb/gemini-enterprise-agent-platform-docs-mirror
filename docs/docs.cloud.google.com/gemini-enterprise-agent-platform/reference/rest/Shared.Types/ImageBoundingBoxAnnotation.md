---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/ImageBoundingBoxAnnotation
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/ImageBoundingBoxAnnotation
title: ImageBoundingBoxAnnotation
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Annotation details specific to image object detection.

Fields

`annotationSpecId` `string`

The resource id of the AnnotationSpec that this Annotation pertains to.

`displayName` `string`

The display name of the AnnotationSpec that this Annotation pertains to.

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
  &quot;annotationSpecId&quot;: string,
  &quot;displayName&quot;: string,
  &quot;xMin&quot;: number,
  &quot;xMax&quot;: number,
  &quot;yMin&quot;: number,
  &quot;yMax&quot;: number
}</code></pre></td>
</tr>
</tbody>
</table>
