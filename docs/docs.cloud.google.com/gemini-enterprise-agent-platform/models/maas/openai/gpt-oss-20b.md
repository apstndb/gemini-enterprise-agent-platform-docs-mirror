---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/models/maas/openai/gpt-oss-20b
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/maas/openai/gpt-oss-20b
title: OpenAI gpt-oss 20B
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

OpenAI gpt-oss 20B is a 20B open-weight language model released under the Apache 2.0 license. It is well-suited for reasoning and function calling use cases. The model is optimized for deployment on consumer hardware.

The 20B model delivers similar results to OpenAI o3-mini on common benchmarks and can run on edge devices with 16GB of memory, making it ideal for on-device use cases, local inference, or rapid iteration without costly infrastructure.

## Managed API (MaaS) specifications

Model ID

`gpt-oss-20b-maas`

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
    Not supported
  - [Batch inference](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/capabilities/batch-inference)  
    Supported
  - [Pay-as-you-go](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/deploy/consumption-options)  
    Standard PayGo  
    Supported
  - [Fixed quota](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/quotas)  
    Supported

Supported regions

**[Model availability](https://docs.cloud.google.com/gemini-enterprise-agent-platform/resources/locations)**

  - United States: `us-central1`

**[ML processing](https://docs.cloud.google.com/gemini-enterprise-agent-platform/resources/data-residency)**

  - Multi-region: `us`

Quotas

  - **`us-central1`** : 32,768 maximum output, 131,072 context length

Versions

`gpt-oss-20b-maas`

  - Launch stage: GA
  - Release date: August 13, 2025

Pricing

See [Pricing](https://cloud.google.com/gemini-enterprise-agent-platform/generative-ai/pricing) .

## Deploy as a self-deployed model

To self-deploy the model, navigate to the [gpt-oss 20B model card](https://console.cloud.google.com/agent-platform/publishers/openai/model-garden/gpt-oss) in the Model Garden console and click **Deploy model** . For more information about deploying and using partner models, see [Deploy a partner model and make prediction requests](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/model-garden/use-models#deploy_a_partner_model_and_make_prediction_requests) .
