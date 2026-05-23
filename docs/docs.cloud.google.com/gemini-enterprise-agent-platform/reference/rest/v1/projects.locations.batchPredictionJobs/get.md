---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.batchPredictionJobs/get
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.batchPredictionJobs/get
title: 'Method: batchPredictionJobs.get'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.batchPredictionJobs.get

Gets a BatchPredictionJob

### Endpoint

get `https: / /{service-endpoint} /v1 /{name}`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`name` `string`

Required. The name of the BatchPredictionJob resource. Format: `projects/{project}/locations/{location}/batchPredictionJobs/{batchPredictionJob}`

### Request body

The request body must be empty.

### Response body

If successful, the response body contains an instance of `  BatchPredictionJob  ` .
