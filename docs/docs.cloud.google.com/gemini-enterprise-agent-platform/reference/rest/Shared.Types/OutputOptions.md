---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/OutputOptions
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/OutputOptions
title: OutputOptions
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Configuration options for the output image.

Fields

`mimeType` `string`

The MIME type of the output image.

The following values are supported:

  - `image/jpeg`
  - `image/png`

If not set, defaults to `image/png` .

`compressionQuality` `integer`

Specifies the compression quality for JPEG images. Accepted values are in the range \[0, 100\].

If not set, defaults to `75` .

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
  &quot;mimeType&quot;: string,
  &quot;compressionQuality&quot;: integer
}</code></pre></td>
</tr>
</tbody>
</table>
