---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/ExportModelOperationMetadata
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/ExportModelOperationMetadata
title: ExportModelOperationMetadata
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Details of [`ModelService.ExportModel`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.models/export#google.cloud.aiplatform.v1.ModelService.ExportModel) operation.

Fields

`genericMetadata` `object ( `[`GenericOperationMetadata`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/GenericOperationMetadata)` )`

The common part of the operation metadata.

`outputInfo` `object ( `[`OutputInfo`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/ExportModelOperationMetadata#OutputInfo)` )`

Output only. Information further describing the output of this Model export.

**JSON representation**

```
{
  "genericMetadata": {
    object (GenericOperationMetadata)
  },
  "outputInfo": {
    object (OutputInfo)
  }
}
```

## OutputInfo

Further describes the output of the ExportModel. Supplements [`ExportModelRequest.OutputConfig`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.models/export#OutputConfig) .

Fields

`artifactOutputUri` `string`

Output only. If the Model artifact is being exported to Google Cloud Storage this is the full path of the directory created, into which the Model files are being written to.

`imageOutputUri` `string`

Output only. If the Model image is being exported to Google Artifact Registry this is the full path of the image created.

**JSON representation**

```
{
  "artifactOutputUri": string,
  "imageOutputUri": string
}
```
