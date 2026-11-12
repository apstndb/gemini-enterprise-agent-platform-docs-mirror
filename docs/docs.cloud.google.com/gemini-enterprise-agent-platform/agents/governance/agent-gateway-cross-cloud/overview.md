---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/agents/governance/agent-gateway-cross-cloud/overview
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/agents/governance/agent-gateway-cross-cloud/overview
title: Agent Gateway for cross-cloud overview
description: Learn how Agent Gateway for cross-cloud extends Gemini Enterprise Agent Platform governance to Kubernetes clusters outside of GKE.
data_source: docs.cloud.google.com
---

> **Preview**
>
> This feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](https://docs.cloud.google.com/terms/service-terms#1) . Pre-GA features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

> **Request access:** Agent Gateway for cross-cloud is available in Limited Preview. To use this feature, complete the [access request form](https://docs.google.com/forms/d/e/1FAIpQLSeUpnNRtYQjLRblii-KoUbJJ7DjEV6fvQAfO21IAXgVSqFjpw/viewform) .

Agent Gateway for cross-cloud extends Gemini Enterprise Agent Platform governance to any Cloud Native Computing Foundation (CNCF)-conformant Kubernetes cluster outside of Google Kubernetes Engine (GKE). Examples include on-premises Red Hat OpenShift clusters, clusters in bare-metal environments, and clusters in third-party clouds like Amazon Elastic Kubernetes Service (Amazon EKS) and Azure Kubernetes Service (AKS).

Agent Gateway for cross-cloud uses a decoupled three-plane architecture:

- **SaaS management plane** : A Google Cloud-hosted central plane for [Agent Registry](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/agent-registry) , [Model Armor](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/configure-model-armor) , [Identity-Aware Proxy (IAP)](https://docs.cloud.google.com/iap/docs/concepts-overview) , [Workload Identity Federation](https://docs.cloud.google.com/iam/docs/workload-identity-federation-with-kubernetes) , and [Google Cloud Observability](https://docs.cloud.google.com/stackdriver/docs) .
- **Cross-cloud control plane** : A globally co-owned xDS control plane and an in-cluster controller ( `agent-governance-cross-cloud-controller` ). The controller watches services, workloads, and custom resources in your cluster and synchronizes them with Google Cloud for agent registration and gateway configuration.
- **Satellite data plane** : Dedicated Envoy proxies ( [Agent Gateway](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/gateways/agent-gateway-overview) for cross-cloud proxies) that you manage in your Kubernetes namespaces. Each proxy runs with an Agent Identity Runtime (AIR) sidecar that brokers workload identities and certificates for the proxy.

## Shared responsibility model

Agent Gateway for cross-cloud integrates with your existing network stack without requiring you to replace your current infrastructure. This approach provides flexibility while maintaining centralized governance.

- **Google's responsibility** : Google manages the SaaS management plane and the cross-cloud control plane routing configuration. Google also provides standard Helm charts for deploying the Agent Gateway for cross-cloud proxies and satellite components.

- **Your responsibility** : You are responsible for your cluster and network configuration outside of Google Cloud, including the following tasks:

  - Forwarding traffic into the Agent Gateway for cross-cloud proxies using your existing service mesh or network stack.
  - Injecting Kubernetes Service Account (KSA) tokens for identity federation.
  - Ensuring outbound network connectivity from in-cluster control plane and data plane components to Google Cloud APIs. For details, see [Allow outbound connectivity to Google APIs](https://docs.cloud.google.com/gemini-enterprise-agent-platform/agents/governance/agent-gateway-cross-cloud/setup#allow-egress) .
  - Protecting your Google Cloud project and registered cluster resources from accidental deletion.

## Identity-first zero trust

Agent Gateway for cross-cloud enforces identity-first zero-trust policies. You define Model Armor and IAP policies centrally in Google Cloud, and the proxy in your cluster enforces them for each request.

## Pricing

During Limited Preview, Agent Gateway for cross-cloud is available at no charge. However, the other Google Cloud products that you configure with Agent Gateway for cross-cloud, such as Model Armor, Cloud Logging, and Cloud Trace, are billed at their standard rates. For details, see the following pricing pages:

- [Model Armor pricing](https://cloud.google.com/security-command-center/pricing#model-armor-pricing)
- [Cloud Logging and Cloud Trace pricing](https://cloud.google.com/stackdriver/pricing)

## Known issues

Agent Gateway for cross-cloud has the following known issues during Limited Preview:

- **Fail-open behavior** : The `failOpen: true` setting on extension bindings doesn't apply when the proxy can't reach Google Cloud, or when a binding references a Model Armor template that doesn't exist. For details, see [Configure Model Armor](https://docs.cloud.google.com/gemini-enterprise-agent-platform/agents/governance/agent-gateway-cross-cloud/enforce-policies#configure-model-armor) .
- **Gateway readiness** : A gateway can report that it's ready up to two minutes before it accepts connections on port `8443` . For details, see [Create the gateway](https://docs.cloud.google.com/gemini-enterprise-agent-platform/agents/governance/agent-gateway-cross-cloud/setup#create-gateway) .
- **Agent Registry URL uniqueness** : In-cluster service URLs must be unique across all clusters that are registered to the same project. For details, see [Label workloads for auto-registration](https://docs.cloud.google.com/gemini-enterprise-agent-platform/agents/governance/agent-gateway-cross-cloud/deploy-agents#annotate-workloads) .

## What's next

- [Set up Agent Gateway for cross-cloud](https://docs.cloud.google.com/gemini-enterprise-agent-platform/agents/governance/agent-gateway-cross-cloud/setup)
- [Deploy and register cross-cloud agents](https://docs.cloud.google.com/gemini-enterprise-agent-platform/agents/governance/agent-gateway-cross-cloud/deploy-agents)
- [Enforce cross-cloud governance policies](https://docs.cloud.google.com/gemini-enterprise-agent-platform/agents/governance/agent-gateway-cross-cloud/enforce-policies)
- [Configure cross-cloud agent observability](https://docs.cloud.google.com/gemini-enterprise-agent-platform/agents/governance/agent-gateway-cross-cloud/observability)
