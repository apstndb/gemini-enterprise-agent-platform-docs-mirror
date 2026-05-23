---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.datasets.dataItems/list
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.datasets.dataItems/list
title: 'Method: dataItems.list'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.datasets.dataItems.list

Lists DataItems in a Dataset.

### Endpoint

get `https: / /{service-endpoint} /v1beta1 /{parent} /dataItems`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`parent` `string`

Required. The resource name of the Dataset to list DataItems from. Format: `projects/{project}/locations/{location}/datasets/{dataset}`

### Query parameters

`filter` `string`

The standard list filter.

`pageSize` `integer`

The standard list page size.

`pageToken` `string`

The standard list page token.

`readMask` ` string ( FieldMask  ` format)

Mask specifying which fields to read.

This is a comma-separated list of fully qualified names of fields. Example: `"user.displayName,photo"` .

`orderBy` `string`

A comma-separated list of fields to order by, sorted in ascending order. Use "desc" after a field name for descending.

### Request body

The request body must be empty.

### Response body

Response message for `  DatasetService.ListDataItems  ` .

If successful, the response body contains data with the following structure:

Fields

`dataItems[]` ` object ( DataItem  ` )

A list of DataItems that matches the specified filter in the request.

`nextPageToken` `string`

The standard List next-page token.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;dataItems&quot;: [{object (DataItem)}],&quot;nextPageToken&quot;: string}</code></pre></td>
</tr>
</tbody>
</table>
