---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/SimpleRetrievalParams
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/SimpleRetrievalParams
title: SimpleRetrievalParams
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Parameters for simple (non-similarity search) retrieval.

Fields

`pageSize` `integer`

Optional. The maximum number of memories to return. The service may return fewer than this value. If unspecified, at most 3 memories will be returned. The maximum value is 100; values above 100 will be coerced to 100.

`pageToken` `string`

Optional. A page token, received from a previous `RetrieveMemories` call. Provide this to retrieve the subsequent page.

**JSON representation**

```
{
  "pageSize": integer,
  "pageToken": string
}
```
