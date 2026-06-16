---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/models/tuning/reinforcement-tuning
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/tuning/reinforcement-tuning
title: About reinforcement learning fine-tuning for Gemini models
description: Adapt Gemini models with reinforcement learning fine-tuning by using user-defined reward functions to optimize for reasoning, instruction following, and other custom objectives.
data_source: docs.cloud.google.com
---

> This product is a Pre-GA offering, subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](https://cloud.google.com/terms/service-terms#1) , the "Agentic AI Services" terms in the [Service Specific Terms](https://cloud.google.com/terms/service-terms#1) , and the [Additional Terms for Generative AI Preview Products](https://cloud.google.com/trustedtester/aitos) . Pre-GA products and features may have limited support, and changes to pre-GA products and features may not be compatible with other pre-GA versions. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .
> 
> These Pre-GA products are in various stages of internal testing and review. As such, **do not use proprietary, sensitive, or other confidential data with these products** . These products are made available to Customers solely for limited testing and evaluation, and may not be used for commercial or production purposes.

Reinforcement learning is a powerful technique to adapt large language models (LLMs) to maximize feedback rewards provided by a user-defined reward function. The model explores many possible answers, observes a numeric reward for each, and gradually shifts its behavior so that high-reward answers become more likely and low-reward answers become less likely. This approach excels in scenarios that require multi-step reasoning, intricate decision-making, or understanding subtle nuances in prompts.

Reinforcement learning fine-tuning for Gemini lets you fine-tune Gemini by using your own prompts and self-defined reward functions. You can use it to boost the reasoning capability and output quality of Gemini models for your own use cases and agentic workflows.

## How it works

Reinforcement learning fine-tuning operates iteratively to refine the behavior of the LLM. During each iteration, the model generates responses to a set of prompts. These responses are then evaluated by a user-defined reward function, which quantifies the quality of the generated output based on your desired criteria. The service uses this reward signal to update the model's parameters through reinforcement learning algorithms, to encourage behaviors that lead to higher rewards. This iterative process of generation, evaluation, and update allows the model to learn and adapt to your specific use cases.

The following diagram shows the overall reinforcement learning fine-tuning workflow:

![The reinforcement learning fine-tuning feedback loop for Gemini models.](https://docs.cloud.google.com/static/gemini-enterprise-agent-platform/images/reinforcement-tuning-overview.png)

## Key features

  - **Customizable reward functions:** Define your own reward functions to precisely optimize for a wide range of custom use cases and align the model's behavior with specific objectives. For details on the supported reward types, see the [Reward functions](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/tuning/reinforcement-tuning/reinforcement-tuning-job/reward-functions) page.

  - **Adapters for efficient tuning:** Reinforcement learning fine-tuning uses [LoRA](https://en.wikipedia.org/wiki/Fine-tuning_\(deep_learning\)#Low-rank_adaptation) adapters, which enable effective adaptation while reusing the existing serving infrastructure.

  - **Multiple thinking levels:** The service supports tuning at two thinking levels, `MINIMAL` and `HIGH` (dynamic thinking), so you can choose the approach that best suits your model's learning objectives and desired response generation patterns. For details, see the [Hyperparameters](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/tuning/reinforcement-tuning/reinforcement-tuning-job/hyperparameters) page.

  - **Continuous tuning:** Further refine a previously tuned model by incorporating additional training examples or epochs. Using an existing tuned model or checkpoint as the foundation enables a more efficient process for tuning experimentation. For details, see the [Continuous tuning](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/tuning/reinforcement-tuning/continuous-tuning) page.

  - **Multimodal datasets:** Supports text, image, video, and audio data modalities.

## When to use reinforcement learning fine-tuning

Reinforcement learning fine-tuning is preferred for fine-tuning LLMs in situations where optimal strategies are not obvious through supervised learning. This includes tasks where the goal is to optimize specific metrics without readily available ground truth labels, where alignment with human preferences is crucial (and a judgement method exists), and for reasoning-heavy tasks that benefit from iterative improvement and exploration.

The following are some scenarios where reinforcement learning fine-tuning is preferred:

  - **Complex instruction following:** When the model needs to follow intricate instructions where the "correct" output isn't a single answer but requires a set of checks. Reinforcement learning can help the model learn to navigate these complex instruction sets.

  - **Creative content generation:** For tasks like generating creative writing, poetry, or highly specialized code, where objective metrics are difficult to define. Reinforcement learning, with a well-designed reward function (potentially involving human feedback or expert evaluation), can guide the model toward more desirable and innovative outputs.

  - **Reasoning tasks:** For tasks that require heavy reasoning, such as solving word puzzles or mathematical problems, reinforcement learning can incentivize the model to explore different "thought" sequences to learn which patterns of reasoning are most effective at solving problems.

## Supported models and regions

The following Gemini models support reinforcement learning fine-tuning:

### Gemini 3.5 Flash

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Specification</th>
<th>Value</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Supported endpoints for model tuning</td>
<td><ul>
<li><code dir="ltr" translate="no">us-central1</code> — <code dir="ltr" translate="no">us-central1-aiplatform.googleapis.com</code></li>
</ul></td>
</tr>
<tr class="even">
<td>Supported endpoints for tuned model serving</td>
<td><ul>
<li><code dir="ltr" translate="no">us</code> multi-region endpoint ( <code dir="ltr" translate="no">aiplatform.us.rep.googleapis.com</code> ) when tuning in <code dir="ltr" translate="no">us-central1</code></li>
</ul></td>
</tr>
<tr class="odd">
<td>API version</td>
<td><code dir="ltr" translate="no">v1beta1</code> only</td>
</tr>
</tbody>
</table>

## Supported tuning modalities

Reinforcement learning fine-tuning supports the following data modalities in your tuning datasets:

  - Text
  - Audio
  - Image
  - Video

For per-modality dataset limits (such as maximum number of files per prompt, maximum file size, and maximum total length), see the [Tuning dataset](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/tuning/reinforcement-tuning/reinforcement-tuning-job/tuning-dataset) page.

## Continuous tuning

You can use the output of a previous tuning job as the base for a new reinforcement learning fine-tuning job. The following continuous tuning patterns are supported:

  - Supervised fine-tuning → Reinforcement learning fine-tuning
  - Reinforcement learning fine-tuning → Reinforcement learning fine-tuning

For configuration details, see the [Continuous tuning](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/tuning/reinforcement-tuning/continuous-tuning) page.

## Serve the tuned model

After a successful reinforcement learning fine-tuning job on the base Gemini model, a tuned model based on the last checkpoint is deployed to an endpoint in your project. Tuned models use the same serving endpoint strategy as the base model. For example, if you run a tuning job in `us-central1` , the tuned model is deployed to a `us` multi-region endpoint (mREP).

To retrieve the deployed tuned-model endpoint and run inference against it, see the [Quick start](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/tuning/reinforcement-tuning/quick-start) page.

## Pricing

### Tuning pricing

Reinforcement learning fine-tuning for Gemini generates tokens in two phases: a sampling phase and a training phase. Tokens generated during the training phase are charged according to the "Model Tuning" section of the [Gemini Enterprise Agent Platform pricing](https://cloud.google.com/gemini-enterprise-agent-platform/generative-ai/pricing) page.

### Inference pricing

After tuning, inference (prediction request) costs for the tuned model still apply. For model inference starting from Gemini 3, the tuned-model endpoint prediction price is 1.5 times the price of the base model. For more information, see [Available Gemini stable model versions](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/model-versions#stable-versions-available) .

If you configure the Gen AI evaluation service to run automatically during tuning, evaluations are charged as batch prediction jobs. For more information, see the "Model Tuning" section of the [Gemini Enterprise Agent Platform pricing](https://cloud.google.com/gemini-enterprise-agent-platform/generative-ai/pricing) page.

## What's next

  - Follow the [Quick start](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/tuning/reinforcement-tuning/quick-start) to create your first reinforcement learning fine-tuning job.
  - Learn how to prepare a [tuning dataset](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/tuning/reinforcement-tuning/reinforcement-tuning-job/tuning-dataset) and configure [reward functions](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/tuning/reinforcement-tuning/reinforcement-tuning-job/reward-functions) .
  - Learn about [deploying a tuned Gemini model](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/deploy/overview#deploy-a-tuned-model) .
