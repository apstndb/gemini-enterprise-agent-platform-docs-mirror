---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.models/listVersions
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.models/listVersions
title: 'Method: models.listVersions'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.models.listVersions

Lists versions of the specified model.

### Endpoint

get `https: / /{service-endpoint} /v1 /{name}:listVersions`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`name` `string`

Required. The name of the model to list versions for.

### Query parameters

`pageSize` `integer`

The standard list page size.

`pageToken` `string`

The standard list page token. Typically obtained via `  nextPageToken  ` of the previous `  models.listVersions  ` call.

`filter` `string`

An expression for filtering the results of the request. For field names both snake\_case and camelCase are supported.

  - `labels` supports general map functions that is:
      - `labels.key=value` - key:value equality
      - \`labels.key:\* or labels:key - key existence
      - A key including a space must be quoted. `labels."a key"` .

Some examples:

  - `labels.myKey="myValue"`

`readMask` ` string ( FieldMask  ` format)

Mask specifying which fields to read.

This is a comma-separated list of fully qualified names of fields. Example: `"user.displayName,photo"` .

`orderBy` `string`

A comma-separated list of fields to order by, sorted in ascending order. Use "desc" after a field name for descending. Supported fields:

  - `createTime`
  - `updateTime`

Example: `updateTime asc, createTime desc` .

### Request body

The request body must be empty.

### Response body

Response message for `  ModelService.ListModelVersions  `

If successful, the response body contains data with the following structure:

Fields

`models[]` ` object ( Model  ` )

List of Model versions in the requested page. In the returned Model name field, version id instead of regvision tag will be included.

`nextPageToken` `string`

A token to retrieve the next page of results. Pass to `  ListModelVersionsRequest.page_token  ` to obtain that page.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;models&quot;: [{object (Model)}],&quot;nextPageToken&quot;: string}</code></pre></td>
</tr>
</tbody>
</table>
