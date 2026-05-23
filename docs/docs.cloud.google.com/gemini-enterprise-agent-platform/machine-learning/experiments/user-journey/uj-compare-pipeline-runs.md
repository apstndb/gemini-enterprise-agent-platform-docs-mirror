---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/experiments/user-journey/uj-compare-pipeline-runs
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/experiments/user-journey/uj-compare-pipeline-runs
title: 'Compare pipeline runs: Notebook'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

As a data scientist, I have a training Pipeline which takes in a number of parameters, I want to compare runs of these Pipelines to each other.

You can view the pipeline runs associated with an experiment on the experiments page in the Google Cloud console.

![compare pipelines to each other](https://docs.cloud.google.com/static/gemini-enterprise-agent-platform/machine-learning/experiments/images/experiment-runs-list.png)

## Notebook: Log a pipeline job directly to an experiment

> To see an example of comparing pipeline runs in Vertex AI Experiments, run the "Compare pipeline runs with Experiments" notebook in one of the following environments:
> 
> [![](https://docs.cloud.google.com/static/vertex-ai/images/colab-logo-32px.png) Open in Colab](https://colab.research.google.com/github/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/experiments/comparing_pipeline_runs.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/colab-enterprise-logo-32px.png) Open in Colab Enterprise](https://console.cloud.google.com/vertex-ai/colab/import/https%3A%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Fexperiments%2Fcomparing_pipeline_runs.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/vertex-ai-workbench-logo-32px.png) Open in Vertex AI Workbench](https://console.cloud.google.com/vertex-ai/workbench/deploy-notebook?download_url=https%3A%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Fexperiments%2Fcomparing_pipeline_runs.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/github-logo-32px.png) View on GitHub](https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/experiments/comparing_pipeline_runs.ipynb)

In the "Compare pipeline runs with Vertex AI Experiments" notebook, you'll learn how to use Vertex AI Experiments to:

  - Log Pipeline Job.
  - Compare different Pipeline Jobs.

Steps involved:

  - Formalize a training component.
  - Build a training pipeline.
  - Run several Pipeline jobs and log their results.
  - Compare different Pipeline jobs.

## Relevant content

  - [Add pipeline run to experiment](https://docs.cloud.google.com/vertex-ai/docs/experiments/add-pipelinerun-experiment)
