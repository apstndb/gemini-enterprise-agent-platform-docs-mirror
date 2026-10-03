---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/UploadModelResponse
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/UploadModelResponse
title: UploadModelResponse
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Response message of [`ModelService.UploadModel`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.models/upload#google.cloud.aiplatform.v1beta1.ModelService.UploadModel) operation.

Fields

`model` `string`

The name of the uploaded Model resource. Format: `projects/{project}/locations/{location}/models/{model}`

`modelVersionId` `string`

Output only. The version id of the model that is uploaded.

**JSON representation**

```
{
  "model": string,
  "modelVersionId": string
}
```
