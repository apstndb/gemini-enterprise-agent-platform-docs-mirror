---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/gemini-cli
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/gemini-cli
title: Use the Gemini CLI with a Gemini Enterprise Agent Platform Workbench instance
description: Use the Gemini CLI in a Agent Platform Workbench instance.
data_source: docs.cloud.google.com
---

# Use the Gemini CLI

> **Preview**
> 
> This feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](https://docs.cloud.google.com/terms/service-terms#1) . Pre-GA features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

This page describes how to use the Gemini command line interface (CLI) with a Gemini Enterprise Agent Platform Workbench instance.

This document is intended for data analysts, data scientists, and data developers who work with Agent Platform Workbench. This document assumes you have knowledge of how to write code in a notebook environment.

## Overview

The Gemini CLI is an open source AI agent that provides access to Gemini directly in a terminal. For more information, see [geminicli.com](https://geminicli.com/) .

The Gemini CLI is available in Agent Platform Workbench instances. You can use the Gemini CLI to do the following:

  - Create a new notebook.
  - Run notebook cells.
  - Write and edit a notebook's code and text cells.
  - Explain code and technical concepts.
  - Interact with a Agent Platform Workbench instance's local file system, including performing complex file operations that span multiple files based on a single, high-level instruction.
  - Run basic shell commands.
  - Run commands to interact with other Google Cloud services, such as Gemini Enterprise Agent Platform and BigQuery.

## Limitations

Consider the following limitations when you use the Gemini CLI with Agent Platform Workbench:

  - The Gemini CLI is a CLI only. A graphical chat interface and advanced in-editor tools aren't included.

  - When you ask Gemini CLI to modify a notebook, the Gemini CLI changes the notebook file directly on the instance's disk. Because of this, you can't undo edits made by the Gemini CLI by using the notebook editor's **Undo** button or Control+Z ( Command+Z on macOS). However, you can ask the Gemini CLI to undo a change by using a natural language command, such as `Undo your last change` .

## Before you begin

> As an early-stage technology, Gemini for Google Cloud products can generate output that seems plausible but is factually incorrect. We recommend that you validate all output from Gemini for Google Cloud products before you use it. For more information, see [Gemini for Google Cloud and responsible AI](https://docs.cloud.google.com/gemini/docs/discover/responsible-ai) .

### Required roles

To use the Gemini CLI in Agent Platform Workbench, you must grant permissions to the user of the Agent Platform Workbench instance and the instance's service account.

> **Note:** The Gemini CLI operates strictly within the permissions of your Agent Platform Workbench instance's environment. If you (or the service account your instance uses) don't have permission to access a specific resource, Gemini CLI won't be able to access it either. If a command fails due to permissions, ask your administrator to grant the necessary permissions.

#### Grant permissions to the user of the instance

To get the permissions that you need to use the Gemini CLI in a Agent Platform Workbench instance, ask your administrator to grant you the [Agent Platform User](https://docs.cloud.google.com/iam/docs/roles-permissions/aiplatform#aiplatform.user) ( `roles/aiplatform.user)` IAM role on the project. For more information about granting roles, see [Manage access to projects, folders, and organizations](https://docs.cloud.google.com/iam/docs/granting-changing-revoking-access) .

You might also be able to get the required permissions through [custom roles](https://docs.cloud.google.com/iam/docs/creating-custom-roles) or other [predefined roles](https://docs.cloud.google.com/iam/docs/roles-overview#predefined) .

#### Grant a permission to your instance's service account

To ensure that your Agent Platform Workbench instance's service account has the necessary permission to enable the Gemini CLI to run in a Agent Platform Workbench instance, ask your administrator to grant the [Agent Platform User](https://docs.cloud.google.com/iam/docs/roles-permissions/aiplatform#aiplatform.user) ( `roles/aiplatform.user)` IAM role to your Agent Platform Workbench instance's service account on the project.

> **Important:** You must grant this role to your Agent Platform Workbench instance's service account, *not* to your user account. Failure to grant the role to the correct principal might result in permission errors.

For more information about granting roles, see [Manage access to projects, folders, and organizations](https://docs.cloud.google.com/iam/docs/granting-changing-revoking-access) .

This predefined role contains the `aiplatform.endpoints.predict` permission, which is required to enable the Gemini CLI to run in a Agent Platform Workbench instance.

Your administrator might also be able to give your Agent Platform Workbench instance's service account this permission with [custom roles](https://docs.cloud.google.com/iam/docs/creating-custom-roles) or other [predefined roles](https://docs.cloud.google.com/iam/docs/roles-overview#predefined) .

## Use the Gemini CLI

1.  In the Google Cloud console, go to the **Instances** page.

2.  Next to a Agent Platform Workbench instance's name, click **Open JupyterLab** .
    
    Your Agent Platform Workbench instance opens JupyterLab.

3.  In JupyterLab, click **File** \> **New launcher** .

4.  In the **Launcher** tab, in the **Other** section, click the **Gemini CLI** tile.

5.  If it's the first time you've opened a Gemini CLI terminal, enter `Y` to agree to the terms and conditions.
    
    Your Agent Platform Workbench instance installs the Gemini CLI.

6.  In the Gemini CLI terminal, enter a prompt.
    
    For example, you might enter `Create a new notebook named 'test-notebook'` . To see examples of prompts that might be helpful, see [Sample prompts](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/gemini-cli#sample-prompts) .

## Sample prompts

To help you get ideas for how to use the Gemini CLI, see the following sample prompts:

  - "Create a new notebook that trains a model to predict 'income bracket' from bigquery-public-data.ml\_datasets.census\_adult\_income, using BigQuery and Python."

  - "Summarize the notebook named 'test-file', and propose next steps for the project."

  - "I want to get a quick overview of the notebooks in this directory. For every .ipynb file, show me the first 5 lines of the file."

  - "Create a script using the contents of the 'test-file' notebook."

  - "Show me how to access data from BigQuery tables from within Agent Platform Workbench."

  - "Query the bigquery-public-data.ml\_datasets.census\_adult\_income table to find the number of people with an income bracket of \> 50K."

  - "Set my default Google Cloud project to my-project."

  - "Create a Cloud Storage bucket, and upload all the CSV files from my current directory to it."

  - "Create a Compute Engine instance with a Debian 11 image and an n1-standard-4 machine type."

  - "Create a notebook file that runs through the code in the 'test-script'. Add text cells that explain the code."

## Control access to the Gemini CLI

You can control access to the Gemini CLI in Agent Platform Workbench by using the following methods:

  - An administrator can set up an organization policy to restrict usage of specific Gemini models at an organization, folder, or project level. See [Control access to Model Garden models](https://docs.cloud.google.com/gemini-enterprise-agent-platform/generative-ai/docs/control-model-access) . The Gemini CLI continues to appear in JupyterLab, but the CLI doesn't respond to prompts.

  - By not granting the `aiplatform.endpoints.predict` permission, an administrator can block some identities from being able to use Gemini endpoints for inference.

## Use the Gemini CLI magic command

To use the Gemini CLI directly within a cell in your notebook file, do the following:

1.  Ensure that the Gemini CLI is enabled and the user or creator has agreed to the terms and conditions.
2.  On the first line of a new cell, enter `%%geminicli_magic` .
3.  In the same cell, enter your prompt on the following line.
4.  Run the cell.

The Gemini CLI adds a new cell below with its response.

## Troubleshoot

If you encounter a problem using the Gemini CLI with Agent Platform Workbench instances, see [Troubleshooting Agent Platform Workbench](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/troubleshooting-workbench#gemini-cli) for help with common issues.

## What's next

  - Learn more about [Gemini](https://docs.cloud.google.com/gemini/docs/overview) .

  - To learn about methods for querying BigQuery data in Agent Platform Workbench notebooks, see [Query data in BigQuery from within JupyterLab](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/bigquery) .
