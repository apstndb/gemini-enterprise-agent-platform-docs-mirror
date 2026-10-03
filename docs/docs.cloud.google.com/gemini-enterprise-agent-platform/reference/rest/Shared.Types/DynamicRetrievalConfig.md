---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/DynamicRetrievalConfig
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/DynamicRetrievalConfig
title: DynamicRetrievalConfig
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Describes the options to customize dynamic retrieval.

Fields

`mode` `enum ( `[`Mode`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/Mode)` )`

The mode of the predictor to be used in dynamic retrieval.

`dynamicThreshold` `number`

Optional. The threshold to be used in dynamic retrieval. If not set, a system default value is used.

**JSON representation**

```
{
  "mode": enum (Mode),
  "dynamicThreshold": number
}
```
