---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/govern/gateways/agent-gateway-overview
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/gateways/agent-gateway-overview
title: Agent Gateway overview
description: Secure and govern AI agent connectivity with Agent Gateway. Centralize access policies, mTLS, and Model Context Protocol (MCP) security for agent-to-agent and agent-to-tool interactions across diverse runtimes.
data_source: docs.cloud.google.com
---

Agent Gateway is the key enforcement component of Agent Platform. It acts as the network entry and exit point for all agentic interactions. It gives enterprise security administrators the ability to secure connectivity for all agentic interactions, whether they occur between users and agents, agents and tools, or among agents themselves.

![Agent Gateway and Agent Platform ecosystem (click to enlarge).](https://docs.cloud.google.com/static/gemini-enterprise-agent-platform/images/geap-architecture.png)

## Core governance components

The following Agent Platform components work together to provide a unified governance architecture:

  - **[Agent Identity](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/gateways/agent-identity-overview) (Who made the request?)** : Assigns a unique, secure ID (a SPIFFE ID) to each agent. This identity acts as the agent's digital signature for authentication, access control, and auditing.
    
    Agent identities are secured by default with Context-Aware Access which enforces end-to-end cryptographic authentication by using [mTLS](https://docs.cloud.google.com/access-context-manager/docs/caa-agent-security#mtls) and [DPoP](https://docs.cloud.google.com/access-context-manager/docs/caa-agent-security#dpop) .

  - **[Agent Registry](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/gateways/agent-registry) (What destinations are approved?)** : Acts as the central directory for all approved agents, tools, Model Context Protocol (MCP) servers, and endpoints (such as essential Google Cloud APIs) in your organization. Agent Gateway uses this directory to check permissions before allowing connections.

  - **[Policies](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/policies/overview-uap) (What actions are permitted?)** : Lets you implement rich sets of agentic security and governance policies that control which agents can reach specific resources and what content is allowed to pass through:
    
      - **[IAM Unified Access Policies](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/policies/iam-overview-uap)** : Access rules that link an agent's identity to approved tools and endpoints in Agent Registry. By default, all connections are blocked unless an explicit IAM policy grants access.
      - **[Model Armor](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/configure-model-armor)** : Content security filters attached to gateways. Model Armor scans user prompts and tool responses in real time to block prompt injection attacks, sensitive data leaks, and harmful content.
      - **[Semantic Governance Policies](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/policies/semantic-governance-overview)** : Rules written in plain language that control how agents use tools. They enforce business rules at runtime to prevent agents from taking unintended actions, such as running unsafe combinations of tools.
      - **[Custom authorization engines](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/gateways/delegate-authorization)** : Custom authorization extensions that let you delegate authorization decisions to third-party systems by using Service Extensions.
    
    Internally, all of these policy types are enforced by using [authorization policies managed through Service Extensions](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/gateways/delegate-authorization) .

  - **[Agent Gateway](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/gateways/agent-gateway-overview) (Where are policies enforced?)** : Serves as the main entry and exit point for network traffic between clients-to-agents, and agents-to-anywhere. It manages encrypted connections (mTLS), translates protocols (such as MCP, REST, and gRPC), and applies policy checks to all traffic. To learn more, see [How Agent Gateway enforces policies](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/gateways/agent-gateway-overview#how-policies-are-enforced) .

  - **[Agent Observability](https://docs.cloud.google.com/gemini-enterprise-agent-platform/optimize/observability/overview)** : Agent Gateway generates observability telemetry for all agent interactions at the network layer and exports it to Agent Observability to provide you with a comprehensive understanding of agent actions.

## Key benefits

Agent Gateway offers several benefits for both AI developers and enterprise administrators, addressing the complexities of securing and managing AI agent interactions at scale.

For AI developers:

  - **Simplified innovation:** Developers can focus on building agents without managing complex networking primitives or security overhead.
  - **Protocol mediation:** Developers can seamlessly use their choice of agentic protocols such Model Context Protocol (MCP), Agent-to-Agent(A2A), REST, and gRPC while adhering to enterprise security standards.
  - **Framework agnostic:** Functionality is available regardless of the development framework or client used.
  - **Secure transport and authentication:** Automatically handles mTLS handshakes and termination to ensure encrypted connectivity between agents and tools without developer effort. Integrates with Agent Platform's [Agent Identity Auth Manager](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/agent-identity-overview) to simplify and secure Oauth 2.0 handshakes between their agents and tools.

For enterprise admins and security teams:

  - **Centralized governance for all agent interactions:** Configure and enforce consistent access policies across diverse agent runtimes and deployment models, ensuring enforcement of least-privilege permissions for agents at runtime.
  - **AI security guardrails:** Protect against novel risks like Model Context Protocol (MCP) prompt injection attacks using integrated services like Model Armor.
  - **Comprehensive observability:** Gain deep visibility into agentic interactions through Cloud Logging and Cloud Trace, facilitating security investigations and performance monitoring.
  - **Perimeter security and data exfiltration protection:** Enforce VPC Service Controls service perimeters for agent communications. When you configure Agent Gateway with an [agent connectivity template](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/gateways/set-up-vpc-connectivity) , agent traffic is routed through your private VPC network attachment, ensuring that your organization's VPC Service Controls perimeter rules are applied to all agent traffic as well.

## Deployment modes

Agent Gateway is a networking abstraction that lets you define rules for agent communication and enforces safety, security, and access control policies, without requiring you to manage complex networking details.

Agent Gateway facilitates two primary governed access paths: **Client-to-Agent** interactions and **Agent-to-Anywhere** interactions.

![Agent Gateway modes of operation (click to enlarge).](https://docs.cloud.google.com/static/gemini-enterprise-agent-platform/images/agent-gateway-modes.png)

  - **Client-to-Agent (ingress)** : This mode is used to secure communications between clients (such as Cursor, Claude Code, Gemini CLI) and agents (and tools) running on Google Cloud. In this mode, Agent Gateway acts as a frontend for your agent and lets you control which clients can access your agents (and tools) and which security policies must be applied to such interactions.

  - **Agent-to-Anywhere (egress)** : This mode is used to secure communications between agents running on Google Cloud and servers, agents, tools, or APIs running anywhere. For example, Agent Gateway can be used to enforce access permissions and security guardrails for your agents that need to communicate with MCP servers that are either created and hosted by your own organization, or remote MCP servers hosted by third-parties.

The applicability of each governance component and policy layer varies depending on the direction of traffic:

| Governance layer                            | Client-to-Agent (ingress)                                                                                                                 | Agent-to-Anywhere (egress)                                                                                        |
| ------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------- |
| **Identity**                                | Client identity or user credentials passed by the client to the Agent Gateway.                                                            | Workload-bound *agent identity* (SPIFFE ID) assigned to the agent.                                                |
| **Agent Registry**                          | Not available for ingress.                                                                                                                | Registers outbound target destination resources such as tools, MCP servers, and other agents.                     |
| **IAM Unified Access Policies**             | Not available for ingress.                                                                                                                | Enforced at runtime by IAP based on the agent's SPIFFE ID and the destination resource that the agent is calling. |
| **Model Armor** (Optional)                  | Inspects client prompts for inbound prompt injection attacks and harmful content.                                                         | Inspects outgoing tool payloads and agent responses for data leakage and prompt injection.                        |
| **Semantic Governance policies** (Optional) | Evaluates natural language constraints against inbound client requests (cannot be combined with Model Armor on the same ingress gateway). | Evaluates natural language constraints against outbound tool calls and agent actions.                             |

## How Agent Gateway enforces policies

Traffic passing through Agent Gateway undergoes specific policy evaluations depending on the direction of traffic. The following sections outline the sequence of events for ingress and egress requests.

![Access control with Agent Gateway (click to enlarge).](https://docs.cloud.google.com/static/gemini-enterprise-agent-platform/images/agent-gateway-access-control.png)

### Client-to-Agent enforcement

In Client-to-Agent mode (supported only for agents deployed in Agent Runtime), a request to an agent governed by Agent Gateway undergoes the following sequence of events:

1.  **Client request** : A client (such as a CLI, web application, or developer tool) sends a request to the agent. The request is intercepted by an Agent Gateway operating in Client-to-Agent mode which acts as the agent's frontend.
2.  **Request inspection** : Agent Gateway evaluates the request using the authorization policy attached to the gateway.
      - **Model Armor** : Scans the inbound user prompt in real time to block prompt injection attacks, jailbreaks, and harmful content.
      - **Semantic Governance policy** (if configured instead of Model Armor): Evaluates natural language constraints against the inbound request.
3.  **Request forwarding** : If all checks pass, Agent Gateway forwards the request to the target destination in Agent Runtime.

### Agent-to-Anywhere enforcement

When an agent running in Agent Runtime or Gemini Enterprise sends an outbound call to an external tool, MCP server, or another agent, the request undergoes the following sequence of events:

1.  **Outbound request and interception** : The agent (identified by its assigned *agent identity* ) sends an outbound call. The request is intercepted by Agent Gateway operating in Agent-to-Anywhere mode.

2.  **IAM and IAP policy verification** : IAP verifies that there is an IAM access policy that grants the agent identity the `iap.resources.egressViaIAP` permission to access the destination.

3.  **Agent Registry verification** : Agent Gateway verifies that the target destination resource is registered in Agent Registry (or resolves the target endpoint URL if the destination is unregistered). Registering destinations in Agent Registry is recommended to enforce granular, per-resource access policies and tool-level controls. If the destination is not registered in Agent Registry, then there must be an explicit IAM access policy targeting the destination URL. By default, if no matching access policy exists, the request is denied.

4.  **Request inspection** : If the previous checks pass, Agent Gateway evaluates the request against any of these other safety guardrails you might have configured:
    
      - **Model Armor** : Inspects tool payloads and agent responses for prompt injection and sensitive data leakage.
      - **Semantic Governance policies** : Evaluate natural language constraints (NLC) against tool invocations and agent actions.
      - **Delegate authorization to a custom authorization engine** : You can delegate authorization decisions to a custom authorization engine by using Service Extensions. Depending on the configured authorization policy, one or more of these authorization engines may allow or deny the request.

5.  **Request forwarding** : If all checks pass, Agent Gateway forwards the request to the target destination.

## Supported agent runtimes

Agent Gateway lets you govern traffic for agents and tools running on the following runtime platforms:

  - **[Agent Runtime](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/runtime)** : Agent Gateway supports both Agent-to-Anywhere (egress) and Client-to-Agent (ingress) modes.

  - **[Gemini Enterprise](https://docs.cloud.google.com/gemini/enterprise/docs/agents-overview)** : Agent Gateway supports only Agent-to-Anywhere (egress) mode.

For details on planning a deployment with these runtimes, see [Plan your Agent Gateway deployment](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/gateways/set-up-agent-gateway#plan-agw) .

## Supported protocols

Agent Gateway supports all HTTP-based traffic, including MCP and A2A traffic. At a minimum, the gateway acts as a passthrough that securely terminates and routes incoming traffic.

For MCP traffic only, Agent Gateway can parse request data to extract attributes. This lets you create authorization policies with conditions based on those attributes. For example, you can create policies that restrict access to specific tools. For details, see [Authorization based on MCP attributes](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/gateways/delegate-authorization#mcp-attributes) .

## Limitations

  - For Gemini Enterprise, Client-to-Agent mode is not supported by Agent Gateway.
  - Agent Gateway doesn't support connections to public or private destinations with self-signed certificate chains. Use publicly trusted CA certificates for all destinations.
  - Each Agent Gateway instance can govern up to 5,000 resources registered in Agent Registry.
  - Review the [limitations](https://docs.cloud.google.com/gemini-enterprise-agent-platform/scale/runtime/agent-gateway-runtime-deploy#limitations) associated with Agent Runtime.
  - Review the [limitations](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/gateways/delegate-authorization#limitations) associated with authorization policies.

## API and gcloud reference

For details about the methods available for Agent Gateway, see the following reference topics:

  - gcloud reference: [`gcloud network-services agent-gateways`](https://docs.cloud.google.com/sdk/gcloud/reference/network-services/agent-gateways)
  - REST API reference: [agentGateways](https://docs.cloud.google.com/service-mesh/docs/reference/network-services/rest/v1/projects.locations.agentGateways)

## What's next

Codelab

### [Codelab: Govern agentic workloads with Agent Platform](https://codelabs.developers.google.com/cloudnet-agent-gateway)

Learn how to govern agentic workloads with Agent Gateway on Gemini Enterprise Agent Platform.

Overview

### [Agent Gateway partners](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/gateways/agw-partners)

Explore the ecosystem of identity and AI security providers integrating with Agent Gateway.

Guide

### [Set up an Agent Gateway](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/gateways/set-up-agent-gateway)

Learn how to set up an Agent Gateway.

Troubleshooting

### [Troubleshoot Agent Gateway](https://docs.cloud.google.com/gemini-enterprise-agent-platform/troubleshooting/troubleshoot-agent-gateway)

Learn how to troubleshoot Agent Gateway connectivity.
