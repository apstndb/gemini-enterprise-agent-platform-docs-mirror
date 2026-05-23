---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/TextExtractionEvaluationMetrics
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/TextExtractionEvaluationMetrics
title: TextExtractionEvaluationMetrics
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Metrics for text extraction evaluation results.

Fields

`confidenceMetrics[]` ` object ( ConfidenceMetrics  ` )

Metrics that have confidence thresholds. Precision-recall curve can be derived from them.

`confusionMatrix` ` object ( ConfusionMatrix  ` )

Confusion matrix of the evaluation. Only set for Models where number of AnnotationSpecs is no more than 10. Only set for ModelEvaluations, not for ModelEvaluationSlices.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;confidenceMetrics&quot;: [{object (ConfidenceMetrics)}],&quot;confusionMatrix&quot;: {object (ConfusionMatrix)}}</code></pre></td>
</tr>
</tbody>
</table>

## ConfidenceMetrics

Fields

`confidenceThreshold` `number`

Metrics are computed with an assumption that the Model never returns predictions with score lower than this value.

`recall` `number`

Recall (True Positive Rate) for the given confidence threshold.

`precision` `number`

Precision for the given confidence threshold.

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
