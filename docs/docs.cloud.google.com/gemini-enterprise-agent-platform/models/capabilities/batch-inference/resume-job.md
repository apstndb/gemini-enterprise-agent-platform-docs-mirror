---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/models/capabilities/batch-inference/resume-job
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/capabilities/batch-inference/resume-job
title: Resume an incomplete batch inference job
description: Learn how to resume batch inference jobs with Gemini models.
data_source: docs.cloud.google.com
---

If an Agent Platform batch inference job fails, is canceled, or expires, you can resume it by creating a new batch job. The new job processes only the incomplete or failed requests from the previous job and merges the new results with those from the previously completed requests. For example, if the incomplete batch job was 90% complete, the new job processes the remaining 10% of the requests.

To resume a batch job, create a new batch job, supplying the [Cloud Storage file](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/capabilities/batch-inference/new-job-from-cloud-storage) or [BigQuery table output](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/capabilities/batch-inference/new-job-from-bigquery) as input to the new job.

> **Note:** In rare cases where users modify the output file of the job before resuming, the system resumes from the modified output file. The system doesn't validate whether the output file has been modified.

## What's next

  - Learn more about [Batch inference from Cloud Storage](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/capabilities/batch-inference/new-job-from-cloud-storage) .
  - Learn more about [Batch inference for BigQuery](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/capabilities/batch-inference/new-job-from-bigquery) .
