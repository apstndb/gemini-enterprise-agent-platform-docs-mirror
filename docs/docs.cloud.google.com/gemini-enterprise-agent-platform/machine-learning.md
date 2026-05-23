---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning
title: Introduction to machine learning on Gemini Enterprise Agent Platform
description: Learn about the machine learning capabilities on Gemini Enterprise Agent Platform, including managed datasets, serverless training, and model management.
data_source: docs.cloud.google.com
---

Gemini Enterprise Agent Platform provides a comprehensive suite of tools to help you build, train, and manage machine learning (ML) models at scale. Whether you are using AutoML for a fast path to high-quality models or creating custom models with popular frameworks like TensorFlow and PyTorch, Agent Platform operationalizes the entire ML lifecycle.

## Data preparation

Before you can train a model, you need to prepare your data. Agent Platform provides managed datasets to simplify this process.

Managed datasets allow you to provide source data for training models. They are required for AutoML and optional for custom training. You can create datasets for different data types, including image and tabular data.

For more information, see [Overview of creating managed datasets on Gemini Enterprise Agent Platform](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/datasets/overview) .

## Model training

Agent Platform provides a managed training service that helps you operationalize large-scale model training.

You can run training applications based on any ML framework on Google Cloud infrastructure. Agent Platform also offers integrated support for popular frameworks like PyTorch, TensorFlow, scikit-learn, and XGBoost.

Key benefits of serverless training include:

  - **Fully managed compute infrastructure** : Train models without provisioning or managing servers.
  - **High performance** : Optimized training jobs that can provide faster performance.
  - **Distributed training** : Support for multi-node distributed training to reduce time and cost.
  - **Hyperparameter optimization** : Automatically discover optimal values for your model.

For more information, see [serverless training overview](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/overview) .

## Model management

After training your model, you can manage it in the Model Registry.

The Model Registry is a central repository where you can manage the lifecycle of your ML models. It allows you to track model versions, evaluate model quality, and deploy models for serving inferences.

For more information, see [Introduction to Model Registry](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/model-registry/introduction) .

## What's next

  - [Create a managed dataset](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/datasets/overview) .
  - [Explore training options](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/overview) .
  - [Learn about Model Registry](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/model-registry/introduction) .
