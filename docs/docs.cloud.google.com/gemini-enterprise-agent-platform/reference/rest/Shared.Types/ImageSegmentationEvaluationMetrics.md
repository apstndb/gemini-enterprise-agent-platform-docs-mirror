---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/ImageSegmentationEvaluationMetrics
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/ImageSegmentationEvaluationMetrics
title: ImageSegmentationEvaluationMetrics
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Metrics for image segmentation evaluation results.

Fields

`confidenceMetricsEntries[]` ` object ( ConfidenceMetricsEntry  ` )

Metrics for each confidenceThreshold in 0.00,0.05,0.10,...,0.95,0.96,0.97,0.98,0.99 Precision-recall curve can be derived from it.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;confidenceMetricsEntries&quot;: [{object (ConfidenceMetricsEntry)}]}</code></pre></td>
</tr>
</tbody>
</table>

## ConfidenceMetricsEntry

Fields

`confusionMatrix` ` object ( ConfusionMatrix  ` )

Confusion matrix for the given confidence threshold.

`confidenceThreshold` `number`

Metrics are computed with an assumption that the model never returns predictions with score lower than this value.

`recall` `number`

Recall (True Positive Rate) for the given confidence threshold.

`precision` `number`

Precision for the given confidence threshold.

`diceScoreCoefficient` `number`

DSC or the F1 score, The harmonic mean of recall and precision.

`iouScore` `number`

The intersection-over-union score. The measure of overlap of the annotation's category mask with ground truth category mask on the DataItem.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;confusionMatrix&quot;: {object (ConfusionMatrix)},&quot;confidenceThreshold&quot;: number,&quot;recall&quot;: number,&quot;precision&quot;: number,&quot;diceScoreCoefficient&quot;: number,&quot;iouScore&quot;: number}</code></pre></td>
</tr>
</tbody>
</table>
