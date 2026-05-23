---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/JobState
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/JobState
title: JobState
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Describes the state of a job.

Enums

`JOB_STATE_UNSPECIFIED`

The job state is unspecified.

`JOB_STATE_QUEUED`

The job has been just created or resumed and processing has not yet begun.

`JOB_STATE_PENDING`

The service is preparing to run the job.

`JOB_STATE_RUNNING`

The job is in progress.

`JOB_STATE_SUCCEEDED`

The job completed successfully.

`JOB_STATE_FAILED`

The job failed.

`JOB_STATE_CANCELLING`

The job is being cancelled. From this state the job may only go to either `JOB_STATE_SUCCEEDED` , `JOB_STATE_FAILED` or `JOB_STATE_CANCELLED` .

`JOB_STATE_CANCELLED`

The job has been cancelled.

`JOB_STATE_PAUSED`

The job has been stopped, and can be resumed.

`JOB_STATE_EXPIRED`

The job has expired.

`JOB_STATE_UPDATING`

The job is being updated. Only jobs in the `RUNNING` state can be updated. After updating, the job goes back to the `RUNNING` state.

`JOB_STATE_PARTIALLY_SUCCEEDED`

The job is partially succeeded, some results may be missing due to errors.
