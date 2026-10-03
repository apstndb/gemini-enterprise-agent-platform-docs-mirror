---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/rest/v1beta/SemanticSearch
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/rest/v1beta/SemanticSearch
title: SemanticSearch
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Defines a semantic search operation.

**JSON representation**

```
{
  "searchText": string,
  "searchField": string,
  "taskType": enum (EmbeddingTaskType),
  "outputFields": {
    object (OutputFields)
  },
  "filter": {
    object
  },
  "searchHint": {
    object (SearchHint)
  },
  "topK": integer
}
```

| Fields         |                                                                                                                                                                                                                                                                                                             |
|----------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `searchText`   | `string` Required. The query text, which is used to generate an embedding according to the embedding model specified in the collection config.                                                                                                                                                              |
| `searchField`  | `string` Required. The vector field to search.                                                                                                                                                                                                                                                              |
| `taskType`     | `enum ( `[`EmbeddingTaskType`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/rest/v1beta/projects.locations.collections#EmbeddingTaskType)` )` Required. The task type of the query embedding.                                                             |
| `outputFields` | `object ( `[`OutputFields`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/rest/v1beta/OutputFields)` )` Optional. The fields to return in the search results.                                                                                              |
| `filter`       | `object ( `[`Struct`](https://protobuf.dev/reference/protobuf/google.protobuf/#struct)` format)` Optional. A JSON filter expression, e.g. {"genre": {"\$eq": "sci-fi"}}, represented as a google.protobuf.Struct.                                                                                           |
| `searchHint`   | `object ( `[`SearchHint`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/rest/v1beta/SearchHint)` )` Optional. Sets the search hint. If no strategy is specified, the service will use an index if one is available, and fall back to KNN search otherwise. |
| `topK`         | `integer` Optional. The number of data objects to return.                                                                                                                                                                                                                                                   |
