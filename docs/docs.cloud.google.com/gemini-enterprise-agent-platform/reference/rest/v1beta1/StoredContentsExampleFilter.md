---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/StoredContentsExampleFilter
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/StoredContentsExampleFilter
title: StoredContentsExampleFilter
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

The metadata filters that will be used to remove or fetch StoredContentsExamples. If a field is unspecified, then no filtering for that field will be applied.

Fields

`searchKeys[]` `string`

Optional. The search keys for filtering. Only examples with one of the specified search keys ( [`StoredContentsExample.search_key`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/Example#StoredContentsExample.FIELDS.search_key) ) are eligible to be returned.

`functionNames` `object ( `[`ExamplesArrayFilter`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/ExamplesArrayFilter)` )`

Optional. The function names for filtering.

**JSON representation**

```
{
  "searchKeys": [
    string
  ],
  "functionNames": {
    object (ExamplesArrayFilter)
  }
}
```
