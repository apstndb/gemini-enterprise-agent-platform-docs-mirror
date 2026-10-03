---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/BatchDeletePipelineJobsResponse
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/BatchDeletePipelineJobsResponse
title: BatchDeletePipelineJobsResponse
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Response message for [`PipelineService.BatchDeletePipelineJobs`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.pipelineJobs/batchDelete#google.cloud.aiplatform.v1beta1.PipelineService.BatchDeletePipelineJobs) .

Fields

`pipelineJobs[]` `object ( `[`PipelineJob`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.pipelineJobs#PipelineJob)` )`

PipelineJobs deleted.

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
