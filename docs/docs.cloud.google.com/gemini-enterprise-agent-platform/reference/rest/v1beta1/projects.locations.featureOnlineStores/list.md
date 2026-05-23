---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.featureOnlineStores/list
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.featureOnlineStores/list
title: 'Method: featureOnlineStores.list'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.featureOnlineStores.list

Lists FeatureOnlineStores in a given project and location.

### Endpoint

get `https: / /{service-endpoint} /v1beta1 /{parent} /featureOnlineStores`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`parent` `string`

Required. The resource name of the Location to list FeatureOnlineStores. Format: `projects/{project}/locations/{location}`

### Query parameters

`filter` `string`

Lists the FeatureOnlineStores that match the filter expression. The following fields are supported:

  - `createTime` : Supports `=` , `!=` , `<` , `>` , `<=` , and `>=` comparisons. Values must be in RFC 3339 format.
  - `updateTime` : Supports `=` , `!=` , `<` , `>` , `<=` , and `>=` comparisons. Values must be in RFC 3339 format.
  - `labels` : Supports key-value equality and key presence.

Examples:

  - `createTime > "2020-01-01" OR updateTime > "2020-01-01"` FeatureOnlineStores created or updated after 2020-01-01.
  - `labels.env = "prod"` FeatureOnlineStores with label "env" set to "prod".

`pageSize` `integer`

The maximum number of FeatureOnlineStores to return. The service may return fewer than this value. If unspecified, at most 100 FeatureOnlineStores will be returned. The maximum value is 100; any value greater than 100 will be coerced to 100.

`pageToken` `string`

A page token, received from a previous `  FeatureOnlineStoreAdminService.ListFeatureOnlineStores  ` call. Provide this to retrieve the subsequent page.

When paginating, all other parameters provided to `  FeatureOnlineStoreAdminService.ListFeatureOnlineStores  ` must match the call that provided the page token.

`orderBy` `string`

A comma-separated list of fields to order by, sorted in ascending order. Use "desc" after a field name for descending. Supported Fields:

  - `createTime`
  - `updateTime`

### Request body

The request body must be empty.

### Response body

Response message for `  FeatureOnlineStoreAdminService.ListFeatureOnlineStores  ` .

If successful, the response body contains data with the following structure:

Fields

`featureOnlineStores[]` ` object ( FeatureOnlineStore  ` )

The FeatureOnlineStores matching the request.

`nextPageToken` `string`

A token, which can be sent as `  ListFeatureOnlineStoresRequest.page_token  ` to retrieve the next page. If this field is omitted, there are no subsequent pages.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;featureOnlineStores&quot;: [{object (FeatureOnlineStore)}],&quot;nextPageToken&quot;: string}</code></pre></td>
</tr>
</tbody>
</table>
