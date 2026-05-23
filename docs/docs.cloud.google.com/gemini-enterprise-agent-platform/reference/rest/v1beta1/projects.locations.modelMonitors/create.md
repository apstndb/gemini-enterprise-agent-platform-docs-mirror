---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.modelMonitors/create
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.modelMonitors/create
title: 'Method: modelMonitors.create'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.modelMonitors.create

Creates a ModelMonitor.

### Endpoint

post `https: / /{service-endpoint} /v1beta1 /{parent} /modelMonitors`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`parent` `string`

Required. The resource name of the Location to create the ModelMonitor in. Format: `projects/{project}/locations/{location}`

### Query parameters

`modelMonitorId` `string`

Optional. The id to use for the Model Monitor, which will become the final component of the model monitor resource name.

The maximum length is 63 characters, and valid characters are `/^[a-z]([a-z0-9-]{0,61}[a-z0-9])?$/` .

### Request body

The request body contains an instance of `  ModelMonitor  ` .

### Response body

If successful, the response body contains a newly created instance of `  Operation  ` .
