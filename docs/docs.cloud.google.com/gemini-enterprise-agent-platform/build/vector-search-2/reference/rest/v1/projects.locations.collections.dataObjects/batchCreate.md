---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/rest/v1/projects.locations.collections.dataObjects/batchCreate
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/rest/v1/projects.locations.collections.dataObjects/batchCreate
title: 'Method: projects.locations.collections.dataObjects.batchCreate'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Creates a batch of dataObjects.

### HTTP request

`POST https://vectorsearch.googleapis.com/v1/{parent}/dataObjects:batchCreate`

### Path parameters

Parameters

`parent`

`string`

Required. The resource name of the Collection to create the DataObjects in. Format: `projects/{project}/locations/{location}/collections/{collection}` . The parent field in the CreateDataObjectRequest messages must match this field.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;requests&quot;: [{object (CreateDataObjectRequest)}]}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`requests[]`

` object ( CreateDataObjectRequest  ` )

Required. The request message specifying the resources to create. A maximum of 1000 DataObjects can be created in a batch.

### Response body

Response message for `  DataObjectService.BatchCreateDataObjects  ` .

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;dataObjects&quot;: [{object (DataObject)}]}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`dataObjects[]`

` object ( DataObject  ` )

Output only. DataObjects created.

### Authorization scopes

Requires the following OAuth scope:

  - `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .

### IAM Permissions

Requires the following [IAM](https://cloud.google.com/iam/docs) permission on the `parent` resource:

  - `vectorsearch.dataObjects.create`

For more information, see the [IAM documentation](https://cloud.google.com/iam/docs) .

## CreateDataObjectRequest

Request message for `  DataObjectService.CreateDataObject  ` .

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;parent&quot;: string,&quot;dataObjectId&quot;: string,&quot;dataObject&quot;: {object (DataObject)}}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`parent`

`string`

Required. The resource name of the Collection to create the DataObject in. Format: `projects/{project}/locations/{location}/collections/{collection}`

`dataObjectId`

`string`

Required. The id of the dataObject to create. The id must be 1-63 characters long, and comply with [RFC1035](https://www.ietf.org/rfc/rfc1035.txt) . Specifically, it must be 1-63 characters long and match the regular expression `[a-z](?:[-a-z0-9]{0,61}[a-z0-9])?` .

`dataObject`

` object ( DataObject  ` )

Required. The DataObject to create.
