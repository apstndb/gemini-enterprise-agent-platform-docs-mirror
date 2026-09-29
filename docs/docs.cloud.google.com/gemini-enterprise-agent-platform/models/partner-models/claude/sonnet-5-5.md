---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/sonnet-5-5
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/sonnet-5-5
title: Claude Sonnet 5.5 on Google Cloud
description: Claude Sonnet 5.5 is built for coding, agents, and professional work at scale.
data_source: docs.cloud.google.com
---

Claude Sonnet 5.5 on Google Cloud is built for coding, agents, and professional work at scale. For full information, see [Anthropic's documentation](https://platform.claude.com/docs/en/models/sonnet-5-5/overview) .

**Retirement Date:** Not sooner than September 28, 2027.

In addition to the features of Claude Sonnet 5 on Google Cloud, Claude Sonnet 5.5 on Google Cloud adds:

  - **New thinking type value** : Claude Sonnet 5.5 on Google Cloud adds a new `thinking.type` value, `between_tools` , which is the lowest thinking setting available on this model. Claude Sonnet 5.5 on Google Cloud doesn't support `thinking: {"type": "disabled"}` . If you want to turn thinking off, or as close to off as possible, use `between_tools` . With `between_tools` , the model does no extended thinking, and the short progress updates it writes between tool calls come back as thinking blocks containing the update text. The response format is unchanged.
  - **Adaptive thinking** can be turned on or off.

[Try in Agent Studio](https://console.cloud.google.com/agent-platform/publishers/anthropic/model-garden/claude-sonnet-5-5) [View model card in Model Garden](https://console.cloud.google.com/agent-platform/publishers/anthropic/model-garden/claude-sonnet-5-5)

Model ID

`claude-sonnet-5-5`

Launch stage

GA

Supported inputs & outputs

  - Inputs:
    Text , Image , PDF
  - Outputs:
    Text

Token limits

  - Maximum input tokens: 1,000,000
  - Maximum output tokens: 128,000

Capabilities

Supported

  - [Computer use](https://docs.anthropic.com/en/docs/build-with-claude/computer-use)
  - [Web search](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/web-search)
  - [Batch predictions](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/batch)
  - [Prompt caching](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/prompt-caching)
  - [Function calling](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/use-claude#tool_use_function_calling)
  - [Count tokens](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/count-tokens)
  - [Memory tool](https://docs.anthropic.com/en/docs/agents-and-tools/tool-use/memory-tool)

Not supported

Usage types

Supported

  - [Shared Model Lineage Quota](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/quotas)
  - [Provisioned Throughput](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/provisioned-throughput)

Not supported

Technical specifications

Images

  - **Limitation and specifications:** See [Vision](https://docs.anthropic.com/en/docs/build-with-claude/vision) in Anthropic's documentation

Documents

  - **Limitation and specifications:** See [PDF support](https://docs.anthropic.com/en/docs/build-with-claude/pdf-support) in Anthropic's documentation

Versions

`claude-sonnet-5-5`

  - **Launch stage:** Generally available
  - **Release date:** September 28, 2026

Supported regions

Model availability

(Includes fixed quota & Provisioned Throughput)

United States

  - `Multi-region`

Europe

  - `Multi-region`

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

Multi-region:

  - QPM: 1,250
  - Input TPM: 12,500,000 [uncached and cache write](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/use-claude#input)
  - Output TPM: 1,250,000
  - Context length: 1,000,000

Multi-region:

  - QPM: 1,250
  - Input TPM: 12,500,000 [uncached and cache write](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/use-claude#input)
  - Output TPM: 1,250,000
  - Context length: 1,000,000

global endpoint:

  - QPM: 2,500
  - Input TPM: 25,000,000 [uncached and cache write](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/use-claude#input)
  - Output TPM: 2,500,000
  - Context length: 1,000,000

Pricing

See [Pricing](https://cloud.google.com/gemini-enterprise-agent-platform/generative-ai/pricing) .
