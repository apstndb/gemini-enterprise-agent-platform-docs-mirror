---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/experiments/user-journey/uj-custom-training-autologging
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/experiments/user-journey/uj-custom-training-autologging
title: 'Custom training autologging: Notebook'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

As a data scientist experimenting with large models, you need a way to run experiments on a scalable training service to log parameters and metrics. This enables reproducibility.

With Gemini Enterprise Agent Platform training and experiments autologging integration, you can run your ML experiments at scale and autolog their parameters and metrics by using the `enable_autolog` argument.

## Notebook: Vertex AI Experiments: Custom training autologging - Local script

> To see an example of getting started with custom autologging with a local script, run the " Experiments: Autologging" notebook in one of the following environments:
> 
> [![](https://docs.cloud.google.com/static/vertex-ai/images/colab-logo-32px.png) Open in Colab](https://colab.research.google.com/github/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/experiments/get_started_with_custom_training_autologging_local_script.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/colab-enterprise-logo-32px.png) Open in Colab Enterprise](https://console.cloud.google.com/vertex-ai/colab/import/https%3A%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Fexperiments%2Fget_started_with_custom_training_autologging_local_script.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/vertex-ai-workbench-logo-32px.png) Open in Agent Platform Workbench](https://console.cloud.google.com/vertex-ai/workbench/deploy-notebook?download_url=https%3A%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Fexperiments%2Fget_started_with_custom_training_autologging_local_script.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/github-logo-32px.png) View on GitHub](https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/experiments/get_started_with_custom_training_autologging_local_script.ipynb)

This tutorial uses the following Google Cloud ML services and resources:

  - Vertex AI Experiments
  - Gemini Enterprise Agent Platform training

The steps performed include:

1.  Formalize model experiment in a script.
2.  Run model training using local script on Gemini Enterprise Agent Platform training.
3.  Check out ML experiment parameters and metrics in Vertex AI Experiments.

## Relevant content

  - [Run training job with experiment tracking](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/experiments/run-training-job-experiments)
