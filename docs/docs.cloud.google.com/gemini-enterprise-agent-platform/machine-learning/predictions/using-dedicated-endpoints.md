---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/using-dedicated-endpoints
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/using-dedicated-endpoints
title: Use dedicated public endpoints for online inference
description: Learn about using dedicated public endpoints for online inference.
data_source: docs.cloud.google.com
---

A *dedicated public endpoint* is a public endpoint for online inference. It offers the following benefits:

  - **Dedicated networking** : When you send an inference request to a dedicated public endpoint, it is isolated from other users' traffic.
  - **Optimized network latency**
  - **Larger payload support** : Up to 10 MB.
  - **Longer request timeouts** : Configurable up to 1 hour.
  - **Generative AI-ready** : Streaming and gRPC are supported. Inference timeout is configurable up to 1 hour.

For these reasons, dedicated public endpoints are recommended as a best practice for serving Gemini Enterprise Agent Platform online inferences.

> **Note:** Tuned Gemini models can only be deployed to shared public endpoints.

To learn more, see [Choose an endpoint type](https://docs.cloud.google.com/vertex-ai/docs/predictions/choose-endpoint-type) .

## Create a dedicated public endpoint and deploy a model to it

You can create a dedicated endpoint and deploy a model to it by using the Google Cloud console. For details, see [Deploy a model by using the Google Cloud console](https://docs.cloud.google.com/vertex-ai/docs/predictions/deploy-model-console) .

You can also create a dedicated public endpoint and deploy a model to it by using the Gemini Enterprise API as follows:

1.  [Create a dedicated public endpoint](https://docs.cloud.google.com/vertex-ai/docs/predictions/create-public-endpoint) . Configuration of the inference timeout and request-response logging settings is supported at the time of endpoint creation.
2.  [Deploy the model by using the Gemini Enterprise API](https://docs.cloud.google.com/vertex-ai/docs/predictions/deploy-model-api) .

## Get online inferences from a dedicated public endpoint

Dedicated endpoints support both HTTP and gRPC communication protocols. For gRPC requests, the x-vertex-ai-endpoint-id header must be included for proper endpoint identification. The following APIs are supported:

  - Predict
  - RawPredict
  - StreamRawPredict
  - Chat Completion (Model Garden only)

You can send online inference requests to a dedicated public endpoint by using the Agent Platform SDK for Python. For details, see [Send an online inference request to a dedicated public endpoint](https://docs.cloud.google.com/vertex-ai/docs/predictions/get-online-predictions#inference-request-dedicated) .

## Tutorial

> To learn more, run the " Model Garden - Gemma (Deployment)" notebook in one of the following environments:
> 
> [![](https://docs.cloud.google.com/static/vertex-ai/images/colab-logo-32px.png) Open in Colab](https://colab.research.google.com/github/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/community/model_garden/model_garden_gemma_deployment_on_vertex.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/colab-enterprise-logo-32px.png) Open in Colab Enterprise](https://console.cloud.google.com/vertex-ai/colab/import/https%3A%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fcommunity%2Fmodel_garden%2Fmodel_garden_gemma_deployment_on_vertex.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/vertex-ai-workbench-logo-32px.png) Open in Vertex AI Workbench](https://console.cloud.google.com/vertex-ai/workbench/deploy-notebook?download_url=https%3A%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fcommunity%2Fmodel_garden%2Fmodel_garden_gemma_deployment_on_vertex.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/github-logo-32px.png) View on GitHub](https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/community/model_garden/model_garden_gemma_deployment_on_vertex.ipynb)

## Limitations

  - Deployment of tuned Gemini models isn't supported.
  - VPC Service Controls isn't supported. Use a Private Service Connect endpoint instead.

## What's next

  - Learn about Gemini Enterprise Agent Platform online inference [endpoint types](https://docs.cloud.google.com/vertex-ai/docs/predictions/choose-endpoint-type) .
