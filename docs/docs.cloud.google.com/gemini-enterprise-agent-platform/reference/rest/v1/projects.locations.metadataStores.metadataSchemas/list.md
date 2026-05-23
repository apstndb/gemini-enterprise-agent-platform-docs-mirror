---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.metadataStores.metadataSchemas/list
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.metadataStores.metadataSchemas/list
title: 'Method: metadataSchemas.list'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.metadataStores.metadataSchemas.list

Lists MetadataSchemas.

### Endpoint

get `https: / /{service-endpoint} /v1 /{parent} /metadataSchemas`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`parent` `string`

Required. The MetadataStore whose MetadataSchemas should be listed. Format: `projects/{project}/locations/{location}/metadataStores/{metadatastore}`

### Query parameters

`pageSize` `integer`

The maximum number of MetadataSchemas to return. The service may return fewer. Must be in range 1-100, inclusive. Defaults to 100.

`pageToken` `string`

A page token, received from a previous `  MetadataService.ListMetadataSchemas  ` call. Provide this to retrieve the next page.

When paginating, all other provided parameters must match the call that provided the page token. (Otherwise the request will fail with INVALID\_ARGUMENT error.)

`filter` `string`

A query to filter available MetadataSchemas for matching results.

### Request body

The request body must be empty.

### Response body

Response message for `  MetadataService.ListMetadataSchemas  ` .

If successful, the response body contains data with the following structure:

Fields

`metadataSchemas[]` ` object ( MetadataSchema  ` )

The MetadataSchemas found for the MetadataStore.

`nextPageToken` `string`

A token, which can be sent as `  ListMetadataSchemasRequest.page_token  ` to retrieve the next page. If this field is not populated, there are no subsequent pages.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;metadataSchemas&quot;: [{object (MetadataSchema)}],&quot;nextPageToken&quot;: string}</code></pre></td>
</tr>
</tbody>
</table>
