---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/RagChunk
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/RagChunk
title: RagChunk
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

A RagChunk includes the content of a chunk of a RagFile, and associated metadata.

Fields

`text` `string`

The content of the chunk.

`fileId` `string`

The id of the file that the chunk belongs to.

`chunkId` `string`

The id of the chunk.

`pageSpan` ` object ( PageSpan  ` )

If populated, represents where the chunk starts and ends in the document.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;text&quot;: string,&quot;fileId&quot;: string,&quot;chunkId&quot;: string,&quot;pageSpan&quot;: {object (PageSpan)}}</code></pre></td>
</tr>
</tbody>
</table>

## PageSpan

Represents where the chunk starts and ends in the document.

Fields

`firstPage` `integer`

Page where chunk starts in the document. Inclusive. 1-indexed.

`lastPage` `integer`

Page where chunk ends in the document. Inclusive. 1-indexed.

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
  &quot;firstPage&quot;: integer,
  &quot;lastPage&quot;: integer
}</code></pre></td>
</tr>
</tbody>
</table>
