---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v1/projects.locations.runtimes/create
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v1/projects.locations.runtimes/create
title: 'Method: projects.locations.runtimes.create'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Creates a new Runtime in a given project and location.

### HTTP request

`POST https://notebooks.googleapis.com/v1/{parent}/runtimes`

### Path parameters

Parameters

`parent`

`string`

Required. Format: `parent=projects/{projectId}/locations/{location}`

Authorization requires the following [IAM](https://cloud.google.com/iam/docs/) permission on the specified resource `parent` :

  - `notebooks.runtimes.create`

### Query parameters

Parameters

`runtimeId`

`string`

Required. User-defined unique ID of this Runtime.

`requestId`

`string`

Idempotent request UUID.

### Request body

The request body contains an instance of `  Runtime  ` .

### Response body

If successful, the response body contains a newly created instance of `  Operation  ` .

### Authorization scopes

Requires the following OAuth scope:

  - `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .
