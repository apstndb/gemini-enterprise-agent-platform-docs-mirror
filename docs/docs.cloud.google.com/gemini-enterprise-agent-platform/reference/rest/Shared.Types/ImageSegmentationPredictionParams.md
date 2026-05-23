---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/ImageSegmentationPredictionParams
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/ImageSegmentationPredictionParams
title: ImageSegmentationPredictionParams
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Prediction model parameters for Image Segmentation.

Fields

`confidenceThreshold` `number`

When the model predicts category of pixels of the image, it will only provide predictions for pixels that it is at least this much confident about. All other pixels will be classified as background. Default value is 0.5.

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
  &quot;confidenceThreshold&quot;: number
}</code></pre></td>
</tr>
</tbody>
</table>
