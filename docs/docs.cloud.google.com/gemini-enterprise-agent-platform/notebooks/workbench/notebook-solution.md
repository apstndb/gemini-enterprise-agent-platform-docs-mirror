---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/notebook-solution
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/notebook-solution
title: Choose a notebook solution
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

This page describes the differences between Gemini Enterprise Agent Platform's notebook environment options so that you can choose the best one for your project.

Agent Platform provides two notebook environment solutions:

  - **Colab Enterprise:** A collaborative, managed notebook environment with the security and compliance capabilities of Google Cloud. If your project's priorities are to collaborate with others and to avoid spending time managing infrastructure, Colab Enterprise might be the best option for you. See the following [Colab Enterprise](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/notebook-solution#colab-enterprise) section.

  - **Gemini Enterprise Agent Platform Workbench:** A Jupyter notebook-based environment provided through virtual machine (VM) instances with features that support the entire data science workflow. If your project's priorities are control and customizability, Agent Platform Workbench might be the best option for you. See the following [Agent Platform Workbench](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/notebook-solution#agent-platform-workbench) section.

## Colab Enterprise

Learn about a few of Colab Enterprise's strengths in the sections that follow. For more information, see [Introduction to Colab Enterprise](https://docs.cloud.google.com/colab/docs/introduction) .

### Share and collaborate

Colab Enterprise lets you share notebooks and collaborate with others. You can share a notebook with a single user, Google group, or Google Workspace domain. You control this access through Identity and Access Management (IAM).

### Managed compute

Colab Enterprise lets you work in notebooks without having to manage infrastructure. Colab Enterprise provisions a runtime for you when you need it. If you want to, you can configure runtimes for specific needs, but Colab Enterprise starts them for you and shuts them down when you no longer need them.

### Integrated into the Google Cloud console

Colab Enterprise's integrations with Google Cloud services make it easier to use notebooks that interact with those services. You can use Colab Enterprise from within the Google Cloud console, with features built into both Agent Platform and BigQuery.

### Write code with Gemini assistance

> **Preview**
> 
> This feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](https://docs.cloud.google.com/terms/service-terms#1) . Pre-GA features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

You can use Gemini in Agent Platform, which is a product in the [Gemini for Google Cloud](https://docs.cloud.google.com/gemini/docs/overview) portfolio, to help you write and generate code in a Gemini Enterprise Agent Platform notebook. Gemini in Agent Platform can generate code completion suggestions while you type in a code cell. You can also use the **Help me code** tool to generate code based on a description of what you want. To learn more, see [Write code with Gemini assistance](https://docs.cloud.google.com/colab/docs/use-code-completion) .

## Agent Platform Workbench

Learn about a few of Agent Platform Workbench's strengths in the sections that follow. For more information, see [Introduction to Agent Platform Workbench](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/introduction) .

### Overview

All Agent Platform Workbench instances provide the following:

  - Prepackaged with [JupyterLab](https://jupyterlab.readthedocs.io/en/stable/getting_started/overview.html) .
  - A preinstalled suite of deep learning packages, including support for the TensorFlow and PyTorch frameworks.
  - Support for GPU accelerators.
  - The ability to sync with a [GitHub](https://github.com/) repository.
  - Google Cloud authentication and authorization.

### Add conda environments

Agent Platform Workbench instances use [kernels](https://jupyterlab.readthedocs.io/en/stable/user/documents_kernels.html) based on conda environments. You can add a conda environment to your Agent Platform Workbench instance, and the environment appears as a kernel in your instance's JupyterLab interface.

Adding conda environments lets you use kernels that aren't available in the default Agent Platform Workbench instance. For example, you can add conda environments for R and Apache Beam. Or you can add conda environments for specific earlier versions of the available frameworks, such as TensorFlow, PyTorch, or Python.

For more information, see [Add a conda environment](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/add-environment) .

### Access to data

You can work more efficiently by accessing your data without leaving the JupyterLab interface.

From within JupyterLab's navigation menu on a Agent Platform Workbench instance, you can [use the Cloud Storage integration](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/cloud-storage) to browse data and other files that you have access to.

Also from within the navigation menu, you can [use the BigQuery integration](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/bigquery) to browse tables that you have access to, write queries, preview results, and load data into your notebook.

### Automated notebook runs

You can [set a notebook to run on a recurring schedule](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/schedule-notebook-run-quickstart) . Even while your instance is shut down, Gemini Enterprise Agent Platform Workbench will run your notebook file and save the results for you to look at and share with others.

### Automated shutdown for idle instances

To help manage costs, you can set your Agent Platform Workbench instance to shut down after being idle for a specific time period. For more information, see [Idle shutdown](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/idle-shutdown) .

### Custom containers

You can create a Agent Platform Workbench instance based on a custom container. Start with a Google-provided base container image, and modify it for your needs. Then create an instance based on your custom container.

For more information, see [Create an instance using a custom container](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/create-custom-container) .

### Use third party credentials

You can create and manage Gemini Enterprise Agent Platform Workbench instances with third party credentials provided by Workforce Identity Federation. Workforce Identity Federation uses your external identity provider (IdP) to grant a group of users access to Agent Platform Workbench instances through a proxy.

For more information, see [Create an instance with third party credentials](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/create-third-party-instance) .

### Health status monitoring

To help ensure that your Agent Platform Workbench instance is working properly, you can [monitor the health status](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/monitor-health) .

### Editable Deep Learning VM instances

Agent Platform Workbench provides API methods for modifying the underlying VM through the Notebooks API.

> **Note:** You can't edit the underlying VM of an instance by using the Google Cloud console or the Compute Engine API.

## What's next

To get started:

  - [Create a Colab Enterprise notebook](https://docs.cloud.google.com/colab/docs/create-console-quickstart) .

  - [Create a Agent Platform Workbench instance](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/create) .
