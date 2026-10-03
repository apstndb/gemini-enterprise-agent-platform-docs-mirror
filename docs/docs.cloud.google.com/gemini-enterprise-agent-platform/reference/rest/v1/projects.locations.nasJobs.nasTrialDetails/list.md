---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.nasJobs.nasTrialDetails/list
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.nasJobs.nasTrialDetails/list
title: 'Method: nasTrialDetails.list'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.nasJobs.nasTrialDetails.list

List top NasTrialDetails of a NasJob.

### Endpoint

get `https: / /{service-endpoint} /v1 /{parent} /nasTrialDetails`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`parent` `string`

Required. The name of the NasJob resource. Format: `projects/{project}/locations/{location}/nasJobs/{nasJob}`

### Query parameters

`pageSize` `integer`

The standard list page size.

`pageToken` `string`

The standard list page token. Typically obtained via [`ListNasTrialDetailsResponse.next_page_token`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.nasJobs.nasTrialDetails/list#body.ListNasTrialDetailsResponse.FIELDS.next_page_token) of the previous [`JobService.ListNasTrialDetails`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.nasJobs.nasTrialDetails/list#google.cloud.aiplatform.v1.JobService.ListNasTrialDetails) call.

### Request body

The request body must be empty.

### Response body

Response message for [`JobService.ListNasTrialDetails`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.nasJobs.nasTrialDetails/list#google.cloud.aiplatform.v1.JobService.ListNasTrialDetails)

If successful, the response body contains data with the following structure:

Fields

`nasTrialDetails[]` `object ( `[`NasTrialDetail`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.nasJobs.nasTrialDetails#NasTrialDetail)` )`

List of top NasTrials in the requested page.

`nextPageToken` `string`

A token to retrieve the next page of results. Pass to [`ListNasTrialDetailsRequest.page_token`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.nasJobs.nasTrialDetails/list#body.QUERY_PARAMETERS.page_token) to obtain that page.

**JSON representation**

```
{
  "nasTrialDetails": [
    {
      object (NasTrialDetail)
    }
  ],
  "nextPageToken": string
}
```
