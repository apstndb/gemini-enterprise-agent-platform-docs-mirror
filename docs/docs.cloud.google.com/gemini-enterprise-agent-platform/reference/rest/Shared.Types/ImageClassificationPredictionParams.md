---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/ImageClassificationPredictionParams
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/ImageClassificationPredictionParams
title: ImageClassificationPredictionParams
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Prediction model parameters for Image Classification.

Fields

`confidenceThreshold` `number`

The Model only returns predictions with at least this confidence score. Default value is 0.0

`maxPredictions` `integer`

The Model only returns up to that many top, by confidence score, predictions per instance. If this number is very high, the Model may return fewer predictions. Default value is 10.

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
