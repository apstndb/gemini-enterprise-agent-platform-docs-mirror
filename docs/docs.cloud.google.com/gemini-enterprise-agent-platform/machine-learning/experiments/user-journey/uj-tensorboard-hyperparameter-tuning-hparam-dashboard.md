---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/experiments/user-journey/uj-tensorboard-hyperparameter-tuning-hparam-dashboard
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/experiments/user-journey/uj-tensorboard-hyperparameter-tuning-hparam-dashboard
title: 'Vertex AI TensorBoard hyperparameter tuning with the HParams dashboard: Notebook'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

In this notebook, you train a model and perform hyperparameter tuning using TensorFlow. You also log the hyperparameters and metrics in Vertex AI TensorBoard.

## Notebook: Vertex AI TensorBoard hyperparameter tuning with the HParams dashboard

> To see an example of hyperparameter tuning using TensorFlow, run the "Vertex AI TensorBoard hyperparameter tuning with the HParams dashboard" notebook in one of the following environments:
> 
> [![](https://docs.cloud.google.com/static/vertex-ai/images/colab-logo-32px.png) Open in Colab](https://colab.research.google.com/github/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/tensorboard/tensorboard_hyperparameter_tuning_with_hparams.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/colab-enterprise-logo-32px.png) Open in Colab Enterprise](https://console.cloud.google.com/agent-platform/colab/import/https%3A%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Ftensorboard%2Ftensorboard_hyperparameter_tuning_with_hparams.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/vertex-ai-workbench-logo-32px.png) Open in Agent Platform Workbench](https://console.cloud.google.com/agent-platform/workbench/deploy-notebook?download_url=https%3A%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Ftensorboard%2Ftensorboard_hyperparameter_tuning_with_hparams.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/github-logo-32px.png) View on GitHub](https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/tensorboard/tensorboard_hyperparameter_tuning_with_hparams.ipynb)

This tutorial uses the following Gemini Enterprise Agent Platform services and resources:

  - Vertex AI TensorBoard
  - Gemini Enterprise Agent Platform Experiments

The steps performed include:

  - Adapt TensorFlow runs to log hyperparameters and metrics.
  - Start runs and log them all under one parent directory.
  - Visualize the results in TensorBoard's HParams dashboard.

## Relevant content

  - [Vertex AI TensorBoard](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/experiments/tensorboard-introduction)
