---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/govern/topology
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/topology
title: Agent topology graphs
description: Learn about viewing agent topologies to help you govern and monitor agents.
data_source: docs.cloud.google.com
---

To support AI application governance, configuration validation, and dependency analysis, you can run queries that correlate agent data with other Google Cloud data and display the results as a topology graph.

There are two ways to view a topology:

  - View topologies for [an agent](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/topology/view-agent-registry-topology) - In Agent Registry, you can run predefined queries to show traffic to and from a selected agent.
  - View topologies for a [project](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/topology/view-project-topology) - The **Topology** page provides full query capabilities. You can run predefined queries or use a visual query builder to create your own queries.

The App Topology API provides these topology graph capabilities in Gemini Enterprise Agent Platform. To learn about using the App Topology MCP server and viewing topology graphs in other products, see the [App Topology documentation](https://docs.cloud.google.com/app-topology) .

> **Note:** On October 15, 2026, the App Topology API transitions to a usage-based billing model that includes a daily free data usage allotment. For more information, see [App Topology pricing](https://docs.cloud.google.com/hub/docs/app-topology#pricing) .

### Limitations

Data availability:

  - Trace connections show latency and error rate information from the most recent hour of data. You can't change the time range.
  - When you delete a Developer Connect insights event, the event might still appear in App Topology query results for a few days.
  - Query results only include components that meet the following criteria:
      - Agents must have [functional type](https://docs.cloud.google.com/app-hub/docs/reference/rest/v1/FunctionalType) set to `AGENT` and be deployed using ADK, Gemini Enterprise, or Cloud Run; or be deployed using GKE and registered with [Agent Registry](https://docs.cloud.google.com/agent-registry/overview) .
      - MCP servers must have [functional type](https://docs.cloud.google.com/app-hub/docs/reference/rest/v1/FunctionalType) set to `MCP` . First-party MCP servers deployed using OneMCP, GKE, or Cloud Run are included. Other MCP servers must be registered with [Agent Registry](https://docs.cloud.google.com/agent-registry/overview) to be included.
      - Other components, such as tools and models, or Workspace Agents aren't included in results.
  - When an MCP server is registered to Agent Registry, it is classified as a shared resource by App Hub which won't show edges to other nodes in the topology graph. This limitation only applies if the MCP server is classified as a shared resource and doesn't apply to application-exclusive resources, such as Gemini Enterprise data connectors or MCP servers hosted on Cloud Run.
  - For security and compliance data provided by Security Command Center:
      - The provided data is in [Preview](https://cloud.google.com/products#product-launch-stages)
      - Data is only available for projects and applications in a Google Cloud organization.

## What's next

  - [View topologies for a project](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/topology/view-project-topology) .
  - [View traffic to and from an agent](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/topology/view-agent-registry-topology) .
