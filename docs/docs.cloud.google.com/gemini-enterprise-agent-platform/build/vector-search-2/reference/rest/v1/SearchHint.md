---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/rest/v1/SearchHint
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/rest/v1/SearchHint
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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{// Union field index_type can be only one of the following:&quot;knnHint&quot;: {object (KnnHint)},&quot;indexHint&quot;: {object (IndexHint)}// End of list of possible types for union field index_type.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

Union field `index_type` . The type of index to use. `index_type` can be only one of the following:

`knnHint`

` object ( KnnHint  ` )

Optional. If set, the search will use the system's default K-Nearest Neighbor (KNN) index engine.

`indexHint`

` object ( IndexHint  ` )

Optional. Specifies that the search should use a particular index.

## KnnHint

This type has no fields.

KnnHint will be used if search should be explicitly done on system's default K-Nearest Neighbor (KNN) index engine.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;name&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`name`

`string`

Required. The resource name of the index to use for the search. The index must be in the same project, location, and collection. Format: `projects/{project}/locations/{location}/collections/{collection}/indexes/{index}`
