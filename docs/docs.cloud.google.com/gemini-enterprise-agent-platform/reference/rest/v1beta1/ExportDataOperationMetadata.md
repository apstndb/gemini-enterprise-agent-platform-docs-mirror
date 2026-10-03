---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/ExportDataOperationMetadata
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/ExportDataOperationMetadata
title: ExportDataOperationMetadata
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Runtime operation information for [`DatasetService.ExportData`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.datasets/export#google.cloud.aiplatform.v1beta1.DatasetService.ExportData) .

Fields

`genericMetadata` `object ( `[`GenericOperationMetadata`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/GenericOperationMetadata)` )`

The common part of the operation metadata.

`gcsOutputDirectory` `string`

A Google Cloud Storage directory which path ends with '/'. The exported data is stored in the directory.

**JSON representation**

```
{
  "genericMetadata": {
    object (GenericOperationMetadata)
  },
  "gcsOutputDirectory": string
}
```
