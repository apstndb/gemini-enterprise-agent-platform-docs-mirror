---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.batchPredictionJobs/cancel
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.batchPredictionJobs/cancel
title: 'Method: batchPredictionJobs.cancel'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.batchPredictionJobs.cancel

Cancels a BatchPredictionJob.

Starts asynchronous cancellation on the BatchPredictionJob. The server makes the best effort to cancel the job, but success is not guaranteed. Clients can use `  JobService.GetBatchPredictionJob  ` or other methods to check whether the cancellation succeeded or whether the job completed despite cancellation. On a successful cancellation, the BatchPredictionJob is not deleted;instead its `  BatchPredictionJob.state  ` is set to `CANCELLED` . Any files already outputted by the job are not deleted.

### Endpoint

post `https: / /{service-endpoint} /v1beta1 /{name}:cancel`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`name` `string`

Required. The name of the BatchPredictionJob to cancel. Format: `projects/{project}/locations/{location}/batchPredictionJobs/{batchPredictionJob}`

### Request body

The request body must be empty.

### Response body

If successful, the response body is an empty JSON object.
