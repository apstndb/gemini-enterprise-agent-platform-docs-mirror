---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/experiments/user-journey/uj-compare-models
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/experiments/user-journey/uj-compare-models
title: 'Compare trained and evaluated models: Notebook'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

As a Data Scientist, this is a common workflow: Train a model locally (in my Notebook), log the parameters, log the training time series metrics to Vertex AI TensorBoard , and log the evaluation metrics.

You can view the experiment runs associated with an experiment on the experiments page in the Google Cloud console.

![train, log parameters and time series metrics to TensorBoard](https://docs.cloud.google.com/static/gemini-enterprise-agent-platform/machine-learning/experiments/images/console-compare.png)

## Notebook: Compare locally trained models

> To see an example of comparing models, run the ": Track parameters and metrics for locally trained models" notebook in one of the following environments:
> 
> [![](https://docs.cloud.google.com/static/vertex-ai/images/colab-logo-32px.png) Open in Colab](https://colab.research.google.com/github/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/experiments/comparing_local_trained_models.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/colab-enterprise-logo-32px.png) Open in Colab Enterprise](https://console.cloud.google.com/vertex-ai/colab/import/https%3A%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Fexperiments%2Fcomparing_local_trained_models.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/vertex-ai-workbench-logo-32px.png) Open in Vertex AI Workbench](https://console.cloud.google.com/vertex-ai/workbench/deploy-notebook?download_url=https%3A%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Fexperiments%2Fcomparing_local_trained_models.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/github-logo-32px.png) View on GitHub](https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/experiments/comparing_local_trained_models.ipynb)

In the "Vertex AI: Track parameters and metrics for locally trained models" notebook, you'll learn how to use Vertex AI Experiments to:

  - Log the model parameters.
  - Log the loss and metrics on every epoch to TensorBoard.
  - Log the evaluation metrics.
  - Compare two experiment runs.

## Relevant content

[Log data to an experiment run](https://docs.cloud.google.com/vertex-ai/docs/experiments/log-data)

  - [Assign backing Vertex AI TensorBoard resource for Time Series Metric](https://docs.cloud.google.com/vertex-ai/docs/experiments/log-data#assign_backing_resource_for_time_series_metric)
  - [Log summary metrics](https://docs.cloud.google.com/vertex-ai/docs/experiments/log-data#summary_metrics)
  - [Log time series metrics](https://docs.cloud.google.com/vertex-ai/docs/experiments/log-data#time_series_metrics)
  - [Log parameters](https://docs.cloud.google.com/vertex-ai/docs/experiments/log-data#parameters)
