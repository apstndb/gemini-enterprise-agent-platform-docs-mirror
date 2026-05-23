---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/PipelineState
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/PipelineState
title: PipelineState
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Describes the state of a pipeline.

Enums

`PIPELINE_STATE_UNSPECIFIED`

The pipeline state is unspecified.

`PIPELINE_STATE_QUEUED`

The pipeline has been created or resumed, and processing has not yet begun.

`PIPELINE_STATE_PENDING`

The service is preparing to run the pipeline.

`PIPELINE_STATE_RUNNING`

The pipeline is in progress.

`PIPELINE_STATE_SUCCEEDED`

The pipeline completed successfully.

`PIPELINE_STATE_FAILED`

The pipeline failed.

`PIPELINE_STATE_CANCELLING`

The pipeline is being cancelled. From this state, the pipeline may only go to either PIPELINE\_STATE\_SUCCEEDED, PIPELINE\_STATE\_FAILED or PIPELINE\_STATE\_CANCELLED.

`PIPELINE_STATE_CANCELLED`

The pipeline has been cancelled.

`PIPELINE_STATE_PAUSED`

The pipeline has been stopped, and can be resumed.
