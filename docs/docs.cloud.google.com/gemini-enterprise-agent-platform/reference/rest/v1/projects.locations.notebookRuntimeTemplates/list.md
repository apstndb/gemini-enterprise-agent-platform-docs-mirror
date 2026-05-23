---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.notebookRuntimeTemplates/list
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.notebookRuntimeTemplates/list
title: 'Method: notebookRuntimeTemplates.list'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.notebookRuntimeTemplates.list

Lists NotebookRuntimeTemplates in a Location.

### Endpoint

get `https: / /{service-endpoint} /v1 /{parent} /notebookRuntimeTemplates`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`parent` `string`

Required. The resource name of the Location from which to list the NotebookRuntimeTemplates. Format: `projects/{project}/locations/{location}`

### Query parameters

`filter` `string`

Optional. An expression for filtering the results of the request. For field names both snake\_case and camelCase are supported.

  - `notebookRuntimeTemplate` supports = and \!=. `notebookRuntimeTemplate` represents the NotebookRuntimeTemplate id, i.e. the last segment of the NotebookRuntimeTemplate's `  resource name  ` .
  - `displayName` supports = and \!=
  - `labels` supports general map functions that is:
      - `labels.key=value` - key:value equality
      - \`labels.key:\* or labels:key - key existence
      - A key including a space must be quoted. `labels."a key"` .
  - `notebookRuntimeType` supports = and \!=. notebookRuntimeType enum: \[USER\_DEFINED, ONE\_CLICK\].
  - `machineType` supports = and \!=.
  - `acceleratorType` supports = and \!=.

Some examples:

  - `notebookRuntimeTemplate=notebookRuntimeTemplate123`
  - `displayName="myDisplayName"`
  - `labels.myKey="myValue"`
  - `notebookRuntimeType=USER_DEFINED`
  - `machineType=e2-standard-4`
  - `acceleratorType=NVIDIA_TESLA_T4`

`pageSize` `integer`

Optional. The standard list page size.

`pageToken` `string`

Optional. The standard list page token. Typically obtained via `  ListNotebookRuntimeTemplatesResponse.next_page_token  ` of the previous `  NotebookService.ListNotebookRuntimeTemplates  ` call.

`readMask` ` string ( FieldMask  ` format)

Optional. Mask specifying which fields to read.

This is a comma-separated list of fully qualified names of fields. Example: `"user.displayName,photo"` .

`orderBy` `string`

Optional. A comma-separated list of fields to order by, sorted in ascending order. Use "desc" after a field name for descending. Supported fields:

  - `displayName`
  - `createTime`
  - `updateTime`

Example: `displayName, createTime desc` .

### Request body

The request body must be empty.

### Response body

Response message for `  NotebookService.ListNotebookRuntimeTemplates  ` .

If successful, the response body contains data with the following structure:

Fields

`notebookRuntimeTemplates[]` ` object ( NotebookRuntimeTemplate  ` )

List of NotebookRuntimeTemplates in the requested page.

`nextPageToken` `string`

A token to retrieve next page of results. Pass to `  ListNotebookRuntimeTemplatesRequest.page_token  ` to obtain that page.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;notebookRuntimeTemplates&quot;: [{object (NotebookRuntimeTemplate)}],&quot;nextPageToken&quot;: string}</code></pre></td>
</tr>
</tbody>
</table>
