---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/LineageSubgraph
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/LineageSubgraph
title: LineageSubgraph
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

A subgraph of the overall lineage graph. Event edges connect Artifact and Execution nodes.

Fields

`artifacts[]` `object ( `[`Artifact`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.metadataStores.artifacts#Artifact)` )`

The Artifact nodes in the subgraph.

`executions[]` `object ( `[`Execution`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.metadataStores.executions#Execution)` )`

The Execution nodes in the subgraph.

`events[]` `object ( `[`Event`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/Event)` )`

The Event edges between Artifacts and Executions in the subgraph.

**JSON representation**

```
{
  "artifacts": [
    {
      object (Artifact)
    }
  ],
  "executions": [
    {
      object (Execution)
    }
  ],
  "events": [
    {
      object (Event)
    }
  ]
}
```
