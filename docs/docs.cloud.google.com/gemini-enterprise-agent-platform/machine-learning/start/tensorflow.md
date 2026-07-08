---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/start/tensorflow
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/start/tensorflow
title: TensorFlow integration
description: Review resources that show you how to use TensorFlow on Gemini Enterprise Agent Platform.
data_source: docs.cloud.google.com
---

This page explains Gemini Enterprise Agent Platform's TensorFlow integration and provides resources that show you how to use TensorFlow on Gemini Enterprise Agent Platform. Gemini Enterprise Agent Platform's TensorFlow integration makes it easier for you to train, deploy, and orchestrate TensorFlow models in production.

## Run code in notebooks

Agent Platform provides two options for running your code in notebooks, Colab Enterprise and Vertex AI Workbench. To learn more about these options, see [choose a notebook solution](https://docs.cloud.google.com/gemini-enterprise-agent-platform/workbench/notebook-solution) .

## Prebuilt containers for training

Gemini Enterprise Agent Platform provides prebuilt Docker container images for model training. These containers are organized by machine learning frameworks and framework versions and include common dependencies that you might want to use in your training code.

To learn about which TensorFlow versions have prebuilt training containers and how to train models with a prebuilt training container, see [Prebuilt containers for custom training](https://docs.cloud.google.com/gemini-enterprise-agent-platform/training/pre-built-containers#tensorflow) .

## Distributed training

You can run distributed training of TensorFlow models on Gemini Enterprise Agent Platform. For multi-worker training, you can use Reduction Server to optimize performance even further for all-reduce collective operations. To learn more about distributed training on Gemini Enterprise Agent Platform, see [Distributed training](https://docs.cloud.google.com/gemini-enterprise-agent-platform/training/distributed-training) .

## Prebuilt containers for inference

Similar to prebuilt containers for training, Gemini Enterprise Agent Platform provides prebuilt container images for serving inferences and explanations from TensorFlow models that you either created within or outside of Gemini Enterprise Agent Platform. These images provide HTTP inference servers that you can use to serve inferences with minimal configuration.

To learn about which TensorFlow versions have prebuilt training containers and how to train models with a prebuilt training container, see [Prebuilt containers for custom training](https://docs.cloud.google.com/gemini-enterprise-agent-platform/predictions/pre-built-containers#tensorflow) .

### Optimized TensorFlow runtime

> **Preview**
> 
> This product or feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](https://docs.cloud.google.com/terms/service-terms#1) . Pre-GA products and features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

The [optimized TensorFlow runtime](https://docs.cloud.google.com/gemini-enterprise-agent-platform/predictions/optimized-tensorflow-runtime) uses model optimizations and new proprietary Google technologies to improve the speed and lower the cost of inferences compared to Gemini Enterprise Agent Platform's standard prebuilt inference containers for TensorFlow.

## TensorFlow Cloud Profiler integration

Train models cheaper and faster by monitoring and optimizing the performance of your training job using Gemini Enterprise Agent Platform's TensorFlow Cloud Profiler integration. TensorFlow Cloud Profiler helps you understand the resource consumption of training operations so you can identify and eliminate performance bottlenecks.

To learn more about Agent Platform TensorFlow Cloud Profiler, see [Profile model training performance using Profiler](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/tensorboard-profiler) .

## Resources for using TensorFlow on Gemini Enterprise Agent Platform

To learn more and start using TensorFlow in Gemini Enterprise Agent Platform, see the following resources.

  - [Prototype to Production](https://www.youtube.com/playlist?list=PLIivdWyY5sqJAyUJbbsc8ZyGLNT4isnuB) : A video series that provides and end-to-end example of developing and deploying a custom TensorFlow model on Gemini Enterprise Agent Platform.

  - [Optimize training performance with Reduction Server on Gemini Enterprise Agent Platform](https://cloud.google.com/blog/topics/developers-practitioners/optimize-training-performance-reduction-server-vertex-ai) : A blog post on optimizing distributed training on Gemini Enterprise Agent Platform by using Reduction Server.

  - [How to optimize training performance with the TensorFlow Cloud Profiler on Gemini Enterprise Agent Platform](https://cloud.google.com/blog/topics/developers-practitioners/how-optimize-training-performance-tensorflow-profiler-vertex-ai) : A blog post that shows you how to identify performance bottlenecks in your training job by using Gemini Enterprise Agent Platform TensorFlow Cloud Profiler.

  - [Custom model batch prediction with feature filtering](https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/prediction/custom_batch_prediction_feature_filter.ipynb) : A notebook tutorial that shows you how to use the Agent Platform SDK for Python to train a custom tabular classification model and perform batch inference with feature filtering.

  - [Agent Platform Pipelines: Custom training with prebuilt Google Cloud Pipeline Components](https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/pipelines/custom_model_training_and_batch_prediction.ipynb) : A notebook tutorial that shows you how to use Gemini Enterprise Agent Platform Pipelines with prebuilt Google Cloud Pipeline Components for custom training.

  - [Co-host TensorFlow models on the same VM for predictions](https://codelabs.developers.google.com/vertex-cohost-prediction#0) : A codelab that shows you how to use the co-hosting model feature in Gemini Enterprise Agent Platform to host multiple models on the same VM for online inferences.
