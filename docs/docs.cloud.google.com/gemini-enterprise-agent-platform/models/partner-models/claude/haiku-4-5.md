---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/haiku-4-5
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/haiku-4-5
title: Claude Haiku 4.5 on Google Cloud
description: Claude Haiku 4.5 on Google Cloud delivers near-frontier performance for a wide range of use cases, and stands out as one of the best coding models in the world on Agent Platform.
data_source: docs.cloud.google.com
---

Claude Haiku 4.5 on Google Cloud delivers near-frontier performance for a wide range of use cases, and is a highly capable coding model—with the right speed and cost to power free products and high-volume user experiences.

**Retirement Date:** Not sooner than Oct 15, 2026.

  - **Free tier user experiences** : Claude Haiku 4.5 on Google Cloud delivers near-frontier performance at a cost and speed that makes free agent products and agentic use cases economically viable at scale.
  - **Latency-sensitive experiences** : Claude Haiku 4.5 on Google Cloud's speed is ideal for real-time applications like customer service agents and chatbots where response time is critical.
  - **Coding sub-agents** : Use Claude Haiku 4.5 on Google Cloud to power sub-agents, enabling multi-agent systems that tackle complex refactors, migrations, and large feature builds with quality and speed.
  - **Financial analysis** : Use Claude Haiku 4.5 on Google Cloud to monitor thousands of data streams—tracking regulatory changes, market signals, and portfolio risks to preemptively adapt compliance and trading systems at previously impossible scales.
  - **Research sub-agents** : Perform parallel analyses across multiple data sources while maintaining fast response times. Ideal for rapid business intelligence, competitive analysis, and real-time decision support.
  - **Business tasks** : Claude Haiku 4.5 on Google Cloud is capable of producing and editing office files like slides, documents, and spreadsheets. It also better supports strategy and campaign planning, business analysis and brainstorming.

[Try in Agent Studio](https://console.cloud.google.com/agent-platform/generative/multimodal/create/text?model=claude-haiku-4-5) [View model card in Model Garden](https://console.cloud.google.com/agent-platform/publishers/anthropic/model-garden/claude-haiku-4-5)

Model ID

`claude-haiku-4-5`

Launch stage

GA

Supported inputs & outputs

  - Inputs:
    Image , PDF , Text
  - Outputs:
    Text

Token limits

  - Maximum input tokens: 200,000
  - Maximum output tokens: 64,000

Capabilities

Supported

  - [Web search](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/web-search)
  - [Batch predictions](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/batch)
  - [Prompt caching](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/prompt-caching)
  - [Function calling](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/use-claude#tool_use_function_calling)
  - [Extended thinking](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/use-claude#use_a_curl_command)
  - [Count tokens](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/count-tokens)

Not supported

Usage types

Supported

  - [Fixed quota](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/quotas)
  - [Provisioned Throughput](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/provisioned-throughput)

Not supported

Technical specifications

Images

  - **Limitation and specifications:** See [Vision](https://docs.anthropic.com/en/docs/build-with-claude/vision) in Anthropic's documentation

Documents

  - **Limitation and specifications:** See [PDF support](https://docs.anthropic.com/en/docs/build-with-claude/pdf-support) in Anthropic's documentation

Versions

`claude-haiku-4-5`

  - **Launch stage:** Generally available
  - **Release date:** October 15, 2025
  - **Retirement date not sooner than:** October 15, 2026

Supported regions

Model availability

(Includes fixed quota & Provisioned Throughput)

United States

  - `us-east5`

Europe

  - `europe-west1`

Global

  - `global endpoint`

ML processing

United States

  - `Multi-region`

Europe

  - `Multi-region`

Quota limits

us-east5:

  - QPM: 1,500
  - Input TPM: 1,500,000 [uncached and cache write](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/use-claude#input)
  - Output TPM: 150,000
  - Context length: 200,000

europe-west1:

  - QPM: 1,800
  - Input TPM: 1,800,000 [uncached and cache write](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/use-claude#input)
  - Output TPM: 180,000
  - Context length: 200,000

global endpoint:

  - QPM: 2,500
  - Input TPM: 2,500,000 [uncached and cache write](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/use-claude#input)
  - Output TPM: 250,000
  - Context length: 200,000

Pricing

See [Pricing](https://cloud.google.com/gemini-enterprise-agent-platform/generative-ai/pricing) .
