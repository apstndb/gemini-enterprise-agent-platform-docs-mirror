---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/deploy-genai
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/deploy-genai
title: Deploy generative AI models
description: Learn about deploying generative AI models in Gemini Enterprise Agent Platform.
data_source: docs.cloud.google.com
---

This page provides guidance for deploying a generative AI model to an endpoint for online inference.

## Check the Model Garden

If the model is in Model Garden, you can deploy it by clicking **Deploy** (available for some models) or **Open Notebook** .

Otherwise, you can do one of the following:

  - If your model is similar to one in the Model Garden, you might be able to directly reuse one of the [model garden containers](https://us-docker.pkg.dev/vertex-ai/vertex-vision-model-garden-dockers) .

  - Build your own custom container that adheres to [Custom container requirements for inference](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/custom-container-requirements) before [importing your model](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/model-registry/import-model) into the [Gemini Enterprise Agent Platform Model Registry](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/model-registry/introduction) . After it's imported, it becomes a [`model`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.models) resource that you can [deploy to an endpoint](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/deployment) .
    
    You can use the [Dockerfiles and scripts](https://github.com/GoogleCloudPlatform/vertex-ai-samples/tree/main/community-content/vertex_model_garden) that we use to build our Model Garden containers as a reference or starting point to build your own custom containers.

## Serving inferences with NVIDIA NIM

[NVIDIA Inference Microservices (NIM)](https://developer.nvidia.com/blog/nvidia-nim-offers-optimized-inference-microservices-for-deploying-ai-models-at-scale/) are pre-trained and optimized AI models that are packaged as microservices. They're designed to simplify the deployment of high-performance, production-ready AI into applications.

NVIDIA NIM can be used together with [Artifact Registry](https://docs.cloud.google.com/artifact-registry/docs/overview) and Gemini Enterprise Agent Platform to deploy generative AI models for online inference.

> To see an example of using NVIDIA NIM, run the "NVIDIA NIM on Google Cloud " notebook in one of the following environments:
> 
> [![](https://docs.cloud.google.com/static/vertex-ai/images/colab-logo-32px.png) Open in Colab](https://colab.research.google.com/github/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/generative_ai/nvidia_nim_vertexai.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/colab-enterprise-logo-32px.png) Open in Colab Enterprise](https://console.cloud.google.com/vertex-ai/colab/import/https%3A%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Fgenerative_ai%2Fnvidia_nim_vertexai.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/vertex-ai-workbench-logo-32px.png) Open in Vertex AI Workbench](https://console.cloud.google.com/vertex-ai/workbench/deploy-notebook?download_url=https%3A%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Fgenerative_ai%2Fnvidia_nim_vertexai.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/github-logo-32px.png) View on GitHub](https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/generative_ai/nvidia_nim_vertexai.ipynb)

## Settings for custom containers

This section describes fields in your model's [`containerSpec`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/ModelContainerSpec) that you may need to specify when importing generative AI models.

You can specify these fields by using the Agent Platform REST API or the [`gcloud ai models upload` command](https://docs.cloud.google.com/sdk/gcloud/reference/ai/models/upload) . For more information, see [Container-related API fields](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/use-custom-container#fields) .

  - `sharedMemorySizeMb`  
    Some generative AI models require more **shared memory** . Shared memory is an Inter-process communication (IPC) mechanism that allows multiple processes to access and manipulate a common block of memory. The default shared memory size is 64MB.
    
    Some model servers, such as [vLLM](https://github.com/GoogleCloudPlatform/vertex-ai-samples/tree/main/community-content/vertex_model_garden/model_oss/vllm) or Nvidia Triton, use shared memory to cache internal data during model inferences. Without enough shared memory, some model servers cannot serve inferences for generative models. The amount of shared memory needed, if any, is an implementation detail of your container and model. Consult your model server documentation for guidelines.
    
    Also, because shared memory can be used for cross GPU communication, using more shared memory can improve performance for accelerators without NVLink capabilities (for example, L4), if the model container requires communication across GPUs.
    
    For information on how to specify a custom value for shared memory, see [Container-related API fields](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/use-custom-container#fields) .

  - `startupProbe`  
    A **startup probe** is an optional probe that is used to detect when the container has started. This probe is used to delay the health probe and [liveness checks](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/custom-container-requirements#liveness_checks) until the container has started, which helps prevent slow starting containers from getting shut down prematurely.
    
    For more information, see [Health checks](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/custom-container-requirements#health) .

  - `healthProbe`  
    The **health probe** checks whether a container is ready to accept traffic. If health probe is not provided, Agent Platform will use the default health checks which issues a HTTP request to the container's port and looks for a `200 OK` response from the model server.
    
    If your model server responds with `200 OK` before the model is fully loaded, which is possible, especially for large models, then the health check will succeed prematurely and Gemini Enterprise Agent Platform will route traffic to the container before it is ready.
    
    In these cases, specify a custom health probe that succeeds only after the model is fully loaded and ready to accept traffic.
    
    For more information, see [Health checks](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/custom-container-requirements#health) .

## Limitations

Consider the following limitations when deploying generative AI models:

  - Generative AI models can only be deployed to a single machine. Multi-host deployment isn't supported.
  - For very large models that don't fit in the largest supported vRAM, such as [Llama 3.1 405B](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/open-models/use-llama#llama_31) , we recommend quantizing them to fit.
