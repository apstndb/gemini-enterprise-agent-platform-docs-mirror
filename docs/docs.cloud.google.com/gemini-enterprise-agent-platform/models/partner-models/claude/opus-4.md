---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/opus-4
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/opus-4
title: Claude Opus 4
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Anthropic's Claude Opus 4 delivers sustained performance on long-running tasks that require focused effort and thousands of steps, significantly expanding what AI agents can solve.

[Try in Agent Studio](https://console.cloud.google.com/vertex-ai/generative/multimodal/create/text?model=claude-opus-4) [View model card in Model Garden](https://console.cloud.google.com/agent-platform/publishers/anthropic/model-garden/claude-opus-4)

Model ID

`claude-opus-4`

Launch stage

GA

Supported inputs & outputs

  - Inputs:
    Text , Code , Images
  - Outputs:
    Text

Token limits

  - Maximum input tokens: 200,000
  - Maximum output tokens: 32,000

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

November 2024

Versions

`claude-opus-4`

  - **Launch stage:** Generally available
  - **Release date:** May 22, 2025
  - **Retirement date not sooner than:** May 14, 2026

Supported regions

Model availability

(Includes fixed quota & Provisioned Throughput)

United States

  - `us-east5`

Global

  - `global endpoint`

ML processing

United States

  - `Multi-region`

Quota limits

us-east5:

  - QPM: 25
  - Input TPM: 60,000 [uncached and cache write](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/use-claude#input)
  - Output TPM: 6,000
  - Context length: 200,000

global endpoint:

  - QPM: 25
  - Input TPM: 60,000 [uncached and cache write](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/use-claude#input)
  - Output TPM: 6,000
  - Context length: 200,000

Pricing

See [Pricing](https://cloud.google.com/gemini-enterprise-agent-platform/generative-ai/pricing) .
