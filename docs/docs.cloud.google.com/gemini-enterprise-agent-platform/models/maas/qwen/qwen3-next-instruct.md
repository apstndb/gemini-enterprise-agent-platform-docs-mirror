---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/models/maas/qwen/qwen3-next-instruct
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/maas/qwen/qwen3-next-instruct
title: Qwen3-Next-80B Instruct
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Qwen3-Next-80B Instruct is a language model from the Qwen3-Next family of models. It is designed for following specific commands and handling long pieces of text. It uses a smart design called Mixture-of-Experts (MoE), which activates a subset of available parameters to process information, which makes it faster and more cost-effective to run than other models of its size.

The Instruct version is tuned for reliable, direct answers in chat and agent applications and its large context window allows it to maintain an entire conversation or large document in memory.

## Managed API (MaaS) specifications

[View model card in Model Garden](https://console.cloud.google.com/agent-platform/publishers/qwen/model-garden/qwen3-next-80b-a3b-instruct-maas)

Model ID

`qwen3-next-80b-a3b-instruct-maas`

Launch stage

GA

Supported inputs & outputs

  - Inputs:
    Text , Code
  - Outputs:
    Text , Code

Capabilities

Supported

  - [Function calling](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/maas/capabilities/function-calling)
  - [Structured output](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/maas/capabilities/structured-output)

Not supported

  - [Batch predictions](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/maas/capabilities/batch-prediction)

Consumption options

Supported

  - [Dynamic shared quota](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/standard-paygo)
  - [Provisioned Throughput](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/provisioned-throughput)

Not supported

  - [Fixed quota](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/quotas)

Versions

`Qwen3-Next Instruct`

  - **Launch stage:** GA
  - **Release date:** September 15, 2025

Supported regions

Model availability

Global

  - `global`

ML processing

United States

  - `Multi-region`

Limits

global:

  - Max output: 262,144
  - Context length: 262,144

Pricing

See [Pricing](https://cloud.google.com/gemini-enterprise-agent-platform/generative-ai/pricing) .

## Deploy as a self-deployed model

To self-deploy the model, navigate to the [Qwen3-Next-80B Instruct model card](https://console.cloud.google.com/agent-platform/publishers/qwen/model-garden/qwen3-next) in the Model Garden console and click **Deploy model** . For more information about deploying and using partner models, see [Deploy a partner model and make prediction requests](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/model-garden/use-models#deploy_a_partner_model_and_make_prediction_requests) .
