---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/BatchCancelPipelineJobsResponse
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/BatchCancelPipelineJobsResponse
title: BatchCancelPipelineJobsResponse
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Response message for [`PipelineService.BatchCancelPipelineJobs`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.pipelineJobs/batchCancel#google.cloud.aiplatform.v1beta1.PipelineService.BatchCancelPipelineJobs) .

Fields

`pipelineJobs[]` `object ( `[`PipelineJob`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.pipelineJobs#PipelineJob)` )`

PipelineJobs cancelled.

**JSON representation**

```
{
  "pipelineJobs": [
    {
      object (PipelineJob)
    }
  ]
}
```
