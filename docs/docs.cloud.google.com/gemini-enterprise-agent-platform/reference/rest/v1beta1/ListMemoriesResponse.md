---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/ListMemoriesResponse
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/ListMemoriesResponse
title: ListMemoriesResponse
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Response message for `  MemoryBankService.ListMemories  ` .

Fields

`memories[]` ` object ( Memory  ` )

List of Memories in the requested page.

`nextPageToken` `string`

A token to retrieve the next page of results. Pass to `  ListMemoriesRequest.page_token  ` to obtain that page.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;memories&quot;: [{object (Memory)}],&quot;nextPageToken&quot;: string}</code></pre></td>
</tr>
</tbody>
</table>
