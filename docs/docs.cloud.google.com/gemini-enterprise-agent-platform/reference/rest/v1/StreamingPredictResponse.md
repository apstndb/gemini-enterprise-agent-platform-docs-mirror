---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/StreamingPredictResponse
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/StreamingPredictResponse
title: StreamingPredictResponse
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Response message for `PredictionService.StreamingPredict` .

Fields

`outputs[]` ` object ( Tensor  ` )

The prediction output.

`parameters` ` object ( Tensor  ` )

The parameters that govern the prediction.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;outputs&quot;: [{object (Tensor)}],&quot;parameters&quot;: {object (Tensor)}}</code></pre></td>
</tr>
</tbody>
</table>
