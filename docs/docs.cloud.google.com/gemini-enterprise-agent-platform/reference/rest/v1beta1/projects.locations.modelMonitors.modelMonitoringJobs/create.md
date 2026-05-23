---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.modelMonitors.modelMonitoringJobs/create
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.modelMonitors.modelMonitoringJobs/create
title: 'Method: modelMonitoringJobs.create'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.modelMonitors.modelMonitoringJobs.create

Creates a ModelMonitoringJob.

### Endpoint

post `https: / /{service-endpoint} /v1beta1 /{parent} /modelMonitoringJobs`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`parent` `string`

Required. The parent of the ModelMonitoringJob. Format: `projects/{project}/locations/{location}/modelMoniitors/{modelMonitor}`

### Query parameters

`modelMonitoringJobId` `string`

Optional. The id to use for the Model Monitoring Job, which will become the final component of the model monitoring job resource name.

The maximum length is 63 characters, and valid characters are `/^[a-z]([a-z0-9-]{0,61}[a-z0-9])?$/` .

### Request body

The request body contains an instance of `  ModelMonitoringJob  ` .

### Response body

If successful, the response body contains a newly created instance of `  ModelMonitoringJob  ` .
