---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.schedules/list
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.schedules/list
title: 'Method: schedules.list'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.schedules.list

Lists Schedules in a Location.

### Endpoint

get `https: / /{service-endpoint} /v1 /{parent} /schedules`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`parent` `string`

Required. The resource name of the Location to list the Schedules from. Format: `projects/{project}/locations/{location}`

### Query parameters

`filter` `string`

Lists the Schedules that match the filter expression. The following fields are supported:

  - `displayName` : Supports `=` , `!=` comparisons, and `:` wildcard.
  - `state` : Supports `=` and `!=` comparisons.
  - `request` : Supports existence of the check. (e.g. `createPipelineJobRequest:*` --\> Schedule has createPipelineJobRequest).
  - `createTime` : Supports `=` , `!=` , `<` , `>` , `<=` , and `>=` comparisons. Values must be in RFC 3339 format.
  - `startTime` : Supports `=` , `!=` , `<` , `>` , `<=` , and `>=` comparisons. Values must be in RFC 3339 format.
  - `endTime` : Supports `=` , `!=` , `<` , `>` , `<=` , `>=` comparisons and `:*` existence check. Values must be in RFC 3339 format.
  - `nextRunTime` : Supports `=` , `!=` , `<` , `>` , `<=` , and `>=` comparisons. Values must be in RFC 3339 format.

Filter expressions can be combined together using logical operators ( `NOT` , `AND` & `OR` ). The syntax to define filter expression is based on <https://google.aip.dev/160> .

Examples:

  - `state="ACTIVE" AND displayName:"my_schedule_*"`
  - `NOT displayName="my_schedule"`
  - `createTime>"2021-05-18T00:00:00Z"`
  - `endTime>"2021-05-18T00:00:00Z" OR NOT endTime:*`
  - `createPipelineJobRequest:*`

`pageSize` `integer`

The standard list page size. Default to 100 if not specified.

`pageToken` `string`

The standard list page token. Typically obtained via `  ListSchedulesResponse.next_page_token  ` of the previous `  ScheduleService.ListSchedules  ` call.

`orderBy` `string`

A comma-separated list of fields to order by. The default sort order is in ascending order. Use "desc" after a field name for descending. You can have multiple orderBy fields provided.

For example, using "createTime desc, endTime" will order results by create time in descending order, and if there are multiple schedules having the same create time, order them by the end time in ascending order.

If orderBy is not specified, it will order by default with createTime in descending order.

Supported fields:

  - `createTime`
  - `startTime`
  - `endTime`
  - `nextRunTime`

### Request body

The request body must be empty.

### Response body

Response message for `  ScheduleService.ListSchedules  `

If successful, the response body contains data with the following structure:

Fields

`schedules[]` ` object ( Schedule  ` )

List of Schedules in the requested page.

`nextPageToken` `string`

A token to retrieve the next page of results. Pass to `  ListSchedulesRequest.page_token  ` to obtain that page.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;schedules&quot;: [{object (Schedule)}],&quot;nextPageToken&quot;: string}</code></pre></td>
</tr>
</tbody>
</table>
