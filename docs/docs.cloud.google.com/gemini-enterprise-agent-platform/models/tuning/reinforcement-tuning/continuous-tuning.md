---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/models/tuning/reinforcement-tuning/continuous-tuning
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/tuning/reinforcement-tuning/continuous-tuning
title: Continuous tuning for reinforcement learning fine-tuning
description: Continue tuning a previously tuned Gemini model or checkpoint by using reinforcement learning fine-tuning.
data_source: docs.cloud.google.com
---

> This product is a Pre-GA offering, subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](https://cloud.google.com/terms/service-terms#1) , the "Agentic AI Services" terms in the [Service Specific Terms](https://cloud.google.com/terms/service-terms#1) , and the [Additional Terms for Generative AI Preview Products](https://cloud.google.com/trustedtester/aitos) . Pre-GA products and features may have limited support, and changes to pre-GA products and features may not be compatible with other pre-GA versions. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .
> 
> These Pre-GA products are in various stages of internal testing and review. As such, **do not use proprietary, sensitive, or other confidential data with these products** . These products are made available to Customers solely for limited testing and evaluation, and may not be used for commercial or production purposes.

Continuous tuning lets you continue tuning an already tuned model or model checkpoint by adding more epochs or training examples. Using an already tuned model or checkpoint as the base model allows for more efficient tuning experimentation.

You can use continuous tuning for the following purposes:

  - To tune with more data if an existing tuned model is underfitting.
  - To boost performance or keep the model up to date with new data.
  - To further customize an existing tuned model.

## Supported continuous tuning patterns

The following continuous tuning patterns are supported:

  - Supervised fine-tuning → Reinforcement learning fine-tuning
  - Reinforcement learning fine-tuning → Reinforcement learning fine-tuning

## Configure continuous tuning

To configure a continuous tuning job, include a `preTunedModel` block in the request body that points to the previously tuned model (and, optionally, a specific checkpoint). The rest of the request follows the same schema as a new reinforcement learning fine-tuning job.

    {
      "description": string,
      "tunedModelDisplayName": string,
      "reinforcementTuningSpec": {
        "trainingDatasetUri": "TRAINING_DATASET",
        "validationDatasetUri": "VALIDATION_DATASET",
        "hyperParameters": "HYPER_PARAMETERS",
        "singleRewardConfig": "REWARD_CONFIG"
      },
      "preTunedModel": {
        "tunedModelName": "projects/PROJECT_ID/locations/LOCATION_ID/models/PRETUNED_MODEL_ID",
        "checkpointId": "CHECKPOINT_ID"
      }
    }

The placeholders in the body are:

  - TRAINING\_DATASET : Cloud Storage URI of the training dataset JSONL file.
  - VALIDATION\_DATASET : Cloud Storage URI of the validation dataset JSONL file. Optional.
  - HYPER\_PARAMETERS : Hyperparameter configuration for the continuous tuning job. For details, see the [Hyperparameters](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/tuning/reinforcement-tuning/reinforcement-tuning-job/hyperparameters) page.
  - REWARD\_CONFIG : Reward configuration. For details, see the [Reward functions](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/tuning/reinforcement-tuning/reinforcement-tuning-job/reward-functions) page.
  - PROJECT\_ID : Your Google Cloud project ID.
  - LOCATION\_ID : The location ID.
  - PRETUNED\_MODEL\_ID : The model ID of the previously tuned model to continue from.
  - CHECKPOINT\_ID : The ID of a specific checkpoint of the previously tuned model. Optional — if omitted, the latest checkpoint of the pretuned model is used.

## What's next

  - [Prepare a tuning dataset](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/tuning/reinforcement-tuning/reinforcement-tuning-job/tuning-dataset) for the continuous tuning job.
  - [Configure hyperparameters](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/tuning/reinforcement-tuning/reinforcement-tuning-job/hyperparameters) and [reward functions](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/tuning/reinforcement-tuning/reinforcement-tuning-job/reward-functions) for the continuous tuning job.
  - [Monitor job status and metrics](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/tuning/reinforcement-tuning/reinforcement-tuning-job/job-status-metrics-monitoring) while continuous tuning runs.
