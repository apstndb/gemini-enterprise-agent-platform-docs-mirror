---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/experiments/user-journey/uj-tensorboard-integration-pipelines
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/experiments/user-journey/uj-tensorboard-integration-pipelines
title: 'Vertex AI TensorBoard integration with Gemini Enterprise Agent Platform Pipelines: Notebook'
description: Learn how to create a training pipeline using the KFP SDK.
data_source: docs.cloud.google.com
---

In this tutorial, you'll learn how to create a training pipeline using the KFP SDK, execute the pipeline in Gemini Enterprise Agent Platform Pipelines, and monitor your training process on Vertex AI TensorBoard in near real time.

> To see an example of tensorboard integration with pipelines, run the "Vertex AI TensorBoard integration with Vertex AI Pipelines" notebook in one of the following environments:
> 
> [![](https://docs.cloud.google.com/static/vertex-ai/images/colab-logo-32px.png) Open in Colab](https://colab.research.google.com/github/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/tensorboard/tensorboard_vertex_ai_pipelines_integration.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/colab-enterprise-logo-32px.png) Open in Colab Enterprise](https://console.cloud.google.com/agent-platform/colab/import/https%3A%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Ftensorboard%2Ftensorboard_vertex_ai_pipelines_integration.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/vertex-ai-workbench-logo-32px.png) Open in Agent Platform Workbench](https://console.cloud.google.com/agent-platform/workbench/deploy-notebook?download_url=https%3A%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Ftensorboard%2Ftensorboard_vertex_ai_pipelines_integration.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/github-logo-32px.png) View on GitHub](https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/tensorboard/tensorboard_vertex_ai_pipelines_integration.ipynb)

This tutorial uses the following Google Cloud ML services and resources:

  - Gemini Enterprise Agent Platform training
  - Vertex AI TensorBoard
  - Gemini Enterprise Agent Platform Pipelines

The steps performed include:

  - Setup a service account and Cloud Storage buckets.
  - Construct a Kubeflow Pipelines (KPT) with your custom training code.
  - Compile and execute the KFP pipeline in Gemini Enterprise Agent Platform Pipelines with Vertex AI TensorBoard enabled for near real time monitoring.

## Relevant content

  - [Use Vertex AI TensorBoardwith Gemini Enterprise Agent Platform Pipelines](https://docs.cloud.google.com/vertex-ai/docs/experiments/tensorboard-with-pipelines)
