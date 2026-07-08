---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/start/install-sdk
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/start/install-sdk
title: Install the Agent Platform SDK for Python
description: Create an isolated Python environment, install the Vertex AI SDK package, and initialize the Vertex AI SDK.
data_source: docs.cloud.google.com
---

Use the Agent Platform SDK for Python to automate your machine learning (ML) workflows. This page shows you how to install the Agent Platform SDK for Python. For more information about the Vertex AI SDK, see the following resources:

  - To learn about the Agent Platform SDK for Python, see [Introduction to the Agent Platform SDK for Python](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/python-sdk/use-vertex-ai-python-sdk) .
  - To learn how to train a model using the Agent Platform SDK for Python, see the [Train a model using Gemini Enterprise Agent Platform and the Python SDK](https://docs.cloud.google.com/gemini-enterprise-agent-platform/tutorials/tabular-bq-prediction) .
  - To learn about the classes and methods in the Agent Platform SDK for Python, see the [Vertex AI SDK reference](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest/google.cloud.aiplatform) .

Installation of the Agent Platform SDK for Python includes the following steps:

1.  [Create an isolated Python environment](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/start/install-sdk#create-isolated-environment)
2.  [Install the Vertex AI SDK package](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/start/install-sdk#install-python-sdk)
3.  [Initialize the Vertex AI SDK](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/start/install-sdk#initialize-python-sdk)

## Create an isolated Python environment

A Python best practice is to install the Vertex AI SDK in an isolated Python environment for each project. This helps prevent dependency, version, and permissions conflicts. You can create an isolated environment for using the command line in a shell or for using a notebook.

To create an isolated environment when you use the command line, [activate a `venv` environment](https://docs.cloud.google.com/python/docs/setup#installing_and_using_virtualenv) . After the `venv` environment is activated, you're ready to install the Vertex AI SDK and run your Python scripts. For more information, see [Use `venv` to isolate dependencies](https://docs.cloud.google.com/python/docs/setup#installing_and_using_virtualenv) and [Set up a Python development environment](https://docs.cloud.google.com/python/docs/setup) .

To use a notebook in an isolated environment, you can create a Gemini Enterprise Agent Platform Workbench instance. Then, install the Vertex AI SDK and run your Python scripts from a notebook on your Gemini Enterprise Agent Platform Workbench instance. For more information, see [Create a Agent Platform Workbench instance](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/create) .

## Install or update the Vertex AI SDK package

To install or update the Vertex AI SDK, run the following command in your virtual environment:

    pip install --upgrade google-cloud-aiplatform

## Initialize the Vertex AI SDK

After you install the Agent Platform SDK for Python, you must initialize the SDK with your Gemini Enterprise Agent Platform and Google Cloud details. For example, when you initialize the SDK, you specify information such as your project name, region, and your staging Cloud Storage bucket. The following method is an example of a method that initializes the Vertex AI SDK.

    def init_sample(
        project: Optional[str] = None,
        location: Optional[str] = None,
        experiment: Optional[str] = None,
        staging_bucket: Optional[str] = None,
        credentials: Optional[google.auth.credentials.Credentials] = None,
        encryption_spec_key_name: Optional[str] = None,
        service_account: Optional[str] = None,
    ):
    
        import vertexai
    
        vertexai.init(
            project=project,
            location=location,
            experiment=experiment,
            staging_bucket=staging_bucket,
            credentials=credentials,
            encryption_spec_key_name=encryption_spec_key_name,
            service_account=service_account,
        )

## What's next

  - Learn more about the [Vertex AI SDK](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/python-sdk/use-vertex-ai-python-sdk) .
