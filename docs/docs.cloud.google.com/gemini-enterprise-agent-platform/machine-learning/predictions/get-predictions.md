---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/get-predictions
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/get-predictions
title: Get inferences from a custom trained model
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

[Video](https://www.youtube.com/watch?v=-9fU1xwBQYU)

An inference is the output of a trained machine learning model. This page provides an overview of the workflow for getting inferences from your models on Agent Platform.

Agent Platform offers two methods for getting inferences:

  - <span id="online-inference">**Online inferences** are synchronous requests made to a model that is deployed to an [`Endpoint`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.endpoints) . Therefore, before sending a request, you must first deploy the [`Model`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.models) resource to an endpoint. This associates [compute resources](https://docs.cloud.google.com/vertex-ai/docs/predictions/configure-compute) with the model so that the model can serve online inferences with low latency. Use online inferences when you are making requests in response to application input or in situations that require timely inference.</span>
  - <span id="batch-inference">**Batch inferences** are asynchronous requests made to a model that isn't deployed to an endpoint. You send the request (as a [`BatchPredictionJob`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.batchPredictionJobs) resource) directly to the `Model` resource. Use batch inferences when you don't require an immediate response and want to process accumulated data by using a single request.</span>

## Test your model locally

Before getting inferences, it's useful to deploy your model to a local endpoint during the development and testing phase. This lets you both iterate more quickly and test your model without deploying it to an online endpoint or incurring inference costs. Local deployment is intended for local development and testing, not for production deployments.

To deploy a model locally, use the Agent Platform SDK for Python and deploy a [`LocalModel`](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.prediction.LocalModel) to a [`LocalEndpoint`](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform.prediction.LocalEndpoint) . For a demonstration, see [this notebook](https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/community/vertex_endpoints/find_ideal_machine_type/find_ideal_machine_type.ipynb) .

Even if your client is not written in Python, you can still use the Agent Platform SDK for Python to launch the container and server so that you can test requests from your client.

## Get inferences from custom trained models

To get inferences, you must first [import your model](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/model-registry/import-model) . After it's imported, it becomes a [`Model`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.models) resource that is visible in [Model Registry](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/model-registry/introduction) .

Then, read the following documentation to learn how to get inferences:

  - [Get batch inferences](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/get-batch-predictions)
    
    Or

  - [Deploy model to endpoint](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/deployment) and [get online inferences](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/get-online-predictions) .

## What's next

  - Learn about [Compute resources for prediction](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/configure-compute) .
