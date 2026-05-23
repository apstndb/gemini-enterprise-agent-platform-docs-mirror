---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.tuningJobs/cancel
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.tuningJobs/cancel
title: 'Method: tuningJobs.cancel'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.tuningJobs.cancel

Cancels a tuning job.

Starts an asynchronous cancellation request. The server makes a best effort to cancel the job, but success is not guaranteed. Clients can use `  GenAiTuningService.GetTuningJob  ` or other methods to check whether the cancellation succeeded or whether the job completed despite cancellation. On successful cancellation, the tuning job is not deleted. Instead, its state is set to `CANCELLED` , and `error` is set to a status with a `google.rpc.Status.code` of 1, corresponding to `code.CANCELLED` .

### Endpoint

post `https: / /{service-endpoint} /v1beta1 /{name}:cancel`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`name` `string`

Required. The name of the tuning job to cancel. Format: `projects/{project}/locations/{location}/tuningJobs/{tuningJob}`

### Request body

The request body must be empty.

### Response body

If successful, the response body is an empty JSON object.
