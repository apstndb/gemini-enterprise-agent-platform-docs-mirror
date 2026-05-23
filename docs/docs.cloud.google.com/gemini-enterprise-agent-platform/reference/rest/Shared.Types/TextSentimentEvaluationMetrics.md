---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/TextSentimentEvaluationMetrics
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/TextSentimentEvaluationMetrics
title: TextSentimentEvaluationMetrics
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Model evaluation metrics for text sentiment problems.

Fields

`confusionMatrix` ` object ( ConfusionMatrix  ` )

Confusion matrix of the evaluation. Only set for ModelEvaluations, not for ModelEvaluationSlices.

`precision` `number`

Precision.

`recall` `number`

Recall.

`f1Score` `number`

The harmonic mean of recall and precision.

`meanAbsoluteError` `number`

Mean absolute error. Only set for ModelEvaluations, not for ModelEvaluationSlices.

`meanSquaredError` `number`

Mean squared error. Only set for ModelEvaluations, not for ModelEvaluationSlices.

`linearKappa` `number`

Linear weighted kappa. Only set for ModelEvaluations, not for ModelEvaluationSlices.

`quadraticKappa` `number`

Quadratic weighted kappa. Only set for ModelEvaluations, not for ModelEvaluationSlices.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;confusionMatrix&quot;: {object (ConfusionMatrix)},&quot;precision&quot;: number,&quot;recall&quot;: number,&quot;f1Score&quot;: number,&quot;meanAbsoluteError&quot;: number,&quot;meanSquaredError&quot;: number,&quot;linearKappa&quot;: number,&quot;quadraticKappa&quot;: number}</code></pre></td>
</tr>
</tbody>
</table>
