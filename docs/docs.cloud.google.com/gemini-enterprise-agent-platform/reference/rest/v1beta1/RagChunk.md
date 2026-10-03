---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/RagChunk
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/RagChunk
title: RagChunk
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

A RagChunk includes the content of a chunk of a RagFile, and associated metadata.

Fields

`text` `string`

The content of the chunk.

`fileId` `string`

The id of the file that the chunk belongs to.

`chunkId` `string`

The id of the chunk.

`pageSpan` `object ( `[`PageSpan`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/RagChunk#PageSpan)` )`

If populated, represents where the chunk starts and ends in the document.

**JSON representation**

```
{
  "text": string,
  "fileId": string,
  "chunkId": string,
  "pageSpan": {
    object (PageSpan)
  }
}
```

## PageSpan

Represents where the chunk starts and ends in the document.

Fields

`firstPage` `integer`

Page where chunk starts in the document. Inclusive. 1-indexed.

`lastPage` `integer`

Page where chunk ends in the document. Inclusive. 1-indexed.

**JSON representation**

```
{
  "firstPage": integer,
  "lastPage": integer
}
```
