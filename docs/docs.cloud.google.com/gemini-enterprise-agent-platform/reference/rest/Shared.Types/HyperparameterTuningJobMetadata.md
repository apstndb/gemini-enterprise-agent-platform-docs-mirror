---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/HyperparameterTuningJobMetadata
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/HyperparameterTuningJobMetadata
title: HyperparameterTuningJobMetadata
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Fields

`backingHyperparameterTuningJob` `string`

The resource name of the HyperparameterTuningJob that has been created to carry out this HyperparameterTuning task.

`bestTrialBackingCustomJob` `string`

The resource name of the CustomJob that has been created to run the best Trial of this HyperparameterTuning task.

**JSON representation**

```
{
  "backingHyperparameterTuningJob": string,
  "bestTrialBackingCustomJob": string
}
```
