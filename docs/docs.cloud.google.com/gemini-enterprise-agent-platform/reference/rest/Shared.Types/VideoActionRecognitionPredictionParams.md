---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/VideoActionRecognitionPredictionParams
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/VideoActionRecognitionPredictionParams
title: VideoActionRecognitionPredictionParams
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Prediction model parameters for Video Action Recognition.

Fields

`confidenceThreshold` `number`

The Model only returns predictions with at least this confidence score. Default value is 0.0

`maxPredictions` `integer`

The model only returns up to that many top, by confidence score, predictions per frame of the video. If this number is very high, the Model may return fewer predictions per frame. Default value is 50.

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
  &quot;confidenceThreshold&quot;: number,
  &quot;maxPredictions&quot;: integer
}</code></pre></td>
</tr>
</tbody>
</table>
