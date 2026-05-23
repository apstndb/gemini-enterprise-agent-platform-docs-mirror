---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.datasets/list
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.datasets/list
title: 'Method: datasets.list'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.datasets.list

Lists Datasets in a Location.

### Endpoint

get `https: / /{service-endpoint} /v1beta1 /{parent} /datasets`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`parent` `string`

Required. The name of the Dataset's parent resource. Format: `projects/{project}/locations/{location}`

### Query parameters

`filter` `string`

An expression for filtering the results of the request. For field names both snake\_case and camelCase are supported.

  - `displayName` : supports = and \!=
  - `metadataSchemaUri` : supports = and \!=
  - `labels` supports general map functions that is:
      - `labels.key=value` - key:value equality
      - \`labels.key:\* or labels:key - key existence
      - A key including a space must be quoted. `labels."a key"` .

Some examples:

  - `displayName="myDisplayName"`
  - `labels.myKey="myValue"`

`pageSize` `integer`

The standard list page size.

`pageToken` `string`

The standard list page token.

`readMask` ` string ( FieldMask  ` format)

Mask specifying which fields to read.

This is a comma-separated list of fully qualified names of fields. Example: `"user.displayName,photo"` .

`orderBy` `string`

A comma-separated list of fields to order by, sorted in ascending order. Use "desc" after a field name for descending. Supported fields:

  - `displayName`
  - `createTime`
  - `updateTime`

### Request body

The request body must be empty.

### Response body

Response message for `  DatasetService.ListDatasets  ` .

If successful, the response body contains data with the following structure:

Fields

`datasets[]` ` object ( Dataset  ` )

A list of Datasets that matches the specified filter in the request.

`nextPageToken` `string`

The standard List next-page token.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;datasets&quot;: [{object (Dataset)}],&quot;nextPageToken&quot;: string}</code></pre></td>
</tr>
</tbody>
</table>
