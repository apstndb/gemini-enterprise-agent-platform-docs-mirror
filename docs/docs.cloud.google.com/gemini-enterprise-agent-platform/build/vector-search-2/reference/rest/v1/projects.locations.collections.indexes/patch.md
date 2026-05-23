---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/rest/v1/projects.locations.collections.indexes/patch
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/rest/v1/projects.locations.collections.indexes/patch
title: 'Method: projects.locations.collections.indexes.patch'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Updates the parameters of a single Index.

### HTTP request

`PATCH https://vectorsearch.googleapis.com/v1/{index.name}`

### Path parameters

Parameters

`index.name`

`string`

Identifier. name of resource

### Query parameters

Parameters

`updateMask`

` string ( FieldMask  ` format)

Optional. Specifies the fields to be overwritten in the Index resource by the update. The fields specified in the updateMask are relative to the resource, not the full request. A field will be overwritten if it is in the mask. If the user does not provide a mask then all fields present in the request with non-empty values will be overwritten.

The following fields support update: \* `displayName` \* `description` \* `labels` \* `dedicatedInfrastructure.autoscaling_spec.min_replica_count` \* `dedicatedInfrastructure.autoscaling_spec.max_replica_count`

If `*` is provided in the `updateMask` , full replacement of mutable fields will be performed.

This is a comma-separated list of fully qualified names of fields. Example: `"user.displayName,photo"` .

`requestId`

`string`

Optional. An optional request ID to identify requests. Specify a unique request ID so that if you must retry your request, the server will know to ignore the request if it has already been completed. The server will guarantee that for at least 60 minutes since the first request.

For example, consider a situation where you make an initial request and the request times out. If you make the request again with the same request ID, the server can check if original operation with the same request ID was received, and if so, will ignore the second request. This prevents clients from accidentally creating duplicate commitments.

The request ID must be a valid UUID with the exception that zero UUID is not supported (00000000-0000-0000-0000-000000000000).

### Request body

The request body contains an instance of `  Index  ` .

### Response body

If successful, the response body contains an instance of `  Operation  ` .

### Authorization scopes

Requires the following OAuth scope:

  - `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .

### IAM Permissions

Requires the following [IAM](https://cloud.google.com/iam/docs) permission on the `name` resource:

  - `vectorsearch.indexes.update`

For more information, see the [IAM documentation](https://cloud.google.com/iam/docs) .
