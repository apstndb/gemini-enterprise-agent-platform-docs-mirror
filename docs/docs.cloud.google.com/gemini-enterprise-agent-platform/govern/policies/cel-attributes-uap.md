---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/govern/policies/cel-attributes-uap
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/policies/cel-attributes-uap
title: CEL attributes for IAM Access policies
description: Reference guide for Common Expression Language (CEL) attributes and functions available for Identity and Access Management access policy rules in Agent Platform.
data_source: docs.cloud.google.com
---

This document describes the Common Expression Language (CEL) attributes and functions that you can use when writing conditional expressions in IAM Unified Access Policies (UAPs) for Agent Gateway.

To learn more about UAP concepts, see [IAM UAPs overview](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/policies/iam-overview-uap) . To learn how to configure UAPs, see [Create IAM UAPs](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/policies/configure-iam-policies-uap) .

## Available CEL attributes

In your UAPs, you can define conditions with conditional expressions. The expressions can contain multiple sub-expressions. The destination resource type that you use in each relational sub-condition determines which attributes you can use.

For example, in the following condition, in the sub-expression `destination.unregistered.path.startsWith('/v1/statements')` , the resource type is an unregistered destination, the attribute is `destination.unregistered.path` , and `startsWith()` is the CEL function.

```text
destination.unregistered.host == 'finance.example.com' &&
destination.unregistered.path.startsWith('/v1/statements')
```

The attributes described in the following table are available for each resource type:

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Destination resource type</th>
<th>Attribute</th>
<th>Details</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Agent Registry</td>
<td><code>destination.is_registered</code></td>
<td><table>
<tbody>
<tr class="odd">
<td>Value type</td>
<td>Boolean</td>
</tr>
<tr class="even">
<td>Supported values</td>
<td><code>true</code> , <code>false</code></td>
</tr>
<tr class="odd">
<td>Supported operations</td>
<td><code>==</code> , <code>!=</code></td>
</tr>
</tbody>
</table></td>
</tr>
<tr class="even">
<td><code>destination.agent_registry.resource_type</code></td>
<td><table>
<tbody>
<tr class="odd">
<td>Value type</td>
<td>String</td>
</tr>
<tr class="even">
<td>Supported values</td>
<td><code>'AGENT'</code> , <code>'ENDPOINT'</code> , <code>'MCP_SERVER'</code> , <code>'SKILL'</code></td>
</tr>
<tr class="odd">
<td>Supported operations</td>
<td><code>==</code> , <code>!=</code> , <code>in</code></td>
</tr>
</tbody>
</table></td>
<td></td>
</tr>
<tr class="odd">
<td><code>destination.agent_registry.location</code></td>
<td><table>
<tbody>
<tr class="odd">
<td>Value type</td>
<td>String</td>
</tr>
<tr class="even">
<td>Supported values</td>
<td>Google Cloud location ID (for example, <code>'global'</code> , <code>'us-central1'</code> )</td>
</tr>
<tr class="odd">
<td>Supported operations</td>
<td><code>==</code> , <code>!=</code> , <code>in</code></td>
</tr>
</tbody>
</table></td>
<td></td>
</tr>
<tr class="even">
<td><code>destination.agent_registry.project_id</code></td>
<td><table>
<tbody>
<tr class="odd">
<td>Value type</td>
<td>String</td>
</tr>
<tr class="even">
<td>Supported values</td>
<td>Google Cloud project ID</td>
</tr>
<tr class="odd">
<td>Supported operations</td>
<td><code>==</code> , <code>!=</code> , <code>in</code></td>
</tr>
</tbody>
</table></td>
<td></td>
</tr>
<tr class="odd">
<td>Agent</td>
<td><code>destination.agent_registry.agent.name</code></td>
<td><table>
<tbody>
<tr class="odd">
<td>Value type</td>
<td>String</td>
</tr>
<tr class="even">
<td>Supported values</td>
<td>Agent resource name ( <code>projects/ </code><var translate="no"> PROJECT_ID </var><code> /locations/ </code><var translate="no"> LOCATION </var><code> /agents/ </code><var translate="no"> AGENT_NAME</var> )</td>
</tr>
<tr class="odd">
<td>Supported operations</td>
<td><code>==</code> , <code>!=</code> , <code>in</code></td>
</tr>
</tbody>
</table></td>
</tr>
<tr class="even">
<td>MCP Server</td>
<td><code>destination.agent_registry.mcp_server.name</code></td>
<td><table>
<tbody>
<tr class="odd">
<td>Value type</td>
<td>String</td>
</tr>
<tr class="even">
<td>Supported values</td>
<td>MCP server resource name ( <code>projects/ </code><var translate="no"> PROJECT_ID </var><code> /locations/ </code><var translate="no"> LOCATION </var><code> /mcpServers/ </code><var translate="no"> MCP_SERVER_NAME</var> )</td>
</tr>
<tr class="odd">
<td>Supported operations</td>
<td><code>==</code> , <code>!=</code> , <code>in</code></td>
</tr>
</tbody>
</table></td>
</tr>
<tr class="odd">
<td><code>destination.agent_registry.mcp_server.method</code></td>
<td><table>
<tbody>
<tr class="odd">
<td>Value type</td>
<td>String</td>
</tr>
<tr class="even">
<td>Supported values</td>
<td>MCP method name (for example, <code>'tools'</code> , <code>'prompts'</code> , <code>'resources'</code> )</td>
</tr>
<tr class="odd">
<td>Supported operations</td>
<td><code>==</code> , <code>!=</code> , <code>in</code></td>
</tr>
</tbody>
</table></td>
<td></td>
</tr>
<tr class="even">
<td><code>destination.agent_registry.mcp_server.tool.name</code></td>
<td><table>
<tbody>
<tr class="odd">
<td>Value type</td>
<td>String</td>
</tr>
<tr class="even">
<td>Supported values</td>
<td>Tool name (for example, <code>'search_code'</code> , <code>'execute'</code> )</td>
</tr>
<tr class="odd">
<td>Supported operations</td>
<td><code>==</code> , <code>!=</code> , <code>in</code></td>
</tr>
</tbody>
</table></td>
<td></td>
</tr>
<tr class="odd">
<td><code>destination.agent_registry.mcp_server.tool.annotations.read_only_hint</code></td>
<td><table>
<tbody>
<tr class="odd">
<td>Value type</td>
<td>Boolean</td>
</tr>
<tr class="even">
<td>Supported values</td>
<td><code>true</code> , <code>false</code></td>
</tr>
<tr class="odd">
<td>Supported operations</td>
<td><code>==</code> , <code>!=</code></td>
</tr>
</tbody>
</table></td>
<td></td>
</tr>
<tr class="even">
<td><code>destination.agent_registry.mcp_server.tool.annotations.destructive_hint</code></td>
<td><table>
<tbody>
<tr class="odd">
<td>Value type</td>
<td>Boolean</td>
</tr>
<tr class="even">
<td>Supported values</td>
<td><code>true</code> , <code>false</code></td>
</tr>
<tr class="odd">
<td>Supported operations</td>
<td><code>==</code> , <code>!=</code></td>
</tr>
</tbody>
</table></td>
<td></td>
</tr>
<tr class="odd">
<td><code>destination.agent_registry.mcp_server.tool.annotations.idempotent_hint</code></td>
<td><table>
<tbody>
<tr class="odd">
<td>Value type</td>
<td>Boolean</td>
</tr>
<tr class="even">
<td>Supported values</td>
<td><code>true</code> , <code>false</code></td>
</tr>
<tr class="odd">
<td>Supported operations</td>
<td><code>==</code> , <code>!=</code></td>
</tr>
</tbody>
</table></td>
<td></td>
</tr>
<tr class="even">
<td><code>destination.agent_registry.mcp_server.tool.annotations.open_world_hint</code></td>
<td><table>
<tbody>
<tr class="odd">
<td>Value type</td>
<td>Boolean</td>
</tr>
<tr class="even">
<td>Supported values</td>
<td><code>true</code> , <code>false</code></td>
</tr>
<tr class="odd">
<td>Supported operations</td>
<td><code>==</code> , <code>!=</code></td>
</tr>
</tbody>
</table></td>
<td></td>
</tr>
<tr class="odd">
<td><code>destination.agent_registry.mcp_server.prompt.name</code></td>
<td><table>
<tbody>
<tr class="odd">
<td>Value type</td>
<td>String</td>
</tr>
<tr class="even">
<td>Supported values</td>
<td>Prompt name</td>
</tr>
<tr class="odd">
<td>Supported operations</td>
<td><code>==</code> , <code>!=</code> , <code>in</code></td>
</tr>
</tbody>
</table></td>
<td></td>
</tr>
<tr class="even">
<td><code>destination.agent_registry.mcp_server.resource.name</code></td>
<td><table>
<tbody>
<tr class="odd">
<td>Value type</td>
<td>String</td>
</tr>
<tr class="even">
<td>Supported values</td>
<td>Resource name</td>
</tr>
<tr class="odd">
<td>Supported operations</td>
<td><code>==</code> , <code>!=</code> , <code>in</code></td>
</tr>
</tbody>
</table></td>
<td></td>
</tr>
<tr class="odd">
<td>Endpoint</td>
<td><code>destination.agent_registry.endpoint.name</code></td>
<td><table>
<tbody>
<tr class="odd">
<td>Value type</td>
<td>String</td>
</tr>
<tr class="even">
<td>Supported values</td>
<td>Endpoint resource name ( <code>projects/ </code><var translate="no"> PROJECT_ID </var><code> /locations/ </code><var translate="no"> LOCATION </var><code> /endpoints/ </code><var translate="no"> ENDPOINT_NAME</var> )</td>
</tr>
<tr class="odd">
<td>Supported operations</td>
<td><code>==</code> , <code>!=</code> , <code>in</code></td>
</tr>
</tbody>
</table></td>
</tr>
<tr class="even">
<td>Unregistered Destination</td>
<td><code>destination.unregistered.host</code></td>
<td><table>
<tbody>
<tr class="odd">
<td>Value type</td>
<td>String</td>
</tr>
<tr class="even">
<td>Supported values</td>
<td>Hostname (for example, <code>'google.com'</code> , <code>'example.com'</code> )</td>
</tr>
<tr class="odd">
<td>Supported operations</td>
<td><code>==</code> , <code>!=</code> , <code>in</code> , <code>.startsWith()</code> , <code>.endsWith()</code> , <code>.contains()</code></td>
</tr>
</tbody>
</table></td>
</tr>
<tr class="odd">
<td><code>destination.unregistered.path</code></td>
<td><table>
<tbody>
<tr class="odd">
<td>Value type</td>
<td>String</td>
</tr>
<tr class="even">
<td>Supported values</td>
<td>Request path (for example, <code>'/admin'</code> , <code>'/api/v1'</code> )</td>
</tr>
<tr class="odd">
<td>Supported operations</td>
<td><code>==</code> , <code>!=</code> , <code>in</code> , <code>.startsWith()</code> , <code>.endsWith()</code> , <code>.contains()</code></td>
</tr>
</tbody>
</table></td>
<td></td>
</tr>
<tr class="even">
<td><code>destination.unregistered.method</code></td>
<td><table>
<tbody>
<tr class="odd">
<td>Value type</td>
<td>String</td>
</tr>
<tr class="even">
<td>Supported values</td>
<td>HTTP method (for example, <code>'get'</code> , <code>'post'</code> , <code>'put'</code> , <code>'delete'</code> )</td>
</tr>
<tr class="odd">
<td>Supported operations</td>
<td><code>==</code> , <code>!=</code> , <code>in</code></td>
</tr>
</tbody>
</table></td>
<td></td>
</tr>
</tbody>
</table>

> **Note:** The `startsWith()` , `endsWith()` , and `contains()` functions (or `STARTS_WITH` , `ENDS_WITH` , and `CONTAINS` ) are supported only for the `destination.unregistered.host` and `destination.unregistered.path` attributes. Other attributes don't support these string functions.

## What's next

- [Create IAM UAPs](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/policies/configure-iam-policies-uap)
- [Manage IAM UAPs](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/policies/manage-iam-policies-uap)
- [Troubleshoot IAM UAPs](https://docs.cloud.google.com/gemini-enterprise-agent-platform/troubleshooting/troubleshoot-iam-policies-uap)

Overview

### [Agent Gateway overview](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/gateways/agent-gateway-overview)

Get an overview of Agent Gateway.

Guide

### [Configure content and business policies](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/policies/configure-semantic-governance)

Learn how to configure content and business policies.

Guide

### [Test policies](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/policies/test-policies)

Learn how to test policies.
