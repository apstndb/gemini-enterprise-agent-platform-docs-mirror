---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/rest/v1beta/projects.locations.collections.dataObjects/patch
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/rest/v1beta/projects.locations.collections.dataObjects/patch
title: 'Method: projects.locations.collections.dataObjects.patch'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Updates a dataObject.

### HTTP request

`PATCH https://vectorsearch.googleapis.com/v1beta/{dataObject.name}`

### Path parameters

Parameters

`dataObject.name`

`string`

Identifier. The fully qualified resource name of the dataObject.

Format: `projects/{project}/locations/{location}/collections/{collection}/dataObjects/{dataObjectId}` The dataObjectId must be 1-63 characters long, and comply with [RFC1035](https://www.ietf.org/rfc/rfc1035.txt) .

### Query parameters

Parameters

`updateMask`

` string ( FieldMask  ` format)

Optional. The update mask applies to the resource. See `  google.protobuf.FieldMask  ` .

This is a comma-separated list of fully qualified names of fields. Example: `"user.displayName,photo"` .

### Request body

The request body contains an instance of `  DataObject  ` .

### Response body

If successful, the response body contains an instance of `  DataObject  ` .

### Authorization scopes

Requires the following OAuth scope:

  - `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .

### IAM Permissions

Requires the following [IAM](https://cloud.google.com/iam/docs) permission on the `name` resource:

  - `vectorsearch.dataObjects.update`

For more information, see the [IAM documentation](https://cloud.google.com/iam/docs) .
