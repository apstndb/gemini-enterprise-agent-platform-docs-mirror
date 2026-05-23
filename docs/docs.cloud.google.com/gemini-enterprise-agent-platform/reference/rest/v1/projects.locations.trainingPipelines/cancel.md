---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.trainingPipelines/cancel
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.trainingPipelines/cancel
title: 'Method: trainingPipelines.cancel'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.trainingPipelines.cancel

Cancels a TrainingPipeline. Starts asynchronous cancellation on the TrainingPipeline. The server makes a best effort to cancel the pipeline, but success is not guaranteed. Clients can use `  PipelineService.GetTrainingPipeline  ` or other methods to check whether the cancellation succeeded or whether the pipeline completed despite cancellation. On successful cancellation, the TrainingPipeline is not deleted; instead it becomes a pipeline with a `  TrainingPipeline.error  ` value with a `  google.rpc.Status.code  ` of 1, corresponding to `code.CANCELLED` , and `  TrainingPipeline.state  ` is set to `CANCELLED` .

### Endpoint

post `https: / /{service-endpoint} /v1 /{name}:cancel`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`name` `string`

Required. The name of the TrainingPipeline to cancel. Format: `projects/{project}/locations/{location}/trainingPipelines/{trainingPipeline}`

### Request body

The request body must be empty.

### Response body

If successful, the response body is an empty JSON object.
