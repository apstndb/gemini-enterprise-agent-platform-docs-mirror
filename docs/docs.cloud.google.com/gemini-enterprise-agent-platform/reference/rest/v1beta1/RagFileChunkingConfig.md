---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/RagFileChunkingConfig
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/RagFileChunkingConfig
title: RagFileChunkingConfig
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Specifies the size and overlap of chunks for RagFiles.

Fields

`chunkSize `**`(deprecated)`** `integer`

> This item is deprecated!

The size of the chunks.

`chunkOverlap `**`(deprecated)`** `integer`

> This item is deprecated!

The overlap between chunks.

`chunking_config` `Union type`

Specifies the chunking config for RagFiles. The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:

`fixedLengthChunking` `object ( `[`FixedLengthChunking`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/RagFileChunkingConfig#FixedLengthChunking)` )`

Specifies the fixed length chunking config.

End of mutually exclusive fields.

**JSON representation**

```
{
  "chunkSize": integer,
  "chunkOverlap": integer,

  // chunking_config
  "fixedLengthChunking": {
    object (FixedLengthChunking)
  }
  // Union type
}
```

## FixedLengthChunking

Specifies the fixed length chunking config.

Fields

`chunkSize` `integer`

The size of the chunks.

`chunkOverlap` `integer`

The overlap between chunks.

**JSON representation**

```
{
  "chunkSize": integer,
  "chunkOverlap": integer
}
```
