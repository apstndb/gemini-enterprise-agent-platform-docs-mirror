---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tabular-data/forecasting/overview
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tabular-data/forecasting/overview
title: Forecasting with AutoML
description: Learn about the workflow for creating a forecast model and making predictions in Gemini Enterprise Agent Platform.
data_source: docs.cloud.google.com
---

> To see an example of how to create, train, and use an AutoML time-series forecasting model for batch prediction, run the " tabular forecasting model for batch prediction" notebook in one of the following environments:
> 
> [![](https://docs.cloud.google.com/static/vertex-ai/images/colab-logo-32px.png) Open in Colab](https://colab.research.google.com/github/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/automl/sdk_automl_tabular_forecasting_batch.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/colab-enterprise-logo-32px.png) Open in Colab Enterprise](https://console.cloud.google.com/agent-platform/colab/import/https%3A%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Fautoml%2Fsdk_automl_tabular_forecasting_batch.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/vertex-ai-workbench-logo-32px.png) Open in Agent Platform Workbench](https://console.cloud.google.com/agent-platform/workbench/deploy-notebook?download_url=https%3A%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Fautoml%2Fsdk_automl_tabular_forecasting_batch.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/github-logo-32px.png) View on GitHub](https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/automl/sdk_automl_tabular_forecasting_batch.ipynb)

[Video](https://www.youtube.com/watch?v=5-qjRpjdE5s)

**Forecasting** models predict a sequence of values. For example, as a retailer, you might want to forecast daily demand of your products for the next 3 months so that you can appropriately stock product inventories in advance.

## Workflow for creating a forecast model and making inferences

The process for creating a forecast model in Agent Platform is as follows:

| Steps                                                                                                                                                                          | Description                                                                    |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------ |
| 1\. [Prepare tabular training data for forecast models](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tabular-data/forecasting/prepare-data) | Prepare your tabular training data for forecast model training.                |
| 2\. [Create a dataset for training forecast models](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tabular-data/forecasting/create-dataset)   | Create a new dataset and associate your prepared training data with it.        |
| 3\. [Train a forecast model](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tabular-data/forecasting/train-model)                             | Train a forecast model in Gemini Enterprise Agent Platform using your dataset. |
| 4\. [Evaluate your model](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tabular-data/forecasting/evaluate-model)                             | Evaluate your newly trained forecast model for inference accuracy.             |
| 5\. [Get inferences for a forecast model](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tabular-data/forecasting/get-predictions)            | Request batch inferences from your forecast model.                             |

Forecasting with AutoML doesn't support online inferences. If you want to request online inferences from your forecast model, use [Tabular Workflow for Forecasting](https://docs.cloud.google.com/vertex-ai/docs/tabular-data/tabular-workflows/forecasting) .
