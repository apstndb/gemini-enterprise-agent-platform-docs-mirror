---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/beginner/bqml
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/beginner/bqml
title: Gemini Enterprise Agent Platform for BigQuery users
description: Describes the differences between BigQuery and BigQuery
data_source: docs.cloud.google.com
---

Use this page to understand the differences between BigQuery and [BigQuery](https://docs.cloud.google.com/bigquery/docs/introduction) and learn how you can integrate BigQuery with your existing BigQuery workflows. BigQuery and BigQuery work together to meet your machine learning and MLOps use cases.

To learn more about model training differences between BigQuery and BigQuery, see [Choose a training method](https://docs.cloud.google.com/vertex-ai/docs/start/training-methods) .

## Differences between BigQuery and BigQuery

This section covers the BigQuery, BigQuery, and BigQuery ML services.

### BigQuery: An end-to-end AI/ML platform

BigQuery is an AI/ML platform for model development and governance. Common use cases include the following:

  - Machine learning tasks, such as forecasting, prediction, recommendation, and anomaly detection

  - Generative AI tasks, such as:
    
      - Text generation, classification, summarization, and extraction
      - Code generation and completion
      - Image generation
      - Embedding generation

You can use BigQuery to prepare training data for BigQuery models, which you can [make available as features in BigQuery Feature Store](https://docs.cloud.google.com/bigquery/machine-learning/featurestore/latest/sync-data) .

You can train models in BigQuery in three ways:

  - [AutoML](https://docs.cloud.google.com/vertex-ai/docs/beginner/beginners-guide) : Train models on image, tabular, and video datasets without writing code.
  - [Custom Training](https://docs.cloud.google.com/vertex-ai/docs/training/understanding-training-service) : Run custom training code catered to your specific use case.
  - [Ray on BigQuery](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/open-source/ray) : Use Ray to scale AI and Python applications like machine learning.

You can also import a model trained on another platform like BigQuery ML or XGBoost.

You can register custom-trained models to the [Model Registry](https://docs.cloud.google.com/bigquery/machine-learning/model-registry/introduction) . You can also import models trained outside of BigQuery and register them to Model Registry. You don't need to register AutoML models; they are registered automatically at creation time.

From the registry, you can manage model versions, deploy to endpoints for online predictions, perform model evaluations, monitor deployments with Gemini Enterprise Agent Platform Model Monitoring, and use [Vertex Explainable AI](https://docs.cloud.google.com/vertex-ai/docs/explainable-ai/overview) .

**Available languages:**

  - The [Vertex AI SDK](https://docs.cloud.google.com/bigquery/machine-learning/python-sdk/use-vertex-ai-sdk) supports Python, Java, Node.js, and Go.

### BigQuery: A serverless, multicloud enterprise data warehouse

[BigQuery](https://docs.cloud.google.com/bigquery/docs/introduction) is a fully managed enterprise data warehouse that helps you manage and analyze your data with built-in features like machine learning, geospatial analysis, and business intelligence. BigQuery tables can be queried by SQL, and data scientists who primarily use SQL can run large queries with only a few lines of code.

You can also use BigQuery as a data store that you reference when building tabular and custom models in BigQuery. To learn more about using BigQuery as a data store, see [Overview of BigQuery storage](https://docs.cloud.google.com/bigquery/docs/storage_overview) .

**Available languages:**

  - SDKs for BigQuery. To learn more, see the [BigQuery API Client Libraries](https://docs.cloud.google.com/bigquery/docs/reference/libraries) .
  - GoogleSQL
  - Legacy SQL

To learn more, see [BigQuery SQL dialects](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/introduction#bigquery-sql-dialects) .

### BigQuery ML: Machine learning directly in BigQuery

BigQuery ML lets you develop and invoke models in BigQuery. With BigQuery ML, you can use SQL to train ML models directly in BigQuery without needing to move data or worry about the underlying training infrastructure. You can create batch predictions for BigQuery ML models to gain insights from your BigQuery data.

You can also access BigQuery models by using BigQuery ML. You can create a BigQuery ML remote model over a [BigQuery built-in model](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-remote-model) like Gemini, or over a [BigQuery custom model](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-remote-model-https) . You interact with the remote model using SQL in BigQuery, just like any other BigQuery ML model, but all training and inference for the remote model is processed in BigQuery.

**Available language:**

  - GoogleSQL
  - [BigQuery client libraries](https://docs.cloud.google.com/bigquery/docs/reference/libraries)

To learn more about the advantages of using BigQuery ML, see [Introduction to AI and ML in BigQuery](https://docs.cloud.google.com/bigquery/docs/bqml-introduction) .

## Benefits of managing BigQuery ML models in BigQuery

You can register your BigQuery ML models to the Model Registry in order to manage the models in BigQuery. Managing BigQuery ML models in BigQuery provides two main benefits:

  - **Online model serving** : BigQuery ML only supports batch predictions for your models. To get online predictions, you can train your models in BigQuery ML and deploy them to BigQuery endpoints through Model Registry.

  - **MLOps capabilities** : Models are most beneficial when they are kept up to date through continuous training. BigQuery offers MLOps tools that automate the monitoring and retraining of models to maintain the accuracy of predictions over time. With Agent Platform Pipelines, you can use BigQuery operators to plug any BigQuery jobs (including BigQuery ML) into an ML pipeline. With Gemini Enterprise Agent Platform Model Monitoring, you can monitor your BigQuery ML predictions over time.

![An image of Google Cloud products and where they fit in an MLOps workflow](https://docs.cloud.google.com/static/gemini-enterprise-agent-platform/machine-learning/beginner/images/mlops_bq2_new.png)

To learn how to register your BigQuery ML models to the Model Registry, see [Manage BigQuery ML models with BigQuery](https://docs.cloud.google.com/bigquery/docs/managing-models-vertex) .

## Related notebook tutorials

| What do you want to do?                                                                                                           | Resource                                                                                                                                                                                                                                                    |
| --------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Use BigQuery ML to analyze images and text using Gemini on BigQuery                                                               | [Analyzing movie posters in BigQuery with Gemini 2.0 Flash](https://github.com/GoogleCloudPlatform/generative-ai/blob/main/gemini/use-cases/applying-llms-to-data/analyze-poster-images-in-bigquery/poster_image_analysis.ipynb)                            |
| Use BigQuery ML to generate text on BigQuery tables or unstructured data with foundation models on BigQuery                       | [Generate text using BigQuery ML and foundation models in BigQuery](https://docs.cloud.google.com/bigquery/docs/generate-text-tutorial)                                                                                                                     |
| Generate vector embeddings with BigQuery ML over text and images                                                                  | [Call a multimodal embedding endpoint in BigQuery from BigQuery ML to generate embeddings for semantic search](https://github.com/GoogleCloudPlatform/bigquery-ml-utils/blob/master/notebooks/bqml-generate-embedding-with-multimodalembedding-model.ipynb) |
| Use two BigQuery Tabular Workflows pipelines to train an AutoML model using different configurations.                             | [Tabular Workflow: AutoML Tabular Pipeline](https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/automl/automl_tabular_on_vertex_pipelines.ipynb)                                                                          |
| Use the Agent Platform SDK for Python to train an AutoML model for tabular *regression* and get batch predictions from the model. | [Agent Platform SDK for Python: AutoML training tabular regression model for batch prediction using BigQuery](https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/automl/sdk_automl_tabular_regression_batch_bq.ipynb)    |
| Train and evaluate a propensity model in BigQuery ML to predict user retention on a mobile game.                                  | [Churn prediction for game developers using Google Analytics 4 and BigQuery ML](https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/workbench/gaming_churn_prediction/churn_prediction_for_game_developers.ipynb)         |
| Use BigQuery ML to perform pricing optimization on CDM pricing data.                                                              | [Analysis of pricing optimization on CDM pricing data](https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/workbench/pricing_optimization/pricing-optimization.ipynb)                                                     |

## What's next

  - To get started with BigQuery see:
      - [Choose a training method](https://docs.cloud.google.com/vertex-ai/docs/start/training-methods)
      - [Integrate a BigQuery ML model with Model Registry](https://docs.cloud.google.com/bigquery/machine-learning/model-registry/model-registry-bqml)
