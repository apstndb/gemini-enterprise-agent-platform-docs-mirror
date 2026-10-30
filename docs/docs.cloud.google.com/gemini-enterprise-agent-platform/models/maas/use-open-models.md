---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/models/maas/use-open-models
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/maas/use-open-models
title: Gemini Enterprise Agent Platform open models for MaaS
description: Understand Gemini Enterprise Agent Platform's managed open models as a service (MaaS). Discover, deploy, and use serverless open models, including embedding models.
data_source: docs.cloud.google.com
---

Gemini Enterprise Agent Platform supports a curated list of open models as managed models. These open models can be used with [Gemini Enterprise Agent Platform](https://docs.cloud.google.com/gemini-enterprise-agent-platform) as a model as a service (MaaS) and are offered as a managed API. When you use a managed open model, you continue to send your requests to Gemini Enterprise Agent Platform endpoints. Managed open models are serverless, so there's no need to provision or manage infrastructure.

Managed open models can be discovered using Model Garden. You can also deploy models using Model Garden. For more information, see [Explore AI models in Model Garden](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/model-garden/explore-models) .

Before you can use open models, you need to [grant user access to open models](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/maas/grant-access-open-models) .

## Open models

The following open models are offered as managed APIs on Gemini Enterprise Agent Platform Model Garden (MaaS):

| Model name                | Modality               | Description                                                                                                                                                                                                                                                          | Quickstart                                                                                                                         |
|---------------------------|------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------|
| DeepSeek-V4.1-Flash       | Language, Vision, Code | DeepSeek's multimodal Mixture-of-Experts model for agentic and coding tasks, with a 1M-token context window.                                                                                                                                                         | [Model card](https://console.cloud.google.com/agent-platform/publishers/deepseek-ai/model-garden/deepseek-v4.1-flash-maas)         |
| Gemma 4 26B A4B IT        | Language, Vision       | Google's family of open models built by Google DeepMind.                                                                                                                                                                                                             | [Model card](https://console.cloud.google.com/agent-platform/publishers/google/model-garden/gemma-4-26b-a4b-it-maas)               |
| GLM 5.2                   | Language, Code         | GLM's model for long-horizon agentic and coding tasks, with a 1M-token context window.                                                                                                                                                                               | [Model card](https://console.cloud.google.com/agent-platform/publishers/zai-org/model-garden/glm-5.2-maas)                         |
| gpt-oss 120B              | Language               | A 120B model that offers high performance on reasoning tasks.                                                                                                                                                                                                        | [Model card](https://console.cloud.google.com/agent-platform/publishers/openai/model-garden/gpt-oss-120b-maas)                     |
| Llama 4 Maverick 17B-128E | Language, Vision       | The largest Llama 4 model that has coding, reasoning, and image capabilities. Llama 4 Maverick 17B-128E is a multimodal model that uses the Mixture-of-Experts (MoE) architecture and early fusion.                                                                  | [Model card](https://console.cloud.google.com/agent-platform/publishers/meta/model-garden/llama-4-maverick-17b-128e-instruct-maas) |
| Llama 4 Scout 17B-16E     | Language, Vision       | Llama 4 Scout 17B-16E delivers high-performance results for its size class, outperforming other open and proprietary models on several benchmarks. Llama 4 Scout 17B-16E is a multimodal model that uses the Mixture-of-Experts (MoE) architecture and early fusion. | [Model card](https://console.cloud.google.com/agent-platform/publishers/meta/model-garden/llama-4-maverick-17b-128e-instruct-maas) |

The following open embedding models are offered as managed APIs on Gemini Enterprise Agent Platform Model Garden (MaaS):

| Model name            | Description                                                                       | Output dimensions | Max sequence length | Supported text languages                                                                         | Quickstart                                                                                                                         |
|-----------------------|-----------------------------------------------------------------------------------|-------------------|---------------------|--------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------|
| multilingual-e5-small | Part of the E5 family of text embedding models. Small variant contains 12 layers. | Up to 384         | 512 tokens          | [Supported languages](https://huggingface.co/intfloat/multilingual-e5-small#supported-languages) | [Model card](https://console.cloud.google.com/agent-platform/publishers/intfloat/model-garden/multilingual-e5-large-instruct-maas) |
| multilingual-e5-large | Part of the E5 family of text embedding models. Large variant contains 24 layers. | Up to 1024        | 512 tokens          | [Supported languages](https://huggingface.co/intfloat/multilingual-e5-small#supported-languages) | [Model card](https://console.cloud.google.com/agent-platform/publishers/intfloat/model-garden/multilingual-e5-large-instruct-maas) |

## Open model regulatory compliance

The [certifications](https://cloud.google.com/security/compliance/services-in-scope/) for [Generative AI on Gemini Enterprise Agent Platform](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models) continue to apply when open models are used as a managed API using Gemini Enterprise Agent Platform. If you need details about the models themselves, additional information can be found in the respective model card, or you can contact the respective model publisher.

Your data is stored at rest within the selected region or multi-region for open models on Gemini Enterprise Agent Platform, but the regionalization of data processing may vary. For a detailed list of open models' data processing commitments, see [Data residency for open models](https://docs.cloud.google.com/gemini-enterprise-agent-platform/resources/locations#genai-open-models) .

Customer prompts and model responses are not shared with third parties when using the Gemini Enterprise API, including open models. Google only processes customer data as instructed by the customer, which is further described in our [Cloud Data Processing Addendum](https://cloud.google.com/terms/data-processing-addendum) .

## Context caching

> **Preview**
>
> This product or feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](https://docs.cloud.google.com/terms/service-terms#1) . Pre-GA products and features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

Context caching helps reduce the cost and latency of requests to Open Models that contain repeated content. This is enabled while using pay-as-you-go traffic only, and doesn't support other traffic types, such as Provisioned Throughput and Batch.

The supported type of caching is implicit caching, which is automatic caching that's enabled in all Google Cloud projects by default and provides a 90% discount on cached tokens compared to standard input tokens when cache hits occur. With this type of caching, you don't define and call the caches explicitly. Instead, our backend pulls from these caches once repeated context is detected.

### Supported models

- qwen3-coder-480b-a35b-instruct-maas
- kimi-k2-thinking-maas
- minimax-m2-maas
- gpt-oss-20b-maas
- deepseek-v3.1-maas
- deepseek-v3.2-maas
- deepseek-v4.1-flash-maas
- gemma-4-26b-a4b-it-maas
- glm-5-maas
- glm-5.2-maas

The [`cachedContentTokenCount`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/GenerateContentResponse) field in your response's metadata indicates the number of tokens in the cached part of your input. Caching requests must contain a minimum of 4096 tokens (this minimum is subject to change during Preview).

When enabled, implicit cache hit cost savings are automatically passed on to you. Cache hits aren't guaranteed and are dependent on requests sent and other factors. To increase the chances of an implicit cache hit, try the following:

- Place large and common contents at the beginning of your prompt.
- Send requests with a similar prefix in a short amount of time.

## What's next

- Before using open models, [Grant user access to open models](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/maas/grant-access-open-models) .
- Learn how to [Call open model APIs](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/maas/call-open-model-apis) .
