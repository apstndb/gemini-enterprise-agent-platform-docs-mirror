---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/govern/policies/iam-overview-uap
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/policies/iam-overview-uap
title: IAM Access policies overview
description: Learn about IAM policies to securely govern agentic communication in Agent Platform.
data_source: docs.cloud.google.com
---

> **Note:** This feature does not support VPC Service Controls.

You can create Identity and Access Management (IAM) Unified Access Policies (Access policies) to help securely govern communication between *agent principals* and *destination resources* , such as destination agents, MCP servers, and endpoints. These policies are bound to the project that contains your Agent Gateway instances.

Agent Gateway uses Identity-Aware Proxy (IAP) to evaluate and enforce the Access policies.

IAP also integrates with Context-Aware Access to [provide end-to-end agent identity authentication and authorization](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/policies/iam-overview-uap#end-to-end-security) .

To set up Access policies for Agent Gateway, see [Configure IAM Access policies](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/policies/configure-iam-policies-uap) .

You can also create a principal access boundary (PAB) on the agent identity. Agent Gateway can use IAP to enforce principal access boundary policies.

## Enable Agent Gateway

To use agentic communication policies, you must [set up Agent Gateway](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/gateways/set-up-agent-gateway) .

We recommend that you configure Agent Gateway in dry-run mode ( `DRY_RUN` ) in a staging environment to verify that your policies are working as expected.

> **Important:** In dry-run mode, IAP logs disallowed agentic communications to Cloud Audit Logs but doesn't block them.

When you are satisfied that the policies are functioning correctly, you can update the Agent Gateway configuration to set enforcement mode to `ENFORCE` . In this mode, agentic communications that violate the policy are disallowed and communication to the resource is blocked.

## Access policies overview

Access policies control whether one or more agent principals can access one or more destination resources. Access policies extend the IAM policy model by supporting multiple *rules* in a single policy. Unlike IAM allow policies and deny policies, each rule in a Access policy can have both an allow effect and a deny effect. Learn more about [IAM policy types](https://docs.cloud.google.com/iam/docs/access-policy-overview#policy-types) .

Rules also contain *conditions* that are expressed in Common Expression Language (CEL). Conditions act as the primary mechanism to control access to post-gateway resources. Enforcing Access policies with Agent Gateway and IAP delivers strict behavioral control over agents deployed across your enterprise. You can represent real-world, fine-grained agent governance use cases in a single policy.

A typical policy contains at least two distinct rules:

  - **Allow rule:** Allow rules have an [allow effect](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/policies/iam-overview-uap#rule-effect) that lets agent principals access specific, safe operations, such as performing a read operation on a tool to fetch tracking data or view registry entries.
  - **Deny rule:** Deny rules have a [deny effect](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/policies/iam-overview-uap#rule-effect) that disallows the agent from executing unwanted actions, such as performing an uncommanded delete or update operation on a critical resource.

For example, consider an automated customer support agent that needs to interact with internal tools that have privileged access to a customer database. The administrator configures an Agent Gateway with IAP to enforce IAM Access policies. The administrator can configure an Access policy with an allow rule that authorizes the agent principal to read support tickets, and a deny rule that disallows the agent principal from deleting or updating database records.

By using Access policies that contain both allow and deny rules, organizations can deploy a single corporate compliance policy directly onto underlying cloud infrastructure to constrain agent behavior.

## Best practices

Follow these best practices when you configure agent egress policies:

  - **Use dry-run mode:** Deploy new or modified policies in dry-run mode first to make sure that your policy works as expected, without blocking active agent traffic.
  - **Apply the principle of least privilege:** Grant only necessary permissions. Use specific tool names or paths in CEL conditions rather than wildcards.
  - **Use deny rules for guardrails:** Use explicit deny rules to implement critical guardrails, such as blocking destructive tools on production endpoints. Using deny rules for guardrails is effective because deny rules override allow rules.
  - **Perform regular audits:** Periodically review Cloud Audit Logs logs and policy configurations to verify that they comply with your organization's security policies.

## Access policy components

Access policies contain one or more rules. Rules have the following components:

### Agent principals

In your IAM Access policies, you define one or more agent principals. Agent principals are the members that you grant access to. You specify agents by their agent identity, the identity of the agent initiating communication with a resource. For more information about how different types of agents receive identities, see [Agent identity](https://docs.cloud.google.com/gemini-enterprise-agent-platform/scale/runtime/agent-identity) . Agent identities are represented by [principal identifiers](https://docs.cloud.google.com/iam/docs/principal-identifiers) that contain the SPIFFE-formatted identity of the agent (for example, `principal://agents.global.org-...` ).

> **Important:** Agent identifiers in URN format, such as `urn:agent:...` , are used solely for inventory and catalog lookup and are not used in IAM policy bindings.

You can specify an array of individual agent identities or an array of principal sets.

Built-in agent identities are provisioned across Google Cloud services such as Agent Runtime (Reasoning Engine), Gemini Enterprise (Discovery Engine), and Cloud Run services configured with agent identity. These agent principals take the form ` principal:// TRUST_DOMAIN / AGENT_UNIQUE_IDENTIFIER  ` , where the identifier represents the resource path of the agent on its hosting service. You can also specify agents using Workload Identity Federation principal identifiers.

### Rule effect

The rule effect defines whether the rule allows or disallows agent principals from accessing a resource.

### Destination resources

IAM Access policies manage access from agent principals to destination resources. Destination resources are the resources that agent principals are trying to access. Destination resources are specified in the rule [conditions](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/policies/iam-overview-uap#conditions) . Destination resources can be either [registered resources](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/policies/iam-overview-uap#registered-resources) or [unregistered resources](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/policies/iam-overview-uap#unregistered-resources) .

#### Registered resources

Registered resources are resources that are registered in an Agent Registry registry.

Registered resources include the following:

  - Registries: Entire agent registries within a project.
  - MCP servers: MCP servers that are registered in an agent registry.
  - Agents: Agents that are registered in an agent registry. Individual agents can be specified individually by their agent identity. A group of agents can be specified by a principal set identifier.
  - Endpoints: Endpoints that are registered in an agent registry.

Individual services can be registered in Agent Registry. If you regionalize your agent registries and your rule manages access to registered resources, then your Access policies applies only to the resources that are in the registry's region.

#### Unregistered resources

Unregistered resources are resources that are not registered in an agent registry. To grant or deny access to unregistered resources in your Access policy rules, you must specify unregistered resources in your rule [conditions](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/policies/iam-overview-uap#conditions) by using Common Expression Language (CEL) expressions that contain [unregistered host and path attributes](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/policies/cel-attributes-uap#unregistered-destination) .

### Conditions

In Access policies rules, you use Common Expression Language (CEL) expressions in the `conditions` block to define both **target resource scope** and **fine-grained access criteria** :

  - **Target resource scope** : Identifies *which* destination resources the rule governs. In JSON-formatted policy files, you specify destination attributes, such as `destination.agent_registry.mcp_server.name` or `destination.unregistered.host` . In the Google Cloud console, selecting destinations under **Target resources** automatically adds these resource criteria to the rule's condition expression.

  - **Access criteria** : Use a Boolean expression to determine *when* and *under what constraints* the rule effect applies. For example, you can restrict access based on tool names, read-only status, HTTP methods, or path prefixes using [Access policy CEL attributes](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/policies/iam-overview-uap#cel-attributes) . The rule effect (allow or deny) takes effect only when the entire CEL expression evaluates to `true` .

In the gcloud CLI and REST API, you specify these CEL expressions in the `conditions` field of the rule definition.

In the Google Cloud console, you can configure standard rules by using the **Condition builder** , or write custom CEL expressions directly in the **Condition editor** .

### Permissions

In IAP V2 with IAM Access policies, the `iap.googleapis.com/resources.egressViaIAP` permission is always granted on the destination resource. In the gcloud CLI and REST API, you specify the permission in the `operation.permissions` field of your policy file.

## Policy creation options

In the **Policies** page in the Google Cloud console, you can create IAM Access policies. We recommend that you create only [Access policies (IAM v3 policies)](https://docs.cloud.google.com/iam/docs/policy-types) .

In both the gcloud CLI and the REST API, you can configure IAM Access policies by first creating a JSON-formatted file. We recommend that you create only Access policies.

## End-to-end authentication and authorization

IAP and Context-Aware Access provide default end-to-end agent identity authentication and authorization by using the following protocols:

  - Mutual TLS (mTLS)
  - Demonstrating Proof of Possession (DPoP)

Agent identities are provisioned with an X.509 certificate and a certificate-bound token. IAP enforces that agent identities use mutual TLS (mTLS) to authenticate to Agent Gateway. When the gateway allows the agent to egress and access Google Cloud APIs, MCP servers, other agents, and endpoints, the agent attempts access outside of the mTLS boundary. To help protect communication, Context-Aware Access enforces a Google-managed Context-Aware Access policy. The policy requires DPoP to validate the certificate-bound token that is bound to the agent identity. For more information about how Context-Aware Access uses mTLS and DPoP, see [Context-Aware Access agent security](https://docs.cloud.google.com/access-context-manager/docs/caa-agent-security) .

## Access policy CEL attributes

In your Access policies, you can define conditions with conditional expressions. The expressions can contain multiple sub-expressions. The destination resource type that you use in each relational sub-condition determines which attributes you can use.

For example, in the following condition, in the sub-expression `destination.unregistered.path.startsWith('/v1/statements')` , the resource type is an unregistered destination, the attribute is `destination.unregistered.path` , and `startsWith()` is the CEL function.

```text
destination.unregistered.host == 'finance.example.com' &&
destination.unregistered.path.startsWith('/v1/statements')
```

The attributes described in the following table are available for each resource type:

Destination resource type

Attribute

Details

### Agent Registry

`destination.is_registered`

|                      |                  |
| -------------------- | ---------------- |
| Value type           | Boolean          |
| Supported values     | `true` , `false` |
| Supported operations | `==` , `!=`      |

`destination.agent_registry.resource_type`

|                      |                                                       |
| -------------------- | ----------------------------------------------------- |
| Value type           | String                                                |
| Supported values     | `'AGENT'` , `'ENDPOINT'` , `'MCP_SERVER'` , `'SKILL'` |
| Supported operations | `==` , `!=` , `in`                                    |

`destination.agent_registry.location`

|                      |                                                                       |
| -------------------- | --------------------------------------------------------------------- |
| Value type           | String                                                                |
| Supported values     | Google Cloud location ID (for example, `'global'` , `'us-central1'` ) |
| Supported operations | `==` , `!=` , `in`                                                    |

`destination.agent_registry.project_id`

|                      |                         |
| -------------------- | ----------------------- |
| Value type           | String                  |
| Supported values     | Google Cloud project ID |
| Supported operations | `==` , `!=` , `in`      |

### Agent

`destination.agent_registry.agent.name`

|                      |                                                                                                                                                                |
| -------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Value type           | String                                                                                                                                                         |
| Supported values     | Agent resource name ( ` projects/             PROJECT_ID            /locations/             LOCATION            /agents/             AGENT_NAME            ` ) |
| Supported operations | `==` , `!=` , `in`                                                                                                                                             |

### MCP Server

`destination.agent_registry.mcp_server.name`

|                      |                                                                                                                                                                              |
| -------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Value type           | String                                                                                                                                                                       |
| Supported values     | MCP server resource name ( ` projects/             PROJECT_ID            /locations/             LOCATION            /mcpServers/             MCP_SERVER_NAME            ` ) |
| Supported operations | `==` , `!=` , `in`                                                                                                                                                           |

`destination.agent_registry.mcp_server.method`

|                      |                                                                         |
| -------------------- | ----------------------------------------------------------------------- |
| Value type           | String                                                                  |
| Supported values     | MCP method name (for example, `'tools'` , `'prompts'` , `'resources'` ) |
| Supported operations | `==` , `!=` , `in`                                                      |

`destination.agent_registry.mcp_server.tool.name`

|                      |                                                         |
| -------------------- | ------------------------------------------------------- |
| Value type           | String                                                  |
| Supported values     | Tool name (for example, `'search_code'` , `'execute'` ) |
| Supported operations | `==` , `!=` , `in`                                      |

`destination.agent_registry.mcp_server.tool.annotations.read_only_hint`

|                      |                  |
| -------------------- | ---------------- |
| Value type           | Boolean          |
| Supported values     | `true` , `false` |
| Supported operations | `==` , `!=`      |

`destination.agent_registry.mcp_server.tool.annotations.destructive_hint`

|                      |                  |
| -------------------- | ---------------- |
| Value type           | Boolean          |
| Supported values     | `true` , `false` |
| Supported operations | `==` , `!=`      |

`destination.agent_registry.mcp_server.tool.annotations.idempotent_hint`

|                      |                  |
| -------------------- | ---------------- |
| Value type           | Boolean          |
| Supported values     | `true` , `false` |
| Supported operations | `==` , `!=`      |

`destination.agent_registry.mcp_server.tool.annotations.open_world_hint`

|                      |                  |
| -------------------- | ---------------- |
| Value type           | Boolean          |
| Supported values     | `true` , `false` |
| Supported operations | `==` , `!=`      |

`destination.agent_registry.mcp_server.prompt.name`

|                      |                    |
| -------------------- | ------------------ |
| Value type           | String             |
| Supported values     | Prompt name        |
| Supported operations | `==` , `!=` , `in` |

`destination.agent_registry.mcp_server.resource.name`

|                      |                    |
| -------------------- | ------------------ |
| Value type           | String             |
| Supported values     | Resource name      |
| Supported operations | `==` , `!=` , `in` |

### Endpoint

`destination.agent_registry.endpoint.name`

|                      |                                                                                                                                                                         |
| -------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Value type           | String                                                                                                                                                                  |
| Supported values     | Endpoint resource name ( ` projects/             PROJECT_ID            /locations/             LOCATION            /endpoints/             ENDPOINT_NAME            ` ) |
| Supported operations | `==` , `!=` , `in`                                                                                                                                                      |

### Unregistered Destination

`destination.unregistered.host`

|                      |                                                                      |
| -------------------- | -------------------------------------------------------------------- |
| Value type           | String                                                               |
| Supported values     | Hostname (for example, `'google.com'` , `'example.com'` )            |
| Supported operations | `==` , `!=` , `in` , `.startsWith()` , `.endsWith()` , `.contains()` |

`destination.unregistered.path`

|                      |                                                                      |
| -------------------- | -------------------------------------------------------------------- |
| Value type           | String                                                               |
| Supported values     | Request path (for example, `'/admin'` , `'/api/v1'` )                |
| Supported operations | `==` , `!=` , `in` , `.startsWith()` , `.endsWith()` , `.contains()` |

`destination.unregistered.method`

|                      |                                                                       |
| -------------------- | --------------------------------------------------------------------- |
| Value type           | String                                                                |
| Supported values     | HTTP method (for example, `'get'` , `'post'` , `'put'` , `'delete'` ) |
| Supported operations | `==` , `!=` , `in`                                                    |

> **Note:** The `startsWith()` , `endsWith()` , and `contains()` functions (or `STARTS_WITH` , `ENDS_WITH` , and `CONTAINS` ) are supported only for the `destination.unregistered.host` and `destination.unregistered.path` attributes. Other attributes don't support these string functions.

## What's next

  - [CEL attributes for Access policies](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/policies/cel-attributes-uap)
  - [Create IAM Access policies](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/policies/configure-iam-policies-uap)
  - [Manage IAM Access policies](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/policies/manage-iam-policies-uap)
  - [Troubleshoot IAM Access policies](https://docs.cloud.google.com/gemini-enterprise-agent-platform/troubleshooting/troubleshoot-iam-policies-uap)

Codelab

### [Codelab: Secure cross-cloud agentic AI applications](https://codelabs.developers.google.com/next26/aiinfra-learning-pod/screen1-securing-cross-cloud-agentic)

Learn how to secure your agentic applications in the Securing Cross-Cloud Agentic AI Applications codelab.

Overview

### [Agent Gateway overview](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/gateways/agent-gateway-overview)

Get an overview of Agent Gateway.

Guide

### [Security controls](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/security-controls)

Learn about security controls for Google Agent Platform.
