---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/models/tuning/reinforcement-tuning/reinforcement-tuning-job/job-status-metrics-monitoring
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/tuning/reinforcement-tuning/reinforcement-tuning-job/job-status-metrics-monitoring
title: Metrics and monitoring for reinforcement learning fine-tuning
description: Track job status and inspect tuning metrics emitted during reinforcement learning fine-tuning of Gemini models.
data_source: docs.cloud.google.com
---

> This product is a Pre-GA offering, subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](https://cloud.google.com/terms/service-terms#1) , the "Agentic AI Services" terms in the [Service Specific Terms](https://cloud.google.com/terms/service-terms#1) , and the [Additional Terms for Generative AI Preview Products](https://cloud.google.com/trustedtester/aitos) . Pre-GA products and features may have limited support, and changes to pre-GA products and features may not be compatible with other pre-GA versions. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .
> 
> These Pre-GA products are in various stages of internal testing and review. As such, **do not use proprietary, sensitive, or other confidential data with these products** . These products are made available to Customers solely for limited testing and evaluation, and may not be used for commercial or production purposes.

This page lists the metrics emitted by a reinforcement learning fine-tuning job and describes how to view job status and results.

## Metrics

The following metrics are emitted at every training step (on the current training batch) and at every evaluation interval (on the entire validation dataset).

### Reward metrics

  - **`/train_mean_reward`** — The mean reward on the batch of samples in the current training step.
  - **`/eval_mean_reward`** — The mean reward on the entire validation dataset.

### Generation length metrics

  - **`/train_generation_length`** — The mean generation length, in number of tokens (including thinking tokens and non-thinking tokens), on the batch of samples in the current training step.
  - **`/eval_generation_length`** — The mean generation length, in number of tokens (including thinking tokens and non-thinking tokens), on the entire validation dataset.
  - **`/train_thinking_token_length`** — The mean thinking token length on the batch of samples in the current training step.
  - **`/eval_thinking_token_length`** — The mean thinking token length on the entire validation dataset.

### Reward latency metrics

  - **`/train_mean_reward_latency`** — The mean latency for computing rewards on the batch of samples in the current training step.
  - **`/eval_mean_reward_latency`** — The mean latency for computing rewards on the entire validation dataset.
  - **`/train_p95_reward_latency`** — The P95 latency for computing rewards on the batch of samples in the current training step.
  - **`/eval_p95_reward_latency`** — The P95 latency for computing rewards on the entire validation dataset.

### Sampling latency metrics

  - **`/train_mean_sampling_latency`** — The mean latency for sampling on the batch of samples in the current training step.
  - **`/eval_mean_sampling_latency`** — The mean latency for sampling on the entire validation dataset.
  - **`/train_p95_sampling_latency`** — The P95 latency for sampling on the batch of samples in the current training step.
  - **`/eval_p95_sampling_latency`** — The P95 latency for sampling on the entire validation dataset.

### Batch composition metrics

  - **`/learnable_prompt_ratio`** — The actual batch size divided by all samples (including samples filtered out) for the current training step. Training metric only.

### Per-reward metrics (for composite rewards)

For composite rewards, each individual reward emits its own group of metrics prefixed with `${reward_name}` . Metrics with the same reward name are grouped together in the monitoring UI, where you can fold and unfold them.

  - **`${reward_name}/train_mean_reward`** — The mean reward for `${reward_name}` on the batch of samples in the current training step.
  - **`${reward_name}/eval_mean_reward`** — The mean reward for `${reward_name}` on the entire validation dataset.
  - **`${reward_name}/train_processing_time`** — The mean latency for computing the rewards for `${reward_name}` on the batch of samples in the current training step.
  - **`${reward_name}/eval_processing_time`** — The mean latency for computing the rewards for `${reward_name}` on the entire validation dataset.
  - **`${reward_name}/train_p95_processing_time`** — The P95 latency for computing rewards for `${reward_name}` on the batch of samples in the current training step.
  - **`${reward_name}/eval_p95_processing_time`** — The P95 latency for computing rewards for `${reward_name}` on the entire validation dataset.
  - **`${reward_name}/train_executing_code_failure_ratio`** — The mean failure ratio for computing Code Execution rewards named `${reward_name}` on the batch of samples in the current training step. Code execution rewards only.
  - **`${reward_name}/eval_executing_code_failure_ratio`** — The mean failure ratio for computing Code Execution rewards named `${reward_name}` on the entire validation dataset. Code execution rewards only.
  - **`${reward_name}/train_rpc_error_ratio`** — The mean RPC failure ratio for computing rewards named `${reward_name}` on the batch of samples in the current training step. Applies to Code execution, Autorater, and Cloud Run rewards; does not apply to string matching.
  - **`${reward_name}/eval_rpc_error_ratio`** — The mean RPC failure ratio for computing rewards named `${reward_name}` on the entire validation dataset. Applies to Code execution, Autorater, and Cloud Run rewards; does not apply to string matching.
  - **`${reward_name}/train_invalid_rpc_response_ratio`** — The mean ratio of invalid RPC responses for rewards named `${reward_name}` on the batch of samples in the current training step. Applies to Code execution, Autorater, and Cloud Run rewards; does not apply to string matching.
  - **`${reward_name}/eval_invalid_rpc_response_ratio`** — The mean ratio of invalid RPC responses for rewards named `${reward_name}` on the entire validation dataset. Applies to Code execution, Autorater, and Cloud Run rewards; does not apply to string matching.
  - **`${reward_name}/train_clipping_rewards_ratio`** — The mean clipping ratio for `${reward_name}` on the batch of samples in the current training step. Rewards are clipped to the range `[-1, 1]` .
  - **`${reward_name}/eval_clipping_rewards_ratio`** — The mean clipping ratio for `${reward_name}` on the entire validation dataset. Rewards are clipped to the range `[-1, 1]` .

## View job status and results

You can view a reinforcement learning fine-tuning job's status and results in two ways:

### Programmatically with `curl`

Issue a `GetTuningJob` request to retrieve the job's state, `tunedModel` , error details, and metadata.

    curl -X GET \
      -H "Authorization: Bearer $(gcloud auth print-access-token)" \
      "https://LOCATION_ID-aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/LOCATION_ID/tuningJobs/TUNING_JOB_ID"

Replace the following:

  - PROJECT\_ID : Your Google Cloud project ID.
  - TUNING\_JOB\_ID : The ID of the tuning job.
  - LOCATION\_ID : The ID of the location.

> **Note:** Only the `v1beta1` API version is supported for reinforcement learning fine-tuning. Using the `v1` API will return a response with insufficient fields populated.

### In the Console

Open the job's monitoring page in the Google Cloud console under [**Agent Platform \> Model \> Tuning**](https://console.cloud.google.com/agent-platform/tuning) . The monitoring view surfaces the underlying tuning experiment with charts for the training and evaluation metrics listed in this page, including reward, generation length, reward latency, and per-reward breakdowns for composite rewards.

## Intermediate checkpoints

Reinforcement learning fine-tuning produces intermediate checkpoints at the frequency set by the `checkpointInterval` hyperparameter. You can deploy and evaluate these checkpoints independently before the job completes. For details on the `checkpointInterval` hyperparameter, see the [Hyperparameters](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/tuning/reinforcement-tuning/reinforcement-tuning-job/hyperparameters#checkpointinterval) page.

## What's next

  - Follow the [Quick start](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/tuning/reinforcement-tuning/quick-start) to create your first reinforcement learning fine-tuning job.
  - [Define reward functions](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/tuning/reinforcement-tuning/reinforcement-tuning-job/reward-functions) .
  - [Configure hyperparameters](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/tuning/reinforcement-tuning/reinforcement-tuning-job/hyperparameters) .
