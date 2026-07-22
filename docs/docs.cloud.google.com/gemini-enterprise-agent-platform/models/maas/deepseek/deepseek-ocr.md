---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/models/maas/deepseek/deepseek-ocr
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/maas/deepseek/deepseek-ocr
title: DeepSeek-OCR
description: Understand DeepSeek-OCR, a comprehensive OCR model for complex document analysis and challenging text recognition.
data_source: docs.cloud.google.com
---

> **Caution:** As of July 21, 2026, the `deepseek-ocr-maas` endpoint is deprecated and will be retired on October 21, 2026. For more information, see [Open model deprecations](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/deprecations/open-models) .

DeepSeek-OCR is a comprehensive Optical Character Recognition (OCR) model that analyzes and understands complex documents. It excels at challenging OCR tasks, including recognizing mathematical formulas and processing text that is curved, rotated, or overlapping.

## Managed API (MaaS) specifications

[View pricing](https://cloud.google.com/gemini-enterprise-agent-platform/generative-ai/pricing)

Model ID

`deepseek-ocr-maas`

Modalities

description

Text  
Input and output

photo

Image  
Input only

mic

Audio  
Not supported

videocam

Video  
Not supported

Capabilities

  - [Function calling](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/tools/function-calling)  
    Not supported
  - [Structured output](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/capabilities/control-generated-output)  
    Not supported
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

  - United States: `us-central1`

**[ML processing](https://docs.cloud.google.com/gemini-enterprise-agent-platform/resources/data-residency)**

  - Multi-region: `us`

Quotas

  - **`us-central1`** : 8,192 maximum output, 8,192 context length

Versions

`DeepSeek-OCR`

  - Launch stage: GA
  - Release date: October 23, 2025

## Deploy as a self-deployed model

To self-deploy the model, navigate to the [DeepSeek-OCR model card](https://console.cloud.google.com/agent-platform/publishers/deepseek-ai/model-garden/deepseek-ocr) in the Model Garden console and click **Deploy model** . For more information about deploying and using partner models, see [Deploy a partner model and make prediction requests](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/model-garden/use-models#deploy_a_partner_model_and_make_prediction_requests) .
