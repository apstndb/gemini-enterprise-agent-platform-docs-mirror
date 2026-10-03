---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/HyperparameterTuningTask
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/HyperparameterTuningTask
title: HyperparameterTuningTask
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

A TrainingJob that tunes Hypererparameters of a custom code Model.

Fields

`inputs` `object ( `[`HyperparameterTuningJobSpec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/HyperparameterTuningJobSpec)` )`

The input parameters of this HyperparameterTuningTask.

`metadata` `object ( `[`HyperparameterTuningJobMetadata`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/HyperparameterTuningJobMetadata)` )`

The metadata information.

**JSON representation**

```
{
  "inputs": {
    object (HyperparameterTuningJobSpec)
  },
  "metadata": {
    object (HyperparameterTuningJobMetadata)
  }
}
```
