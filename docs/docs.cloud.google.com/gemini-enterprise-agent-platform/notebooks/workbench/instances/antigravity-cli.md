---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/antigravity-cli
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/antigravity-cli
title: Use the Antigravity CLI with a Gemini Enterprise Agent Platform Workbench instance
description: Use the Antigravity CLI in an Agent Platform Workbench instance.
data_source: docs.cloud.google.com
---

# Use the Antigravity CLI

> **Preview**
>
> This feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](https://docs.cloud.google.com/terms/service-terms#1) . Pre-GA features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

This page describes how to use the Antigravity command line interface (CLI) with a Gemini Enterprise Agent Platform Workbench instance.

This document is intended for data analysts, data scientists, and data developers who work with Agent Platform Workbench. This document assumes you have knowledge of how to write code in a notebook environment.

## Overview

Antigravity CLI is the terminal-first surface of Google Antigravity, an AI coding agent that runs in a terminal. For more information, see [antigravity.google](https://antigravity.google/) .

The Antigravity CLI is available in a terminal in your Agent Platform Workbench instance's JupyterLab interface. You can use it to work with the notebooks and files on your instance, and to run shell commands and Google Cloud commands, by giving instructions in natural language.

Agent Platform Workbench adds the following to the Antigravity CLI:

- [Notebook skills](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/antigravity-cli#skills) that create, explain, edit, check, and run notebooks, and create Jupyter kernels.
- A [Google Cloud plugin](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/antigravity-cli#skills) with Google Cloud documentation and guidance for `gcloud` commands.
- The [`%%agy` cell magic](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/antigravity-cli#agy-magic) , which writes the code for a notebook cell from your description.

## Limitations

Consider the following limitations when you use the Antigravity CLI with Agent Platform Workbench:

- The Antigravity CLI is a CLI only. A graphical chat interface and advanced in-editor tools aren't included.

- When you ask the Antigravity CLI to modify a notebook, it changes the notebook file directly on the instance's disk. As a result, you can't undo edits made by the Antigravity CLI by using the notebook editor's **Undo** button or <span class="kbd"> Control+Z </span> ( <span class="kbd"> Command+Z </span> on macOS). However, you can ask the Antigravity CLI to undo a change by using a natural language command, such as `Undo your last change` .

- The Antigravity CLI writes directly to disk and can change files that you also have open in JupyterLab. **If you have unsaved changes in a notebook, save them before you ask the Antigravity CLI to modify that same notebook.**

- The Antigravity CLI is pinned to the version that is included in your instance's image, and it can't update itself. To use a newer version, upgrade your instance to a newer image version. For more information, see [Upgrade the environment of an instance](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/upgrade) .

- The Antigravity CLI runs with the credentials that are active on your instance. By default, these are your Agent Platform Workbench instance's service account credentials, so the Antigravity CLI can access the same resources the instance can. If you authenticate a different identity on the instance (for example, by running `gcloud auth login` or `gcloud auth application-default login` ), the Antigravity CLI uses that identity's permissions instead.

## Before you begin

> As an early-stage technology, Gemini for Google Cloud products can generate output that seems plausible but is factually incorrect. We recommend that you validate all output from Gemini for Google Cloud products before you use it. For more information, see [Gemini for Google Cloud and responsible AI](https://docs.cloud.google.com/gemini/docs/discover/responsible-ai) .

### Required roles

To use the Antigravity CLI in Agent Platform Workbench, you must grant permissions to the user of the Agent Platform Workbench instance and the instance's service account.

> **Note:** The Antigravity CLI operates strictly within the permissions of your Agent Platform Workbench instance's environment. If you (or the service account your instance uses) don't have permission to access a specific resource, the Antigravity CLI won't be able to access it either. If a command fails due to permissions, ask your administrator to grant the necessary permissions.

#### Grant permissions to the user of the instance

To get the permissions that you need to use the Antigravity CLI in a Agent Platform Workbench instance, ask your administrator to grant you the [Agent Platform User](https://docs.cloud.google.com/iam/docs/roles-permissions/aiplatform#aiplatform.user) ( `roles/aiplatform.user` ) IAM role on the project. For more information about granting roles, see [Manage access to projects, folders, and organizations](https://docs.cloud.google.com/iam/docs/granting-changing-revoking-access) .

You might also be able to get the required permissions through [custom roles](https://docs.cloud.google.com/iam/docs/creating-custom-roles) or other [predefined roles](https://docs.cloud.google.com/iam/docs/roles-overview#predefined) .

#### Grant a permission to your instance's service account

To ensure that your Agent Platform Workbench instance's service account has the necessary permission to enable the Antigravity CLI to run in a Agent Platform Workbench instance, ask your administrator to grant the [Agent Platform User](https://docs.cloud.google.com/iam/docs/roles-permissions/aiplatform#aiplatform.user) ( `roles/aiplatform.user` ) IAM role to your Agent Platform Workbench instance's service account on the project.

> **Important:** You must grant this role to your Agent Platform Workbench instance's service account, *not* to your user account. Failure to grant the role to the correct principal might result in permission errors.

For more information about granting roles, see [Manage access to projects, folders, and organizations](https://docs.cloud.google.com/iam/docs/granting-changing-revoking-access) .

This predefined role contains the `aiplatform.endpoints.predict` permission, which is required to enable the Antigravity CLI to run in a Agent Platform Workbench instance.

Your administrator might also be able to give your Agent Platform Workbench instance's service account this permission with [custom roles](https://docs.cloud.google.com/iam/docs/creating-custom-roles) or other [predefined roles](https://docs.cloud.google.com/iam/docs/roles-overview#predefined) .

### Enable the Antigravity CLI

The Antigravity CLI is available only on Agent Platform Workbench instances that use a Debian 12 ( `workbench-instances-2603` ) or later image. It isn't installed on instances that use the Debian 11 ( `workbench-instances` ) image.

New instances have the Antigravity CLI turned on by default. If you don't set the `enable-antigravity` instance metadata key when you create an instance, Agent Platform Workbench sets it to `true` .

To turn the Antigravity CLI off or on for an instance, set the `enable-antigravity` instance metadata key to `false` or `true` , and then stop and start the instance. The instance applies the setting when it starts. For more information, see [Manage features through metadata](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/manage-metadata) .

## Use the Antigravity CLI

1.  In the Google Cloud console, go to the **Instances** page.

2.  Next to a Agent Platform Workbench instance's name, click **Open JupyterLab** .

3.  In JupyterLab, click **File** \> **New launcher** .

4.  In the **Launcher** tab, in the **Other** section, click the **Antigravity CLI** tile.

    A terminal opens and starts the Antigravity CLI. You can also enter `agy` in any JupyterLab terminal.

5.  Enter a prompt, such as "Create a new notebook named 'test-notebook'". For more examples, see [Sample prompts](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/antigravity-cli#sample-prompts) .

6.  When the Antigravity CLI proposes an action, such as editing a file or running a shell command, review it and approve or reject it. For more information, see [Approve tool actions](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/antigravity-cli#tool-approval) .

## Notebook skills and the Google Cloud plugin

Skills are instructions and scripts that the Antigravity CLI uses for a type of task. When the Antigravity CLI is on, Agent Platform Workbench gives it the following notebook skills:

- **Notebook targeter:** finds the notebook that you have open in JupyterLab, so that you can refer to it as "this notebook".
- **Notebook explainer:** summarizes a notebook's cells and their text outputs.
- **Notebook modifier:** adds and edits cells. It changes only the target cell and keeps the notebook in the format that JupyterLab uses.
- **Notebook validator:** checks that a notebook is valid. It asks you before it repairs a notebook that was already invalid.
- **Notebook creator:** creates a notebook with a kernel that is available on the instance.
- **Notebook executor:** runs a notebook on the instance's kernels and saves the outputs. If a cell fails, it names the cell.
- **Kernel creator:** creates a Python environment and a Jupyter kernel with the packages that you ask for.

The Antigravity CLI also comes with the `google-cloud-developer` plugin from the [Antigravity plugin marketplace](https://github.com/google/skills) . The plugin gives the Antigravity CLI guidance for `gcloud` commands, help with authentication, Google Cloud documentation, and skills for products such as Cloud Logging, Cloud Monitoring, and Agent Platform.

The Antigravity CLI uses a skill or the plugin when your prompt needs it. You don't have to name them in your prompt.

## Sample prompts

To get ideas for how to use the Antigravity CLI, see the following sample prompts:

- "Explain this notebook."

- "Add a cell to this notebook that plots the distribution of the 'age' column."

- "Create a notebook that loads bigquery-public-data.ml_datasets.census_adult_income into a pandas DataFrame, and then run it."

- "Create a kernel named 'forecast' with pandas and prophet."

- "Check that every notebook in this directory is a valid notebook."

- "Query the bigquery-public-data.ml_datasets.census_adult_income table to find the number of people with an income bracket of \>50K."

## Use the `%%agy` cell magic

To have the Antigravity CLI write the code for a cell in your notebook, do the following:

1.  On the first line of a new cell in a Python notebook, enter `%%agy` .
2.  On the next lines of the same cell, describe the code that you want.
3.  Run the cell.

The Antigravity CLI adds a new cell below with the code. Review the code before you run it.

The `%%agy` cell magic is designed strictly for generating code. Unlike the terminal interface, the cell magic can't prompt you for approval, so it automatically refuses any action that requires approval, such as running a shell command.

The `%%agy` cell magic is available whenever the Antigravity CLI is enabled.

## Approve tool actions

By default, the Antigravity CLI in Agent Platform Workbench asks for your approval before it takes any action, such as editing a file, running a shell command, or fetching a URL. Review each proposed action before you approve it.

This default protects against prompt injection. A notebook, script, or web page that the Antigravity CLI reads could contain hidden instructions that attempt to make the agent run commands you didn't intend, such as sending your data to an external address. The Antigravity CLI runs with your instance's credentials, so requiring approval gives you the opportunity to see and stop such an action before it runs.

For this reason, the option to skip approval prompts is disabled for the Antigravity CLI on Agent Platform Workbench instances.

## Control access to the Antigravity CLI

You can control access to the Antigravity CLI in Agent Platform Workbench by using the following methods:

- An administrator can set the `enable-antigravity` instance metadata key to `false` . The **Antigravity CLI** tile, the notebook skills, the plugin, and the `%%agy` cell magic are then removed at the next start of the instance. The `agy` command stays installed. To prevent model calls, use the methods that follow.

- An administrator can set up an organization policy to restrict usage of specific models at an organization, folder, or project level. See [Control access to Model Garden models](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/control-model-access) .

- By not granting the `aiplatform.endpoints.predict` permission, an administrator can block some identities from being able to use model endpoints for inference.

## What's next

- Learn more about [Gemini Enterprise Agent Platform](https://docs.cloud.google.com/gemini-enterprise-agent-platform/overview) .

- To learn how to set instance metadata, see [Manage features through metadata](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/manage-metadata) .
