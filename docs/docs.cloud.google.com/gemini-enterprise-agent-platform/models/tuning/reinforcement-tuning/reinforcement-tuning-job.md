---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/models/tuning/reinforcement-tuning/reinforcement-tuning-job
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/tuning/reinforcement-tuning/reinforcement-tuning-job
title: Reinforcement learning fine-tuning job
description: Overview of the reinforcement learning fine-tuning job for Gemini models, including dataset, hyperparameters, reward functions, and monitoring.
data_source: docs.cloud.google.com
---

> This product is a Pre-GA offering, subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](https://cloud.google.com/terms/service-terms#1) , the "Agentic AI Services" terms in the [Service Specific Terms](https://cloud.google.com/terms/service-terms#1) , and the [Additional Terms for Generative AI Preview Products](https://cloud.google.com/trustedtester/aitos) . Pre-GA products and features may have limited support, and changes to pre-GA products and features may not be compatible with other pre-GA versions. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .
> 
> These Pre-GA products are in various stages of internal testing and review. As such, **do not use proprietary, sensitive, or other confidential data with these products** . These products are made available to Customers solely for limited testing and evaluation, and may not be used for commercial or production purposes.

A reinforcement learning fine-tuning job for Gemini models is configured with three main building blocks: a [tuning dataset](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/tuning/reinforcement-tuning/reinforcement-tuning-job/tuning-dataset) , [hyperparameters](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/tuning/reinforcement-tuning/reinforcement-tuning-job/hyperparameters) that control the training process, and one or more [reward functions](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/tuning/reinforcement-tuning/reinforcement-tuning-job/reward-functions) that score each model response. The service also exposes [metrics and job status for monitoring](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/tuning/reinforcement-tuning/reinforcement-tuning-job/job-status-metrics-monitoring) .

For an end-to-end example of creating a tuning job, retrieving the tuned model, and running inference, see the [Quick start](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/tuning/reinforcement-tuning/quick-start) .

## Prepare the tuning dataset

A reinforcement learning fine-tuning job is driven by a training dataset and an optional validation dataset. Each dataset is a JSONL file stored in Cloud Storage. Every line is a single tuning example that contains a `systemInstruction` , `contents` (the prompt the model responds to during tuning), and a `references` map that carries any metadata your reward function needs to score the model's response (for example, a ground-truth answer, a rubric, or unit-test input).

Reinforcement learning fine-tuning supports multimodal prompts (text, image, audio, and video), subject to per-file and per-prompt limits.

For the full dataset schema, the modality-specific dataset limits, and an example of how to populate `references` for reward computation, see the [Tuning dataset](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/tuning/reinforcement-tuning/reinforcement-tuning-job/tuning-dataset) page.

## Configure hyperparameters

Hyperparameters control how the model is updated during reinforcement learning fine-tuning, including the thinking level used during generation, batch size, samples per prompt, learning rate multiplier, epoch count, evaluation and checkpoint intervals, maximum output length, and the LoRA adapter size. The defaults work well for most workloads, but you can override any of them in the request body when you create a tuning job.

For default values, allowed ranges, dataset-size-dependent rules, and recommended combinations, see the [Hyperparameters](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/tuning/reinforcement-tuning/reinforcement-tuning-job/hyperparameters) page.

## Define reward functions

A reward function numerically scores each model response during tuning. The reward signal is what reinforcement learning optimizes against, so its quality directly determines tuning quality. All rewards are clipped to the range `[-1, 1]` .

Reinforcement learning fine-tuning supports the following reward types:

  - **String matching reward** — Compares the model response (or a parsed substring of it) against a ground-truth value supplied in `references` .
  - **Gemini-based autorater reward** — Uses an LLM-as-a-judge to score each response, optionally with response parsing.
  - **Cloud Run reward** — Calls a user-managed Cloud Run service that returns a scalar reward, for fully customizable scoring logic.
  - **Composite reward** — Combines any of the above reward types with per-scorer weights.

Before you launch a tuning job, we strongly recommend validating your reward configuration with the `ValidateReinforcementTuningReward` API.

For detailed configuration schemas, code samples, IAM setup, and reward-design best practices, see the [Reward functions](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/tuning/reinforcement-tuning/reinforcement-tuning-job/reward-functions) page.

## Monitor job status and metrics

Once a tuning job is launched, you can track its lifecycle state (such as `JOB_STATE_PENDING` , `JOB_STATE_RUNNING` , `JOB_STATE_SUCCEEDED` , `JOB_STATE_FAILED` , `JOB_STATE_CANCELLING` , `JOB_STATE_CANCELLED` ) and inspect tuning progress in two ways:

  - **Programmatically** — Issue a `GetTuningJob` request to retrieve the job's state, `tunedModel` , error details, and metadata. See the [Quick start](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/tuning/reinforcement-tuning/quick-start#get-the-tuned-model-endpoint) for an example `curl` command.
  - **Visually** — Open the job's monitoring page in the Google Cloud console under [**Agent Platform \> Model \> Tuning**](https://console.cloud.google.com/agent-platform/tuning) , which shows the underlying tuning experiment with charts for the training and evaluation metrics emitted at each step (reward, generation length, reward latency, per-reward breakdowns for composite rewards, and so on).

Reinforcement learning fine-tuning also produces intermediate checkpoints at the frequency set by `checkpointInterval` , which you can deploy and evaluate independently before the job completes.

For the complete list of emitted metrics, per-reward-type metrics, how to interpret them, and how to access checkpoints, see the [Metrics and monitoring](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/tuning/reinforcement-tuning/reinforcement-tuning-job/job-status-metrics-monitoring) page.

## What's next

  - [Prepare a tuning dataset](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/tuning/reinforcement-tuning/reinforcement-tuning-job/tuning-dataset) .
  - [Configure hyperparameters](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/tuning/reinforcement-tuning/reinforcement-tuning-job/hyperparameters) .
  - [Define reward functions](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/tuning/reinforcement-tuning/reinforcement-tuning-job/reward-functions) .
  - [Monitor job status and metrics](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/tuning/reinforcement-tuning/reinforcement-tuning-job/job-status-metrics-monitoring) .
