---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/query-search/reranking
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/query-search/reranking
title: About reranking search results with the VertexRanker
description: Learn about how to rerank searche results in Vector Search 2.0.
data_source: docs.cloud.google.com
---

> **Preview**
> 
> This feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](https://docs.cloud.google.com/terms/service-terms#1) . Pre-GA features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

VertexRanker is a semantic reranking layer powered by the [Ranking API](https://docs.cloud.google.com/generative-ai-app-builder/docs/ranking) .

After Vector Search 2.0 retrieves and fuses candidate results (using Reciprocal Rank Fusion (RRF)), VertexRanker rescores the merged candidates against your natural-language query using a dedicated semantic model. This improves the relevance of the top-k results, especially for queries where search alone misses nuance. Reranking happens server-side with calls to `BatchSearchDataObjects` . No additional client-side wiring or additional round trips are needed.

## VertexRanker

VertexRanker is configured as the reranker for the `combine.ranker` field of the `BatchSearchDataObjectsRequest` object. You must configure a primary ranker (only RRF is supported). The reranker runs after the RRF fusion step and replaces the output with the semantically rescored list.

The following table lists ranker configuration fields.

| Field                                                            | Required | Description                                                                                                                                                     |
| :--------------------------------------------------------------- | :------- | :-------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `combine.ranker.rrf.weights`                                     | Yes      | The weights for the RRF fusion of the underlying search results.                                                                                                |
| `combine.ranker.vertex_ranker.model`                             | Yes      | The ranking model name. Only `semantic-ranker-fast@latest` is supported.                                                                                        |
| `combine.ranker.vertex_ranker.top_n`                             | Yes      | The maximum number of candidates from the fused list to send to the ranker. Valid values are from `1` to `200` .                                                |
| `combine.ranker.vertex_ranker.text_record_spec.query`            | Yes      | The natural language query used by the ranker to score records.                                                                                                 |
| `combine.ranker.vertex_ranker.text_record_spec.title_template`   | Yes      | The template string, for example, `{title}` , specifying how to extract (construct) the title for each records. Use dot-paths to specify data fields.           |
| `combine.ranker.vertex_ranker.text_record_spec.content_template` | Yes      | The template string, for example, `{body.text}` , specifying how to extract (construct) the main content for each record. Use dot-paths to specify data fields. |
| `combine.top_k`                                                  | Optional | The final number of results to return after reranking. This must be less than or equal to `vertex_ranker.top_n` and less than or equal to 200.                  |

The following example demonstrates the body of a request.

    {
      "searches": [
        { "semantic_search": { "search_text": "running shoes", "search_field": "embedding", "task_type": "RETRIEVAL_QUERY", "top_k": 50 } },
        { "text_search":     { "search_text": "running shoes", "data_field_names": ["title"], "top_k": 50 } }
      ],
      "combine": {
        "top_k": 10,
        "ranker": {
          "rrf": { "weights": [1.0, 1.0] },
          "vertex_ranker": {
            "model": "semantic-ranker-fast@latest",
            "top_n": 50,
            "text_record_spec": {
              "query": "running shoes",
              "title_template": "{title}",
              "content_template": "{body.text}"
            }
          }
        }
      }
    }

Templates use dot-paths to Data Object data fields, for example, `{title}` or `{nested.field}` . These fields must exist in the Collection schema, otherwise the request is rejected during validation. If a Data Object is missing the provided field, the server transparently refetches the full record from storage so the template can still be populated.

## Quota

**Free during preview** : VertexRanker traffic is provided at no extra cost up to **300 queries per minute (QPM)** for each underlying searches are fused. Requests above the 300 QPM ceiling are rejected by the ranker and provided as a warning. The call still returns the fused (RRF) results so search remains available. The maximum number of records sent to the ranker per request is 200 (top\_n must be in the range \[1, 200\] and top\_k is less than or equal to `top_n` ).

## Failure handling and warnings

VertexRanker is a best-effort reranker. If the ranking call fails, the `BatchSearchDataObjects` RPC still succeeds and returns the RRF-fused results truncated to top\_k. The failure is reported in the `search_response_metadata.warnings` field in the response. The full status code from the Ranking API is preserved. The warning code for unexpected statuses is `UNAVAILABLE` with the warning message: `"Reranking is temporarily unavailable. Returning fused (RRF) results without semantic reranking."`

### Failure conditions

The entire `BatchSearchDataObjects` RPC fails with `FAILED_PRECONDITION` (no fallback to RRF) in the following cases.

  - **Discovery Engine API not enabled** — the Ranking API returns `FAILED_PRECONDITION` with the message `Discovery Engine API is not enabled for the consumer project /<N/>. Please enable the API and try again."` Fix: enable the Discovery Engine API on the consumer project.

The customer must enable the Discovery Engine for the consumer project for reranking to occur.

The following table lists warning codes, the typical causes generating the warnings, and the message explaining the warning.

> **Note:** Warning messages are for demonstration purposes only and shouldn't be used for validation.

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th style="text-align: left;">Warning Code</th>
<th style="text-align: left;">Typical Cause</th>
<th style="text-align: left;">Warning Message</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td style="text-align: left;"><code dir="ltr" translate="no">RESOURCE_EXHAUSTED</code></td>
<td style="text-align: left;">Exceeded the 300 QPM free quota on the consumer project.</td>
<td style="text-align: left;"><code dir="ltr" translate="no">&lt;Quota exceeded message from SuperQuota&gt;; RankService.Rank call failed for consumer project &lt;N&gt; with request query: &lt;query&gt; and &lt;model&gt;: semantic-ranker-fast@latest number of records: &lt;N&gt;</code></td>
</tr>
<tr class="even">
<td style="text-align: left;"><code dir="ltr" translate="no">DEADLINE_EXCEEDED</code></td>
<td style="text-align: left;"><code dir="ltr" translate="no">Ranker.Rank</code> did not complete within the request deadline.</td>
<td style="text-align: left;"><code dir="ltr" translate="no">&lt;deadline-exceeded message from Ranker.Rank&gt;; RankService.Rank call failed for consumer project &lt;N&gt; with request query: &lt;query&gt; and &lt;model&gt;: semantic-ranker-fast@latest number of records: &lt;N&gt;</code></td>
</tr>
<tr class="odd">
<td style="text-align: left;"><code dir="ltr" translate="no">UNAVAILABLE</code></td>
<td style="text-align: left;">Either <code dir="ltr" translate="no">Ranker.Rank</code> returned <code dir="ltr" translate="no">UNAVAILABLE</code> , or it returned a non-preserved code (for example, <code dir="ltr" translate="no">INTERNAL</code> ) which is collapsed to <code dir="ltr" translate="no">UNAVAILABLE</code> .</td>
<td style="text-align: left;">If underlying code is <code dir="ltr" translate="no">UNAVAILABLE</code> : <code dir="ltr" translate="no">"RankService.Rank call failed for consumer project...</code><br />
<br />
Otherwise: <code dir="ltr" translate="no">"Reranking is temporarily unavailable. Returning fused (RRF) results without semantic reranking."</code></td>
</tr>
<tr class="even">
<td style="text-align: left;"><code dir="ltr" translate="no">FAILED_PRECONDITION</code></td>
<td style="text-align: left;">Any <code dir="ltr" translate="no">FAILED_PRECONDITION</code> returned by the Ranking API or SuperQuota, excluding <code dir="ltr" translate="no">"Discovery Engine API is not enabled"</code> .</td>
<td style="text-align: left;"><code dir="ltr" translate="no">RankService.Rank call failed for consumer project &lt;N&gt; with request query: &lt;query&gt; and &lt;model&gt;: semantic-ranker-fast@latest number of records: &lt;N&gt;</code></td>
</tr>
<tr class="odd">
<td style="text-align: left;"><code dir="ltr" translate="no">CANCELLED</code></td>
<td style="text-align: left;">The caller cancelled the <code dir="ltr" translate="no">BatchSearchDataObjects</code> RPC before reranking completed.</td>
<td style="text-align: left;"><code dir="ltr" translate="no">&lt;cancellation message from the cancelled RankService.Rank RPC&gt;; RankService.Rank call failed for consumer project &lt;N&gt; with request query: &lt;query&gt; and &lt;model&gt;: semantic-ranker-fast@latest number of records: &lt;N&gt;</code></td>
</tr>
</tbody>
</table>
