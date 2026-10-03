---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/CustomTask
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/CustomTask
title: CustomTask
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

A TrainingJob that trains a custom code Model.

Fields

`inputs` `object ( `[`CustomJobSpec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/CustomJobSpec)` )`

The input parameters of this CustomTask.

`metadata` `object ( `[`CustomJobMetadata`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/Shared.Types/CustomJobMetadata)` )`

The metadata information.

**JSON representation**

```
{
  "inputs": {
    object (CustomJobSpec)
  },
  "metadata": {
    object (CustomJobMetadata)
  }
}
```
