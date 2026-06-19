---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/start/pytorch
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/start/pytorch
title: PyTorch integration
description: Review resources that show you how to use PyTorch on Gemini Enterprise Agent Platform.
data_source: docs.cloud.google.com
---

> To see an example of PyTorch integration, run the "Training, tuning and deploying a PyTorch text sentiment classification model" notebook in one of the following environments:
> 
> [![](https://docs.cloud.google.com/static/vertex-ai/images/colab-logo-32px.png) Open in Colab](https://colab.research.google.com/github/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/training/pytorch-text-sentiment-classification-custom-train-deploy.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/colab-enterprise-logo-32px.png) Open in Colab Enterprise](https://console.cloud.google.com/agent-platform/colab/import/https%3A%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Ftraining%2Fpytorch-text-sentiment-classification-custom-train-deploy.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/vertex-ai-workbench-logo-32px.png) Open in Agent Platform Workbench](https://console.cloud.google.com/agent-platform/workbench/deploy-notebook?download_url=https%3A%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Ftraining%2Fpytorch-text-sentiment-classification-custom-train-deploy.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/github-logo-32px.png) View on GitHub](https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/training/pytorch-text-sentiment-classification-custom-train-deploy.ipynb)

[Video](https://www.youtube.com/watch?v=0R6O7o6Hluw)

This page explains Gemini Enterprise Agent Platform's PyTorch integration and provides resources that show you how to use PyTorch on Gemini Enterprise Agent Platform. Gemini Enterprise Agent Platform's PyTorch integration makes it easier for you to train, deploy, and orchestrate PyTorch models in production.

## Run code in notebooks

Agent Platform provides two options for running your code in notebooks, Colab Enterprise and Vertex AI Workbench. To learn more about these options, see [choose a notebook solution](https://docs.cloud.google.com/vertex-ai/docs/workbench/notebook-solution) .

## Prebuilt containers for training

Gemini Enterprise Agent Platform provides prebuilt Docker container images for model training. These containers are organized by machine learning frameworks and framework versions and include common dependencies that you might want to use in your training code. To learn about which PyTorch versions have prebuilt training containers and how to train models with a prebuilt training container, see [Prebuilt containers for custom training](https://docs.cloud.google.com/vertex-ai/docs/training/pre-built-containers#pytorch) .

## Prebuilt containers for serving inferences

Gemini Enterprise Agent Platform provides prebuilt Docker container images for serving both batch and online inferences. These containers are organized by machine learning frameworks and framework versions and include common dependencies that you might want to use in your inference code. To learn about which PyTorch versions have prebuilt inference containers and how to serve models with a prebuilt inference container, see [Prebuilt containers for custom training](https://docs.cloud.google.com/vertex-ai/docs/predictions/pre-built-containers) .

## Distributed training

You can run distributed training of PyTorch models on Gemini Enterprise Agent Platform. For multi-worker training, you can use Reduction Server to optimize performance even further for all-reduce collective operations. To learn more about distributed training on Gemini Enterprise Agent Platform, see [Distributed training](https://docs.cloud.google.com/vertex-ai/docs/training/distributed-training) .

## Resources for using PyTorch on Gemini Enterprise Agent Platform

To learn more and start using PyTorch in Gemini Enterprise Agent Platform, see the following resources:

  - [How to train and tune PyTorch models on Gemini Enterprise Agent Platform](https://cloud.google.com/blog/topics/developers-practitioners/pytorch-google-cloud-how-train-and-tune-pytorch-models-vertex-ai) : Learn how to use [Gemini Enterprise Agent Platform Training](https://docs.cloud.google.com/vertex-ai/docs/training/overview) to build and train a sentiment text classification model using PyTorch and [Gemini Enterprise Agent Platform Hyperparameter Tuning](https://docs.cloud.google.com/vertex-ai/docs/training/using-hyperparameter-tuning) to tune hyperparameters of PyTorch models.
  - [How to deploy PyTorch models on Gemini Enterprise Agent Platform](https://cloud.google.com/blog/topics/developers-practitioners/pytorch-google-cloud-how-deploy-pytorch-models-vertex-ai) : Walk through the deployment of a Pytorch model using [TorchServe](https://pytorch.org/serve/) as a custom container, by deploying the model artifacts to a [Vertex AI Inference](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions) service.
  - [Orchestrating PyTorch ML Workflows on Agent Platform Pipelines](https://cloud.google.com/blog/topics/developers-practitioners/orchestrating-pytorch-ml-workflows-vertex-ai-pipelines) : See how to build and orchestrate ML pipelines for training and deploying PyTorch models on Google Cloud Gemini Enterprise Agent Platform using [Agent Platform Pipelines](https://docs.cloud.google.com/vertex-ai/docs/pipelines/introduction) .
  - [Scalable ML Workflows using PyTorch on Kubeflow Pipelines and Vertex Pipelines](https://cloud.google.com/blog/topics/developers-practitioners/scalable-ml-workflows-using-pytorch-kubeflow-pipelines-and-vertex-pipelines) : Take a look at examples of [PyTorch](https://pytorch.org/) -based ML workflows on OSS [Kubeflow Pipelines](https://www.kubeflow.org/docs/components/pipelines/) , (part of the Kubeflow project) and [Agent Platform Pipelines](https://docs.cloud.google.com/vertex-ai/docs/pipelines) . We share [new PyTorch built-in components](https://github.com/kubeflow/pipelines/tree/master/components/PyTorch/pytorch-kfp-components) added to the Kubeflow Pipelines.
  - [Serving PyTorch image models with prebuilt containers on Agent Platform](https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/prediction/pytorch_image_classification_with_prebuilt_serving_containers.ipynb) : This notebook deploys a PyTorch image classification model on Agent Platform using prebuilt PyTorch serving images.

## What's next

  - Tutorial: Use Gemini Enterprise Agent Platform to train a PyTorch image classification model in one of Gemini Enterprise Agent Platform's prebuilt container environments by using the Google Cloud console.
    
    -----
    
    To follow step-by-step guidance for this task directly in the Google Cloud console, click **Guide me** :
    
    -----
