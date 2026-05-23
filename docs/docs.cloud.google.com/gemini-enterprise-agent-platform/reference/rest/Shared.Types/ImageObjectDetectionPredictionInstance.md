---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/ImageObjectDetectionPredictionInstance
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/ImageObjectDetectionPredictionInstance
title: ImageObjectDetectionPredictionInstance
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Prediction input format for Image Object Detection.

Fields

`content` `string`

The image bytes or Cloud Storage URI to make the prediction on.

`mimeType` `string`

The MIME type of the content of the image. Only the images in below listed MIME types are supported. - image/jpeg - image/gif - image/png - image/webp - image/bmp - image/tiff - image/vnd.microsoft.icon

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
  &quot;mimeType&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>
