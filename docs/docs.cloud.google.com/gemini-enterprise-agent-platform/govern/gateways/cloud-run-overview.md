---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/govern/gateways/cloud-run-overview
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/gateways/cloud-run-overview
title: Agent Gateway for Cloud Run overview
description: Learn how Agent Gateway governs outbound traffic from AI agents hosted on Cloud Run using Secure Web Proxy, Agent Identity, and Model Armor.
data_source: docs.cloud.google.com
---

> **Limited Preview for Agent Gateway on Cloud Run**
>
> This feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](https://cloud.google.com/terms/service-terms#1) . Pre-GA features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .
>
> This feature is in Limited Preview and is available only to projects on an allowlist. To request early access, [sign up here for the preview](https://docs.google.com/forms/d/e/1FAIpQLSeUpnNRtYQjLRblii-KoUbJJ7DjEV6fvQAfO21IAXgVSqFjpw/viewform) .

Agent Gateway extends Gemini Enterprise Agent Platform governance to AI agents that you build and deploy on Cloud Run. By routing outbound requests from your Cloud Run services through a self-managed Agent Gateway backed by [Secure Web Proxy](https://docs.cloud.google.com/secure-web-proxy/docs/overview) , you can enforce unified access policies, inspect prompts and tool payloads for content safety, and capture logs and traces without changing your agent application code.

For complete step-by-step setup instructions, see [Govern agents with Agent Gateway](https://docs.cloud.google.com/run/docs/securing/agent-gateway-cloud-run) in the Cloud Run documentation.

## Benefits

Using Agent Gateway with Cloud Run provides the following capabilities for your agent workloads:

- Enforce least-privilege access rules on outbound calls to Model Context Protocol (MCP) servers, tools, and external endpoints based on each service's cryptographic [Agent Identity](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/agent-identity-overview) .
- Attach [Model Armor](https://docs.cloud.google.com/model-armor/overview) templates through [Service Extensions](https://docs.cloud.google.com/service-extensions/docs/overview) extension bindings to scan prompts and responses for prompt injection, jailbreaks, and sensitive data leakage.
- Route outbound container traffic with Cloud Run [ambient networking](https://docs.cloud.google.com/run/docs/configuring/ambient-networking) and [Direct VPC egress](https://docs.cloud.google.com/run/docs/configuring/vpc-direct-vpc) without building custom proxy logic into your agent framework.
- Host your gateway in the same Google Cloud project as your Cloud Run service, or share a central gateway across multiple service projects using Shared VPC.
- Monitor policy decisions, MCP tool invocations, and request latency in Cloud Logging and Cloud Trace.

## Key components

A self-managed Agent Gateway deployment for Cloud Run combines the following components:

- **[Cloud Run ambient networking](https://docs.cloud.google.com/run/docs/configuring/ambient-networking)** : Runs a Google-managed Envoy sidecar alongside your agent container to intercept outbound connections and forward them over mTLS.
- **[Secure Web Proxy](https://docs.cloud.google.com/secure-web-proxy/docs/deploy-swp-as-agent-gateway)** : Runs inside your Virtual Private Cloud (VPC) network as the outbound policy enforcement point, performing TLS inspection and evaluating authorization rules and extension bindings.
- **[Agent Identity and Agent Registry](https://docs.cloud.google.com/run/docs/ai/agent-platform-features)** : Assigns a workload-bound SPIFFE identity to your Cloud Run agent and registers agents, MCP servers, and tools in your organization's central inventory.
- **[Identity-Aware Proxy (IAP) and Identity and Access Management (IAM) Unified Access Policies](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/policies/iam-overview-uap)** : Evaluates whether a specific Cloud Run agent identity is authorized to call target MCP servers, tools, or endpoints.
- **[Extension bindings](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/gateways/extension-bindings-overview)** : Binds IAP and Model Armor to your Agent Gateway resource to evaluate outbound requests and responses.

## How it works

When you deploy a Cloud Run service with `--ambient-networking` , `--vpc-egress=all` , `--functional-type=agent` , and `--identity-type=agent-identity` , Cloud Run provisions an ambient Envoy sidecar and assigns an Agent Identity principal to the service.

You create a Network Services API `EgressRouting` policy that directs outbound traffic from your Cloud Run service to a Secure Web Proxy instance associated with your self-managed Agent Gateway resource. The ambient sidecar sends outbound connections over Direct VPC egress through an mTLS `CONNECT` tunnel that carries your agent's identity to Secure Web Proxy.

Secure Web Proxy terminates outbound TLS sessions using a certificate authority from Certificate Authority Service or your private PKI, evaluates `ALLOW` authorization policies for MCP methods and model endpoints, and calls IAP and Model Armor through extension bindings before forwarding approved requests to their destination.

## Supported regions

You can use Agent Gateway on Cloud Run in the following regions:

- `europe-west1`
- `us-central1`

## What's next

- Set up outbound governance for single-project or Shared VPC deployments in [Govern agents with Agent Gateway](https://docs.cloud.google.com/run/docs/securing/agent-gateway-cloud-run) .
- Diagnose routing, xDS permission, TLS inspection, and policy errors in [Troubleshoot Agent Gateway](https://docs.cloud.google.com/run/docs/securing/troubleshoot-agent-gateway) .
- Learn about Agent Identity and automatic registration in [Configure Agent Platform features for Cloud Run](https://docs.cloud.google.com/run/docs/ai/agent-platform-features) .
- Configure the underlying proxy resource in [Deploy Secure Web Proxy as an Agent Gateway](https://docs.cloud.google.com/secure-web-proxy/docs/deploy-swp-as-agent-gateway) .
- View telemetry across runtimes in [Monitor Agent Gateway traffic](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/gateways/monitor-agent-gateway) .
