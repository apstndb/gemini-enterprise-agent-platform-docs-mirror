---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/rest/v1beta/projects.locations.dataStores/list
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/rest/v1beta/projects.locations.dataStores/list
title: 'Method: projects.locations.dataStores.list'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Lists DataStores in a given project and location.

### HTTP request

`GET https://vectorsearch.googleapis.com/v1beta/{parent}/dataStores`

### Path parameters

| Parameters |                                                            |
|------------|------------------------------------------------------------|
| `parent`   | `string` Required. Parent value for ListDataStoresRequest. |

### Query parameters

| Parameters  |                                                                                                                                                 |
|-------------|-------------------------------------------------------------------------------------------------------------------------------------------------|
| `pageSize`  | `integer` Optional. Requested page size. Server may return fewer items than requested. If unspecified, server will pick an appropriate default. |
| `pageToken` | `string` Optional. A token identifying a page of results the server should return.                                                              |
| `filter`    | `string` Optional. Filtering results                                                                                                            |
| `orderBy`   | `string` Optional. Hint for how to order the results                                                                                            |

### Request body

The request body must be empty.

### Response body

Message for response to listing DataStores.

If successful, the response body contains data with the following structure:

**JSON representation**

```
{
  "dataStores": [
    {
      object (DataStore)
    }
  ],
  "nextPageToken": string,
  "unreachable": [
    string
  ]
}
```

| Fields          |                                                                                                                                                                                                        |
|-----------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `dataStores[]`  | `object ( `[`DataStore`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/rest/v1beta/projects.locations.dataStores#DataStore)` )` The list of DataStore |
| `nextPageToken` | `string` A token identifying a page of results the server should return.                                                                                                                               |
| `unreachable[]` | `string` Unordered list. Locations that could not be reached.                                                                                                                                          |

### Authorization scopes

Requires one of the following OAuth scopes:

- `https://www.googleapis.com/auth/cloud-platform`
- `https://www.googleapis.com/auth/vectorsearch`
- `https://www.googleapis.com/auth/vectorsearch.readonly`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .
