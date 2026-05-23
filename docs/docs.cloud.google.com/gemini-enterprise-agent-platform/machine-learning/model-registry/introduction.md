---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/model-registry/introduction
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/model-registry/introduction
title: Introduction to Model Registry
description: Gemini Enterprise Agent Platform Model Registry is a central repository for managing the lifecycle of ML models, supporting custom models, AutoML data types, and BigQuery ML models, offering a streamlined interface to organize, track, train, and deploy models to production.
data_source: docs.cloud.google.com
---

> To see an example of getting started with Model Registry, run the "Get started with " notebook in one of the following environments:
> 
> [![](https://docs.cloud.google.com/static/vertex-ai/images/colab-logo-32px.png) Open in Colab](https://colab.research.google.com/github/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/model_registry/get_started_with_model_registry.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/colab-enterprise-logo-32px.png) Open in Colab Enterprise](https://console.cloud.google.com/agent-platform/colab/import/https%3A%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Fmodel_registry%2Fget_started_with_model_registry.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/vertex-ai-workbench-logo-32px.png) Open in Agent Platform Workbench](https://console.cloud.google.com/agent-platform/workbench/deploy-notebook?download_url=https%3A%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Fmodel_registry%2Fget_started_with_model_registry.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/github-logo-32px.png) View on GitHub](https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/model_registry/get_started_with_model_registry.ipynb)

The Gemini Enterprise Agent Platform Model Registry is a central repository where you can manage the lifecycle of your ML models. From the Model Registry, you have an overview of your models so you can better organize, track, and train new versions. When you have a model version you would like to deploy, you can assign it to an endpoint directly from the registry, or using aliases, deploy models to an endpoint.

The Model Registry supports custom models and all AutoML data types - tabular and image. The Model Registry can also support BigQuery ML models. If you have models trained in BigQuery ML, you can register them with the Model Registry without needing to export them from BigQuery ML or import them into the Model Registry.

From the model version details page you can evaluate, deploy to an endpoint, set up batch inference, and view specific model details. The Model Registry provides a straightforward and streamlined interface to manage and deploy your best models to production.

## Common workflow

There are many valid workflows for working in the Model Registry. To get started, you might want to follow these guidelines to understand what you can do in the Model Registry and at what stage in your model-training journey.

  - Import models to the Model Registry.
  - Create new models, assign a model version the default alias, ready for production.
  - Add other aliases, or labels to help you manage and organize your models and model versions.
  - Deploy your models to an endpoint for online inference.
  - Run batch inference, and start your model evaluation pipeline.
  - View your model details and view performance metrics from the model details page.

To learn more about how to integrate your BigQuery ML models with Gemini Enterprise Agent Platform, see the [BigQuery ML documentation.](https://docs.cloud.google.com/bigquery-ml/docs/managing-models-vertex)

## Search and discover models using Knowledge Catalog

Knowledge Catalog is a platform for storing, managing, and accessing your metadata. Knowledge Catalog provides a way to search for your Agent Platform models across projects and regions.

For more information, see [About data catalog management in Knowledge Catalog](https://docs.cloud.google.com/dataplex/docs/catalog-overview) .

## What's next

To get started using Model Registry, see:

  - [Import models to Agent Platform](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/model-registry/import-model)
  - [Model versioning with Model Registry](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/model-registry/versioning)
  - [How to use model version aliases](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/model-registry/model-alias)
  - [BigQuery ML and Model Registry](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/model-registry/model-registry-bqml)
  - [Copy a model in Model Registry](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/model-registry/copy-model)
