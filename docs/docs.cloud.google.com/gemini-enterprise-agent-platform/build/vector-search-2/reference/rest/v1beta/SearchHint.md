---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/rest/v1beta/SearchHint
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/rest/v1beta/SearchHint
title: SearchHint
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Represents a hint to the search index engine.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{// Union field index_type can be only one of the following:&quot;useIndex&quot;: {object (IndexHint)},&quot;useKnn&quot;: boolean,&quot;knnHint&quot;: {object (KnnHint)},&quot;indexHint&quot;: {object (IndexHint)}// End of list of possible types for union field index_type.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

Union field `index_type` . The type of index to use. `index_type` can be only one of the following:

` useIndex (deprecated)  `

` object ( IndexHint  ` )

> This item is deprecated\!

Optional. Deprecated: Use `indexHint` instead. Specifies that the search should use a particular index.

` useKnn (deprecated)  `

`boolean`

> This item is deprecated\!

Optional. Deprecated: Use `knnHint` instead. If set to true, the search will use the system's default K-Nearest Neighbor (KNN) index engine.

`knnHint`

` object ( KnnHint  ` )

Optional. If set, the search will use the system's default K-Nearest Neighbor (KNN) index engine.

`indexHint`

` object ( IndexHint  ` )

Optional. Specifies that the search should use a particular index.

## IndexHint

Message to specify the index to use for the search.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;name&quot;: string,// Union field params can be only one of the following:&quot;denseScannParams&quot;: {object (DenseScannParams)}// End of list of possible types for union field params.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`name`

`string`

Required. The resource name of the index to use for the search. The index must be in the same project, location, and collection. Format: `projects/{project}/locations/{location}/collections/{collection}/indexes/{index}`

Union field `params` . The parameters for the index. `params` can be only one of the following:

`denseScannParams`

` object ( DenseScannParams  ` )

Optional. Dense ScaNN parameters.

## DenseScannParams

Parameters for dense ScaNN.

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
  &quot;searchLeavesPct&quot;: integer,
  &quot;initialCandidateCount&quot;: integer
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`searchLeavesPct`

`integer`

Optional. Dense ANN param overrides to control recall and latency. The percentage of leaves to search, in the range \[0, 100\].

`initialCandidateCount`

`integer`

Optional. The number of initial candidates. Must be a positive integer (\> 0).

## KnnHint

This type has no fields.

KnnHint will be used if search should be explicitly done on system's default K-Nearest Neighbor (KNN) index engine.
