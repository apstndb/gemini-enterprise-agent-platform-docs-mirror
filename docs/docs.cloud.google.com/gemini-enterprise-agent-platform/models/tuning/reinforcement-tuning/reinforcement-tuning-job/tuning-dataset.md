---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/models/tuning/reinforcement-tuning/reinforcement-tuning-job/tuning-dataset
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/tuning/reinforcement-tuning/reinforcement-tuning-job/tuning-dataset
title: Tuning dataset for reinforcement learning fine-tuning
description: Prepare and structure tuning datasets for reinforcement learning fine-tuning of Gemini models, including modality-specific limits.
data_source: docs.cloud.google.com
---

> This product is a Pre-GA offering, subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](https://cloud.google.com/terms/service-terms#1) , the "Agentic AI Services" terms in the [Service Specific Terms](https://cloud.google.com/terms/service-terms#1) , and the [Additional Terms for Generative AI Preview Products](https://cloud.google.com/trustedtester/aitos) . Pre-GA products and features may have limited support, and changes to pre-GA products and features may not be compatible with other pre-GA versions. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .
> 
> These Pre-GA products are in various stages of internal testing and review. As such, **do not use proprietary, sensitive, or other confidential data with these products** . These products are made available to Customers solely for limited testing and evaluation, and may not be used for commercial or production purposes.

A reinforcement learning fine-tuning job is driven by a training dataset and an optional validation dataset. Each dataset is a JSON file stored in Cloud Storage, where every line is a single tuning example.

This page describes the dataset schema, how to use the `references` field for reward computation, and the per-modality dataset limits enforced by the service.

## Dataset schema

Each line of the JSONL dataset file follows this schema:

    {
      "systemInstruction": {
        "role": string,
        "parts": [
          {
            "text": string
          }
        ]
      },
      "contents": [
        {
          "role": string,
          "parts": [
            {
              // Union field data: text or fileData.
              "text": string,
              "fileData": {
                "mimeType": string,
                "fileUri": string
              }
            }
          ]
        }
      ],
      "references": {
        string: string,
        ...
      }
    }

The `contents` and `systemInstruction` fields use the same schema as the Gemini Enterprise Agent Platform [`generateContent`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.endpoints/generateContent) API. `systemInstruction` accepts text only. `contents` can include text or file data (image, audio, or video), subject to the [dataset limits](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/tuning/reinforcement-tuning/reinforcement-tuning-job/tuning-dataset#dataset-limits) .

### The `references` field

The `references` field is specific to reinforcement learning fine-tuning. It stores any metadata that your reward function needs to score the model's response. It accepts a string-to-string dictionary.

For example, a string-matching reward that compares the model's answer to a known ground truth could use a dataset line like the following:

    {
      "systemInstruction": {
        "role": "system",
        "parts": [{ "text": "You are a helpful math tutor." }]
      },
      "contents": [
        {
          "role": "user",
          "parts": [{ "text": "What is 17 * 23? Put your final answer in $\\text{your answer}$." }]
        }
      ],
      "references": {
        "ground_truth_answer": "391"
      }
    }

Your reward function may read `references["ground_truth_answer"]` and compares it to the value the model produces. For details on how each reward type consumes `references` , see the [Reward functions](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/tuning/reinforcement-tuning/reinforcement-tuning-job/reward-functions) page.

## Dataset limits

The following limits apply to reinforcement learning fine-tuning datasets:

| Specification                                                 | Value  |
| ------------------------------------------------------------- | ------ |
| Maximum number of examples in a training dataset              | 5,000  |
| Maximum number of examples in a validation dataset            | 500    |
| Maximum dataset file size                                     | 1 GB   |
| Maximum input tokens per example                              | 32,768 |
| Maximum output tokens per example (including thinking tokens) | 32,768 |

### Multimodal limits

The following per-modality limits apply when your dataset includes image, audio, or video data:

### Audio

| Specification                                             | Value      |
| --------------------------------------------------------- | ---------- |
| Maximum number of audio files per prompt                  | 15         |
| Maximum total audio length per example (across all files) | 10 minutes |
| Maximum audio file size                                   | 100 MB     |

### Video

| Specification                                             | Value     |
| --------------------------------------------------------- | --------- |
| Maximum number of video files per prompt                  | 10        |
| Maximum total video length per example (across all files) | 5 minutes |
| Maximum video file size                                   | 20 MB     |

### Image

| Specification                       | Value |
| ----------------------------------- | ----- |
| Maximum number of images per prompt | 15    |
| Maximum image file size             | 20 MB |

## What's next

  - [Configure hyperparameters](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/tuning/reinforcement-tuning/reinforcement-tuning-job/hyperparameters) for your tuning job.
  - [Define reward functions](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/tuning/reinforcement-tuning/reinforcement-tuning-job/reward-functions) .
  - [Monitor job status and metrics](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/tuning/reinforcement-tuning/reinforcement-tuning-job/job-status-metrics-monitoring) .
  - Follow the [Quick start](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/tuning/reinforcement-tuning/quick-start) to create your first reinforcement learning fine-tuning job.
