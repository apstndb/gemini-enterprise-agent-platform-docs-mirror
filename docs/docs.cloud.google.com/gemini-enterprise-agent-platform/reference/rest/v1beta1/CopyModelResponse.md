---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/CopyModelResponse
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/CopyModelResponse
title: CopyModelResponse
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Response message of [`ModelService.CopyModel`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.models/copy#google.cloud.aiplatform.v1beta1.ModelService.CopyModel) operation.

Fields

`model` `string`

The name of the copied Model resource. Format: `projects/{project}/locations/{location}/models/{model}`

`modelVersionId` `string`

Output only. The version id of the model that is copied.

**JSON representation**

```
{
  "model": string,
  "modelVersionId": string
}
```
