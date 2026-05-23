---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.reasoningEngines.sessions.events/list
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.reasoningEngines.sessions.events/list
title: 'Method: events.list'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.reasoningEngines.sessions.events.list

Lists `  events  ` in a given session.

### Endpoint

get `https: / /{service-endpoint} /v1beta1 /{parent} /events`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`parent` `string`

Required. The resource name of the session to list events from. Format: `projects/{project}/locations/{location}/reasoningEngines/{reasoningEngine}/sessions/{session}`

### Query parameters

`pageSize` `integer`

Optional. The maximum number of events to return. The service may return fewer than this value. If unspecified, at most 100 events will be returned. These events are ordered by timestamp in ascending order.

`pageToken` `string`

Optional. The `  nextPageToken  ` value returned from a previous list `  SessionService.ListEvents  ` call.

`filter` `string`

Optional. The standard list filter. Supported fields: \* `timestamp` range (i.e. `timestamp>="2025-01-31T11:30:00-04:00"` where the timestamp is in RFC 3339 format)

More detail in [AIP-160](https://google.aip.dev/160) .

`orderBy` `string`

Optional. A comma-separated list of fields to order by, sorted in ascending order. Use "desc" after a field name for descending. Supported fields: \* `timestamp`

Example: `timestamp desc` .

### Request body

The request body must be empty.

### Response body

Response message for `  SessionService.ListEvents  ` .

If successful, the response body contains data with the following structure:

Fields

`sessionEvents[]` ` object ( SessionEvent  ` )

A list of events matching the request. Ordered by timestamp in ascending order.

`nextPageToken` `string`

A token, which can be sent as `  ListEventsRequest.page_token  ` to retrieve the next page. Absence of this field indicates there are no subsequent pages.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;sessionEvents&quot;: [{object (SessionEvent)}],&quot;nextPageToken&quot;: string}</code></pre></td>
</tr>
</tbody>
</table>
