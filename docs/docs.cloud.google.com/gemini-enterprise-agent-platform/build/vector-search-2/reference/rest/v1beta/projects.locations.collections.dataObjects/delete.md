---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/rest/v1beta/projects.locations.collections.dataObjects/delete
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/rest/v1beta/projects.locations.collections.dataObjects/delete
title: 'Method: projects.locations.collections.dataObjects.delete'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Deletes a dataObject.

### HTTP request

`DELETE https://vectorsearch.googleapis.com/v1beta/{name}`

### Path parameters

Parameters

`name`

`string`

Required. The name of the DataObject resource to be deleted. Format: `projects/{project}/locations/{location}/collections/{collection}/dataObjects/{dataObject}`

### Query parameters

Parameters

`etag`

`string`

Optional. The current etag of the DataObject. If an etag is provided and does not match the current etag of the DataObject, deletion will be blocked and an ABORTED error will be returned.

### Request body

The request body must be empty.

### Response body

If successful, the response body is an empty JSON object.

### Authorization scopes

Requires the following OAuth scope:

  - `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .

### IAM Permissions

Requires the following [IAM](https://cloud.google.com/iam/docs) permission on the `name` resource:

  - `vectorsearch.dataObjects.delete`

For more information, see the [IAM documentation](https://cloud.google.com/iam/docs) .
