---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/TextSentimentPredictionResult
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/TextSentimentPredictionResult
title: TextSentimentPredictionResult
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Prediction output format for Text Sentiment

Fields

`sentiment` `integer`

The integer sentiment labels between 0 (inclusive) and sentimentMax label (inclusive), while 0 maps to the least positive sentiment and sentimentMax maps to the most positive one. The higher the score is, the more positive the sentiment in the text snippet is. Note: sentimentMax is an integer value between 1 (inclusive) and 10 (inclusive).

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
  &quot;sentiment&quot;: integer
}</code></pre></td>
</tr>
</tbody>
</table>
