---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.schedules/pause
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.schedules/pause
title: 'Method: schedules.pause'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

**Full name** : projects.locations.schedules.pause

Pauses a Schedule. Will mark `  Schedule.state  ` to 'PAUSED'. If the schedule is paused, no new runs will be created. Already created runs will NOT be paused or canceled.

### Endpoint

post `https: / /{service-endpoint} /v1beta1 /{name}:pause`  

Where `{service-endpoint}` is one of the [supported service endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest#rest_endpoints) .

### Path parameters

`name` `string`

Required. The name of the Schedule resource to be paused. Format: `projects/{project}/locations/{location}/schedules/{schedule}`

### Request body

The request body must be empty.

### Response body

If successful, the response body is an empty JSON object.
