---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/ExamplesArrayFilter
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/ExamplesArrayFilter
title: ExamplesArrayFilter
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Filters for examples' array metadata fields. An array field is example metadata where multiple values are attributed to a single example.

Fields

`values[]` `string`

Required. The values by which to filter examples.

`arrayOperator` `enum ( `[`ArrayOperator`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/ExamplesArrayFilter#ArrayOperator)` )`

Required. The operator logic to use for filtering.

**JSON representation**

```
{
  "values": [
    string
  ],
  "arrayOperator": enum (ArrayOperator)
}
```

## ArrayOperator

The logic to use for filtering.

| Enums                        |                                                                                  |
|------------------------------|----------------------------------------------------------------------------------|
| `ARRAY_OPERATOR_UNSPECIFIED` | Not specified. This value should not be used.                                    |
| `CONTAINS_ANY`               | The metadata array field in the example must contain at least one of the values. |
| `CONTAINS_ALL`               | The metadata array field in the example must contain all of the values.          |
