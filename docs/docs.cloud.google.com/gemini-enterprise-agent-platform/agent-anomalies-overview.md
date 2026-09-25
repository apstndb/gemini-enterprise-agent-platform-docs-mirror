---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/agent-anomalies-overview
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/agent-anomalies-overview
title: Agent Anomaly Detection overview
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

> **Preview**
> 
> This product is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](https://cloud.google.com/terms/service-terms#1) and the [Generative AI Service Specific Terms](https://cloud.google.com/terms/service-terms#20) , as well as the [Additional Terms for Generative AI Preview Products](https://cloud.google.com/trustedtester/aitos?e=48754805) .
> 
> When you use this product with AI Agents, the terms applicable to AI Agents in the Agreement apply.
> 
> Pre-GA products are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

> **Caution:** This product is available to approved users that are signed in to their browser with an allowlisted email address. To request access to use this product, read this page to understand the prerequisites and complete the form at the bottom of this page.

Agent Anomaly Detection provides a dynamic, reasoning-based oversight and audit layer designed specifically for autonomous enterprise AI agents. Unlike conventional application security tools that only scan static code for vulnerabilities or inspect network traffic at the perimeter, Agent Anomaly Detection evaluates the live reasoning traces, tool interactions, and execution flows of agents to detect suspicious intent, policy violations, and behavioral anomalies.

The core of Agent Anomaly Detection is a multi-layered anomaly analysis framework that analyzes agent session activity asynchronously. By ingesting OpenTelemetry logs and execution traces, the service determines whether an agent is operating outside of its intended boundaries without introducing execution latency into your live agent workflows.

## Key benefits

Agent Anomaly Detection includes these features:

| Benefit or Feature                           | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| :------------------------------------------- | :--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Asynchronous near real-time security**     | Telemetry (logs and traces) is processed out-of-band, maintaining fast agent response times. A multi-layered analysis model allows for maintaining cost efficiency with near real-time assessments.                                                                                                                                                                                                                                                                                                                    |
| **Reasoning-based intent analysis**          | Anomaly analysis reasons over flagged traces to differentiate complex business logic from unauthorized action.                                                                                                                                                                                                                                                                                                                                                                                                         |
| **Comprehensive threat detection**           | Audits agent-specific security risks out of the box with default detectors that capture [threat patterns outlined in the OWASP Top 10 for Agentic Security Threats](https://docs.cloud.google.com/gemini-enterprise-agent-platform/agent-anomalies-overview#threat-categories) , including tool misuse, privilege abuse, cascading agent failures, rogue behaviors, and resource exhaustion.                                                                                                                           |
| **Integration with Security Command Center** | Anomaly findings are surfaced directly in Security Command Center for centralized security management, search, and incident tracking. For information on Security Command Center, see [Overview of Security Command Center](https://docs.cloud.google.com/security-command-center/docs/activate-scc-overview) . **Note:** This integration requires one of the [Security Command Center](https://docs.cloud.google.com/security-command-center/docs/service-tiers) -supported tiers: Standard, Premium, or Enterprise. |

## Multi-layered detection system

To balance assessment coverage and cost, Agent Anomaly Detection uses a multi-layered detection system that analyzes agent logs to identify and report on anomalous sessions:

  - **Layer 1 (Lightweight ML detectors)** : High-speed statistical and lightweight machine learning models identify initial outliers and downstream telemetry trends to down-sample baseline traffic.
  - **Layer 2 (Anomaly analysis)** : Anomaly analysis evaluates flagged sessions asynchronously to render threat verdicts and natural language explanation reasoning.
  - **Layer 3 (Invocation-level analysis)** : Performs a deep-dive analysis of individual tool executions, execution states, and parameter histories within the conversation trace.

## Availability

Agent Anomaly Detection is available for agents meeting the following criteria. Agents that meet the criteria are automatically recognized as **monitored agents** by Agent Anomaly Detection (the service is aware of the agent's existence, but nothing is run on the agent's logs and no costs are incurred). You must explicitly **enable** a monitored agent for Agent Anomaly Detection for active anomaly analysis to run on its logs and traces.

  - **Compatible runtime** : Deployed on the Agent Runtime.
  - **ADK version** : Built using Agent Development Kit (ADK) for Python, version 1.2 or later. Version 2.1.0 or later is recommended.
  - **Logging and observability buckets** : Agent Anomaly Detection is currently available for US (multi-region) buckets. Both the logging and observability buckets must be in the same region.
  - **Telemetry capture** : OpenTelemetry tracing and logging are enabled using the ADK.
  - **Metadata capture** : Raw telemetry is configured to capture prompt input and response output contents.
  - **Active tracing** : The `enable_tracing` flag is not explicitly set to `false` in the ADK configuration.
  - **Permissions and access** : Regional scanners' service accounts hold sufficient reader permissions over the active logs and observability buckets. The log bucket should have [Log Analytics and Observability Analytics enabled](https://docs.cloud.google.com/logging/docs/log-analytics) .
  - **Active data flow** : The agent must have active data; the system cannot verify configuration or enroll an agent that has no telemetry data.

Agents that don't meet these criteria aren't discoverable by Agent Anomaly Detection and don't appear in the list of monitored agents to enable.

## Threat categories

Agent Anomaly Detection continuously monitors agent activities and flags risks across key categories aligned with agentic security frameworks:

  - **Tool misuse (OWASP ASI02)** : Detects when tools are used in unsafe or unintended ways, such as through dangerous tool chaining, parameter manipulation, or indirect prompt injection.
  - **Identity privilege abuse (OWASP ASI03)** : Identifies unauthorized actions resulting from dynamic trust delegation, persona forgery, memory escalation, or confused deputy vulnerabilities.
  - **Agentic cascading failures (OWASP ASI08)** : Monitors fault propagation, infinite execution loops, oscillating retries, and feedback loop amplifications across agent workflows.
  - **Rogue agents (OWASP ASI10)** : Flags when an agent abandons its declared role, bypasses safety guardrails, or deviates from assigned system instructions.
  - **Resource exhaustion** : Detects intentional or runaway over-consumption of compute, LLM tokens, or network bandwidth.

## Opt-in to try Agent Anomaly Detection

To opt-in to try Agent Anomaly Detection, complete this form: [Agent Anomaly Detection access request form](https://forms.gle/rS5haEt4mHPFnRqe9) .

## Use Agent Anomaly Detection

If you're already opted in to use Agent Anomaly Detection, see [Agent Anomaly Detection](https://docs.cloud.google.com/gemini-enterprise-agent-platform/audit/agent-anomalies) for usage instructions.
