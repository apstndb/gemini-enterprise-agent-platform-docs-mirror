---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/rest/v1/projects.locations.operations/list
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/rest/v1/projects.locations.operations/list
title: 'Method: projects.locations.operations.list'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Lists operations that match the specified filter in the request. If the server doesn't support this method, it returns `UNIMPLEMENTED` .

### HTTP request

`GET https://vectorsearch.googleapis.com/v1/{name}/operations`

### Path parameters

Parameters

`name`

`string`

The name of the operation's parent resource.

### Query parameters

Parameters

`filter`

`string`

The standard list filter.

`pageSize`

`integer`

The standard list page size.

`pageToken`

`string`

The standard list page token.

`returnPartialSuccess`

`boolean`

When set to `true` , operations that are reachable are returned as normal, and those that are unreachable are returned in the `  ListOperationsResponse.unreachable  ` field.

This can only be `true` when reading across collections. For example, when `parent` is set to `"projects/example/locations/-"` .

This field is not supported by default and will result in an `UNIMPLEMENTED` error if set unless explicitly documented otherwise in service or product specific documentation.

### Request body

The request body must be empty.

### Response body

If successful, the response body contains an instance of `  ListOperationsResponse  ` .

### Authorization scopes

Requires the following OAuth scope:

  - `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .

### IAM Permissions

Requires the following [IAM](https://cloud.google.com/iam/docs) permission on the `name` resource:

  - `vectorsearch.operations.list`

For more information, see the [IAM documentation](https://cloud.google.com/iam/docs) .
