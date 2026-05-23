---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/rest/v1beta/projects.locations.collections.dataObjects/batchDelete
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/rest/v1beta/projects.locations.collections.dataObjects/batchDelete
title: 'Method: projects.locations.collections.dataObjects.batchDelete'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Deletes dataObjects in a batch.

### HTTP request

`POST https://vectorsearch.googleapis.com/v1beta/{parent}/dataObjects:batchDelete`

### Path parameters

Parameters

`parent`

`string`

Required. The resource name of the Collection to delete the DataObjects in. Format: `projects/{project}/locations/{location}/collections/{collection}` .

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;requests&quot;: [{object (DeleteDataObjectRequest)}]}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`requests[]`

` object ( DeleteDataObjectRequest  ` )

Required. The request message specifying the resources to delete. A maximum of 1000 DataObjects can be deleted in a batch.

### Response body

If successful, the response body is an empty JSON object.

### Authorization scopes

Requires the following OAuth scope:

  - `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .

### IAM Permissions

Requires the following [IAM](https://cloud.google.com/iam/docs) permission on the `parent` resource:

  - `vectorsearch.dataObjects.delete`

For more information, see the [IAM documentation](https://cloud.google.com/iam/docs) .

## DeleteDataObjectRequest

Request message for `  DataObjectService.DeleteDataObject  ` .

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
  &quot;name&quot;: string,
  &quot;etag&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`name`

`string`

Required. The name of the DataObject resource to be deleted. Format: `projects/{project}/locations/{location}/collections/{collection}/dataObjects/{dataObject}`

`etag`

`string`

Optional. The current etag of the DataObject. If an etag is provided and does not match the current etag of the DataObject, deletion will be blocked and an ABORTED error will be returned.
