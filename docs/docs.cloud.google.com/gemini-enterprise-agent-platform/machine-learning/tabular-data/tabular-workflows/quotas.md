---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tabular-data/tabular-workflows/quotas
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tabular-data/tabular-workflows/quotas
title: Manage quotas for Tabular Workflows
description: Review quotas and limits for Tabular Workflows.
data_source: docs.cloud.google.com
---

If you receive a quota-related error while running the Tabular Workflow for End-to-End AutoML, request a higher quota. To learn more, see [View and manage quotas](https://docs.cloud.google.com/docs/quotas/view-manage) .

The following table shows our recommended quota values. We recommend setting the quota values as a function of the number of concurrent training jobs ( `num_concurrent_pipeline` ) and the number of CPUs in the requested region. The recommended values are valid only if you use the default Compute Engine resource configuration for your workflow.

| Service            | Quota                                                                       | Recommendation                                  |
| ------------------ | --------------------------------------------------------------------------- | ----------------------------------------------- |
| Compute Engine API | CPUs                                                                        | `num_concurrent_pipeline` x 440 CPUs            |
| Compute Engine API | Persistent Disk Standard (GB)                                               | `num_concurrent_pipeline` x 5TB persistent disk |
| Agent Platform API | Restricted image training CPUs for N1/E2 machine types per region           | `num_concurrent_pipeline` x 440 CPUs            |
| Agent Platform API | Restricted image training total persistent disk SSD storage (GB) per region | `num_concurrent_pipeline` x 8TB persistent disk |
| Agent Platform API | Resource management (CRUD) requests per minute per region                   | `num_concurrent_pipeline` x 150                 |
| Agent Platform API | Job or LRO submission requests per minute per region                        | `num_concurrent_pipeline` x 6                   |

## What's next

  - [Train a model using End-to-End AutoML](https://docs.cloud.google.com/vertex-ai/docs/tabular-data/tabular-workflows/e2e-automl-train) .
