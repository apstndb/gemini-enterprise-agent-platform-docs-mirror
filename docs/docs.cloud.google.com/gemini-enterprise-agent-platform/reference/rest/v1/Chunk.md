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

`data` `string ( `[`bytes`](https://developers.google.com/discovery/v1/type-format)` format)`

Required. The data in the chunk.

A base64-encoded string.

`metadata` `object ( `[`Metadata`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/Chunk#Metadata)` )`

Optional. metadata that is associated with the data in the payload.

**JSON representation**

```
{
  "mimeType": string,
  "data": string,
  "metadata": {
    object (Metadata)
  }
}
```

## Metadata

metadata for a chunk.

Fields

`attributes` `map (key: string, value: string ( `[`bytes`](https://developers.google.com/discovery/v1/type-format)` format))`

Optional. Attributes attached to the data. The keys have semantic conventions and the consumers of the attributes should know how to deserialize the value bytes based on the keys.

**JSON representation**

```
{
  "attributes": {
    string: string,
    ...
  }
}
```
