---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/PairwiseTextGenerationEvaluationMetrics
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/PairwiseTextGenerationEvaluationMetrics
title: PairwiseTextGenerationEvaluationMetrics
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Metrics for general pairwise text generation evaluation results.

Fields

`modelWinRate` `number`

Percentage of time the autorater decided the model had the better response.

`baselineModelWinRate` `number`

Percentage of time the autorater decided the baseline model had the better response.

`humanPreferenceModelWinRate` `number`

Percentage of time humans decided the model had the better response.

`humanPreferenceBaselineModelWinRate` `number`

Percentage of time humans decided the baseline model had the better response.

`truePositiveCount` `string ( int64 format)`

Number of examples where both the autorater and humans decided that the model had the better response.

`falsePositiveCount` `string ( int64 format)`

Number of examples where the autorater chose the model, but humans preferred the baseline model.

`falseNegativeCount` `string ( int64 format)`

Number of examples where the autorater chose the baseline model, but humans preferred the model.

`trueNegativeCount` `string ( int64 format)`

Number of examples where both the autorater and humans decided that the model had the worse response.

`accuracy` `number`

Fraction of cases where the autorater agreed with the human raters.

`precision` `number`

Fraction of cases where the autorater and humans thought the model had a better response out of all cases where the autorater thought the model had a better response. True positive divided by all positive.

`recall` `number`

Fraction of cases where the autorater and humans thought the model had a better response out of all cases where the humans thought the model had a better response.

`f1Score` `number`

Harmonic mean of precision and recall.

`cohensKappa` `number`

A measurement of agreement between the autorater and human raters that takes the likelihood of random agreement into account.

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
  &quot;modelWinRate&quot;: number,
  &quot;baselineModelWinRate&quot;: number,
  &quot;humanPreferenceModelWinRate&quot;: number,
  &quot;humanPreferenceBaselineModelWinRate&quot;: number,
  &quot;truePositiveCount&quot;: string,
  &quot;falsePositiveCount&quot;: string,
  &quot;falseNegativeCount&quot;: string,
  &quot;trueNegativeCount&quot;: string,
  &quot;accuracy&quot;: number,
  &quot;precision&quot;: number,
  &quot;recall&quot;: number,
  &quot;f1Score&quot;: number,
  &quot;cohensKappa&quot;: number
}</code></pre></td>
</tr>
</tbody>
</table>
