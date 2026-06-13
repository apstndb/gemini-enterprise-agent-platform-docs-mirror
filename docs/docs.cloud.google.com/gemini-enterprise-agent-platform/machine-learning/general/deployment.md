---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/deployment
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/deployment
title: Deploy a model to an endpoint
description: Learn how to deploy a model to an endpoint.
data_source: docs.cloud.google.com
---

Before you can [get online inferences](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/get-online-predictions) from a trained model, you must deploy the model to an [endpoint](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/choose-endpoint-type) . This can be done by using the Google Cloud console, the Google Cloud CLI, or the Gemini Enterprise API.

This document describes the process for deploying models to endpoints.

## What happens when you deploy a model

Deploying a model associates physical resources with the model so that it can serve online inferences with low latency.

You can deploy multiple models to an endpoint, or you can deploy the same model to multiple endpoints. For more information, see [Reasons to deploy more than one model to the same endpoint](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/deployment#models-endpoint) .

## Prepare to deploy a model to an endpoint

During model deployment, you make the following important decisions about how to run online inference:

| Resource created | Setting specified at resource creation                                                                                                                         |
| ---------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Endpoint         | Location in which to run inferences                                                                                                                            |
| Model            | Container to use ( [`ModelContainerSpec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/ModelContainerSpec) )               |
| DeployedModel    | [Compute resources to use for online inference](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/configure-compute) |

After the model is deployed to the endpoint, these deployment settings can't be changed. To change them, you must redeploy your model.

The first step in the deployment process is to decide which type of endpoint to use. For more information, see [Choose an endpoint type](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/choose-endpoint-type) .

Next, make sure that the model is visible in Gemini Enterprise Agent Platform Model Registry. This is required for the model to be deployable. For information about Model Registry, including how to import model artifacts or create them directly in Model Registry, see [Introduction to Gemini Enterprise Agent Platform Model Registry](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/model-registry/introduction) .

The next decision to make is which compute resources to use for serving the model. The model's training type (AutoML or custom) and (AutoML) data type determine the kinds of physical resources available to the model. After model deployment, you can [`mutate`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.endpoints/mutateDeployedModel) some of those resources without creating a new deployment.

The endpoint resource provides the service endpoint (URL) you use to request the inference. For example:

``` 
   https://us-central1-aiplatform.googleapis.com/v1/projects/{project}/locations/{location}/endpoints/{endpoint}:predict
```

## Deploy a model to an endpoint

You can deploy a model to an endpoint by [using the Google Cloud console](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/deployment#create-dedicated-endpoint) or by [using the gcloud CLI or Gemini Enterprise API](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/deployment#create-endpoint) .

### Deploy a model to a public endpoint by using the Google Cloud console

In the Google Cloud console, you can deploy a model to an existing dedicated or shared public endpoint, or you can create a new endpoint during the deployment process. For details, see [Deploy a model by using the Google Cloud console](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/deploy-model-console) .

### Deploy a model to a public endpoint by using the gcloud CLI or Gemini Enterprise API

When you deploy a model by using the gcloud CLI or Gemini Enterprise API, you must first create a dedicated or shared endpoint and then deploy the model to it. For details, see:

1.  [Create a dedicated or shared public endpoint](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/create-public-endpoint)
2.  [Deploy a model by using the gcloud CLI or Gemini Enterprise API](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/deploy-model-api)

### Deploy a model to a Private Service Connect endpoint

For details, see [Use Private Service Connect endpoints for online inference](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/private-service-connect) .

### Use a rolling deployment to update a deployed model

You can use a *rolling deployment* to replace a deployed model with a new version of the same model. The new model reuses the compute resources from the previous one. For details, see [Use a rolling deployment to replace a deployed model](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/rolling-deployment) .

### Undeploy a model and delete the endpoint

You can undeploy a model and delete the endpoint. For details, see [Undeploy a model and delete the endpoint](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/undeploy-model) .

## Reasons to deploy more than one model to the same endpoint

Deploying two models to the same endpoint lets you gradually replace one model with the other. For example, suppose you're using a model, and find a way to increase the accuracy of that model with new training data. However, you don't want to update your application to point to a new endpoint URL, and you don't want to create sudden changes in your application. You can add the new model to the same endpoint, serving a small percentage of traffic, and gradually increase the traffic split for the new model until it is serving 100% of the traffic.

Because the resources are associated with the model rather than the endpoint, you could deploy models of different types to the same endpoint. However, the best practice is to deploy models of a specific type (for example, AutoML tabular or custom-trained) to an endpoint. This configuration is easier to manage.

## Reasons to deploy a model to more than one endpoint

You might want to deploy your models with different resources for different application environments, such as testing and production. You might also want to support different SLOs for your inference requests. Perhaps one of your applications has much higher performance needs than the others. In this case, you can deploy that model to a higher-performance endpoint with more machine resources. To optimize costs, you can also deploy the model to a lower-performance endpoint with fewer machine resources.

## Scaling behavior

Vertex AI Inference autoscaling scales the number of inference nodes based on the number of concurrent requests. This lets you dynamically adjust to changing request loads while managing costs. For more information, see [Scale inference nodes for Vertex AI Inference](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/autoscaling) .

## What's next

  - [Choose an endpoint type](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/choose-endpoint-type) .
  - [Deploy a model by using the Google Cloud console](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/deploy-model-console) .
  - Learn about [Inference request-response logging for dedicated endpoints and Private Service Connect endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/online-prediction-logging#dedicated-and-psc) .
  - Learn how to [get an online inference](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/get-online-predictions) .
  - Learn how to [change the default settings for inference logging](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/online-prediction-logging#enabling-and-disabling) .
