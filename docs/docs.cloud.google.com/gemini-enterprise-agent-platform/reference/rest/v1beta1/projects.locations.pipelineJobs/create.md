---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.pipelineJobs/create
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.pipelineJobs/create
title: 'Method: pipelineJobs.create'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.pipelineJobs.create

Creates a PipelineJob. A PipelineJob will run immediately when created.

### Endpoint

post `https: / /{service-endpoint} /v1beta1 /{parent} /pipelineJobs`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`parent` `string`

Required. The resource name of the Location to create the PipelineJob in. Format: `projects/{project}/locations/{location}`

### Query parameters

`pipelineJobId` `string`

The id to use for the PipelineJob, which will become the final component of the PipelineJob name. If not provided, an id will be automatically generated.

This value should be less than 128 characters, and valid characters are `/[a-z][0-9]-/` .

### Request body

The request body contains an instance of `  PipelineJob  ` .

### Response body

If successful, the response body contains a newly created instance of `  PipelineJob  ` .
