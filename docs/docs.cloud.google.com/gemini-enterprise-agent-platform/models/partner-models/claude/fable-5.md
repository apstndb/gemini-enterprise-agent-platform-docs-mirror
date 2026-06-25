---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/fable-5
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/fable-5
title: Claude Fable 5
description: Claude Fable 5 is optimized for autonomous knowledge work and coding, handling long-running, complex, and asynchronous tasks.
data_source: docs.cloud.google.com
---

Claude Fable 5 is optimized for autonomous knowledge work and coding, handling long-running, complex, and asynchronous tasks.

> **Advanced AI Safety Notice:** Claude Fable 5 is within the scope of the [Advanced AI Safety Addendum](https://cloud.google.com/terms/advanced-ai-safety-addendum) . All prompts and responses are stored for up to 60 days for the sole purpose of monitoring for potential abuse of relevant terms of service. See [Responsible AI](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/responsible-ai) and [Abuse Monitoring](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/abuse-monitoring#advanced_ai_safety) to learn more.

**Retirement Date:** Not sooner than June 8, 2027.

[Try in Agent Studio](https://console.cloud.google.com/agent-platform/publishers/anthropic/model-garden/claude-fable-5) [View model card in Model Garden](https://console.cloud.google.com/agent-platform/publishers/anthropic/model-garden/claude-fable-5)

Model ID

`claude-fable-5`

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

`claude-fable-5`

  - **Launch stage:** Generally available
  - **Release date:** June 9, 2026

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

  - QPM: 1,000
  - Input TPM: 10,000,000 [uncached and cache write](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/use-claude#input)
  - Output TPM: 1,000,000
  - Context length: 1,000,000

Multi-region:

  - QPM: 1,000
  - Input TPM: 10,000,000 [uncached and cache write](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/use-claude#input)
  - Output TPM: 1,000,000
  - Context length: 1,000,000

global endpoint:

  - QPM: 2,000
  - Input TPM: 20,000,000 [uncached and cache write](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/use-claude#input)
  - Output TPM: 2,000,000
  - Context length: 1,000,000

Pricing

See [Pricing](https://cloud.google.com/gemini-enterprise-agent-platform/generative-ai/pricing) .

## Enable Claude Fable 5 in your project

Follow these steps to enable Claude Fable 5 in your project:

  - Consent to the [Advanced AI Safety Addendum](https://cloud.google.com/terms/advanced-ai-safety-addendum) in Model Garden (required once per project). See [Abuse Monitoring](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/abuse-monitoring#advanced_ai_safety) to learn more.
  - For online terms customers, click 'enable' on the [Model Garden model card](https://console.cloud.google.com/agent-platform/publishers/anthropic/model-garden/claude-fable-5) to:
      - Answer relevant company and use case questions in Model Garden.
      - Accept Anthropic and Marketplace terms of service in Cloud Marketplace.
  - For Private Offer customers:
      - [Accept the Private Offer in Cloud Marketplace](https://docs.cloud.google.com/marketplace/docs/offers/accepting-private-offer) (required once per Billing Account).
      - Enable the model location using the `enableModel` API
  - As required by Section F of Anthropic's [Service Specific Terms](https://www.anthropic.com/legal/service-specific-terms) , enable prompt-response sharing with Anthropic for each model location. See [Request-Response Logging and Sharing](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/capabilities/request-response-logging#share-requests-responses-with-maas-partners) to learn more.
