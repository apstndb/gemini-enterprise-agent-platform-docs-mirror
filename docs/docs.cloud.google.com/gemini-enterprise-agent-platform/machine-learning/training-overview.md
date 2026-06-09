---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training-overview
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training-overview
title: Train and use your own models
description: Develop and deploy ML models on Agent Platform. Choose AutoML, run custom training with serverless jobs or dedicated clusters, or scale with Ray.
data_source: docs.cloud.google.com
---

This page provides an overview of the workflow for training and using your own machine learning (ML) models on Agent Platform. Agent Platform offers a spectrum of training methods designed to meet your needs, from fully automated to fully custom.

  - **AutoML** : Build high-quality models with minimal technical effort by leveraging Google's automated ML capabilities.
  - **Vertex AI serverless training** : Run your custom training code in a fully managed, on-demand environment without worrying about infrastructure.
  - **Vertex AI training clusters** : Run large-scale, high-performance training jobs on a dedicated cluster of accelerators reserved for your exclusive use.
  - **Ray on Agent Platform** : Scale Python applications and ML workloads using the open-source Ray framework on a managed service.

For help on deciding which of these methods to use, see [Choose a training method](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/start/training-methods) .

## AutoML

AutoML on Gemini Enterprise Agent Platform lets you build a code-free ML model based on the training data that you provide. AutoML can automate tasks like data preparation, model selection, hyperparameter tuning, and deployment for various data types and prediction tasks, which can make ML more accessible for a wide range of users.

### Types of models you can build using AutoML

The types of models you can build depend on the type of data that you have. Gemini Enterprise Agent Platform offers AutoML solutions for the following data types and model objectives:

| Data type    | Supported objectives                    |
| ------------ | --------------------------------------- |
| Image data   | Classification, object detection.       |
| Tabular data | Classification/regression, forecasting. |

To learn more about AutoML, see [AutoML training overview](https://docs.cloud.google.com/vertex-ai/docs/training/automl-training-overview) .

## Run custom training code on Agent Platform

If AutoML doesn't address your needs, you can provide your own training code and run it on Agent Platform's managed infrastructure. This gives you full control and flexibility over your model's architecture and training logic, letting you use any ML framework you choose.

Agent Platform provides two primary modes for running your custom training code: a serverless, on-demand environment, or a dedicated, reserved cluster.

### Vertex AI serverless training

Serverless training is a fully managed service that lets you run your custom training application without provisioning or managing any infrastructure. You package your code in a container, define your machine specifications (including CPUs and GPUs), and submit it as a `CustomJob` .

Agent Platform handles the rest:

  - Provisioning the compute resources for the duration of your job.
  - Executing your training code.
  - Deleting the resources after the job completes.

This pay-per-use, on-demand model is ideal for experimentation, rapid prototyping, and for production jobs that don't require assured, instantaneous capacity.

To learn more, see [Create a serverless training custom job](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/create-custom-job)

### Vertex AI training clusters

For large-scale, high-performance, and mission-critical training, you can reserve a dedicated cluster of accelerators. This provides assured capacity and eliminates queues, ensuring your jobs start immediately.

While you have exclusive use of these resources, Agent Platform still handles the operational overhead of managing the cluster, including hardware maintenance and OS patching. This "managed serverful" approach gives you the power of a dedicated cluster without the management complexity.

## Ray on Gemini Enterprise Agent Platform

Ray on Gemini Enterprise Agent Platform is a service that lets you use the open-source Ray framework for scaling AI and Python applications directly within Agent Platform. Ray is designed to provide the infrastructure for distributed computing and parallel processing for your ML workflow.

Ray on Gemini Enterprise Agent Platform provides a managed environment for running distributed applications using the Ray framework, offering scalability and integration with Google Cloud services.

To learn more about Ray on Gemini Enterprise Agent Platform see [Ray on Gemini Enterprise Agent Platform overview](https://docs.cloud.google.com/vertex-ai/docs/open-source/ray-on-vertex-ai/overview) .
