---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/models/tuning
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/tuning
title: Introduction to tuning
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

[Video](https://www.youtube.com/watch?v=4A4W03qUTsw)

*Model tuning* is a crucial process in adapting Gemini to perform specific tasks with greater precision and accuracy. Model tuning works by providing a model with a training dataset that contains a set of examples of specific downstream tasks.

This page provides an overview of model tuning for Gemini, describes the tuning options available for Gemini, and helps you determine when each tuning option should be used.

## Benefits of model tuning

Model tuning is an effective way to customize large models to your tasks. It's a key step to improve the model's quality and efficiency. Model tuning provides the following benefits:

- Higher quality for your specific tasks
- Increased model robustness
- Lower inference latency and cost due to shorter prompts

## Tuning compared to prompt design

- **Prompting with pre-trained Gemini models** : Prompting is the art of crafting effective instructions to guide AI models like Gemini in generating the outputs you want. It involves designing prompts that clearly convey the task, format you want, and any relevant context. You can use Gemini's capabilities with minimal setup. It's best suited for:
  - Limited labeled data: If you have a small amount of labeled data or can't afford a lengthy fine-tuning process.
  - Rapid prototyping: When you need to quickly test a concept or get a baseline performance without heavy investment in fine-tuning.
- **Customized fine-tuning of Gemini models** : For more tailored results, Gemini lets you fine-tune its models on your specific datasets. To create an AI model that excels in your specific domain, consider fine-tuning. This involves retraining the base model on your own labeled dataset, adapting its weights to your task and data. You can adapt Gemini to your use cases. Fine-tuning is most effective when:
  - You have labeled data: A sizable dataset to train on (think 100 examples or more), which allows the model to deeply learn your task's specifics.
  - Complex or unique tasks: For scenarios where advanced prompting strategies are not sufficient, and a model tailored to your data is essential.

Start with prompting to find the optimal prompt. Then, move on to fine-tuning (if required) to further boost performance or fix recurring errors. Although adding more examples can be beneficial, it is important to evaluate where the model makes mistakes before adding more data. High-quality, well-labeled data is crucial for good performance and better than quantity. Also, the data you use for fine-tuning should reflect the prompt distribution, format, and context that the model encounters in production.

Tuning provides the following benefits over prompt design:

- Allows deep customization on the model and results in better performance on specific tasks.
- Align the model with custom syntax, instructions, domain specific semantic rules.
- Offers more consistent and reliable results.
- Capable of handling more examples at once.
- Save cost at inference by removing few-shot examples, long instructions in the prompts

## Tuning approaches

Parameter-efficient tuning and full fine-tuning are two approaches to customizing large models. Both methods have their advantages and implications in terms of model quality and resource efficiency.

### Parameter efficient tuning

Parameter-efficient tuning, also called adapter tuning, enables efficient adaptation of large models to your specific tasks or domain. Parameter-efficient tuning updates a relatively small subset of the model's parameters during the tuning process.

To understand how Gemini Enterprise Agent Platform supports adapter tuning and serving, you can find more details in the following whitepaper, [Adaptation of Large Foundation Models](https://services.google.com/fh/files/misc/adaptation_of_foundation_models_whitepaper_google_cloud.pdf) .

### Full fine-tuning

Full fine-tuning updates all parameters of the model, making it suitable for adapting the model to highly complex tasks, with the potential of achieving higher quality. However full fine tuning demands higher computational resources for both tuning and serving, leading to higher overall costs.

### Parameter efficient tuning compared to full fine tuning

Parameter-efficient tuning is more resource efficient and cost effective compared to full fine-tuning. It uses significantly lower computational resources to train. It's able to adapt the model faster with a smaller dataset. The flexibility of parameter-efficient tuning offers a solution for multi-task learning without the need for extensive retraining.

## Supported tuning methods

Agent Platform supports supervised fine-tuning, preference tuning, and reinforcement learning fine-tuning to customize foundation models. You can also use tuning checkpoints and continuous tuning across training runs.

The following table compares the primary tuning methods:

| Tuning method                                 | How it works                                                                                                                                          | Typical dataset size                                       | Best suited for                                                                                                                                                    |
|-----------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Supervised fine-tuning (SFT)**              | Trains on labeled input-output demonstrations                                                                                                         | Hundreds to thousands of labeled examples                  | Strict output formatting, classification, sentiment analysis, entity extraction, and domain-specific style or tone.                                                |
| **Preference tuning**                         | Optimizes pairwise preferences (chosen vs. rejected responses)                                                                                        | Hundreds to thousands of preference pairs                  | Aligning model behavior with subjective human preferences, helpfulness, or conversational tone.                                                                    |
| **Reinforcement learning fine-tuning (RLFT)** | Generates candidate reasoning traces and responses ( `MINIMAL` or `HIGH` thinking level) and maximizes scores from up to 16 weighted reward functions | Dozens to a few hundred prompts with `references` metadata | Multi-step reasoning, complex domain rules, verifiable tasks (such as code or SQL generation), and optimizing thinking models without degrading reasoning quality. |

### Supervised fine-tuning

Supervised fine-tuning improves the performance of the model by teaching it a new skill. Data that contains hundreds of labeled examples is used to teach the model to mimic a target behavior or task. Each labeled example demonstrates what you want the model to output during inference.

When you run a supervised fine-tuning job, the model learns additional parameters that help it encode the necessary information to perform the target task or learn the expected behavior. These parameters are used during inference. The output of the tuning job is a new model that combines the newly learned parameters with the original model.

Supervised fine-tuning of a text model is a good option when the output of your model isn't complex and is relatively easy to define. Supervised fine-tuning is recommended for classification, sentiment analysis, entity extraction, summarization of content that's not complex, and writing domain-specific queries.

#### Models that support supervised fine-tuning

The following Gemini models support supervised tuning:

#### Click to expand supported models

- [Gemini 3.5 Flash-Lite](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/3-5-flash-lite)
- [Gemini 3.5 Flash](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/3-5-flash)
- [Gemini 3.1 Flash-Lite](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/3-1-flash-lite)
- [Gemini 2.5 Pro](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/2-5-pro)
- [Gemini 2.5 Flash-Lite](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/2-5-flash-lite)
- [Gemini 2.5 Flash](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/2-5-flash)

For more information about using supervised fine-tuning with each data type, see the following pages: Tune [text](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/tuning/text) , [image](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/tuning/image) , [audio](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/tuning/audio) , [video](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/tuning/video) , and [document](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/tuning/document) data types.

### Preference tuning

Agent Platform preference tuning builds on supervised fine-tuning by letting you tune your Gemini models with human feedback data.

Preference tuning enables the model to learn from subjective user preferences that are hard to define by using specific labels and supervised fine-tuning alone.

#### Models that support preference tuning

The following Gemini models support preference tuning:

#### Click to expand supported models

- [Gemini 2.5 Flash-Lite](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/2-5-flash-lite)
- [Gemini 2.5 Flash](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/2-5-flash)

For more information about preference tuning, see [About preference tuning for Gemini models](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/tuning/preference-tuning) .

### Reinforcement learning fine-tuning

Reinforcement learning fine-tuning (RLFT) adapts Gemini models through trial-and-error exploration guided by programmatic or model-based reward functions. During training, the model samples multiple candidate responses and reasoning traces ( `MINIMAL` or `HIGH` thinking level) for each prompt, evaluates them using your reward configuration on a `[-1, 1]` scale, and updates a parameter-efficient LoRA adapter to maximize the reward.

Unlike supervised fine-tuning, which omits intermediate thinking tokens during training, reinforcement learning fine-tuning directly optimizes multi-step reasoning and generalizes well with smaller datasets (often dozens to a few hundred prompts). You can evaluate outputs using a single reward function or a weighted composite of up to 16 reward functions across four scorer types:

- **String match** : Compares model outputs against ground-truth fields in the dataset's `references` dictionary (exact string or JSON match, with optional regular expression extraction).
- **Gemini-based autorater** : Uses an LLM-as-a-judge rubric to return a numeric score or structured verdict.
- **Code execution** : Runs a custom Python `evaluate(example, response)` function in a managed sandbox environment.
- **Cloud Run** : Sends candidate responses to a custom HTTP endpoint hosted on Cloud Run for domain-specific verification.

#### Models that support reinforcement learning fine-tuning

The following Gemini models support reinforcement learning fine-tuning:

#### Click to expand supported models

- [Gemini 3.5 Flash](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/3-5-flash)
- [Gemini 3.1 Flash-Lite](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/3-1-flash-lite)

For more information about reinforcement learning fine-tuning, see [About reinforcement learning fine-tuning](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/tuning/reinforcement-tuning) .

### Tuning checkpoints

Tuning checkpoints let you save tuning progress, compare checkpoint performance, and choose the best-performing checkpoint, either by epoch for supervised fine-tuning or by step interval ( `checkpointInterval` ) for reinforcement learning fine-tuning.

#### Models that support tuning checkpoints

The following Gemini models support tuning checkpoints:

#### Click to expand supported models

- [Gemini 3.5 Flash](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/3-5-flash)
- [Gemini 3.1 Flash-Lite](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/3-1-flash-lite)
- [Gemini 2.5 Pro](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/2-5-pro)
- [Gemini 2.5 Flash-Lite](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/2-5-flash-lite)
- [Gemini 2.5 Flash](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/2-5-flash)

For more information about tuning checkpoints, see [Use checkpoints in Gemini tuning](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/tuning/checkpoints) and [Job status, metrics, and monitoring for reinforcement learning fine-tuning](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/tuning/reinforcement-tuning/reinforcement-tuning-job/job-status-metrics-monitoring) .

### Continuous tuning

Continuous tuning lets you continue tuning an already tuned model or model checkpoint. You can run additional supervised fine-tuning epochs on a tuned model ( `SFT -> SFT` ), apply reinforcement learning fine-tuning on top of a supervised fine-tuned checkpoint to combine strict formatting with enhanced reasoning ( `SFT -> RLFT` ), or continue training from a previous reinforcement learning checkpoint ( `RLFT -> RLFT` ).

#### Models that support continuous tuning

The following Gemini models support continuous tuning:

#### Click to expand supported models

- [Gemini 3.5 Flash](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/3-5-flash)
- [Gemini 3.1 Flash-Lite](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/3-1-flash-lite)
- [Gemini 2.5 Pro](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/2-5-pro)
- [Gemini 2.5 Flash-Lite](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/2-5-flash-lite)
- [Gemini 2.5 Flash](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/2-5-flash)

For more information about continuous tuning, see [About continuous tuning for Gemini models](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/tuning/continuous-tuning) and [Continuous tuning with reinforcement learning fine-tuning](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/tuning/reinforcement-tuning/continuous-tuning) .

## What's next

- Learn about [supervised fine-tuning](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/tuning/supervised-tuning) .
- Learn about [preference tuning](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/tuning/preference-tuning) .
- Learn about [reinforcement learning fine-tuning](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/tuning/reinforcement-tuning) .
- To start tuning, see [Tune Gemini models by using supervised fine-tuning](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/tuning/supervised-tuning/use) or [Create a reinforcement learning fine-tuning job](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/tuning/reinforcement-tuning/quick-start) .
- To learn how supervised fine-tuning can be used in a solution that builds a generative AI knowledge base, see [Jump Start Solution: Generative AI knowledge base](https://docs.cloud.google.com/architecture/ai-ml/generative-ai-knowledge-base) .
- To learn about tuning costs, see [Pricing](https://cloud.google.com/gemini-enterprise-agent-platform/generative-ai/pricing#model-tuning) .
