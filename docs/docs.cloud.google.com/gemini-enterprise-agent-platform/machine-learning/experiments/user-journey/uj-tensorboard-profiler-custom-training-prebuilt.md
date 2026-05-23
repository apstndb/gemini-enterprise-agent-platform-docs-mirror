---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/experiments/user-journey/uj-tensorboard-profiler-custom-training-prebuilt
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/experiments/user-journey/uj-tensorboard-profiler-custom-training-prebuilt
title: 'Profile model training performance using Cloud Profiler in custom training with prebuilt container: Notebook'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

In this tutorial, you learn how to enable Profiler in Vertex AI for custom training jobs with a prebuilt container.

## Notebook: Profile model training performance using Cloud Profiler in prebuilt container

> To see an example of profile model training performance, run the "Profile model training performance using Cloud Profiler in custom training with prebuilt container" notebook in one of the following environments:
> 
> [![](https://docs.cloud.google.com/static/vertex-ai/images/colab-logo-32px.png) Open in Colab](https://colab.research.google.com/github/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/tensorboard/tensorboard_profiler_custom_training_with_prebuilt_container.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/colab-enterprise-logo-32px.png) Open in Colab Enterprise](https://console.cloud.google.com/vertex-ai/colab/import/https%3A%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Ftensorboard%2Ftensorboard_profiler_custom_training_with_prebuilt_container.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/vertex-ai-workbench-logo-32px.png) Open in Vertex AI Workbench](https://console.cloud.google.com/vertex-ai/workbench/deploy-notebook?download_url=https%3A%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Ftensorboard%2Ftensorboard_profiler_custom_training_with_prebuilt_container.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/github-logo-32px.png) View on GitHub](https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/tensorboard/tensorboard_profiler_custom_training_with_prebuilt_container.ipynb)

This tutorial uses the following Google Cloud ML services and resources:

  - Vertex AI training
  - Vertex AI TensorBoard

The steps performed include:

  - Prepare your custom training code and load your training code as a Python package to a prebuilt container.
  - Create and run a custom training job that enables Profiler.
  - View the Profiler dashboard to debug your model training performance.

## Relevant content

  - [Profile model training performance using Profiler](https://docs.cloud.google.com/vertex-ai/machine-learning/training/tensorboard-profiler)
