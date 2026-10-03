---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/TextEmbedding
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/TextEmbedding
title: TextEmbedding
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

An embedding is a vector (list) of floating-point numbers that represents the semantic meaning of text. Embeddings can be used to compare text for similarity, classify text, or cluster text. Text with similar meaning will have similar embedding vectors.

Fields

`values[]` `number`

The embedding vector. The size of the vector is fixed and determined by the model used for embedding generation.

`statistics` `object ( `[`Statistics`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/TextEmbedding#Statistics)` )`

Statistics about the input text.

**JSON representation**

```
{
  "values": [
    number
  ],
  "statistics": {
    object (Statistics)
  }
}
```

## Statistics

Statistics about the input text.

Fields

`tokenCount` `integer`

The number of tokens in the input text.

`truncated` `boolean`

Whether the input text was truncated. If true, the embedding was generated from a truncated version of the input text. This can happen if the input text was longer than the model's input token limit.

**JSON representation**

```
{
  "tokenCount": integer,
  "truncated": boolean
}
```
