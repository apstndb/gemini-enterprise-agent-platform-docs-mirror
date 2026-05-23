---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/rest/v1/projects.locations.collections.dataObjects/create
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/rest/v1/projects.locations.collections.dataObjects/create
title: 'Method: projects.locations.collections.dataObjects.create'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Creates a dataObject.

### HTTP request

`POST https://vectorsearch.googleapis.com/v1/{parent}/dataObjects`

### Path parameters

Parameters

`parent`

`string`

Required. The resource name of the Collection to create the DataObject in. Format: `projects/{project}/locations/{location}/collections/{collection}`

### Query parameters

Parameters

`dataObjectId`

`string`

Required. The id of the dataObject to create. The id must be 1-63 characters long, and comply with [RFC1035](https://www.ietf.org/rfc/rfc1035.txt) . Specifically, it must be 1-63 characters long and match the regular expression `[a-z](?:[-a-z0-9]{0,61}[a-z0-9])?` .

### Request body

The request body contains an instance of `  DataObject  ` .

### Response body

If successful, the response body contains a newly created instance of `  DataObject  ` .

### Authorization scopes

Requires the following OAuth scope:

  - `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .

### IAM Permissions

Requires the following [IAM](https://cloud.google.com/iam/docs) permission on the `parent` resource:

  - `vectorsearch.dataObjects.create`

For more information, see the [IAM documentation](https://cloud.google.com/iam/docs) .
