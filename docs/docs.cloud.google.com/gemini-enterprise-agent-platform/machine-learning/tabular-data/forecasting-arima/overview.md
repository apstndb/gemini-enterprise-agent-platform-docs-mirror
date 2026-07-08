---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tabular-data/forecasting-arima/overview
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tabular-data/forecasting-arima/overview
title: Forecasting with ARIMA+
description: Learn about using BigQuery ML ARIMA_PLUS in Gemini Enterprise Agent Platform.
data_source: docs.cloud.google.com
---

> To see an example of how to train a model with ARIMA+, run the "Train a BigQuery ML ARIMA\_PLUS model using Agent Platform tabular workflows" notebook in one of the following environments:
> 
> [![](https://docs.cloud.google.com/static/vertex-ai/images/colab-logo-32px.png) Open in Colab](https://colab.research.google.com/github/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/tabular_workflows/bqml_arima_plus.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/colab-enterprise-logo-32px.png) Open in Colab Enterprise](https://console.cloud.google.com/agent-platform/colab/import/https%3A%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Ftabular_workflows%2Fbqml_arima_plus.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/vertex-ai-workbench-logo-32px.png) Open in Agent Platform Workbench](https://console.cloud.google.com/agent-platform/workbench/deploy-notebook?download_url=https%3A%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Ftabular_workflows%2Fbqml_arima_plus.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/github-logo-32px.png) View on GitHub](https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/tabular_workflows/bqml_arima_plus.ipynb)

[BigQuery ML ARIMA\_PLUS](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-time-series) is a univariate forecasting model. As a statistical model, it is faster to train than a [model based on neural networks](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tabular-data/forecasting/overview) . We recommend training a BigQuery ML ARIMA\_PLUS model if you need to perform many quick iterations of model training or if you need an inexpensive baseline to measure other models against.

Like [Prophet](https://docs.cloud.google.com/gemini-enterprise-agent-platform/tabular-data/forecasting-prophet) , BigQuery ML ARIMA\_PLUS attempts to decompose each time series into trends, seasons, and holidays, producing a forecast using the aggregation of these models' inferences. One of the many differences, however, is that BQML ARIMA+ uses ARIMA to model the trend component, while Prophet attempts to fit a curve using a piecewise logistic or linear model.

Google Cloud offers a pipeline for training a BigQuery ML ARIMA\_PLUS model and a pipeline for getting batch inferences from a BigQuery ML ARIMA\_PLUS model. Both pipelines are instances of [Gemini Enterprise Agent Platform Pipelines](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/pipelines/introduction) from [Google Cloud Pipeline Components](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/pipelines/components-introduction) (GCPC).

## What's next

  - Learn more about [BigQuery ML ARIMA\_PLUS](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-time-series) .
  - Learn about [the service accounts used by this workflow](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tabular-data/tabular-workflows/service-accounts#arima) .
