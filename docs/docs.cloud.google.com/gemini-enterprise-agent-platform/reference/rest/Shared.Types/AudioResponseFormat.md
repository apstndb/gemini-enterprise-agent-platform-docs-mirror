---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/AudioResponseFormat
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/AudioResponseFormat
title: AudioResponseFormat
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Configuration for audio-specific output formatting.

Fields

`delivery` ` enum ( DeliveryMode  ` )

Optional. Delivery mode for the generated content.

`mimeType` ` enum ( MimeType  ` )

Optional. The MIME type of the audio output.

`sampleRate` `integer`

Optional. Sample rate for the generated audio in Hertz.

`bitRate` `integer`

Optional. Bit rate in bits per second (bps). Only applicable for compressed formats (MP3, Opus).

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;delivery&quot;: enum (DeliveryMode),&quot;mimeType&quot;: enum (MimeType),&quot;sampleRate&quot;: integer,&quot;bitRate&quot;: integer}</code></pre></td>
</tr>
</tbody>
</table>
