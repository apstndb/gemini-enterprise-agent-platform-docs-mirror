---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.exampleStores/list
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.exampleStores/list
title: 'Method: exampleStores.list'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.exampleStores.list

List ExampleStores in a Location.

### Endpoint

get `https: / /{service-endpoint} /v1beta1 /{parent} /exampleStores`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`parent` `string`

Required. The resource name of the Location to list the ExampleStores from. Format: `projects/{project}/locations/{location}`

### Query parameters

`filter` `string`

Optional. The standard list filter. More detail in [AIP-160](https://google.aip.dev/160) .

`pageSize` `integer`

Optional. The standard list page size.

`pageToken` `string`

Optional. The standard list page token.

### Request body

The request body must be empty.

### Response body

Response message for `  ExampleStoreService.ListExampleStores  ` .

If successful, the response body contains data with the following structure:

Fields

`exampleStores[]` ` object ( ExampleStore  ` )

List of ExampleStore in the requested page.

`nextPageToken` `string`

A token to retrieve the next page of results. Pass to `  ListExampleStoresRequest.page_token  ` to obtain that page.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;exampleStores&quot;: [{object (ExampleStore)}],&quot;nextPageToken&quot;: string}</code></pre></td>
</tr>
</tbody>
</table>
