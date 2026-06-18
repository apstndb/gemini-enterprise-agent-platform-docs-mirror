---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/python-sdk/use-vertex-ai-python-sdk
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/python-sdk/use-vertex-ai-python-sdk
title: Introduction to the Agent Platform SDK for Python
description: Learn about the Agent Platform SDK for Python and how it differs from the Gemini Enterprise Agent Platform Python client library.
data_source: docs.cloud.google.com
---

The Agent Platform SDK for Python helps you automate data ingestion, train models, and get predictions on Gemini Enterprise Agent Platform. The Vertex AI SDK uses Python code to access the Agent Platform API so that you can programmatically accomplish most of what you can do in the Google Cloud console.

To learn how to install or update the Agent Platform SDK for Python, see [Install the Agent Platform SDK for Python](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/start/install-sdk) . For more information, see the [Agent Platform SDK for Python API reference documentation](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest) .

## Why use the Vertex AI SDK

The Agent Platform SDK for Python is recommended if you're an experienced machine learning (ML) and artificial intelligence (AI) engineer or a data scientist who wants to programmatically automate your workflow. The Agent Platform SDK for Python is similar to the Gemini Enterprise Agent Platform Python client library, except the Vertex AI SDK is higher-level and less granular. For more information, see [Understand the SDK and client library differences](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/python-sdk/use-vertex-ai-python-sdk#sdk-vs-client-library) .

## Write code with the Agent Platform SDK for Python

To use the Agent Platform SDK for Python:

1.  Install the `google-cloud-aiplatform` package, which includes both the Agent Platform SDK for Python and the Gemini Enterprise Agent Platform Python client library, by running the following command in your virtual environment:
    
        pip install --upgrade google-cloud-aiplatform

2.  Use the following code to import the `google.cloud.aiplatform` namespace:
    
        from google.cloud import aiplatform
    
    > **Preview:** To use features for the Agent Platform SDK for Python that are still in [preview](https://cloud.google.com/products/#product-launch-stages) , import `vertexai.preview` :
    > 
    >     import vertexai.preview

3.  If you're using a local shell, then create local authentication credentials for your user account:
    
        gcloud auth application-default login
    
    You don't need to do this if you're using Cloud Shell.
    
    If an authentication error is returned, and you are using an external identity provider (IdP), confirm that you have [signed in to the gcloud CLI with your federated identity](https://docs.cloud.google.com/iam/docs/workforce-log-in-gcloud) .

### Learn about the Agent Platform SDK for Python

See the following documentation:

  - [Vertex AI SDK class overview](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/python-sdk/python-sdk-class-overview) : introduces the key classes and functionality in the Vertex AI SDK.

  - [Python reference for Gemini Enterprise Agent Platform](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest) : contains reference documentation for all of the namespaces, classes, methods, and properties in the `google-cloud-aiplatform` package, which includes the Vertex AI SDK, the Vertex AI SDK preview, and the Gemini Enterprise Agent Platform Client libraries.

### Try code samples and tutorials

Notebook tutorials show how to use the Agent Platform SDK for Python as part of a larger workflow. For more information, see [Gemini Enterprise Agent Platform notebook tutorials](https://docs.cloud.google.com/vertex-ai/docs/tutorials/jupyter-notebooks) .

Code samples in the Agent Platform SDK for Python GitHub repository show you how to complete individual tasks. For more information, see the [Agent Platform SDK for Python GitHub repository](https://github.com/googleapis/python-aiplatform/) .

> To see an example of using the Vertex AI SDK as part of a more comprehensive workflow, run the "Custom training and online prediction" notebook in one of the following environments:
> 
> [![](https://docs.cloud.google.com/static/vertex-ai/images/colab-logo-32px.png) Open in Colab](https://colab.research.google.com/github/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/custom/sdk-custom-image-classification-online.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/colab-enterprise-logo-32px.png) Open in Colab Enterprise](https://console.cloud.google.com/agent-platform/colab/import/https%3A%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Fcustom%2Fsdk-custom-image-classification-online.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/vertex-ai-workbench-logo-32px.png) Open in Agent Platform Workbench](https://console.cloud.google.com/agent-platform/workbench/deploy-notebook?download_url=https%3A%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Fcustom%2Fsdk-custom-image-classification-online.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/github-logo-32px.png) View on GitHub](https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/custom/sdk-custom-image-classification-online.ipynb)

## Understand the Vertex AI SDK and client library differences

When you install the Agent Platform SDK for Python, the Gemini Enterprise Agent Platform Python client library is also installed. The Vertex AI SDK and the Gemini Enterprise Agent Platform Python client library provide similar functionality with different levels of granularity. The Vertex AI SDK operates at a higher level of abstraction than the client library and is suitable for most common data science workflows. If you need lower-level functionality, then use the Gemini Enterprise Agent Platform Python client library.

The Vertex AI SDK is available for Python and a Gemini Enterprise Agent Platform client library is available for Python, Java, and Node.js. To learn how to install the Java or Node.js client library, see [Install the Gemini Enterprise Agent Platform client libraries](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/start/client-libraries) . If a client library isn't available in your preferred programming language, you can use the Gemini Enterprise Agent Platform REST API. For more information, see the [Gemini Enterprise Agent Platform REST reference](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest) .

### Use Gemini Enterprise Agent Platform Python client library and SDK together

If you use the Agent Platform SDK for Python and discover you need greater flexibility or control, or if you need a method not included in the Vertex AI SDK, you can use the Gemini Enterprise Agent Platform Python client library in the same workflow. The Gemini Enterprise Agent Platform Python client library uses a different namespace to access the Agent Platform API. The client library and the Agent Platform SDK for Python namespaces can be used in the same Python script by adding an `import` line for each in your Python script.

### Import the Gemini Enterprise Agent Platform Python client library namespace

The Gemini Enterprise Agent Platform Python client library namespace is `google.cloud.aiplatform.gapic` . This namespace maps to the `google.cloud.aiplatform_v1` namespace. These two namespaces can be used interchangeably. To import the Python client library, include one of the following in your Python script:

    from google.cloud import aiplatform_v1

    from google.cloud.aiplatform import gapic

## What's next

  - Learn how to [choose a training method](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/start/training-methods) .
