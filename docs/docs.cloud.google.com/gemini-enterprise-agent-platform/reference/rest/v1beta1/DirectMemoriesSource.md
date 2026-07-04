---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/DirectMemoriesSource
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/DirectMemoriesSource
title: DirectMemoriesSource
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Defines a direct source of memories that should be uploaded to Memory Bank with consolidation.

Fields

`directMemories[]` ` object ( DirectMemory  ` )

Required. The direct memories to upload to Memory Bank. At most 5 direct memories are allowed per request.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;directMemories&quot;: [{object (DirectMemory)}]}</code></pre></td>
</tr>
</tbody>
</table>

## DirectMemory

A direct memory to upload to Memory Bank.

Fields

`fact` `string`

Required. The fact to consolidate with existing memories.

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
  &quot;fact&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>
