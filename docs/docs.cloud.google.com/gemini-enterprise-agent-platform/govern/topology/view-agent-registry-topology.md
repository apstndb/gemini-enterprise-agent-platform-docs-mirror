---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/govern/topology/view-agent-registry-topology
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/topology/view-agent-registry-topology
title: View topologies for an agent
description: Use topology graphs to analyze traffic to and from an agent.
data_source: docs.cloud.google.com
---

In [Agent Registry](https://docs.cloud.google.com/agent-registry/overview) you can view a topology graph that shows traffic to and from an agent or AI application. Analyzing the graph helps you to understand if the agent or AI application is communicating with trusted agents, MCP servers, and endpoints.

To get more insights about your agent resources, use the query builder to on the [Topology page](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/topology/view-project-topology) . You can visualize observability, security, software supply chain, and infrastructure resource data associated with your agents.

Some [limitations](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/topology#limitations) apply to topology data.

## Before you begin

These instructions assume that you have [set up Agent Registry](https://docs.cloud.google.com/agent-registry/setup) and registered your agent resources.

1.  To view agent traffic, [instrument your AI applications](https://docs.cloud.google.com/stackdriver/docs/instrumentation/ai-agent-overview) .

2.  Enable the App Hub, App Topology, Cloud Asset Inventory, and Observability APIs, if any are not already enabled.
    
    **Roles required to enable APIs**
    
    To enable APIs, you need the `serviceusage.services.enable` permission. If you created the project, then you likely already have this permission through the Owner role ( `roles/owner` ). Otherwise, you can get this permission through the Service Usage Admin role ( `roles/serviceusage.serviceUsageAdmin` ). [Learn how to grant roles](https://docs.cloud.google.com/iam/docs/granting-changing-revoking-access) .

3.  [Verify that billing is enabled for your Google Cloud project](https://docs.cloud.google.com/billing/docs/how-to/verify-billing-enabled#confirm_billing_is_enabled_on_a_project) .

4.  If you are protecting services in a VPC Service Controls perimeter, update the perimeter to include App Topology and services that provide underlying data. [Learn more](https://docs.cloud.google.com/app-topology/use-vpc-sc) .

### Required roles

To get the permissions that you need to view topology graphs in Agent Registry, ask your administrator to grant you the following IAM roles on the projects where you want to use App Topology:

  - [App Topology Viewer](https://docs.cloud.google.com/iam/docs/roles-permissions/apptopology#apptopology.viewer) ( `roles/apptopology.viewer` )
  - [Agent Registry API Viewer](https://docs.cloud.google.com/iam/docs/roles-permissions/agentregistry#agentregistry.viewer) ( `roles/agentregistry.viewer` )

For more information about granting roles, see [Manage access to projects, folders, and organizations](https://docs.cloud.google.com/iam/docs/granting-changing-revoking-access) .

These predefined roles contain the permissions required to view topology graphs in Agent Registry. To see the exact permissions that are required, expand the **Required permissions** section:

#### Required permissions

The following permissions are required to view topology graphs in Agent Registry:

  - Get discovered resource data: `apptopology.discoveredResourcesTopologies.generate`
  - Get resource data data: `apptopology.sreDomainTopologies.generate`

You might also be able to get these permissions with [custom roles](https://docs.cloud.google.com/iam/docs/creating-custom-roles) or other [predefined roles](https://docs.cloud.google.com/iam/docs/roles-overview#predefined) .

## View an agent topology

1.  In the Google Cloud console, go to the Agent Registry page.

2.  In the project picker, select the project that contains your agents.

3.  On the **Agents** tab, click the name of the agent that you want to view.

4.  Click the **Topology** tab.

5.  In the **Quick Queries** section, click a query. If there are results that match your query, the topology graph is displayed.

6.  Explore the topology graph. The graph shows resources that match your query and the relationships between them.
    
      - Icons represent nodes, discovered and registered resources and their resource type.
      - Lines represent connections, the relationships between nodes.
    
    ![An example topology graph with a selected node](https://docs.cloud.google.com/static/gemini-enterprise-agent-platform/images/topology-graph.png)
    
    You can interact with a topology in the following ways:
    
      - Change the visualization by zooming in or out or repositioning nodes.
      - View the label for a connection by hovering over the connection line between two nodes.
      - Get information about a node or connection by selecting it.
      - Hide or show the query panel by clicking **Toggle panel** first\_page .

To view additional data about the selected agent, view the dashboards in [Application Monitoring](https://docs.cloud.google.com/monitoring/docs/application-monitoring-ai-resources) .

## View an AI application topology

1.  In the Google Cloud console, go to the Agent Registry page.

2.  In the project picker, select the project that contains your AI application.

3.  On the **AI applications** tab, click the name of the agent that you want to view.

4.  Click the **Topology** tab.

5.  In the **Quick Queries** section, click a query. If there are results that match your query, the topology graph is displayed.

6.  Explore the topology graph. The graph shows resources that match your query and the relationships between them.
    
      - Icons represent nodes, discovered and registered resources and their resource type.
      - Lines represent connections, the relationships between nodes.
    
    ![An example topology graph with a selected node](https://docs.cloud.google.com/static/gemini-enterprise-agent-platform/images/topology-graph.png)
    
    You can interact with a topology in the following ways:
    
      - Change the visualization by zooming in or out or repositioning nodes.
      - View the label for a connection by hovering over the connection line between two nodes.
      - Get information about a node or connection by selecting it.
      - Hide or show the query panel by clicking **Toggle panel** first\_page .

To view additional data about the selected application, view the dashboards in [Application Monitoring](https://docs.cloud.google.com/monitoring/docs/application-monitoring-ai-resources) .

## What's next

  - Visualize more data about your agent resources on the [Topology page](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/topology/view-project-topology) .
