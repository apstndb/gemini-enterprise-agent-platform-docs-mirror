---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/rest/v1beta/projects.locations.dataStores.documents/list
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/rest/v1beta/projects.locations.dataStores.documents/list
title: 'Method: projects.locations.dataStores.documents.list'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Lists Documents in a DataStore.

### HTTP request

`GET https://vectorsearch.googleapis.com/v1beta/{parent}/documents`

### Path parameters

| Parameters |                                                                                                                                                        |
|------------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| `parent`   | `string` Required. The resource name of the DataStore to list Documents from. Format: `projects/{project}/locations/{location}/dataStores/{dataStore}` |

### Query parameters

| Parameters  |                                                                                                                                                                                                           |
|-------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `pageSize`  | `integer` Optional. Requested page size. Server may return fewer items than requested. If unspecified, at most 10 Documents are returned. The maximum value is 1,000; larger values are coerced to 1,000. |
| `pageToken` | `string` Optional. A token identifying a page of results the server should return.                                                                                                                        |
| `filter`    | `string` Optional. Not currently supported. A request that sets this field fails with `INVALID_ARGUMENT` .                                                                                                |
| `orderBy`   | `string` Optional. Not currently supported. A request that sets this field fails with `INVALID_ARGUMENT` .                                                                                                |

### Request body

The request body must be empty.

### Response body

Response message for [`DocumentService.ListDocuments`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/rest/v1beta/projects.locations.dataStores.documents/list#google.cloud.vectorsearch.v1beta.DocumentService.ListDocuments) .

If successful, the response body contains data with the following structure:

**JSON representation**

```
{
  "documents": [
    {
      object (Document)
    }
  ],
  "nextPageToken": string
}
```

| Fields          |                                                                                                                                                                                                                 |
|-----------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `documents[]`   | `object ( `[`Document`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/rest/v1beta/projects.locations.dataStores.documents#Document)` )` The list of Documents. |
| `nextPageToken` | `string` A token identifying a page of results the server should return.                                                                                                                                        |

### Authorization scopes

Requires one of the following OAuth scopes:

- `https://www.googleapis.com/auth/cloud-platform`
- `https://www.googleapis.com/auth/vectorsearch`
- `https://www.googleapis.com/auth/vectorsearch.readonly`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .
