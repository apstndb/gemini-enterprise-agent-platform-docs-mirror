---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/govern/gateways/gke-overview
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/gateways/gke-overview
title: Agent Gateway for GKE overview
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

> **Preview**
>
> This product or feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](https://docs.cloud.google.com/terms/service-terms#1) . Pre-GA products and features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

When you deploy autonomous AI agents on Google Kubernetes Engine (GKE), those workloads connect to external resources such as Model Context Protocol (MCP) servers, SaaS APIs, and other agents.

Because AI agents determine their execution paths dynamically based on user prompts, their network dependencies change in real time. Agent Gateway provides a centralized governance model to secure, manage, and monitor this dynamic agent traffic.

This document is intended for platform engineers who manage and secure GKE infrastructure, and for developers who build and deploy AI agents on GKE.

## Why use Agent Gateway?

Agent Gateway for GKE offers a consistent user experience for governing self-managed, GKE-hosted agents, with central enforcement of governance and access policies across all agent interactions throughout your fleet.

- **Apply semantic context:** enforce Zero Trust principles. The Gateway moves beyond firewall rules, accounting for the semantic context, intent, and payload content (prompts/responses) of every interaction.
- **Compound authorization:** solve the "identity imperative." Security models can handle compound authorizations, enforcing policies that validate both the agent's identity (is the code trusted?) and the user's identity (does the person have permission?) whenever agents act on a user's behalf.
- **AI guardrails:** to protect workloads from prompt injection, jailbreaks, and data exfiltration, the Gateway integrates with Google Cloud Model Armor. Using Extension bindings, you can attach request and response sanitization templates to Gateways to evaluate payloads before they reach agents or external targets.
- **Automated encryption:** the Gateway uses the sidecar-less GKE ambient proxy and other networking services to automate mTLS handshakes, TLS termination, and inspection between Gateways and agent workloads, requiring no code changes or custom certificate management.
- **Turnkey observability:** governed agents automatically surface rich telemetry, including session tracing with interactive waterfall traces that display execution paths, stack traces, attributes, and step-by-step inputs and outputs.

## Key concepts

Understanding the following concepts and products is fundamental to working with Agent Gateway on GKE:

- **[GKE ambient proxy](https://docs.cloud.google.com/kubernetes-engine/docs/how-to/prepare-ambient-networking) :** a sidecar-less service mesh data plane that simplifies GKE networking. You use it to automate mutual TLS (mTLS) and intercept outbound agent traffic.
- **[Secure Web Proxy (SWP)](https://docs.cloud.google.com/secure-web-proxy/docs/overview) :** a transparent forward proxy used to enforce security policies and perform TLS inspection on your agents' outbound traffic.
- **[GKE Gateway](https://docs.cloud.google.com/kubernetes-engine/docs/concepts/gateway-api) :** the GKE implementation of the Kubernetes Gateway API, used to provision Application Load Balancers for inbound client-to-agent traffic.
- **[Model Armor](https://docs.cloud.google.com/security-command-center/docs/model-armor-overview) :** an AI security service used to sanitize incoming prompts and outgoing responses to protect against prompt injection and data exfiltration.
- **[Identity-Aware Proxy (IAP)](https://docs.cloud.google.com/iap/docs/concepts-overview) :** a service that establishes a central authorization layer, used here to enforce access policies for traffic egressing through the Secure Web Proxy.
- **[Agent Identity](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/agent-identity-overview) :** the secure, workload-bound SPIFFE ID assigned to your agents, used for authentication and access control.
- **[Agent Registry](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/agent-registry) :** the central directory for all approved agents, Model Context Protocol (MCP) servers, and tools in your organization.
- **[Extension binding](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/gateways/extension-bindings-overview) :** the mechanism used to attach customizable authorization and content security extensions (like Model Armor) to your Agent Gateway to evaluate payloads.

## How it works

You compose Agent Gateway with Google Cloud networking services to secure specific agentic interaction flows across ingress and egress traffic patterns.

- **Egress (Agent-to-Anywhere):** securely route your agents' outbound requests to external services, tools, and other agents. You configure the GKE ambient proxy to intercept and redirect traffic through a Google Cloud Secure Web Proxy (SWP). SWP enforces your security policies, performs TLS inspection, and lets you delegate access decisions to Google Cloud Identity-Aware Proxy (IAP) (IAP) or custom extensions.
- **Ingress (Client-to-Agent or MCP Server):** manage how external clients and Google-hosted services interact with your self-managed agents in a GKE cluster. You provision standard Google Cloud Application Load Balancers (GKE Gateway) and use Kubernetes custom resources to apply comprehensive guardrails. You use `GCPAuthzPolicy` to enforce identity, metadata, and MCP tool RBAC controls, and `GCPExtensionBinding` for payload evaluation and delegated guardrails (like Model Armor).

## Supported versions and regions

Your cluster must run GKE version 1.37.2-gke.1042000 or later, which is available in the Rapid release channel.

Additionally, you can use Agent Gateway for GKE only in the following regions:

- `europe-west1`
- `us-central1`

## When to use Agent Gateway

Use Agent Gateway if you are deploying self-managed AI agents on GKE clusters and need to accomplish any of the following:

- Secure and govern how your agents interact with users, other agents, and external tools and services.
- Maintain a strict security posture without slowing down your developers.
- Monitor the performance, behavior, and health of your agents.
- Automate complex networking tasks, including mutual TLS (mTLS) and TLS inspection.
- Apply AI-specific guardrails, such as prompt sanitization.

## Prerequisites and requirements

Before you configure ingress or egress governance, complete the following prerequisites:

1.  Enable the required APIs:

    ```
    gcloud services enable \
        agentregistry.googleapis.com \
        certificatemanager.googleapis.com \
        gkehub.googleapis.com \
        iap.googleapis.com \
        modelarmor.googleapis.com \
        networksecurity.googleapis.com \
        networkservices.googleapis.com \
        privateca.googleapis.com \
        serviceextensions.googleapis.com
    ```

2.  Create a new GKE cluster configured for ambient networking. Your cluster must run GKE version 1.37.2-gke.1042000 or later, which is available in the Rapid release channel.

    To create a Standard cluster with all required features enabled, run the following command:

    ```
    gcloud beta container clusters create CLUSTER_NAME \
        --machine-type=e2-standard-4 \
        --enable-ambient-networking \
        --enable-dataplane-v2 \
        --enable-fleet \
        --gateway-api=standard \
        --location=LOCATION \
        --release-channel=rapid \
        --workload-pool=PROJECT_ID.svc.id.goog
    ```

    Replace the following:

    - `CLUSTER_NAME` : the name of your cluster.
    - `LOCATION` : the region or zone of your cluster.
    - `PROJECT_ID` : your Google Cloud project ID.

3.  Configure `kubectl` to communicate with your cluster:

    ```
    gcloud container clusters get-credentials CLUSTER_NAME \
        --location=LOCATION
    ```

    Replace the following:

    - `CLUSTER_NAME` : the name of your cluster.
    - `LOCATION` : the region or zone of your cluster.

## What's next

- To register your agents with Agent Registry, see [Register GKE-hosted agents](https://docs.cloud.google.com/agent-registry/register-agents) .
- To secure and govern your agents' outbound traffic, see [Set up agent egress governance on GKE](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/gateways/set-up-gke-egress) .
- To secure and govern your agents' inbound traffic, see [Set up agent ingress governance on GKE](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/gateways/set-up-gke-ingress) .
- To monitor your agents' traffic and behavior, see [Monitor Agent Gateway traffic](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/gateways/monitor-agent-gateway) .
