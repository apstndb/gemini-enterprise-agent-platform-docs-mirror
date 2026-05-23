---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.tensorboards.experiments/create
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.tensorboards.experiments/create
title: 'Method: experiments.create'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.tensorboards.experiments.create

Creates a TensorboardExperiment.

### Endpoint

post `https: / /{service-endpoint} /v1 /{parent} /experiments`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`parent` `string`

Required. The resource name of the Tensorboard to create the TensorboardExperiment in. Format: `projects/{project}/locations/{location}/tensorboards/{tensorboard}`

### Query parameters

`tensorboardExperimentId` `string`

Required. The id to use for the Tensorboard experiment, which becomes the final component of the Tensorboard experiment's resource name.

This value should be 1-128 characters, and valid characters are `/[a-z][0-9]-/` .

### Request body

The request body contains an instance of `  TensorboardExperiment  ` .

### Response body

If successful, the response body contains a newly created instance of `  TensorboardExperiment  ` .
