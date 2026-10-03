---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/ExportDataResponse
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/ExportDataResponse
title: ExportDataResponse
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Response message for [`DatasetService.ExportData`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.datasets/export#google.cloud.aiplatform.v1.DatasetService.ExportData) .

Fields

`exportedFiles[]` `string`

All of the files that are exported in this export operation. For custom code training export, only three (training, validation and test) Cloud Storage paths in wildcard format are populated (for example, gs://.../training-\*).

`dataStats` `object ( `[`DataStats`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.models#Model.DataStats)` )`

Only present for custom code training export use case. Records data stats, i.e., train/validation/test item/annotation counts calculated during the export operation.

**JSON representation**

```
{
  "exportedFiles": [
    string
  ],
  "dataStats": {
    object (DataStats)
  }
}
```
