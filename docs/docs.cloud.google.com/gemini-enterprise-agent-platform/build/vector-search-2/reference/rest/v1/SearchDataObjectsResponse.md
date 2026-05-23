---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/rest/v1/SearchDataObjectsResponse
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/rest/v1/SearchDataObjectsResponse
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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;results&quot;: [{object (SearchResult)}],&quot;nextPageToken&quot;: string}</code></pre></td>
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
