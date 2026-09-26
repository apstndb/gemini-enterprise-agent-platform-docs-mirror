---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/llama/llama4-maverick
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/llama/llama4-maverick
title: Llama 4 Maverick 17B-128E
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Llama 4 Maverick 17B-128E is the largest and most capable Llama 4 model that offers coding, reasoning, and image capabilities. It features Mixture-of-Experts (MoE) architecture with 17 billion active parameters out of 400 billion total parameters and 128 experts. Llama 4 Maverick 17B-128E uses alternating dense and MoE layers, where each token activates a shared expert plus one of the 128 routed experts. The model is pretrained on 200 languages and optimized for high-quality chat interactions through a refined post-training pipeline.

Llama 4 Maverick 17B-128E is multimodal and is suited for advanced image captioning, analysis, precise image understanding, visual questions and answers, creative text generation, general-purpose AI assistants, and sophisticated chatbots requiring top-tier intelligence and image understanding.

## Managed API (MaaS) specifications

[Try in Agent Studio](https://console.cloud.google.com/agent-platform/generative/multimodal/create/text?model=llama-4-maverick-17b-128e-instruct-maas) [View model card in Model Garden](https://console.cloud.google.com/agent-platform/publishers/meta/model-garden/llama-4-maverick-17b-128e-instruct-maas)

Model ID

`llama-4-maverick-17b-128e-instruct-maas`

Launch stage

GA

Supported inputs & outputs

  - Inputs:
    Text , Code , Images
  - Outputs:
    Text

Capabilities

Supported

  - [Batch predictions](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/maas/capabilities/batch-prediction)
  - [Function calling](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/maas/capabilities/function-calling)
  - [Structured output](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/maas/capabilities/structured-output)

Not supported

  - [Llama Guard](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/llama)

Usage types

Supported

  - [Standard pay-as-you-go](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/standard-paygo)
  - [Provisioned Throughput](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/provisioned-throughput)

Not supported

  - [Fixed quota](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/quotas)

Knowledge cutoff date

August 2024

Versions

`llama-4-maverick-17b-128e-instruct-maas`

  - **Launch stage:** GA
  - **Release date:** April 29, 2025

Supported regions

Model availability

United States

  - `us-east5`

ML processing

United States

  - `Multi-region`

Quota limits

us-east5:

  - Max output: 8,192
  - Context length: 524,288

Pricing

See [Pricing](https://cloud.google.com/gemini-enterprise-agent-platform/generative-ai/pricing) .

## Deploy as a self-deployed model

To self-deploy the model, navigate to the [Llama 4 Maverick 17B-128E model card](https://console.cloud.google.com/agent-platform/publishers/meta/model-garden/llama4) in the Model Garden console and click **Deploy model** . For more information about deploying and using partner models, see [Deploy a partner model and make prediction requests](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/model-garden/use-models#deploy_a_partner_model_and_make_prediction_requests) .

## Considerations

  - You can include a maximum of three images per request.
  - The MaaS endpoint doesn't use Llama Guard, unlike previous versions. To use Llama Guard, deploy Llama Guard from Model Garden and then send the prompts and responses to that endpoint. However, compared to Llama 4, Llama Guard has a more limited context (128,000) and can only process requests with a single image at the beginning of the prompt.
  - Batch predictions aren't supported.
