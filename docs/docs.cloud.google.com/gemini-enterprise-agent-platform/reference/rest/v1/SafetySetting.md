---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/SafetySetting
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/SafetySetting
title: SafetySetting
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

A safety setting that affects the safety-blocking behavior.

A `SafetySetting` consists of a harm `category` and a `threshold` for that category.

Fields

`category` `enum ( `[`HarmCategory`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/HarmCategory)` )`

Required. The harm category to be blocked.

`threshold` `enum ( `[`HarmBlockThreshold`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/HarmBlockThreshold)` )`

Required. The threshold for blocking content. If the harm probability exceeds this threshold, the content will be blocked.

`method` `enum ( `[`HarmBlockMethod`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/SafetySetting#HarmBlockMethod)` )`

Optional. The method for blocking content. If not specified, the default behavior is to use the probability score.

**JSON representation**

```
{
  "category": enum (HarmCategory),
  "threshold": enum (HarmBlockThreshold),
  "method": enum (HarmBlockMethod)
}
```

## HarmBlockMethod

The method for blocking content.

| Enums                           |                                                                  |
|---------------------------------|------------------------------------------------------------------|
| `HARM_BLOCK_METHOD_UNSPECIFIED` | The harm block method is unspecified.                            |
| `SEVERITY`                      | The harm block method uses both probability and severity scores. |
| `PROBABILITY`                   | The harm block method uses the probability score.                |
