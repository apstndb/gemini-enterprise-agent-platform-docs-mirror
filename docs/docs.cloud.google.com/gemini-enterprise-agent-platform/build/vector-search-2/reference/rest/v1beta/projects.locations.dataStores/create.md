---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/rest/v1beta/projects.locations.dataStores/create
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/rest/v1beta/projects.locations.dataStores/create
title: 'Method: projects.locations.dataStores.create'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Creates a new DataStore in a given project and location.

The DataStore's backing Collection (see `DataStore.collection_name` ) is created with it. The request fails with `FAILED_PRECONDITION` if a Collection with that ID already exists, for example one kept when an earlier DataStore with the same ID was deleted without `backingCollectionDeleted` .

### HTTP request

`POST https://vectorsearch.googleapis.com/v1beta/{parent}/dataStores`

### Path parameters

| Parameters |                                      |
|------------|--------------------------------------|
| `parent`   | `string` Required. Value for parent. |

### Query parameters

| Parameters    |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
|---------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `dataStoreId` | `string` Required. ID of the DataStore to create. The id must be 1-63 characters long, and comply with [RFC1035](https://www.ietf.org/rfc/rfc1035.txt) . Specifically, it must be 1-63 characters long and match the regular expression `[a-z](?:[-a-z0-9]{0,61}[a-z0-9])?` .                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| `requestId`   | `string` Optional. An optional request ID to identify requests. Specify a unique request ID so that if you must retry your request, the server will know to ignore the request if it has already been completed. The server will guarantee that for at least 60 minutes since the first request. For example, consider a situation where you make an initial request and the request times out. If you make the request again with the same request ID, the server can check if original operation with the same request ID was received, and if so, will ignore the second request. This prevents clients from accidentally creating duplicate commitments. The request ID must be a valid UUID with the exception that zero UUID is not supported (00000000-0000-0000-0000-000000000000). |

### Request body

The request body contains an instance of [`DataStore`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/rest/v1beta/projects.locations.dataStores#DataStore) .

### Response body

If successful, the response body contains a newly created instance of [`Operation`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/rest/Shared.Types/ListOperationsResponse#Operation) .

### Authorization scopes

Requires one of the following OAuth scopes:

- `https://www.googleapis.com/auth/cloud-platform`
- `https://www.googleapis.com/auth/vectorsearch`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .
