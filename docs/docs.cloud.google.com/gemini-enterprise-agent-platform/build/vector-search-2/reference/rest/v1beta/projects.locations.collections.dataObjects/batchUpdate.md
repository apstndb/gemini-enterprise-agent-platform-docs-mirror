---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/rest/v1beta/projects.locations.collections.dataObjects/batchUpdate
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/rest/v1beta/projects.locations.collections.dataObjects/batchUpdate
title: 'Method: projects.locations.collections.dataObjects.batchUpdate'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Updates dataObjects in a batch.

### HTTP request

`POST https://vectorsearch.googleapis.com/v1beta/{parent}/dataObjects:batchUpdate`

### Path parameters

Parameters

`parent`

`string`

Required. The resource name of the Collection to update the DataObjects in. Format: `projects/{project}/locations/{location}/collections/{collection}` . The parent field in the UpdateDataObjectRequest messages must match this field.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;requests&quot;: [{object (UpdateDataObjectRequest)}]}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`requests[]`

` object ( UpdateDataObjectRequest  ` )

Required. The request message specifying the resources to update. A maximum of 1000 DataObjects can be updated in a batch.

### Response body

If successful, the response body is empty.

### Authorization scopes

Requires the following OAuth scope:

  - `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .

### IAM Permissions

Requires the following [IAM](https://cloud.google.com/iam/docs) permission on the `parent` resource:

  - `vectorsearch.dataObjects.update`

For more information, see the [IAM documentation](https://cloud.google.com/iam/docs) .

## UpdateDataObjectRequest

Request message for `  DataObjectService.UpdateDataObject  ` .

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;dataObject&quot;: {object (DataObject)},&quot;updateMask&quot;: string}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`dataObject`

` object ( DataObject  ` )

Required. The DataObject which replaces the resource on the server.

`updateMask`

` string ( FieldMask  ` format)

Optional. The update mask applies to the resource. See `  google.protobuf.FieldMask  ` .

This is a comma-separated list of fully qualified names of fields. Example: `"user.displayName,photo"` .
