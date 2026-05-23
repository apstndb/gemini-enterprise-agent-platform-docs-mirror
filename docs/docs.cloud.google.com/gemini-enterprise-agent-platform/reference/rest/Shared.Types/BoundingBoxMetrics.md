---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/BoundingBoxMetrics
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/BoundingBoxMetrics
title: BoundingBoxMetrics
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Bounding box matching model metrics for a single intersection-over-union threshold and multiple label match confidence thresholds.

Fields

`confidenceMetrics[]` ` object ( ConfidenceMetrics  ` )

Metrics for each label-match confidenceThreshold from 0.05,0.10,...,0.95,0.96,0.97,0.98,0.99. Precision-recall curve is derived from them.

`iouThreshold` `number`

The intersection-over-union threshold value used to compute this metrics entry.

`meanAveragePrecision` `number`

The mean average precision, most often close to `auPrc` .

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;confidenceMetrics&quot;: [{object (ConfidenceMetrics)}],&quot;iouThreshold&quot;: number,&quot;meanAveragePrecision&quot;: number}</code></pre></td>
</tr>
</tbody>
</table>

## ConfidenceMetrics

Metrics for a single confidence threshold.

Fields

`confidenceThreshold` `number`

The confidence threshold value used to compute the metrics.

`recall` `number`

Recall under the given confidence threshold.

`precision` `number`

Precision under the given confidence threshold.

`f1Score` `number`

The harmonic mean of recall and precision.

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
  &quot;recall&quot;: number,
  &quot;precision&quot;: number,
  &quot;f1Score&quot;: number
}</code></pre></td>
</tr>
</tbody>
</table>
