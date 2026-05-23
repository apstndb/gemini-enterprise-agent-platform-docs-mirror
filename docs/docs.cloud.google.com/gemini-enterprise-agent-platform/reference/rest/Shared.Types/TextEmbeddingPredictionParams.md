---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/TextEmbeddingPredictionParams
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/TextEmbeddingPredictionParams
title: TextEmbeddingPredictionParams
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Prediction model parameters for Text Embedding. Text embeddings are numerical representations of text that capture semantic meaning, used for tasks like semantic search, classification, and clustering.

Fields

`autoTruncate` `boolean`

Optional. Whether to silently truncate inputs longer than the maximum input token limit. This behavior is enabled by default. If this option is set to false, inputs longer than the limit will cause an INVALID\_ARGUMENT error.

`outputDimensionality` `integer`

Parameter to reduce the dimensionality of the output embedding. Some models support this feature, which can reduce storage and computation costs. If you specify this parameter, you must use a value supported by the model. If the model does not support it, or if you specify an unsupported dimension, the request will fail with an `INVALID_ARGUMENT` error.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;autoTruncate&quot;: boolean,
  &quot;outputDimensionality&quot;: integer
}</code></pre></td>
</tr>
</tbody>
</table>
