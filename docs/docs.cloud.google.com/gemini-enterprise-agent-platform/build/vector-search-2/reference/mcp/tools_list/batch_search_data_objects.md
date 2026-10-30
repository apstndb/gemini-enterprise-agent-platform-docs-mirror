---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/mcp/tools_list/batch_search_data_objects
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/mcp/tools_list/batch_search_data_objects
title: 'MCP Tools Reference: vectorsearch.googleapis.com'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

## Tool: `batch_search_data_objects`

Runs multiple `Search` operations against one collection in a single RPC and, optionally, fuses them into one ranked list.

- **Primary use case: hybrid retrieval** — run semantic + text + explicit vector searches in parallel and combine them, recovering results that no single strategy would surface. Also useful for query expansion (fan one query into N rewrites) and multi-field search (same query against different vector fields).

- If `combine` is omitted, per-search results are returned unmerged in `results[]` (one entry per input search).

- `combine.ranker.rrf.weights` (required when combining): Reciprocal Rank Fusion. Provide N weights matching the order of `searches` ; equal weights are a sane default.

- `combine.reranker.vertexRanker` (optional; runs *after* RRF): cross-encoder rerank via the Vertex Ranking API. Substantially better quality for RAG and ambiguous natural-language queries; adds \~50-200 ms latency. Specify a supported ranking `model` (for example, `semantic-ranker-fast@latest` ). `topN` must be positive, `<= 1000` , and `>= combine.topK` . Templates in `textRecordSpec` ( `titleTemplate` , `contentTemplate` ) use single-brace field substitution (e.g. `"{title}"` , `"{genre}: {content}"` ); every `{field}` referenced must exist in the collection's `dataSchema` or the RPC returns `INVALID_ARGUMENT` .

- **Choose RRF-only for latency-critical paths (\<100 ms budget); add Vertex Ranker for quality-critical retrieval.**

- **Example** (hybrid RAG: semantic + text merged with RRF, then reranked):

  ```
  searches:
    - semanticSearch: { searchText: "<query>", searchField: "text_embedding" }
    - textSearch:     { searchText: "<query>", dataFieldNames: ["title", "content"] }
  combine:
    ranker:   { rrf: { weights: [1.0, 1.0] } }
    reranker: { vertexRanker: {
      model: "semantic-ranker-fast@latest",
      topN: 100,
      textRecordSpec: {
        query: "<query>",
        titleTemplate: "{title}",
        contentTemplate: "{genre}: {content}",
      },
    } }
    topK: 10
  ```

The following code sample shows how to use `curl` to call the `batch_search_data_objects` MCP tool.

**Curl Request**

```
curl --location 'https://vectorsearch.googleapis.com/mcp' \
--header 'content-type: application/json' \
--header 'accept: application/json, text/event-stream' \
--data '{
  "method": "tools/call",
  "params": {
    "name": "batch_search_data_objects",
    "arguments": {
      // Provide these details according to the MCP tool specification.
    }
  },
  "jsonrpc": "2.0",
  "id": 1
}'
```

## Input Schema

Request for `batch_search_data_objects` .

### BatchSearchDataObjectsRequest

**JSON representation**

```
{
  "projectId": string,
  "location": string,
  "collectionId": string,
  "searches": [
    {
      object (Search)
    }
  ],
  "combine": {
    object (CombineResultsOptions)
  }
}
```

| Fields         |                                                                                                                                                                                                                                                                                                  |
|----------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `projectId`    | `string` Required. The project ID or number.                                                                                                                                                                                                                                                     |
| `location`     | `string` Required. The region of the Collection, e.g. `us-central1` .                                                                                                                                                                                                                            |
| `collectionId` | `string` Required. The ID of the Collection to search.                                                                                                                                                                                                                                           |
| `searches[]`   | `object ( `[`Search`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/mcp/tools_list/batch_search_data_objects#Input.Schema.Search)` )` Required. A list of search requests to execute in parallel.                                               |
| `combine`      | `object ( `[`CombineResultsOptions`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/mcp/tools_list/batch_search_data_objects#Input.Schema.CombineResultsOptions)` )` Optional. Options for combining the results of the batch search operations. |

### Search

**JSON representation**

```
{

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

| Fields                                                                                                     |                                                                                                                                                                                                                     |
|------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Union field `search_type` . The type of search to perform. `search_type` can be only one of the following: |                                                                                                                                                                                                                     |
| `vectorSearch`                                                                                             | `object ( `[`VectorSearch`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/mcp/tools_list/search_data_objects#Input.Schema.VectorSearch)` )` A vector-based search. |
| `semanticSearch`                                                                                           | `object ( `[`SemanticSearch`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/mcp/tools_list/search_data_objects#Input.Schema.SemanticSearch)` )` A semantic search. |
| `textSearch`                                                                                               | `object ( `[`TextSearch`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/mcp/tools_list/search_data_objects#Input.Schema.TextSearch)` )` A text search operation.   |
|                                                                                                            |                                                                                                                                                                                                                     |

### VectorSearch

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

  // Union field _top_k can be only one of the following:
  "topK": integer
  // End of list of possible types for union field _top_k.
}
```

| Fields                                                                                                                         |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
|--------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `searchField`                                                                                                                  | `string` Required. The vector field to search.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
| `filter`                                                                                                                       | `object ( `[`Struct`](https://protobuf.dev/reference/protobuf/google.protobuf/#struct)` format)` Optional. A JSON filter expression, e.g. `{"genre": {"$eq": "sci-fi"}}` , represented as a `google.protobuf.Struct` . An empty filter ( `{}` ) matches all data objects. Otherwise, each JSON object in the filter must have exactly one key: either a field name mapped to one operator ( `{"price": {"$lt": 100}}` ), or a logical operator: `$and` or `$or` with a list of filters, or `$not` with one filter. Field operators and their values: `$eq` and `$ne` take a string, number or bool; `$lt` , `$lte` , `$gt` and `$gte` take a number; `$in` , `$nin` and `$all` take a list of strings; `$exists` takes a bool. Several keys in one object (implicit AND) and implicit equality ( `{"genre": "sci-fi"}` ) are rejected; use `$and` and `$eq` instead. Logical operators can be nested at most 2 levels deep, e.g. `{"$and": [{"$or": [{"a": {"$eq": 1}}, {"b": {"$eq": 2}}]}]}` . Deeper filters are rejected with `INVALID_ARGUMENT` . Which filters are accepted depends on how the search is served. If it is served by an approximate nearest neighbor (ANN) index (by default when a ready index exists on `search_field` , or when one is selected via `search_hint.index_hint` ), every filtered field must be listed in `Index.filter_fields` at index creation, `$or` and `$all` are accepted only at the top level of the filter, and `$not` and `$exists` are not supported. Not every unsupported filter is rejected: most produce `INVALID_ARGUMENT` , but some are silently ignored, so do not rely on the error. If no ready index exists on `search_field` , or if `search_hint.knn_hint` is set, the search is served by K-Nearest Neighbor (KNN) search, which has none of these filter restrictions. |
| `outputFields`                                                                                                                 | `object ( `[`OutputFields`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/mcp/tools_list/search_data_objects#Input.Schema.OutputFields)` )` Optional. Mask specifying which fields to return.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
| `searchHint`                                                                                                                   | `object ( `[`SearchHint`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/mcp/tools_list/search_data_objects#Input.Schema.SearchHint)` )` Optional. Sets the search hint. If no strategy is specified, the service will use an index if one is available, and fall back to the default KNN search otherwise.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| `distanceMetric`                                                                                                               | `enum ( `[`DistanceMetric`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/mcp/tools_list/list_indexes#Output.Schema.DistanceMetric)` )` Optional. The distance metric to use for the KNN search. If not specified, DOT_PRODUCT will be used as the default.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| Union field `vector_type` . Specifies the type of vector to use for the query. `vector_type` can be only one of the following: |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| `vector`                                                                                                                       | `object ( `[`DenseVector`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/mcp/tools_list/get_data_object#Output.Schema.DenseVector)` )` A dense vector for the query.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| `sparseVector`                                                                                                                 | `object ( `[`SparseVector`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/mcp/tools_list/get_data_object#Output.Schema.SparseVector)` )` A sparse vector for the query.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
|                                                                                                                                |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| Union field `_top_k` . `_top_k` can be only one of the following:                                                              |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| `topK`                                                                                                                         | `integer` Optional. The number of nearest neighbors to return.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
|                                                                                                                                |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |

### DenseVector

**JSON representation**

```
{
  "values": [
    number
  ]
}
```

| Fields     |                                              |
|------------|----------------------------------------------|
| `values[]` | `number` Required. The values of the vector. |

### SparseVector

**JSON representation**

```
{
  "values": [
    number
  ],
  "indices": [
    integer
  ]
}
```

| Fields      |                                                               |
|-------------|---------------------------------------------------------------|
| `values[]`  | `number` Required. The values of the vector.                  |
| `indices[]` | `integer` Required. The corresponding indices for the values. |

### Struct

**JSON representation**

```
{
  "fields": {
    string: value,
    ...
  }
}
```

| Fields   |                                                                                                                                                                                                                                                                                          |
|----------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `fields` | `map (key: string, value: value ( `[`Value`](https://protobuf.dev/reference/protobuf/google.protobuf/#value)` format))` Unordered map of dynamically typed values. An object containing a list of `"key": value` pairs. Example: `{ "name": "wrench", "mass": "1.3kg", "count": "3" }` . |

### FieldsEntry

**JSON representation**

```
{
  "key": string,
  "value": value
}
```

| Fields  |                                                                                               |
|---------|-----------------------------------------------------------------------------------------------|
| `key`   | `string`                                                                                      |
| `value` | `value ( `[`Value`](https://protobuf.dev/reference/protobuf/google.protobuf/#value)` format)` |

### Value

**JSON representation**

```
{

  // Union field kind can be only one of the following:
  "nullValue": null,
  "numberValue": number,
  "stringValue": string,
  "boolValue": boolean,
  "structValue": {
    object
  },
  "listValue": array
  // End of list of possible types for union field kind.
}
```

| Fields                                                                           |                                                                                                                                                                                                                                                |
|----------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Union field `kind` . The kind of value. `kind` can be only one of the following: |                                                                                                                                                                                                                                                |
| `nullValue`                                                                      | `null` Represents a JSON `null` .                                                                                                                                                                                                              |
| `numberValue`                                                                    | `number` Represents a JSON number. Must not be `NaN` , `Infinity` or `-Infinity` , since those are not supported in JSON. This also cannot represent large Int64 values, since JSON format generally does not support them in its number type. |
| `stringValue`                                                                    | `string` Represents a JSON string.                                                                                                                                                                                                             |
| `boolValue`                                                                      | `boolean` Represents a JSON boolean ( `true` or `false` literal in JSON).                                                                                                                                                                      |
| `structValue`                                                                    | `object ( `[`Struct`](https://protobuf.dev/reference/protobuf/google.protobuf/#struct)` format)` Represents a JSON object.                                                                                                                     |
| `listValue`                                                                      | `array ( `[`ListValue`](https://protobuf.dev/reference/protobuf/google.protobuf/#list-value)` format)` Represents a JSON array.                                                                                                                |
|                                                                                  |                                                                                                                                                                                                                                                |

### ListValue

**JSON representation**

```
{
  "values": [
    value
  ]
}
```

| Fields     |                                                                                                                                           |
|------------|-------------------------------------------------------------------------------------------------------------------------------------------|
| `values[]` | `value ( `[`Value`](https://protobuf.dev/reference/protobuf/google.protobuf/#value)` format)` Repeated field of dynamically typed values. |

### OutputFields

**JSON representation**

```
{
  "dataFields": [
    string
  ],
  "vectorFields": [
    string
  ],
  "metadataFields": [
    string
  ]
}
```

| Fields             |                                                                                                                                                                                                                   |
|--------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `dataFields[]`     | `string` Optional. The fields from the data fields to include in the output. Use `"*"` to include all data fields. If empty, `data` is omitted from results.                                                      |
| `vectorFields[]`   | `string` Optional. The fields from the vector fields to include in the output. Use `"*"` to include all vector fields. If empty, `vectors` is omitted from results.                                               |
| `metadataFields[]` | `string` Optional. The DataObject metadata fields to include in the output: `create_time` , `update_time` and `etag` . Use `"*"` to include all metadata fields. If empty, these fields are omitted from results. |

### SearchHint

**JSON representation**

```
{

  // Union field index_type can be only one of the following:
  "knnHint": {
    object (KnnHint)
  },
  "indexHint": {
    object (IndexHint)
  }
  // End of list of possible types for union field index_type.
}
```

| Fields                                                                                              |                                                                                                                                                                                                                                                           |
|-----------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Union field `index_type` . The type of index to use. `index_type` can be only one of the following: |                                                                                                                                                                                                                                                           |
| `knnHint`                                                                                           | `object ( ``KnnHint`` )` Optional. If set, the search will use the system's default K-Nearest Neighbor (KNN) index engine.                                                                                                                                |
| `indexHint`                                                                                         | `object ( `[`IndexHint`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/mcp/tools_list/search_data_objects#Input.Schema.IndexHint)` )` Optional. Specifies that the search should use a particular index. |
|                                                                                                     |                                                                                                                                                                                                                                                           |

### IndexHint

**JSON representation**

```
{
  "name": string,

  // Union field params can be only one of the following:
  "denseScannParams": {
    object (DenseScannParams)
  }
  // End of list of possible types for union field params.
}
```

| Fields                                                                                          |                                                                                                                                                                                                                                        |
|-------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `name`                                                                                          | `string` Required. The resource name of the index to use for the search. The index must be in the same project, location, and collection. Format: `projects/{project}/locations/{location}/collections/{collection}/indexes/{index}`   |
| Union field `params` . The parameters for the index. `params` can be only one of the following: |                                                                                                                                                                                                                                        |
| `denseScannParams`                                                                              | `object ( `[`DenseScannParams`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/mcp/tools_list/search_data_objects#Input.Schema.DenseScannParams)` )` Optional. Dense ScaNN parameters. |
|                                                                                                 |                                                                                                                                                                                                                                        |

### DenseScannParams

**JSON representation**

```
{

  // Union field _target_recall can be only one of the following:
  "targetRecall": number
  // End of list of possible types for union field _target_recall.
}
```

| Fields                                                                            |                                                                                                                                                                           |
|-----------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Union field `_target_recall` . `_target_recall` can be only one of the following: |                                                                                                                                                                           |
| `targetRecall`                                                                    | `number` Optional. The target recall for the search. Must be a double in the range \[0, 1\]. While the search aims to achieve this level of recall, it is not guaranteed. |
|                                                                                   |                                                                                                                                                                           |

### SemanticSearch

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

  // Union field _top_k can be only one of the following:
  "topK": integer
  // End of list of possible types for union field _top_k.
}
```

| Fields                                                            |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
|-------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `searchText`                                                      | `string` Optional. The query text, which is used to generate an embedding according to the embedding model specified in the collection config. Required when using the text search mode.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| `searchField`                                                     | `string` Required. The vector field to search.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
| `taskType`                                                        | `enum ( `[`EmbeddingTaskType`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/mcp/tools_list/list_collections#Output.Schema.EmbeddingTaskType)` )` Optional. The task type of the query embedding. Must be specified for text-only embedding models, see <https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/embeddings/task-types> Not needed for multi modal embedding models, see <https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/embeddings/get-multimodal-embeddings#specify-task-instructions>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
| `outputFields`                                                    | `object ( `[`OutputFields`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/mcp/tools_list/search_data_objects#Input.Schema.OutputFields)` )` Optional. The fields to return in the search results.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| `filter`                                                          | `object ( `[`Struct`](https://protobuf.dev/reference/protobuf/google.protobuf/#struct)` format)` Optional. A JSON filter expression, e.g. `{"genre": {"$eq": "sci-fi"}}` , represented as a `google.protobuf.Struct` . An empty filter ( `{}` ) matches all data objects. Otherwise, each JSON object in the filter must have exactly one key: either a field name mapped to one operator ( `{"price": {"$lt": 100}}` ), or a logical operator: `$and` or `$or` with a list of filters, or `$not` with one filter. Field operators and their values: `$eq` and `$ne` take a string, number or bool; `$lt` , `$lte` , `$gt` and `$gte` take a number; `$in` , `$nin` and `$all` take a list of strings; `$exists` takes a bool. Several keys in one object (implicit AND) and implicit equality ( `{"genre": "sci-fi"}` ) are rejected; use `$and` and `$eq` instead. Logical operators can be nested at most 2 levels deep, e.g. `{"$and": [{"$or": [{"a": {"$eq": 1}}, {"b": {"$eq": 2}}]}]}` . Deeper filters are rejected with `INVALID_ARGUMENT` . Which filters are accepted depends on how the search is served. If it is served by an approximate nearest neighbor (ANN) index (by default when a ready index exists on `search_field` , or when one is selected via `search_hint.index_hint` ), every filtered field must be listed in `Index.filter_fields` at index creation, `$or` and `$all` are accepted only at the top level of the filter, and `$not` and `$exists` are not supported. Not every unsupported filter is rejected: most produce `INVALID_ARGUMENT` , but some are silently ignored, so do not rely on the error. If no ready index exists on `search_field` , or if `search_hint.knn_hint` is set, the search is served by K-Nearest Neighbor (KNN) search, which has none of these filter restrictions. |
| `searchHint`                                                      | `object ( `[`SearchHint`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/mcp/tools_list/search_data_objects#Input.Schema.SearchHint)` )` Optional. Sets the search hint. If no strategy is specified, the service will use an index if one is available, and fall back to KNN search otherwise.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| Union field `_top_k` . `_top_k` can be only one of the following: |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| `topK`                                                            | `integer` Optional. The number of data objects to return.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
|                                                                   |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |

### TextSearch

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

  // Union field _top_k can be only one of the following:
  "topK": integer
  // End of list of possible types for union field _top_k.
}
```

| Fields                                                            |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
|-------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `searchText`                                                      | `string` Optional. The query text.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| `dataFieldNames[]`                                                | `string` Optional. The data field names to search.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| `outputFields`                                                    | `object ( `[`OutputFields`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/mcp/tools_list/search_data_objects#Input.Schema.OutputFields)` )` Optional. The fields to return in the search results.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| `filter`                                                          | `object ( `[`Struct`](https://protobuf.dev/reference/protobuf/google.protobuf/#struct)` format)` Optional. A JSON filter expression, e.g. `{"genre": {"$eq": "sci-fi"}}` , represented as a `google.protobuf.Struct` . An empty filter ( `{}` ) matches all data objects. Otherwise, each JSON object in the filter must have exactly one key: either a field name mapped to one operator ( `{"price": {"$lt": 100}}` ), or a logical operator: `$and` or `$or` with a list of filters, or `$not` with one filter. Field operators and their values: `$eq` and `$ne` take a string, number or bool; `$lt` , `$lte` , `$gt` and `$gte` take a number; `$in` , `$nin` and `$all` take a list of strings; `$exists` takes a bool. Several keys in one object (implicit AND) and implicit equality ( `{"genre": "sci-fi"}` ) are rejected; use `$and` and `$eq` instead. Logical operators can be nested at most 2 levels deep, e.g. `{"$and": [{"$or": [{"a": {"$eq": 1}}, {"b": {"$eq": 2}}]}]}` . Deeper filters are rejected with `INVALID_ARGUMENT` . |
| Union field `_top_k` . `_top_k` can be only one of the following: |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| `topK`                                                            | `integer` Optional. The number of results to return.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
|                                                                   |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |

### CombineResultsOptions

**JSON representation**

```
{
  "ranker": {
    object (Ranker)
  },
  "outputFields": {
    object (OutputFields)
  },
  "topK": integer
}
```

| Fields         |                                                                                                                                                                                                                                                |
|----------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `ranker`       | `object ( `[`Ranker`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/mcp/tools_list/batch_search_data_objects#Input.Schema.Ranker)` )` Required. The ranker to use for combining the results.  |
| `outputFields` | `object ( `[`OutputFields`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/mcp/tools_list/search_data_objects#Input.Schema.OutputFields)` )` Optional. Mask specifying which fields to return. |
| `topK`         | `integer` Optional. The number of results to return. If not set, a default value will be used.                                                                                                                                                 |

### Ranker

**JSON representation**

```
{

  // Union field ranker can be only one of the following:
  "rrf": {
    object (ReciprocalRankFusion)
  }
  // End of list of possible types for union field ranker.

  // Union field reranker can be only one of the following:
  "vertexRanker": {
    object (VertexRanker)
  }
  // End of list of possible types for union field reranker.
}
```

| Fields                                                                                                                                             |                                                                                                                                                                                                                                                    |
|----------------------------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Union field `ranker` . The ranking method to use. `ranker` can be only one of the following:                                                       |                                                                                                                                                                                                                                                    |
| `rrf`                                                                                                                                              | `object ( `[`ReciprocalRankFusion`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/mcp/tools_list/batch_search_data_objects#Input.Schema.ReciprocalRankFusion)` )` Reciprocal Rank Fusion ranking. |
|                                                                                                                                                    |                                                                                                                                                                                                                                                    |
| Union field `reranker` . The reranker to use for final ranking of the results combined by the ranker. `reranker` can be only one of the following: |                                                                                                                                                                                                                                                    |
| `vertexRanker`                                                                                                                                     | `object ( `[`VertexRanker`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/mcp/tools_list/batch_search_data_objects#Input.Schema.VertexRanker)` )` Optional. Vertex AI ranking.                    |
|                                                                                                                                                    |                                                                                                                                                                                                                                                    |

### ReciprocalRankFusion

**JSON representation**

```
{
  "weights": [
    number
  ]
}
```

| Fields      |                                                                                  |
|-------------|----------------------------------------------------------------------------------|
| `weights[]` | `number` Required. The weights to apply to each search result set during fusion. |

### VertexRanker

**JSON representation**

```
{
  "model": string,
  "topN": integer,

  // Union field record_spec can be only one of the following:
  "textRecordSpec": {
    object (TextRecordSpec)
  }
  // End of list of possible types for union field record_spec.
}
```

| Fields                                                                                                                                                  |                                                                                                                                                                                                                                                   |
|---------------------------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `model`                                                                                                                                                 | `string` Required. The model used for ranking documents. The list of available models is described in <https://docs.cloud.google.com/generative-ai-app-builder/docs/ranking#models> . Currently, only `semantic-ranker-fast@latest` is supported. |
| `topN`                                                                                                                                                  | `integer` Required. The number of documents to be processed for ranking.                                                                                                                                                                          |
| Union field `record_spec` . The record specification for ranking. At least one record spec must be set. `record_spec` can be only one of the following: |                                                                                                                                                                                                                                                   |
| `textRecordSpec`                                                                                                                                        | `object ( `[`TextRecordSpec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/mcp/tools_list/batch_search_data_objects#Input.Schema.TextRecordSpec)` )` The record spec for text search.           |
|                                                                                                                                                         |                                                                                                                                                                                                                                                   |

### TextRecordSpec

**JSON representation**

```
{
  "query": string,
  "titleTemplate": string,
  "contentTemplate": string
}
```

| Fields            |                                                                               |
|-------------------|-------------------------------------------------------------------------------|
| `query`           | `string` Required. The query against which the records are ranked and scored. |
| `titleTemplate`   | `string` Optional. The template used to generate the record's title.          |
| `contentTemplate` | `string` Optional. The template used to generate the record's content.        |

### NullValue

Represents a JSON `null` .

`NullValue` is a sentinel, using an enum with only one value to represent the null value for the `Value` type union.

A field of type `NullValue` with any value other than `0` is considered invalid. Most ProtoJSON serializers will emit a `Value` with a `null_value` set as a JSON `null` regardless of the integer value, and so will round trip to a `0` value.

| Enums        |             |
|--------------|-------------|
| `NULL_VALUE` | Null value. |

### DistanceMetric

Distance metric for vector search.

| Enums                         |                                                  |
|-------------------------------|--------------------------------------------------|
| `DISTANCE_METRIC_UNSPECIFIED` | Default value, distance metric is not specified. |
| `DOT_PRODUCT`                 | Dot product distance metric.                     |
| `COSINE_DISTANCE`             | Cosine distance metric.                          |

### EmbeddingTaskType

Represents the task the embeddings will be used for.

| Enums                             |                                                                        |
|-----------------------------------|------------------------------------------------------------------------|
| `EMBEDDING_TASK_TYPE_UNSPECIFIED` | Unspecified task type.                                                 |
| `RETRIEVAL_QUERY`                 | Specifies the given text is a query in a search/retrieval setting.     |
| `RETRIEVAL_DOCUMENT`              | Specifies the given text is a document from the corpus being searched. |
| `SEMANTIC_SIMILARITY`             | Specifies the given text will be used for STS.                         |
| `CLASSIFICATION`                  | Specifies that the given text will be classified.                      |
| `CLUSTERING`                      | Specifies that the embeddings will be used for clustering.             |
| `QUESTION_ANSWERING`              | Specifies that the embeddings will be used for question answering.     |
| `FACT_VERIFICATION`               | Specifies that the embeddings will be used for fact verification.      |
| `CODE_RETRIEVAL_QUERY`            | Specifies that the embeddings will be used for code retrieval.         |

## Output Schema

A response from a batch search operation.

### BatchSearchDataObjectsResponse

**JSON representation**

```
{
  "results": [
    {
      object (SearchDataObjectsResponse)
    }
  ]
}
```

| Fields      |                                                                                                                                                                                                                                                                                                                                                                       |
|-------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `results[]` | `object ( `[`SearchDataObjectsResponse`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/mcp/tools_list/search_data_objects#Output.Schema.SearchDataObjectsResponse)` )` Output only. A list of search responses, one for each request in the batch. If a ranker is used, a single ranked list of results is returned. |

### SearchDataObjectsResponse

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

| Fields          |                                                                                                                                                                                                                                                                    |
|-----------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `results[]`     | `object ( `[`SearchResult`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/mcp/tools_list/search_data_objects#Output.Schema.SearchResult)` )` Output only. The list of dataObjects that match the search criteria. |
| `nextPageToken` | `string` Output only. A token to retrieve next page of results. Pass to `pageToken` to obtain that page.                                                                                                                                                           |

### SearchResult

**JSON representation**

```
{
  "dataObject": {
    object (DataObject)
  },

  // Union field _distance can be only one of the following:
  "distance": number
  // End of list of possible types for union field _distance.
}
```

| Fields                                                                  |                                                                                                                                                                                                                              |
|-------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `dataObject`                                                            | `object ( `[`DataObject`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/mcp/tools_list/get_data_object#Output.Schema.DataObject)` )` Output only. The matching data object. |
| Union field `_distance` . `_distance` can be only one of the following: |                                                                                                                                                                                                                              |
| `distance`                                                              | `number` Output only. Similarity distance or ranker score returned by BatchSearchDataObjects.                                                                                                                                |
|                                                                         |                                                                                                                                                                                                                              |

### DataObject

**JSON representation**

```
{
  "name": string,
  "dataObjectId": string,
  "createTime": string,
  "updateTime": string,
  "data": {
    object
  },
  "vectors": {
    string: {
      object (Vector)
    },
    ...
  },
  "etag": string
}
```

| Fields         |                                                                                                                                                                                                                                                                                                                                                                                                                               |
|----------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `name`         | `string` Identifier. The fully qualified resource name of the dataObject. Format: `projects/{project}/locations/{location}/collections/{collection}/dataObjects/{data_object_id}` The data_object_id must be 1-63 characters long, and comply with [RFC1035](https://www.ietf.org/rfc/rfc1035.txt) .                                                                                                                          |
| `dataObjectId` | `string` Output only. The id of the dataObject.                                                                                                                                                                                                                                                                                                                                                                               |
| `createTime`   | `string ( `[`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp)` format)` Output only. Timestamp the dataObject was created at. Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` .   |
| `updateTime`   | `string ( `[`Timestamp`](https://protobuf.dev/reference/protobuf/google.protobuf/#timestamp)` format)` Output only. Timestamp the dataObject was last updated. Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `"2014-10-02T15:01:23Z"` , `"2014-10-02T15:01:23.045123456Z"` or `"2014-10-02T15:01:23+05:30"` . |
| `data`         | `object ( `[`Struct`](https://protobuf.dev/reference/protobuf/google.protobuf/#struct)` format)` Optional. The data of the dataObject.                                                                                                                                                                                                                                                                                        |
| `vectors`      | `map (key: string, value: object ( `[`Vector`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/mcp/tools_list/get_data_object#Output.Schema.Vector)` ))` Optional. The vectors of the dataObject. An object containing a list of `"key": value` pairs. Example: `{ "name": "wrench", "mass": "1.3kg", "count": "3" }` .                                                        |
| `etag`         | `string` Optional. The etag of the dataObject.                                                                                                                                                                                                                                                                                                                                                                                |

### Timestamp

**JSON representation**

```
{
  "seconds": string,
  "nanos": integer
}
```

| Fields    |                                                                                                                                                                                                                                                                                                                      |
|-----------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `seconds` | `string ( `[`int64`](https://developers.google.com/discovery/v1/type-format)` format)` Represents seconds of UTC time since Unix epoch 1970-01-01T00:00:00Z. Must be between -62135596800 and 253402300799 inclusive (which corresponds to 0001-01-01T00:00:00Z to 9999-12-31T23:59:59Z).                            |
| `nanos`   | `integer` Non-negative fractions of a second at nanosecond resolution. This field is the nanosecond portion of the duration, not an alternative to seconds. Negative second values with fractions must still have non-negative nanos values that count forward in time. Must be between 0 and 999,999,999 inclusive. |

### Struct

**JSON representation**

```
{
  "fields": {
    string: value,
    ...
  }
}
```

| Fields   |                                                                                                                                                                                                                                                                                          |
|----------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `fields` | `map (key: string, value: value ( `[`Value`](https://protobuf.dev/reference/protobuf/google.protobuf/#value)` format))` Unordered map of dynamically typed values. An object containing a list of `"key": value` pairs. Example: `{ "name": "wrench", "mass": "1.3kg", "count": "3" }` . |

### FieldsEntry

**JSON representation**

```
{
  "key": string,
  "value": value
}
```

| Fields  |                                                                                               |
|---------|-----------------------------------------------------------------------------------------------|
| `key`   | `string`                                                                                      |
| `value` | `value ( `[`Value`](https://protobuf.dev/reference/protobuf/google.protobuf/#value)` format)` |

### Value

**JSON representation**

```
{

  // Union field kind can be only one of the following:
  "nullValue": null,
  "numberValue": number,
  "stringValue": string,
  "boolValue": boolean,
  "structValue": {
    object
  },
  "listValue": array
  // End of list of possible types for union field kind.
}
```

| Fields                                                                           |                                                                                                                                                                                                                                                |
|----------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Union field `kind` . The kind of value. `kind` can be only one of the following: |                                                                                                                                                                                                                                                |
| `nullValue`                                                                      | `null` Represents a JSON `null` .                                                                                                                                                                                                              |
| `numberValue`                                                                    | `number` Represents a JSON number. Must not be `NaN` , `Infinity` or `-Infinity` , since those are not supported in JSON. This also cannot represent large Int64 values, since JSON format generally does not support them in its number type. |
| `stringValue`                                                                    | `string` Represents a JSON string.                                                                                                                                                                                                             |
| `boolValue`                                                                      | `boolean` Represents a JSON boolean ( `true` or `false` literal in JSON).                                                                                                                                                                      |
| `structValue`                                                                    | `object ( `[`Struct`](https://protobuf.dev/reference/protobuf/google.protobuf/#struct)` format)` Represents a JSON object.                                                                                                                     |
| `listValue`                                                                      | `array ( `[`ListValue`](https://protobuf.dev/reference/protobuf/google.protobuf/#list-value)` format)` Represents a JSON array.                                                                                                                |
|                                                                                  |                                                                                                                                                                                                                                                |

### ListValue

**JSON representation**

```
{
  "values": [
    value
  ]
}
```

| Fields     |                                                                                                                                           |
|------------|-------------------------------------------------------------------------------------------------------------------------------------------|
| `values[]` | `value ( `[`Value`](https://protobuf.dev/reference/protobuf/google.protobuf/#value)` format)` Repeated field of dynamically typed values. |

### VectorsEntry

**JSON representation**

```
{
  "key": string,
  "value": {
    object (Vector)
  }
}
```

| Fields  |                                                                                                                                                                               |
|---------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `key`   | `string`                                                                                                                                                                      |
| `value` | `object ( `[`Vector`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/mcp/tools_list/get_data_object#Output.Schema.Vector)` )` |

### Vector

**JSON representation**

```
{

  // Union field vector_type can be only one of the following:
  "dense": {
    object (DenseVector)
  },
  "sparse": {
    object (SparseVector)
  }
  // End of list of possible types for union field vector_type.
}
```

| Fields                                                                                              |                                                                                                                                                                                                            |
|-----------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Union field `vector_type` . The type of the vector. `vector_type` can be only one of the following: |                                                                                                                                                                                                            |
| `dense`                                                                                             | `object ( `[`DenseVector`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/mcp/tools_list/get_data_object#Output.Schema.DenseVector)` )` A dense vector.    |
| `sparse`                                                                                            | `object ( `[`SparseVector`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/mcp/tools_list/get_data_object#Output.Schema.SparseVector)` )` A sparse vector. |
|                                                                                                     |                                                                                                                                                                                                            |

### DenseVector

**JSON representation**

```
{
  "values": [
    number
  ]
}
```

| Fields     |                                              |
|------------|----------------------------------------------|
| `values[]` | `number` Required. The values of the vector. |

### SparseVector

**JSON representation**

```
{
  "values": [
    number
  ],
  "indices": [
    integer
  ]
}
```

| Fields      |                                                               |
|-------------|---------------------------------------------------------------|
| `values[]`  | `number` Required. The values of the vector.                  |
| `indices[]` | `integer` Required. The corresponding indices for the values. |

### NullValue

Represents a JSON `null` .

`NullValue` is a sentinel, using an enum with only one value to represent the null value for the `Value` type union.

A field of type `NullValue` with any value other than `0` is considered invalid. Most ProtoJSON serializers will emit a `Value` with a `null_value` set as a JSON `null` regardless of the integer value, and so will round trip to a `0` value.

| Enums        |             |
|--------------|-------------|
| `NULL_VALUE` | Null value. |

### Tool Annotations

[Tool annotations](https://modelcontextprotocol.io/specification/latest/schema#toolannotations) are sent to MCP clients to describe the basic risk of a given tool. Most clients treat these hints as untrusted, but they can be used to decide when a confirmation prompt might be sent to a user.

Along with the title string, the following boolean hints are defined as follows:

- `readOnlyHint` : If true, the tool doesn't modify its environment. Default: false.
- `destructiveHint` : If true, then the tool can perform destructive actions. If false, then the tool can only perform additive actions. Default: true.
- `idempotentHint` : If true, then calling the tool repeatedly with the same arguments will have no additional effect on its environment. Default: false.
- `openWorldHint` : If true, then the tool can interact with an 'open world' of external entities. If false, then the tool can only interact with internal entities. For example, a web search tool would be open world, while a memory tool would not be open world.

Destructive Hint: ❌ \| Idempotent Hint: ✅ \| Read Only Hint: ✅ \| Open World Hint: ❌
