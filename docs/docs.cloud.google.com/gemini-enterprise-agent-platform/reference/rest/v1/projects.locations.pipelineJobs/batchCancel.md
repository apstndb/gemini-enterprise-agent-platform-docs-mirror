---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.pipelineJobs/batchCancel
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.pipelineJobs/batchCancel
title: 'Method: pipelineJobs.batchCancel'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.pipelineJobs.batchCancel

Batch cancel PipelineJobs. Firstly the server will check if all the jobs are in non-terminal states, and skip the jobs that are already terminated. If the operation failed, none of the pipeline jobs are cancelled. The server will poll the states of all the pipeline jobs periodically to check the cancellation status. This operation will return an LRO.

### Endpoint

post `https: / /{service-endpoint} /v1 /{parent} /pipelineJobs:batchCancel`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`parent` `string`

Required. The name of the PipelineJobs' parent resource. Format: `projects/{project}/locations/{location}`

### Request body

The request body contains data with the following structure:

Fields

`names[]` `string`

Required. The names of the PipelineJobs to cancel. A maximum of 32 PipelineJobs can be cancelled in a batch. Format: `projects/{project}/locations/{location}/pipelineJobs/{pipelineJob}`

### Response body

If successful, the response body contains an instance of `  Operation  ` .
