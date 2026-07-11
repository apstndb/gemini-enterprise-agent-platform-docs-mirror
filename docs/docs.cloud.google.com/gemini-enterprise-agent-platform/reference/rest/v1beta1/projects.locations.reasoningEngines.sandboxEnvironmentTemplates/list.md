---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.reasoningEngines.sandboxEnvironmentTemplates/list
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.reasoningEngines.sandboxEnvironmentTemplates/list
title: 'Method: sandboxEnvironmentTemplates.list'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.reasoningEngines.sandboxEnvironmentTemplates.list

Lists `  SandboxEnvironmentTemplate  ` s in a given reasoning engine.

### Endpoint

get `https: / /{service-endpoint} /v1beta1 /{parent} /sandboxEnvironmentTemplates`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`parent` `string`

Required. The resource name of the reasoning engine to list sandbox environment templates from. Format: `projects/{project}/locations/{location}/reasoningEngines/{reasoningEngine}`

### Query parameters

`filter` `string`

Optional. The standard list filter. More detail in [AIP-160](https://google.aip.dev/160) .

`pageSize` `integer`

Optional. The maximum number of SandboxEnvironmentTemplates to return. The service may return fewer than this value. If unspecified, at most 100 SandboxEnvironmentTemplates will be returned.

`pageToken` `string`

Optional. The standard list page token, received from a previous `sandboxEnvironmentTemplates.list` call. Provide this to retrieve the subsequent page.

### Request body

The request body must be empty.

### Response body

Response message for `  SandboxEnvironmentService.ListSandboxEnvironmentTemplates  ` .

If successful, the response body contains data with the following structure:

Fields

`sandboxEnvironmentTemplates[]` ` object ( SandboxEnvironmentTemplate  ` )

The SandboxEnvironmentTemplates matching the request.

`nextPageToken` `string`

A token, which can be sent as `  ListSandboxEnvironmentTemplatesRequest.page_token  ` to retrieve the next page. Absence of this field indicates there are no subsequent pages.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;sandboxEnvironmentTemplates&quot;: [{object (SandboxEnvironmentTemplate)}],&quot;nextPageToken&quot;: string}</code></pre></td>
</tr>
</tbody>
</table>
