---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/TextEmbeddingPredictionResult
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/TextEmbeddingPredictionResult
title: TextEmbeddingPredictionResult
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Prediction output format for Text Embedding. LINT.IfChange Represents the prediction result for a text embedding request.

Fields

`embeddings` `object ( `[`TextEmbedding`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/TextEmbedding)` )`

The embedding generated from the input text.

**JSON representation**

```
{
  "embeddings": {
    object (TextEmbedding)
  }
}
```
