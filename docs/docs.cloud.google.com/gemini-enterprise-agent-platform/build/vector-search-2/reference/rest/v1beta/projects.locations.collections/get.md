---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/rest/v1beta/projects.locations.collections/get
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/rest/v1beta/projects.locations.collections/get
title: 'Method: projects.locations.collections.get'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Gets details of a single Collection.

### HTTP request

`GET https://vectorsearch.googleapis.com/v1beta/{name}`

### Path parameters

Parameters

`name`

`string`

Required. Name of the resource

### Request body

The request body must be empty.

### Response body

If successful, the response body contains an instance of `  Collection  ` .

### Authorization scopes

Requires the following OAuth scope:

  - `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .

### IAM Permissions

Requires the following [IAM](https://cloud.google.com/iam/docs) permission on the `name` resource:

  - `vectorsearch.collections.get`

For more information, see the [IAM documentation](https://cloud.google.com/iam/docs) .
