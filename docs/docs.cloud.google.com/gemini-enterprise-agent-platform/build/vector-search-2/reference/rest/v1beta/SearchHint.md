---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/rest/v1beta/SearchHint
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/rest/v1beta/SearchHint
title: SearchHint
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Represents a hint to the search index engine.

**JSON representation**

```
{

  // The following is a list of mutually exclusive fields. At most one of the
  // fields will be set in a response:
  "useIndex": {
    object (IndexHint)
  },
  "useKnn": boolean,
  "knnHint": {
    object (KnnHint)
  },
  "indexHint": {
    object (IndexHint)
  }
  // End of mutually exclusive fields.
}
```

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Fields</th>
<th></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>The type of index to use. The following is a list of mutually exclusive fields. At most one of the fields will be set in a response:</td>
<td></td>
</tr>
<tr class="even">
<td><code>useIndex </code><strong><code>(deprecated)</code></strong></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/rest/v1beta/SearchHint#IndexHint"><code>IndexHint</code></a><code> )</code></p>
<blockquote>
<p>This item is deprecated!</p>
</blockquote>
<p>Optional. Deprecated: Use <code>indexHint</code> instead. Specifies that the search should use a particular index.</p></td>
</tr>
<tr class="odd">
<td><code>useKnn </code><strong><code>(deprecated)</code></strong></td>
<td><p><code>boolean</code></p>
<blockquote>
<p>This item is deprecated!</p>
</blockquote>
<p>Optional. Deprecated: Use <code>knnHint</code> instead. If set to true, the search will use the system's default K-Nearest Neighbor (KNN) index engine.</p></td>
</tr>
<tr class="even">
<td><code>knnHint</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/rest/v1beta/SearchHint#KnnHint"><code>KnnHint</code></a><code> )</code></p>
<p>Optional. If set, the search will use the system's default K-Nearest Neighbor (KNN) index engine.</p></td>
</tr>
<tr class="odd">
<td><code>indexHint</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/rest/v1beta/SearchHint#IndexHint"><code>IndexHint</code></a><code> )</code></p>
<p>Optional. Specifies that the search should use a particular index.</p></td>
</tr>
<tr class="even">
<td>End of mutually exclusive fields.</td>
<td></td>
</tr>
</tbody>
</table>

## IndexHint

Message to specify the index to use for the search.

**JSON representation**

```
{
  "name": string,

  // The following is a list of mutually exclusive fields. At most one of the
  // fields will be set in a response:
  "denseScannParams": {
    object (DenseScannParams)
  }
  // End of mutually exclusive fields.
}
```

| Fields                                                                                                                                   |                                                                                                                                                                                                                                      |
|------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `name`                                                                                                                                   | `string` Required. The resource name of the index to use for the search. The index must be in the same project, location, and collection. Format: `projects/{project}/locations/{location}/collections/{collection}/indexes/{index}` |
| The parameters for the index. The following is a list of mutually exclusive fields. At most one of the fields will be set in a response: |                                                                                                                                                                                                                                      |
| `denseScannParams`                                                                                                                       | `object ( `[`DenseScannParams`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/rest/v1beta/SearchHint#DenseScannParams)` )` Optional. Dense ScaNN parameters.                        |
| End of mutually exclusive fields.                                                                                                        |                                                                                                                                                                                                                                      |

## DenseScannParams

Parameters for dense ScaNN.

**JSON representation**

```
{
  "searchLeavesPct": integer,
  "initialCandidateCount": integer,
  "targetRecall": number
}
```

| Fields                  |                                                                                                                                                                                                                                       |
|-------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `searchLeavesPct`       | `integer` Optional. Dense ANN param overrides to control recall and latency. The percentage of leaves to search, in the range \[0, 100\]. Not supported for `STORAGE_OPTIMIZED` indexes. Cannot be set together with `targetRecall` . |
| `initialCandidateCount` | `integer` Optional. The number of initial candidates. Must be a positive integer (\> 0). Not supported for `STORAGE_OPTIMIZED` indexes. Cannot be set together with `targetRecall` .                                                  |
| `targetRecall`          | `number` Optional. The target recall for the search. Must be a double in the range \[0, 1\]. While the search aims to achieve this level of recall, it is not guaranteed.                                                             |

## KnnHint

This type has no fields.

KnnHint will be used if search should be explicitly done on system's default K-Nearest Neighbor (KNN) index engine.
