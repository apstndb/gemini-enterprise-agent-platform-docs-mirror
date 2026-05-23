---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/rest/v1/projects.locations.collections.dataObjects/search
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/rest/v1/projects.locations.collections.dataObjects/search
title: 'Method: projects.locations.collections.dataObjects.search'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Searches data objects.

### HTTP request

`POST https://vectorsearch.googleapis.com/v1/{parent}/dataObjects:search`

### Path parameters

Parameters

`parent`

`string`

Required. The resource name of the Collection for which to search. Format: `projects/{project}/locations/{location}/collections/{collection}`

### Request body

The request body contains data with the following structure:

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;pageSize&quot;: integer,&quot;pageToken&quot;: string,// Union field search_type can be only one of the following:&quot;vectorSearch&quot;: {object (VectorSearch)},&quot;semanticSearch&quot;: {object (SemanticSearch)},&quot;textSearch&quot;: {object (TextSearch)}// End of list of possible types for union field search_type.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`pageSize`

`integer`

Optional. The standard list page size. Only supported for KNN. If not set, up to search\_type.top\_k results will be returned. The maximum value is 1000; values above 1000 will be coerced to 1000.

`pageToken`

`string`

Optional. The standard list page token. Typically obtained via `  SearchDataObjectsResponse.next_page_token  ` of the previous `  DataObjectSearchService.SearchDataObjects  ` call.

Union field `search_type` . The query to search for. `search_type` can be only one of the following:

`vectorSearch`

` object ( VectorSearch  ` )

A vector search operation.

`semanticSearch`

` object ( SemanticSearch  ` )

A semantic search operation.

`textSearch`

` object ( TextSearch  ` )

Optional. A text search operation.

### Response body

If successful, the response body contains an instance of `  SearchDataObjectsResponse  ` .

### Authorization scopes

Requires the following OAuth scope:

  - `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .

### IAM Permissions

Requires the following [IAM](https://cloud.google.com/iam/docs) permission on the `parent` resource:

  - `vectorsearch.dataObjects.search`

For more information, see the [IAM documentation](https://cloud.google.com/iam/docs) .
