---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.featureOnlineStores.featureViews/list
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.featureOnlineStores.featureViews/list
title: 'Method: featureViews.list'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.featureOnlineStores.featureViews.list

Lists FeatureViews in a given FeatureOnlineStore.

### Endpoint

get `https: / /{service-endpoint} /v1 /{parent} /featureViews`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`parent` `string`

Required. The resource name of the FeatureOnlineStore to list FeatureViews. Format: `projects/{project}/locations/{location}/featureOnlineStores/{featureOnlineStore}`

### Query parameters

`filter` `string`

Lists the FeatureViews that match the filter expression. The following filters are supported:

  - `createTime` : Supports `=` , `!=` , `<` , `>` , `>=` , and `<=` comparisons. Values must be in RFC 3339 format.
  - `updateTime` : Supports `=` , `!=` , `<` , `>` , `>=` , and `<=` comparisons. Values must be in RFC 3339 format.
  - `labels` : Supports key-value equality as well as key presence.

Examples:

  - `createTime > \"2020-01-31T15:30:00.000000Z\" OR updateTime > \"2020-01-31T15:30:00.000000Z\"` --\> FeatureViews created or updated after 2020-01-31T15:30:00.000000Z.
  - `labels.active = yes AND labels.env = prod` --\> FeatureViews having both (active: yes) and (env: prod) labels.
  - `labels.env: *` --\> Any FeatureView which has a label with 'env' as the key.

`pageSize` `integer`

The maximum number of FeatureViews to return. The service may return fewer than this value. If unspecified, at most 1000 FeatureViews will be returned. The maximum value is 1000; any value greater than 1000 will be coerced to 1000.

`pageToken` `string`

A page token, received from a previous `  FeatureOnlineStoreAdminService.ListFeatureViews  ` call. Provide this to retrieve the subsequent page.

When paginating, all other parameters provided to `  FeatureOnlineStoreAdminService.ListFeatureViews  ` must match the call that provided the page token.

`orderBy` `string`

A comma-separated list of fields to order by, sorted in ascending order. Use "desc" after a field name for descending.

Supported fields:

  - `featureViewId`
  - `createTime`
  - `updateTime`

### Request body

The request body must be empty.

### Response body

Response message for `  FeatureOnlineStoreAdminService.ListFeatureViews  ` .

If successful, the response body contains data with the following structure:

Fields

`featureViews[]` ` object ( FeatureView  ` )

The FeatureViews matching the request.

`nextPageToken` `string`

A token, which can be sent as `  ListFeatureViewsRequest.page_token  ` to retrieve the next page. If this field is omitted, there are no subsequent pages.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;featureViews&quot;: [{object (FeatureView)}],&quot;nextPageToken&quot;: string}</code></pre></td>
</tr>
</tbody>
</table>
