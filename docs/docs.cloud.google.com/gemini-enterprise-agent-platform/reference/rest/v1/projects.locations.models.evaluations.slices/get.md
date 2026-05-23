---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.models.evaluations.slices/get
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.models.evaluations.slices/get
title: 'Method: slices.get'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.models.evaluations.slices.get

Gets a ModelEvaluationSlice.

### Endpoint

get `https: / /{service-endpoint} /v1 /{name}`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`name` `string`

Required. The name of the ModelEvaluationSlice resource. Format: `projects/{project}/locations/{location}/models/{model}/evaluations/{evaluation}/slices/{slice}`

### Request body

The request body must be empty.

### Response body

If successful, the response body contains an instance of `  ModelEvaluationSlice  ` .
