---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/models/maas/qwen/qwen3-next-instruct
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/maas/qwen/qwen3-next-instruct
title: Qwen3-Next-80B Instruct
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

> **Caution:** As of July 21, 2026, the `qwen3-next-80b-a3b-instruct-maas` endpoint is deprecated and will be retired on October 21, 2026. For more information, see [Open model deprecations](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/deprecations/open-models) .

Qwen3-Next-80B Instruct is a language model from the Qwen3-Next family of models. It is designed for following specific commands and handling long pieces of text. It uses a smart design called Mixture-of-Experts (MoE), which activates a subset of available parameters to process information, which makes it faster and more cost-effective to run than other models of its size.

The Instruct version is tuned for reliable, direct answers in chat and agent applications and its large context window allows it to maintain an entire conversation or large document in memory.

## Managed API (MaaS) specifications

[View pricing](https://cloud.google.com/gemini-enterprise-agent-platform/generative-ai/pricing)

Model ID

`qwen3-next-80b-a3b-instruct-maas`

Modalities

description

Text  
Input and output

photo

Image  
Not supported

mic

Audio  
Not supported

videocam

Video  
Not supported

Capabilities

  - [Function calling](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/tools/function-calling)  
    Supported
  - [Structured output](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/capabilities/control-generated-output)  
    Supported
  - [Thinking](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/thinking)  
    Not supported

Consumption options

  - [Provisioned Throughput](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/provisioned-throughput)  
    Supported
  - [Batch inference](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/capabilities/batch-inference)  
    Not supported
  - [Pay-as-you-go](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/deploy/consumption-options)  
    Standard PayGo  
    Supported
  - [Fixed quota](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/quotas)  
    Not supported

Supported regions

**[Model availability](https://docs.cloud.google.com/gemini-enterprise-agent-platform/resources/locations)**

  - Global: `global`

**[ML processing](https://docs.cloud.google.com/gemini-enterprise-agent-platform/resources/data-residency)**

  - Multi-region: `us`

Quotas

  - **`global`** : 262,144 maximum output, 262,144 context length

Versions

`Qwen3-Next Instruct`

  - Launch stage: GA
  - Release date: September 15, 2025

## Deploy as a self-deployed model

To self-deploy the model, navigate to the [Qwen3-Next-80B Instruct model card](https://console.cloud.google.com/agent-platform/publishers/qwen/model-garden/qwen3-next) in the Model Garden console and click **Deploy model** . For more information about deploying and using partner models, see [Deploy a partner model and make prediction requests](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/model-garden/use-models#deploy_a_partner_model_and_make_prediction_requests) .
