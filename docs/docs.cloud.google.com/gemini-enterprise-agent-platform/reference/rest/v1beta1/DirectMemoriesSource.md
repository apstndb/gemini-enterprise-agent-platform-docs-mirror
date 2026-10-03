---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/DirectMemoriesSource
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/DirectMemoriesSource
title: DirectMemoriesSource
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Defines a direct source of memories that should be uploaded to Memory Bank with consolidation.

Fields

`directMemories[]` `object ( `[`DirectMemory`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/DirectMemoriesSource#DirectMemory)` )`

Required. The direct memories to upload to Memory Bank. At most 5 direct memories are allowed per request.

**JSON representation**

```
{
  "directMemories": [
    {
      object (DirectMemory)
    }
  ]
}
```

## DirectMemory

A direct memory to upload to Memory Bank.

Fields

`fact` `string`

Required. The fact to consolidate with existing memories.

**JSON representation**

```
{
  "fact": string
}
```
