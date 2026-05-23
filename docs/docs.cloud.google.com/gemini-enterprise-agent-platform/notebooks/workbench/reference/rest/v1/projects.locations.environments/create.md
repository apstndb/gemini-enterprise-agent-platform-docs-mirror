---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v1/projects.locations.environments/create
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v1/projects.locations.environments/create
title: 'Method: projects.locations.environments.create'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Creates a new Environment.

### HTTP request

`POST https://notebooks.googleapis.com/v1/{parent}/environments`

### Path parameters

Parameters

`parent`

`string`

Required. Format: `projects/{projectId}/locations/{location}`

Authorization requires the following [IAM](https://cloud.google.com/iam/docs/) permission on the specified resource `parent` :

  - `notebooks.environments.create`

### Query parameters

Parameters

`environmentId`

`string`

Required. User-defined unique ID of this environment. The `environmentId` must be 1 to 63 characters long and contain only lowercase letters, numeric characters, and dashes. The first character must be a lowercase letter and the last character cannot be a dash.

### Request body

The request body contains an instance of `  Environment  ` .

### Response body

If successful, the response body contains a newly created instance of `  Operation  ` .

### Authorization scopes

Requires the following OAuth scope:

  - `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .
