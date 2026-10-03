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

Response message for [`ReasoningEngineRuntimeRevisionService.ListReasoningEngineRuntimeRevisions`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.reasoningEngines.runtimeRevisions/list#google.cloud.aiplatform.v1beta1.ReasoningEngineRuntimeRevisionService.ListReasoningEngineRuntimeRevisions)

If successful, the response body contains data with the following structure:

Fields

`reasoningEngineRuntimeRevisions[]` `object ( `[`ReasoningEngineRuntimeRevision`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.reasoningEngines.runtimeRevisions#ReasoningEngineRuntimeRevision)` )`

List of ReasoningEngineRuntimeRevisions in the requested page.

`nextPageToken` `string`

A token to retrieve the next page of results. Pass to [`ListReasoningEngineRuntimeRevisionsRequest.page_token`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.reasoningEngines.runtimeRevisions/list#body.QUERY_PARAMETERS.page_token) to obtain that page.

**JSON representation**

```
{
  "reasoningEngineRuntimeRevisions": [
    {
      object (ReasoningEngineRuntimeRevision)
    }
  ],
  "nextPageToken": string
}
```
