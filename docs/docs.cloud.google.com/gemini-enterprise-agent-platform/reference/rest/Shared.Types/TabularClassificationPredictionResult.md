---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/TabularClassificationPredictionResult
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/TabularClassificationPredictionResult
title: TabularClassificationPredictionResult
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Prediction output format for Tabular Classification.

Fields

`classes[]` `string`

The name of the classes being classified, contains all possible values of the target column.

`scores[]` `number`

The model's confidence in each class being correct, higher value means higher confidence. The N-th score corresponds to the N-th class in classes.

**JSON representation**

```
{
  "classes": [
    string
  ],
  "scores": [
    number
  ]
}
```
