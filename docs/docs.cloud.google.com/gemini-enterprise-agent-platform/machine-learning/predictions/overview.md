---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/overview
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/overview
title: Overview of getting inferences on Gemini Enterprise Agent Platform
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

An inference is the output of a trained machine learning model. This page provides an overview of the workflow for getting inferences from your models on Agent Platform.

Agent Platform offers two methods for getting inferences:

  - <span id="online-inference">**Online inferences** are synchronous requests made to a model that is deployed to an [`Endpoint`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.endpoints) . Therefore, before sending a request, you must first deploy the [`Model`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.models) resource to an endpoint. This associates [compute resources](https://docs.cloud.google.com/vertex-ai/docs/predictions/configure-compute) with the model so that the model can serve online inferences with low latency. Use online inferences when you are making requests in response to application input or in situations that require timely inference.</span>
  - <span id="batch-inference">**Batch inferences** are asynchronous requests made to a model that isn't deployed to an endpoint. You send the request (as a [`BatchPredictionJob`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.batchPredictionJobs) resource) directly to the `Model` resource. Use batch inferences when you don't require an immediate response and want to process accumulated data by using a single request.</span>

## Get inferences from custom trained models

To get inferences, you must first [import your model](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/model-registry/import-model) . After it's imported, it becomes a [`Model`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.models) resource that is visible in [Model Registry](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/model-registry/introduction) .

Then, read the following documentation to learn how to get inferences:

  - [Get batch inferences](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/get-batch-predictions)
    
    Or

  - [Deploy model to endpoint](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/deployment) and [get online inferences](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/get-online-predictions) .

## Get inferences from AutoML models

Unlike custom trained models, AutoML models are automatically imported into the Model Registry after training.

Other than that, the workflow for AutoML models is similar, but varies slightly based on your data type and model objective. The documentation for getting AutoML inferences is located alongside the other AutoML documentation. Here are links to the documentation:

### Image

Learn how to get inferences from the following types of image AutoML models:

  - [Image classification models](https://docs.cloud.google.com/vertex-ai/docs/image-data/classification/get-predictions)
  - [Image object detection models](https://docs.cloud.google.com/vertex-ai/docs/image-data/object-detection/get-predictions)

### Tabular

Learn how to get inferences from the following types of tabular AutoML models:

  - Tabular classification and regression models
    
      - [Online inferences](https://docs.cloud.google.com/vertex-ai/docs/tabular-data/classification-regression/get-online-predictions)
      - [Batch inferences](https://docs.cloud.google.com/vertex-ai/docs/tabular-data/classification-regression/get-batch-predictions)

  - [Tabular forecasting models](https://docs.cloud.google.com/vertex-ai/docs/tabular-data/forecasting/get-predictions) (batch inferences only)

## Get inferences from BigQuery ML models

You can get inferences from BigQuery ML models in two ways:

  - Request batch inferences directly from the model in BigQuery ML.
  - Register the models directly with the Model Registry, without exporting them from BigQuery ML or importing them into the Model Registry.
