---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/experiments/user-journey/uj-tensorboard-custom-training-custom-container
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/experiments/user-journey/uj-tensorboard-custom-training-custom-container
title: 'Vertex AI TensorBoard custom training with custom container: Notebook'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

In this tutorial, you learn how to create a custom training job using custom containers, and monitor your training process on Vertex AI TensorBoard in near real time.

## Notebook: Create custom training jobs using custom containers

> To see an example of tensorboard custom training with custom container, run the "Vertex AI TensorBoard custom training with custom container" notebook in one of the following environments:
> 
> [![](https://docs.cloud.google.com/static/vertex-ai/images/colab-logo-32px.png) Open in Colab](https://colab.research.google.com/github/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/tensorboard/tensorboard_custom_training_with_custom_container.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/colab-enterprise-logo-32px.png) Open in Colab Enterprise](https://console.cloud.google.com/vertex-ai/colab/import/https%3A%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Ftensorboard%2Ftensorboard_custom_training_with_custom_container.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/vertex-ai-workbench-logo-32px.png) Open in Agent Platform Workbench](https://console.cloud.google.com/vertex-ai/workbench/deploy-notebook?download_url=https%3A%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Ftensorboard%2Ftensorboard_custom_training_with_custom_container.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/github-logo-32px.png) View on GitHub](https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/tensorboard/tensorboard_custom_training_with_custom_container.ipynb)

This tutorial uses the following Google Cloud ML services and resources:

  - Gemini Enterprise Agent Platform training
  - Vertex AI TensorBoard

The steps performed include:

  - Create a Docker repository and config.
  - Create a custom container image with your customized training code.
  - Set up a service account and Cloud Storage buckets.
  - Create and launch your custom training job with your custom container.

## Relevant content

  - [Vertex AI TensorBoard](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/experiments/tensorboard-introduction)
  - [Custom training](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/overview)
