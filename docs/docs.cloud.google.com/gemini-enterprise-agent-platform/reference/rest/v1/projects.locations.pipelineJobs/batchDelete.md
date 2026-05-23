---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.pipelineJobs/batchDelete
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.pipelineJobs/batchDelete
title: 'Method: pipelineJobs.batchDelete'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.pipelineJobs.batchDelete

Batch deletes PipelineJobs The Operation is atomic. If it fails, none of the PipelineJobs are deleted. If it succeeds, all of the PipelineJobs are deleted.

### Endpoint

post `https: / /{service-endpoint} /v1 /{parent} /pipelineJobs:batchDelete`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`parent` `string`

Required. The name of the PipelineJobs' parent resource. Format: `projects/{project}/locations/{location}`

### Request body

The request body contains data with the following structure:

Fields

`names[]` `string`

Required. The names of the PipelineJobs to delete. A maximum of 32 PipelineJobs can be deleted in a batch. Format: `projects/{project}/locations/{location}/pipelineJobs/{pipelineJob}`

### Response body

If successful, the response body contains an instance of `  Operation  ` .
