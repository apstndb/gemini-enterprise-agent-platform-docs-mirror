---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v1/projects.locations.schedules/get
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v1/projects.locations.schedules/get
title: 'Method: projects.locations.schedules.get'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Gets details of schedule

### HTTP request

`GET https://notebooks.googleapis.com/v1/{name}`

### Path parameters

Parameters

`name`

`string`

Required. Format: `projects/{projectId}/locations/{location}/schedules/{scheduleId}`

Authorization requires the following [IAM](https://cloud.google.com/iam/docs/) permission on the specified resource `name` :

  - `notebooks.schedules.get`

### Request body

The request body must be empty.

### Response body

If successful, the response body contains an instance of `  Schedule  ` .

### Authorization scopes

Requires the following OAuth scope:

  - `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .
