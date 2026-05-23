---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/ImageSegmentationPredictionResult
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/ImageSegmentationPredictionResult
title: ImageSegmentationPredictionResult
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Prediction output format for Image Segmentation.

Fields

`categoryMask` `string`

A PNG image where each pixel in the mask represents the category in which the pixel in the original image was predicted to belong to. The size of this image will be the same as the original image. The mapping between the AnntoationSpec and the color can be found in model's metadata. The model will choose the most likely category and if none of the categories reach the confidence threshold, the pixel will be marked as background.

`confidenceMask` `string`

A one channel image which is encoded as an 8bit lossless PNG. The size of the image will be the same as the original image. For a specific pixel, darker color means less confidence in correctness of the cateogry in the categoryMask for the corresponding pixel. Black means no confidence and white means complete confidence.

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
  &quot;categoryMask&quot;: string,
  &quot;confidenceMask&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>
