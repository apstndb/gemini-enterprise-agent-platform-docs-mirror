---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.reasoningEngines/list
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.reasoningEngines/list
title: 'Method: reasoningEngines.list'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.reasoningEngines.list

Lists reasoning engines in a location.

### Endpoint

get `https: / /{service-endpoint} /v1beta1 /{parent} /reasoningEngines`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`parent` `string`

Required. The resource name of the Location to list the ReasoningEngines from. Format: `projects/{project}/locations/{location}`

### Query parameters

`filter` `string`

Optional. The standard list filter. More detail in [AIP-160](https://google.aip.dev/160) .

`pageSize` `integer`

Optional. The standard list page size.

`pageToken` `string`

Optional. The standard list page token.

### Request body

The request body must be empty.

### Response body

Response message for [`ReasoningEngineService.ListReasoningEngines`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.reasoningEngines/list#google.cloud.aiplatform.v1beta1.ReasoningEngineService.ListReasoningEngines)

If successful, the response body contains data with the following structure:

Fields

`reasoningEngines[]` `object ( `[`ReasoningEngine`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.reasoningEngines#ReasoningEngine)` )`

List of ReasoningEngines in the requested page.

`nextPageToken` `string`

A token to retrieve the next page of results. Pass to [`ListReasoningEnginesRequest.page_token`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.reasoningEngines/list#body.QUERY_PARAMETERS.page_token) to obtain that page.

**JSON representation**

```
{
  "reasoningEngines": [
    {
      object (ReasoningEngine)
    }
  ],
  "nextPageToken": string
}
```
