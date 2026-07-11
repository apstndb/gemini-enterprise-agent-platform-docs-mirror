---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/Chunk
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/Chunk
title: Chunk
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Container for bytes-encoded data such as video frame, audio sample, or a complete binary/text data.

Fields

`mimeType` `string`

Required. Mime type of the chunk data. See <https://www.iana.org/assignments/media-types/media-types.xhtml> for the full list.

`data` `string ( bytes format)`

Required. The data in the chunk.

A base64-encoded string.

`metadata` ` object ( Metadata  ` )

Optional. metadata that is associated with the data in the payload.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;mimeType&quot;: string,&quot;data&quot;: string,&quot;metadata&quot;: {object (Metadata)}}</code></pre></td>
</tr>
</tbody>
</table>

## Metadata

metadata for a chunk.

Fields

`attributes` `map (key: string, value: string ( bytes format))`

Optional. Attributes attached to the data. The keys have semantic conventions and the consumers of the attributes should know how to deserialize the value bytes based on the keys.

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
  &quot;attributes&quot;: {
    string: string,
    ...
  }
}</code></pre></td>
</tr>
</tbody>
</table>
