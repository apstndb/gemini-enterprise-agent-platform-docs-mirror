---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/models/maas/deepseek/deepseek-v31
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/maas/deepseek/deepseek-v31
title: DeepSeek-V3.1
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

> **Caution:** As of July 21, 2026, the `deepseek-v3.1-maas` endpoint is deprecated and will be retired on October 21, 2026. For more information, see [Open model deprecations](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/deprecations/open-models) .

DeepSeek-V3.1 is a hybrid model that supports both thinking mode and non-thinking mode. Compared to the previous version, this upgrade brings improvements in hybrid thinking modes, tool calling, and thinking efficiency.

## Managed API (MaaS) specifications

[View pricing](https://cloud.google.com/gemini-enterprise-agent-platform/generative-ai/pricing)

Model ID

`deepseek-v3.1-maas`

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
    Not supported

Supported regions

**[Model availability](https://docs.cloud.google.com/gemini-enterprise-agent-platform/resources/locations)**

  - United States: `us-central1`

**[ML processing](https://docs.cloud.google.com/gemini-enterprise-agent-platform/resources/data-residency)**

  - Multi-region: `us`

Quotas

  - **`us-central1`** : 32,768 maximum output, 163,840 context length

Versions

`deepseek-v3.1-maas`

  - Launch stage: GA
  - Release date: August 28, 2025

## Deploy as a self-deployed model

To self-deploy the model, navigate to the [DeepSeek-V3.1 model card](https://console.cloud.google.com/agent-platform/publishers/deepseek-ai/model-garden/deepseek-v3-1) in the Model Garden console and click **Deploy model** . For more information about deploying and using partner models, see [Deploy a partner model and make prediction requests](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/model-garden/use-models#deploy_a_partner_model_and_make_prediction_requests) .
