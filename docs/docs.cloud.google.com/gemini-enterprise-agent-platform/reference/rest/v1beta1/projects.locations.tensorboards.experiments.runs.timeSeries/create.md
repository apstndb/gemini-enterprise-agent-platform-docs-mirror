---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.tensorboards.experiments.runs.timeSeries/create
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.tensorboards.experiments.runs.timeSeries/create
title: 'Method: timeSeries.create'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.tensorboards.experiments.runs.timeSeries.create

Creates a TensorboardTimeSeries.

### Endpoint

post `https: / /{service-endpoint} /v1beta1 /{parent} /timeSeries`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`parent` `string`

Required. The resource name of the TensorboardRun to create the TensorboardTimeSeries in. Format: `projects/{project}/locations/{location}/tensorboards/{tensorboard}/experiments/{experiment}/runs/{run}`

### Query parameters

`tensorboardTimeSeriesId` `string`

Optional. The user specified unique id to use for the TensorboardTimeSeries, which becomes the final component of the TensorboardTimeSeries's resource name. This value should match "\[a-z0-9\]\[a-z0-9-\]{0, 127}"

### Request body

The request body contains an instance of `  TensorboardTimeSeries  ` .

### Response body

If successful, the response body contains a newly created instance of `  TensorboardTimeSeries  ` .
