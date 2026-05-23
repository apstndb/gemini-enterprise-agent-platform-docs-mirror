---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/models/maas/qwen
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/maas/qwen
title: Qwen models
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

> **Note:** Qwen models are not a Google product, and its availability in Gemini Enterprise Agent Platform is subject to the terms for "Separate Offerings" in the AI/ML Services section of the [Service Specific Terms](https://cloud.google.com/terms/service-terms) , and separate terms found in the relevant model card.

Qwen models are available for use as managed APIs and self-deployed models on Gemini Enterprise Agent Platform. You can stream your responses to reduce the end-user latency perception. A streamed response uses *server-sent events* (SSE) to incrementally stream the response.

## Managed Qwen models

The following models are available from Qwen to use in Gemini Enterprise Agent Platform. To access a Qwen model, go to its Model Garden model card.

### Qwen3-Next-80B Instruct

Qwen3-Next-80B Instruct is a language model from the Qwen3-Next family of models. It is designed for following specific commands and handling very long pieces of text. It uses a smart design called Mixture-of-Experts (MoE), which activates a subset of available parameters to process information, which makes it faster and more cost-effective to run than other models of its size.

The Instruct version is tuned for reliable, direct answers in chat and agent applications and its large context window allows it to maintain an entire conversation or large document in memory.

### Qwen3-Next-80B Thinking

Qwen3-Next-80B Thinking is a language model from the Qwen3-Next family of models. It is specialized for complex problem-solving and deep reasoning. Its "thinking" mode generates a visible, step-by-step reasoning process alongside the final answer, making it ideal for tasks requiring transparent logic, like mathematical proofs, intricate code debugging, or multi-step agent planning.

### Qwen3 Coder (Qwen3 Coder)

Qwen3 Coder ( `Qwen3 Coder` ) is a large-scale, open-weight model developed for advanced software development tasks. The model's key feature is its large context window, allowing it to process and understand large codebases comprehensively.

### Qwen3 235B (Qwen3 235B)

Qwen3 235B ( `Qwen3 235B` ) is a large 235B parameter model. The model is distinguished by its "hybrid thinking" capability, which allows users to dynamically switch between a methodical, step-by-step "thinking" mode for complex tasks like mathematical reasoning and coding, and a rapid "non-thinking" mode for general-purpose conversation. Its large context window makes it suitable for use cases requiring deep reasoning and long-form comprehension.

## Use Qwen models

For managed models, you can use curl commands to send requests to the Gemini Enterprise Agent Platform endpoint using the following model names. To learn how to make streaming and non-streaming calls to Qwen models, see [Call open model APIs](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/maas/call-open-model-apis) .

To use a self-deployed Gemini Enterprise Agent Platform model:

1.  Navigate to the [Model Garden console](https://console.cloud.google.com/agent-platform/model-garden) .
2.  Find the relevant Gemini Enterprise Agent Platform model.
3.  Click **Enable** and complete the provided form to get the necessary commercial use licenses.

For more information about deploying and using partner models, see [Deploy a partner model and make prediction requests](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/model-garden/use-models#deploy_a_partner_model_and_make_prediction_requests) .

## What's next

  - Learn how to [Call open model APIs](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/maas/call-open-model-apis) .
