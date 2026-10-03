---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/GenerateVideoResponse
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/GenerateVideoResponse
title: GenerateVideoResponse
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Generate video response.

Fields

`generatedSamples[] `**`(deprecated)`** `string`

> This item is deprecated!

The cloud storage uris of the generated videos.

`raiMediaFilteredReasons[]` `string`

Returns rai failure reasons if any.

`raiMediaFilteredCount` `integer`

Returns if any videos were filtered due to RAI policies.

**JSON representation**

```
{
  "generatedSamples": [
    string
  ],
  "raiMediaFilteredReasons": [
    string
  ],
  "raiMediaFilteredCount": integer
}
```
