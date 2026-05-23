---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/TextExtractionPredictionInstance
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/TextExtractionPredictionInstance
title: TextExtractionPredictionInstance
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Prediction input format for Text Extraction.

Fields

`content` `string`

The text snippet to make the predictions on.

`mimeType` `string`

The MIME type of the text snippet. The supported MIME types are listed below. - text/plain

`key` `string`

This field is only used for batch prediction. If a key is provided, the batch prediction result will by mapped to this key. If omitted, then the batch prediction result will contain the entire input instance. Agent Platform will not check if keys in the request are duplicates, so it is up to the caller to ensure the keys are unique.

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
  &quot;content&quot;: string,
  &quot;mimeType&quot;: string,
  &quot;key&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>
