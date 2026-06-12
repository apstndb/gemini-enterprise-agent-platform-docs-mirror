---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/custom-training-methods
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/custom-training-methods
title: Choose a Gemini Enterprise Agent Platform serverless training method
description: 'Learn about three types of resources that you can use to train custom models on Agent Platform: custom jobs, hyperparameter tuning jobs, and training pipelines.'
data_source: docs.cloud.google.com
---

If you're writing your own training code instead of using AutoML}, there are several ways of doing Gemini Enterprise Agent Platform serverless training to consider. This document provides a brief overview and comparison of the different ways you can run serverless training.

## Serverless training resources on Agent Platform

There are three types of Agent Platform resources you can create to train custom models on Agent Platform:

  - [Custom jobs](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/create-custom-job)
  - [Hyperparameter tuning jobs](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/using-hyperparameter-tuning)
  - [Training pipelines](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/create-training-pipeline)

When you create a *custom job* , you specify settings that Agent Platform needs to run your training code, including:

  - One worker pool for single-node training ( [`WorkerPoolSpec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/CustomJobSpec#workerpoolspec) ), or multiple worker pools for distributed training
  - Optional settings for configuring job scheduling ( [`Scheduling`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/CustomJobSpec#scheduling) ), [setting certain environment variables for your training code](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/code-requirements#environment-variables) , [using a custom service account](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/custom-service-account) , and [using VPC Network Peering](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/vpc-peering)

Within the worker pool(s), you can specify the following settings:

  - [Machine types and accelerators](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/configure-compute)
  - [Configuration of what type of training code the worker pool runs](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/configure-container-settings) : either a Python training application ( [`PythonPackageSpec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/CustomJobSpec#pythonpackagespec) ) or a custom container ( [`ContainerSpec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/CustomJobSpec#containerspec) )

[Hyperparameter tuning jobs](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/using-hyperparameter-tuning) have additional settings to configure, such as the metric. Learn more about [hyperparameter tuning](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/hyperparameter-tuning-overview) .

A *training pipeline* orchestrates serverless training jobs or hyperparameter tuning jobs with additional steps, such as loading a dataset or uploading the model to Agent Platform after the training job is successfully completed.

### Serverless training resources

To view existing training pipelines in your project, go to the **Training Pipelines** page in the **Agent Platform** section of the Google Cloud console.

> **Note:** The **Training pipelines** page shows AutoML training pipelines, in addition to serverless training pipelines. You can use the **Model type** column to distinguish between the two.

To view existing custom jobs in your project, go to the **Custom jobs** page.

To view existing hyperparameter tuning jobs in your project, go to the **Hyperparameter tuning** page.

## Prebuilt and custom containers

Before you submit a serverless training job, hyperparameter tuning job, or a training pipeline to Agent Platform, you need to create a [Python training application](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/create-python-pre-built-container) or a [custom container](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/create-custom-container) to define the training code and dependencies you want to run on Agent Platform. If you create a Python training application using TensorFlow, PyTorch, scikit-learn, or XGBoost, you can use our prebuilt containers to run your code. If you're not sure which of these options to choose, refer to the [training code requirements](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/code-requirements) to learn more.

## Distributed training

You can configure a serverless training job, hyperparameter tuning job, or a training pipeline for distributed training by specifying multiple worker pools:

  - Use your first worker pool to configure your primary replica, and set the replica count to 1.
  - Add more worker pools to configure worker replicas, parameter server replicas, or evaluator replicas, if your machine learning framework supports these additional cluster tasks for distributed training.

Learn more about [using distributed training](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/distributed-training) .

## What's next

  - Learn how to [create a persistent resource](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/persistent-resource-create) to run serverless training jobs.
  - See [Create serverless training jobs](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/create-custom-job) to learn how to create serverless training jobs to run your serverless training applications on Gemini Enterprise Agent Platform.
  - See [Create training pipelines](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/create-training-pipeline) to learn how to create training pipelines to run serverless training applications on Gemini Enterprise Agent Platform.
  - See [Use hyperparameter tuning](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/using-hyperparameter-tuning) to learn about Hyperparameter tuning searches.
