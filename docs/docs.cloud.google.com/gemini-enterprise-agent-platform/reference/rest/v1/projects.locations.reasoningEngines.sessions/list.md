---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.reasoningEngines.sessions/list
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.reasoningEngines.sessions/list
title: 'Method: sessions.list'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.reasoningEngines.sessions.list

Lists [`Sessions`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.reasoningEngines.sessions#Session) in a given reasoning engine.

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

Optional. The [`nextPageToken`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.reasoningEngines.sessions/list#body.ListSessionsResponse.FIELDS.next_page_token) value returned from a previous list [`SessionService.ListSessions`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.reasoningEngines.sessions/list#google.cloud.aiplatform.v1.SessionService.ListSessions) call.

`filter` `string`

Optional. The standard list filter. Supported fields: \* `displayName` \* `userId` \* `labels`

Example: `displayName="abc"` , `userId="123"` , `labels.key="value"` .

`orderBy` `string`

Optional. A comma-separated list of fields to order by, sorted in ascending order. Use "desc" after a field name for descending. Supported fields: \* `createTime` \* `updateTime`

Example: `createTime desc` .

### Request body

The request body must be empty.

### Response body

Response message for [`SessionService.ListSessions`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.reasoningEngines.sessions/list#google.cloud.aiplatform.v1.SessionService.ListSessions) .

If successful, the response body contains data with the following structure:

Fields

`sessions[]` `object ( `[`Session`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.reasoningEngines.sessions#Session)` )`

A list of sessions matching the request.

`nextPageToken` `string`

A token, which can be sent as [`ListSessionsRequest.page_token`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.reasoningEngines.sessions/list#body.QUERY_PARAMETERS.page_token) to retrieve the next page. Absence of this field indicates there are no subsequent pages.

**JSON representation**

```
{
  "sessions": [
    {
      object (Session)
    }
  ],
  "nextPageToken": string
}
```
