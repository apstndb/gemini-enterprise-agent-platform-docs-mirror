---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.pipelineJobs/list
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.pipelineJobs/list
title: 'Method: pipelineJobs.list'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.pipelineJobs.list

Lists PipelineJobs in a Location.

### Endpoint

get `https: / /{service-endpoint} /v1 /{parent} /pipelineJobs`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`parent` `string`

Required. The resource name of the Location to list the PipelineJobs from. Format: `projects/{project}/locations/{location}`

### Query parameters

`filter` `string`

Lists the PipelineJobs that match the filter expression. The following fields are supported:

  - `pipelineName` : Supports `=` and `!=` comparisons.
  - `displayName` : Supports `=` , `!=` comparisons, and `:` wildcard.
  - `pipelineJobUserId` : Supports `=` , `!=` comparisons, and `:` wildcard. for example, can check if pipeline's displayName contains *step* by doing displayName:"\*step\*"
  - `state` : Supports `=` and `!=` comparisons.
  - `createTime` : Supports `=` , `!=` , `<` , `>` , `<=` , and `>=` comparisons. Values must be in RFC 3339 format.
  - `updateTime` : Supports `=` , `!=` , `<` , `>` , `<=` , and `>=` comparisons. Values must be in RFC 3339 format.
  - `endTime` : Supports `=` , `!=` , `<` , `>` , `<=` , and `>=` comparisons. Values must be in RFC 3339 format.
  - `labels` : Supports key-value equality and key presence.
  - `templateUri` : Supports `=` , `!=` comparisons, and `:` wildcard.
  - `templateMetadata.version` : Supports `=` , `!=` comparisons, and `:` wildcard.

Filter expressions can be combined together using logical operators ( `AND` & `OR` ). For example: `pipelineName="test" AND createTime>"2020-05-18T13:30:00Z"` .

The syntax to define filter expression is based on <https://google.aip.dev/160> .

Examples:

  - `createTime>"2021-05-18T00:00:00Z" OR updateTime>"2020-05-18T00:00:00Z"` PipelineJobs created or updated after 2020-05-18 00:00:00 UTC.
  - `labels.env = "prod"` PipelineJobs with label "env" set to "prod".

`pageSize` `integer`

The standard list page size.

`pageToken` `string`

The standard list page token. Typically obtained via `  ListPipelineJobsResponse.next_page_token  ` of the previous `  PipelineService.ListPipelineJobs  ` call.

`orderBy` `string`

A comma-separated list of fields to order by. The default sort order is in ascending order. Use "desc" after a field name for descending. You can have multiple orderBy fields provided e.g. "createTime desc, endTime", "endTime, startTime, updateTime" For example, using "createTime desc, endTime" will order results by create time in descending order, and if there are multiple jobs having the same create time, order them by the end time in ascending order. if orderBy is not specified, it will order by default order is create time in descending order. Supported fields:

  - `createTime`
  - `updateTime`
  - `endTime`
  - `startTime`

`readMask` ` string ( FieldMask  ` format)

Mask specifying which fields to read.

This is a comma-separated list of fully qualified names of fields. Example: `"user.displayName,photo"` .

### Request body

The request body must be empty.

### Response body

Response message for `  PipelineService.ListPipelineJobs  `

If successful, the response body contains data with the following structure:

Fields

`pipelineJobs[]` ` object ( PipelineJob  ` )

List of PipelineJobs in the requested page.

`nextPageToken` `string`

A token to retrieve the next page of results. Pass to `  ListPipelineJobsRequest.page_token  ` to obtain that page.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;pipelineJobs&quot;: [{object (PipelineJob)}],&quot;nextPageToken&quot;: string}</code></pre></td>
</tr>
</tbody>
</table>
