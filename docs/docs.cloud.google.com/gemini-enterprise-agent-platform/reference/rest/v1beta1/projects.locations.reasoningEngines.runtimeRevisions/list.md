---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.reasoningEngines.runtimeRevisions/list
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.reasoningEngines.runtimeRevisions/list
title: 'Method: runtimeRevisions.list'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.reasoningEngines.runtimeRevisions.list

Lists runtime revisions in a reasoning engine.

### Endpoint

get `https: / /{service-endpoint} /v1beta1 /{parent} /runtimeRevisions`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`parent` `string`

Required. The resource name of the ReasoningEngine to list the ReasoningEngineRuntimeRevisions from. Format: `projects/{project}/locations/{location}/reasoningEngines/{reasoningEngine}`

### Query parameters

`filter` `string`

Optional. The standard list filter. More detail in [AIP-160](https://google.aip.dev/160) .

`pageSize` `integer`

Optional. The maximum number of ReasoningEngineRuntimeRevisions to return. The service may return fewer than this value.

If unspecified, at most 50 revisions will be returned.

The maximum value is 100; values above 100 will be coerced to 100.

`pageToken` `string`

Optional. The standard list page token.

### Request body

The request body must be empty.

### Response body

Response message for `  ReasoningEngineRuntimeRevisionService.ListReasoningEngineRuntimeRevisions  `

If successful, the response body contains data with the following structure:

Fields

`reasoningEngineRuntimeRevisions[]` ` object ( ReasoningEngineRuntimeRevision  ` )

List of ReasoningEngineRuntimeRevisions in the requested page.

`nextPageToken` `string`

A token to retrieve the next page of results. Pass to `  ListReasoningEngineRuntimeRevisionsRequest.page_token  ` to obtain that page.

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;reasoningEngineRuntimeRevisions&quot;: [{object (ReasoningEngineRuntimeRevision)}],&quot;nextPageToken&quot;: string}</code></pre></td>
</tr>
</tbody>
</table>
