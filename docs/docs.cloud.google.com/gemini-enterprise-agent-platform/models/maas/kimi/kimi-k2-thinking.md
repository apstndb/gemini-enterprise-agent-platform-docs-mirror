---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/models/maas/kimi/kimi-k2-thinking
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/maas/kimi/kimi-k2-thinking
title: Kimi K2 Thinking
description: Explore Kimi K2 Thinking, a thinking model that excels at complex problem-solving and deep reasoning.
data_source: docs.cloud.google.com
---

Kimi K2 Thinking is an open-source model that operates as a "thinking agent," reasoning step-by-step while using tools to achieve state-of-the-art performance on various benchmarks. It is capable of executing up to 200-300 sequential tool calls without human intervention, allowing it to solve complex problems across a wide range of tasks. The model uses Quantization-Aware Training (QAT) to support INT4 inference, which provides a roughly 2x improvement in generation speed.

## Managed API (MaaS) specifications

[View model card in Model Garden](https://console.cloud.google.com/agent-platform/publishers/moonshotai/model-garden/kimi-k2-thinking-maas)

Model ID

`kimi-k2-thinking-maas`

Launch stage

GA

Supported inputs & outputs

  - Inputs:
    Text , Documents
  - Outputs:
    Text

Capabilities

Supported

  - [Function calling](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/maas/capabilities/function-calling)
  - [Structured output](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/maas/capabilities/structured-output)
  - [Thinking](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/maas/capabilities/thinking)

Not supported

  - [Batch predictions](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/maas/capabilities/batch-prediction)

Consumption options

Supported

  - [Dynamic shared quota](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/dynamic-shared-quota)
  - [Provisioned Throughput](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/provisioned-throughput)

Not supported

  - [Fixed quota](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/quotas)

Versions

`Kimi K2 Thinking`

  - **Launch stage:** GA
  - **Release date:** Nov 13, 2025

Supported regions

Model availability

Global

  - `global`

ML processing

Region

  - `Multi-region`

Limits

global:

  - Max output: 262,144
  - Context length: 262,144

## Deploy as a self-deployed model

To self-deploy the model, navigate to the [Kimi K2 Thinking model card](https://console.cloud.google.com/agent-platform/publishers/moonshotai/model-garden/kimi-k2) in the Model Garden console and click **Deploy model** . For more information about deploying and using partner models, see [Deploy a partner model and make prediction requests](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/model-garden/use-models#deploy_a_partner_model_and_make_prediction_requests) .
