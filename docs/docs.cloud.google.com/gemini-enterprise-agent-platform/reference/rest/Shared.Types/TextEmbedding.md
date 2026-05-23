---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/TextEmbedding
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/TextEmbedding
title: TextEmbedding
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

An embedding is a vector (list) of floating-point numbers that represents the semantic meaning of text. Embeddings can be used to compare text for similarity, classify text, or cluster text. Text with similar meaning will have similar embedding vectors.

Fields

`values[]` `number`

The embedding vector. The size of the vector is fixed and determined by the model used for embedding generation.

`statistics` ` object ( Statistics  ` )

Statistics about the input text.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;values&quot;: [number],&quot;statistics&quot;: {object (Statistics)}}</code></pre></td>
</tr>
</tbody>
</table>

## Statistics

Statistics about the input text.

Fields

`tokenCount` `integer`

The number of tokens in the input text.

`truncated` `boolean`

Whether the input text was truncated. If true, the embedding was generated from a truncated version of the input text. This can happen if the input text was longer than the model's input token limit.

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
  &quot;tokenCount&quot;: integer,
  &quot;truncated&quot;: boolean
}</code></pre></td>
</tr>
</tbody>
</table>
