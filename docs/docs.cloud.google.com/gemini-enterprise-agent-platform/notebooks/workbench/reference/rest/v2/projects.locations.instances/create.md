---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v2/projects.locations.instances/create
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v2/projects.locations.instances/create
title: 'Method: projects.locations.instances.create'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Creates a new Instance in a given project and location.

### HTTP request

`POST https://notebooks.googleapis.com/v2/{parent}/instances`

### Path parameters

Parameters

`parent`

`string`

Required. Format: `parent=projects/{projectId}/locations/{location}`

Authorization requires the following [IAM](https://cloud.google.com/iam/docs/) permission on the specified resource `parent` :

  - `notebooks.instances.create`

### Query parameters

Parameters

`instanceId`

`string`

Required. User-defined unique ID of this instance.

`requestId`

`string`

Optional. Idempotent request UUID.

### Request body

The request body contains an instance of `  Instance  ` .

### Response body

If successful, the response body contains a newly created instance of `  Operation  ` .

### Authorization scopes

Requires the following OAuth scope:

  - `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .
