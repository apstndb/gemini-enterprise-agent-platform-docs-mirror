---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/opencode-cli
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/opencode-cli
title: Use the OpenCode CLI with a Gemini Enterprise Agent Platform Workbench instance
description: Use the OpenCode CLI in an Agent Platform Workbench instance.
data_source: docs.cloud.google.com
---

# Use the OpenCode CLI

> **Preview**
> 
> This feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](https://docs.cloud.google.com/terms/service-terms#1) . Pre-GA features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

This page describes how to use the OpenCode command line interface (CLI) with a Gemini Enterprise Agent Platform Workbench instance.

This document is intended for data analysts, data scientists, and data developers who work with Agent Platform Workbench. This document assumes you have knowledge of how to write code in a notebook environment.

## Overview

OpenCode is an open source AI coding agent that runs in a terminal. For more information, see [opencode.ai](https://opencode.ai/) .

When an administrator enables it, the OpenCode CLI is available in a terminal in your Agent Platform Workbench instance's JupyterLab interface. You can use it to work with the notebooks and files on your instance, and to run shell commands and Google Cloud commands, by giving instructions in natural language.

## Limitations

Consider the following limitations when you use the OpenCode CLI with Agent Platform Workbench:

  - OpenCode is a CLI only. A graphical chat interface and advanced in-editor tools aren't included.

  - When you ask OpenCode to modify a notebook, OpenCode changes the notebook file directly on the instance's disk. Because of this, you can't undo edits made by OpenCode by using the notebook editor's **Undo** button or Control+Z ( Command+Z on macOS). However, you can ask OpenCode to undo a change by using a natural language command, such as `Undo your last change` .

  - Because OpenCode writes directly to disk, it can change a file that you also have open in JupyterLab. **If you have unsaved changes in a notebook, save them before you ask OpenCode to modify that same notebook.**

  - OpenCode runs with the credentials that are active on your instance. By default, these are your Agent Platform Workbench instance's service account credentials, so OpenCode can access the same resources the instance can. If you authenticate a different identity on the instance (for example, by running `gcloud auth login` or `gcloud auth application-default login` ), OpenCode uses that identity's permissions instead.

## Before you begin

> As an early-stage technology, Gemini for Google Cloud products can generate output that seems plausible but is factually incorrect. We recommend that you validate all output from Gemini for Google Cloud products before you use it. For more information, see [Gemini for Google Cloud and responsible AI](https://docs.cloud.google.com/gemini/docs/discover/responsible-ai) .

### Required roles

To use the OpenCode CLI in Agent Platform Workbench, you must grant permissions to the user of the Agent Platform Workbench instance and the instance's service account.

> **Note:** OpenCode operates strictly within the permissions of your Agent Platform Workbench instance's environment. If you (or the service account your instance uses) don't have permission to access a specific resource, OpenCode won't be able to access it either. If a command fails due to permissions, ask your administrator to grant the necessary permissions.

#### Grant permissions to the user of the instance

To get the permissions that you need to use the OpenCode CLI in a Agent Platform Workbench instance, ask your administrator to grant you the [](https://docs.cloud.google.com/iam/docs/roles-permissions/aiplatform#aiplatform.user) [Agent Platform User](https://docs.cloud.google.com/iam/docs/roles-permissions/aiplatform#aiplatform.user) ( `roles/aiplatform.user` ) IAM role on the project. For more information about granting roles, see [Manage access to projects, folders, and organizations](https://docs.cloud.google.com/iam/docs/granting-changing-revoking-access) .

You might also be able to get the required permissions through [custom roles](https://docs.cloud.google.com/iam/docs/creating-custom-roles) or other [predefined roles](https://docs.cloud.google.com/iam/docs/roles-overview#predefined) .

#### Grant a permission to your instance's service account

To ensure that your Agent Platform Workbench instance's service account has the necessary permission to enable the OpenCode CLI to run in a Agent Platform Workbench instance, ask your administrator to grant the [](https://docs.cloud.google.com/iam/docs/roles-permissions/aiplatform#aiplatform.user) [Agent Platform User](https://docs.cloud.google.com/iam/docs/roles-permissions/aiplatform#aiplatform.user) ( `roles/aiplatform.user` ) IAM role to your Agent Platform Workbench instance's service account on the project.

> **Important:** You must grant this role to your Agent Platform Workbench instance's service account, *not* to your user account. Failure to grant the role to the correct principal might result in permission errors.

For more information about granting roles, see [Manage access to projects, folders, and organizations](https://docs.cloud.google.com/iam/docs/granting-changing-revoking-access) .

This predefined role contains the `aiplatform.endpoints.predict` permission, which is required to enable the OpenCode CLI to run in a Agent Platform Workbench instance.

Your administrator might also be able to give your Agent Platform Workbench instance's service account this permission with [custom roles](https://docs.cloud.google.com/iam/docs/creating-custom-roles) or other [predefined roles](https://docs.cloud.google.com/iam/docs/roles-overview#predefined) .

### Enable the OpenCode CLI

The OpenCode CLI is available only on Agent Platform Workbench instances that use the Debian 12 ( `workbench-instances-2603` ) image. It isn't installed on instances that use the Debian 11 ( `workbench-instances` ) image.

The OpenCode CLI is turned on by default on supported instances. To turn it off, set the `enable-opencode` instance metadata key to `false` . For more information, see [Manage features through metadata](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/manage-metadata) .

## Use the OpenCode CLI

1.  In the Google Cloud console, go to the **Instances** page.

2.  Next to a Agent Platform Workbench instance's name, click **Open JupyterLab** .

3.  In JupyterLab, click **File** \> **New launcher** .

4.  In the **Launcher** tab, in the **Other** section, click the **OpenCode** tile.
    
    A terminal opens and starts the OpenCode CLI.

5.  Enter a prompt, such as "Create a new notebook named 'test-notebook'".

6.  When OpenCode proposes an action, such as editing a file or running a shell command, review it and approve or reject it. For more information, see [Approve tool actions](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/opencode-cli#tool-approval) .

## Approve tool actions

By default, OpenCode in Agent Platform Workbench asks for your approval before it takes any action, such as editing a file, running a shell command, or fetching a URL. Review each proposed action before you approve it.

This default protects against prompt injection. A notebook, script, or web page that OpenCode reads could contain hidden instructions that attempt to make the agent run commands you didn't intend, such as sending your data to an external address. Because OpenCode runs with your instance's credentials, requiring approval gives you the opportunity to see and stop such an action before it runs.

> **Caution:** You can change this behavior in your own OpenCode configuration, including turning off approval prompts entirely. If you do, OpenCode runs actions without asking you first, and you accept the resulting risk of prompt injection and data exfiltration for your workloads.

## Use third-party models

By default, OpenCode in Agent Platform Workbench is configured to use only the Gemini and Claude models served through Gemini Enterprise Agent Platform in your project. These requests are authenticated with your instance's credentials against your project's own Gemini Enterprise Agent Platform, so they stay within your Google Cloud project and remain subject to the security controls that apply to it.

OpenCode also supports model providers whose requests are sent outside your project. These include Google AI Studio (the Gemini Developer API), which despite offering Gemini models is a separate service that authenticates with a personal API key rather than your project's credentials, as well as non-Google providers such as OpenAI and Anthropic's direct APIs. All of these are turned off by default. You can turn one on by editing your own OpenCode configuration and supplying the provider's API key.

> **Warning:** If you enable one of these providers, your prompts—and any data contained in them, including data read from your notebooks and files—are sent to that provider's external API. **This data leaves the confines of your Google Cloud project.** It is no longer protected by the security controls that apply within your project, including [Model Armor](https://docs.cloud.google.com/security-command-center/docs/model-armor-overview) protection against prompt injection, if you have configured it. Enabling such a provider is your decision and your responsibility, including compliance with any data handling agreement you have with that provider.

## Control access to the OpenCode CLI

Access to OpenCode is governed by two independent controls: whether the OpenCode launcher is shown, and whether the underlying models can be called. These are separate—hiding the launcher doesn't block the models, and restricting the models doesn't remove the launcher—so configure both to match your organization's policy.

### Control whether the OpenCode launcher appears

To control whether OpenCode is offered on an instance, use the `enable-opencode` instance metadata key. OpenCode is on by default: the OpenCode tile appears in the JupyterLab launcher unless an administrator sets the key to `false` , which hides it.

This setting controls only whether the launcher is presented. It doesn't, by itself, block access to the models: a user who can reach the instance's environment (for example, through a terminal) can still start OpenCode and call any models that their credentials are allowed to use. To restrict what OpenCode can do, control access to the models as described in the next section.

### Control access to the models

OpenCode calls models through Gemini Enterprise Agent Platform using your instance's credentials—the same Gemini Enterprise Agent Platform authentication that the Gemini CLI uses. Users don't enter an API key to use the default Gemini and Claude models; a request succeeds only if the instance's identity is permitted to call the model and the project has access to it. This control determines whether OpenCode can generate responses, and it applies however OpenCode is started.

To manage model access, use the same controls that apply to any Gemini Enterprise Agent Platform client:

  - To allow or restrict specific models at an organization, folder, or project level, set up an organization policy. See [Control access to Model Garden models](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/control-model-access) .

  - To block an identity from using model endpoints for inference, don't grant it the `aiplatform.endpoints.predict` permission.

  - Models from providers outside your project (for example, Anthropic's direct API) require the user to supply that provider's API key in their own OpenCode configuration, and are turned off by default. For more information, see [Use third-party models](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/opencode-cli#third-party-models) .

## What's next

  - Learn more about [Gemini Enterprise Agent Platform](https://docs.cloud.google.com/gemini-enterprise-agent-platform/docs/overview) .

  - To learn how to set instance metadata, see [Manage features through metadata](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/manage-metadata) .
