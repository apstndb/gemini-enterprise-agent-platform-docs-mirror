---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.modelDeploymentMonitoringJobs/delete
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.modelDeploymentMonitoringJobs/delete
title: 'Method: modelDeploymentMonitoringJobs.delete'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.modelDeploymentMonitoringJobs.delete

Deletes a ModelDeploymentMonitoringJob.

### Endpoint

delete `https: / /{service-endpoint} /v1 /{name}`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`name` `string`

Required. The resource name of the model monitoring job to delete. Format: `projects/{project}/locations/{location}/modelDeploymentMonitoringJobs/{modelDeploymentMonitoringJob}`

### Request body

The request body must be empty.

### Response body

If successful, the response body contains an instance of `  Operation  ` .
