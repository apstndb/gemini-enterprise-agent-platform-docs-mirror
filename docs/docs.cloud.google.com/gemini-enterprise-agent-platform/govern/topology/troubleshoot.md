---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/govern/topology/troubleshoot
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/topology/troubleshoot
title: Troubleshoot queries
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Use the information in this document to help you to identify and resolve issues with queries that return no results or seem to be missing data.

## Verify requirements

Review the requirements to view topologies and the underlying data.

  - [Requirements for the Gemini Enterprise Agent Platform **Topology** page](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/topology/view-project-topology#requirements)
  - [Requirements for topologies in Agent Registry](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/topology/view-agent-registry-topology#requirements)

You can also review App Topology [limitations](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/topology#limitations) for additional considerations.

## Query does not return data

If a query does not return data, try starting from a predefined query or broadening your query. Make one change at a time so that you can track which changes improve your query results.

1.  Try a suggested query. The predefined query suggestions are designed to return results that are relevant for most environments. If a suggested query works, try modifying it to better meet your needs.

2.  Test a broader query. For example, if the query filters a node with a `Where` clause, remove the `Where` clause and run the query again. If the broader query works, the original query might be too specific for the available data.

3.  Check the query logic. Avoid combining too many constraints that might unintentionally exclude all results. For example, if a test project has no active deployments, looking for `Critical` vulnerabilities in active deployments will produce no results.

## Data is missing or looks old

If some data seems to be missing or appears outdated, try the following steps:

1.  Wait a few minutes for data synchronization to occur. Recently created or updated resources might take a few minutes to appear in query results. For example, if a user just deployed a new workload or updated an IAM policy, there might be a delay before these changes are reflected in the query results.
2.  Some types of data are not supported or might have longer latency for data synchronization. See the list of [limitations](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/topology#limitations) .
