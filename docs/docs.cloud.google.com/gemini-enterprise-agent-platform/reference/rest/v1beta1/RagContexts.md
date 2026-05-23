---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/RagContexts
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/RagContexts
title: RagContexts
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Relevant contexts for one query.

Fields

`contexts[]` ` object ( Context  ` )

All its contexts.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;contexts&quot;: [{object (Context)}]}</code></pre></td>
</tr>
</tbody>
</table>

## Context

A context of the query.

Fields

`sourceUri` `string`

If the file is imported from Cloud Storage or Google Drive, sourceUri will be original file URI in Cloud Storage or Google Drive; if file is uploaded, sourceUri will be file display name.

`sourceDisplayName` `string`

The file display name.

`text` `string`

The text chunk.

` distance (deprecated)  ` `number`

> This item is deprecated\!

The distance between the query dense embedding vector and the context text vector.

` sparseDistance (deprecated)  ` `number`

> This item is deprecated\!

The distance between the query sparse embedding vector and the context text vector.

`chunk` ` object ( RagChunk  ` )

Context of the retrieved chunk.

`score` `number`

According to the underlying Vector DB and the selected metric type, the score can be either the distance or the similarity between the query and the context and its range depends on the metric type.

For example, if the metric type is COSINE\_DISTANCE, it represents the distance between the query and the context. The larger the distance, the less relevant the context is to the query. The range is \[0, 2\], while 0 means the most relevant and 2 means the least relevant.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;sourceUri&quot;: string,&quot;sourceDisplayName&quot;: string,&quot;text&quot;: string,&quot;distance&quot;: number,&quot;sparseDistance&quot;: number,&quot;chunk&quot;: {object (RagChunk)},&quot;score&quot;: number}</code></pre></td>
</tr>
</tbody>
</table>
