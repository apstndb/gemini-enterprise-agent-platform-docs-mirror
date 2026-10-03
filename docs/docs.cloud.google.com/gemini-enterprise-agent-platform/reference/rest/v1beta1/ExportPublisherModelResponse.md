---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/ExportPublisherModelResponse
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/ExportPublisherModelResponse
title: ExportPublisherModelResponse
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Response message for [`ModelGardenService.ExportPublisherModel`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.publishers.models/export#google.cloud.aiplatform.v1beta1.ModelGardenService.ExportPublisherModel) .

Fields

`publisherModel` `string`

The name of the PublisherModel resource. Format: `publishers/{publisher}/models/{publisherModel}@{versionId}`

`destinationUri` `string`

The destination uri of the model weights.

**JSON representation**

```
{
  "publisherModel": string,
  "destinationUri": string
}
```
