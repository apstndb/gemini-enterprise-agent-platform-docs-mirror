---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/TftFeatureImportance
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/TftFeatureImportance
title: TftFeatureImportance
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Fields

`contextWeights[]` `number`

TFT feature importance values. Each pair for {context/horizon/attribute} should have the same shape since the weight corresponds to the column names.

`contextColumns[]` `string`

`horizonWeights[]` `number`

`horizonColumns[]` `string`

`attributeWeights[]` `number`

`attributeColumns[]` `string`

**JSON representation**

```
{
  "contextWeights": [
    number
  ],
  "contextColumns": [
    string
  ],
  "horizonWeights": [
    number
  ],
  "horizonColumns": [
    string
  ],
  "attributeWeights": [
    number
  ],
  "attributeColumns": [
    string
  ]
}
```
