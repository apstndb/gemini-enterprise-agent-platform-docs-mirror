---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.featureGroups.featureMonitors/list
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.featureGroups.featureMonitors/list
title: 'Method: featureMonitors.list'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.featureGroups.featureMonitors.list

Lists FeatureGroups in a given project and location.

### Endpoint

get `https: / /{service-endpoint} /v1beta1 /{parent} /featureMonitors`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`parent` `string`

Required. The resource name of the FeatureGroup to list FeatureMonitors. Format: `projects/{project}/locations/{location}/featureGroups/{featureGroup}`

### Query parameters

`filter` `string`

Optional. Lists the FeatureMonitors that match the filter expression. The following fields are supported:

  - `createTime` : Supports `=` , `!=` , `<` , `>` , `<=` , and `>=` comparisons. Values must be in RFC 3339 format.
  - `updateTime` : Supports `=` , `!=` , `<` , `>` , `<=` , and `>=` comparisons. Values must be in RFC 3339 format.
  - `labels` : Supports key-value equality and key presence.

Examples:

  - `createTime > "2020-01-01" OR updateTime > "2020-01-01"` FeatureMonitors created or updated after 2020-01-01.
  - `labels.env = "prod"` FeatureGroups with label "env" set to "prod".

`pageSize` `integer`

Optional. The maximum number of FeatureGroups to return. The service may return fewer than this value. If unspecified, at most 100 FeatureMonitors will be returned. The maximum value is 100; any value greater than 100 will be coerced to 100.

`pageToken` `string`

Optional. A page token, received from a previous `  FeatureRegistryService.ListFeatureMonitors  ` call. Provide this to retrieve the subsequent page.

When paginating, all other parameters provided to `  FeatureRegistryService.ListFeatureMonitors  ` must match the call that provided the page token.

`orderBy` `string`

Optional. A comma-separated list of fields to order by, sorted in ascending order. Use "desc" after a field name for descending. Supported Fields:

  - `createTime`
  - `updateTime`

### Request body

The request body must be empty.

### Response body

Response message for `  FeatureRegistryService.ListFeatureMonitors  ` .

If successful, the response body contains data with the following structure:

Fields

`featureMonitors[]` ` object ( FeatureMonitor  ` )

The FeatureMonitors matching the request.

`nextPageToken` `string`

A token, which can be sent as `  ListFeatureMonitorsRequest.page_token  ` to retrieve the next page. If this field is omitted, there are no subsequent pages.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;featureMonitors&quot;: [{object (FeatureMonitor)}],&quot;nextPageToken&quot;: string}</code></pre></td>
</tr>
</tbody>
</table>
