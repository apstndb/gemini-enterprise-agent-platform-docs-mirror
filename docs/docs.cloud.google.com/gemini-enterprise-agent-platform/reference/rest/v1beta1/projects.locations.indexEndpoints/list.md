---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.indexEndpoints/list
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.indexEndpoints/list
title: 'Method: indexEndpoints.list'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.indexEndpoints.list

Lists IndexEndpoints in a Location.

### Endpoint

get `https: / /{service-endpoint} /v1beta1 /{parent} /indexEndpoints`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`parent` `string`

Required. The resource name of the Location from which to list the IndexEndpoints. Format: `projects/{project}/locations/{location}`

### Query parameters

`filter` `string`

Optional. An expression for filtering the results of the request. For field names both snake\_case and camelCase are supported.

  - `indexEndpoint` supports = and \!=. `indexEndpoint` represents the IndexEndpoint id, ie. the last segment of the IndexEndpoint's `  resourcename  ` .
  - `displayName` supports =, \!= and regex() (uses [re2](https://github.com/google/re2/wiki/Syntax) syntax)
  - `labels` supports general map functions that is: `labels.key=value` - key:value equality `labels.key:* or labels:key - key existence A key including a space must be quoted.` labels."a key"\`.

Some examples: \* `indexEndpoint="1"` \* `displayName="myDisplayName"` \* `regex(displayName, "^A") -> The display name starts with an A. *` labels.myKey="myValue"\`

`pageSize` `integer`

Optional. The standard list page size.

`pageToken` `string`

Optional. The standard list page token. Typically obtained via `  ListIndexEndpointsResponse.next_page_token  ` of the previous `  IndexEndpointService.ListIndexEndpoints  ` call.

`readMask` ` string ( FieldMask  ` format)

Optional. Mask specifying which fields to read.

This is a comma-separated list of fully qualified names of fields. Example: `"user.displayName,photo"` .

### Request body

The request body must be empty.

### Response body

Response message for `  IndexEndpointService.ListIndexEndpoints  ` .

If successful, the response body contains data with the following structure:

Fields

`indexEndpoints[]` ` object ( IndexEndpoint  ` )

List of IndexEndpoints in the requested page.

`nextPageToken` `string`

A token to retrieve next page of results. Pass to `  ListIndexEndpointsRequest.page_token  ` to obtain that page.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;indexEndpoints&quot;: [{object (IndexEndpoint)}],&quot;nextPageToken&quot;: string}</code></pre></td>
</tr>
</tbody>
</table>
