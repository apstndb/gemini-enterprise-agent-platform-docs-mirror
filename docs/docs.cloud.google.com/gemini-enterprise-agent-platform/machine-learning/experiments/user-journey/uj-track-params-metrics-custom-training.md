---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/experiments/user-journey/uj-track-params-metrics-custom-training
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/experiments/user-journey/uj-track-params-metrics-custom-training
title: 'Track parameters and metrics for custom training jobs: Notebook'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

This notebook demonstrates how to use Agent Platform SDK for Python to track metrics and parameters for Gemini Enterprise Agent Platform custom training jobs, and how to perform detailed analysis using this data.

## Notebook:

> To see an example of tracking parameters and metrics for a custom training job, run the "Track parameters and metrics for custom training job" notebook in one of the following environments:
> 
> [![](https://docs.cloud.google.com/static/vertex-ai/images/colab-logo-32px.png) Open in Colab](https://colab.research.google.com/github/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/ml_metadata/sdk-metric-parameter-tracking-for-custom-jobs.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/colab-enterprise-logo-32px.png) Open in Colab Enterprise](https://console.cloud.google.com/vertex-ai/colab/import/https%3A%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Fml_metadata%2Fsdk-metric-parameter-tracking-for-custom-jobs.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/vertex-ai-workbench-logo-32px.png) Open in Agent Platform Workbench](https://console.cloud.google.com/vertex-ai/workbench/deploy-notebook?download_url=https%3A%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Fml_metadata%2Fsdk-metric-parameter-tracking-for-custom-jobs.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/github-logo-32px.png) View on GitHub](https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/ml_metadata/sdk-metric-parameter-tracking-for-custom-jobs.ipynb)

This tutorial uses the following Google Cloud ML services and resources:

  - Gemini Enterprise Agent Platform dataset
  - Gemini Enterprise Agent Platform model
  - Gemini Enterprise Agent Platform endpoint
  - Gemini Enterprise Agent Platform custom training Job
  - Vertex AI Experiments

The steps performed include:

1.  Track training parameters and prediction metrics for a custom training job.
2.  Extract and perform analysis for all parameters and metrics within a Vertex AI Experiments.

## Relevant content

  - [Vertex ML Metadata](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/ml-metadata/introduction)
  - [Custom training overview](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/overview)
  - [Endpoint](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/python-sdk/prediction-classes#endpoint)
  - [Create and manage experiment runs](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/experiments/create-manage-exp-run#vertex-ai-sdk-for-python)
