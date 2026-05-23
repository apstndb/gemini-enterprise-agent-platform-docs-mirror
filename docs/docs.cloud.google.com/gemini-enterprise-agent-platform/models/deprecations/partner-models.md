---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/models/deprecations/partner-models
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/deprecations/partner-models
title: Model deprecations (MaaS)
description: Get deprecation and shutdown details for partner models offered through Model as a Service (MaaS).
data_source: docs.cloud.google.com
---

After a period of time, [MaaS models](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/use-partner-models) are deprecated and typically replaced with newer model versions. This page lists deprecated MaaS models and their shutdown dates to help you plan and migrate to newer model versions.

## Anthropic's Claude 3 Haiku

Anthropic's Claude 3 Haiku is **deprecated as of February 23, 2026** and will be **shut down on August 23, 2026** . Anthropic's Claude 3 Haiku is available to existing customers only.

Anthropic's Claude 3 Haiku is Anthropic's fastest vision and text model for near-instant responses to basic queries, meant for seamless AI experiences mimicking human interactions.

Model ID

`claude-3-haiku`

Launch stage

deprecated

Supported inputs & outputs

  - Inputs:
    Text , Code , Images
  - Outputs:
    Text

Token limits

  - Maximum input tokens: 200,000
  - Maximum output tokens: 8,000

Capabilities

Supported

  - [Prompt caching](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/prompt-caching)
  - [Function calling](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/use-claude#tool_use_function_calling)
  - [Count tokens](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/count-tokens)

Not supported

  - [Batch predictions](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/batch)
  - [Extended thinking](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/use-claude#use_a_curl_command)

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

August 2023

Versions

`claude-3-haiku`

  - **Launch stage:** Deprecated
  - **Release date:** March 19, 2024

Supported regions

Model availability

(Includes fixed quota & Provisioned Throughput)

United States

  - `us-east5`

Europe

  - `europe-west1`

Asia Pacific

  - `asia-southeast1`

ML processing

United States

  - `Multi-region`

Europe

  - `Multi-region`

Asia Pacific

  - `asia-southeast1`

Quota limits

us-east5:

  - QPM: 245
  - TPM: 600,000 (input and output)
  - Context length: 200,000

europe-west1:

  - QPM: 75
  - TPM: 181,000 (input and output)
  - Context length: 200,000

asia-southeast1:

  - QPM: 70
  - TPM: 174,000 (input and output)
  - Context length: 200,000

Pricing

See [Pricing](https://cloud.google.com/gemini-enterprise-agent-platform/generative-ai/pricing) .

## Claude 3.5 Haiku

Claude 3.5 Haiku is **deprecated as of January 5, 2026** and will be **shut down on July 5, 2026** . Claude 3.5 Haiku is available to existing customers only.

Claude 3.5 Haiku, the next generation of Anthropic's fastest and most cost-effective model, is optimal for use cases where speed and affordability matter.

[View model card in Model Garden](https://console.cloud.google.com/agent-platform/publishers/anthropic/model-garden/claude-3-5-haiku)

Model ID

`claude-3-5-haiku`

Launch stage

deprecated

Supported inputs & outputs

  - Inputs:
    Text , Code , Images
  - Outputs:
    Text

Token limits

  - Maximum input tokens: 200,000
  - Maximum output tokens: 8,000

Capabilities

Supported

  - [Batch predictions](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/batch)
  - [Prompt caching](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/prompt-caching)
  - [Function calling](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/use-claude#tool_use_function_calling)
  - [Count tokens](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/count-tokens)

Not supported

  - [Extended thinking](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/use-claude#use_a_curl_command)

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

July 2024

Versions

`claude-3-5-haiku`

  - **Launch stage:** Deprecated
  - **Release date:** October 22, 2024

Supported regions

Model availability

(Includes fixed quota & Provisioned Throughput)

United States

  - `us-east5`

Europe

  - `europe-west1`

ML processing

United States

  - `Multi-region`

Europe

  - `Multi-region`

Quota limits

us-east5:

  - QPM: 80
  - TPM: 350,000 (input and output)
  - Context length: 200,000

europe-west1:

  - QPM: 90
  - TPM: 400,000 (input and output)
  - Context length: 200,000

Pricing

See [Pricing](https://cloud.google.com/gemini-enterprise-agent-platform/generative-ai/pricing) .

## Claude 3.7 Sonnet

Claude 3.7 Sonnet is **deprecated as of November 11, 2025** and will be **shut down on May 11, 2026** . Claude 3.7 Sonnet is available to existing customers only.

Claude 3.7 Sonnet is a state-of-the-art model for real-world software engineering tasks and agentic capabilities.

Model ID

`claude-3-7-sonnet`

Launch stage

deprecated

Supported inputs & outputs

  - Inputs:
    Text , Code , Images
  - Outputs:
    Text

Token limits

  - Maximum input tokens: 200,000
  - Maximum output tokens: 128,000

Capabilities

Supported

  - [Batch predictions](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/batch)
  - [Prompt caching](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/prompt-caching)
  - [Function calling](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/use-claude#tool_use_function_calling)
  - [Count tokens](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/count-tokens)

Not supported

  - [Extended thinking](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/use-claude#use_a_curl_command)

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

`claude-3-7-sonnet`

  - **Launch stage:** Deprecated
  - **Release date:** March 20, 2025

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

  - QPM: 55
  - TPM: 500,000 ( [uncached](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/use-claude#input) input and output)
  - Context length: 200,000

europe-west1:

  - QPM: 40
  - TPM: 300,000 ( [uncached](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/use-claude#input) input and output)
  - Context length: 200,000

global endpoint:

  - QPM: 35
  - TPM: 300,000 ( [uncached](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/use-claude#input) input and output)
  - Context length: 200,000

Pricing

See [Pricing](https://cloud.google.com/gemini-enterprise-agent-platform/generative-ai/pricing) .

## Claude 3.5 Sonnet v2

Claude 3.5 Sonnet v2 is **deprecated as of August 20, 2025** and will be **shut down on February 19, 2026** . Claude 3.5 Sonnet v2 is available to existing customers only.

Claude 3.5 Sonnet v2 is a state-of-the-art model for real-world software engineering tasks and agentic capabilities.

[Try in Agent Platform](https://console.cloud.google.com/vertex-ai/generative/multimodal/create/text?model=claude-3-5-sonnet-v2)

Model ID

`claude-3-5-sonnet-v2`

Launch stage

GA

Supported inputs & outputs

  - Inputs:
    Text , Code , Images
  - Outputs:
    Text

Token limits

  - Maximum input tokens: 200,000
  - Maximum output tokens: 8,000

Capabilities

Supported

  - [Batch predictions](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/batch)
  - [Prompt caching](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/prompt-caching)
  - [Function calling](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/use-claude#tool_use_function_calling)
  - [Count tokens](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/count-tokens)

Not supported

  - [Extended thinking](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/use-claude#use_a_curl_command)

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

August 2024

Versions

`claude-3-5-sonnet-v2`

  - **Launch stage:** Generally available
  - **Release date:** October 22, 2024

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

  - QPM: 90
  - TPM: 540,000 (input and output)
  - Context length: 200,000

europe-west1:

  - QPM: 55
  - TPM: 330,000 (input and output)
  - Context length: 200,000

global endpoint:

  - QPM: 25
  - TPM: 140,000 (input and output)
  - Context length: 200,000

Pricing

See [Pricing](https://cloud.google.com/gemini-enterprise-agent-platform/generative-ai/pricing) .

## Claude 3.5 Sonnet

Claude 3.5 Sonnet is **deprecated as of August 20, 2025** and will be **shut down on February 19, 2026** . Claude 3.5 Sonnet is available to existing customers only.

Claude 3.5 Sonnet outperforms Anthropic's Claude 3 Opus on a wide range of Anthropic's evaluations with the speed and cost of Anthropic's mid-tier model, Claude 3 Sonnet.

Model ID

`claude-3-5-sonnet`

Launch stage

GA

Supported inputs & outputs

  - Inputs:
    Text , Code , Images
  - Outputs:
    Text

Token limits

  - Maximum input tokens: 200,000
  - Maximum output tokens: 8,000

Capabilities

Supported

  - [Prompt caching](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/prompt-caching)
  - [Function calling](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/use-claude#tool_use_function_calling)
  - [Count tokens](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/count-tokens)

Not supported

  - [Batch predictions](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/batch)
  - [Extended thinking](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/use-claude#use_a_curl_command)

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

April 2024

Versions

`claude-3-5-sonnet`

  - **Launch stage:** Generally available
  - **Release date:** June 20, 2024

Supported regions

Model availability

(Includes fixed quota & Provisioned Throughput)

United States

  - `us-east5`

Europe

  - `europe-west1`

Asia Pacific

  - `asia-southeast1`

ML processing

United States

  - `Multi-region`

Europe

  - `Multi-region`

Asia Pacific

  - `asia-southeast1`

Quota limits

us-east5:

  - QPM: 80
  - TPM: 350,000 (input and output)
  - Context length: 200,000

europe-west1:

  - QPM: 130
  - TPM: 600,000 (input and output)
  - Context length: 200,000

asia-southeast1:

  - QPM: 35
  - TPM: 150,000 (input and output)
  - Context length: 200,000

Pricing

See [Pricing](https://cloud.google.com/gemini-enterprise-agent-platform/generative-ai/pricing) .

## Jamba 1.5 Large

Jamba 1.5 Large is **deprecated as of August 27, 2025** and will be **shut down on February 27, 2026** . Jamba 1.5 Large is available to existing customers only.

AI21 Labs's Jamba 1.5 Large is well balanced across quality, throughput, and low cost.

[View model card in Model Garden](https://console.cloud.google.com/agent-platform/model-garden)

Model ID

`jamba-1.5-large`

Launch stage

Preview

Supported inputs & outputs

  - Inputs:
    Text , Documents
  - Outputs:
    Text

Usage types

Supported

  - [Fixed quota](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/quotas)

Not supported

  - [Provisioned Throughput](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/provisioned-throughput)

Knowledge cutoff date

March 2024

Versions

`jamba-1.5-large`

  - **Launch stage:** Preview
  - **Release date:** August 22, 2024

Supported regions

Model availability

United States

  - `us-central1`

Europe

  - `europe-west4`

ML processing

United States

  - `Multi-region`

Quota limits

us-central1:

  - QPM: 20
  - TPM: 20,000
  - Context length: 256,000

europe-west4:

  - QPM: 20
  - TPM: 20,000
  - Context length: 256,000

Pricing

See [Pricing](https://cloud.google.com/gemini-enterprise-agent-platform/generative-ai/pricing) .

## Jamba 1.5 Mini

Jamba 1.5 Mini is **deprecated as of August 27, 2025** and will be **shut down on February 27, 2026** . Jamba 1.5 Mini is available to existing customers only.

AI21 Labs's Jamba 1.5 Mini is well balanced across quality, throughput, and low cost.

[View model card in Model Garden](https://console.cloud.google.com/agent-platform/model-garden)

Model ID

`jamba-1.5-mini`

Launch stage

Preview

Supported inputs & outputs

  - Inputs:
    Text , Documents
  - Outputs:
    Text

Usage types

Supported

  - [Fixed quota](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/quotas)

Not supported

  - [Provisioned Throughput](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/provisioned-throughput)

Knowledge cutoff date

March 2024

Versions

`jamba-1.5-mini`

  - **Launch stage:** Preview
  - **Release date:** August 22, 2024

Supported regions

Model availability

United States

  - `us-central1`

Europe

  - `europe-west4`

ML processing

United States

  - `Multi-region`

Quota limits

us-central1:

  - QPM: 50
  - TPM: 60,000
  - Context length: 256,000

europe-west4:

  - QPM: 50
  - TPM: 60,000
  - Context length: 256,000

Pricing

See [Pricing](https://cloud.google.com/gemini-enterprise-agent-platform/generative-ai/pricing) .

## Claude 3 Opus

Anthropic's Claude 3 Opus is **deprecated as of June 30, 2025** and will be **shut down on August 1, 2025** . Claude 3 Opus is available to existing customers only.

Anthropic's Claude 3 Opus is a powerful AI model with top-level performance on highly complex tasks. It can navigate open-ended prompts and sight-unseen scenarios with remarkable fluency and human-like understanding. Claude 3 Opus is optimized for the following use cases:

  - Task automation, such as interactive coding and planning, or running complex actions across APIs and databases.

  - Research and development tasks, such as research review, brainstorming and hypothesis generation, and product testing.

  - Strategy tasks, such as advanced analysis of charts and graphs, financials and market trends, and forecasting.

  - Vision tasks, such as processing images to return text output. Also, analysis of charts, graphs, technical diagrams, reports, and other visual content.

Model ID

`claude-3-opus`

Launch stage

deprecated

Supported inputs & outputs

  - Inputs:
    Text , Code , Images
  - Outputs:
    Text

Token limits

  - Maximum input tokens: 200,000
  - Maximum output tokens: 8,000

Capabilities

Supported

  - [Prompt caching](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/prompt-caching)
  - [Function calling](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/use-claude#tool_use_function_calling)
  - [Count tokens](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/count-tokens)

Not supported

  - [Batch predictions](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/batch)
  - [Extended thinking](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/use-claude#use_a_curl_command)

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

August 2023

Versions

`claude-3-opus`

  - **Launch stage:** Deprecated
  - **Release date:** May 31, 2024

Supported regions

Model availability

(Includes fixed quota & Provisioned Throughput)

United States

  - `us-east5`

ML processing

United States

  - `Multi-region`

Quota limits

us-east5:

  - QPM: 20
  - TPM: 105,000 (input and output)
  - Context length: 200,000

Pricing

See [Pricing](https://cloud.google.com/gemini-enterprise-agent-platform/generative-ai/pricing) .
