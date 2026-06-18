---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/create-specific-version
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/create-specific-version
title: Create a specific version of a Agent Platform Workbench instance
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

This page describes how to create a specific version of a Gemini Enterprise Agent Platform Workbench instance.

## Why you might want to create a specific version

To ensure that your Agent Platform Workbench instance has software that is compatible with your code or application, you might want to create a specific version.

Agent Platform Workbench instance images are updated frequently, and specific versions of preinstalled software and packages vary from version to version.

To learn more about specific Agent Platform Workbench versions, see the [Agent Platform release notes](https://docs.cloud.google.com/vertex-ai/docs/release-notes) .

After you create a specific version of a Agent Platform Workbench instance, you can upgrade it. Upgrading the instance updates the preinstalled software and packages. For more information, see [Upgrade an instance's environment](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/upgrade) .

## Before you begin

## Create a specific version

You can create a specific version of a Agent Platform Workbench instance by using the Google Cloud console or the Google Cloud CLI.

### Console

To create a specific version of a Agent Platform Workbench instance, do the following:

1.  When you [create an instance](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/create) , in the **Environment** section, select **Use a previous version** .

2.  Click the **Version** list, and select a version. Versions are numbered in the form of an `M` followed by the number of the release, for example, `M123` .

3.  Complete the rest of the instance-creation dialog, and then click **Create** .
    
    Agent Platform Workbench creates an instance and automatically starts it. When the instance is ready to use, Agent Platform Workbench activates an **Open JupyterLab** link.

### gcloud

Before using any of the command data below, make the following replacements:

  - `  INSTANCE_NAME  ` : the name of your Agent Platform Workbench instance; must start with a letter followed by up to 62 lowercase letters, numbers, or hyphens (-), and cannot end with a hyphen

  - `  PROJECT_ID  ` : your project ID

  - `  LOCATION  ` : the zone where you want your instance to be located

  - `  VM_IMAGE_NAME  ` : the image name; to get a list of the available image names, use the [`get-config` command](https://docs.cloud.google.com/sdk/gcloud/reference/workbench/instances/get-config)

  - `  MACHINE_TYPE  ` : the [machine type](https://docs.cloud.google.com/compute/docs/machine-resource) of your instance's VM

  - `  METADATA  ` : custom metadata to apply to this instance; for example, to specify a post-startup-script, you can use the `post-startup-script` metadata tag, in the format: `--metadata=post-startup-script=gs:// BUCKET_NAME /hello.sh`
    
    > To enable the JupyterLab 4 preview, use `--metadata=enable-jupyterlab4-preview=true` . For more information, see [JupyterLab 4 preview](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/create#jupyterlab-preview) .

Execute the following command:

#### Linux, macOS, or Cloud Shell

> **Note:** Ensure you have initialized the Google Cloud CLI with authentication and a project by running either [gcloud init](https://docs.cloud.google.com/sdk/gcloud/reference/init) ; or [gcloud auth login](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) and [gcloud config set project](https://docs.cloud.google.com/sdk/gcloud/reference/config/set) .

    gcloud workbench instances create INSTANCE_NAME \
        --project=PROJECT_ID \
        --location=LOCATION \
        --vm-image-project="cloud-notebooks-managed" \
        --vm-image-name=VM_IMAGE_NAME \
        --machine-type=MACHINE_TYPE \
        --metadata=METADATA

#### Windows (PowerShell)

> **Note:** Ensure you have initialized the Google Cloud CLI with authentication and a project by running either [gcloud init](https://docs.cloud.google.com/sdk/gcloud/reference/init) ; or [gcloud auth login](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) and [gcloud config set project](https://docs.cloud.google.com/sdk/gcloud/reference/config/set) .

    gcloud workbench instances create INSTANCE_NAME `
        --project=PROJECT_ID `
        --location=LOCATION `
        --vm-image-project="cloud-notebooks-managed" `
        --vm-image-name=VM_IMAGE_NAME `
        --machine-type=MACHINE_TYPE `
        --metadata=METADATA

#### Windows (cmd.exe)

> **Note:** Ensure you have initialized the Google Cloud CLI with authentication and a project by running either [gcloud init](https://docs.cloud.google.com/sdk/gcloud/reference/init) ; or [gcloud auth login](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) and [gcloud config set project](https://docs.cloud.google.com/sdk/gcloud/reference/config/set) .

    gcloud workbench instances create INSTANCE_NAME ^
        --project=PROJECT_ID ^
        --location=LOCATION ^
        --vm-image-project="cloud-notebooks-managed" ^
        --vm-image-name=VM_IMAGE_NAME ^
        --machine-type=MACHINE_TYPE ^
        --metadata=METADATA

For more information about the command for creating an instance from the command line, see the [gcloud CLI documentation](https://docs.cloud.google.com/sdk/gcloud/reference/workbench/instances/create) .

Agent Platform Workbench creates an instance and automatically starts it. When the instance is ready to use, Agent Platform Workbench activates an **Open JupyterLab** link in the Google Cloud console.

## What's next

  - Learn more about [upgrading Agent Platform Workbench instances](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/upgrade) to ensure that your instance upgrades only when you are ready.

  - Learn about [monitoring the health status](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/monitor-health) of your Agent Platform Workbench instance.
