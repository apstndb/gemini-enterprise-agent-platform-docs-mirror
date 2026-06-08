---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.agents/list
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.agents/list
title: 'Method: agents.list'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.agents.list

Lists agents in a location.

### Endpoint

get `https: / /{service-endpoint} /v1beta1 /{parent} /agents`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`parent` `string`

Required. The resource name of the location to list agents from. Format: `projects/{project}/locations/{location}` .

### Query parameters

`pageSize` `integer`

Optional. The maximum number of agents to return. The service may return fewer than this value. The maximum page size is 100; values above 100 will be coerced to 100. If unspecified, the default page size is 10.

`pageToken` `string`

Optional. A page token, received from a previous `  AgentService.ListAgents  ` call. Provide this to retrieve the subsequent page.

`orderBy` `string`

Optional. A comma-separated list of fields to order by. Supported fields:

  - `created`
  - `updated`

Use `desc` after a field name for descending order. Example: `created desc` .

### Request body

The request body must be empty.

### Response body

Response message for `  AgentService.ListAgents  ` .

If successful, the response body contains data with the following structure:

Fields

`agents[]` ` object ( Agent  ` )

The agents matching the request.

`nextPageToken` `string`

A token to retrieve the next page of results. Pass this value as `  ListAgentsRequest.page_token  ` in a subsequent call.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;agents&quot;: [{object (Agent)}],&quot;nextPageToken&quot;: string}</code></pre></td>
</tr>
</tbody>
</table>
