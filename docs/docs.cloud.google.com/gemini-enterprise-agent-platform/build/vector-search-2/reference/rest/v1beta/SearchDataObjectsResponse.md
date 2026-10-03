---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/rest/v1beta/SearchDataObjectsResponse
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/rest/v1beta/SearchDataObjectsResponse
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
  "nextPageToken": string,
  "searchResponseMetadata": {
    object (SearchResponseMetadata)
  }
}
```

| Fields                   |                                                                                                                                                                                                                                                          |
|--------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `results[]`              | `object ( `[`SearchResult`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/rest/v1beta/SearchDataObjectsResponse#SearchResult)` )` Output only. The list of dataObjects that match the search criteria.  |
| `nextPageToken`          | `string` Output only. A token to retrieve next page of results. Pass to \[DataObjectSearchService.SearchDataObjectsRequest.page_token\]\[\] to obtain that page.                                                                                         |
| `searchResponseMetadata` | `object ( `[`SearchResponseMetadata`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/rest/v1beta/SearchDataObjectsResponse#SearchResponseMetadata)` )` Output only. Metadata about the search execution. |

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

| Fields       |                                                                                                                                                                                                                                        |
|--------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `dataObject` | `object ( `[`DataObject`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/rest/v1beta/projects.locations.collections.dataObjects#DataObject)` )` Output only. The matching data object. |
| `distance`   | `number` Output only. Similarity distance or ranker score returned by BatchSearchDataObjects.                                                                                                                                          |

## SearchResponseMetadata

Metadata about the search execution.

**JSON representation**

```
{
  "warnings": [
    {
      object (Status)
    }
  ],

  // Union field index_type can be only one of the following:
  "usedIndex": {
    object (IndexInfo)
  },
  "usedKnn": boolean
  // End of list of possible types for union field index_type.
}
```

| Fields                                                                                            |                                                                                                                                                                                                                                                     |
|---------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `warnings[]`                                                                                      | `object ( `[`Status`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/rest/Shared.Types/ListOperationsResponse#Status)` )` Output only. Warnings or non-fatal errors that occurred during execution. |
| Union field `index_type` . The type of index used. `index_type` can be only one of the following: |                                                                                                                                                                                                                                                     |
| `usedIndex`                                                                                       | `object ( `[`IndexInfo`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/rest/v1beta/SearchDataObjectsResponse#IndexInfo)` )` Indicates that the search used a particular index.                     |
| `usedKnn`                                                                                         | `boolean` Output only. If true, the search used the system's default K-Nearest Neighbor (KNN) index engine.                                                                                                                                         |

## IndexInfo

Message that indicates the index used for the search.

**JSON representation**

```
{
  "name": string
}
```

| Fields |                                                                                                                                                                      |
|--------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `name` | `string` Output only. The resource name of the index used for the search. Format: `projects/{project}/locations/{location}/collections/{collection}/indexes/{index}` |
