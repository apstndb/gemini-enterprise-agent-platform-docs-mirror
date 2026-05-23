---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/datasets/overview
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/datasets/overview
title: Overview of creating managed datasets on Gemini Enterprise Agent Platform
description: Overview of creating managed datasets on Gemini Enterprise Agent Platform.
data_source: docs.cloud.google.com
---

You can use a managed dataset to provide the source data used to train AutoML and custom models on Gemini Enterprise Agent Platform. A managed dataset is required for AutoML and is optional for custom training.

## Permissions and access control

When you use data from a Cloud Storage bucket to create a dataset, Agent Platform requires permissions to access the data. Agent Platform uses a special Google-managed service account known as a Service Agent to securely access your data. For more information on the roles required and how the Service Agent works, see [Access control with IAM](https://docs.cloud.google.com/vertex-ai/docs/general/access-control#service-agents) .

## Create a managed dataset for AutoML models

You can create managed datasets for training AutoML models by using the Google Cloud console or the Agent Platform API. The instructions for how to do this slightly vary based on your data type and model objective. Start by preparing your training data.

### Image

Learn how to create a managed dataset for the following types of image AutoML models:

  - [Image classification models](https://docs.cloud.google.com/vertex-ai/docs/image-data/classification/prepare-data)
  - [Image object detection models](https://docs.cloud.google.com/vertex-ai/docs/image-data/object-detection/prepare-data)

### Tabular

Learn how to create a managed dataset for the following types of tabular AutoML models:

  - [Tabular classification and regression models](https://docs.cloud.google.com/vertex-ai/docs/tabular-data/classification-regression/prepare-data)
  - [Tabular forecasting models](https://docs.cloud.google.com/vertex-ai/docs/tabular-data/forecasting/prepare-data)

## Create a managed dataset for custom trained models

The instructions on how to create a managed dataset for training custom models are the same, regardless of your data type or model objective.

For details, see [Use managed datasets](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/using-managed-datasets) .

## View managed datasets using Knowledge Catalog

Knowledge Catalog is a fully managed, scalable metadata management service that provides a centralized location to search for datasets across projects and regions. It's integrated with Gemini Enterprise Agent Platform and offers similar capabilities to the deprecated Data Catalog.

You can use Knowledge Catalog to discover, understand, and enrich your data with aspects (which are similar to Data Catalog tags).

For details on managing metadata and aspects for your Agent Platform resources, see [Manage aspects and enrich metadata](https://docs.cloud.google.com/dataplex/docs/enrich-entries-metadata) in the [Knowledge Catalog](https://docs.cloud.google.com/dataplex/docs/catalog-overview) .
