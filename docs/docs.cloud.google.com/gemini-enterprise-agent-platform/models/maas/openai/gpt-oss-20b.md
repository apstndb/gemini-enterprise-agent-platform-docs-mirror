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

[View model card in Model Garden](https://console.cloud.google.com/agent-platform/publishers/openai/model-garden/gpt-oss-20b-maas)

Model ID

`gpt-oss-20b-maas`

Launch stage

GA

Supported inputs & outputs

  - Inputs:
    Text
  - Outputs:
    Text

Capabilities

Supported

  - [Batch predictions](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/maas/capabilities/batch-prediction)
  - [Function calling](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/maas/capabilities/function-calling)
  - [Structured output](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/maas/capabilities/structured-output)

Not supported

Consumption options

Supported

  - [Standard pay-as-you-go](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/standard-paygo)
  - [Fixed quota](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/quotas)
  - [Provisioned Throughput](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/provisioned-throughput)

Not supported

Versions

`gpt-oss-20b-maas`

  - **Launch stage:** GA
  - **Release date:** August 13, 2025

Supported regions

Model availability

United States

  - `us-central1`

ML processing

United States

  - `Multi-region`

Limits

us-central1:

  - Max output: 32,768
  - Context length: 131,072

Pricing

See [Pricing](https://cloud.google.com/gemini-enterprise-agent-platform/generative-ai/pricing) .

## Deploy as a self-deployed model

To self-deploy the model, navigate to the [gpt-oss 20B model card](https://console.cloud.google.com/agent-platform/publishers/openai/model-garden/gpt-oss) in the Model Garden console and click **Deploy model** . For more information about deploying and using partner models, see [Deploy a partner model and make prediction requests](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/model-garden/use-models#deploy_a_partner_model_and_make_prediction_requests) .
