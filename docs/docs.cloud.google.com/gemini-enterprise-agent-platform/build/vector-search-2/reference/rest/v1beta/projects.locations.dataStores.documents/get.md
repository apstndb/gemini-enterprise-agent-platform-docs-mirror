---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/rest/v1beta/projects.locations.dataStores.documents/get
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/rest/v1beta/projects.locations.dataStores.documents/get
title: 'Method: projects.locations.dataStores.documents.get'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Gets a Document.

### HTTP request

`GET https://vectorsearch.googleapis.com/v1beta/{name}`

### Path parameters

| Parameters |                                                                                                                                                     |
|------------|-----------------------------------------------------------------------------------------------------------------------------------------------------|
| `name`     | `string` Required. The name of the Document resource. Format: `projects/{project}/locations/{location}/dataStores/{dataStore}/documents/{document}` |

### Request body

The request body must be empty.

### Response body

If successful, the response body contains an instance of [`Document`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/rest/v1beta/projects.locations.dataStores.documents#Document) .

### Authorization scopes

Requires one of the following OAuth scopes:

- `https://www.googleapis.com/auth/cloud-platform`
- `https://www.googleapis.com/auth/vectorsearch`
- `https://www.googleapis.com/auth/vectorsearch.readonly`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .
