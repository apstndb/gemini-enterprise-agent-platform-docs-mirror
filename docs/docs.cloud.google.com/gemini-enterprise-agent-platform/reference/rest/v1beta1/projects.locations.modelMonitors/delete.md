---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.modelMonitors/delete
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.modelMonitors/delete
title: 'Method: modelMonitors.delete'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.modelMonitors.delete

Deletes a ModelMonitor.

### Endpoint

delete `https: / /{service-endpoint} /v1beta1 /{name}`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`name` `string`

Required. The name of the ModelMonitor resource to be deleted. Format: `projects/{project}/locations/{location}/modelMonitords/{modelMonitor}`

### Query parameters

`force` `boolean`

Optional. Force delete the model monitor with schedules.

### Request body

The request body must be empty.

### Response body

If successful, the response body contains an instance of `  Operation  ` .
