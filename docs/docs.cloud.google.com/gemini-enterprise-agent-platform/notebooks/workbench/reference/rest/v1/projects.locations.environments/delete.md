---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v1/projects.locations.environments/delete
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/reference/rest/v1/projects.locations.environments/delete
title: 'Method: projects.locations.environments.delete'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Deletes a single Environment.

### HTTP request

`DELETE https://notebooks.googleapis.com/v1/{name}`

### Path parameters

Parameters

`name`

`string`

Required. Format: `projects/{projectId}/locations/{location}/environments/{environmentId}`

Authorization requires the following [IAM](https://cloud.google.com/iam/docs/) permission on the specified resource `name` :

  - `notebooks.environments.delete`

### Request body

The request body must be empty.

### Response body

If successful, the response body contains an instance of `  Operation  ` .

### Authorization scopes

Requires the following OAuth scope:

  - `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .
