---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.nasJobs/list
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.nasJobs/list
title: 'Method: nasJobs.list'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.nasJobs.list

Lists NasJobs in a Location.

### Endpoint

get `https: / /{service-endpoint} /v1 /{parent} /nasJobs`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`parent` `string`

Required. The resource name of the Location to list the NasJobs from. Format: `projects/{project}/locations/{location}`

### Query parameters

`filter` `string`

The standard list filter.

Supported fields:

- `displayName` supports `=` , `!=` comparisons, and `:` wildcard.
- `state` supports `=` , `!=` comparisons.
- `createTime` supports `=` , `!=` , `<` , `<=` , `>` , `>=` comparisons. `createTime` must be in RFC 3339 format.
- `labels` supports general map functions that is: `labels.key=value` - key:value equality \`labels.key:\* - key existence

Some examples of using the filter are:

- `state="JOB_STATE_SUCCEEDED" AND displayName:"my_job_*"`
- `state!="JOB_STATE_FAILED" OR displayName="my_job"`
- `NOT displayName="my_job"`
- `createTime>"2021-05-18T00:00:00Z"`
- `labels.keyA=valueA`
- `labels.keyB:*`

`pageSize` `integer`

The standard list page size.

`pageToken` `string`

The standard list page token. Typically obtained via [`ListNasJobsResponse.next_page_token`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.nasJobs/list#body.ListNasJobsResponse.FIELDS.next_page_token) of the previous [`JobService.ListNasJobs`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.nasJobs/list#google.cloud.aiplatform.v1.JobService.ListNasJobs) call.

`readMask` `string ( `[`FieldMask`](https://protobuf.dev/reference/protobuf/google.protobuf/#field-mask)` format)`

Mask specifying which fields to read.

This is a comma-separated list of fully qualified names of fields. Example: `"user.displayName,photo"` .

### Request body

The request body must be empty.

### Response body

Response message for [`JobService.ListNasJobs`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.nasJobs/list#google.cloud.aiplatform.v1.JobService.ListNasJobs)

If successful, the response body contains data with the following structure:

Fields

`nasJobs[]` `object ( `[`NasJob`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.nasJobs#NasJob)` )`

List of NasJobs in the requested page. [`NasJob.nas_job_output`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.nasJobs#NasJob.FIELDS.nas_job_output) of the jobs will not be returned.

`nextPageToken` `string`

A token to retrieve the next page of results. Pass to [`ListNasJobsRequest.page_token`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.nasJobs/list#body.QUERY_PARAMETERS.page_token) to obtain that page.

**JSON representation**

```
{
  "nasJobs": [
    {
      object (NasJob)
    }
  ],
  "nextPageToken": string
}
```
