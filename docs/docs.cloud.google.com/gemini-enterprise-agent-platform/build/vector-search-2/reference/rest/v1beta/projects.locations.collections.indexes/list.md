---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/rest/v1beta/projects.locations.collections.indexes/list
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/rest/v1beta/projects.locations.collections.indexes/list
title: 'Method: projects.locations.collections.indexes.list'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Lists Indexes in a given project and location.

### HTTP request

`GET https://vectorsearch.googleapis.com/v1beta/{parent}/indexes`

### Path parameters

Parameters

`parent`

`string`

Required. Parent value for ListIndexesRequest

### Query parameters

Parameters

`pageSize`

`integer`

Optional. Requested page size. Server may return fewer items than requested. If unspecified, server will pick an appropriate default.

`pageToken`

`string`

Optional. A token identifying a page of results the server should return.

`filter`

`string`

Optional. Filtering results

`orderBy`

`string`

Optional. Hint for how to order the results

### Request body

The request body must be empty.

### Response body

Message for response to listing Indexes

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;indexes&quot;: [{object (Index)}],&quot;nextPageToken&quot;: string}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`indexes[]`

` object ( Index  ` )

The list of Index

`nextPageToken`

`string`

A token identifying a page of results the server should return.

### Authorization scopes

Requires the following OAuth scope:

  - `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .

### IAM Permissions

Requires the following [IAM](https://cloud.google.com/iam/docs) permission on the `parent` resource:

  - `vectorsearch.indexes.list`

For more information, see the [IAM documentation](https://cloud.google.com/iam/docs) .
