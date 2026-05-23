---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.featureOnlineStores.featureViews.featureViewSyncs/list
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.featureOnlineStores.featureViews.featureViewSyncs/list
title: 'Method: featureViewSyncs.list'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.featureOnlineStores.featureViews.featureViewSyncs.list

Lists FeatureViewSyncs in a given FeatureView.

### Endpoint

get `https: / /{service-endpoint} /v1beta1 /{parent} /featureViewSyncs`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`parent` `string`

Required. The resource name of the FeatureView to list FeatureViewSyncs. Format: `projects/{project}/locations/{location}/featureOnlineStores/{featureOnlineStore}/featureViews/{featureView}`

### Query parameters

`filter` `string`

Lists the FeatureViewSyncs that match the filter expression. The following filters are supported:

  - `createTime` : Supports `=` , `!=` , `<` , `>` , `>=` , and `<=` comparisons. Values must be in RFC 3339 format.

Examples:

  - `createTime > \"2020-01-31T15:30:00.000000Z\"` --\> FeatureViewSyncs created after 2020-01-31T15:30:00.000000Z.

`pageSize` `integer`

The maximum number of FeatureViewSyncs to return. The service may return fewer than this value. If unspecified, at most 1000 FeatureViewSyncs will be returned. The maximum value is 1000; any value greater than 1000 will be coerced to 1000.

`pageToken` `string`

A page token, received from a previous `  FeatureOnlineStoreAdminService.ListFeatureViewSyncs  ` call. Provide this to retrieve the subsequent page.

When paginating, all other parameters provided to `  FeatureOnlineStoreAdminService.ListFeatureViewSyncs  ` must match the call that provided the page token.

`orderBy` `string`

A comma-separated list of fields to order by, sorted in ascending order. Use "desc" after a field name for descending.

Supported fields:

  - `createTime`

### Request body

The request body must be empty.

### Response body

Response message for `  FeatureOnlineStoreAdminService.ListFeatureViewSyncs  ` .

If successful, the response body contains data with the following structure:

Fields

`featureViewSyncs[]` ` object ( FeatureViewSync  ` )

The FeatureViewSyncs matching the request.

`nextPageToken` `string`

A token, which can be sent as `  ListFeatureViewSyncsRequest.page_token  ` to retrieve the next page. If this field is omitted, there are no subsequent pages.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;featureViewSyncs&quot;: [{object (FeatureViewSync)}],&quot;nextPageToken&quot;: string}</code></pre></td>
</tr>
</tbody>
</table>
