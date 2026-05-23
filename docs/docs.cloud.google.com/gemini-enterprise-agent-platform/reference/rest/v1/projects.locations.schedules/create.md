---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.schedules/create
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.schedules/create
title: 'Method: schedules.create'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.schedules.create

Creates a Schedule.

### Endpoint

post `https: / /{service-endpoint} /v1 /{parent} /schedules`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`parent` `string`

Required. The resource name of the Location to create the Schedule in. Format: `projects/{project}/locations/{location}`

### Request body

The request body contains an instance of `  Schedule  ` .

### Response body

If successful, the response body contains a newly created instance of `  Schedule  ` .
