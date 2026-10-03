---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/DeployResponse
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/DeployResponse
title: DeployResponse
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Response message for [`ModelGardenService.Deploy`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations/deploy#google.cloud.aiplatform.v1.ModelGardenService.Deploy) .

Fields

`publisherModel` `string`

Output only. The name of the PublisherModel resource. Format: `publishers/{publisher}/models/{publisherModel}@{versionId}` , or `publishers/hf-{hugging-face-author}/models/{hugging-face-model-name}@001`

`endpoint` `string`

Output only. The name of the Endpoint created. Format: `projects/{project}/locations/{location}/endpoints/{endpoint}`

`model` `string`

Output only. The name of the Model created. Format: `projects/{project}/locations/{location}/models/{model}`

**JSON representation**

```
{
  "publisherModel": string,
  "endpoint": string,
  "model": string
}
```
