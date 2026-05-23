---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/VideoClassificationAnnotation
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/VideoClassificationAnnotation
title: VideoClassificationAnnotation
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Annotation details specific to video classification.

Fields

`timeSegment` ` object ( TimeSegment  ` )

This Annotation applies to the time period represented by the TimeSegment. If it's not set, the Annotation applies to the whole video.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;timeSegment&quot;: {object (TimeSegment)},&quot;annotationSpecId&quot;: string,&quot;displayName&quot;: string}</code></pre></td>
</tr>
</tbody>
</table>
