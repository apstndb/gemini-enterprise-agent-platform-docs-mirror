---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/UpgradeNotebookRuntimeOperationMetadata
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/UpgradeNotebookRuntimeOperationMetadata
title: UpgradeNotebookRuntimeOperationMetadata
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

metadata information for [`NotebookService.UpgradeNotebookRuntime`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.notebookRuntimes/upgrade#google.cloud.aiplatform.v1beta1.NotebookService.UpgradeNotebookRuntime) .

Fields

`genericMetadata` `object ( `[`GenericOperationMetadata`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/GenericOperationMetadata)` )`

The operation generic information.

`progressMessage` `string`

A human-readable message that shows the intermediate progress details of NotebookRuntime.

**JSON representation**

```
{
  "genericMetadata": {
    object (GenericOperationMetadata)
  },
  "progressMessage": string
}
```
