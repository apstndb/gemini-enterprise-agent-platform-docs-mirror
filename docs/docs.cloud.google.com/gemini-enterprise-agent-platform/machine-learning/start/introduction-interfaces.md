---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/start/introduction-interfaces
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/start/introduction-interfaces
title: Interfaces for Gemini Enterprise Agent Platform
description: Learn about the different tools available for interacting with Gemini Enterprise Agent Platform and when to use each.
data_source: docs.cloud.google.com
---

This page describes the interfaces that you can use to interact with Gemini Enterprise Agent Platform and when you should use them. You can use these interfaces along with one of Agent Platform's [notebook solutions](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/notebook-solution) .

Some Gemini Enterprise Agent Platform operations are only available through specific interfaces, so you may need to switch between interfaces during your workflow. For example, in Vertex AI Experiments, you must use the API to log data to an experiment run, but you can view the results in the console.

### Console

The Google Cloud console is a graphical user interface that you can use to work with your machine learning resources.

In the Google Cloud console, you can manage your managed datasets , models, endpoints, and jobs. You can also access other Google Cloud services, such as Cloud Storage and BigQuery, through the console.

Use the Google Cloud console if you prefer to view and manage your Gemini Enterprise Agent Platform resources and visualizations through a graphical user interface.

For more information, see the **Dashboard** page of the Gemini Enterprise Agent Platform section:

### gcloud

The [Google Cloud command-line interface (CLI)](https://docs.cloud.google.com/sdk/gcloud) is a set of tools for creating and managing Google Cloud resources using the `gcloud` command.

Use the Google Cloud CLI when you want to manage your Gemini Enterprise Agent Platform resources from the command line or through scripts and other automation.

For more information, see [Install the gcloud CLI](https://docs.cloud.google.com/sdk/docs/install) and the [`gcloud ai`](https://docs.cloud.google.com/sdk/gcloud/reference/ai) reference.

### Terraform

Terraform is an infrastructure as code (IaC) tool that you can use to provision the infrastructure, such as resources and permissions, for multiple Google Cloud services, including Gemini Enterprise Agent Platform.

You can define the Gemini Enterprise Agent Platform resources and permissions for your Google Cloud project in a Terraform configuration file. You can then use Terraform to apply the configuration to your project by creating new resources and updating existing resources.

Use Terraform if you want to standardize the infrastructure for Gemini Enterprise Agent Platform resources in your Google Cloud project and update the existing Google Cloud project infrastructure while fulfilling resource dependencies.

To get started, see [Terraform support for Gemini Enterprise Agent Platform](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/start/use-terraform-vertex-ai) .

### Python

Use the [Agent Platform SDK for Python](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/python-sdk/use-vertex-ai-python-sdk) to programmatically automate your Gemini Enterprise Agent Platform workflow.

The Agent Platform SDK for Python is similar to the Gemini Enterprise Agent Platform Python client library, except the SDK is higher-level and less granular. For more information, see the [Understand the SDK and client library differences](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/python-sdk/use-vertex-ai-python-sdk#sdk-vs-client-library) .

To get started, see [Install the Agent Platform SDK](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/start/install-sdk) .

### Client libraries

Client libraries use each supported language's natural conventions to call the Agent Platform API and reduce boilerplate code that you have to write.

The following languages are supported for Gemini Enterprise Agent Platform:

  - Python. The Gemini Enterprise Agent Platform Python client library is installed when you install the [Agent Platform SDK for Python](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/python-sdk/use-vertex-ai-python-sdk) .

  - Java

  - Node.js

  - C\#

  - Go

For more information, see [Install the Gemini Enterprise Agent Platform client libraries](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/start/client-libraries) .

### REST

The Gemini Enterprise Agent Platform REST API provides RESTful services for managing jobs, models, and endpoints, and for making inferences with hosted models on Google Cloud.

Use the REST API if you need to use your own libraries to call the Agent Platform API from your application.

To get started, see the [Agent Platform API REST reference](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest) .

## What's next

  - [Set up a project and a development environment](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/start/cloud-environment) .
  - [Choose a training method](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/start/training-methods) .
  - Tutorials for [Image](https://docs.cloud.google.com/vertex-ai/docs/tutorials/image-classification-automl/overview) , [Tabular](https://docs.cloud.google.com/vertex-ai/docs/tutorials/tabular-automl/overview) , and [Custom training](https://docs.cloud.google.com/vertex-ai/docs/tutorials/image-classification-custom/overview) .
  - Learn [best practices for implementing custom-trained ML models on Gemini Enterprise Agent Platform](https://docs.cloud.google.com/architecture/ml-on-gcp-best-practices) .
