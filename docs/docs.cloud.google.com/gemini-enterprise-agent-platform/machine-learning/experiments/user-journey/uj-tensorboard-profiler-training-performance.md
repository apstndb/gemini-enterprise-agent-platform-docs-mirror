---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/experiments/user-journey/uj-tensorboard-profiler-training-performance
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/experiments/user-journey/uj-tensorboard-profiler-training-performance
title: 'Profile model training performance using Cloud Profiler: Notebook'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

In this tutorial, you learn how to enable Profiler for custom training jobs.

## Notebook: Profile model training performance using Cloud Profiler

> To see an example of profile model training performance using , run the "Profile model training performance using Cloud Profiler" notebook in one of the following environments:
> 
> [![](https://docs.cloud.google.com/static/vertex-ai/images/colab-logo-32px.png) Open in Colab](https://colab.research.google.com/github/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/tensorboard/tensorboard_profiler_custom_training.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/colab-enterprise-logo-32px.png) Open in Colab Enterprise](https://console.cloud.google.com/agent-platform/colab/import/https%3A%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Ftensorboard%2Ftensorboard_profiler_custom_training.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/vertex-ai-workbench-logo-32px.png) Open in Agent Platform Workbench](https://console.cloud.google.com/agent-platform/workbench/deploy-notebook?download_url=https%3A%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Ftensorboard%2Ftensorboard_profiler_custom_training.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/github-logo-32px.png) View on GitHub](https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/tensorboard/tensorboard_profiler_custom_training.ipynb)

This tutorial uses the following Google Cloud ML services and resources:

  - Gemini Enterprise Agent Platform training
  - Vertex AI TensorBoard

The steps performed include:

  - Set up a service account and a Cloud Storage bucket.
  - Create a Vertex AI TensorBoard instance.
  - Create and run a custom training job that enables Profiler.
  - View the Profiler dashboard to debug your model training performance.

## Relevant content

  - [Profile model training performance using Profiler](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/tensorboard-profiler)
