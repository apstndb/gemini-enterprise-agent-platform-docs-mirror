---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/rest/v1/OutputFields
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/reference/rest/v1/OutputFields
title: OutputFields
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Defines a output fields struct for data in DataObject.

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

| Fields             |                                                                                      |
|--------------------|--------------------------------------------------------------------------------------|
| `dataFields[]`     | `string` Optional. The fields from the data fields to include in the output.         |
| `vectorFields[]`   | `string` Optional. The fields from the vector fields to include in the output.       |
| `metadataFields[]` | `string` Optional. The fields from the DataObject metadata to include in the output. |
