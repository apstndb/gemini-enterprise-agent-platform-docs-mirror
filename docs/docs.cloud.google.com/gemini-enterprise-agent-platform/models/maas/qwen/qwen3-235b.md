---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/models/maas/qwen/qwen3-235b
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/maas/qwen/qwen3-235b
title: Qwen3 235B
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Qwen3 235B is a large 235B parameter model. The model is distinguished by its "hybrid thinking" capability, which allows users to dynamically switch between a methodical, step-by-step "thinking" mode for complex tasks like mathematical reasoning and coding, and a rapid "non-thinking" mode for general-purpose conversation. Its large context window makes it suitable for use cases requiring deep reasoning and long-form comprehension.

## Managed API (MaaS) specifications

[View pricing](https://cloud.google.com/gemini-enterprise-agent-platform/generative-ai/pricing)

Model ID

`qwen3-235b-a22b-instruct-2507-maas`

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
    Supported
  - [Pay-as-you-go](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/deploy/consumption-options)  
    Standard PayGo  
    Supported
  - [Fixed quota](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/quotas)  
    Not supported

Supported regions

**[Model availability](https://docs.cloud.google.com/gemini-enterprise-agent-platform/resources/locations)**

  - Global: `global`
  - United States: `us-south1`

**[ML processing](https://docs.cloud.google.com/gemini-enterprise-agent-platform/resources/data-residency)**

  - Multi-region: `us`

Quotas

  - **`global`** : 16,384 maximum output, 262,144 context length
  - **`us-south1`** : 16,384 maximum output, 262,144 context length

Versions

`qwen3-235b-a22b-instruct-2507-maas`

  - Launch stage: GA
  - Release date: August 13, 2025

## Deploy as a self-deployed model

To self-deploy the model, navigate to the [Qwen3 235B model card](https://console.cloud.google.com/agent-platform/publishers/qwen/model-garden/qwen3) in the Model Garden console and click **Deploy model** . For more information about deploying and using partner models, see [Deploy a partner model and make prediction requests](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/model-garden/use-models#deploy_a_partner_model_and_make_prediction_requests) .
