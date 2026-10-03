---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/AudioResponseFormat
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/AudioResponseFormat
title: AudioResponseFormat
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Configuration for audio-specific output formatting.

Fields

`delivery` `enum ( `[`DeliveryMode`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/DeliveryMode)` )`

Optional. Delivery mode for the generated content.

`mimeType` `enum ( `[`MimeType`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/MimeType)` )`

Optional. The MIME type of the audio output.

`sampleRate` `integer`

Optional. Sample rate for the generated audio in Hertz.

`bitRate` `integer`

Optional. Bit rate in bits per second (bps). Only applicable for compressed formats (MP3, Opus).

**JSON representation**

```
{
  "delivery": enum (DeliveryMode),
  "mimeType": enum (MimeType),
  "sampleRate": integer,
  "bitRate": integer
}
```
