---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/DirectContentsSource
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/DirectContentsSource
title: DirectContentsSource
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Defines a direct source of content from which to generate the memories.

Fields

`events[]` `object ( `[`Event`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/DirectContentsSource#Event)` )`

Required. The source content (i.e. chat history) to generate memories from.

**JSON representation**

```
{
  "events": [
    {
      object (Event)
    }
  ]
}
```

## Event

A single piece of conversation from which to generate memories.

Fields

`content` `object ( `[`Content`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/Content)` )`

Required. A single piece of content from which to generate memories.

**JSON representation**

```
{
  "content": {
    object (Content)
  }
}
```
