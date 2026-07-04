---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/RetrieveMemoriesResponse
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/RetrieveMemoriesResponse
title: RetrieveMemoriesResponse
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Response message for `  MemoryBankService.RetrieveMemories  ` .

Fields

`retrievedMemories[]` ` object ( RetrievedMemory  ` )

The retrieved memories.

`nextPageToken` `string`

A token that can be sent as `pageToken` to retrieve the next page. If this field is omitted, there are no subsequent pages. This token is not set if similarity search was used for retrieval.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;retrievedMemories&quot;: [{object (RetrievedMemory)}],&quot;nextPageToken&quot;: string}</code></pre></td>
</tr>
</tbody>
</table>

## RetrievedMemory

A retrieved memory.

Fields

`memory` ` object ( Memory  ` )

The retrieved Memory.

`distance` `number`

The distance between the query and the retrieved Memory. Smaller values indicate more similar memories. This is only set if similarity search was used for retrieval.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;memory&quot;: {object (Memory)},&quot;distance&quot;: number}</code></pre></td>
</tr>
</tbody>
</table>
