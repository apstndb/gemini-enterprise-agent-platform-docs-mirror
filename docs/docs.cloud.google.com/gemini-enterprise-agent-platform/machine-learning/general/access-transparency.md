---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/access-transparency
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/access-transparency
title: Access Transparency in Agent Platform
description: Learn about Access Transparency for Gemini Enterprise Agent Platform.
data_source: docs.cloud.google.com
---

This page provides an overview of the support [Access Transparency](https://docs.cloud.google.com/assured-workloads/access-transparency/docs/overview) provides for Agent Platform.

## Overview

Access Transparency provides you with logs that capture the actions Google personnel take when accessing your content.

[Cloud Audit Logs](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/audit-logging) show when members of your organization access content in your Google Cloud projects. Similarly, Access Transparency provides [logs](https://docs.cloud.google.com/assured-workloads/access-transparency/docs/reading-logs) of the actions taken by Google personnel.

You can [enable Access Transparency](https://docs.cloud.google.com/assured-workloads/access-transparency/docs/enable) for a Google Cloud project, if the project resides in an organization.

## Supported services

Access Transparency supports the following Gemini Enterprise Agent Platform services:

  - [Colab Enterprise](https://docs.cloud.google.com/colab/docs/introduction)
  - [Generative AI on Gemini Enterprise Agent Platform](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/overview)
  - [Gemini Enterprise Agent Platform AutoML training](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/training)
  - [Gemini Enterprise Agent Platform custom training](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/overview)
  - [Agent Platform Feature Store](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/featurestore)
  - [Gemini Enterprise Agent Platform Model Monitoring](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/model-monitoring/overview)
  - [Gemini Enterprise Agent Platform Pipelines](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/pipelines)
  - [Vertex AI Inference](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions)
  - [Vector Search](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search/overview)
  - [Vertex AI TensorBoard](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/experiments/tensorboard-introduction)
  - [Gemini Enterprise Agent Platform Workbench instances](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/introduction)
  - [Vertex Explainable AI](https://docs.cloud.google.com/vertex-ai/docs/explainable-ai)
  - [Vertex ML Metadata](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/ml-metadata/introduction)
  - [Agent Platform Vizier](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/vizier)
  - [Gemini Enterprise Agent Platform Agent Engine](https://docs.cloud.google.com/agent-builder/agent-engine/overview)
  - [Gemini Enterprise Agent Platform model tuning](https://docs.cloud.google.com/vertex-ai/generative-ai/docs/models/tune-models)

## Limitations of Access Transparency in Agent Platform

All access to your data in Gemini Enterprise Agent Platform by Google personnel is logged, except for the following scenarios:

  - [Scenarios where Access Transparency logs are excluded in all supported Google Cloud services](https://docs.cloud.google.com/assured-workloads/access-transparency/docs/exclusions)
  - Using [custom containers](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/use-custom-container) to serve [online inference](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/get-online-predictions) or [batch inference](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/get-batch-predictions) requests from custom-trained models
  - Using [Vertex Explainable AI](https://docs.cloud.google.com/vertex-ai/docs/explainable-ai/overview) with [custom containers](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/use-custom-container)
  - Using AutoML forecasting-related resources such as forecasting datasets and forecasting models.
  - Using the following components:
      - [Generative AI on Gemini Enterprise Agent Platform: Online inference (Vision)](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/image/generate-images)
      - [Agent Platform Vizier](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/vizier)
      - [Gemini Enterprise Agent Platform RAG Engine](https://docs.cloud.google.com/vertex-ai/generative-ai/docs/rag-overview)
      - [Gemini Enterprise Agent Platform Vector Search 2.0](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/vector-search-2/overview)

## What's next

  - Learn about the [content of Access Transparency logs](https://docs.cloud.google.com/assured-workloads/access-transparency/docs/reading-logs) .
  - Learn [when you would use Access Transparency](https://docs.cloud.google.com/assured-workloads/access-transparency/docs/overview#when-to-use) .
