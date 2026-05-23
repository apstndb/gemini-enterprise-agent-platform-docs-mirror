---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.tensorboards.experiments.runs/create
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.tensorboards.experiments.runs/create
title: 'Method: runs.create'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.tensorboards.experiments.runs.create

Creates a TensorboardRun.

### Endpoint

post `https: / /{service-endpoint} /v1beta1 /{parent} /runs`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`parent` `string`

Required. The resource name of the TensorboardExperiment to create the TensorboardRun in. Format: `projects/{project}/locations/{location}/tensorboards/{tensorboard}/experiments/{experiment}`

### Query parameters

`tensorboardRunId` `string`

Required. The id to use for the Tensorboard run, which becomes the final component of the Tensorboard run's resource name.

This value should be 1-128 characters, and valid characters are `/[a-z][0-9]-/` .

### Request body

The request body contains an instance of `  TensorboardRun  ` .

### Response body

If successful, the response body contains a newly created instance of `  TensorboardRun  ` .
