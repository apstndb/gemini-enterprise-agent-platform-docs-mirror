---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.tensorboards.experiments.runs/write
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.tensorboards.experiments.runs/write
title: 'Method: runs.write'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.tensorboards.experiments.runs.write

Write time series data points into multiple TensorboardTimeSeries under a TensorboardRun. If any data fail to be ingested, an error is returned.

### Endpoint

post `https: / /{service-endpoint} /v1 /{tensorboardRun}:write`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`tensorboardRun` `string`

Required. The resource name of the TensorboardRun to write data to. Format: `projects/{project}/locations/{location}/tensorboards/{tensorboard}/experiments/{experiment}/runs/{run}`

### Request body

The request body contains data with the following structure:

Fields

`timeSeriesData[]` ` object ( TimeSeriesData  ` )

Required. The TensorboardTimeSeries data to write. Values with in a time series are indexed by their step value. Repeated writes to the same step will overwrite the existing value for that step. The upper limit of data points per write request is 5000.

### Response body

If successful, the response body is empty.
