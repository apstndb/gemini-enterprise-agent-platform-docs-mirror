---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.studies/list
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.studies/list
title: 'Method: studies.list'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.studies.list

Lists all the studies in a region for an associated project.

### Endpoint

get `https: / /{service-endpoint} /v1 /{parent} /studies`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`parent` `string`

Required. The resource name of the Location to list the Study from. Format: `projects/{project}/locations/{location}`

### Query parameters

`pageToken` `string`

Optional. A page token to request the next page of results. If unspecified, there are no subsequent pages.

`pageSize` `integer`

Optional. The maximum number of studies to return per "page" of results. If unspecified, service will pick an appropriate default.

### Request body

The request body must be empty.

### Response body

Response message for [`VizierService.ListStudies`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.studies/list#google.cloud.aiplatform.v1.VizierService.ListStudies) .

If successful, the response body contains data with the following structure:

Fields

`studies[]` `object ( `[`Study`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.studies#Study)` )`

The studies associated with the project.

`nextPageToken` `string`

Passes this token as the `pageToken` field of the request for a subsequent call. If this field is omitted, there are no subsequent pages.

**JSON representation**

```
{
  "studies": [
    {
      object (Study)
    }
  ],
  "nextPageToken": string
}
```
