---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/govern/gateways/agent-gateway-managed-overview
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/gateways/agent-gateway-managed-overview
title: Agent Gateway for Runtime and Gemini Enterprise
description: Overview of Agent Gateway for Google-managed runtimes, including Agent Runtime on Gemini Enterprise Agent Platform and Gemini Enterprise. Learn how Agent Gateway enforces ingress and egress access policies, mTLS, and Model Armor security.
data_source: docs.cloud.google.com
---

Agent Gateway for Agent Platform provides fully managed traffic governance and security enforcement for AI agents deployed in Agent Runtime and Gemini Enterprise.

In this deployment model, Google hosts and manages all gateway infrastructure, allowing you to define access rules, mTLS termination, and safety guardrails without managing gateway hosting infrastructure.

## Supported access paths

The governed access paths available in Agent Gateway on Agent Platform depends on your agent runtime platform:

- **[Agent Runtime](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/runtime) :** Supports both **Client-to-Agent** (ingress) and **Agent-to-Anywhere** (egress) modes.
- **[Gemini Enterprise](https://docs.cloud.google.com/gemini/enterprise/docs/agents-overview) :** Supports **Agent-to-Anywhere** (egress) mode only.

![Agent Gateway modes of operation (click to enlarge).](https://docs.cloud.google.com/static/gemini-enterprise-agent-platform/images/agent-gateway-modes.png)

The following table summarizes the governance controls supported for Agent Gateway for each access path:

The following table summarizes the role played by each governance component for each governed access path:

| Governance layer                 | Client-to-Agent                                                                                  | Agent-to-Anywhere                                                                                                             |
|----------------------------------|--------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------|
| **Identity**                     | Client identity or user credentials passed by the client to the gateway.                         | Workload-bound *agent identity* (SPIFFE ID or WIF token) assigned to the agent.                                               |
| **Agent Registry**               | Not applicable for Client-to-Agent mode.                                                         | Registers outbound target destination resources (tools, MCP servers, agents).                                                 |
| **Access control policies**      |                                                                                                  |                                                                                                                               |
| **IAM Unified Access Policies**  | Evaluated at the gateway based on incoming client identity and target agent.                     | Evaluated by Identity-Aware Proxy (IAP) and Principal Access Boundary (PAB) policies based on agent identity and destination. |
| **Model Armor guardrails**       | Scans inbound client prompts in real time for prompt injection, jailbreaks, and harmful content. | Inspects outgoing tool payloads and agent responses to prevent sensitive data leakage.                                        |
| **Semantic governance policies** | Evaluates natural language constraints against client requests.                                  | Evaluates natural language constraints against outbound tool actions and agent delegations.                                   |

## How Agent Gateway enforces policies

Traffic passing through Agent Gateway undergoes specific policy evaluations depending on the direction of traffic. The following sections outline the sequence of events for inbound and outbound requests passing through Agent Gateway.

![Access control with Agent Gateway (click to enlarge).](https://docs.cloud.google.com/static/gemini-enterprise-agent-platform/images/agent-gateway-access-control.png)

### Client-to-Agent enforcement

In Client-to-Agent mode (supported only for agents deployed in Agent Runtime), a request to an agent governed by Agent Gateway undergoes the following sequence of events:

1.  **Client request** : A client (such as a CLI, web application, or developer tool) sends a request to the agent. The request is intercepted by an Agent Gateway operating in Client-to-Agent mode which acts as the agent's frontend.
2.  **Request inspection** : Agent Gateway evaluates the request using the authorization policy attached to the gateway.
    - **Model Armor** : Scans the inbound user prompt in real time to block prompt injection attacks, jailbreaks, and harmful content.
    - **Semantic governance policy** (if configured instead of Model Armor): Evaluates natural language constraints against the inbound request.
3.  **Request forwarding** : If all checks pass, Agent Gateway forwards the request to the target destination in Agent Runtime.

### Agent-to-Anywhere enforcement

When an agent running in Agent Runtime or Gemini Enterprise sends an outbound call to an external tool, MCP server, or another agent, the request undergoes the following sequence of events:

1.  **Outbound request and interception** : The agent (identified by its assigned *agent identity* ) sends an outbound call. The request is intercepted by Agent Gateway operating in Agent-to-Anywhere mode.

2.  **IAM, Principal Access Boundary, and IAP policy verification** : IAP verifies that there is an IAM access policy that grants the agent identity the `iap.resources.egressViaIAP` permission to access the destination. Any Principal Access Boundary policies applied to the agent identity are also evaluated. Agent identities that are subject to Principal Access Boundary policies are only eligible to access the resources specified in those policies, strictly isolating the agent to its designated access boundary.

3.  **Agent Registry verification** : Agent Gateway verifies that the target destination resource is registered in Agent Registry (or resolves the target endpoint URL if the destination is unregistered). Registering destinations in Agent Registry is recommended to enforce granular, per-resource access policies and tool-level controls. If the destination is not registered in Agent Registry, then there must be an explicit IAM access policy targeting the destination URL. By default, if no matching access policy exists, the request is denied.

4.  **Request inspection** : If the previous checks pass, Agent Gateway evaluates the request against any of these other safety guardrails you might have configured:

    - **Model Armor** : Inspects tool payloads and agent responses for prompt injection and sensitive data leakage.
    - **Semantic governance policies** : Evaluate natural language constraints (NLC) against tool invocations and agent actions.
    - **Delegate authorization to a custom authorization engine** : You can delegate authorization decisions to a custom authorization engine by using Service Extensions. Depending on the configured authorization policy, one or more of these authorization engines may allow or deny the request.

5.  **Request forwarding** : If all checks pass, Agent Gateway forwards the request to the target destination.

## Deploy Agent Gateway on Agent Platform

To deploy and configure Agent Gateway for Google-managed runtimes, follow the general setup topics to configure gateway infrastructure and access policies, and then refer to the runtime-specific guides to route traffic from your agent workloads.

### General setup and policy configuration

- **[Set up Agent Gateway](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/gateways/set-up-agent-gateway) :** Learn how to create `agentGateways` resources, assign agent identities, register destination tools in Agent Registry, and attach access policies.
- **[Set up Agent Gateway with VPC connectivity](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/gateways/set-up-vpc-connectivity) :** Learn how to configure private VPC connectivity so that Agent Gateway can send outbound traffic to resources in your VPC network.
- **[Delegate authorization](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/gateways/delegate-authorization) :** Learn how to configure authorization policies and extensions to delegate traffic decisions to IAP, Model Armor, Semantic governance policies, or custom Service Extensions engines.

### Runtime-specific traffic routing

- **[Route Runtime traffic through Agent Gateway](https://docs.cloud.google.com/gemini-enterprise-agent-platform/scale/runtime/agent-gateway-runtime-deploy) :** Learn how to configure Agent Runtime agents to route inbound (Client-to-Agent) and outbound (Agent-to-Anywhere) traffic through Agent Gateway.
- **[Route Gemini Enterprise traffic through Agent Gateway](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/gateways/agent-gateway-ge-deploy) :** Learn how to configure Gemini Enterprise apps to route traffic through Agent Gateway when connecting to external tools and APIs.

## Limitations

The following limitations apply to Agent Gateway for Agent Platform:

- For Gemini Enterprise, Client-to-Agent mode is not supported.
- Each Agent Gateway instance can govern up to 5,000 resources registered in Agent Registry.
- Review the following pages to learn about limitations associated with your chosen deployment and features:
  - [Agent Runtime](https://docs.cloud.google.com/gemini-enterprise-agent-platform/scale/runtime/agent-gateway-runtime-deploy#limitations)
  - [Authorization policies](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/gateways/delegate-authorization#limitations)
  - [VPC connectivity](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/gateways/set-up-vpc-connectivity)

## What's next

Guide

### [Monitor Agent Gateway](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/gateways/monitor-agent-gateway)

Learn how to monitor Agent Gateway.

Guide

### [Set up an Agent Gateway](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/gateways/set-up-agent-gateway)

Learn how to set up an Agent Gateway.

Troubleshooting

### [Troubleshoot Agent Gateway](https://docs.cloud.google.com/gemini-enterprise-agent-platform/troubleshooting/troubleshoot-agent-gateway)

Learn how to troubleshoot Agent Gateway connectivity.
