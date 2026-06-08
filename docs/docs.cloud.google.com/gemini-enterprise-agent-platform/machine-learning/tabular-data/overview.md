---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tabular-data/overview
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tabular-data/overview
title: Tabular data overview
description: Learn how to perform machine learning (ML) with tabular data in Gemini Enterprise Agent Platform.
data_source: docs.cloud.google.com
---

Agent Platform lets you perform machine learning with tabular data using low-complexity processes and interfaces. You can create the following model types for your tabular data problems:

  - **Binary classification** models predict a binary outcome (one of two classes). Use this model type for yes or no questions. For example, you might want to build a binary classification model to predict whether a customer would buy a subscription. Generally, a binary classification problem requires less data than other model types.
  - **Multi-class classification** models predict one class from three or more discrete classes. Use this model type for categorization. For example, as a retailer, you might want to build a multi-class classification model to segment customers into different personas.
  - **Regression** models predict a continuous value. For example, as a retailer, you might want to build a regression model to predict how much a customer will spend next month.
  - **Forecasting** models predict a sequence of values. For example, as a retailer, you might want to forecast daily demand of your products for the next 3 months so that you can appropriately stock product inventories in advance.

For an introduction to machine learning with tabular data, see [Introduction to Tabular Data](https://docs.cloud.google.com/vertex-ai/docs/tabular-data/tabular101) . For further information about Agent Platform solutions, see [Agent Platform solutions for classification and regression](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tabular-data/overview#classification-regression) and [Agent Platform solutions for forecasting](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tabular-data/overview#forecasting) .

## A note about fairness

Google commits to making progress in following [responsible AI practices](https://ai.google/responsibilities/responsible-ai-practices/) . To this end, our ML products, including AutoML, are designed around core principles such as fairness and [human-centered machine learning](https://medium.com/google-design/human-centered-machine-learning-a770d10562cd) .

## Agent Platform solutions for classification and regression

Agent Platform offers the following solutions for classification and regression:

  - [Tabular Workflow for End-to-End AutoML](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tabular-data/overview#workflow-automl)
  - [Classification and regression with AutoML](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tabular-data/overview#cr-automl)

### Tabular Workflow for End-to-End AutoML

Tabular Workflow for End-to-End AutoML is a complete AutoML pipeline for classification and regression tasks. It is similar to the [AutoML API](https://docs.cloud.google.com/vertex-ai/docs/tabular-data/classification-regression/overview) , but allows you to choose what to control and what to automate. Instead of having controls for the *whole* pipeline, you have controls for *every step* in the pipeline. These pipeline controls include:

  - Data splitting
  - Feature engineering
  - Architecture search
  - Model training
  - Model ensembling
  - Model distillation

#### Benefits

  - Supports **large datasets** that are multiple TB in size and have up to 1000 columns.
  - Allows you to **improve stability and lower training time** by limiting the search space of architecture types or skipping architecture search.
  - Allows you to **improve training speed** by manually selecting the hardware used for training and architecture search.
  - Allows you to **reduce model size and improve latency** with distillation or by changing the ensemble size.
  - Each AutoML component can be inspected in a powerful pipelines graph interface that lets you see the transformed data tables, evaluated model architectures, and many more details.
  - Each AutoML component gets extended flexibility and transparency, such as being able to customize parameters, hardware, view process status, logs, and more.

To learn more about Tabular Workflows, see [Tabular Workflows on Agent Platform](https://docs.cloud.google.com/vertex-ai/docs/tabular-data/tabular-workflows/overview) . To learn more about Tabular Workflow for End-to-End AutoML, see [Tabular Workflow for End-to-End AutoML](https://docs.cloud.google.com/vertex-ai/docs/tabular-data/tabular-workflows/e2e-automl) .

### Classification and regression with AutoML

Agent Platform offers integrated, fully managed pipelines for end-to-end classification or regression tasks. Agent Platform searches for the optimal set of hyperparameters, trains multiple models with multiple sets of hyperparameters, and then creates a single, final model from an ensemble of the top models. Agent Platform considers [neural networks](https://developers.google.com/machine-learning/glossary#neural_network) and boosted trees for the model types.

#### Benefits

  - Agent Platform chooses the model type, model parameters, and hardware for you.

For further information, see [Classification and Regression Overview](https://docs.cloud.google.com/vertex-ai/docs/tabular-data/classification-regression/overview) .

## Agent Platform solutions for forecasting

Agent Platform offers the following solutions for forecasting:

  - [Tabular Workflow for Forecasting](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tabular-data/overview#workflow-forecasting)
  - [Forecasting with AutoML](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tabular-data/overview#f-automl)
  - [Forecasting with BigQuery ML ARIMA\_PLUS](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tabular-data/overview#arima)
  - [Forecasting with Prophet](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tabular-data/overview#prophet)

### Tabular Workflow for Forecasting

> **Preview**
> 
> This feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](https://docs.cloud.google.com/terms/service-terms#1) . Pre-GA features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

Tabular Workflow for Forecasting is the complete pipeline for forecasting tasks. It is similar to the [AutoML API](https://docs.cloud.google.com/vertex-ai/docs/tabular-data/forecasting/overview) , but lets you to choose what to control and what to automate. Instead of having controls for the *whole* pipeline, you have controls for *every step* in the pipeline. These pipeline controls include:

  - Data splitting
  - Feature engineering
  - Architecture search
  - Model training
  - Model ensembling

#### Benefits

  - Supports **large datasets** that are up to 1TB in size and have up to 200 columns.
  - Lets you **improve stability and lower training time** by limiting the search space of architecture types or skipping architecture search.
  - Lets you **improve training speed** by manually selecting the hardware used for training and architecture search.
  - Lets you **reduce model size and improve latency** by changing the ensemble size.
  - Each component can be inspected in a powerful pipelines graph interface that lets you see the transformed data tables, evaluated model architectures and many more details.
  - Each component gets extended flexibility and transparency, such as being able to customize parameters, hardware, view process status, logs and more.

To learn more about Tabular Workflows, see [Tabular Workflows on Agent Platform](https://docs.cloud.google.com/vertex-ai/docs/tabular-data/tabular-workflows/overview) . To learn more about Tabular Workflow for Forecasting, see [Tabular Workflow for Forecasting](https://docs.cloud.google.com/vertex-ai/docs/tabular-data/tabular-workflows/forecasting) .

### Forecasting with AutoML

Agent Platform offers an integrated, fully managed pipeline for end-to-end forecasting tasks. Agent Platform searches for the optimal set of hyperparameters, trains multiple models with multiple sets of hyperparameters, and then creates a single, final model from an ensemble of the top models. You can choose between [Time series Dense Encoder (TiDE)](https://arxiv.org/abs/2304.08424) , [Temporal Fusion Transformer (TFT)](https://ai.googleblog.com/2021/12/interpretable-deep-learning-for-time.html) , [AutoML (L2L)](https://ai.googleblog.com/2020/12/using-automl-for-time-series-forecasting.html) , and Seq2Seq+ for your model training method. Agent Platform considers only [neural networks](https://developers.google.com/machine-learning/glossary#neural_network) for the model type.

#### Benefits

  - Agent Platform chooses model parameters and hardware for you.

For further information, see [Forecasting Overview](https://docs.cloud.google.com/vertex-ai/docs/tabular-data/forecasting/overview) .

### Forecasting with BigQuery ML ARIMA\_PLUS

[BigQuery ML ARIMA\_PLUS](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-time-series) is a univariate forecasting model. As a statistical model, it is faster to train than a [model based on neural networks](https://docs.cloud.google.com/vertex-ai/docs/tabular-data/forecasting/overview) . We recommend training a BigQuery ML ARIMA\_PLUS model if you need to perform many quick iterations of model training or if you need an inexpensive baseline to measure other models against.

Like [Prophet](https://docs.cloud.google.com/vertex-ai/docs/tabular-data/forecasting-prophet) , BigQuery ML ARIMA\_PLUS attempts to decompose each time series into trends, seasons, and holidays, producing a forecast using the aggregation of these models' inferences. One of the many differences, however, is that BQML ARIMA+ uses ARIMA to model the trend component, while Prophet attempts to fit a curve using a piecewise logistic or linear model.

Google Cloud offers a pipeline for training a BigQuery ML ARIMA\_PLUS model and a pipeline for getting batch inferences from a BigQuery ML ARIMA\_PLUS model. Both pipelines are instances of [Gemini Enterprise Agent Platform Pipelines](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/pipelines/introduction) from [Google Cloud Pipeline Components](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/pipelines/components-introduction) (GCPC).

#### Benefits

  - BigQuery chooses model parameters and hardware for you.
  - Model training provides a low-cost baseline to compare other models against.

For further information, see [Forecasting with ARIMA+](https://docs.cloud.google.com/vertex-ai/docs/tabular-data/forecasting-arima/overview) .

### Forecasting with Prophet

Prophet is a forecasting model maintained by Meta. See the [Prophet paper](https://peerj.com/preprints/3190/) for algorithm details and the [documentation](https://facebook.github.io/prophet/docs/quick_start.html) for more information about the library.

Like [BigQuery ML ARIMA\_PLUS](https://docs.cloud.google.com/vertex-ai/docs/tabular-data/forecasting-arima/overview) , Prophet attempts to decompose each time series into trends, seasons, and holidays, producing a forecast using the aggregation of these models' inferences. An important difference, however, is that BQML ARIMA+ uses ARIMA to model the trend component, while Prophet attempts to fit a curve using a piecewise logistic or linear model.

Google Cloud offers a pipeline for training a Prophet model and a pipeline for getting batch inferences from a Prophet model. Both pipelines are instances of [Gemini Enterprise Agent Platform Pipelines](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/pipelines/introduction) from [Google Cloud Pipeline Components](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/pipelines/components-introduction) (GCPC).

Integration of Prophet with Agent Platform means that you can do the following:

  - Use Agent Platform [data splitting](https://docs.cloud.google.com/vertex-ai/docs/tabular-data/forecasting/prepare-data#split) and [windowing strategies](https://docs.cloud.google.com/vertex-ai/docs/tabular-data/forecasting/train-model#forecast-window) .
  - Read data from either BigQuery tables or CSVs stored in Cloud Storage. Agent Platform expects each row to have the same format as [Agent Platform Forecasting](https://docs.cloud.google.com/vertex-ai/docs/tabular-data/forecasting/prepare-data) .

Although Prophet is a multivariate model, Agent Platform supports only a univariate version of it.

#### Benefits

  - You can improve training speed by selecting the hardware used for training.

For further information, see [Forecasting with Prophet](https://docs.cloud.google.com/vertex-ai/docs/tabular-data/forecasting-prophet) .

## What's next

  - Learn about [machine learning with tabular data](https://docs.cloud.google.com/vertex-ai/docs/tabular-data/tabular101) .
  - Learn about [classification and regression with AutoML](https://docs.cloud.google.com/vertex-ai/docs/tabular-data/classification-regression/overview) .
  - Learn about [forecasting with AutoML](https://docs.cloud.google.com/vertex-ai/docs/tabular-data/forecasting/overview) .
  - Learn about [forecasting with Prophet](https://docs.cloud.google.com/vertex-ai/docs/tabular-data/forecasting-prophet) .
  - Learn about [forecasting with BigQuery ML ARIMA\_PLUS](https://docs.cloud.google.com/vertex-ai/docs/tabular-data/forecasting-arima/overview) .
  - Learn about [Tabular Workflows](https://docs.cloud.google.com/vertex-ai/docs/tabular-data/tabular-workflows/overview) .
