---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/ImageObjectDetectionEvaluationMetrics
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/ImageObjectDetectionEvaluationMetrics
title: ImageObjectDetectionEvaluationMetrics
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Metrics for image object detection evaluation results.

Fields

`boundingBoxMetrics[]` ` object ( BoundingBoxMetrics  ` )

The bounding boxes match metrics for each intersection-over-union threshold 0.05,0.10,...,0.95,0.96,0.97,0.98,0.99 and each label confidence threshold 0.05,0.10,...,0.95,0.96,0.97,0.98,0.99 pair.

`evaluatedBoundingBoxCount` `integer`

The total number of bounding boxes (i.e. summed over all images) the ground truth used to create this evaluation had.

`boundingBoxMeanAveragePrecision` `number`

The single metric for bounding boxes evaluation: the `meanAveragePrecision` averaged over all `boundingBoxMetricsEntries` .

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;boundingBoxMetrics&quot;: [{object (BoundingBoxMetrics)}],&quot;evaluatedBoundingBoxCount&quot;: integer,&quot;boundingBoxMeanAveragePrecision&quot;: number}</code></pre></td>
</tr>
</tbody>
</table>
