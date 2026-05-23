---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/TextExtractionPredictionResult
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/TextExtractionPredictionResult
title: TextExtractionPredictionResult
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Prediction output format for Text Extraction.

Fields

`ids[]` `string ( int64 format)`

The resource IDs of the AnnotationSpecs that had been identified, ordered by the confidence score descendingly.

`displayNames[]` `string`

The display names of the AnnotationSpecs that had been identified, order matches the IDs.

`textSegmentStartOffsets[]` `string ( int64 format)`

The start offsets, inclusive, of the text segment in which the AnnotationSpec has been identified. Expressed as a zero-based number of characters as measured from the start of the text snippet.

`textSegmentEndOffsets[]` `string ( int64 format)`

The end offsets, inclusive, of the text segment in which the AnnotationSpec has been identified. Expressed as a zero-based number of characters as measured from the start of the text snippet.

`confidences[]` `number`

The Model's confidences in correctness of the predicted IDs, higher value means higher confidence. Order matches the Ids.

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
  &quot;ids&quot;: [
    string
  ],
  &quot;displayNames&quot;: [
    string
  ],
  &quot;textSegmentStartOffsets&quot;: [
    string
  ],
  &quot;textSegmentEndOffsets&quot;: [
    string
  ],
  &quot;confidences&quot;: [
    number
  ]
}</code></pre></td>
</tr>
</tbody>
</table>
