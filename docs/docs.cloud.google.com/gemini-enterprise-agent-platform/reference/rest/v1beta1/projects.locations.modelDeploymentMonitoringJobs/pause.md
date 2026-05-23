---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.modelDeploymentMonitoringJobs/pause
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.modelDeploymentMonitoringJobs/pause
title: 'Method: modelDeploymentMonitoringJobs.pause'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.modelDeploymentMonitoringJobs.pause

Pauses a ModelDeploymentMonitoringJob. If the job is running, the server makes a best effort to cancel the job. Will mark `  ModelDeploymentMonitoringJob.state  ` to 'PAUSED'.

### Endpoint

post `https: / /{service-endpoint} /v1beta1 /{name}:pause`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`name` `string`

Required. The resource name of the ModelDeploymentMonitoringJob to pause. Format: `projects/{project}/locations/{location}/modelDeploymentMonitoringJobs/{modelDeploymentMonitoringJob}`

### Request body

The request body must be empty.

### Response body

If successful, the response body is an empty JSON object.
