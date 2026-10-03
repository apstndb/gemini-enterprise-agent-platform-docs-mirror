---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/rest/v1beta/VectorSearch
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/rest/v1beta/VectorSearch
title: VectorSearch
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Defines a search operation using a query vector.

**JSON representation**

```
{
  "searchField": string,
  "filter": {
    object
  },
  "outputFields": {
    object (OutputFields)
  },
  "searchHint": {
    object (SearchHint)
  },
  "distanceMetric": enum (DistanceMetric),

  // Union field vector_type can be only one of the following:
  "vector": {
    object (DenseVector)
  },
  "sparseVector": {
    object (SparseVector)
  }
  // End of list of possible types for union field vector_type.
  "topK": integer
}
```

| Fields                                                                                                                         |                                                                                                                                                                                                                                                                                                                         |
|--------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `searchField`                                                                                                                  | `string` Required. The vector field to search.                                                                                                                                                                                                                                                                          |
| `filter`                                                                                                                       | `object ( `[`Struct`](https://protobuf.dev/reference/protobuf/google.protobuf/#struct)` format)` Optional. A JSON filter expression, e.g. {"genre": {"\$eq": "sci-fi"}}, represented as a google.protobuf.Struct.                                                                                                       |
| `outputFields`                                                                                                                 | `object ( `[`OutputFields`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/rest/v1beta/OutputFields)` )` Optional. Mask specifying which fields to return.                                                                                                              |
| `searchHint`                                                                                                                   | `object ( `[`SearchHint`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/rest/v1beta/SearchHint)` )` Optional. Sets the search hint. If no strategy is specified, the service will use an index if one is available, and fall back to the default KNN search otherwise. |
| `distanceMetric`                                                                                                               | `enum ( `[`DistanceMetric`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/rest/v1beta/projects.locations.collections.indexes#DistanceMetric)` )` Optional. The distance metric to use for the KNN search. If not specified, DOT_PRODUCT will be used as the default.   |
| Union field `vector_type` . Specifies the type of vector to use for the query. `vector_type` can be only one of the following: |                                                                                                                                                                                                                                                                                                                         |
| `vector`                                                                                                                       | `object ( `[`DenseVector`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/rest/v1beta/projects.locations.collections.dataObjects#DenseVector)` )` A dense vector for the query.                                                                                         |
| `sparseVector`                                                                                                                 | `object ( `[`SparseVector`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/rest/v1beta/projects.locations.collections.dataObjects#SparseVector)` )` A sparse vector for the query.                                                                                      |
| `topK`                                                                                                                         | `integer` Optional. The number of nearest neighbors to return.                                                                                                                                                                                                                                                          |
