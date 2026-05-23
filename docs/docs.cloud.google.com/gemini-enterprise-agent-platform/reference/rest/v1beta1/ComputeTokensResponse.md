---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/ComputeTokensResponse
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/ComputeTokensResponse
title: ComputeTokensResponse
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Response message for ComputeTokens RPC call.

Fields

`tokensInfo[]` ` object ( TokensInfo  ` )

Lists of tokens info from the input. A ComputeTokensRequest could have multiple instances with a prompt in each instance. We also need to return lists of tokens info for the request with multiple instances.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;tokensInfo&quot;: [{object (TokensInfo)}]}</code></pre></td>
</tr>
</tbody>
</table>

## TokensInfo

Tokens info with a list of tokens and the corresponding list of token ids.

Fields

`tokens[]` `string ( bytes format)`

A list of tokens from the input.

A base64-encoded string.

`tokenIds[]` `string ( int64 format)`

A list of token ids from the input.

`role` `string`

Optional. Optional fields for the role from the corresponding Content.

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
  &quot;tokens&quot;: [
    string
  ],
  &quot;tokenIds&quot;: [
    string
  ],
  &quot;role&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>
