---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.reasoningEngines.sessions/list
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.reasoningEngines.sessions/list
title: 'Method: sessions.list'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.reasoningEngines.sessions.list

Lists `  Sessions  ` in a given reasoning engine.

### Endpoint

get `https: / /{service-endpoint} /v1 /{parent} /sessions`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`parent` `string`

Required. The resource name of the location to list sessions from. Format: `projects/{project}/locations/{location}/reasoningEngines/{reasoningEngine}`

### Query parameters

`pageSize` `integer`

Optional. The maximum number of sessions to return. The service may return fewer than this value. If unspecified, the default page size is 100. Values greater than 100 will be capped at 100.

`pageToken` `string`

Optional. The `  nextPageToken  ` value returned from a previous list `  SessionService.ListSessions  ` call.

`filter` `string`

Optional. The standard list filter. Supported fields: \* `displayName` \* `userId` \* `labels`

Example: `displayName="abc"` , `userId="123"` , `labels.key="value"` .

`orderBy` `string`

Optional. A comma-separated list of fields to order by, sorted in ascending order. Use "desc" after a field name for descending. Supported fields: \* `createTime` \* `updateTime`

Example: `createTime desc` .

### Request body

The request body must be empty.

### Response body

Response message for `  SessionService.ListSessions  ` .

If successful, the response body contains data with the following structure:

Fields

`sessions[]` ` object ( Session  ` )

A list of sessions matching the request.

`nextPageToken` `string`

A token, which can be sent as `  ListSessionsRequest.page_token  ` to retrieve the next page. Absence of this field indicates there are no subsequent pages.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;sessions&quot;: [{object (Session)}],&quot;nextPageToken&quot;: string}</code></pre></td>
</tr>
</tbody>
</table>
