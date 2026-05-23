---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/RagFileTransformationConfig
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/RagFileTransformationConfig
title: RagFileTransformationConfig
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Specifies the transformation config for RagFiles.

Fields

`ragFileChunkingConfig` ` object ( RagFileChunkingConfig  ` )

Specifies the chunking config for RagFiles.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;ragFileChunkingConfig&quot;: {object (RagFileChunkingConfig)}}</code></pre></td>
</tr>
</tbody>
</table>

## RagFileChunkingConfig

Specifies the size and overlap of chunks for RagFiles.

Fields

`chunking_config` `Union type`

Specifies the chunking config for RagFiles. `chunking_config` can be only one of the following:

`fixedLengthChunking` ` object ( FixedLengthChunking  ` )

Specifies the fixed length chunking config.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{// chunking_config&quot;fixedLengthChunking&quot;: {object (FixedLengthChunking)}// Union type}</code></pre></td>
</tr>
</tbody>
</table>

## FixedLengthChunking

Specifies the fixed length chunking config.

Fields

`chunkSize` `integer`

The size of the chunks.

`chunkOverlap` `integer`

The overlap between chunks.

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
  &quot;chunkSize&quot;: integer,
  &quot;chunkOverlap&quot;: integer
}</code></pre></td>
</tr>
</tbody>
</table>
