---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/experiments/user-journey/uj-get-started-vertex-ai-experiments
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/experiments/user-journey/uj-get-started-vertex-ai-experiments
title: 'Get started with Vertex AI Experiments: Notebook'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

This tutorial demonstrates how to use Vertex AI in production and covers getting started with Vertex AI Experiments.

## Notebook: Get started with Vertex AI Experiments

> To see an example of getting started with Vertex AI Experiments, run the "Get started with Experiments" notebook in one of the following environments:
> 
> [![](https://docs.cloud.google.com/static/vertex-ai/images/colab-logo-32px.png) Open in Colab](https://colab.research.google.com/github/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/experiments/get_started_with_vertex_experiments.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/colab-enterprise-logo-32px.png) Open in Colab Enterprise](https://console.cloud.google.com/vertex-ai/colab/import/https%3A%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Fexperiments%2Fget_started_with_vertex_experiments.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/vertex-ai-workbench-logo-32px.png) Open in Vertex AI Workbench](https://console.cloud.google.com/vertex-ai/workbench/deploy-notebook?download_url=https%3A%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Fexperiments%2Fget_started_with_vertex_experiments.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/github-logo-32px.png) View on GitHub](https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/experiments/get_started_with_vertex_experiments.ipynb)

This tutorial uses the following Google Cloud ML services:

  - Vertex AI Experiments
  - Vertex ML Metadata
  - Vertex AI training

The steps performed include:

  - Local (notebook) training
      - Create an experiment.
      - Create a first run in the experiment.
      - Log parameters and metrics.
      - Create artifact lineage.
      - Visualize the experiment results.
      - Execute a second run.
      - Compare the two runs in the experiment.
  - Cloud (Vertex AI) training
      - Within the training script:
          - Create an experiment.
          - Log parameters and metrics.
          - Create artifact lineage.
      - Create a Vertex AI training custom job.
      - Execute the custom job.
      - Visualize the experiment results.

## Relevant content

  - [Introduction to Vertex AI Experiments](https://docs.cloud.google.com/vertex-ai/machine-learning/experiments/intro-vertex-ai-experiments)
