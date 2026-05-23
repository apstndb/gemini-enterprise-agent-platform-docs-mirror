---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/TextEmbeddingPredictionInstance
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/TextEmbeddingPredictionInstance
title: TextEmbeddingPredictionInstance
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Prediction input format for Text Embedding. An embedding is a numerical representation (a vector of floating-point numbers) of text that captures its semantic meaning, enabling tasks like semantic search, classification, and clustering. LINT.IfChange

Fields

`content` `string`

The text passage to generate the embedding for. This can be a phrase, sentence, or document.

`title` `string`

The title for the text passage in the `content` field. If you are embedding documents for the `RETRIEVAL_DOCUMENT` task type, providing a title can improve the quality of the embedding.

`taskType` ` enum ( TaskType  ` )

The task that the generated embeddings will be used for. The model uses this hint to generate embeddings that are optimized for your use case. If not set, the default task type is used.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;content&quot;: string,&quot;title&quot;: string,&quot;taskType&quot;: enum (TaskType)}</code></pre></td>
</tr>
</tbody>
</table>
