---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/containers-overview
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/containers-overview
title: Custom containers overview
description: Learn about custom containers for training on Gemini Enterprise Agent Platform.
data_source: docs.cloud.google.com
---

A custom container is a Docker image that you create to run your training application. By running your machine learning (ML) training job in a *custom container* , you can use ML frameworks, non-ML dependencies, libraries, and binaries that are not otherwise supported on Agent Platform.

## How training with containers works

Your training application, implemented in the ML framework of your choice, is the core of the training process.

1.  Create an application that trains your model, using the ML framework of your choice.

2.  Decide whether to use a custom container. There could be a [prebuilt container](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/pre-built-containers) that already supports your dependencies. Otherwise, you need to [build a custom container for your training job](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/create-custom-container) . In your custom container, you pre-install your training application and all its dependencies onto an image that is used to run your training job.

3.  Store your training and verification data in a source that Agent Platform can access. To simplify authentication and reduce latency, store your data in Cloud Storage, Bigtable, or another Google Cloud storage service in the same Google Cloud project and region that you are using for Agent Platform. Learn more about [the ways Agent Platform can load your data](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/code-requirements#loading-data) .

4.  When your application is ready to run, you must build your Docker image and push it to Artifact Registry or Docker Hub, making sure that [Agent Platform can access your registry](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/create-custom-container#manage-container-registry-permissions) .

5.  Submit your serverless training job by [creating a custom job](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/create-custom-job) or [creating a serverless training pipeline](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/create-training-pipeline) .

6.  Agent Platform sets up resources for your job. It allocates one or more virtual machines (called *training instances* ) based on your job configuration. You set up a training instance by using the custom container you specify as part of the [`WorkerPoolSpec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/CustomJobSpec#workerpoolspec) object when you [submit your serverless training job](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/create-custom-job) .

7.  Agent Platform runs your Docker image, passing through any command-line arguments you specify when you create the training job.

8.  When your training job succeeds or encounters an unrecoverable error, Agent Platform halts all job processes and cleans up the resources.

## Advantages of custom containers

Custom containers let you specify and pre-install all the dependencies needed for your application.

  - **Faster start-up time.** If you use a custom container with your dependencies pre-installed, you can save the time that your training application would otherwise take to install dependencies when starting up.
  - **Use the ML framework of your choice.** If you can't find an Agent Platform prebuilt container with the ML framework you want to use, you can build a custom container with your chosen framework and use it to run jobs on Agent Platform. For example, you can use a customer container to train with PyTorch.
  - **Extended support for distributed training.** With custom containers, you can do distributed training using any ML framework.
  - **Use the newest version.** You can also use the latest build or minor version of an ML framework. For example, you can build a custom container to train with `tf-nightly` .

## Hyperparameter tuning with custom containers

To do [hyperparameter tuning](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/hyperparameter-tuning-overview) on Agent Platform, you specify goal metrics, along with whether to minimize or maximize each metric. For example, you might want to maximize your model accuracy, or minimize your model loss. You also list the hyperparameters you'd like to tune, along with the range of acceptable values for each hyperparameter. Agent Platform does multiple *trials* of your training application, tracking and adjusting the hyperparameters after each trial. When the hyperparameter tuning job is complete, Agent Platform reports values for the most effective configuration of your hyperparameters, and a summary for each trial.

To do hyperparameter tuning with custom containers, you need to make the following adjustments:

  - In your Dockerfile: install [`cloudml-hypertune`](https://github.com/GoogleCloudPlatform/cloudml-hypertune) .
  - In your training code:
      - Use `cloudml-hypertune` to report the results of each trial by calling its helper function, [`report_hyperparameter_tuning_metric`](https://github.com/GoogleCloudPlatform/cloudml-hypertune/blob/master/hypertune/hypertune.py#L49) .
      - Add command-line arguments for each hyperparameter, and handle the argument parsing with an argument parser such as [`argparse`](https://docs.python.org/3/library/argparse.html) .

See how to [configure a hyperparameter tuning job that uses custom containers](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/using-hyperparameter-tuning) or learn more about [how hyperparameter tuning works on Agent Platform](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/hyperparameter-tuning-overview) .

## GPUs in custom containers

For training with GPUs, your custom container needs to meet a few special requirements. You must build a different Docker image than what you'd use for training with CPUs.

  - Pre-install the CUDA toolkit and cuDNN in your Docker image. The recommended way to build a custom container with support for GPUs is to use the [`nvidia/cuda`](https://hub.docker.com/r/nvidia/cuda/) image as your base image for your custom container. The `nvidia/cuda` container image has matching versions of CUDA toolkit and cuDNN pre-installed, and it helps you set up the related environment variables correctly.
  - Install your training application, along with your required ML framework and other dependencies in your Docker image.

See an [example Dockerfile for training with GPUs](https://github.com/GoogleCloudPlatform/cloudml-samples/blob/master/pytorch/containers/quickstart/mnist/Dockerfile-gpu) .

## What's next

  - Learn more about how to [create a custom container for your training job](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/create-custom-container) .
