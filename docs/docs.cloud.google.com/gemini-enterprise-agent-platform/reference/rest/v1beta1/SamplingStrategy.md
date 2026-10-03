---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/SamplingStrategy
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/SamplingStrategy
title: SamplingStrategy
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Sampling Strategy for logging, can be for both training and prediction dataset.

Fields

`randomSampleConfig` `object ( `[`RandomSampleConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/SamplingStrategy#RandomSampleConfig)` )`

Random sample config. Will support more sampling strategies later.

**JSON representation**

```
{
  "randomSampleConfig": {
    object (RandomSampleConfig)
  }
}
```

## RandomSampleConfig

Requests are randomly selected.

Fields

`sampleRate` `number`

Sample rate (0, 1\]

**JSON representation**

```
{
  "sampleRate": number
}
```
