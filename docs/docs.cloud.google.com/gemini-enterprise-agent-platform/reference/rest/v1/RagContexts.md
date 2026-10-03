---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/RagContexts
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/RagContexts
title: RagContexts
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Relevant contexts for one query.

Fields

`contexts[]` `object ( `[`Context`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/RagContexts#Context)` )`

All its contexts.

**JSON representation**

```
{
  "contexts": [
    {
      object (Context)
    }
  ]
}
```

## Context

A context of the query.

Fields

`sourceUri` `string`

If the file is imported from Cloud Storage or Google Drive, sourceUri will be original file URI in Cloud Storage or Google Drive; if file is uploaded, sourceUri will be file display name.

`sourceDisplayName` `string`

The file display name.

`text` `string`

The text chunk.

`chunk` `object ( `[`RagChunk`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/RagChunk)` )`

Context of the retrieved chunk.

`score` `number`

According to the underlying Vector DB and the selected metric type, the score can be either the distance or the similarity between the query and the context and its range depends on the metric type.

For example, if the metric type is COSINE_DISTANCE, it represents the distance between the query and the context. The larger the distance, the less relevant the context is to the query. The range is \[0, 2\], while 0 means the most relevant and 2 means the least relevant.

**JSON representation**

```
{
  "sourceUri": string,
  "sourceDisplayName": string,
  "text": string,
  "chunk": {
    object (RagChunk)
  },
  "score": number
}
```
