---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.featureGroups.featureMonitors.featureMonitorJobs/list
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.featureGroups.featureMonitors.featureMonitorJobs/list
title: 'Method: featureMonitorJobs.list'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.featureGroups.featureMonitors.featureMonitorJobs.list

List feature monitor jobs.

### Endpoint

get `https: / /{service-endpoint} /v1beta1 /{parent} /featureMonitorJobs`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`parent` `string`

Required. The resource name of the FeatureMonitor to list FeatureMonitorJobs. Format: `projects/{project}/locations/{location}/featureGroups/{featureGroup}/featureMonitors/{featureMonitor}`

### Query parameters

`filter` `string`

Optional. Lists the FeatureMonitorJobs that match the filter expression. The following fields are supported:

- `createTime` : Supports `=` , `!=` , `<` , `>` , `<=` , and `>=` comparisons. Values must be

Examples:

- `createTime > "2020-01-01"` FeatureMonitorJobs created after 2020-01-01.

`pageSize` `integer`

Optional. The maximum number of FeatureMonitorJobs to return. The service may return fewer than this value. If unspecified, at most 100 FeatureMonitorJobs will be returned. The maximum value is 100; any value greater than 100 will be coerced to 100.

`pageToken` `string`

Optional. A page token, received from a previous [`FeatureRegistryService.ListFeatureMonitorJobs`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.featureGroups.featureMonitors.featureMonitorJobs/list#google.cloud.aiplatform.v1beta1.FeatureRegistryService.ListFeatureMonitorJobs) call. Provide this to retrieve the subsequent page.

When paginating, all other parameters provided to [`FeatureRegistryService.ListFeatureMonitorJobs`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.featureGroups.featureMonitors.featureMonitorJobs/list#google.cloud.aiplatform.v1beta1.FeatureRegistryService.ListFeatureMonitorJobs) must match the call that provided the page token.

`orderBy` `string`

Optional. A comma-separated list of fields to order by, sorted in ascending order. Use "desc" after a field name for descending. Supported Fields:

- `createTime`

### Request body

The request body must be empty.

### Response body

Response message for [`FeatureRegistryService.ListFeatureMonitorJobs`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.featureGroups.featureMonitors.featureMonitorJobs/list#google.cloud.aiplatform.v1beta1.FeatureRegistryService.ListFeatureMonitorJobs) .

If successful, the response body contains data with the following structure:

Fields

`featureMonitorJobs[]` `object ( `[`FeatureMonitorJob`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.featureGroups.featureMonitors.featureMonitorJobs#FeatureMonitorJob)` )`

The FeatureMonitorJobs matching the request.

`nextPageToken` `string`

A token, which can be sent as [`ListFeatureMonitorJobsRequest.page_token`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.featureGroups.featureMonitors.featureMonitorJobs/list#body.QUERY_PARAMETERS.page_token) to retrieve the next page. If this field is omitted, there are no subsequent pages.

**JSON representation**

```
{
  "featureMonitorJobs": [
    {
      object (FeatureMonitorJob)
    }
  ],
  "nextPageToken": string
}
```
