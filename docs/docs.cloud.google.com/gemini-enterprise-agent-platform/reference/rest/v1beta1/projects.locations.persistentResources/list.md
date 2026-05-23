---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.persistentResources/list
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.persistentResources/list
title: 'Method: persistentResources.list'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.persistentResources.list

Lists PersistentResources in a Location.

### Endpoint

get `https: / /{service-endpoint} /v1beta1 /{parent} /persistentResources`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`parent` `string`

Required. The resource name of the Location to list the PersistentResources from. Format: `projects/{project}/locations/{location}`

### Query parameters

`pageSize` `integer`

Optional. The standard list page size.

`pageToken` `string`

Optional. The standard list page token. Typically obtained via `  ListPersistentResourcesResponse.next_page_token  ` of the previous \[PersistentResourceService.ListPersistentResource\]\[\] call.

### Request body

The request body must be empty.

### Response body

Response message for `  PersistentResourceService.ListPersistentResources  `

If successful, the response body contains data with the following structure:

Fields

`persistentResources[]` ` object ( PersistentResource  ` )

`nextPageToken` `string`

A token to retrieve next page of results. Pass to `  ListPersistentResourcesRequest.page_token  ` to obtain that page.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;persistentResources&quot;: [{object (PersistentResource)}],&quot;nextPageToken&quot;: string}</code></pre></td>
</tr>
</tbody>
</table>
