---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.modelMonitors/list
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.modelMonitors/list
title: 'Method: modelMonitors.list'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.modelMonitors.list

Lists ModelMonitors in a Location.

### Endpoint

get `https: / /{service-endpoint} /v1beta1 /{parent} /modelMonitors`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`parent` `string`

Required. The resource name of the Location to list the ModelMonitors from. Format: `projects/{project}/locations/{location}`

### Query parameters

`filter` `string`

The standard list filter. More detail in [AIP-160](https://google.aip.dev/160) .

`pageSize` `integer`

The standard list page size.

`pageToken` `string`

The standard list page token.

`readMask` `string ( `[`FieldMask`](https://protobuf.dev/reference/protobuf/google.protobuf/#field-mask)` format)`

Mask specifying which fields to read.

This is a comma-separated list of fully qualified names of fields. Example: `"user.displayName,photo"` .

### Request body

The request body must be empty.

### Response body

Response message for [`ModelMonitoringService.ListModelMonitors`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.modelMonitors/list#google.cloud.aiplatform.v1beta1.ModelMonitoringService.ListModelMonitors)

If successful, the response body contains data with the following structure:

Fields

`modelMonitors[]` `object ( `[`ModelMonitor`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.modelMonitors#ModelMonitor)` )`

List of ModelMonitor in the requested page.

`nextPageToken` `string`

A token to retrieve the next page of results. Pass to [`ListModelMonitorsRequest.page_token`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.modelMonitors/list#body.QUERY_PARAMETERS.page_token) to obtain that page.

**JSON representation**

```
{
  "modelMonitors": [
    {
      object (ModelMonitor)
    }
  ],
  "nextPageToken": string
}
```
