---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/RagFileTransformationConfig
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/RagFileTransformationConfig
title: RagFileTransformationConfig
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Specifies the transformation config for RagFiles.

Fields

`ragFileChunkingConfig` `object ( `[`RagFileChunkingConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/RagFileTransformationConfig#RagFileChunkingConfig)` )`

Specifies the chunking config for RagFiles.

**JSON representation**

```
{
  "ragFileChunkingConfig": {
    object (RagFileChunkingConfig)
  }
}
```

## RagFileChunkingConfig

Specifies the size and overlap of chunks for RagFiles.

Fields

`chunking_config` `Union type`

Specifies the chunking config for RagFiles. The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:

`fixedLengthChunking` `object ( `[`FixedLengthChunking`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/RagFileTransformationConfig#FixedLengthChunking)` )`

Specifies the fixed length chunking config.

End of mutually exclusive fields.

**JSON representation**

```
{

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
