---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/rest/v1/VectorSearch
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/rest/v1/VectorSearch
title: VectorSearch
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Defines a search operation using a query vector.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;searchField&quot;: string,&quot;filter&quot;: {object},&quot;outputFields&quot;: {object (OutputFields)},&quot;searchHint&quot;: {object (SearchHint)},&quot;distanceMetric&quot;: enum (DistanceMetric),// Union field vector_type can be only one of the following:&quot;vector&quot;: {object (DenseVector)},&quot;sparseVector&quot;: {object (SparseVector)}// End of list of possible types for union field vector_type.&quot;topK&quot;: integer}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`searchField`

`string`

Required. The vector field to search.

`filter`

` object ( Struct  ` format)

Optional. A JSON filter expression, e.g. {"genre": {"$eq": "sci-fi"}}, represented as a google.protobuf.Struct.

`outputFields`

` object ( OutputFields  ` )

Optional. Mask specifying which fields to return.

`searchHint`

` object ( SearchHint  ` )

Optional. Sets the search hint. If no strategy is specified, the service will use an index if one is available, and fall back to the default KNN search otherwise.

`distanceMetric`

` enum ( DistanceMetric  ` )

Optional. The distance metric to use for the KNN search. If not specified, DOT\_PRODUCT will be used as the default.

Union field `vector_type` . Specifies the type of vector to use for the query. `vector_type` can be only one of the following:

`vector`

` object ( DenseVector  ` )

A dense vector for the query.

`sparseVector`

` object ( SparseVector  ` )

A sparse vector for the query.

`topK`

`integer`

Optional. The number of nearest neighbors to return.
