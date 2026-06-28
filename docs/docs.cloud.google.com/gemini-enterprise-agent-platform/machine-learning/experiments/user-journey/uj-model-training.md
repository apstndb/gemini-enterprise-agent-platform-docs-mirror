---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/experiments/user-journey/uj-model-training
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/experiments/user-journey/uj-model-training
title: 'Model training with prebuilt data pre-processing code: Notebook'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

As a Data Scientist, this is a common workflow: Train a model locally (in my Notebook), log the parameters, log the training time series metrics to Vertex AI TensorBoard , and log the evaluation metrics.

As a Data Scientist, I want to be able to reuse data pre-processing code that others within my company have written to simplify and standardize all the complex data wrangling that we do. I want to be able to:

1.  Use a Python data pre-processing library to clean up an in memory dataset (a Pandas Dataframe), in a notebook.
2.  Train a model using Keras (again in a notebook).

## Notebook: Model experimentation with preprocessed data

> To see an example of building a Vertex AI Experiments lineage for custom training, run the "Build Experiment lineage for custom training" notebook in one of the following environments:
> 
> [![](https://docs.cloud.google.com/static/vertex-ai/images/colab-logo-32px.png) Open in Colab](https://colab.research.google.com/github/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/experiments/build_model_experimentation_lineage_with_prebuild_code.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/colab-enterprise-logo-32px.png) Open in Colab Enterprise](https://console.cloud.google.com/agent-platform/colab/import/https%3A%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Fexperiments%2Fbuild_model_experimentation_lineage_with_prebuild_code.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/vertex-ai-workbench-logo-32px.png) Open in Agent Platform Workbench](https://console.cloud.google.com/agent-platform/workbench/deploy-notebook?download_url=https%3A%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Fexperiments%2Fbuild_model_experimentation_lineage_with_prebuild_code.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/github-logo-32px.png) View on GitHub](https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/experiments/build_model_experimentation_lineage_with_prebuild_code.ipynb)

In the "Build Vertex AI Experiments lineage for custom training" notebook, you'll learn how to integrate preprocessing code in Vertex AI Experiments. Also, you'll build the experiment lineage that lets you record, analyze, debug, and audit metadata and artifacts produced along your ML journey.

You can view the artifact lineage in the Google Cloud console.

![Agent Platform view artifact lineage](https://docs.cloud.google.com/static/gemini-enterprise-agent-platform/machine-learning/experiments/images/artifact-lineage-graph.png)

## Relevant content

[Manually log data to an experiment run](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/experiments/log-data)

  - [Log summary metrics](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/experiments/log-data#summary-metrics)
  - [Log time series metrics](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/experiments/log-data#time_series_metrics)
  - [Log parameters](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/experiments/log-data#parameters)
  - [Log classification metrics](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/experiments/log-data#classification-metrics)

<!-- end list -->

  - [Track executions and artifacts](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/experiments/track-executions-artifacts)
