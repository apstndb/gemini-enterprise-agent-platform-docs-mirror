---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/rest/v1beta/projects.locations/list
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/rest/v1beta/projects.locations/list
title: 'Method: projects.locations.list'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Lists information about the supported locations for this service.

This method lists locations based on the resource scope provided in the `  ListLocationsRequest.name  ` field:

  - **Global locations** : If `name` is empty, the method lists the public locations available to all projects.
  - **Project-specific locations** : If `name` follows the format `projects/{project}` , the method lists locations visible to that specific project. This includes public, private, or other project-specific locations enabled for the project.

For gRPC and client library implementations, the resource name is passed as the `name` field. For direct service calls, the resource name is incorporated into the request path based on the specific service implementation and version.

### HTTP request

`GET https://vectorsearch.googleapis.com/v1beta/{name}/locations`

### Path parameters

Parameters

`name`

`string`

The resource that owns the locations collection, if applicable.

### Query parameters

Parameters

`filter`

`string`

A filter to narrow down results to a preferred subset. The filtering language accepts strings like `"displayName=tokyo"` , and is documented in more detail in [AIP-160](https://google.aip.dev/160) .

`pageSize`

`integer`

The maximum number of results to return. If not set, the service selects a default.

`pageToken`

`string`

A page token received from the `nextPageToken` field in the response. Send that page token to receive the subsequent page.

`extraLocationTypes[]`

`string`

Optional. Do not use this field unless explicitly documented otherwise. This is primarily for internal usage.

### Request body

The request body must be empty.

### Response body

If successful, the response body contains an instance of `  ListLocationsResponse  ` .

### Authorization scopes

Requires the following OAuth scope:

  - `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .

### IAM Permissions

Requires the following [IAM](https://cloud.google.com/iam/docs) permission on the `name` resource:

  - `vectorsearch.locations.list`

For more information, see the [IAM documentation](https://cloud.google.com/iam/docs) .
