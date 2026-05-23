---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/genai-training-overview
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/genai-training-overview
title: Generative AI on Gemini Enterprise Agent Platform training overview
description: Provides an overview of the various training options available in Generative AI.
data_source: docs.cloud.google.com
---

Generative AI often relies on large-scale machine learning (ML) models that are pre-trained on vast amounts of data. These are referred to as foundation models and serve as a base for various tasks. There are numerous ways to customize foundation models using Generative AI on Gemini Enterprise Agent Platform:

  - Tuning: Tuning involves providing a model with a training dataset of specific examples relevant to the chosen downstream task.
    
      - [Supervised tuning](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/tune-models#how-tuning-works) : This technique uses labeled examples to fine-tune a model. Each example demonstrates the chosen output for a given input during inference. Supervised tuning is effective for tasks where the expected output isn't overly complex and can be clearly defined, such as classification, sentiment analysis, entity extraction, summarization of less complex content, and generating domain-specific queries. You can tune text, image, audio, and document data types using supervised learning.
      - Reinforcement Learning from Human Feedback (RLHF) tuning: This method is suitable when the selected model output is more complex. RLHF tuning works well for objectives that aren't easily differentiated through supervised tuning, such as question answering, summarization of complex content, and creative content generation.

  - Distillation: Distillation often involves training a smaller "student" model to mimic the behavior of a larger, more capable "teacher" model.

  - Adapter model training: This involves training smaller adapter models (or layers) that work in conjunction with a foundation model to improve performance on specialized tasks. The original foundation model's parameters are often kept frozen, and only the adapter's weights are updated during training.

  - Grounding: While not a training method, grounding is a critical aspect of ensuring the reliability of generative AI outputs. [Grounding](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/grounding/overview) involves connecting the model's output to verifiable sources of information, reducing the likelihood of invented content. This often involves providing the model with access to specific data sources during inference.

## What's next

  - [Overview of Generative AI on Agent Platform](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/overview)
