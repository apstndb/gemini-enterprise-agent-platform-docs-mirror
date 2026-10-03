---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/StreamingPredictResponse
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/StreamingPredictResponse
title: StreamingPredictResponse
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Response message for `PredictionService.StreamingPredict` .

Fields

`outputs[]` `object ( `[`Tensor`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/Tensor)` )`

The prediction output.

`parameters` `object ( `[`Tensor`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/Tensor)` )`

The parameters that govern the prediction.

**JSON representation**

```
{
  "outputs": [
    {
      object (Tensor)
    }
  ],
  "parameters": {
    object (Tensor)
  }
}
```
