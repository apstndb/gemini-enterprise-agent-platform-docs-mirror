---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.modelDeploymentMonitoringJobs/resume
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.modelDeploymentMonitoringJobs/resume
title: 'Method: modelDeploymentMonitoringJobs.resume'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.modelDeploymentMonitoringJobs.resume

Resumes a paused ModelDeploymentMonitoringJob. It will start to run from next scheduled time. A deleted ModelDeploymentMonitoringJob can't be resumed.

### Endpoint

post `https: / /{service-endpoint} /v1 /{name}:resume`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`name` `string`

Required. The resource name of the ModelDeploymentMonitoringJob to resume. Format: `projects/{project}/locations/{location}/modelDeploymentMonitoringJobs/{modelDeploymentMonitoringJob}`

### Request body

The request body must be empty.

### Response body

If successful, the response body is an empty JSON object.
