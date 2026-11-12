---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/optimize/observability/overview
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/optimize/observability/overview
title: Observability overview
description: Overview of observability features in Gemini Enterprise Agent Platform.
data_source: docs.cloud.google.com
---

Agent observability in Gemini Enterprise Agent Platform provides comprehensive visibility into the performance, behavior, and health of your deployed agents and Model Context Protocol (MCP) servers. By monitoring key metrics, tracing execution paths, and observing your multi-agent system as a whole, you can diagnose issues, optimize resource consumption, and improve the reliability of your agents.

This document provides an overview of the observability tools available within Gemini Enterprise Agent Platform, including system-wide topology, individual agent monitoring, and MCP server metrics.

## Telemetry setup

To populate these observability dashboards, topologies, and traces, your agents must be configured to send telemetry data in the OpenTelemetry format to storage systems in Google Cloud Observability.

Ensure your agent and MCP server environments are properly configured to emit this data. Built-in Google Cloud components automatically emit telemetry in the OpenTelemetry format. For example, Model Armor natively emits standardized telemetry, allowing you to seamlessly expose and monitor real-time policy interceptions directly within your trace data without requiring any custom instrumentation.

For agent telemetry setup instructions and requirements, see the following resources:

- To instrument agents built with the ADK, see [Instrument ADK applications with OpenTelemetry](https://docs.cloud.google.com/stackdriver/docs/instrumentation/ai-agent-adk) .
- To instrument agents on Agent Runtime on Gemini Enterprise Agent Platform that were not built with ADK, see [Observability for AI agent developers](https://docs.cloud.google.com/stackdriver/docs/opentelemetry/ai-agent-developers) .
- For MCP server telemetry, see [Use Cloud Trace to monitor MCP tool use](https://docs.cloud.google.com/mcp/monitor-mcp-tool-use-with-cloud-trace) .
- For Model Armor telemetry, see [Configure Model Armor logging](https://docs.cloud.google.com/model-armor/configure-logging) .

## Observability signals

Gemini Enterprise Agent Platform provides observability through metrics, traces, and logs.

When you select a specific agent from the Registry, the **Observability** tab provides a suite of targeted dashboards to monitor its operational health, performance, and infrastructure utilization. Use the left-hand navigation within the **Observability** tab to switch between the following views:

- **Overview:** Tracks high-level usage over your selected timeframe, including total sessions, average turns per session, and total agent invocations. Time-series charts display token usage (input versus output), overall agent traffic volume, latency percentiles (p50, p95, p99), and error rates.
- **Evaluation:** Displays online monitors for continuous quality assessment. This includes time-series widgets tracking average response quality, safety metrics, hallucination rates, and tool use quality.
- **Models:** Breaks down performance by the underlying foundation model. You can monitor p95 latency, total call counts, error rates, quota failures, and token usage isolated by specific models.
- **Tools:** Monitors the external tools and services connected to the agent. This view details p95 latency, call counts, and error rates per tool, as well as the frequency of interactions where no tool was called.
- **Usage:** Provides infrastructure-level metrics for the agent's runtime environment, including container CPU allocation, container memory allocation, and token usage.
- **Logs:** Displays a filterable stream of raw agent logs, including severity, timestamps, and execution summaries for deep-dive troubleshooting. For more information, see [View agent logs](https://docs.cloud.google.com/gemini-enterprise-agent-platform/scale/runtime/logging#view-logs) .

In addition to the dashboards on the **Observability** tab, you can use the agent's **Traces** tab to inspect the step-by-step execution of specific sessions, including directed acyclic graphs of spans and inputs/outputs. For more information, see [View Agent Traces](https://docs.cloud.google.com/gemini-enterprise-agent-platform/optimize/observability/traces) . You can also use the **Topology** tab to view the specific inbound and outbound dependencies for that single agent.

For MCP servers, you can monitor request count and p95 request duration to track utilization and responsiveness.

## Auditing agent actions

To support enterprise security and compliance audits, Gemini Enterprise Agent Platform uses *dual-attribution logging* to record agent activity in Cloud Logging. When an agent performs an action or calls a tool on behalf of a person (user-delegated authority), audit and execution logs record both the SPIFFE-based [agent identity](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/agent-identity-overview#spiffe-identity) ( `principal://...` in audit logs, or `spiffe://...` in execution logs) and the identity of the initiating human user. When an agent acts autonomously on its own authority, logs attribute the action directly to the unique agent identity.

Auditors and security administrators can isolate and review agent-initiated events in Cloud Logging by filtering for the `is_agentic=true` flag in log queries. Combining `is_agentic=true` with the agent identity or user principal lets you trace end-to-end execution paths and verify policy enforcement across all agent interactions.

### Emergency stop and policy propagation expectations

When responding to a security incident or anomalous agent behavior, Agent Platform provides two complementary layers for stopping agent activity:

- **Immediate runtime termination or traffic rerouting** : Deleting a deployed agent on Agent Runtime ( `runtimes.delete` or `reasoningEngines.delete` ) immediately terminates its container instances, stops active sessions and streaming invocations, and permanently invalidates its SPIFFE agent identity once the delete operation completes. Alternatively, you can reroute 100% of root traffic to a known-good revision using `trafficSplitManual` or archive pre-existing revisions by updating `spec.deployment_spec.agent_gateway_config` .
- **Policy-based access revocation** : Adding a `DENY` rule to Unified Access Policies (UAPs) (UAPs) enforced by Agent Gateway ( `iamEnforcementMode: "ENFORCE"` ), or applying an Identity and Access Management (IAM) (IAM) deny policy or role revocation, blocks outbound tool and API calls while preserving the runtime container for forensic analysis. However, UAPs and IAM policy updates are eventually consistent: direct policy changes typically take effect within 2 minutes, but can take up to 7 minutes or longer to propagate globally (see [Access change propagation](https://docs.cloud.google.com/iam/docs/access-change-propagation) ), and `principalSet` or group membership updates can take several minutes to hours to synchronize. Policy updates evaluate on new authorization checks and don't forcibly close already-established streaming connections unless re-authorized.

For an immediate kill switch during an active incident, delete the agent runtime or reroute its revision traffic in addition to applying a policy deny rule. For step-by-step instructions, see [Emergency stop and access revocation](https://docs.cloud.google.com/gemini-enterprise-agent-platform/scale/runtime/manage-deployed-agents#emergency-stop) .

### Telemetry and security finding latency

Different observability and security controls operate on different ingestion and evaluation schedules. Understanding these latency expectations helps incident responders distinguish between inline enforcement and asynchronous threat detection.

The following table summarizes the evaluation model and expected latency for each telemetry and security signal in Agent Platform:

| Signal or control                                                                                                                                                                                                 | Evaluation and ingestion model                                                                                                                                          | Typical latency                                                                                                                                                                                                                                                                                                                                           |
|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Cloud Audit Logs and Agent Gateway request logs** ( `cloudaudit.googleapis.com/*` , `networkservices.googleapis.com/gateway_requests` )                                                                         | Generated synchronously when API calls and gateway authorization checks are evaluated, then ingested into Logging.                                                      | Near real time (typically searchable in Logs Explorer within seconds). Narrow CLI freshness filters such as `--freshness=6h` can occasionally miss recently indexed entries; use `--freshness=1d` when verifying recent events.                                                                                                                           |
| **Agent Runtime execution logs** ( `aiplatform.googleapis.com/reasoning_engine_stdout` , `reasoning_engine_stderr` )                                                                                              | Streamed asynchronously from the runtime container to Logging.                                                                                                          | Typically visible within seconds of emission.                                                                                                                                                                                                                                                                                                             |
| **Distributed traces in Cloud Trace**                                                                                                                                                                             | Exported asynchronously as OpenTelemetry spans complete, subject to configured `samplingRate` and `parentBasedSampling` rules.                                          | Typically searchable within seconds of span completion.                                                                                                                                                                                                                                                                                                   |
| **Cloud Monitoring metrics**                                                                                                                                                                                      | Sampled periodically from Agent Runtime, Agent Gateway, and anomaly detection pipelines.                                                                                | Sampled every 60 to 120 seconds, with a visibility delay of up to 180 to 420 seconds in Metrics Explorer and dashboards.                                                                                                                                                                                                                                  |
| **Inline policy enforcement** (Agent Gateway, Identity-Aware Proxy, Model Armor)                                                                                                                                  | Evaluated synchronously on the live request path before a tool call, MCP request, or model prompt completes.                                                            | Real-time inline interception (zero post-processing delay).                                                                                                                                                                                                                                                                                               |
| **[Agent Anomaly Detection](https://docs.cloud.google.com/gemini-enterprise-agent-platform/agent-anomalies-overview) and Security Command Center (Security Command Center) findings** ( `AGENT_SESSION_ANOMALY` ) | Evaluated asynchronously out-of-band across a multi-layered detection pipeline after session logs and traces are ingested, adding zero latency to live agent responses. | Initial scope enablement takes approximately 40 minutes. Anomaly metrics are sampled every 120 seconds (up to 420 seconds visibility delay), and additional synchronization latency applies before confirmed findings appear in [Security Command Center](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/view-security-findings) . |

### Tamper-evident retention for audit logs

Cloud Audit Logs entries are immutable by design: after Logging writes an audit log entry, its payload and metadata cannot be modified. Admin Activity and System Event audit logs are stored in the `_Required` log bucket, which enforces a fixed 400-day retention period and cannot be modified or deleted.

By default, Data Access audit logs ( `cloudaudit.googleapis.com/data_access` ), Policy Denied logs ( `cloudaudit.googleapis.com/policy_denied` ), Agent Gateway request logs ( `networkservices.googleapis.com/gateway_requests` ), and dual-attribution agent execution logs ( `is_agentic=true` ) are routed to the `_Default` log bucket with a 30-day retention period.

To enforce tamper-evident, write-once, read-many (WORM) retention for compliance evidence, route your agent audit and gateway logs to a custom Logging bucket, configure a custom retention period (from 1 to 3,650 days), and permanently lock the bucket. Locking a Logging bucket is an irreversible action that prevents anyone, including project owners and organization administrators, from deleting the bucket, deleting log entries before their retention period expires, or reducing the retention period.

To create and lock a custom Logging bucket for agent audit logs using the Google Cloud CLI, run the following commands:

```
gcloud logging buckets create BUCKET_ID \
    --location=LOCATION \
    --retention-days=RETENTION_DAYS \
    --project=PROJECT_ID

gcloud logging buckets update BUCKET_ID \
    --location=LOCATION \
    --locked \
    --project=PROJECT_ID
```

Replace the following:

- `BUCKET_ID` : A unique identifier for your audit log bucket (for example, `agent-audit-worm-bucket` ).
- `LOCATION` : The bucket location (for example, `global` , `us` , or `eu` ).
- `RETENTION_DAYS` : The number of days to retain log entries (between `1` and `3650` ).
- `PROJECT_ID` : Your Google Cloud project ID.

To protect a locked log bucket from being removed if its parent project is deleted, place a [project lien](https://docs.cloud.google.com/resource-manager/docs/project-liens) on the project. Alternatively, you can export audit logs to a Cloud Storage bucket configured with a locked retention policy ( [Bucket Lock](https://docs.cloud.google.com/storage/docs/bucket-lock) ). For more information, see [Configure and manage log buckets](https://docs.cloud.google.com/logging/docs/buckets) .

### Export audit logs to a SIEM

To centralize security monitoring, correlation, and long-term compliance archiving, you can continuously export agent audit logs, Agent Gateway authorization decisions, and `is_agentic=true` execution logs to Google Security Operations (Google SecOps) or a third-party Security Information and Event Management (SIEM) system.

You can configure a project-level Logging sink or an organization-level or folder-level [aggregated sink](https://docs.cloud.google.com/logging/docs/export/aggregated_sinks) to route logs to the following destinations:

- **Google Security Operations** : Ingest Cloud Audit Logs, Agent Gateway logs, and `AGENT_SESSION_ANOMALY` findings from Security Command Center into Google SecOps natively or through a Pub/Sub or Cloud Storage feed to investigate agent sessions alongside enterprise security telemetry. For setup instructions, see [Export Google Cloud data to Google SecOps](https://docs.cloud.google.com/chronicle/docs/ingestion/cloud/ingest-gcp-logs) .
- **Pub/Sub (Pub/Sub)** : Stream agent audit logs in real time to a Pub/Sub topic for ingestion by third-party SIEM platforms (such as Splunk, Datadog, or QRadar) using a Pub/Sub subscription or Dataflow connector. For details, see [Route logs to Pub/Sub](https://docs.cloud.google.com/logging/docs/export/configure_export_v2#dest-create) .
- **BigQuery (BigQuery) or Observability Analytics** : Export logs to a BigQuery dataset or link a Observability Analytics-enabled log bucket to BigQuery to run SQL compliance queries across agent identities, user delegations, and gateway policy denials.
- **Cloud Storage** : Export batched JSON log files to a Cloud Storage bucket with [Bucket Lock](https://docs.cloud.google.com/storage/docs/bucket-lock) enabled for long-term immutable archiving.

To create a Logging sink that streams agent audit and gateway logs to a Pub/Sub topic for SIEM ingestion, complete the following steps:

1.  Create the log sink with an inclusion filter that captures Cloud Audit Logs, Agent Gateway request logs, Agent Runtime logs, and dual-attribution entries ( `is_agentic=true` ):

    ```
    gcloud logging sinks create SINK_NAME \
        pubsub.googleapis.com/projects/DESTINATION_PROJECT_ID/topics/TOPIC_ID \
        --log-filter='logName:("cloudaudit.googleapis.com" OR "networkservices.googleapis.com%2Fgateway_requests" OR "aiplatform.googleapis.com%2Freasoning_engine") OR jsonPayload.is_agentic=true OR labels.is_agentic="true"' \
        --project=PROJECT_ID
    ```

    Replace the following:

    - `SINK_NAME` : A name for your log sink (for example, `agent-audit-siem-sink` ).
    - `DESTINATION_PROJECT_ID` : The project ID hosting the destination Pub/Sub topic.
    - `TOPIC_ID` : The ID of the Pub/Sub topic that your SIEM subscribes to.
    - `PROJECT_ID` : The project ID from which you are exporting logs. To export across an entire organization, replace `--project= `` PROJECT_ID` with `--organization= `` ORGANIZATION_ID `` --include-children` .

2.  Retrieve the sink's writer service account identity and grant it the Pub/Sub Publisher role ( `roles/pubsub.publisher` ) on the destination topic:

    ```
    WRITER_IDENTITY=$(gcloud logging sinks describe SINK_NAME \
        --project=PROJECT_ID \
        --format='value(writerIdentity)')

    gcloud pubsub topics add-iam-policy-binding TOPIC_ID \
        --project=DESTINATION_PROJECT_ID \
        --member="${WRITER_IDENTITY}" \
        --role="roles/pubsub.publisher"
    ```

## OpenTelemetry generative AI conventions

Agent traces and prompt-and-response logs rely heavily on the [OpenTelemetry Semantic Conventions for generative AI systems](https://opentelemetry.io/docs/specs/semconv/gen-ai/) to standardize how generative AI telemetry is captured, structured, and reported.

Adhering to these conventions is critical for agent tracing because it establishes a universal, vendor-agnostic format for describing complex, multi-step agent workflows, such as tool executions, retrieval steps, and token consumption. This standardization helps seamless interoperability across different observability backends and analytics tools, both inside and outside of Google Cloud.

## What's next

- [View agent relationships](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/topology) as a topology graph.
- [View agent traces](https://docs.cloud.google.com/gemini-enterprise-agent-platform/optimize/observability/traces) to debug agent behavior.
- [Evaluate your agents](https://docs.cloud.google.com/gemini-enterprise-agent-platform/optimize/evaluation/evaluate-agents) .
