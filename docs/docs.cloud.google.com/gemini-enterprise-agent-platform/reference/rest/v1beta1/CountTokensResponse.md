---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/CountTokensResponse
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/CountTokensResponse
title: CountTokensResponse
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Response message for [`PredictionService.CountTokens`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.endpoints/countTokens#google.cloud.aiplatform.v1beta1.PredictionService.CountTokens) .

Fields

`totalTokens` `integer`

The total number of tokens counted across all instances from the request.

`totalBillableCharacters` `integer`

The total number of billable characters counted across all instances from the request.

`promptTokensDetails[]` `object ( `[`ModalityTokenCount`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/ModalityTokenCount)` )`

Output only. List of modalities that were processed in the request input.

**JSON representation**

```
{
  "totalTokens": integer,
  "totalBillableCharacters": integer,
  "promptTokensDetails": [
    {
      object (ModalityTokenCount)
    }
  ]
}
```
