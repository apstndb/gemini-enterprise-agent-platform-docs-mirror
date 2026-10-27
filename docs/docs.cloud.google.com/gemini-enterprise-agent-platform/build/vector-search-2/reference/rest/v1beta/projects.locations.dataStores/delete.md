---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/rest/v1beta/projects.locations.dataStores/delete
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/rest/v1beta/projects.locations.dataStores/delete
title: 'Method: projects.locations.dataStores.delete'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Deletes a single DataStore.

### HTTP request

`DELETE https://vectorsearch.googleapis.com/v1beta/{name}`

### Path parameters

| Parameters |                                         |
|------------|-----------------------------------------|
| `name`     | `string` Required. Name of the resource |

### Query parameters

| Parameters                 |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
|----------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `requestId`                | `string` Optional. An optional request ID to identify requests. Specify a unique request ID so that if you must retry your request, the server will know to ignore the request if it has already been completed. The server will guarantee that for at least 60 minutes after the first request. For example, consider a situation where you make an initial request and the request times out. If you make the request again with the same request ID, the server can check if original operation with the same request ID was received, and if so, will ignore the second request. This prevents clients from accidentally creating duplicate commitments. The request ID must be a valid UUID with the exception that zero UUID is not supported (00000000-0000-0000-0000-000000000000). |
| `force`                    | `boolean` Optional. If set to true, any Documents from this DataStore will also be deleted. (Otherwise, the request will only work if the DataStore has no Documents.)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
| `backingCollectionDeleted` | `boolean` Optional. If set to true, the DataStore's auto-created backing Collection is torn down alongside the DataStore, force-deleting its DataObjects and Indexes. Defaults to false, retaining the Collection so its DataObjects keep serving. While a retained Collection exists, a DataStore with the same ID can't be created again.                                                                                                                                                                                                                                                                                                                                                                                                                                                 |

### Request body

The request body must be empty.

### Response body

If successful, the response body contains an instance of [`Operation`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/rest/Shared.Types/ListOperationsResponse#Operation) .

### Authorization scopes

Requires one of the following OAuth scopes:

- `https://www.googleapis.com/auth/cloud-platform`
- `https://www.googleapis.com/auth/vectorsearch`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .
