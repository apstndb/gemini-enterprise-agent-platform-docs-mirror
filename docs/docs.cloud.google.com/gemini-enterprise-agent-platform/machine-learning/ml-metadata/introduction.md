---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/ml-metadata/introduction
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/ml-metadata/introduction
title: Introduction to Gemini Enterprise Agent Platform ML Metadata
description: Introduction to Gemini Enterprise Agent Platform ML Metadata
data_source: docs.cloud.google.com
---

A critical part of the scientific method is recording both your observations and the parameters of an experiment. In data science, it's also critical to track the parameters, artifacts, and metrics used in a machine learning (ML) experiment. This metadata helps you:

  - Analyze runs of a production ML system to understand changes in the quality of predictions.
  - Analyze ML experiments to compare the effectiveness of different sets of hyperparameters.
  - Track the lineage of ML artifacts, for example datasets and models, to understand just what contributed to the creation of an artifact or how that artifact was used to create descendant artifacts.
  - Rerun an ML workflow with the same artifacts and parameters.
  - Track the downstream usage of ML artifacts for governance purposes.

Agent Platform ML Metadata lets you record the metadata and artifacts produced by your ML system and query that metadata to help analyze, debug, and audit the performance of your ML system or the artifacts that it produces.

Agent Platform ML Metadata builds on the concepts used in the open source [ML Metadata (MLMD)](https://www.tensorflow.org/tfx/guide/mlmd) library that was developed by Google's TensorFlow Extended team.

## Overview of Agent Platform ML Metadata

Agent Platform ML Metadata captures your ML system's metadata as a graph.

In the metadata graph, artifacts and executions are nodes, and events are edges that link artifacts as inputs or outputs of executions. Contexts represent subgraphs that are used to logically group sets of artifacts and executions.

You can apply key-value pair metadata to artifacts, executions, and contexts. For example, a model could have metadata that describes the framework used to train the model and performance metrics, such as the model's accuracy, precision, and recall.

Learn more about [tracking your ML system's metadata](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/ml-metadata/tracking) . If you're interested in analyzing metadata from Agent Platform Pipelines, check out [this step-by-step tutorial](https://codelabs.developers.google.com/vertex-mlmd-pipelines#0) .

## ML artifact lineage

In order to understand changes in the performance of your machine ML system, you must be able to analyze the metadata produced by your ML workflow and the lineage of its artifacts. An artifact's lineage includes all the factors that contributed to its creation, as well as artifacts and metadata that descend from this artifact.

For example, a model's lineage could include the following:

  - The training, test, and evaluation data used to create the model.
  - The hyperparameters used during model training.
  - The code that was used to train the model.
  - Metadata recorded from the training and evaluation process, such as the model's accuracy.
  - Artifacts that descend from this model, such as the results of batch predictions.

By tracking your ML system's metadata using Agent Platform ML Metadata, you can answer questions like the following:

  - Which dataset was used to train a certain model?
  - Which of my organization's models have been trained using a certain dataset?
  - Which run produced the most accurate model, and what hyperparameters were used to train the model?
  - Which deployment targets was a certain model deployed to and when was it deployed?
  - Which version of your model was used to create a prediction at a given point in time?

Learn more about [analyzing your ML system's metadata](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/ml-metadata/analyzing) .
