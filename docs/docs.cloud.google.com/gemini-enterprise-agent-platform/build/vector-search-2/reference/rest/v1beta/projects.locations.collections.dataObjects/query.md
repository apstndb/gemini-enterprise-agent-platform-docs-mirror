---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/rest/v1beta/projects.locations.collections.dataObjects/query
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/rest/v1beta/projects.locations.collections.dataObjects/query
title: 'Method: projects.locations.collections.dataObjects.query'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Queries data objects.

### HTTP request

`POST https://vectorsearch.googleapis.com/v1beta/{parent}/dataObjects:query`

### Path parameters

Parameters

`parent`

`string`

Required. The resource name of the Collection for which to query. Format: `projects/{project}/locations/{location}/collections/{collection}`

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;filter&quot;: {object},&quot;outputFields&quot;: {object (OutputFields)},&quot;pageSize&quot;: integer,&quot;pageToken&quot;: string}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`filter`

` object ( Struct  ` format)

Optional. A JSON filter expression, e.g. {"genre": {"$eq": "sci-fi"}}, represented as a google.protobuf.Struct.

`outputFields`

` object ( OutputFields  ` )

Optional. Mask specifying which fields to return.

`pageSize`

`integer`

Optional. The standard list page size. Default is 100. The maximum value is 1000; values above 1000 will be coerced to 1000.

`pageToken`

`string`

Optional. The standard list page token. Typically obtained via `  QueryDataObjectsResponse.next_page_token  ` of the previous `  DataObjectSearchService.QueryDataObjects  ` call.

### Response body

Response message for `  DataObjectSearchService.QueryDataObjects  ` .

If successful, the response body contains data with the following structure:

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;dataObjects&quot;: [{object (DataObject)}],&quot;nextPageToken&quot;: string}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`dataObjects[]`

` object ( DataObject  ` )

Output only. The list of dataObjects that match the query.

`nextPageToken`

`string`

Output only. A token to retrieve next page of results. Pass to \[DataObjectSearchService.QueryDataObjectsRequest.page\_token\]\[\] to obtain that page.

### Authorization scopes

Requires the following OAuth scope:

  - `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .

### IAM Permissions

Requires the following [IAM](https://cloud.google.com/iam/docs) permission on the `parent` resource:

  - `vectorsearch.dataObjects.query`

For more information, see the [IAM documentation](https://cloud.google.com/iam/docs) .
