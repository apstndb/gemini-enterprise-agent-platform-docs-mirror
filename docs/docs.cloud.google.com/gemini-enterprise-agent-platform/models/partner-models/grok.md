---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/grok
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/grok
title: xAI Grok models
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

> **Note:** xAI models are not Google products, and their availability in Gemini Enterprise Agent Platform is subject to the terms for "Separate Offerings" in the AI/ML Services section of the [Service Specific Terms](https://cloud.google.com/terms/service-terms) , and separate terms found in the relevant model card.

xAI Grok models are available for use as managed APIs on Gemini Enterprise Agent Platform. You can stream your responses to reduce the end-user latency perception. A streamed response uses *server-sent events* (SSE) to incrementally stream the response.

## Managed xAI models

The following models are available from xAI to use in Gemini Enterprise Agent Platform. To access an xAI model, go to its Model Garden model card.

[Grok 4.6](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/grok/grok-4-6) A high-capability model from xAI, built for coding, agentic tasks, and knowledge work.

[Grok 4.3](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/grok/grok-4-3) A high-performance model from xAI.

[Grok 4.20 (Reasoning)](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/grok/grok-4-20#reasoning) A high-performance model from xAI, featuring a low hallucination rate. Excels at document understanding tasks and long-horizon agentic tool calling.

[Grok 4.20 (Non-reasoning)](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/grok/grok-4-20#non-reasoning) A high-performance non-thinking model from xAI, featuring a low hallucination rate. Excels in latency-sensitive use cases like customer support and categorization.

block [Grok 4.1 Fast (Reasoning)](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/grok/grok-4-1-fast#reasoning) (Deprecated) A cost-effective model from xAI, featuring strong tool-calling capabilities and efficient knowledge base synthesis. Excels at search tasks involving web data and internal knowledge base tools.

block [Grok 4.1 Fast (Non-reasoning)](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/grok/grok-4-1-fast#non-reasoning) (Deprecated) A cost-effective non-thinking model from xAI, optimized for low-latency performance. Excels at high-volume tasks like summarization and categorization.

## Use xAI models

To learn how to make streaming and non-streaming calls to xAI models, see [Call open model APIs](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/maas/call-open-model-apis) .

For managed models, you can use curl commands to send requests to the Gemini Enterprise Agent Platform endpoint using the following model names:

  - For Grok 4.6, use `grok-4.6`
  - For Grok 4.3, use `grok-4.3`
  - For Grok 4.20 (Reasoning), use `grok-4.20-reasoning`
  - For Grok 4.20 (Non-reasoning), use `grok-4.20-non-reasoning`
  - For Grok 4.1 Fast (Reasoning), use `grok-4.1-fast-reasoning`
  - For Grok 4.1 Fast (Non-reasoning), use `grok-4.1-fast-non-reasoning`

## Grok quotas

Grok models have a single global quota that applies per base model rather than per endpoint: requests to the global endpoint and the US multi-region endpoint draw on the same underlying limit. The quota is specified in queries per minute (QPM) and tokens per minute (TPM), where TPM includes both input and output tokens.

To maintain overall service performance and acceptable use, the maximum quotas might vary by account and, in some cases, access might be restricted. View your project's quotas on the [**Quotas & System Limits**](https://console.cloud.google.com/quotas) page in the Google Cloud console. You must also have the following quotas available:

  - `global_generate_content_requests_per_minute_per_project_per_base_model` defines your QPM quota.

  - For TPM, there are two quota values that apply to particular models: `global_generate_content_input_tokens_per_minute_per_base_model` defines the input TPM quota and `global_generate_content_output_tokens_per_minute_per_base_model` defines the output TPM quota.

To see which models count input and output tokens separately, see the specific model pages.

## What's next

  - Learn how to [Call open model APIs](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/maas/call-open-model-apis) .
  - Learn how to [Call Responses API](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/grok/responses) .
