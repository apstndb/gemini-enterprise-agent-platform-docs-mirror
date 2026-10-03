---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.tensorboards.experiments.runs/batchCreate
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.tensorboards.experiments.runs/batchCreate
title: 'Method: runs.batchCreate'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.tensorboards.experiments.runs.batchCreate

Batch create TensorboardRuns.

### Endpoint

post `https: / /{service-endpoint} /v1 /{parent} /runs:batchCreate`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`parent` `string`

Required. The resource name of the TensorboardExperiment to create the TensorboardRuns in. Format: `projects/{project}/locations/{location}/tensorboards/{tensorboard}/experiments/{experiment}` The parent field in the CreateTensorboardRunRequest messages must match this field.

### Request body

The request body contains data with the following structure:

Fields

`requests[]` `object ( `[`CreateTensorboardRunRequest`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.tensorboards.experiments.runs/batchCreate#CreateTensorboardRunRequest)` )`

Required. The request message specifying the TensorboardRuns to create. A maximum of 1000 TensorboardRuns can be created in a batch.

### Response body

Response message for [`TensorboardService.BatchCreateTensorboardRuns`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.tensorboards.experiments.runs/batchCreate#google.cloud.aiplatform.v1.TensorboardService.BatchCreateTensorboardRuns) .

If successful, the response body contains data with the following structure:

Fields

`tensorboardRuns[]` `object ( `[`TensorboardRun`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.tensorboards.experiments.runs#TensorboardRun)` )`

The created TensorboardRuns.

**JSON representation**

```
{
  "tensorboardRuns": [
    {
      object (TensorboardRun)
    }
  ]
}
```

## CreateTensorboardRunRequest

Request message for [`TensorboardService.CreateTensorboardRun`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.tensorboards.experiments.runs/create#google.cloud.aiplatform.v1.TensorboardService.CreateTensorboardRun) .

Fields

`parent` `string`

Required. The resource name of the TensorboardExperiment to create the TensorboardRun in. Format: `projects/{project}/locations/{location}/tensorboards/{tensorboard}/experiments/{experiment}`

`tensorboardRun` `object ( `[`TensorboardRun`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.tensorboards.experiments.runs#TensorboardRun)` )`

Required. The TensorboardRun to create.

`tensorboardRunId` `string`

Required. The id to use for the Tensorboard run, which becomes the final component of the Tensorboard run's resource name.

This value should be 1-128 characters, and valid characters are `/[a-z][0-9]-/` .

**JSON representation**

```
{
  "parent": string,
  "tensorboardRun": {
    object (TensorboardRun)
  },
  "tensorboardRunId": string
}
```
