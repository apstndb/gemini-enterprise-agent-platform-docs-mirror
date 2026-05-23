---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/rest/Shared.Types/ListLocationsRequest
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/rest/Shared.Types/ListLocationsRequest
title: ListLocationsRequest
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

The request message for `Locations.ListLocations` .

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;name&quot;: string,
  &quot;filter&quot;: string,
  &quot;pageSize&quot;: integer,
  &quot;pageToken&quot;: string,
  &quot;extraLocationTypes&quot;: [
    string
  ]
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`name`

`string`

The resource that owns the locations collection, if applicable.

`filter`

`string`

A filter to narrow down results to a preferred subset. The filtering language accepts strings like `"displayName=tokyo"` , and is documented in more detail in [AIP-160](https://google.aip.dev/160) .

`pageSize`

`integer`

The maximum number of results to return. If not set, the service selects a default.

`pageToken`

`string`

A page token received from the `nextPageToken` field in the response. Send that page token to receive the subsequent page.

`extraLocationTypes[]`

`string`

Optional. Do not use this field unless explicitly documented otherwise. This is primarily for internal usage.
