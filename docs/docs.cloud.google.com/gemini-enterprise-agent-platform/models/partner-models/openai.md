---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/openai
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/openai
title: OpenAI GPT Models
description: Explore OpenAI partner models in Private Preview on Gemini Enterprise Agent Platform, including model capabilities, data handling, and zero data retention.
data_source: docs.cloud.google.com
---

> **Private Preview**
>
> This product or feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](https://docs.cloud.google.com/terms/service-terms#1) , and the [Additional Terms for Generative AI Preview Products](https://cloud.google.com/trustedtester/aitos) . Pre-GA products and features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

OpenAI partner models are available in Private Preview on Gemini Enterprise Agent Platform. You can call these models through the OpenAI Responses API.

## Request Private Preview access

To request Private Preview access to OpenAI partner models, contact your Google Cloud account team. If your organization's policy restricts model access, [allow the model in that policy](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/control-model-access) .

## Available OpenAI models

Available OpenAI partner models on Gemini Enterprise Agent Platform include flagship models across the Astra, Sol, Terra, and Luna families. These flagship models share the following core capabilities:

- **1,050,000-token context window:** Supports up to 922,000 input tokens and 128,000 output tokens.
- **Multimodal input:** Accepts text and image inputs, and returns text outputs.
- **Configurable reasoning effort:** Controls the amount of reasoning tokens generated during inference.
- **Multi-region endpoints:** Supports both the global endpoint ( `global` ) and the US multi-region endpoint ( `us` ).
- **Long-context pricing tiers:** Requests that exceed 272,000 input tokens are billed under long-context pricing rates.

### Model families

OpenAI groups these models into four distinct families:

- **GPT Astra family:** Highest-capability partner models for complex multi-step reasoning, difficult engineering tasks, and long-horizon agent workflows.
- **GPT Sol family:** Flagship partner models built for autonomous coding, agentic tool orchestration, and complex analytical workloads.
- **GPT Terra family:** High-throughput, cost-balanced reasoning models built for general enterprise workloads and high-volume automation.
- **GPT Luna family:** Low-latency partner models optimized for fast interactive coding assistants and latency-sensitive enterprise workloads.

## GPT Astra models

cognition [GPT 6.0 Astra](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/openai/gpt-6-astra) ( `gpt-6-astra` ) Highest-capability partner model from OpenAI ( `gpt-6-astra` ), built for complex multi-step reasoning, difficult engineering tasks, and long-horizon agent workflows.

## GPT Sol models

arrow_selector_tool [GPT 6.1 Sol](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/openai/gpt-6-1-sol) ( `gpt-6.1-sol` ) Flagship partner model from OpenAI ( `gpt-6.1-sol` ), built for autonomous coding, agentic tool orchestration, and complex analytical workloads.

## GPT Terra models

graph_5 [GPT 6.1 Terra](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/openai/gpt-6-1-terra) ( `gpt-6.1-terra` ) High-throughput, cost-balanced reasoning model from OpenAI ( `gpt-6.1-terra` ), built for general enterprise workloads and high-volume automation.

## GPT Luna models

bolt [GPT 6.0 Luna](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/openai/gpt-6-luna) ( `gpt-6-luna` ) Low-latency partner model from OpenAI ( `gpt-6-luna` ), optimized for fast interactive coding assistants and latency-sensitive enterprise workloads.

## Feature availability

OpenAI models on Agent Platform expose the OpenAI Responses API while authenticating with Google Cloud Identity and Access Management (IAM) and OAuth 2.0 credentials. During Private Preview, a subset of hosted tools, endpoints, and features from the direct OpenAI API isn't supported on Agent Platform. For a detailed capability breakdown, see OpenAI's [Private Preview Feature Availability](https://openai-gcp-preview-feature-guide.openai.chatgpt.site/) guide.

| Feature or capability                                     | Direct OpenAI API | Agent Platform (Private Preview) | Details                                                                                                                                                                                                                                                          |
|-----------------------------------------------------------|-------------------|----------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| API requests and endpoints                                |                   |                                  |                                                                                                                                                                                                                                                                  |
| Responses API                                             | Supported         | Supported                        | Available at `publishers/openai/v1/responses` on the `global` and `us` multi-region endpoints. See [Call Responses API](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/openai/responses) .                                 |
| Streaming responses                                       | Supported         | Supported                        | Streams incremental text and tool events using server-sent events (SSE).                                                                                                                                                                                         |
| Chat Completions, Assistants, Decisions, and Sandbox APIs | Supported         | Not supported                    | Only the Responses API is available in Private Preview. Chat Completions, Assistants, Decisions API, Sandbox API, and remote code execution sandboxes aren't supported.                                                                                          |
| Batch, background, and Realtime (WebSocket) APIs          | Supported         | Not supported                    | Asynchronous Batches, background mode, stream resume, input token counting, and the Realtime API (WebSocket connections) aren't supported.                                                                                                                       |
| Output and reasoning                                      |                   |                                  |                                                                                                                                                                                                                                                                  |
| Function calling and structured outputs                   | Supported         | Supported                        | Supports client-side parallel and asynchronous function calling, JSON Schema structured outputs, and JSON mode.                                                                                                                                                  |
| Configurable reasoning effort                             | Supported         | Supported                        | Supports reasoning effort levels and encrypted reasoning tokens across turns.                                                                                                                                                                                    |
| Raw reasoning mode and summaries                          | Supported         | Not supported                    | Raw reasoning mode and reasoning summaries aren't supported.                                                                                                                                                                                                     |
| Tools and integrations                                    |                   |                                  |                                                                                                                                                                                                                                                                  |
| Client-side tools and search                              | Supported         | Supported                        | Supports client-side function calling, parallel tool calls, structured function arguments, custom tools, client-side tool search, client-run MCP, and client-side shell tools.                                                                                   |
| Hosted OpenAI tools and Web Search                        | Supported         | Not supported                    | Hosted Web Search, File Search, Code Interpreter, Vector Stores, and remote MCP servers aren't supported. Tools run client-side.                                                                                                                                 |
| Codex CLI and Codex Desktop App                           | Supported         | Supported (API mode)             | Runs locally on developer workstations against Agent Platform endpoints using Google Cloud OAuth credentials. Hosted Codex Cloud isn't supported.                                                                                                                |
| Documents and media                                       |                   |                                  |                                                                                                                                                                                                                                                                  |
| Multimodal image and file inputs                          | Supported         | Supported                        | Supports inline image inputs and direct PDF text extraction.                                                                                                                                                                                                     |
| Conversation state and caching                            |                   |                                  |                                                                                                                                                                                                                                                                  |
| Conversation compaction                                   | Supported         | Supported                        | Supports the standalone `POST .../responses/compact` endpoint to compress conversation history into encrypted compaction items.                                                                                                                                  |
| Prompt caching                                            | Supported         | Supported                        | Supports automatic prefix caching and explicit prompt-cache controls in volatile memory.                                                                                                                                                                         |
| Flex mode                                                 | Supported         | Not supported                    | OpenAI flex mode pricing and execution aren't supported.                                                                                                                                                                                                         |
| Regional and enterprise availability                      |                   |                                  |                                                                                                                                                                                                                                                                  |
| Regional availability (APAC and EU)                       | Supported         | Not supported                    | Only the `global` endpoint and the `us` multi-region endpoint are available in Private Preview. APAC, EU, and single-region endpoints aren't available.                                                                                                          |
| Legacy, media, Cyber, and specialty models                | Supported         | Not supported                    | Legacy models (such as GPT-4, GPT-4o, and GPT-3.5), image models (such as DALL-E), voice and audio models (such as Whisper and TTS), Cyber models, and other specialty models aren't supported. Only the specified GPT 6.0 and 6.1 partner models are supported. |
| Model Armor                                               | Not applicable    | Not supported                    | Model Armor safety filters aren't available for OpenAI partner models during Private Preview.                                                                                                                                                                    |
| FedRAMP High                                              | Not applicable    | Not supported                    | FedRAMP High authorization isn't supported for OpenAI partner models during Private Preview.                                                                                                                                                                     |

## Data logging, data retention, and no human review

By default, Google Cloud logs and retains prompts and responses for up to 30 days for abuse monitoring. During Private Preview, neither Google nor OpenAI conducts human review of customer prompts or responses.

- **Default 30-day safety retention inside Google Cloud:** OpenAI partner models on Agent Platform are designated as "Advanced AI" models under Google's [Advanced AI Safety Addendum](https://cloud.google.com/terms/advanced-ai-safety-addendum) . Enabling these models requires one-time project consent in Model Garden. This consent permits Google Cloud to log prompts and responses for up to 30 days in Google-owned US storage solely to detect abuse and policy violations.
- **No human review during Private Preview:** During Private Preview, neither Google nor OpenAI uses human reviewers to assess customer prompts, file inputs, or model responses. Automated classifiers and safety systems evaluate requests within the serving boundary.
- **Zero model training:** Neither Google nor OpenAI uses customer prompts, inputs, or responses to train, fine-tune, or improve any AI/ML models.

For additional details, see [Abuse monitoring](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/abuse-monitoring) .

## Zero Data Retention (ZDR)

Zero Data Retention (ZDR) is configured at the Google Cloud project level and is off by default for all OpenAI partner models on Agent Platform. Until ZDR is approved and active for your project, requests remain subject to 30-day abuse-monitoring logs under the [Advanced AI Safety Addendum](https://cloud.google.com/terms/advanced-ai-safety-addendum) . In addition, enabling a model in Model Garden still presents the Addendum consent prompt.

Existing direct OpenAI API ZDR approvals or setting `store: false` in API requests don't configure ZDR on Agent Platform. Setting `store: false` configures requests to be stateless, but doesn't grant or guarantee ZDR. ZDR requires project-level approval from OpenAI and confirmation during onboarding.

### What ZDR means on Agent Platform

When ZDR is approved and distributed for a Google Cloud project, OpenAI's [API Data Controls](https://platform.openai.com/docs/guides/your-data) commitments apply alongside Google Cloud enforcement:

- **Real-time processing with no persistence at rest:** Customer prompts, file inputs, and model responses are processed in real time. They aren't stored on persistent disk or retained in 30-day abuse-monitoring logs, and undergo zero human review.
- **Ephemeral in-memory prompt caching:** Automatic prompt caching stores derived key-value prefix representations encrypted strictly in volatile RAM. Cached data is never written to persistent disk and is evicted automatically within 24 hours.
- **Operational telemetry and billing metadata:** Standard operational metrics such as request counts, latency, and token counts continue to be recorded for quota management and billing.

### Request ZDR and verify activation

To enable ZDR for your Google Cloud projects, follow these steps:

1.  Contact your Google Cloud account team and provide the Google Cloud project IDs and project numbers that you want covered by ZDR.
2.  Your Google Cloud account team submits your request to OpenAI. OpenAI reviews and decides whether to approve ZDR for your organization and specified projects.
3.  After OpenAI approves ZDR and issues confirmation, Google Cloud applies the ZDR configuration to your approved Google Cloud projects. This configuration distributes to all serving infrastructure within 24 hours.
4.  After distribution completes, ZDR is active for the approved Google Cloud project. Verify that ZDR is active by checking for the **Zero Data Retention active** banner on the model page in Model Garden. In an active ZDR project, prompts and model responses are excluded from 30-day safety logs. The Advanced AI Safety Addendum consent prompt no longer appears when enabling the model.

See also [Agent Platform and zero data retention](https://docs.cloud.google.com/gemini-enterprise-agent-platform/resources/zero-data-retention) .

## What's next

- Learn how to use the [Responses API](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/openai/responses) .
- Configure developer tools in [Connect OpenAI Codex to Google Cloud](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/openai/codex) .
- Review [Abuse monitoring](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/abuse-monitoring) and [Zero data retention](https://docs.cloud.google.com/gemini-enterprise-agent-platform/resources/zero-data-retention) .
- Compare features in OpenAI's [Private Preview Feature Availability](https://openai-gcp-preview-feature-guide.openai.chatgpt.site/) guide.
- Explore OpenAI's [OpenAI on Google Cloud](https://developers.openai.com/api/docs/guides/google-cloud) and [Connect Codex to Google Cloud Vertex AI](https://developers.openai.com/codex/enterprise/connect-to-vertex-ai) guides.
