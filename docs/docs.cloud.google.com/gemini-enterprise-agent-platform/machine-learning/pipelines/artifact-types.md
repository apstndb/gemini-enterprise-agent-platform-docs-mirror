---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/pipelines/artifact-types
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/pipelines/artifact-types
title: ML metadata artifact types
description: Learn about artifact types in Gemini Enterprise Agent Platform Pipelines and their role in tracking ML metadata.
data_source: docs.cloud.google.com
---

For the purpose of tracking resources and for functionality across the Google Cloud Pipeline Components, a set of standard Vertex ML Metadata artifact types are defined. These first-party artifacts types are defined by Google Cloud Pipeline Components.

| Artifact type                     | Description                                                                                                                                                                                                          |
| --------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `google.VertexModel`              | An artifact representing a Gemini Enterprise Agent Platform [`Model`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.models) resource                           |
| `google.VertexEndpoint`           | An artifact representing a Gemini Enterprise Agent Platform [`Endpoint`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.endpoints) resource                     |
| `google.VertexBatchPredictionJob` | An artifact representing a Gemini Enterprise Agent Platform [`BatchPredictionJob`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.batchPredictionJobs) resource |
| `google.VertexDataset`            | An artifact representing a Gemini Enterprise Agent Platform [`Dataset`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.datasets) resource                       |
| `google.BQMLModel`                | An artifact representing a BigQuery ML [`Model`](https://docs.cloud.google.com/bigquery/docs/reference/rest/v2/models) resource                                                                                      |
| `google.BQTable`                  | An artifact representing a BigQuery [`Table`](https://docs.cloud.google.com/bigquery/docs/reference/rest/v2/tables) resource                                                                                         |
| `google.UnmanagedContainerModel`  | An artifact representing an [`UnmanagedContainerModel`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.batchPredictionJobs#unmanagedcontainermodel) resource    |

For more information about using ML metadata artifacts, see [Consume or produce artifacts in your component](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/pipelines/use-components#consume_or_produce_artifacts_in_your_component) .
