---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/experiments/user-journey/uj-delete-outdated-tb-experiments
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/experiments/user-journey/uj-delete-outdated-tb-experiments
title: 'Delete outdated Vertex AI TensorBoard experiments: Notebook'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

In this tutorial, you'll learn how to delete outdated Vertex AI TensorBoard experiments to avoid unnecessary storage costs.

## Notebook

> To see an example of deleting outdated experiments in TensorBoard, run the "Delete Outdated Experiments in TensorBoard" notebook in one of the following environments:
> 
> [![](https://docs.cloud.google.com/static/vertex-ai/images/colab-logo-32px.png) Open in Colab](https://colab.research.google.com/github/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/experiments/delete_outdated_tensorboard_experiments.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/colab-enterprise-logo-32px.png) Open in Colab Enterprise](https://console.cloud.google.com/vertex-ai/colab/import/https%3A%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Fexperiments%2Fdelete_outdated_tensorboard_experiments.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/vertex-ai-workbench-logo-32px.png) Open in Vertex AI Workbench](https://console.cloud.google.com/vertex-ai/workbench/deploy-notebook?download_url=https%3A%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Fexperiments%2Fdelete_outdated_tensorboard_experiments.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/github-logo-32px.png) View on GitHub](https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/experiments/delete_outdated_tensorboard_experiments.ipynb)

This tutorial uses the following Google Cloud ML services:

  - Vertex AI TensorBoard

The steps performed include:

  - How to delete the Vertex AI TensorBoard experiment with a predefined key-value label pair `<label_key, label_value>` .
  - How to delete the Vertex AI TensorBoard experiment created before the `create_time` .
  - How to delete the Vertex AI TensorBoard experiment created before the `update_time` .

## Relevant content

  - [Create or delete an experiment](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/experiments/create-experiment)
