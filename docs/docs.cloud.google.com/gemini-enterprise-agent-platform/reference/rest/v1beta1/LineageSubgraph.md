---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/LineageSubgraph
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/LineageSubgraph
title: LineageSubgraph
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

A subgraph of the overall lineage graph. Event edges connect Artifact and Execution nodes.

Fields

`artifacts[]` ` object ( Artifact  ` )

The Artifact nodes in the subgraph.

`executions[]` ` object ( Execution  ` )

The Execution nodes in the subgraph.

`events[]` ` object ( Event  ` )

The Event edges between Artifacts and Executions in the subgraph.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;artifacts&quot;: [{object (Artifact)}],&quot;executions&quot;: [{object (Execution)}],&quot;events&quot;: [{object (Event)}]}</code></pre></td>
</tr>
</tbody>
</table>
