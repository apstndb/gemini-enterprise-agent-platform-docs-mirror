---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tabular-data/tabular-workflows/forecasting
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tabular-data/tabular-workflows/forecasting
title: Tabular Workflow for Forecasting
description: Learn about the pipeline and components of Tabular Workflow for Forecasting .
data_source: docs.cloud.google.com
---

> **Preview**
> 
> This feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](https://docs.cloud.google.com/terms/service-terms#1) . Pre-GA features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

This document provides an overview of Tabular Workflow for Forecasting [pipeline and components](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tabular-data/tabular-workflows/forecasting#components) . To learn how to train a model, see [Train a model with Tabular Workflow for Forecasting](https://docs.cloud.google.com/vertex-ai/docs/tabular-data/tabular-workflows/forecasting-train) .

Tabular Workflow for Forecasting is the complete pipeline for forecasting tasks. It is similar to the [AutoML API](https://docs.cloud.google.com/vertex-ai/docs/tabular-data/forecasting/overview) , but lets you to choose what to control and what to automate. Instead of having controls for the *whole* pipeline, you have controls for *every step* in the pipeline. These pipeline controls include:

  - Data splitting
  - Feature engineering
  - Architecture search
  - Model training
  - Model ensembling

## Benefits

The following are some of the benefits of Tabular Workflow for Forecasting :

  - Supports **large datasets** that are up to 1TB in size and have up to 200 columns.
  - Lets you **improve stability and lower training time** by limiting the search space of architecture types or skipping architecture search.
  - Lets you **improve training speed** by manually selecting the hardware used for training and architecture search.
  - Lets you **reduce model size and improve latency** by changing the ensemble size.
  - Each component can be inspected in a powerful pipelines graph interface that lets you see the transformed data tables, evaluated model architectures and many more details.
  - Each component gets extended flexibility and transparency, such as being able to customize parameters, hardware, view process status, logs and more.

## Forecasting on Gemini Enterprise Agent Platform Pipelines

Tabular Workflow for Forecasting is a managed instance of Gemini Enterprise Agent Platform Pipelines.

[Gemini Enterprise Agent Platform Pipelines](https://docs.cloud.google.com/vertex-ai/docs/pipelines/introduction) is a serverless service that runs Kubeflow pipelines. You can use pipelines to automate and monitor your machine learning and data preparation tasks. Each step in a pipeline performs part of the pipeline's workflow. For example, a pipeline can include steps to split data, transform data types, and train a model. Since steps are instances of pipeline components, steps have inputs, outputs, and a container image. Step inputs can be set from the pipeline's inputs or they can depend on the output of other steps within this pipeline. These dependencies define the pipeline's workflow as a directed acyclic graph.

## Overview of pipeline and components

The following diagram shows the modeling pipeline for Tabular Workflow for Forecasting :

![Pipeline for Forecasting](https://docs.cloud.google.com/static/vertex-ai/docs/tabular-data/images/forecasting.svg)  

The pipeline components are:

1.  **training-configurator-and-validator** : Validates the training configuration and generates the training metadata.
    
    Input:
    
      - `instance_schema` : Instance schema in OpenAPI specification, which describes the data types of the inference data.
      - `dataset_stats` : Statistics that describe the raw dataset. For example, `dataset_stats` gives the number of rows in the dataset.
      - `training_schema` : Training data schema in OpenAPI specification, which describes the data types of the training data.

2.  **split-materialized-data** : Splits the materialized data into a training set, an evaluation set, and a test set.
    
    Input:
    
      - `materialized_data` : Materialized data.
    
    Output:
    
      - `materialized_train_split` : Materialized training split.
      - `materialized_eval_split` : Materialized evaluation split.
      - `materialized_test_split` : Materialized test set.

3.  **calculate-training-parameters-2** : Calculates the expected runtime duration for **automl-forecasting-stage-1-tuner** .

4.  **get-hyperparameter-tuning-results** - **Optional** : If you configure the pipeline to skip the architecture search, load the hyperparameter tuning results from a previous pipeline run.

5.  Perform model architecture search and tune hyperparameters ( **automl-forecasting-stage-1-tuner** ) or use the hyperparameter tuning results from a previous pipeline run ( **automl-forecasting-stage-2-tuner** ).
    
      - An architecture is defined by a set of hyperparameters.
      - Hyperparameters include the model type and the model parameters.
      - Model types considered are neural networks and boosted trees.
      - A model is trained for each architecture considered.
    
    Input:
    
      - `materialized_train_split` : Materialized training split.
      - `materialized_eval_split` : Materialized evaluation split.
      - `artifact` - Hyperparameter tuning results from a previous pipeline run. This artifact is an input only if you configure the pipeline to skip the architecture search.
    
    Output:
    
      - `tuning_result_output` : Tuning output.

6.  **get-prediction-image-uri-2** : Produces the correct inference image URI based on the [model type](https://docs.cloud.google.com/vertex-ai/docs/tabular-data/forecasting/train-model#training-methods) .

7.  **automl-forecasting-ensemble-2** : Ensembles the best architectures to produce a final model.
    
    Input:
    
      - `tuning_result_output` : Tuning output.
    
    Output:
    
      - `unmanaged_container_model` : Output model.

8.  **model-upload-2** - Uploads the model.
    
    Input:
    
      - `unmanaged_container_model` : Output model.
    
    Output:
    
      - `model` : Agent Platform model.

9.  **should\_run\_model\_evaluation** - **Optional** : Use the test set to calculate evaluation metrics.

## What's next

  - [Train a model using Tabular Workflow for Forecasting](https://docs.cloud.google.com/vertex-ai/docs/tabular-data/tabular-workflows/forecasting-train) .
