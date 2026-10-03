---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/rest/v1/SearchHint
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/rest/v1/SearchHint
title: SearchHint
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Represents a hint to the search index engine.

**JSON representation**

```
{

  // The following is a list of mutually exclusive fields. At most one of the
  // fields will be set in a response:
  "knnHint": {
    object (KnnHint)
  },
  "indexHint": {
    object (IndexHint)
  }
  // End of mutually exclusive fields.
}
```

| Fields                                                                                                                               |                                                                                                                                                                                                                                                         |
|--------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| The type of index to use. The following is a list of mutually exclusive fields. At most one of the fields will be set in a response: |                                                                                                                                                                                                                                                         |
| `knnHint`                                                                                                                            | `object ( `[`KnnHint`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/rest/v1/SearchHint#KnnHint)` )` Optional. If set, the search will use the system's default K-Nearest Neighbor (KNN) index engine. |
| `indexHint`                                                                                                                          | `object ( `[`IndexHint`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/rest/v1/SearchHint#IndexHint)` )` Optional. Specifies that the search should use a particular index.                            |
| End of mutually exclusive fields.                                                                                                    |                                                                                                                                                                                                                                                         |

## KnnHint

This type has no fields.

KnnHint will be used if search should be explicitly done on system's default K-Nearest Neighbor (KNN) index engine.

## IndexHint

Message to specify the index to use for the search.

**JSON representation**

```
{
  "name": string,

  // The following is a list of mutually exclusive fields. At most one of the
  // fields will be set in a response:
  "denseScannParams": {
    object (DenseScannParams)
  }
  // End of mutually exclusive fields.
}
```

| Fields                                                                                                                                   |                                                                                                                                                                                                                                      |
|------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `name`                                                                                                                                   | `string` Required. The resource name of the index to use for the search. The index must be in the same project, location, and collection. Format: `projects/{project}/locations/{location}/collections/{collection}/indexes/{index}` |
| The parameters for the index. The following is a list of mutually exclusive fields. At most one of the fields will be set in a response: |                                                                                                                                                                                                                                      |
| `denseScannParams`                                                                                                                       | `object ( `[`DenseScannParams`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/rest/v1/SearchHint#DenseScannParams)` )` Optional. Dense ScaNN parameters.                            |
| End of mutually exclusive fields.                                                                                                        |                                                                                                                                                                                                                                      |

## DenseScannParams

Parameters for dense ScaNN.

**JSON representation**

```
{
  "targetRecall": number
}
```

| Fields         |                                                                                                                                                                           |
|----------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `targetRecall` | `number` Optional. The target recall for the search. Must be a double in the range \[0, 1\]. While the search aims to achieve this level of recall, it is not guaranteed. |
