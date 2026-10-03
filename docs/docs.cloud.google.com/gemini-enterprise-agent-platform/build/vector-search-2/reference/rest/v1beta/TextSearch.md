---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/rest/v1beta/TextSearch
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/rest/v1beta/TextSearch
title: TextSearch
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Defines a text search operation.

**JSON representation**

```
{
  "searchText": string,
  "dataFieldNames": [
    string
  ],
  "outputFields": {
    object (OutputFields)
  },
  "filter": {
    object
  },
  "topK": integer
}
```

| Fields             |                                                                                                                                                                                                                        |
|--------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `searchText`       | `string` Required. The query text.                                                                                                                                                                                     |
| `dataFieldNames[]` | `string` Required. The data field names to search.                                                                                                                                                                     |
| `outputFields`     | `object ( `[`OutputFields`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/rest/v1beta/OutputFields)` )` Optional. The fields to return in the search results.         |
| `filter`           | `object ( `[`Struct`](https://protobuf.dev/reference/protobuf/google.protobuf/#struct)` format)` Optional. A JSON filter expression, e.g. `{"genre": {"$eq": "sci-fi"}}` , represented as a `google.protobuf.Struct` . |
| `topK`             | `integer` Optional. The number of results to return.                                                                                                                                                                   |
