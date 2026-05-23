---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/FunctionCallingConfig
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/FunctionCallingConfig
title: FunctionCallingConfig
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Function calling config.

Fields

`mode` `enum ( Mode` )

Optional. Function calling mode.

`allowedFunctionNames[]` `string`

Optional. Function names to call. Only set when the Mode is ANY. Function names should match `  FunctionDeclaration.name  ` . With mode set to ANY, model will predict a function call from the set of function names provided.

`streamFunctionCallArguments` `boolean`

Optional. When set to true, arguments of a single function call will be streamed out in multiple parts/contents/responses. Partial parameter results will be returned in the `FunctionCall.partial_args` field.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;mode&quot;: enum (Mode),&quot;allowedFunctionNames&quot;: [string],&quot;streamFunctionCallArguments&quot;: boolean}</code></pre></td>
</tr>
</tbody>
</table>
