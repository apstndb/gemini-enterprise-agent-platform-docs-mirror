---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/rest/v1beta/SearchDataObjectsResponse
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/rest/v1beta/SearchDataObjectsResponse
title: SearchDataObjectsResponse
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Response for a search request.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;results&quot;: [{object (SearchResult)}],&quot;nextPageToken&quot;: string,&quot;searchResponseMetadata&quot;: {object (SearchResponseMetadata)}}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`results[]`

` object ( SearchResult  ` )

Output only. The list of dataObjects that match the search criteria.

`nextPageToken`

`string`

Output only. A token to retrieve next page of results. Pass to \[DataObjectSearchService.SearchDataObjectsRequest.page\_token\]\[\] to obtain that page.

`searchResponseMetadata`

` object ( SearchResponseMetadata  ` )

Output only. Metadata about the search execution.

## SearchResult

A single search result.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;dataObject&quot;: {object (DataObject)},&quot;distance&quot;: number}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`dataObject`

` object ( DataObject  ` )

Output only. The matching data object.

`distance`

`number`

Output only. Similarity distance or ranker score returned by BatchSearchDataObjects.

## SearchResponseMetadata

Metadata about the search execution.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;warnings&quot;: [{object (Status)}],// Union field index_type can be only one of the following:&quot;usedIndex&quot;: {object (IndexInfo)},&quot;usedKnn&quot;: boolean// End of list of possible types for union field index_type.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`warnings[]`

` object ( Status  ` )

Output only. Warnings or non-fatal errors that occurred during execution.

Union field `index_type` . The type of index used. `index_type` can be only one of the following:

`usedIndex`

` object ( IndexInfo  ` )

Indicates that the search used a particular index.

`usedKnn`

`boolean`

Output only. If true, the search used the system's default K-Nearest Neighbor (KNN) index engine.

## IndexInfo

Message that indicates the index used for the search.

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

Output only. The resource name of the index used for the search. Format: `projects/{project}/locations/{location}/collections/{collection}/indexes/{index}`
