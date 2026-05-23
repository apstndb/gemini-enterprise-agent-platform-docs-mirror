---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.featurestores/list
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.featurestores/list
title: 'Method: featurestores.list'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.featurestores.list

Lists Featurestores in a given project and location.

### Endpoint

get `https: / /{service-endpoint} /v1 /{parent} /featurestores`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`parent` `string`

Required. The resource name of the Location to list Featurestores. Format: `projects/{project}/locations/{location}`

### Query parameters

`filter` `string`

Lists the featurestores that match the filter expression. The following fields are supported:

  - `createTime` : Supports `=` , `!=` , `<` , `>` , `<=` , and `>=` comparisons. Values must be in RFC 3339 format.
  - `updateTime` : Supports `=` , `!=` , `<` , `>` , `<=` , and `>=` comparisons. Values must be in RFC 3339 format.
  - `onlineServingConfig.fixed_node_count` : Supports `=` , `!=` , `<` , `>` , `<=` , and `>=` comparisons.
  - `labels` : Supports key-value equality and key presence.

Examples:

  - `createTime > "2020-01-01" OR updateTime > "2020-01-01"` Featurestores created or updated after 2020-01-01.
  - `labels.env = "prod"` Featurestores with label "env" set to "prod".

`pageSize` `integer`

The maximum number of Featurestores to return. The service may return fewer than this value. If unspecified, at most 100 Featurestores will be returned. The maximum value is 100; any value greater than 100 will be coerced to 100.

`pageToken` `string`

A page token, received from a previous `  FeaturestoreService.ListFeaturestores  ` call. Provide this to retrieve the subsequent page.

When paginating, all other parameters provided to `  FeaturestoreService.ListFeaturestores  ` must match the call that provided the page token.

`orderBy` `string`

A comma-separated list of fields to order by, sorted in ascending order. Use "desc" after a field name for descending. Supported Fields:

  - `createTime`
  - `updateTime`
  - `onlineServingConfig.fixed_node_count`

`readMask` ` string ( FieldMask  ` format)

Mask specifying which fields to read.

This is a comma-separated list of fully qualified names of fields. Example: `"user.displayName,photo"` .

### Request body

The request body must be empty.

### Response body

Response message for `  FeaturestoreService.ListFeaturestores  ` .

If successful, the response body contains data with the following structure:

Fields

`featurestores[]` ` object ( Featurestore  ` )

The Featurestores matching the request.

`nextPageToken` `string`

A token, which can be sent as `  ListFeaturestoresRequest.page_token  ` to retrieve the next page. If this field is omitted, there are no subsequent pages.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;featurestores&quot;: [{object (Featurestore)}],&quot;nextPageToken&quot;: string}</code></pre></td>
</tr>
</tbody>
</table>
