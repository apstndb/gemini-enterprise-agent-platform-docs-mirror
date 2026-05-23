---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.hyperparameterTuningJobs/delete
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.hyperparameterTuningJobs/delete
title: 'Method: hyperparameterTuningJobs.delete'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.hyperparameterTuningJobs.delete

Deletes a HyperparameterTuningJob.

### Endpoint

delete `https: / /{service-endpoint} /v1 /{name}`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`name` `string`

Required. The name of the HyperparameterTuningJob resource to be deleted. Format: `projects/{project}/locations/{location}/hyperparameterTuningJobs/{hyperparameterTuningJob}`

### Request body

The request body must be empty.

### Response body

If successful, the response body contains an instance of `  Operation  ` .
