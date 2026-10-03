---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/Status
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/Status
title: Status
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

The status of the interaction.

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
<td><code>UNSPECIFIED</code></td>
<td>Default value. This value is unused.</td>
</tr>
<tr class="even">
<td><code>IN_PROGRESS</code></td>
<td>The interaction is in progress.</td>
</tr>
<tr class="odd">
<td><code>REQUIRES_ACTION</code></td>
<td>The interaction requires action/input from the user.</td>
</tr>
<tr class="even">
<td><code>COMPLETED</code></td>
<td>The interaction is completed.</td>
</tr>
<tr class="odd">
<td><code>FAILED</code></td>
<td>The interaction failed.</td>
</tr>
<tr class="even">
<td><code>CANCELLED</code></td>
<td>The interaction was cancelled.</td>
</tr>
<tr class="odd">
<td><code>INCOMPLETE</code></td>
<td>The interaction is completed, but contains incomplete results (e.g. hitting maxTokens).</td>
</tr>
<tr class="even">
<td><code>BUDGET_EXCEEDED</code></td>
<td><p>Deprecated: token and execution budget exhaustion returns INCOMPLETE (11).</p>
<blockquote>
<p>This item is deprecated!</p>
</blockquote></td>
</tr>
<tr class="odd">
<td><code>QUEUED</code></td>
<td>The interaction is queued, waiting for processing (e.g. waiting for off-peak capacity).</td>
</tr>
</tbody>
</table>
