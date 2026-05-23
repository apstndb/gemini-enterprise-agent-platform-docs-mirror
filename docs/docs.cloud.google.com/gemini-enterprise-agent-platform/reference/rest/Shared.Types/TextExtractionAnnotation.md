---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/TextExtractionAnnotation
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/TextExtractionAnnotation
title: TextExtractionAnnotation
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Annotation details specific to text extraction.

Fields

`textSegment` ` object ( TextSegment  ` )

The segment of the text content.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;textSegment&quot;: {object (TextSegment)},&quot;annotationSpecId&quot;: string,&quot;displayName&quot;: string}</code></pre></td>
</tr>
</tbody>
</table>

## TextSegment

The text segment inside of DataItem.

Fields

`startOffset` `string`

Zero-based character index of the first character of the text segment (counting characters from the beginning of the text).

`endOffset` `string`

Zero-based character index of the first character past the end of the text segment (counting character from the beginning of the text). The character at the endOffset is NOT included in the text segment.

`content` `string`

The text content in the segment for output only.

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
  &quot;startOffset&quot;: string,
  &quot;endOffset&quot;: string,
  &quot;content&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>
