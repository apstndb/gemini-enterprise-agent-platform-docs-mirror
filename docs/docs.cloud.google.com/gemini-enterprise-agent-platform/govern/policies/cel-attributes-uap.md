---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/govern/policies/cel-attributes-uap
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/policies/cel-attributes-uap
title: CEL attributes for IAM Access policies
description: Reference guide for Common Expression Language (CEL) attributes and functions available for Identity and Access Management access policy rules in Agent Platform.
data_source: docs.cloud.google.com
---

This document describes the Common Expression Language (CEL) attributes and functions that you can use when writing conditional expressions in IAM Unified Access Policies (Access policies) for Agent Gateway.

To learn more about Access policy concepts, see [IAM Access policies overview](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/policies/iam-overview-uap) . To learn how to configure Access policies, see [Create IAM Access policies](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/policies/configure-iam-policies-uap) .

## Available CEL attributes

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

  - [Create IAM Access policies](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/policies/configure-iam-policies-uap)
  - [Manage IAM Access policies](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/policies/manage-iam-policies-uap)
  - [Troubleshoot IAM Access policies](https://docs.cloud.google.com/gemini-enterprise-agent-platform/troubleshooting/troubleshoot-iam-policies-uap)

Overview

### [Agent Gateway overview](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/gateways/agent-gateway-overview)

Get an overview of Agent Gateway.

Guide

### [Configure content and business policies](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/policies/configure-semantic-governance)

Learn how to configure content and business policies.

Guide

### [Test policies](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/policies/test-policies)

Learn how to test policies.
