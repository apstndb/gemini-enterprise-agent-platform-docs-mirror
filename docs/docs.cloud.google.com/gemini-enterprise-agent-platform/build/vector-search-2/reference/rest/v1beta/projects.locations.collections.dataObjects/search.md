---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/rest/v1beta/projects.locations.collections.dataObjects/search
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/rest/v1beta/projects.locations.collections.dataObjects/search
title: 'Method: projects.locations.collections.dataObjects.search'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Searches data objects.

### HTTP request

`POST https://vectorsearch.googleapis.com/v1beta/{parent}/dataObjects:search`

### Path parameters

| Parameters |                                                                                                                                                        |
|------------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| `parent`   | `string` Required. The resource name of the Collection for which to search. Format: `projects/{project}/locations/{location}/collections/{collection}` |

### Request body

The request body contains data with the following structure:

**JSON representation**

```
{
  "pageSize": integer,
  "pageToken": string,

  // Union field search_type can be only one of the following:
  "vectorSearch": {
    object (VectorSearch)
  },
  "semanticSearch": {
    object (SemanticSearch)
  },
  "textSearch": {
    object (TextSearch)
  }
  // End of list of possible types for union field search_type.
}
```

| Fields                                                                                               |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
|------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `pageSize`                                                                                           | `integer` Optional. The standard list page size. Only supported for KNN. If not set, up to search_type.top_k results will be returned. The maximum value is 1000; values above 1000 will be coerced to 1000.                                                                                                                                                                                                                                                                                                                                                                                    |
| `pageToken`                                                                                          | `string` Optional. The standard list page token. Typically obtained via [`SearchDataObjectsResponse.next_page_token`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/rest/v1beta/SearchDataObjectsResponse#FIELDS.next_page_token) of the previous [`DataObjectSearchService.SearchDataObjects`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/rest/v1beta/projects.locations.collections.dataObjects/search#google.cloud.vectorsearch.v1beta.DataObjectSearchService.SearchDataObjects) call. |
| Union field `search_type` . The query to search for. `search_type` can be only one of the following: |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| `vectorSearch`                                                                                       | `object ( `[`VectorSearch`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/rest/v1beta/VectorSearch)` )` A vector search operation.                                                                                                                                                                                                                                                                                                                                                                                                             |
| `semanticSearch`                                                                                     | `object ( `[`SemanticSearch`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/rest/v1beta/SemanticSearch)` )` A semantic search operation.                                                                                                                                                                                                                                                                                                                                                                                                       |
| `textSearch`                                                                                         | `object ( `[`TextSearch`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/rest/v1beta/TextSearch)` )` Optional. A text search operation.                                                                                                                                                                                                                                                                                                                                                                                                         |

### Response body

If successful, the response body contains an instance of [`SearchDataObjectsResponse`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/rest/v1beta/SearchDataObjectsResponse) .

### Authorization scopes

Requires the following OAuth scope:

- `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .

### IAM Permissions

Requires the following [IAM](https://cloud.google.com/iam/docs) permission on the `parent` resource:

- `vectorsearch.dataObjects.search`

For more information, see the [IAM documentation](https://cloud.google.com/iam/docs) .
