---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/govern/policies/iam-overview-uap
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/policies/iam-overview-uap
title: IAM Access policies overview
description: Learn about IAM policies to securely govern agentic communication in Agent Platform.
data_source: docs.cloud.google.com
---

> **Note:** This feature does not support VPC Service Controls.

You can create Identity and Access Management (IAM) Unified Access Policies (UAPs) to help securely govern communication between *agent principals* and *destination resources* , such as destination agents, MCP servers, and endpoints. These policies are bound to the project that contains your Agent Gateway instances.

Agent Gateway uses Identity-Aware Proxy (IAP) to evaluate and enforce the UAPs.

IAP also integrates with Context-Aware Access to [provide end-to-end agent identity authentication and authorization](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/policies/iam-overview-uap#end-to-end-security) .

To set up UAPs for Agent Gateway, see [Configure IAM UAPs](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/policies/configure-iam-policies-uap) .

You can also create a Principal Access Boundary (PAB) on the agent identity. Agent Gateway can use IAP to enforce Principal Access Boundary policies.

## Enable Agent Gateway

To use agentic communication policies, you must [set up Agent Gateway](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/gateways/set-up-agent-gateway) .

We recommend that you configure Agent Gateway in dry-run mode ( `DRY_RUN` ) in a staging environment to verify that your policies are working as expected.

> **Important:** In dry-run mode, IAP logs disallowed agentic communications to Cloud Audit Logs but doesn't block them.

When you are satisfied that the policies are functioning correctly, you can update the Agent Gateway configuration to set enforcement mode to `ENFORCE` . In this mode, agentic communications that violate the policy are disallowed and communication to the resource is blocked.

## UAPs overview

UAPs control whether one or more agent principals can access one or more destination resources. UAPs extend the IAM policy model by supporting multiple *rules* in a single policy. Unlike IAM allow policies and deny policies, each rule in a UAP can have both an allow effect and a deny effect. Learn more about [IAM policy types](https://docs.cloud.google.com/iam/docs/policy-types) .

Rules also contain *conditions* that are expressed in Common Expression Language (CEL). Conditions act as the primary mechanism to control access to post-gateway resources. Enforcing UAPs with Agent Gateway and IAP delivers strict behavioral control over agents deployed across your enterprise. You can represent real-world, fine-grained agent governance use cases in a single policy.

A typical policy contains at least two distinct rules:

- **Allow rule:** Allow rules have an [allow effect](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/policies/iam-overview-uap#rule-effect) that lets agent principals access specific, safe operations, such as performing a read operation on a tool to fetch tracking data or view registry entries.
- **Deny rule:** Deny rules have a [deny effect](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/policies/iam-overview-uap#rule-effect) that disallows the agent from executing unwanted actions, such as performing an uncommanded delete or update operation on a critical resource.

For example, consider an automated customer support agent that needs to interact with internal tools that have privileged access to a customer database. The administrator configures an Agent Gateway with IAP to enforce IAM UAPs. The administrator can configure a UAP with an allow rule that authorizes the agent principal to read support tickets, and a deny rule that disallows the agent principal from deleting or updating database records.

By using UAPs that contain both allow and deny rules, organizations can deploy a single corporate compliance policy directly onto underlying cloud infrastructure to constrain agent behavior.

## Best practices

Follow these best practices when you configure agent egress policies:

- **Use dry-run mode:** Deploy new or modified policies in dry-run mode first to make sure that your policy works as expected, without blocking active agent traffic.
- **Apply the principle of least privilege:** Grant only necessary permissions. Use specific tool names or paths in CEL conditions rather than wildcards.
- **Use deny rules for guardrails:** Use explicit deny rules to implement critical guardrails, such as blocking destructive tools on production endpoints. Using deny rules for guardrails is effective because deny rules override allow rules.
- **Perform regular audits:** Periodically review Cloud Audit Logs logs and policy configurations to verify that they comply with your organization's security policies.

## UAP components

UAPs contain one or more rules. Rules have the following components:

### Agent principals

In your IAM UAPs, you define one or more agent principals. Agent principals are the members that you grant access to. You specify agents by their agent identity, the identity of the agent initiating communication with a resource. For more information about how different types of agents receive identities, see [Agent identity](https://docs.cloud.google.com/gemini-enterprise-agent-platform/scale/runtime/agent-identity) . Agent identities are represented by [principal identifiers](https://docs.cloud.google.com/iam/docs/principal-identifiers) that contain the SPIFFE-formatted identity of the agent (for example, `principal://agents.global.org-...` ).

> **Important:** Agent identifiers in URN format, such as `urn:agent:...` , are used solely for inventory and catalog lookup and are not used in IAM policy bindings.

You can specify an array of individual agent identities or an array of principal sets.

Built-in agent identities are provisioned across Google Cloud services such as Agent Runtime (Reasoning Engine), Gemini Enterprise (Discovery Engine), and Cloud Run services configured with agent identity. These agent principals take the form `principal:// `` TRUST_DOMAIN `` / `` AGENT_UNIQUE_IDENTIFIER` , where the identifier represents the resource path of the agent on its hosting service. You can also specify agents using Workload Identity Federation principal identifiers.

### Rule effect

The rule effect defines whether the rule allows or disallows agent principals from accessing a resource.

### Destination resources

IAM UAPs manage access from agent principals to destination resources. Destination resources are the resources that agent principals are trying to access. Destination resources are specified in the rule [conditions](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/policies/iam-overview-uap#conditions) . Destination resources can be either [registered resources](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/policies/iam-overview-uap#registered-resources) or [unregistered resources](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/policies/iam-overview-uap#unregistered-resources) .

#### Registered resources

Registered resources are resources that are registered in an Agent Registry registry.

Registered resources include the following:

- Registries: Entire agent registries within a project.
- MCP servers: MCP servers that are registered in an agent registry.
- Agents: Agents that are registered in an agent registry. Individual agents can be specified individually by their agent identity. A group of agents can be specified by a principal set identifier.
- Endpoints: Endpoints that are registered in an agent registry.

Individual services can be registered in Agent Registry. If you regionalize your agent registries and your rule manages access to registered resources, then your UAPs applies only to the resources that are in the registry's region.

#### Unregistered resources

Unregistered resources are resources that are not registered in an agent registry. To grant or deny access to unregistered resources in your UAP rules, you must specify unregistered resources in your rule [conditions](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/policies/iam-overview-uap#conditions) by using Common Expression Language (CEL) expressions that contain [unregistered host and path attributes](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/policies/cel-attributes-uap#unregistered-destination) .

### Conditions

In UAPs rules, you use Common Expression Language (CEL) expressions in the `conditions` block to define both **target resource scope** and **fine-grained access criteria** :

- **Target resource scope** : Identifies *which* destination resources the rule governs. In JSON-formatted policy files, you specify destination attributes, such as `destination.agent_registry.mcp_server.name` or `destination.unregistered.host` . In the Google Cloud console, selecting destinations under **Target resources** automatically adds these resource criteria to the rule's condition expression.

- **Access criteria** : Use a Boolean expression to determine *when* and *under what constraints* the rule effect applies. For example, you can restrict access based on tool names, read-only status, HTTP methods, or path prefixes using [UAP CEL attributes](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/policies/iam-overview-uap#cel-attributes) . The rule effect (allow or deny) takes effect only when the entire CEL expression evaluates to `true` .

In the gcloud CLI and REST API, you specify these CEL expressions in the `conditions` field of the rule definition.

In the Google Cloud console, you can configure standard rules by using the **Condition builder** , or write custom CEL expressions directly in the **Condition editor** .

### Permissions

In IAP V2 with IAM UAPs, the `iap.googleapis.com/resources.egressViaIAP` permission is always granted on the destination resource. In the gcloud CLI and REST API, you specify the permission in the `operation.permissions` field of your policy file.

## Policy creation options

In the **Policies** page in the Google Cloud console, you can create IAM UAPs. We recommend that you create only [UAPs (IAM v3 policies)](https://docs.cloud.google.com/iam/docs/policy-types) .

In both the gcloud CLI and the REST API, you can configure IAM UAPs by first creating a JSON-formatted file. We recommend that you create only UAPs.

## End-to-end authentication and authorization

IAP and Context-Aware Access provide default end-to-end agent identity authentication and authorization by using the following protocols:

- Mutual TLS (mTLS)
- Demonstrating Proof of Possession (DPoP)

Agent identities are provisioned with an X.509 certificate and a certificate-bound token. IAP enforces that agent identities use mutual TLS (mTLS) to authenticate to Agent Gateway. When the gateway allows the agent to egress and access Google Cloud APIs, MCP servers, other agents, and endpoints, the agent attempts access outside of the mTLS boundary. To help protect communication, Context-Aware Access enforces a Google-managed Context-Aware Access policy. The policy requires DPoP to validate the certificate-bound token that is bound to the agent identity. For more information about how Context-Aware Access uses mTLS and DPoP, see [Context-Aware Access agent security](https://docs.cloud.google.com/access-context-manager/docs/caa-agent-security) .

## UAP CEL attributes

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

- [CEL attributes for UAPs](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/policies/cel-attributes-uap)
- [Create IAM UAPs](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/policies/configure-iam-policies-uap)
- [Manage IAM UAPs](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/policies/manage-iam-policies-uap)
- [Troubleshoot IAM UAPs](https://docs.cloud.google.com/gemini-enterprise-agent-platform/troubleshooting/troubleshoot-iam-policies-uap)

Codelab

### [Codelab: Secure cross-cloud agentic AI applications](https://codelabs.developers.google.com/next26/aiinfra-learning-pod/screen1-securing-cross-cloud-agentic)

Learn how to secure your agentic applications in the Securing Cross-Cloud Agentic AI Applications codelab.

Overview

### [Agent Gateway overview](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/gateways/agent-gateway-overview)

Get an overview of Agent Gateway.

Guide

### [Security controls](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/security-controls)

Learn about security controls for Google Agent Platform.
