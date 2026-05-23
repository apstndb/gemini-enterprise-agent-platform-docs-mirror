---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.modelDeploymentMonitoringJobs/create
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.modelDeploymentMonitoringJobs/create
title: 'Method: modelDeploymentMonitoringJobs.create'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.modelDeploymentMonitoringJobs.create

Creates a ModelDeploymentMonitoringJob. It will run periodically on a configured interval.

### Endpoint

post `https: / /{service-endpoint} /v1beta1 /{parent} /modelDeploymentMonitoringJobs`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`parent` `string`

Required. The parent of the ModelDeploymentMonitoringJob. Format: `projects/{project}/locations/{location}`

### Request body

The request body contains an instance of `  ModelDeploymentMonitoringJob  ` .

### Response body

If successful, the response body contains a newly created instance of `  ModelDeploymentMonitoringJob  ` .
