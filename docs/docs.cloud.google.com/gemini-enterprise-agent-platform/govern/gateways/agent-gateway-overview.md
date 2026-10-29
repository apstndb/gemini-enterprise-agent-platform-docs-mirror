---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/govern/gateways/agent-gateway-overview
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/gateways/agent-gateway-overview
title: Agent Gateway overview
description: Secure and govern AI agent connectivity with Agent Gateway. Centralize access policies, mTLS, and Model Context Protocol (MCP) security for agent-to-agent and agent-to-tool interactions across Agent Runtime on Gemini Enterprise Agent Platform, Gemini Enterprise, Google Kubernetes Engine, Cloud Run, and cross-cloud environments.
data_source: docs.cloud.google.com
---

Agent Gateway is the governance and security enforcement layer for Google Cloud agent governance. It acts as the software-defined network entry and exit point for all agentic interactions across managed runtimes, container platforms, infrastructure-as-a-service (IaaS) virtual machines, and cross-cloud environments.

Agent Gateway gives enterprise security and platform administrators the ability to enforce consistent, least-privilege security postures for all agent interactions—whether occurring between human users and agents, agents and Model Context Protocol (MCP) tools, or among autonomous agents themselves.

![Agent Gateway and Agent Platform ecosystem (click to enlarge).](https://docs.cloud.google.com/static/gemini-enterprise-agent-platform/images/geap-architecture.png)

## Core governance components

The following Agent Platform components work together to provide a unified agent governance architecture:

- **[Agent Identity](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/agent-identity-overview) (Who made the request?)** : Assigns a unique, secure ID (a SPIFFE ID) to each agent. This identity acts as the agent's digital signature for authentication, access control, and auditing.

  Agent identities are secured by default with Context-Aware Access which enforces end-to-end cryptographic authentication by using [mTLS](https://docs.cloud.google.com/access-context-manager/docs/caa-agent-security#mtls) and [DPoP](https://docs.cloud.google.com/access-context-manager/docs/caa-agent-security#dpop) .

- **[Agent Registry](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/agent-registry) (What destinations are approved?)** : Acts as the central directory for all approved agents, tools, Model Context Protocol (MCP) servers, and endpoints (such as essential Google Cloud APIs) in your organization. Agent Gateway uses this directory to check permissions before allowing connections.

- **[Policies](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/policies/overview-uap) (What actions are permitted?)** : Lets you implement rich sets of agentic security and governance policies that control which agents can reach specific resources and what content is allowed to pass through:

  - **[IAM Unified Access Policies](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/policies/iam-overview-uap)** : Access rules that link an agent's identity to approved tools and endpoints in Agent Registry. By default, all connections are blocked unless an explicit IAM policy grants access.
  - **[Model Armor](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/configure-model-armor)** : Content security filters attached to gateways. Model Armor scans user prompts and tool responses in real time to block prompt injection attacks, sensitive data leaks, and harmful content.
  - **[Semantic governance policies](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/policies/semantic-governance-overview)** : Rules written in plain language that control how agents use tools. They enforce business rules at runtime to prevent agents from taking unintended actions, such as running unsafe combinations of tools.
  - **[Token management policies](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/policies/token-management-overview)** : Policies that monitor and attribute large language model (LLM) token usage, and enforce shared token budgets across your agents and applications to prevent runaway token consumption and unexpected cost spikes.
  - **[Custom authorization engines](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/gateways/delegate-authorization)** : Custom authorization extensions that let you delegate authorization decisions to third-party systems by using Service Extensions.

  Internally, all of these policy types are enforced by using [authorization policies](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/gateways/delegate-authorization) or [extension bindings](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/gateways/extension-bindings-overview) managed through Service Extensions.

  > Support for token management policies and extension bindings is coming soon. Features and timing are subject to change. To request early access, [sign up here for early preview access](https://docs.google.com/forms/d/e/1FAIpQLSeUpnNRtYQjLRblii-KoUbJJ7DjEV6fvQAfO21IAXgVSqFjpw/viewform) .

- **[Agent Gateway](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/gateways/agent-gateway-overview) (Where are policies enforced?)** : Serves as the main entry and exit point for network traffic between clients-to-agents and agents-to-anywhere, and applies security and governance policies to all traffic passing through the gateway. To learn more, see [How Agent Gateway enforces policies](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/gateways/agent-gateway-overview#how-policies-are-enforced) .

- **[Agent observability](https://docs.cloud.google.com/gemini-enterprise-agent-platform/optimize/observability/overview)** : Agent Gateway generates observability telemetry for all agent interactions at the network layer and exports it to Agent Observability to provide you with a comprehensive understanding of agent actions.

## Key benefits

Agent Gateway addresses the security, compliance, and networking complexities of operating AI agents at scale across heterogeneous compute runtimes.

For AI developers:

- **Simplified innovation:** Focus on building agent logic without managing underlying VPC routing, Envoy configurations, or mTLS certificate rotation.
- **Protocol mediation:** Seamlessly connect agents using Model Context Protocol (MCP), Agent-to-Agent (A2A), REST, or gRPC while adhering to enterprise governance standards.
- **Framework agnostic:** Support for agents built with standard AI frameworks or custom clients across any runtime environment.
- **Secure transport and identity:** Automatically terminates mTLS handshakes and integrates with Agent Platform's [Agent Identity Auth Manager](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/agent-identity-overview) to transparently handle OAuth 2.0 handshakes and Workload Identity Federation (WIF).

For enterprise security teams and platform administrators:

- **Centralized governance across all runtimes:** Define and enforce unified access policies, tool RBAC, and safety guardrails across managed runtimes, Google Kubernetes Engine (GKE) clusters, Cloud Run services, and non-Google Cloud Kubernetes clusters.
- **AI security guardrails:** Intercept and sanitize inbound prompts and outbound tool payloads using integrated safety providers like Model Armor to block prompt injection, jailbreaks, and sensitive data leakage.
- **Perimeter security & data exfiltration protection:** Direct traffic through private Virtual Private Cloud (VPC) network attachments to enforce strict VPC Service Controls perimeter rules.
- **End-to-end observability:** Capture enriched Layer 7 and Layer 8 OpenTelemetry traces and access logs in Cloud Logging and Cloud Trace for complete auditability.

## Governed access paths

Agent Gateway facilitates two primary governed access paths: **Client-to-Agent** (ingress) and **Agent-to-Anywhere** (egress).

![Agent Gateway modes of operation (click to enlarge).](https://docs.cloud.google.com/static/gemini-enterprise-agent-platform/images/agent-gateway-modes.png)

- **Client-to-Agent (ingress):** Secures communications between clients (such as web applications, developer CLIs, or external systems) and hosted agents or MCP tools. The gateway acts as a frontend policy enforcement point, authenticating incoming user credentials and inspecting prompts.

- **Agent-to-Anywhere (egress):** Governs outbound requests initiated by agents to external tools, remote MCP servers, SaaS APIs, or downstream agents. Enforces workload-bound identity, destination registry compliance, Identity and Access Management (IAM) access policies, and payload sanitization.

## Deployment models

> **Sign up for early preview access**
>
> Agent Gateway is currently available for agents running on Gemini Enterprise Agent Platform. Support for GKE, Cloud Run, and cross-cloud environments will be available soon through an early preview. [Sign up here for early preview access](https://docs.google.com/forms/d/e/1FAIpQLSeUpnNRtYQjLRblii-KoUbJJ7DjEV6fvQAfO21IAXgVSqFjpw/viewform) .

To support diverse AI application architectures, Agent Gateway provides flexible deployment models that determine where and how gateway proxy infrastructure is provisioned, managed, and integrated with your agent workloads. Whether your agents run on fully managed Google Cloud runtimes, self-managed Kubernetes clusters, virtual machines, or cross-cloud environments, Agent Gateway offers a deployment option tailored to your infrastructure control preferences and network perimeter requirements.

![Agent Gateway deployment models across infrastructure boundaries (click to enlarge).](https://docs.cloud.google.com/static/gemini-enterprise-agent-platform/images/agent-gateway-deployment-models.svg)

### Summary of deployment models

| Agent host environment                                                                                                                                               | Supported deployment model                     | Proxy infrastructure                                                                                                                                                               | Documentation                                                                                                                                                                                                                           |
|----------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [Agent Runtime and Gemini Enterprise](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/gateways/agent-gateway-overview#managed-agw)             | Agent Gateway on Google Cloud (Google-managed) | Not applicable (Google-managed)                                                                                                                                                    | [Overview](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/gateways/agent-gateway-managed-overview) [Set up](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/gateways/set-up-agent-gateway) |
| [GKE](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/gateways/agent-gateway-overview#gke-agw)                                                 | Agent Gateway on Google Cloud (Self-managed)   | Client-to-Agent: GKE Gateway API Agent-to-Anywhere for cross-cluster and external connectivity: Secure Web Proxy Agent-to-Anywhere for pod-to-pod connectivity: Ambient networking | [Coming soon](https://docs.google.com/forms/d/e/1FAIpQLSeUpnNRtYQjLRblii-KoUbJJ7DjEV6fvQAfO21IAXgVSqFjpw/viewform)                                                                                                                      |
| [Cloud Run](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/gateways/agent-gateway-overview#cloud-run-agw)                                     | Agent Gateway on Google Cloud (Self-managed)   | Client-to-Agent: Application Load Balancer Agent-to-Anywhere: Secure Web Proxy                                                                                                     | [Coming soon](https://docs.google.com/forms/d/e/1FAIpQLSeUpnNRtYQjLRblii-KoUbJJ7DjEV6fvQAfO21IAXgVSqFjpw/viewform)                                                                                                                      |
| [Cross-cloud environments](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/gateways/agent-gateway-overview#cross-cloud-agw) (non-Google Cloud) | Agent Gateway for cross-cloud                  | Self-managed Envoy proxy in your environment                                                                                                                                       | [Coming soon](https://docs.google.com/forms/d/e/1FAIpQLSeUpnNRtYQjLRblii-KoUbJJ7DjEV6fvQAfO21IAXgVSqFjpw/viewform)                                                                                                                      |

### Agent Gateway on Google Cloud

Agent Gateway on Google Cloud governs agents and MCP servers that run on Google Cloud compute environments, including Agent Runtime, Gemini Enterprise, GKE, and Cloud Run. Depending on your host environment, Google either manages the gateway proxy infrastructure for you, or you attach Agent Gateway to proxy and load-balancing resources that you manage in your own project. Across all Google Cloud runtimes, you use the same central control plane to manage agent identities, Agent Registry entries, and access policies.

#### For Agent Runtime and Gemini Enterprise

Agent Gateway provides fully Google-managed, zero-maintenance gateway infrastructure hosted directly within Google Cloud. It is optimized specifically for agents running on Agent Runtime and Gemini Enterprise.

- **Architecture & infrastructure:** Google fully manages both the gateway management services and proxy infrastructure. Organizations require no proxy setup, container management, or manual maintenance overhead.
- **Key capabilities:** Provides built-in zero-maintenance mTLS termination, IAP access policies, Model Armor prompt scanning and DLP, and Semantic governance policies.
- **Primary use case:** Ideal for enterprise teams building serverless AI agents on Google Cloud who want comprehensive governance without managing network infrastructure.

For setup details, see [Agent Gateway on Agent Platform overview](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/gateways/agent-gateway-managed-overview) .

#### For GKE

Agent Gateway extends Agent Platform governance to agents and MCP servers that you run on your own GKE clusters. Platform teams configure governance with Kubernetes-native resources and the Google Kubernetes Engine Gateway API. The same Agent Identity, Agent Registry, and policies that govern agents on Agent Runtime also apply to agents on GKE.

- **Architecture and infrastructure:** You run the proxy infrastructure in your own project.
  - **Client-to-Agent:** Client traffic enters your cluster through a GKE Gateway, which is a regional Application Load Balancer.
  - **Agent-to-Anywhere:** GKE ambient networking redirects outbound agent traffic to Secure Web Proxy without sidecars, and policies are enforced before traffic leaves the cluster. Agent-to-agent traffic within the cluster is governed by Layer 7 ambient proxies that run per namespace.
- **Key capabilities:** Kubernetes-native policy configuration, identity-based access control using each agent's SPIFFE identity, Model Armor screening of prompts and responses, TLS inspection of outbound agent traffic, and custom policy engines through extension bindings.
- **Primary use case:** Platform and security teams that run agents on GKE and want to govern inbound, outbound, and in-cluster agent traffic with the Kubernetes tooling they already use.

Agent Gateway support for GKE agents is coming soon. Features and timing are subject to change. To request early access, [sign up for preview](https://docs.google.com/forms/d/e/1FAIpQLSeUpnNRtYQjLRblii-KoUbJJ7DjEV6fvQAfO21IAXgVSqFjpw/viewform) .

#### For Cloud Run

Agent Gateway extends Agent Platform governance to agents and MCP servers that you deploy on Cloud Run. You attach Agent Gateway to Google Cloud networking infrastructure that you already manage in your project. Secure Web Proxy governs your agents' outbound traffic, and an Application Load Balancer governs inbound traffic to your agents. Agent Gateway enforces policies on both paths based on agent and caller identity, without changes to your agent code.

- **Architecture and infrastructure:** You run the proxy infrastructure in your own project.

  - **Client-to-Agent:** For Client-to-Agent traffic, clients reach your agents through a regional Application Load Balancer, either external for internet clients or internal for clients in your VPC network. Agent Gateway is attached to the load balancer, so it authenticates and checks every inbound request before the request reaches the agent.
  - **Agent-to-Anywhere:** For Agent-to-Anywhere traffic, Cloud Run ambient networking intercepts outbound traffic from your agent container. It then forwards that traffic over Direct VPC egress through a mutually authenticated (mTLS) tunnel that carries the agent's identity, to a Secure Web Proxy instance in your VPC network that acts as the policy enforcement point.

  You create and manage the Secure Web Proxy and load balancer resources, and keep control of your VPC network, certificates, and network perimeter.

- **Key capabilities:** Identity-based access policies for outbound calls to tools, models, and APIs, authentication and authorization of inbound callers through Identity-Aware Proxy (IAP), Model Armor screening of prompts, responses, and tool payloads in both directions, TLS inspection of outbound traffic with a certificate authority that you control, and one central set of policies across many Cloud Run services, with custom policy engines through extension bindings.

- **Primary use case:** Security and platform teams that run agents on Cloud Run and need centralized governance of inbound and outbound agent traffic. This includes organizations that require security enforcement on infrastructure that's separate from the application runtime, and organizations that route traffic through a hub-and-spoke VPC network for inspection.

Agent Gateway support for Cloud Run agents is coming soon. Features and timing are subject to change. To request early access, [sign up for preview](https://docs.google.com/forms/d/e/1FAIpQLSeUpnNRtYQjLRblii-KoUbJJ7DjEV6fvQAfO21IAXgVSqFjpw/viewform) .

### Agent Gateway for cross-cloud

Agent Gateway for cross-cloud extends Agent Platform governance to agents that run on Kubernetes clusters outside Google Cloud, such as Amazon EKS, Azure AKS, Red Hat OpenShift, or clusters in your own data centers. You manage governance centrally in Google Cloud, and policies are enforced inside your own cluster.

- **Architecture and infrastructure:** Google Cloud hosts the management plane, where you define agent identities, registry entries, and policies. You deploy a lightweight, Envoy-based Agent Gateway and its supporting components into your Kubernetes cluster. You're responsible for your cluster's networking, including routing agent traffic to the gateway. Agent traffic stays in your environment. Only the policy checks that you configure, such as Model Armor screening, call out to Google Cloud.
- **Key capabilities:** Governance of Agent-to-Anywhere traffic from your agents, exchange of Kubernetes workload credentials for Agent Identity credentials through workload identity federation, and enforcement of policies that you define centrally, such as Model Armor. It also extends Agent Registry and Agent Observability (access logs and traces) to agents outside Google Cloud.
- **Primary use case:** Enterprises that run agents across multiple clouds or in their own data centers and want one set of governance policies, one registry, and one view of agent activity for all of their agents.

Agent Gateway for cross-cloud is coming soon. Features and timing are subject to change. To request early access, [sign up for preview](https://docs.google.com/forms/d/e/1FAIpQLSeUpnNRtYQjLRblii-KoUbJJ7DjEV6fvQAfO21IAXgVSqFjpw/viewform) .

## Supported protocols

Agent Gateway supports standard HTTP-based agentic communication protocols across all deployment models, including:

- **Model Context Protocol (MCP):** Governs outbound and inbound MCP tool calls over Server-Sent Events (SSE) or HTTP POST requests.
- **Agent-to-Agent (A2A):** Governs inter-agent delegation and task execution APIs.
- **REST and gRPC:** Supports HTTP/1.1 and HTTP/2 (gRPC) traffic across GKE, Cloud Run, and cross-cloud deployments.

For MCP traffic, Agent Gateway inspects JSON-RPC requests to extract tool names and method attributes, enabling fine-grained tool access policies across all deployment models. For details, see [Authorization based on MCP attributes](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/gateways/delegate-authorization#mcp-attributes) .

## Limitations

- Each Agent Gateway instance can govern up to 5,000 resources registered in Agent Registry.
- Review the following pages to learn about limitations associated with your chosen deployment model and features:
  - [Agent Runtime](https://docs.cloud.google.com/gemini-enterprise-agent-platform/scale/runtime/agent-gateway-runtime-deploy#limitations)
  - [Authorization policies](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/gateways/delegate-authorization#limitations)
  - [VPC connectivity](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/gateways/set-up-vpc-connectivity)

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
