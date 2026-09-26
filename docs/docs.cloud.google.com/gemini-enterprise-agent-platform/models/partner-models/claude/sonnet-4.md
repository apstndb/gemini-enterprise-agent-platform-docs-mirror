---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/sonnet-4
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/sonnet-4
title: Claude Sonnet 4 on Google Cloud
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Claude Sonnet 4 on Google Cloud balances impressive performance for coding with the right speed and cost for high-volume use cases:

**Retirement Date:** Not sooner than May 14, 2026.

  - **Coding** : Handle everyday development tasks with enhanced performance—power code reviews, bug fixes, API integrations, and feature development with immediate feedback loops.
  - **AI Assistants** : Power production-ready assistants for real-time applications—from customer support automation to operational workflows that require both intelligence and speed.
  - **Efficient research** : Perform focused analysis across multiple data sources while maintaining fast response times. Ideal for rapid business intelligence, competitive analysis, and real-time decision support.
  - **Large-scale content** : Generate and analyze content at scale with improved quality. Create customer communications, analyze user feedback, and produce marketing materials with the right balance of quality and throughput.

[Try in Agent Studio](https://console.cloud.google.com/agent-platform/generative/multimodal/create/text?model=claude-sonnet-4) [View model card in Model Garden](https://console.cloud.google.com/agent-platform/publishers/anthropic/model-garden/claude-sonnet-4)

Model ID

`claude-sonnet-4`

Launch stage

GA

Supported inputs & outputs

  - Inputs:
    Text , Code , Images
  - Outputs:
    Text

Token limits

  - Maximum input tokens: 1M (Preview)  
    200,000 (GA)
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

Knowledge cutoff date

March 2025

Versions

`claude-sonnet-4`

  - **Launch stage:** Generally available
  - **Release date:** May 22, 2025
  - **Retirement date not sooner than:** May 14, 2026

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

  - QPM: 35
  - Input TPM: 280,000 [uncached and cache write](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/use-claude#input)
  - Output TPM: 20,000
  - Context length: 1,000,000

europe-west1:

  - QPM: 25
  - Input TPM: 180,000 [uncached and cache write](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/use-claude#input)
  - Output TPM: 20,000
  - Context length: 1,000,000

global endpoint:

  - QPM: 35
  - Input TPM: 276,000 [uncached and cache write](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/use-claude#input)
  - Output TPM: 24,000
  - Context length: 1,000,000

Pricing

See [Pricing](https://cloud.google.com/gemini-enterprise-agent-platform/generative-ai/pricing) .
