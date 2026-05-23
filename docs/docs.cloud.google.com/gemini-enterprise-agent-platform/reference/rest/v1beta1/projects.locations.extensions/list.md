---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.extensions/list
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.extensions/list
title: 'Method: extensions.list'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.extensions.list

Lists extensions in a location.

### Endpoint

get `https: / /{service-endpoint} /v1beta1 /{parent} /extensions`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`parent` `string`

Required. The resource name of the Location to list the extensions from. Format: `projects/{project}/locations/{location}`

### Query parameters

`filter` `string`

Optional. The standard list filter. Supported fields: \* `displayName` \* `createTime` \* `updateTime`

More detail in [AIP-160](https://google.aip.dev/160) .

`pageSize` `integer`

Optional. The standard list page size.

`pageToken` `string`

Optional. The standard list page token.

`orderBy` `string`

Optional. A comma-separated list of fields to order by, sorted in ascending order. Use "desc" after a field name for descending. Supported fields: \* `displayName` \* `createTime` \* `updateTime`

Example: `displayName, createTime desc` .

### Request body

The request body must be empty.

### Response body

Response message for `  ExtensionRegistryService.ListExtensions  `

If successful, the response body contains data with the following structure:

Fields

`extensions[]` ` object ( Extension  ` )

List of Extension in the requested page.

`nextPageToken` `string`

A token to retrieve the next page of results. Pass to `  ListExtensionsRequest.page_token  ` to obtain that page.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;extensions&quot;: [{object (Extension)}],&quot;nextPageToken&quot;: string}</code></pre></td>
</tr>
</tbody>
</table>
