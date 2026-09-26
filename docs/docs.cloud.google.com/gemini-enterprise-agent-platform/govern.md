---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/govern
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern
title: Govern your agents
description: Learn how to use Agent Platform to govern your AI agents at scale.
data_source: docs.cloud.google.com
---

Gemini Enterprise Agent Platform provides a full suite of capabilities for the complete agentic development lifecycle, to help agent developers and enterprises Build, Scale, Govern, and Optimize their agentic applications.

Governance provides the framework for discovering, securing, and auditing AI agents and their underlying infrastructure at scale. As organizations deploy complex agentic workflows, the Govern suite of capabilities serves as the centralized command center for administrators and security teams to maintain oversight.

![Agent Platform governance ecosystem (click to enlarge).](https://docs.cloud.google.com/static/gemini-enterprise-agent-platform/images/geap-architecture.png)

## Core governance components

The following Agent Platform components work together to provide a unified governance architecture:

  - **[Agent Identity](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/agent-identity-overview) (Who made the request?)** : Assigns a unique, secure ID (a SPIFFE ID) to each agent. This identity acts as the agent's digital signature for authentication, access control, and auditing.
    
    Agent identities are secured by default with Context-Aware Access which enforces end-to-end cryptographic authentication by using [mTLS](https://docs.cloud.google.com/access-context-manager/docs/caa-agent-security#mtls) and [DPoP](https://docs.cloud.google.com/access-context-manager/docs/caa-agent-security#dpop) .

  - **[Agent Registry](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/agent-registry) (What destinations are approved?)** : Acts as the central directory for all approved agents, tools, Model Context Protocol (MCP) servers, and endpoints (such as essential Google Cloud APIs) in your organization. Agent Gateway uses this directory to check permissions before allowing connections.

  - **[Policies](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/policies/overview-uap) (What actions are permitted?)** : Lets you implement rich sets of agentic security and governance policies that control which agents can reach specific resources and what content is allowed to pass through:
    
      - **[IAM Unified Access Policies](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/policies/iam-overview-uap)** : Access rules that link an agent's identity to approved tools and endpoints in Agent Registry. By default, all connections are blocked unless an explicit IAM policy grants access.
      - **[Model Armor](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/configure-model-armor)** : Content security filters attached to gateways. Model Armor scans user prompts and tool responses in real time to block prompt injection attacks, sensitive data leaks, and harmful content.
      - **[Semantic Governance Policies](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/policies/semantic-governance-overview)** : Rules written in plain language that control how agents use tools. They enforce business rules at runtime to prevent agents from taking unintended actions, such as running unsafe combinations of tools.
      - **[Custom authorization engines](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/gateways/delegate-authorization)** : Custom authorization extensions that let you delegate authorization decisions to third-party systems by using Service Extensions.
    
    Internally, all of these policy types are enforced by using [authorization policies managed through Service Extensions](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/gateways/delegate-authorization) .

  - **[Agent Gateway](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/gateways/agent-gateway-overview) (Where are policies enforced?)** : Serves as the main entry and exit point for network traffic between clients-to-agents, and agents-to-anywhere. It manages encrypted connections (mTLS), translates protocols (such as MCP, REST, and gRPC), and applies policy checks to all traffic. To learn more, see [How Agent Gateway enforces policies](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/gateways/agent-gateway-overview#how-policies-are-enforced) .

  - **[Agent Observability](https://docs.cloud.google.com/gemini-enterprise-agent-platform/optimize/observability/overview)** : Agent Gateway generates observability telemetry for all agent interactions at the network layer and exports it to Agent Observability to provide you with a comprehensive understanding of agent actions.

## Recommended order of configuration

To ensure a smooth deployment process, we recommend that you follow this sequence when setting up a governed Agent Platform environment:

1.  **Provision Agent Identities** : Provision workload identities (SPIFFE IDs) for your agents. For instructions, see [Agent identities](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/agent-identity-overview) .

2.  **Register destinations in Agent Registry** : Register target tools, MCP servers, endpoints, and agents in Agent Registry. For instructions, see [Agent Registry](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/agent-registry) .

3.  **Configure IAM policies** : Define IAM access policies that grant agent identities (SPIFFE IDs) access to essential platform APIs and your registered destinations. For instructions, see [Configure IAM access policies](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/policies/configure-iam-policies-uap) .
    
    > **Tip:** For testing in audit mode, set `iamEnforcementMode: "DRY_RUN"` in the authorization policy metadata block to log evaluations without blocking access. Set `iamEnforcementMode: "ENFORCED"` (or remove the `iamEnforcementMode` parameter) to enable active enforcement.

4.  **Configure Model Armor templates** : Set up content security templates to inspect prompt payloads and tool responses for prompt injections, jailbreaks, and sensitive data leaks. For instructions, see [Configure Model Armor](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/configure-model-armor) .
    
    > **Tip:** For testing in audit mode, set `enforcement_type: "INSPECT_ONLY"` in the authorization policy metadata block to log findings without blocking requests. Set `enforcement_type: "INSPECT_AND_BLOCK"` to start active enforcement.

5.  **Configure Semantic Governance policies** : Define natural language constraints that regulate tool usage and prevent unsafe tool combinations at runtime. For instructions, see [Configure Semantic Governance policies](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/policies/configure-semantic-governance) .
    
    > **Tip:** For testing in audit mode, you can set `sgpEnforcementMode: "DRY_RUN"` in the authorization policy metadata block to evaluate constraints in log-only mode. Remove the `sgpEnforcementMode` parameter to enforce natural language rules at runtime.

6.  **Deploy Agent Gateway and monitor traffic** : Deploy Agent Gateway to begin intercepting traffic. If you enabled any of the access control mechanisms in audit mode, check the logs in Cloud Logging to confirm that access is being evaluated as expected before transitioning your policies to active enforcement posture. For instructions, see [Set up Agent Gateway](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/gateways/set-up-agent-gateway) .

## Agent Registry, safety, and sharing

Overview

### [Agent Registry](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/agent-registry)

Agent Registry is a centralized catalog that lets you store, discover, and govern servers, tools, and AI agents in Google Cloud.

Overview

### [Agent Identity](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/agent-identity-overview)

Agent identity allows agents to securely authenticate to cloud resources, endpoints, and other agents, acting as themselves or on behalf of the end user.

Guide

### [Share an agent](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/share-agent)

Learn how to share an agent.

Guide

### [Safety](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/safety)

Ensure your agents are safe and reliable using Google Agent Platform.

Guide

### [View agent relationships](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/topology)

View real-time relationships and traffic flows across all agents and MCP servers known to Agent Registry.

## Policies

Guide

### [Configure semantic governance policies](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/policies/configure-semantic-governance)

Semantic Governance policies add an additional security layer to ensure agent actions match user intent and organizational constraints.

Overview

### [Policies overview](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/policies/overview)

Get an overview of policies in Google Agent Platform.

## Agent Gateway

Guide

### [Route Agent Runtime traffic through Agent Gateway](https://docs.cloud.google.com/gemini-enterprise-agent-platform/scale/runtime/agent-gateway-runtime-deploy)

Learn how to route Agent Runtime traffic through Agent Gateway for secure and governed connectivity.

Codelab

### [Codelab: Govern agentic workloads with Agent Platform](https://codelabs.developers.google.com/cloudnet-agent-gateway)

Learn how to govern agentic workloads with Agent Gateway on Gemini Enterprise Agent Platform.

Codelab

### [Codelab: Agent Gateway egress from Agent Runtime to Google MCP servers](https://codelabs.developers.google.com/agw-cuj-arun-egress-gmcp)

Learn about Agent Gateway egress governance for AI agents accessing Google Cloud Model Context Protocol (MCP) servers.

Codelab

### [Codelab: Agent Gateway egress from Agent Runtime to external MCP servers](https://codelabs.developers.google.com/agw-cuj-arun-egress-emcp)

Learn about Agent Gateway egress governance for AI agents accessing external MCP servers.

Codelab

### [Codelab: Agent Gateway egress from Agent Runtime to VPC networks](https://codelabs.developers.google.com/agw-cuj-arun-egress-vpc)

Learn about Agent Gateway egress governance for AI agents accessing destinations in a VPC network.

Codelab

### [Codelab: Agent Gateway governance with cross-project Agent Runtime](https://codelabs.developers.google.com/agw-multiproject)

Learn about Agent Gateway governance for cross-project Agent Runtime agents.

Codelab

### [Codelab: Agent Gateway egress from Gemini Enterprise to custom MCP servers](https://codelabs.developers.google.com/agw-ge-custom-mcp-egress-vpc-registry)

Learn about setting up private Agent Gateway egress governance for Gemini Enterprise.

Overview

### [Agent Gateway overview](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/gateways/agent-gateway-overview)

Get an overview of Agent Gateway.

Guide

### [Delegate authorization for Agent Gateway](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/gateways/delegate-authorization)

Learn how to delegate authorization for Agent Gateway to IAP, Model Armor, or your own custom authorization service.

Guide

### [Monitor Agent Gateway](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/gateways/monitor-agent-gateway)

Learn how to monitor Agent Gateway.

Guide

### [Set up an Agent Gateway](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/gateways/set-up-agent-gateway)

Learn how to set up an Agent Gateway.

Troubleshooting

### [Troubleshoot Agent Gateway](https://docs.cloud.google.com/gemini-enterprise-agent-platform/troubleshooting/troubleshoot-agent-gateway)

Learn how to troubleshoot Agent Gateway connectivity.

Guide

### [Route Gemini Enterprise traffic through Agent Gateway](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/gateways/agent-gateway-ge-deploy)

Learn how to route Gemini Enterprise traffic through Agent Gateway.

## Security

Codelab

### [Codelab: Secure cross-cloud agentic AI applications](https://codelabs.developers.google.com/next26/aiinfra-learning-pod/screen1-securing-cross-cloud-agentic)

Learn how to secure your agentic applications in the Securing Cross-Cloud Agentic AI Applications codelab.

Resource

### [Whitepaper: Building secure multi-agent systems on Google Cloud](https://goo.gle/agent-security-enterprise)

Learn how to build secure multi-agent architectures on Google Cloud's Gemini Enterprise Agent Platform.

Guide

### [View security findings](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/view-security-findings)

Learn how to view security findings.

Guide

### [Configure Model Armor on a gateway](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/configure-model-armor)

Learn how to configure Model Armor on a gateway.

Guide

### [Monitor content security](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/monitor-content-security)

Learn how to monitor content security.

Guide

### [View Model Armor spans](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/view-model-armor-spans)

Learn how to view Model Armor spans.
