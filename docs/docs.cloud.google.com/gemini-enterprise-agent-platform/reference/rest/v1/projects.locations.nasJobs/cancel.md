---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.nasJobs/cancel
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.nasJobs/cancel
title: 'Method: nasJobs.cancel'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.nasJobs.cancel

Cancels a NasJob. Starts asynchronous cancellation on the NasJob. The server makes a best effort to cancel the job, but success is not guaranteed. Clients can use `  JobService.GetNasJob  ` or other methods to check whether the cancellation succeeded or whether the job completed despite cancellation. On successful cancellation, the NasJob is not deleted; instead it becomes a job with a `  NasJob.error  ` value with a `  google.rpc.Status.code  ` of 1, corresponding to `code.CANCELLED` , and `  NasJob.state  ` is set to `CANCELLED` .

### Endpoint

post `https: / /{service-endpoint} /v1 /{name}:cancel`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`name` `string`

Required. The name of the NasJob to cancel. Format: `projects/{project}/locations/{location}/nasJobs/{nasJob}`

### Request body

The request body must be empty.

### Response body

If successful, the response body is an empty JSON object.
