---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/CountTokensResponse
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/CountTokensResponse
title: CountTokensResponse
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Response message for `  PredictionService.CountTokens  ` .

Fields

`totalTokens` `integer`

The total number of tokens counted across all instances from the request.

`totalBillableCharacters` `integer`

The total number of billable characters counted across all instances from the request.

`promptTokensDetails[]` ` object ( ModalityTokenCount  ` )

Output only. List of modalities that were processed in the request input.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;totalTokens&quot;: integer,&quot;totalBillableCharacters&quot;: integer,&quot;promptTokensDetails&quot;: [{object (ModalityTokenCount)}]}</code></pre></td>
</tr>
</tbody>
</table>
