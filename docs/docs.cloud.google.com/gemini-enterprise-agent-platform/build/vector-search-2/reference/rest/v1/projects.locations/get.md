---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/rest/v1/projects.locations/get
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/rest/v1/projects.locations/get
title: 'Method: projects.locations.get'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Gets information about a location.

### HTTP request

`GET https://vectorsearch.googleapis.com/v1/{name}`

### Path parameters

Parameters

`name`

`string`

Resource name for the location.

### Request body

The request body must be empty.

### Response body

If successful, the response body contains an instance of `  Location  ` .

### Authorization scopes

Requires the following OAuth scope:

  - `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .

### IAM Permissions

Requires the following [IAM](https://cloud.google.com/iam/docs) permission on the `name` resource:

  - `vectorsearch.locations.get`

For more information, see the [IAM documentation](https://cloud.google.com/iam/docs) .
