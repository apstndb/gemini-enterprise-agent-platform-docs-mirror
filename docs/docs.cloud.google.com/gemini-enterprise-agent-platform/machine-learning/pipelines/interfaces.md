---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/pipelines/interfaces
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/pipelines/interfaces
title: Interfaces for Gemini Enterprise Agent Platform Pipelines
description: Understand the interfaces and APIs for interacting with Gemini Enterprise Agent Platform Pipelines.
data_source: docs.cloud.google.com
---

> To learn more, run the "Learn how to build Python function-based Kubeflow pipeline components" notebook in one of the following environments:
> 
> [![](https://docs.cloud.google.com/static/vertex-ai/images/colab-logo-32px.png) Open in Colab](https://colab.research.google.com/github/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/pipelines/lightweight_functions_component_io_kfp.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/colab-enterprise-logo-32px.png) Open in Colab Enterprise](https://console.cloud.google.com/vertex-ai/colab/import/https%3A%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Fpipelines%2Flightweight_functions_component_io_kfp.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/vertex-ai-workbench-logo-32px.png) Open in Vertex AI Workbench](https://console.cloud.google.com/vertex-ai/workbench/deploy-notebook?download_url=https%3A%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Fpipelines%2Flightweight_functions_component_io_kfp.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/github-logo-32px.png) View on GitHub](https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/pipelines/lightweight_functions_component_io_kfp.ipynb)

This page lists the interfaces that you can use to define and run ML pipelines on Agent Platform Pipelines.

## Interfaces to define a pipeline

Agent Platform Pipelines supports ML pipelines defined using the Kubeflow Pipelines (KFP) SDK or the TensorFlow Extended (TFX) SDK.

### Kubeflow Pipelines (KFP) SDK

![Kubeflow Pipelines logo](https://docs.cloud.google.com/static/gemini-enterprise-agent-platform/machine-learning/pipelines/images/icons/kfp_logo.png) Use KFP for all use cases where you don't need to use TensorFlow Extended to process huge amounts of structured or text data. Agent Platform Pipelines supports KFP SDK v2.0 or later.

When you use the KFP SDK, you can define your ML workflow by building custom components and also by reusing prebuilt components, such as the Google Cloud Pipeline Components. Google Cloud Pipeline Components let you easily use Gemini Enterprise services like AutoML in your ML pipeline. Agent Platform Pipelines supports Google Cloud Pipeline Components SDK v2 or later. For more information about Google Cloud Pipeline Components, see [Introduction to Google Cloud Pipeline Components](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/pipelines/components-introduction) .

To learn how to build a pipeline using the Kubeflow Pipelines, see [Build a pipeline](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/pipelines/build-pipeline) . To learn more about Kubeflow Pipelines, see the [Kubeflow Pipelines documentation](https://www.kubeflow.org/docs/components/pipelines/) .

### TensorFlow Extended (TFX) SDK

![TFX SDK logo](https://docs.cloud.google.com/static/gemini-enterprise-agent-platform/machine-learning/pipelines/images/icons/tfx_icon.png) Use TFX if you use TensorFlow Extended in your ML workflow to process terabytes of structured or text data. Agent Platform Pipelines supports TFX SDK v0.30.0 or later.

To learn how to build ML pipelines using TFX, see the [Getting started tutorials](https://www.tensorflow.org/tfx/tutorials) section on the [TensorFlow Extended in Production tutorials](https://www.tensorflow.org/tfx/tutorials#tfx-on-google-cloud) .

## Interfaces to run a pipeline

After you define your ML pipeline, you can create an ML pipeline run using any of the following interfaces:

  - REST API

  - SDK clients

  - Google Cloud console

> **Note:** Agent Platform Pipelines doesn't support the gcloud CLI interface.

For more information about the interfaces you can use to interact with Gemini Enterprise API, see [Interfaces for Gemini Enterprise API](https://docs.cloud.google.com/vertex-ai/docs/start/introduction-interfaces) .

### REST API

To create a pipeline run using REST, use the `Pipelines` service API. This API uses the [`projects.locations.pipelineJobs`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.pipelineJobs) REST resource.

> **Note:** Breaking changes to the `Pipelines` service API are communicated as preview launches. You can test the changes announced in preview, see the the API documentation for [`projects.locations.pipelineJobs` (v1beta1)](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.pipelineJobs) . For more information about the preview launch stage, see the [launch stage descriptions](https://cloud.google.com/products#product-launch-stages) .

### SDK Clients

Agent Platform Pipelines lets you create pipeline runs using the Vertex AI SDK for Python or client libraries.

#### Agent Platform SDK for Python

The Vertex AI SDK for Python ( `aiplatform` ) is the recommended SDK for programmatically working with the `Pipelines` service API. For more information about this SDK, see the [API documentation for `google.cloud.aiplatform.PipelineJob`](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform/google.cloud.aiplatform.PipelineJob) .

#### Client libraries

Client libraries are programmatically Generated API Clients (GAPIC) SDKs. Agent Platform Pipelines supports the following client libraries:

  - Python ( `aiplatform` `v1` and `v1beta1` )

  - Java

  - Node.js

  - [Go](https://cloud.google.com/go/docs/reference/cloud.google.com/go/aiplatform/latest/apiv1#cloud_google_com_go_aiplatform_apiv1_PipelineClient)

For more information, see [Install the Gemini Enterprise Agent Platform client libraries](https://docs.cloud.google.com/vertex-ai/docs/start/client-libraries) .

### Google Cloud console (GUI)

Google Cloud console is the recommended way for reviewing and monitoring your pipeline runs. You can also perform other tasks using the Google Cloud console, such as creating, deleting and cloning pipeline runs, accessing the Template Gallery, and retrieving the billing label for a pipeline run.

## What's next

  - Get started by [learning how to define a pipeline using the Kubeflow Pipelines SDK](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/pipelines/build-pipeline) .

  - [Learn how to run a pipeline](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/pipelines/run-pipeline) .

  - Learn about [best practices for implementing custom-trained ML models on Gemini Enterprise Agent Platform](https://cloud.google.com/architecture/ml-on-gcp-best-practices#machine-learning-workflow-orchestration) .
