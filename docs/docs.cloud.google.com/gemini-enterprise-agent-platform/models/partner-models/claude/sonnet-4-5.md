---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/sonnet-4-5
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/sonnet-4-5
title: Claude Sonnet 4.5
description: Model details for Claude Sonnet 4.5
data_source: docs.cloud.google.com
---

Anthropic's mid-sized model for powering real-world agents, with capabilities in coding, computer use, cybersecurity, and working with office files like spreadsheets.

[Try in Agent Platform](https://console.cloud.google.com/vertex-ai/generative/multimodal/create/text?model=claude-sonnet-4-5) [View model card in Model Garden](https://console.cloud.google.com/agent-platform/publishers/anthropic/model-garden/claude-sonnet-4-5)

Model ID

`claude-sonnet-4-5`

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

July, 2025

Versions

`claude-sonnet-4-5`

  - **Launch stage:** Generally available
  - **Release date:** September 29, 2025
  - **Retirement date not sooner than:** September 29, 2026

Supported regions

Model availability

(Includes fixed quota & Provisioned Throughput)

United States

  - `us-east5`

Europe

  - `europe-west1`

Asia Pacific

  - `asia-southeast1`

Global

  - `global endpoint`

ML processing

United States

  - `Multi-region`

Europe

  - `Multi-region`

Asia Pacific

  - `asia-southeast1`

Quota limits

us-east5:

  - QPM: 1,500
  - Input TPM: 1,500,000 [uncached and cache write](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/use-claude#input)
  - Output TPM: 150,000
  - Context length: 1,000,000 (beta), 200,000 (GA)

europe-west1:

  - QPM: 1,800
  - Input TPM: 1,800,000 [uncached and cache write](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/use-claude#input)
  - Output TPM: 180,000
  - Context length: 1,000,000 (beta), 200,000 (GA)

asia-southeast1:

  - QPM: 1,500
  - Input TPM: 1,500,000 [uncached and cache write](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/use-claude#input)
  - Output TPM: 150,000
  - Context length: 1,000,000 (beta), 200,000 (GA)

global endpoint:

  - QPM: 1,500
  - Input TPM: 1,500,000 [uncached and cache write](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/use-claude#input)
  - Output TPM: 150,000
  - Context length: 1,000,000 (beta), 200,000 (GA)

Pricing

See [Pricing](https://cloud.google.com/gemini-enterprise-agent-platform/generative-ai/pricing) .
