---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.hyperparameterTuningJobs/cancel
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.hyperparameterTuningJobs/cancel
title: 'Method: hyperparameterTuningJobs.cancel'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.hyperparameterTuningJobs.cancel

Cancels a HyperparameterTuningJob. Starts asynchronous cancellation on the HyperparameterTuningJob. The server makes a best effort to cancel the job, but success is not guaranteed. Clients can use `  JobService.GetHyperparameterTuningJob  ` or other methods to check whether the cancellation succeeded or whether the job completed despite cancellation. On successful cancellation, the HyperparameterTuningJob is not deleted; instead it becomes a job with a `  HyperparameterTuningJob.error  ` value with a `  google.rpc.Status.code  ` of 1, corresponding to `code.CANCELLED` , and `  HyperparameterTuningJob.state  ` is set to `CANCELLED` .

### Endpoint

post `https: / /{service-endpoint} /v1 /{name}:cancel`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`name` `string`

Required. The name of the HyperparameterTuningJob to cancel. Format: `projects/{project}/locations/{location}/hyperparameterTuningJobs/{hyperparameterTuningJob}`

### Request body

The request body must be empty.

### Response body

If successful, the response body is an empty JSON object.
