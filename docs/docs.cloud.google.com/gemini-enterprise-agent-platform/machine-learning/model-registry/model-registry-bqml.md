---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/model-registry/model-registry-bqml
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/model-registry/model-registry-bqml
title: BigQuery ML and Model Registry
description: By registering BigQuery ML models in the Model Registry, you can manage them alongside other ML models, easily version, evaluate, and deploy them for online inference within a unified platform.
data_source: docs.cloud.google.com
---

[Video](https://www.youtube.com/watch?v=AVwwkqLOito)

[BigQuery ML](https://docs.cloud.google.com/bigquery/docs/bqml-introduction) is a Google Cloud service that lets you create and execute machine learning models in BigQuery ML by using standard SQL queries. With Gemini Enterprise Agent Platform, you can use pre-trained and custom tooling within a unified platform. After you register your BigQuery ML models in the Model Registry, you can manage them with your other ML models for versioning, evaluation, and deployment.

With this integration, you can choose which BigQuery ML models to register to the Model Registry. After you've registered your BigQuery ML models, you can deploy your BigQuery ML model to an endpoint for online inference.

To learn how to integrate your BigQuery ML models with Gemini Enterprise Agent Platform Model Registry, see [Manage BigQuery ML models in Gemini Enterprise Agent Platform](https://docs.cloud.google.com/bigquery/docs/managing-models-vertex) .

## Limitations

  - You can't register [remote models](https://docs.cloud.google.com/bigquery/docs/bqml-introduction#remote_models) .

  - The following models can be registered in Model Registry, but they can't be deployed in Agent Platform:
    
      - [Imported XGBoost models](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-xgboost)
      - [`ARIMA_PLUS` models](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-time-series)
      - [`ARIMA_PLUS_XREG` models](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-multivariate-time-series)
