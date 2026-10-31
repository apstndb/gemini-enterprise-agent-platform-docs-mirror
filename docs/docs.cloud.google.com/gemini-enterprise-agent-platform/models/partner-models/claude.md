---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude
title: Anthropic's Claude on Google Cloud models
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

> **Note:** Anthropic models are not a Google product, and their availability in Gemini Enterprise Agent Platform is subject to the terms for "Separate Offerings" in the AI/ML Services section of the [Service Specific Terms](https://cloud.google.com/terms/service-terms) , and separate terms found in the relevant model card.

The Anthropic Claude models on Google Cloud offer fully managed and serverless models as APIs. To use a Claude model on Agent Platform, send a request directly to the Agent Platform API endpoint. Because the Anthropic Claude models use a managed API, there's no need to provision or manage infrastructure. To use Anthropic's Claude developer platform on Anthropic-managed infrastructure instead, see [Use Claude models on Google Cloud (Anthropic managed)](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/anthropic-managed) .

You can stream your Claude responses to reduce the end-user latency perception. A streamed response uses server-sent events (SSE) to incrementally stream the response.

You pay for Claude models as you use them (pay as you go), or you pay a fixed fee when using [provisioned throughput](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/provisioned-throughput) . For pay-as-you-go pricing, see [Anthropic Claude models on the Google Cloud pricing page](https://cloud.google.com/gemini-enterprise-agent-platform/generative-ai/pricing#partner-models) .

## Available Claude on Google Cloud models

> **Important:** Accessing Claude on Google Cloud models through Agent Platform meets the FedRAMP High requirements, and operates within the Google Cloud FedRAMP High authorization boundary.

The following models are available from Anthropic to use in Gemini Enterprise Agent Platform. To access a Claude on Google Cloud model, go to its Model Garden model card.

Anthropic's Claude models support Agent Platform request-response logging. Enable 30-day request-response logging of your prompt and completion activity to track any model misuse by your users. For more information, see [Log requests and responses](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/capabilities/request-response-logging) .

To log token counts, latency and errors for every Claude request without storing prompts or responses, see [Log inference request metadata](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/capabilities/inference-metadata-logging) . For Claude field names, see [Token counts for Claude models](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/capabilities/inference-metadata-logging#claude-models) .

## Claude Fable models

cognition [Anthropic's Claude Fable 5.1 on Google Cloud](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/fable-5-1) Optimized for autonomous knowledge work and coding, handling long-running, complex, and asynchronous tasks.

cognition [Anthropic's Claude Fable 5 on Google Cloud](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/fable-5) Optimized for autonomous knowledge work and coding, handling long-running, complex, and asynchronous tasks with agent harnesses.

## Claude Opus models

arrow_selector_tool [Anthropic's Claude Opus 5.5 on Google Cloud](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/opus-5-5) Anthropic's most advanced Opus model, powering long-running agents while delivering improvements in coding and professional work.

arrow_selector_tool [Anthropic's Claude Opus 5 on Google Cloud](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/opus-5) A high-intelligence model from Anthropic, built for coding, agents, and professional work.

arrow_selector_tool [Anthropic's Claude Opus 4.8 on Google Cloud](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/opus-4-8) A high-intelligence Opus model built for coding and agents, featuring deep reasoning for enterprise workflows.

arrow_selector_tool [Anthropic's Claude Opus 4.7 on Google Cloud](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/opus-4-7) Optimized for coding, enterprise agents, UI design, and multi-day enterprise workflows.

arrow_selector_tool [Anthropic's Claude Opus 4.6 on Google Cloud](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/opus-4-6) Optimized for coding, enterprise agents, real-time operational workflows, and professional work.

arrow_selector_tool [Anthropic's Claude Opus 4.5 on Google Cloud](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/opus-4-5) Optimized for coding, agents, computer use, and sprawling enterprise workflows.

## Claude Sonnet models

graph_5 [Anthropic's Claude Sonnet 5.5 on Google Cloud](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/sonnet-5-5) Built for coding, agents, and professional work at scale.

graph_5 [Anthropic's Claude Sonnet 5 on Google Cloud](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/sonnet-5) Built for coding, agents, and professional work at scale.

graph_5 [Anthropic's Claude Sonnet 4.6 on Google Cloud](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/sonnet-4-6) Delivers frontier intelligence at scale—built for coding, agents, cybersecurity, and enterprise workflows.

graph_5 [Anthropic's Claude Sonnet 4.5 on Google Cloud](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/sonnet-4-5) Built for powering real-world agents with strong capabilities across coding, computer use, and office files.

## Claude Haiku models

raven [Anthropic's Claude Haiku 5.5 on Google Cloud](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/haiku-5-5) High-performance, cost-effective model built for coding, sub-agents, and latency-sensitive experiences at scale.

raven [Anthropic's Claude Haiku 4.5 on Google Cloud](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/haiku-4-5) High-performance model with the speed and cost efficiency to power free products and latency-sensitive experiences at scale.

## Claude models on Google Cloud (Anthropic managed)

**Claude models on Google Cloud (Anthropic managed)** is a service that lets you use Anthropic's Claude developer platform in Google Cloud. Use it to access Anthropic's latest features—including new models and research previews—the same day that they're released by Anthropic.

For more information, see [Use Claude models on Google Cloud (Anthropic managed)](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/anthropic-managed) .
