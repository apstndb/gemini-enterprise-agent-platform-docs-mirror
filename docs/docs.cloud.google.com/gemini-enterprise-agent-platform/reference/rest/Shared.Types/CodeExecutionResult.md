---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/CodeExecutionResult
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/CodeExecutionResult
title: CodeExecutionResult
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

result of executing the `  ExecutableCode  ` .

Generated only when the `CodeExecution` tool is used.

Fields

`outcome` ` enum ( Outcome  ` )

Required. Outcome of the code execution.

`output` `string`

Optional. Contains stdout when code execution is successful, stderr or other description otherwise.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;outcome&quot;: enum (Outcome),&quot;output&quot;: string}</code></pre></td>
</tr>
</tbody>
</table>
