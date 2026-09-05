---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/models/context-cache/context-cache-for-tuned-gemini
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/context-cache/context-cache-for-tuned-gemini
title: Context Caching for Fine-tuned Gemini Models
description: Learn how to use context caching for your fine-tuned Gemini models to improve performance and reduce costs for prompts that include large amounts of context.
data_source: docs.cloud.google.com
---

You can use context caching for your fine-tuned Gemini models to improve performance and reduce costs for prompts that include large amounts of context. By caching frequently used context, you avoid re-sending large amounts of data with each request to your fine-tuned model.

The management operations ( `Read` , `Update` , `Delete` ) of the context cache for tuned Gemini models remain consistent with base models. Only cached content creation and inference require specific adjustment, which is detailed in the following sections.

## Prerequisites

**Fine-tuning a Gemini Model:** You need a deployed fine-tuned Gemini model based on a supported base model (see [Context caching overview](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/context-cache/context-cache-overview#supported_models) ). For details on how to fine-tune a Gemini model, see [Fine-tune a Gemini model](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini-use-supervised-tuning) . To get the endpoint for your deployed tuned model, see [Deploy a tuned model](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/deploy/overview#deploy_a_tuned_model) .

Make sure that you have the following information:

  - The ID and the version of the tuned Gemini model
  - The endpoint resource name for the deployed fine-tuned model

## Supported versions

Fine-tuned Gemini models support implicit caching for the following versions:

  - [Gemini 3.1 Pro](https://docs.cloud.google.com/vertex-ai/generative-ai/docs/models/gemini/3-1-pro)
  - [Gemini 3.1 Flash-Lite](https://docs.cloud.google.com/vertex-ai/generative-ai/docs/models/gemini/3-1-flash-lite)
  - [Gemini 3 Pro](https://docs.cloud.google.com/vertex-ai/generative-ai/docs/models/gemini/3-pro)
  - [Gemini 3 Flash](https://docs.cloud.google.com/vertex-ai/generative-ai/docs/models/gemini/3-flash)
  - [Gemini 2.5 Pro](https://docs.cloud.google.com/vertex-ai/generative-ai/docs/models/gemini/2-5-pro)
  - [Gemini 2.5 Flash](https://docs.cloud.google.com/vertex-ai/generative-ai/docs/models/gemini/2-5-flash)
  - [Gemini 2.5 Flash-Lite](https://docs.cloud.google.com/vertex-ai/generative-ai/docs/models/gemini/2-5-flash-lite)

Explicit caching is not supported for fine-tuned models.
