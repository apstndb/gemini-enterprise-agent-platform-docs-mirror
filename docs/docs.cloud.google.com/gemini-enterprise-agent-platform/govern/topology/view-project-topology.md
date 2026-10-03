---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/govern/topology/view-project-topology
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/topology/view-project-topology
title: View topologies for a project
description: Use topology graphs to analyze agent relationships, dependencies, and compliance.
data_source: docs.cloud.google.com
---

To answer questions about agent health, relationships, dependencies, and policy compliance, you can run queries that correlate agent data, traffic data, and other resource data. The results are displayed as topology graph that you can explore.

A topology graph can help you to do the following:

- **Map resource relationships:** Visualize data associated with your agents, including, MCP servers, underlying infrastructure, endpoints, skills, and identities.
- **Identify registration gaps:** Identify discovered compute workloads that aren't registered in Agent Registry.
- **Validate policy compliance:** Identify vulnerabilities and security issues identified by Security Command Center.
- **Analyze impacts of changes:** Assess impacts of changes to access policies, endpoint credentials, or infrastructure that agent resources depend on.

You can run suggested queries, customize a suggested query, or create your own custom query.

## Before you begin

1.  Identify the Google Cloud project that you want to set up.

    Security and compliance data provided by Security Command Center is only available for projects in a Google Cloud organization. If you want to migrate a project to an organization, see the [migration instructions](https://docs.cloud.google.com/resource-manager/docs/handle-special-cases#migrating_projects_no_org) .

2.  Set up the services that provide the resource data that you want to query:

    - To view software supply chain data such as build provenance, [configure Developer Connect insights](https://docs.cloud.google.com/developer-connect/docs/set-up-insights) .

    - To view data for agent resources registered in Agent Registry, [set up Agent Registry](https://docs.cloud.google.com/agent-registry/setup) and register your agent resources.

    - To view agent traffic, [instrument your AI applications](https://docs.cloud.google.com/stackdriver/docs/instrumentation/ai-agent-overview) .

    - To view security and compliance data, set up Security Command Center for security and compliance data. [Activate Security Command Center](https://docs.cloud.google.com/security-command-center/docs/activate-scc-overview) at the organization level and [configure](https://docs.cloud.google.com/security-command-center/docs/how-to-configure-security-command-center) the features that you want to use. Querying data from Security Command Center is only available for [Premium and Enterprise tiers](https://docs.cloud.google.com/security-command-center/docs/service-tiers) .

3.  Enable the App Hub, App Topology, Cloud Asset Inventory, and Observability APIs, if any are not already enabled.

    **Roles required to enable APIs**

    To enable APIs, you need the `serviceusage.services.enable` permission. If you created the project, then you likely already have this permission through the Owner role ( `roles/owner` ). Otherwise, you can get this permission through the Service Usage Admin role ( `roles/serviceusage.serviceUsageAdmin` ). [Learn how to grant roles](https://docs.cloud.google.com/iam/docs/granting-changing-revoking-access) .

<!-- -->

1.  [Verify that billing is enabled for your Google Cloud project](https://docs.cloud.google.com/billing/docs/how-to/verify-billing-enabled#confirm_billing_is_enabled_on_a_project) .

2.  If you are protecting services in a VPC Service Controls perimeter, update the perimeter to include App Topology and services that provide underlying data. [Learn more](https://docs.cloud.google.com/app-topology/use-vpc-sc) .

### Required roles

To get the permissions that you need to view topology graphs, ask your administrator to grant you the [App Topology Viewer](https://docs.cloud.google.com/iam/docs/roles-permissions/apptopology#apptopology.viewer) ( `roles/apptopology.viewer` ) IAM role on the projects where you want to use App Topology. For more information about granting roles, see [Manage access to projects, folders, and organizations](https://docs.cloud.google.com/iam/docs/granting-changing-revoking-access) .

This predefined role contains the permissions required to view topology graphs. To see the exact permissions that are required, expand the **Required permissions** section:

#### Required permissions

The following permissions are required to view topology graphs:

- Get discovered resource data: `apptopology.discoveredResourcesTopologies.generate`
- Get resource data data: `apptopology.sreDomainTopologies.generate`

You might also be able to get these permissions with [custom roles](https://docs.cloud.google.com/iam/docs/creating-custom-roles) or other [predefined roles](https://docs.cloud.google.com/iam/docs/roles-overview#predefined) .

## About queries

App Topology queries consist of several components:

- **Nodes** - Discovered or registered Google Cloud resources. Examples of nodes include:

  - A Compute Engine VM
  - A container image in Artifact Registry
  - An agent
  - A Cloud Monitoring [alert](https://docs.cloud.google.com/monitoring/alerts)
  - An AI application
  - A vulnerability

  The query builder groups nodes by service.

- **Where clause** : a filter that's applied to a node to refine the query based on the specific properties of the node.

- **Connections** : A directional relationship between two nodes. Connections are context-aware, and only valid relationships are available for a selected node type. Examples include:

  - `contained in`
  - `sends traffic to`
  - `owns`
  - `depends on`

The following example query searches for deployments that have a specific vulnerability:

![A query example using a variety of components](https://docs.cloud.google.com/static/gemini-enterprise-agent-platform/images/topology-query.png)

The query establishes the key nodes of the investigation: - `Agent` - `Vulnerability`

The connection `contains` indicate the node relationships:

- `Agent contains Vulnerability`

The Where clause filters vulnerability results to show a specific CVE.

- `Where Id = CVE-2026-24061`

## Use or customize a suggested query

App Topology provides query suggestions that you can use without any changes, or you can customize those suggestions to fit your specific requirements.

1.  In the Google Cloud console, go to the Topology page.

2.  In the project picker, select the project that contains your agents.

3.  Under **Quick Queries** , click a query to see a preview of the query components.

4.  To use the query, click **Use suggestion** . The query appears in the **Show** section.

5.  To make changes to the query, add, edit, or remove components.

    - To add a component to the query, click the plus icon ( add ) next to the node.
    - To remove a component, click the close icon close .
    - To change the value of a `Where` clause, click the value.

    You can click **Undo** undo to revert a change or **Redo** redo to re-apply changes you reverted with **Undo** .

    As you build your query, the available nodes, filters, and connections are updated.

6.  When you are finished editing the query, click **Run query** . If the results of your query includes Google Cloud discovered resources or resources registered in Agent Registry, a topology graph is displayed.

    Graphs aren't available for query results that only include data types such as strings or counts.

    Based on the results, you can edit the query and then click **Run query** to update the topology graph.

7.  Explore the topology graph. The graph shows resources that match your query and the relationships between them.

    - Icons represent nodes, discovered and registered resources and their resource type.
    - Lines represent connections, the relationships between nodes.

    ![An example topology graph with a selected node](https://docs.cloud.google.com/static/gemini-enterprise-agent-platform/images/topology-graph.png)

    You can interact with a topology in the following ways:

    - Change the visualization by zooming in or out or repositioning nodes.
    - View the label for a connection by hovering over the connection line between two nodes.
    - Get information about a node or connection by selecting it.
    - Hide or show the query panel by clicking **Toggle panel** first_page .

If there are no results, try [refining your query](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/topology/troubleshoot#no-data) .

### Create custom queries

To create a custom query, either start a new query or [customize an existing suggested query](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/topology/view-project-topology#suggested-query) using the following steps:

1.  In the Google Cloud console, go to the Topology page.

2.  In the project picker, select the project that contains your agents.

3.  In the query builder, click add and select a resource or finding as the primary node for your query, and then click **Continue** .

4.  To refine your query, click the toggle for any filter or connection to enable it for the selected node. Define the value for each filter you enable.

    > **Note:** All customizations are context-aware. You only see the filters and connections that are valid for the selected node type.

5.  To make changes to the query, add, edit, or remove components.

    - To add a component to the query, click the plus icon ( add ) next to the node.
    - To remove a component, click the close icon close .
    - To change the value of a `Where` clause, click the value.

    You can click **Undo** undo to revert a change or **Redo** redo to re-apply changes you reverted with **Undo** .

    As you build your query, the available nodes, filters, and connections are updated.

6.  When you are finished editing the query, click **Run query** . If the results of your query includes Google Cloud discovered resources or resources registered in Agent Registry, a topology graph is displayed.

    Graphs aren't available for query results that only include data types such as strings or counts.

    Based on the results, you can edit the query and then click **Run query** to update the topology graph.

7.  Explore the topology graph. The graph shows resources that match your query and the relationships between them.

    - Icons represent nodes, discovered and registered resources and their resource type.
    - Lines represent connections, the relationships between nodes.

    ![An example topology graph with a selected node](https://docs.cloud.google.com/static/gemini-enterprise-agent-platform/images/topology-graph.png)

    You can interact with a topology in the following ways:

    - Change the visualization by zooming in or out or repositioning nodes.
    - View the label for a connection by hovering over the connection line between two nodes.
    - Get information about a node or connection by selecting it.
    - Hide or show the query panel by clicking **Toggle panel** first_page .

Some [limitations](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/topology#limitations) apply to queries. If there are no results, try [refining your query](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/topology/troubleshoot#no-data) .

## What's next

- [Register discovered agents](https://docs.cloud.google.com/agent-registry/register-agents) in Agent Registry.
