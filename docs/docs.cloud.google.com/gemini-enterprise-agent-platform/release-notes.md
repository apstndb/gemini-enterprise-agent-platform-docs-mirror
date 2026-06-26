---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/release-notes
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/release-notes
title: Gemini Enterprise Agent Platform release notes
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

This page documents production updates to Gemini Enterprise Agent Platform. Check this page for announcements about new or updated features, bug fixes, known issues, and deprecated functionality.

You can see the latest product updates for all of Google Cloud on the [Google Cloud](https://docs.cloud.google.com/release-notes) page, browse and filter all release notes in the [Google Cloud console](https://console.cloud.google.com/release-notes) , or programmatically access release notes in [BigQuery](https://console.cloud.google.com/bigquery?p=bigquery-public-data&d=google_cloud_release_notes&t=release_notes&page=table) .

## June 24, 2026

Feature

**AI security findings in Agent Platform**

Viewing AI security findings and posture management summaries in Gemini Enterprise Agent Platform is [generally available](https://cloud.google.com/products#product-launch-stages) .

With this release, the **Security** dashboard introduces the **Top security findings** widget.

Also, specific features within the AI security widgets are available in [Preview](https://cloud.google.com/products#product-launch-stages) , including the following:

  - Vulnerability findings and threat monitoring for agent runtimes (such as Cloud Run)
  - Historical content violation trends ( **Violations over time** )

For more information, see [View security findings](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/view-security-findings) .

Feature

**Model Armor for Agent Gateway in General Availability**

You can enable Model Armor on an Agent Gateway resource to apply your organization's content security guardrails to prompts and responses that pass through the gateway. This feature is generally available ( [GA](https://cloud.google.com/products#product-launch-stages) ).

For more information, see [Configure Model Armor on a gateway](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/configure-model-armor) .

## June 22, 2026

Change

**Supervised fine-tuning available for Gemini 3.1 Flash Lite and Gemini 3.5 Flash in Public Preview**

Supervised fine-tuning is now available for the `gemini-3.1-flash-lite` and `gemini-3.5-flash` models in [Preview](https://cloud.google.com/products#product-launch-stages) . Model tuning for Gemini 3.1 Flash Lite and Gemini 3.5 Flash is restricted to `us-central1` and `europe-west4` and tuned model serving is restricted to the `us` and `eu` multi-region endpoints.

See [About supervised fine-tuning](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini-supervised-tuning) for more information.

Feature

**Provisioned Throughput support for supervised fine-tuned Gemini 3 model inference.**

Provisioned Throughput can be used to assure supervised fine-tuned inference using the same quota. Supervised fine-tuned inference for Gemini 3 models incurs a higher burndown rate compared to base model inference. Learn more [here](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/provisioned-throughput/supported-models#supervised-fine-tuned-model-support) .

## June 18, 2026

Feature

**Agent Gateway in General Availability**

Agent Gateway is the networking component of the Gemini Enterprise Agent Platform ecosystem. It secures and governs connectivity for all agentic interactions, whether they occur between users and agents, agents and tools, or among agents themselves.

For details, see [Agent Gateway overview](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/gateways/agent-gateway-overview) .

Feature

**Agent Observability is generally available (GA)**

This release provides visibility into the performance, behavior, and health of deployed agents and Model Context Protocol (MCP) servers directly within the agent management workflow.

Key updates in this release include:

  - **Default-On Tracing:** OpenTelemetry tracing is now enabled by default for newly deployed Agent Development Kit (ADK) agents on Agent Engine, simplifying the observability setup process without requiring manual configuration.
  - **Storage Prioritization:** Google Cloud Storage (GCS) is the default storage choice in the Google Cloud Console, instead of Cloud Logging. We recommend that you store your multimodal prompt and response payloads in a Cloud Storage (GCS) bucket. This solution provides robust support for large payloads and it enables fine-grained lifecycle management.
  - **Enhanced Tracing:** Inspect step-by-step session execution and view directed acyclic graphs (DAGs) of trace spans.

For more information, see the following:

  - [Observability overview](https://docs.cloud.google.com/gemini-enterprise-agent-platform/optimize/observability/overview)
  - [View agent traces](https://docs.cloud.google.com/gemini-enterprise-agent-platform/optimize/observability/traces)
  - [Set up tracing](https://docs.cloud.google.com/gemini-enterprise-agent-platform/scale/runtime/tracing)

Feature

**Agent Registry is generally available (GA)**

Agent Registry is [generally available (GA)](https://cloud.google.com/products#product-launch-stages) . Agent Registry is a centralized catalog for discovering and registering agents and Model Context Protocol (MCP) servers.

The following features are available in Agent Registry for the GA launch stage:

  - **API v1 and client libraries:** The `v1` version of the Agent Registry API is available. Cloud client libraries are available in C\#, Go, Java, Node.js, PHP, Python, and Ruby.
  - **A2A v1 support:** Agent Registry supports Agent-to-Agent (A2A) protocol version `1.0` , letting you explicitly declare transport endpoints and bindings inside the `supportedInterfaces` array, in addition to the existing `0.3` schema support.
  - **Terraform support:** Terraform scripts for Application Default Credentials (ADC) have graduated to General Availability. You can use Terraform to configure and manage your agents, MCP servers, endpoints, and bindings.

**Known limitations:**

  - **Access Transparency and Access Approval:** [Access Transparency](https://docs.cloud.google.com/assured-workloads/access-transparency/docs/overview) logs, which provide visibility into when Google personnel access your content, and [Access Approval](https://docs.cloud.google.com/assured-workloads/access-approval/docs/overview) controls aren't available for Agent Registry configurations.
  - **Data Residency:** If you configure the [resource location constraint](https://docs.cloud.google.com/organization-policy/restrict-locations) in your organization policy, Agent Registry enforces the constraint when you register a resource. However, detective controls for data residency compliance reporting are limited.

For more information, see the [Agent Registry overview](https://docs.cloud.google.com/agent-registry/overview) .

Feature

The Agent Identity API ( `agentidentity.googleapis.com` ) is available in [Preview](https://cloud.google.com/products#product-launch-stages) . This new API replaces the legacy IAM Connectors API ( `iamconnectors.googleapis.com` ) for managing auth providers and agent identities.

During the preview migration period, both APIs operate side-by-side. Existing auth providers are automatically mirrored to the new V2 resource hierarchy ( `authProviders/` ), allowing you to migrate your IAM policies, agent code, and client applications without downtime.

## June 17, 2026

Feature

**Memory Bank and Sessions global and multi-regional endpoints GA**

Memory Bank and Sessions support for multi-regional and global endpoints is now in General Availability (GA). For more information, see [Supported locations for agents](https://docs.cloud.google.com/gemini-enterprise-agent-platform/resources/agent-locations#multi-regional-and-global-endpoints) . Note that Customer-Managed Encryption Keys (CMEK) cannot be used if your Memory Bank or Sessions instance is configured to use the global endpoint.

## June 15, 2026

Feature

**Reinforcement Learning fine-tuning is available for Gemini 3.5 Flash in Public Preview**

Reinforcement Learning fine-tuning is now available for the `gemini-3.5-flash` models in [Preview](https://cloud.google.com/products#product-launch-stages) . Model tuning for Gemini 3.5 Flash is restricted to `us-central1` and `europe-west4` , and tuned model serving is restricted to the `us` and `eu` multi-region endpoints.

See [About reinforcement learning fine-tuning](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/tuning/reinforcement-tuning) for more information.

## June 09, 2026

Feature

**Anthropic's Claude Fable 5**

[Claude Fable 5](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/fable-5) is available in Model Garden.

## June 02, 2026

Announcement

**Updates to abuse monitoring and zero data retention documentation**

Documentation for abuse monitoring, zero data retention, and responsible AI has been updated to align with the Advanced AI Safety Addendum. These updates include new details regarding Advanced AI safety, partner-specific terms, and request-response logging for models like Claude Mythos and Opus.

For more information, see:

  - [Abuse monitoring](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/abuse-monitoring)
  - [Zero data retention](https://docs.cloud.google.com/gemini-enterprise-agent-platform/resources/zero-data-retention)
  - [Responsible AI](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/responsible-ai)

## June 01, 2026

Breaking

**Gemini 2.0 Flash and Gemini 2.0 Flash-Lite are discontinued**

Gemini 2.0 Flash and 2.0 Flash-Lite are discontinued and are no longer available. This includes both model serving and Provisioned Throughput. Use Gemini 3.1 Flash-Lite, Gemma 4, or more recent Gemini releases.

## May 28, 2026

Feature

**Agent Platform Gemini 3.1 Flash Image and Gemini 3 Pro Image**

Gemini Enterprise Agent Platform Gemini 3.1 Flash Image and Gemini 3 Pro Image are [Generally Available](https://cloud.google.com/products#product-launch-stages) .

With this release, Gemini 3.1 Flash Image and Gemini 3 Pro Image support 4K image outputs in [Preview](https://cloud.google.com/products#product-launch-stages) .

Also supported in this release, Gemini 3.1 Flash Image supports video inputs in [Preview](https://cloud.google.com/products#product-launch-stages) . You can use video inputs to generate thumbnails or representative images of videos.

For more information, see the following:

  - [Gemini 3.1 Flash Image (Nano Banana 2)](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/3-1-flash-image)
  - [Gemini 3 Pro Image (Nano Banana Pro)](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/3-pro-image)

Deprecated

**Agent Platform Gemini 3.1 Flash Image Preview and Gemini 3 Pro Image Preview deprecation**

Gemini Enterprise Agent Platform Gemini 3.1 Flash Image Preview and Gemini 3 Pro Image Preview are deprecated. We recommend that you update your model endpoints before July 17, 2026, to avoid service disruption.

The following are the discontinued endpoints and recommended endpoint migration:

| Discontinued endpoints           | Recommended endpoint migration |
| -------------------------------- | ------------------------------ |
| `gemini-3.1-flash-image-preview` | `gemini-3.1-flash-image`       |
| `gemini-3-pro-image-preview`     | `gemini-3-pro-image`           |

Feature

**Anthropic's Claude Opus 4.8**

[Claude Opus 4.8](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/opus-4-8) is available in Model Garden.

## May 27, 2026

Feature

**User ID logging now included with agent logs when you opt in to "Enable logging of prompt inputs and response outputs"**

Prompt input and response output logging now includes the `user.id` field. This addition allows better tracking of anomalous tool interactions.

> **Important:** Logging of `user.id` is included when opting in to "Enable logging of prompt inputs and response outputs" effective May 22, 2026 and later and with the Agent Development Kit (ADK) version 2.1 and later. If you opted in prior to this change, your logs do not include `user.id` . You will need to redeploy your agents and opt-in again for this setting to take effect.

For details on configuration, see [Write traces for an agent](https://docs.cloud.google.com/gemini-enterprise-agent-platform/scale/runtime/tracing#write-traces) .

## May 26, 2026

Feature

**The Gemini Deep Research Agent released in Preview**

The Gemini Deep Research Agent has been released in Preview. The Gemini Deep Research Agent is a managed AI agent that plans, executes, and synthesizes complex, multi-step research workflows across the public web and private enterprise data to generate comprehensive, cited reports.

For more information, see [Use the Gemini Deep Research Agent](https://docs.cloud.google.com/gemini-enterprise-agent-platform/agents/use-deep-research) .

Feature

**Agent Platform Sandboxes**

Additional Agent Platform [sandbox](https://docs.cloud.google.com/gemini-enterprise-agent-platform/scale/sandbox) features are now available:

  - **[Computer use](https://docs.cloud.google.com/gemini-enterprise-agent-platform/scale/sandbox/computer-use) (Preview)** : Enables agents to automate browser-based tasks within an isolated web browser environment. You can control the browser using the API or connect directly using the Chrome DevTools Protocol (CDP).
  - **[Custom container sandboxes](https://docs.cloud.google.com/gemini-enterprise-agent-platform/scale/sandbox/custom-containers) (Preview)** : Bring your own container (BYOC) to run custom workloads with specialized dependencies hosted in Artifact Registry.
  - **[Sandbox templates](https://docs.cloud.google.com/gemini-enterprise-agent-platform/scale/sandbox/manage-templates) (Preview)** : Define sandbox specifications as reusable templates relying on pre-warmed pools to facilitate rapid, reliable startups.
  - **[Sandbox snapshots](https://docs.cloud.google.com/gemini-enterprise-agent-platform/scale/sandbox/manage-snapshots) (Preview)** : Save the exact state of your sandbox environment (including dependencies and file systems) and restore it to a new sandbox.

Feature

**Identify the agents with the most content security violations**

The **Security** dashboard displays the top 10 agents with the most content violations detected by Model Armor. The list shows the agent ID of each agent and the number of violations detected for that agent. For more information, see [Monitor content security](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/monitor-content-security) .

## May 20, 2026

Change

**Supervised fine-tuning available for Gemini 3.1 Flash Lite (Preview)**

Supervised fine-tuning is now available for limited support for the `gemini-3.1-flash-lite` model. During this period, model tuning for Gemini 3.1 Flash Lite is restricted to `us-central1` and `europe-west4` and tuned model serving is restricted to the `us` and `eu` multi-region endpoints.

See [About supervised fine-tuning](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini-supervised-tuning) for more information.

Change

**Set media resolution at a Part-level for data when using supervised fine-tuning**

Supervised fine-tuning now supports `Part` -level `mediaResolution` declarations for images, videos, and PDFs. `Part` -level media resolution declarations also support the `MEDIA_RESOLUTION_ULTRA_HIGH` level.

See the following media type–specific pages for more information:

  - [Document tuning](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/tune_gemini/doc_tune)
  - [Image tuning](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/tune_gemini/image_tune)
  - [Video tuning](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/tune_gemini/video_tune)

## May 19, 2026

Feature

**Gemini 3.5 Flash is generally available (GA)**

For details, see the [model specifications page](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/3-5-flash) .

Feature

**Manage agent revisions and traffic splitting**

Agent revisions and traffic splitting are now available in public preview. You can create immutable revisions of deployed agents, and split traffic between the different active revisions. This enables canary deployments and safe testing of new agent versions. For more information, see [Manage revisions and traffic](https://docs.cloud.google.com/gemini-enterprise-agent-platform/scale/runtime/manage-revisions-and-traffic) .

Feature

**Manage and discover agent skills with Skill Registry**

Manage and discover agent skills with the Skill Registry, in public preview. This secure, private, and low-latency repository stores skills as self-contained packages, including instructions, code, and documentation, to enhance agent abilities.

For more information, see:

  - [Skill Registry overview](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/skill-registry)
  - [Create and manage skills](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/skill-registry/create-manage)

Feature

**Managed Agents API on Agent Platform released in Preview**

The Managed Agents API on Agent Platform has been released in Preview.

This feature allows you to build and scale autonomous agents, including those built from configuration using the Antigravity harness. These agents run in a fully managed and isolated sandbox environment, equipped with tools and skills, and can be interacted with via a dedicated API.

For more information, see the following:

  - [Managed Agents API on Agent Platform overview](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/managed-agents)
  - [Create and manage agents](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/managed-agents/create-manage)
  - [Interact with agents](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/managed-agents/interact-with-agents)
  - [Managed Agents API on Agent Platform sandbox environment](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/managed-agents/sandbox-environment)

Feature

**AI Content Detection API available**

AI Content Detection API is available in [Preview](https://cloud.google.com/products#product-launch-stages) . For details see [AI Content Detection](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/ai-content-detection) .

Feature

**Provisioned Throughput for Gemini now supports latency SLA**

Provisioned Throughput now provides a tokens per second latency SLA, covering generation speed from the first returned token to the last.

For more information, see the [Gemini Enterprise Agent Platform Online Inference Service Level Agreement (SLA)](https://cloud.google.com/vertex-ai/generative-ai/sla?e=48754805) .

Change

Memory Bank and Sessions support for multi-regional and global endpoints is in [Preview](https://cloud.google.com/products#product-launch-stages) . For more, see [Supported locations for agents in Agent Platform](https://docs.cloud.google.com/gemini-enterprise-agent-platform/resources/agent-locations#multi-regional_and_global_endpoints) .

## May 14, 2026

Feature

**Priority PayGo is generally available (GA)**

Priority PayGo is a consumption option that provides more consistent performance than standard PayGo without the upfront commitment of Provisioned Throughput. It is ideal for business-critical workloads with fluctuating or unpredictable traffic patterns.

For more information, see [Priority PayGo](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/priority-paygo) .

## May 11, 2026

Change

You can purchase **Provisioned Throughput for Gemma 4** . To learn more, see the list of [supported open models](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/provisioned-throughput/supported-models#open-models) .

## May 08, 2026

Change

**Gemini Distillation Service Early Access**

We're introduction Gemini Distillation Service in Early Access. For information about requesting access, see [Gemini Distillation Service](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/tuning/distillation) .

Change

**Improvements to the Provisioned Throughput orders page** have now made it possible to:

  - View all scheduled orders by using the Start Date column.
  - Enable filtering and sorting of orders by using column names.
  - Download all order data to a CSV file (including across all regions).

See [View standard Provisioned Throughput orders](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/provisioned-throughput/purchase-provisioned-throughput#view-orders) .

## May 07, 2026

Change

**Gemini 3.1 Flash-Lite is now generally available**

Our most cost-efficient Gemini model, **3.1 Flash-Lite** , is out of preview and is now generally available. For technical information on this model, see the [model information card](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/3-1-flash-lite) .

Change

You can purchase **Provisioned Throughput for Gemini 3.1 Flash-Lite** . To learn more, see the [Provisioned Throughput overview](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/provisioned-throughput/overview) .

## May 06, 2026

Fixed

Fixed an issue with **Audio track extraction (Gemini Embedding 2 only)** where the `audio_track_extraction` feature did not work. For more information, see [Issue \#504505771](https://issuetracker.google.com/504505771) .

Change

**Agent Platform Gemini 3.1 Flash Image and Gemini 3 Pro Image**

Gemini Enterprise Agent Platform Gemini 3.1 Flash Image Preview and Gemini 3 Pro Image Preview are introducing the following changes:

  - Upgrades to improve 4K outputs and efficiency in both models
  - Gemini 3.1 Flash Image Preview and Gemini 3 Pro Image Preview will now return a maximum of 1 thought image.
  - The image\_size parameter for Gemini 3.1 Flash Image Preview now accepts "512", "512p", "512P", "512PX", "512px" to generate 0.5MP resolution output images.
  - The default thinking level for Gemini 3.1 Flash Image Preview changed to Minimal.

## April 28, 2026

Feature

**Improved transcription quality for Gemini Live API**

You can now improve transcription quality for multilingual automatic speech recognition (ASR) by using the `[input/output]_audio_transcription.language_codes` field.

For more information, see [Enable audio transcription for the session](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/live-api/start-manage-session#enable-audio-transcription) .

Feature

**Asynchronous function calling with Live API**

Asynchronous function calling is now available in [public preview](https://cloud.google.com/products#product-launch-stages) in Gemini Live API. You can run functions in parallel with conversation, manage background processing, and handle function responses with policies including `SILENT` , `WHEN_IDLE` , and `INTERRUPT` . For more information, see [Asynchronous function calling with Gemini Live API](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/live-api/asynchronous-function-calling) .

## April 22, 2026

Change

**Vertex AI to Gemini Enterprise Agent Platform naming changes**

The table below lists all of the features that have been transitioned from Vertex AI and what their new names are in Agent Platform.

#### Click to expand naming changes list

| Vertex AI name                                                                             | Agent Platform name                                           |
| ------------------------------------------------------------------------------------------ | ------------------------------------------------------------- |
| Vertex AI Platform                                                                         | Agent Platform                                                |
| Generative AI on Vertex AI                                                                 | Generative AI                                                 |
| Vertex AI Studio                                                                           | Agent Studio                                                  |
| Vertex AI API                                                                              | Agent Platform API                                            |
| Vertex AI Model Garden                                                                     | Model Garden                                                  |
| Vertex AI Models as a Service (MaaS)                                                       | MaaS                                                          |
| (Gemini/Veo) on Vertex AI                                                                  | (Gemini/Veo) on Agent Platform                                |
| (Claude/Llama/DeepSeek/etc.) on Vertex AI                                                  | (Claude/Llama/DeepSeek/etc.), available on Agent Platform     |
| Pre-trained APIs on Vertex AI                                                              | Pre-trained APIs on Agent Platform                            |
| (Provisioned Throughput/Pay-as-you-go/etc.) on Vertex AI                                   | (Provisioned Throughput/Pay-as-you-go/etc.) on Agent Platform |
| Gemini Live API on Vertex AI                                                               | Gemini Live API on Agent Platform                             |
| Vertex AI Search                                                                           | Agent Search                                                  |
| Vertex AI Search for Industry                                                              | Agent Search for Industry                                     |
| Vertex AI Search for Commerce                                                              | Agent Search for Commerce                                     |
| Recommendations from Vertex AI Search                                                      | Recommendations                                               |
| Vertex AI Conversation                                                                     | Agent Conversation                                            |
| Vertex AI RAG Engine                                                                       | RAG Engine                                                    |
| Vertex AI Vector Search                                                                    | Vector Search                                                 |
| Vertex AI Vector Search 2.0                                                                | Agent Retrieval                                               |
| Vertex AI Agent Engine                                                                     | Agent Runtime                                                 |
| Vertex AI Studio App Builder                                                               | App Builder in Agent Studio                                   |
| Vertex AI Agent Engine Memory Bank                                                         | Agent Platform Memory Bank                                    |
| Vertex AI Agent Engine Sessions                                                            | Agent Platform Sessions                                       |
| Vertex AI Agent Engine Code Execution                                                      | Agent Platform Code Execution                                 |
| Grounding with Google \[...\] in Vertex AI                                                 | Grounding with Google \[...\] in Agent Platform               |
| Grounding with Google \[...\] in Vertex AI Search                                          | Grounding with Google \[...\] in Agent Search                 |
| Grounding with Google \[...\] in Vertex AI Studio                                          | Grounding with Google \[...\] in Agent Studio                 |
| Vertex AI Training                                                                         | Agent Platform Managed Training                               |
| Vertex AI Serverless Training                                                              | Agent Platform Serverless Training                            |
| Vertex AI Training Clusters (VTC)                                                          | Managed Training Clusters                                     |
| Ray on Vertex AI                                                                           | Ray on Agent Platform                                         |
| Reinforcement Learning from Human Feedback (RLHF)/Reinforcement Learning (RL) on Vertex AI | Reinforcement Learning on Agent Platform                      |
| Vertex AI Neural Architecture Search                                                       | Neural Architecture Search on Agent Platform                  |
| Vertex AI Prediction/Vertex AI Inference                                                   | Agent Platform Inference                                      |
| Vertex AI Vision                                                                           | Agent Platform Vision                                         |
| Vertex AI Batch Inference                                                                  | Agent Platform Batch Inference                                |
| Vertex AI Online Inference                                                                 | Agent Platform Online Inference                               |
| Vertex AI Endpoints                                                                        | Agent Platform Endpoints                                      |
| Vertex AI Forecasting/Forecasting with AutoML                                              | Forecasting on Agent Platform                                 |
| Vertex AI Pipelines                                                                        | Agent Platform Pipelines                                      |
| Vertex AI Notebooks                                                                        | Agent Platform Notebooks                                      |
| Vertex AI Colab Enterprise                                                                 | Agent Platform Colab Enterprise                               |
| Vertex AI Workbench                                                                        | Agent Platform Workbench                                      |
| Vertex AI Workbench Instances                                                              | Agent Platform Workbench Instances                            |
| Vertex AI Feature Store                                                                    | Agent Platform Feature Store                                  |
| Vertex AI Model Registry                                                                   | Agent Platform Model Registry                                 |
| Vertex AI Model Evaluation                                                                 | Agent Platform Model Evaluation                               |
| Gen AI evaluation service on Vertex AI                                                     | Gen AI evals                                                  |
| Vertex AI AutoML (Vision/Video/Tables)                                                     | Agent Platform AutoML                                         |
| Data Labeling on Vertex AI                                                                 | Data Labeling                                                 |
| Vertex AI on GDC                                                                           | Agent Platform on GDC                                         |
| Vertex AI Experiments                                                                      | Experiments on Agent Platform                                 |
| Vertex AI Model Monitoring                                                                 | Model Monitoring on Agent Platform                            |
| Vertex AI Media Studio                                                                     | Agent Media Studio                                            |
| Vertex AI                                                                                  | Agent Platform                                                |
| Vertex AI Generative AI                                                                    | Agent Platform Generative AI                                  |

Change

**Initial release of Gemini Enterprise Agent Platform**

This initial release includes (but is not limited to) the following releases or changes:

  - Change **Vertex AI** is now part of Gemini Enterprise Agent Platform. Information on model support for Vertex AI is now under [Gemini Enterprise Agent Platform \> Models](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/overview) .
  - Change **Agent Builder** is now part of Gemini Enterprise Agent Platform. Features have been renamed as follows:
      - **Agent Engine** is now [**Agent Runtime**](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/runtime) .
      - **Agent Builder Sessions** is [**Agent Platform Sessions**](https://docs.cloud.google.com/gemini-enterprise-agent-platform/scale/sessions) .
      - **Memory Bank** is now [**Agent Platform Memory Bank**](https://docs.cloud.google.com/gemini-enterprise-agent-platform/scale/memory-bank) .
  - Change **Agent Runtime** now supports long-running operations (up to 7 days).
  - Change **Agent Runtime** now supports sub-second cold starts.
  - Change Provisioning for **Agent Runtime** has been reduced to less than 1 minute.
  - Release You can now use your own [custom-built containers](https://docs.cloud.google.com/gemini-enterprise-agent-platform/release-notes/gemini-enterprise-agent-platform/build/runtime/setup#byoc) when you deploy agents with **Agent Runtime** .
  - Change When [creating a Session](https://docs.cloud.google.com/gemini-enterprise-agent-platform/scale/sessions/manage-with-api) , you can specify your own session ID.
  - Release Memory Bank now enables continuous event streaming with automated memory generation triggered by configurable criteria like event count or idle time. For more information, see [Ingest events](https://docs.cloud.google.com/gemini-enterprise-agent-platform/scale/memory-bank/ingest-events) .
  - Release Memory Bank now automatically maintains an immutable version history of memories through revision resources. For more information, see [Memory revisions](https://docs.cloud.google.com/gemini-enterprise-agent-platform/release-notes/gemini-enterprise-agent-platform/scale/memory-bank/revisions) .
  - Release [**Agent Identity**](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/agent-identity-overview) for General Availability. Agent Identity helps let your agent securely authenticate to MCP servers, cloud resources, endpoints, and other agents, either acting as itself or acting on behalf of the end user.
  - Release [**Agent Gateway**](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/gateways/agent-gateway-overview) for Private Preview. Agent Gateway is the networking component of the Gemini Enterprise Agent Platform ecosystem. It secures and governs connectivity for all agentic interactions, whether they occur between users and agents, agents and tools, or among agents themselves.
  - Release [**Agent Registry**](https://docs.cloud.google.com/agent-registry/overview) for Public Preview. Agent Registry is a centralized, unified catalog that lets you store, discover, and govern Model Context Protocol (MCP) servers, tools, and AI agents within Google Cloud.
  - Release New [**IAM governance policies**](https://docs.cloud.google.com/gemini-enterprise-agent-platform/release-notes/gemini-enterprise-agent-platform/govern/policies/overview) are available in Private Preview.
  - Release [**Agent Observability**](https://docs.cloud.google.com/gemini-enterprise-agent-platform/optimize/observability/overview) for Preview. Agent Observability in Gemini Enterprise Agent Platform provides comprehensive visibility into the performance, behavior, and health of your deployed agents and Model Context Protocol (MCP) servers. By monitoring key metrics, tracing execution paths, and observing your multi-agent system as a whole, you can diagnose issues, optimize resource consumption, and improve the reliability of your agents.
  - Release [**Gemini Embedding 2**](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/embedding-2) ( `gemini-embedding-2` ) for General Availability.
  - Release The [**Gemini Deep Research Agent**](https://docs.cloud.google.com/gemini-enterprise-agent-platform/agents/deep-research) , a pre-built agent designed to help you plan, execute, and synthesize multi-step research tasks. It uses Gemini 3.1 Pro to bridge the gap between public web data and private enterprise context by simultaneously grounding research across three distinct, high-fidelity data streams.
  - Release [**Agent Platform remote MCP server**](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/use-agent-platform-mcp) for General Availability. Support for Model Context Protocol (MCP) use is available for Agent Platform.
  - Change **Google Cloud console navigation** : The navigation menus under Agent Platform (formerly Vertex AI) and Data Analytics have been updated to centralize agentic products and features. Bookmarked links will continue to work via automatic redirects.

Issue

The following known issues affect Gemini Enterprise Agent Platform:

  - **Audio track extraction (Gemini Embedding 2 only):** The `audio_track_extraction` feature does not work. For more information, see [Issue \#504505771](https://issuetracker.google.com/504505771) .
