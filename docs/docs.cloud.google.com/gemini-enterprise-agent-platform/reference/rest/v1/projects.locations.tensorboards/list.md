---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.tensorboards/list
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.tensorboards/list
title: 'Method: tensorboards.list'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.tensorboards.list

Lists Tensorboards in a Location.

### Endpoint

get `https: / /{service-endpoint} /v1 /{parent} /tensorboards`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`parent` `string`

Required. The resource name of the Location to list Tensorboards. Format: `projects/{project}/locations/{location}`

### Query parameters

`filter` `string`

Lists the Tensorboards that match the filter expression.

`pageSize` `integer`

The maximum number of Tensorboards to return. The service may return fewer than this value. If unspecified, at most 100 Tensorboards are returned. The maximum value is 100; values above 100 are coerced to 100.

`pageToken` `string`

A page token, received from a previous `  TensorboardService.ListTensorboards  ` call. Provide this to retrieve the subsequent page.

When paginating, all other parameters provided to `  TensorboardService.ListTensorboards  ` must match the call that provided the page token.

`orderBy` `string`

Field to use to sort the list.

`readMask` ` string ( FieldMask  ` format)

Mask specifying which fields to read.

This is a comma-separated list of fully qualified names of fields. Example: `"user.displayName,photo"` .

### Request body

The request body must be empty.

### Response body

Response message for `  TensorboardService.ListTensorboards  ` .

If successful, the response body contains data with the following structure:

Fields

`tensorboards[]` ` object ( Tensorboard  ` )

The Tensorboards mathching the request.

`nextPageToken` `string`

A token, which can be sent as `  ListTensorboardsRequest.page_token  ` to retrieve the next page. If this field is omitted, there are no subsequent pages.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;tensorboards&quot;: [{object (Tensorboard)}],&quot;nextPageToken&quot;: string}</code></pre></td>
</tr>
</tbody>
</table>
