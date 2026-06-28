---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/python-sdk/python-sdk-class-overview
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/python-sdk/python-sdk-class-overview
title: Vertex AI SDK class overview
description: Learn about using the Vertex AI SDK to build, train, and deploy custom machine learning models and create generative AI solutions.
data_source: docs.cloud.google.com
---

Data scientists and machine learning (ML) developers use the Agent Platform SDK for Python to build, train, and deploy models in a custom ML workflow. This includes creating datasets and uploading data, training an ML model, uploading and storing your model, deploying your model, running batch prediction jobs, and managing your models and endpoints.

The Vertex AI SDK also includes classes to create generative AI solutions with text, code, chat, and text embedding foundation models. You can use these classes to generate text, create a text or code chatbot, tune a foundation model, and create a text embedding. A text embedding is text in the form of a vector used to search for items. For more information, see [Introduction to language model classes in the Vertex AI SDK](https://docs.cloud.google.com/vertex-ai/generative-ai/docs/sdk-for-llm/llm-sdk-overview) .

You can use the Agent Platform SDK for Python in hosted JupyterLab notebooks within Gemini Enterprise Agent Platform to write and run your code. The notebooks include preinstalled ML frameworks, such as TensorFlow and PyTorch. You can also use other notebooks, such as Colab notebooks, or use a developer environment of your choice that supports Python.

If you want to try using the Agent Platform SDK for Python right now, see the following resources:

  - [Introduction to the Agent Platform SDK for Python](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/python-sdk/use-vertex-ai-python-sdk)
  - [Vertex AI SDK reference](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform)
  - [Vertex AI SDK language model reference](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/vertexai.language_models)
  - [Train a model using Gemini Enterprise Agent Platform and the Python SDK](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tutorials/tabular-bq-prediction)

The Vertex AI SDK includes many classes to help you automate data ingestion, train models, and get predictions. It also includes classes to help you monitor, evaluate, and optimize your machine learning (ML) workflow. The classes can be loosely grouped into the following categories:

  - [Data classes](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/python-sdk/data-classes) include classes that work with structured data, unstructured data, and the Vertex AI Feature Store.
  - [Training classes](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/python-sdk/training-classes) include classes that work with AutoML training for structured and unstructured data, custom training, hyperparameter training, and pipeline training.
  - [Model classes](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/python-sdk/model-classes) work with models and model evaluations.
  - [Prediction classes](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/python-sdk/prediction-classes) work with batch predictions, online predictions, and Vector Search predictions.
  - [Tracking classes](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/python-sdk/tracking-classes) work with Vertex ML Metadata, Vertex AI Experiments, and Vertex AI TensorBoard.
