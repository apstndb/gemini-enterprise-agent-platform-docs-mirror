---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v1/projects.locations.schedules/create
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v1/projects.locations.schedules/create
title: 'Method: projects.locations.schedules.create'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Creates a new Scheduled Notebook in a given project and location.

### HTTP request

`POST https://notebooks.googleapis.com/v1/{parent}/schedules`

### Path parameters

Parameters

`parent`

`string`

Required. Format: `parent=projects/{projectId}/locations/{location}`

Authorization requires the following [IAM](https://cloud.google.com/iam/docs/) permission on the specified resource `parent` :

  - `notebooks.schedules.create`

### Query parameters

Parameters

`scheduleId`

`string`

Required. User-defined unique ID of this schedule.

### Request body

The request body contains an instance of `  Schedule  ` .

### Response body

If successful, the response body contains a newly created instance of `  Operation  ` .

### Authorization scopes

Requires the following OAuth scope:

  - `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .
