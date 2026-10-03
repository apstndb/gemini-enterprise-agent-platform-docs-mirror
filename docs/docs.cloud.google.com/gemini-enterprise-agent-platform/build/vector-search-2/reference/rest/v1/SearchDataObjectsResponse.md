---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/rest/v1/SearchDataObjectsResponse
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/rest/v1/SearchDataObjectsResponse
title: SearchDataObjectsResponse
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Response for a search request.

**JSON representation**

```
{
  "results": [
    {
      object (SearchResult)
    }
  ],
  "nextPageToken": string
}
```

| Fields          |                                                                                                                                                                                                                                                     |
|-----------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `results[]`     | `object ( `[`SearchResult`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/rest/v1/SearchDataObjectsResponse#SearchResult)` )` Output only. The list of dataObjects that match the search criteria. |
| `nextPageToken` | `string` Output only. A token to retrieve next page of results. Pass to \[DataObjectSearchService.SearchDataObjectsRequest.page_token\]\[\] to obtain that page.                                                                                    |

## SearchResult

A single search result.

**JSON representation**

```
{
  "dataObject": {
    object (DataObject)
  },
  "distance": number
}
```

| Fields       |                                                                                                                                                                                                                                    |
|--------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `dataObject` | `object ( `[`DataObject`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/rest/v1/projects.locations.collections.dataObjects#DataObject)` )` Output only. The matching data object. |
| `distance`   | `number` Output only. Similarity distance or ranker score returned by BatchSearchDataObjects.                                                                                                                                      |
