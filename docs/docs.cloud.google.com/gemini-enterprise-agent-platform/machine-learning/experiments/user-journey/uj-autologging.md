---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/experiments/user-journey/uj-autologging
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/experiments/user-journey/uj-autologging
title: 'Autologging: Notebook'
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

As part of the data science team, you want to try different modeling approaches during experimentation phase.To guarantee reproducibility, each approach has different parameters that you need to manually track. Google Cloud SDK for Python autologging, which is a one-line code SDK capability leveraging MLflow, provides automatic metrics and parameters tracking associated with your Vertex AI Experiments and experiment runs.

## Notebook: Vertex AI Experiments Autologging

> To see an example of autologging in Vertex AI Experiments, run the " Experiments: Autologging" notebook in one of the following environments:
> 
> [![](https://docs.cloud.google.com/static/vertex-ai/images/colab-logo-32px.png) Open in Colab](https://colab.research.google.com/github/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/experiments/get_started_with_vertex_experiments_autologging.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/colab-enterprise-logo-32px.png) Open in Colab Enterprise](https://console.cloud.google.com/vertex-ai/colab/import/https%3A%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Fexperiments%2Fget_started_with_vertex_experiments_autologging.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/vertex-ai-workbench-logo-32px.png) Open in Vertex AI Workbench](https://console.cloud.google.com/vertex-ai/workbench/deploy-notebook?download_url=https%3A%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Fexperiments%2Fget_started_with_vertex_experiments_autologging.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/github-logo-32px.png) View on GitHub](https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/experiments/get_started_with_vertex_experiments_autologging.ipynb)

In the "Vertex AI Experiments: Autologging" notebook, you'll learn how to use Vertex AI Experiments to:

  - Enable autologging in the Google Cloud SDK for Python.
  - Train scikit-learn model and see the resulting experiment run with metrics and parameters autologged to Vertex AI Experiments without setting an experiment run.
  - Train TensorFlow model, check autologged metrics and parameters to Vertex AI Experiments by manually setting an experiment run with `aiplatform.start_run()` and `aiplatform.end_run()` .
  - Disable autologging in the Google Cloud SDK for Python, train a PyTorch model and check that none of the parameters or metrics are logged.

## Relevant content

  - [Autolog data](https://docs.cloud.google.com/vertex-ai/docs/experiments/autolog-data#auto-created)
