---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/SimilaritySearchParams
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/SimilaritySearchParams
title: SimilaritySearchParams
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Parameters for semantic similarity search based retrieval.

Fields

`searchQuery` `string`

Required. Query to use for similarity search retrieval. If provided, then the parent ReasoningEngine must have `  ReasoningEngineContextSpec.MemoryBankConfig.SimilaritySearchConfig  ` set.

`topK` `integer`

Optional. The maximum number of memories to return. The service may return fewer than this value. If unspecified, at most 3 memories will be returned. The maximum value is 100; values above 100 will be coerced to 100.

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
  &quot;searchQuery&quot;: string,
  &quot;topK&quot;: integer
}</code></pre></td>
</tr>
</tbody>
</table>
