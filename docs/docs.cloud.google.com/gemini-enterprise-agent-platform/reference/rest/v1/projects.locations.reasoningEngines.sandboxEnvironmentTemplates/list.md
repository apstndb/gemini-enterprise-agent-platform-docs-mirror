---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.reasoningEngines.sandboxEnvironmentTemplates/list
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.reasoningEngines.sandboxEnvironmentTemplates/list
title: 'Method: sandboxEnvironmentTemplates.list'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.reasoningEngines.sandboxEnvironmentTemplates.list

Lists [`SandboxEnvironmentTemplate`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.reasoningEngines.sandboxEnvironmentTemplates#SandboxEnvironmentTemplate) s in a given reasoning engine.

### Endpoint

get `https: / /{service-endpoint} /v1 /{parent} /sandboxEnvironmentTemplates`  

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

Response message for [`SandboxEnvironmentService.ListSandboxEnvironmentTemplates`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.reasoningEngines.sandboxEnvironmentTemplates/list#google.cloud.aiplatform.v1.SandboxEnvironmentService.ListSandboxEnvironmentTemplates) .

If successful, the response body contains data with the following structure:

Fields

`sandboxEnvironmentTemplates[]` `object ( `[`SandboxEnvironmentTemplate`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.reasoningEngines.sandboxEnvironmentTemplates#SandboxEnvironmentTemplate)` )`

The SandboxEnvironmentTemplates matching the request.

`nextPageToken` `string`

A token, which can be sent as [`ListSandboxEnvironmentTemplatesRequest.page_token`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.reasoningEngines.sandboxEnvironmentTemplates/list#body.QUERY_PARAMETERS.page_token) to retrieve the next page. Absence of this field indicates there are no subsequent pages.

**JSON representation**

```
{
  "sandboxEnvironmentTemplates": [
    {
      object (SandboxEnvironmentTemplate)
    }
  ],
  "nextPageToken": string
}
```
