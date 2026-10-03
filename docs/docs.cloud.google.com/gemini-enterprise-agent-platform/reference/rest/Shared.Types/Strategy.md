---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/Strategy
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/Strategy
title: Strategy
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Optional. This determines which type of scheduling strategy to use. Right now users have two options such as STANDARD which will use regular on demand resources to schedule the job, the other is SPOT which would leverage spot resources alongwith regular resources to schedule the job.

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Enums</th>
<th></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code>STRATEGY_UNSPECIFIED</code></td>
<td>Strategy will default to STANDARD.</td>
</tr>
<tr class="even">
<td><code>ON_DEMAND</code></td>
<td><p>Deprecated. Regular on-demand provisioning strategy.</p>
<blockquote>
<p>This item is deprecated!</p>
</blockquote></td>
</tr>
<tr class="odd">
<td><code>LOW_COST</code></td>
<td><p>Deprecated. Low cost by making potential use of spot resources.</p>
<blockquote>
<p>This item is deprecated!</p>
</blockquote></td>
</tr>
<tr class="even">
<td><code>STANDARD</code></td>
<td>Standard provisioning strategy uses regular on-demand resources.</td>
</tr>
<tr class="odd">
<td><code>SPOT</code></td>
<td>Spot provisioning strategy uses spot resources.</td>
</tr>
<tr class="even">
<td><code>FLEX_START</code></td>
<td>Flex Start strategy uses DWS to queue for resources.</td>
</tr>
</tbody>
</table>
