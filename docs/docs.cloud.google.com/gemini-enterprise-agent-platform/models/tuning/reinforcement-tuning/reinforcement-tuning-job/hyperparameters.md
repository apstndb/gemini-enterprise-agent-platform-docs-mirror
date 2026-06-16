---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/models/tuning/reinforcement-tuning/reinforcement-tuning-job/hyperparameters
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/tuning/reinforcement-tuning/reinforcement-tuning-job/hyperparameters
title: Hyperparameters for reinforcement learning fine-tuning
description: Hyperparameters that control how Gemini models are updated during reinforcement learning fine-tuning.
data_source: docs.cloud.google.com
---

> This product is a Pre-GA offering, subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](https://cloud.google.com/terms/service-terms#1) , the "Agentic AI Services" terms in the [Service Specific Terms](https://cloud.google.com/terms/service-terms#1) , and the [Additional Terms for Generative AI Preview Products](https://cloud.google.com/trustedtester/aitos) . Pre-GA products and features may have limited support, and changes to pre-GA products and features may not be compatible with other pre-GA versions. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .
> 
> These Pre-GA products are in various stages of internal testing and review. As such, **do not use proprietary, sensitive, or other confidential data with these products** . These products are made available to Customers solely for limited testing and evaluation, and may not be used for commercial or production purposes.

Hyperparameters control how the model weights are updated during reinforcement learning fine-tuning. The defaults are tuned to work well for most workloads, but you can override any of them in the request body when you create a tuning job.

## Available hyperparameters

### `epochCount`

The number of times the dataset is iterated over. This is different from the number of training *steps* — each epoch can produce a varying number of training steps.

  - **Default:** `min(110 * promptsPerBatch / promptsInDataset, 10)` if left empty. The default is computed dynamically so that the model sees each prompt multiple times, capped at 10 epochs to prevent overfitting on smaller datasets.
  - **Maximum:** The total training run is capped at 500 *steps* for stable tuning.

### `learningRateMultiplier`

A multiplier applied to the base learning rate for the adapter layer.

  - **Default:** `1`
  - **Allowed range:** `[1/4, 4]`

### `thinkingLevel`

Controls the length and depth of the internal chain-of-thought processing used during generation.

  - **Default:** `HIGH`
  - **Allowed values:** `MINIMAL` , `HIGH` (dynamic thinking)

### `batchSize` and `samplesPerPrompt`

These two hyperparameters control how prompts are batched and how many responses the model generates per prompt during each training step.

  - **`batchSize`** — The number of prompts per batch (also called `promptsPerBatch` ). A larger batch size slows down tuning but can produce more stable updates for each step.
      - **Default:** `32`
  - **`samplesPerPrompt`** — The number of different responses the model generates for each prompt during a single training step. A larger `samplesPerPrompt` slows down tuning but can increase the diversity of responses the model explores.
      - **Default:** `16`

The product `batchSize * samplesPerPrompt` is subject to modality-specific restrictions:

| Modality                            | Restriction on `batchSize * samplesPerPrompt`           |
| ----------------------------------- | ------------------------------------------------------- |
| Text                                | Must be divisible by 16 and less than or equal to 8,192 |
| Multimodal (image, audio, or video) | Must be divisible by 16 and less than or equal to 1,024 |

### `evaluateInterval`

The frequency at which the model is evaluated during tuning. The interval is measured in **steps** , not epochs.

### `checkpointInterval`

The frequency at which the model's tuning progress is saved as a checkpoint, for recovery or later use. The interval is measured in **steps** , not epochs.

  - **Recommended:** Set `checkpointInterval = evaluateInterval * N` , where `N` is a positive integer.

### `maxOutputTokens`

The maximum output generation length for the tuned model.

  - **Default and upper limit:** `32,768`

### `adapterSize`

The LoRA adapter size. Larger adapter sizes provide greater learning capacity for complex tasks at the cost of additional training time and memory.

  - **Default:** `ADAPTER_SIZE_SIXTEEN`

## What's next

  - [Prepare a tuning dataset](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/tuning/reinforcement-tuning/reinforcement-tuning-job/tuning-dataset) .
  - [Define reward functions](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/tuning/reinforcement-tuning/reinforcement-tuning-job/reward-functions) for your tuning job.
  - [Monitor job status and metrics](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/tuning/reinforcement-tuning/reinforcement-tuning-job/job-status-metrics-monitoring) .
  - Follow the [Quick start](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/tuning/reinforcement-tuning/quick-start) to create your first reinforcement learning fine-tuning job.
