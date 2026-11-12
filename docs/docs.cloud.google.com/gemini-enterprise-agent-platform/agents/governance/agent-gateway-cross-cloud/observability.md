---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/agents/governance/agent-gateway-cross-cloud/observability
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/agents/governance/agent-gateway-cross-cloud/observability
title: Configure cross-cloud agent observability
description: Configure observability and telemetry for Agent Gateway for cross-cloud using Agent Gateway access logs and Cloud Logging.
data_source: docs.cloud.google.com
---

> **Preview**
>
> This feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](https://docs.cloud.google.com/terms/service-terms#1) . Pre-GA features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

> **Request access:** Agent Gateway for cross-cloud is available in Limited Preview. To use this feature, complete the [access request form](https://docs.google.com/forms/d/e/1FAIpQLSeUpnNRtYQjLRblii-KoUbJJ7DjEV6fvQAfO21IAXgVSqFjpw/viewform) .

This guide explains how to configure observability and telemetry for [Agent Gateway for cross-cloud](https://docs.cloud.google.com/gemini-enterprise-agent-platform/agents/governance/agent-gateway-cross-cloud/overview) in Gemini Enterprise Agent Platform.

Cross-cloud agent observability is enabled by default through an OpenTelemetry (OTel) collector, which sends access logs and agent telemetry to Cloud Logging and Cloud Trace. The collector runs in the `geap-system` namespace. It receives Layer 8 (L8) agentic signals for large language model (LLM), Model Context Protocol (MCP), and Agent-to-Agent (A2A) traffic, and exports them with each agent's Agent Identity.

## View Agent Gateway access logs

Agent Gateway for cross-cloud writes an access log entry to Cloud Logging for every request that passes through the gateway. The entries use the `networkservices.googleapis.com/AgentGateway` resource type.

To read the access logs, run the following command:

```
gcloud logging read \
    'resource.type="networkservices.googleapis.com/AgentGateway"
    resource.labels.location="LOCATION"
    logName="projects/PROJECT_ID/logs/networkservices.googleapis.com%2Fagent_gateway_hybrid_access"' \
    --project=PROJECT_ID
```

Replace the following:

- `LOCATION` : the region where you [registered the cluster](https://docs.cloud.google.com/gemini-enterprise-agent-platform/agents/governance/agent-gateway-cross-cloud/setup#register-cluster) .
- `PROJECT_ID` : your Google Cloud project ID.

## Configure agents to emit traces

You can configure your agents to emit trace spans that follow the OpenTelemetry [semantic conventions for generative AI agent spans](https://opentelemetry.io/docs/specs/semconv/gen-ai/gen-ai-agent-spans/) . The OTel collector forwards these spans to Cloud Trace.

To send spans to the collector, configure your agent's OTel exporter to use one of the following OTLP endpoints. The collector accepts OTLP over both gRPC and HTTP:

- **gRPC** : `http://gboc.geap-system.svc.cluster.local:4317`
- **HTTP** : `http://gboc.geap-system.svc.cluster.local:4318`

Many OTel SDKs read the `OTEL_EXPORTER_OTLP_ENDPOINT` and `OTEL_EXPORTER_OTLP_PROTOCOL` environment variables. For example, to export over gRPC:

```
env:
- name: OTEL_EXPORTER_OTLP_ENDPOINT
  value: "http://gboc.geap-system.svc.cluster.local:4317"
- name: OTEL_EXPORTER_OTLP_PROTOCOL
  value: "grpc"
```

To export over HTTP:

```
env:
- name: OTEL_EXPORTER_OTLP_ENDPOINT
  value: "http://gboc.geap-system.svc.cluster.local:4318"
- name: OTEL_EXPORTER_OTLP_PROTOCOL
  value: "http/protobuf"
```

The agent that emits the telemetry must be [registered in Agent Registry](https://docs.cloud.google.com/gemini-enterprise-agent-platform/agents/governance/agent-gateway-cross-cloud/deploy-agents#annotate-workloads) .

## What's next

- [Review the Agent Gateway for cross-cloud overview](https://docs.cloud.google.com/gemini-enterprise-agent-platform/agents/governance/agent-gateway-cross-cloud/overview)
- [Enforce cross-cloud governance policies](https://docs.cloud.google.com/gemini-enterprise-agent-platform/agents/governance/agent-gateway-cross-cloud/enforce-policies)
- [Monitor Agent Gateway traffic](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/gateways/monitor-agent-gateway)
- [View agent traces](https://docs.cloud.google.com/gemini-enterprise-agent-platform/optimize/observability/traces)
