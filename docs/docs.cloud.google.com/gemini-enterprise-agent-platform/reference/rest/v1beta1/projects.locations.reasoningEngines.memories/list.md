---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.reasoningEngines.memories/list
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.reasoningEngines.memories/list
title: 'Method: memories.list'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.reasoningEngines.memories.list

List Memories.

### Endpoint

get `https: / /{service-endpoint} /v1beta1 /{parent} /memories`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`parent` `string`

Required. The resource name of the ReasoningEngine to list the Memories under. Format: `projects/{project}/locations/{location}/reasoningEngines/{reasoningEngine}`

### Query parameters

`filter` `string`

Optional. The standard list filter. More detail in [AIP-160](https://google.aip.dev/160) .

Supported fields: \* `scope` (as a JSON string with equality match only) \* `topics` (i.e. `topics.custom_memory_topic_label: "example topic" OR topics.managed_memory_topic: USER_PREFERENCES` )

`pageSize` `integer`

Optional. The standard list page size.

`pageToken` `string`

Optional. The standard list page token.

`orderBy` `string`

Optional. The standard list order by string. If not specified, the default order is `createTime desc` . If specified, the default sorting order of provided fields is ascending.

More detail in [AIP-132](https://google.aip.dev/132) .

Supported fields: \* `createTime` \* `updateTime`

### Request body

The request body must be empty.

### Response body

Response message for `  MemoryBankService.ListMemories  ` .

If successful, the response body contains data with the following structure:

Fields

`memories[]` ` object ( Memory  ` )

List of Memories in the requested page.

`nextPageToken` `string`

A token to retrieve the next page of results. Pass to `  ListMemoriesRequest.page_token  ` to obtain that page.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;memories&quot;: [{object (Memory)}],&quot;nextPageToken&quot;: string}</code></pre></td>
</tr>
</tbody>
</table>
