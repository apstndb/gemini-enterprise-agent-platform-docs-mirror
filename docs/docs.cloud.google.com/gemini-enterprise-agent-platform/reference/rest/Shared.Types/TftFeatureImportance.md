---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/TftFeatureImportance
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/TftFeatureImportance
title: TftFeatureImportance
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Fields

`contextWeights[]` `number`

TFT feature importance values. Each pair for {context/horizon/attribute} should have the same shape since the weight corresponds to the column names.

`contextColumns[]` `string`

`horizonWeights[]` `number`

`horizonColumns[]` `string`

`attributeWeights[]` `number`

`attributeColumns[]` `string`

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
  &quot;contextWeights&quot;: [
    number
  ],
  &quot;contextColumns&quot;: [
    string
  ],
  &quot;horizonWeights&quot;: [
    number
  ],
  &quot;horizonColumns&quot;: [
    string
  ],
  &quot;attributeWeights&quot;: [
    number
  ],
  &quot;attributeColumns&quot;: [
    string
  ]
}</code></pre></td>
</tr>
</tbody>
</table>
