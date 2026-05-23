---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/migrate
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/migrate
title: Migrate data to a new Agent Platform Workbench instance
description: Migrate data and files from an existing Agent Platform Workbench instance to a new one
data_source: docs.cloud.google.com
---

# Migrate data to a new Agent Platform Workbench instance

This page describes how to migrate data and files from an existing Agent Platform Workbench instance to a new one.

## When to migrate

You might need to migrate your data to a new Agent Platform Workbench instance if you can't upgrade the environment of your existing instance. See the [requirements for upgrading the environment of a Agent Platform Workbench instance](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/upgrade#requirements) .

## Migration options

To migrate data and files from one Agent Platform Workbench instance to another, consider using the following methods:

  - **Use GitHub** : Copy your data and files to a GitHub repository by using the Git extension for JupyterLab.

  - **Use Cloud Storage and the terminal** : Copy your data and files to Cloud Storage and then to another instance by using the terminal.

  - **Use Cloud Storage within JupyterLab notebooks** : Copy your data and files to Cloud Storage and then to another instance by running commands within your respective instances' notebook cells.

This guide describes how to migrate data and files by using Cloud Storage and the terminal.

## Requirements

You must have terminal access to your Agent Platform Workbench instance. Terminal access is manually set when you create an instance. The terminal access setting cannot be changed after the instance is created.

## Before you begin

[Create a Cloud Storage bucket](https://docs.cloud.google.com/storage/docs/creating-buckets) in the same project where your Agent Platform Workbench instance is located.

## Migrate your data to a new Agent Platform Workbench instance

To migrate data and files to a new Agent Platform Workbench instance by using Cloud Storage and the terminal, complete the following steps.

1.  In your Agent Platform Workbench instance's JupyterLab interface, select **File \> New \> Terminal** to open a terminal window.

2.  Use the [gcloud CLI](https://docs.cloud.google.com/sdk/gcloud) to copy your user data to a Cloud Storage bucket. The following example command copies all of the files from your instance's `/home/jupyter/` directory to a directory in a Cloud Storage bucket.
    
        gcloud storage cp /home/jupyter/* gs://BUCKET_NAMEPATH --recursive
    
    Replace the following:
    
      - `  BUCKET_NAME  ` : the name of your Cloud Storage bucket
      - `  PATH  ` : the path to the directory where you want to copy your files, for example: `/copy/jupyter/`

3.  Open your Agent Platform Workbench instance's JupyterLab interface.

4.  In your Agent Platform Workbench instance's JupyterLab interface, select **File \> New \> Terminal** to open a terminal window.

5.  Use the gcloud CLI to restore your data on the new instance. The following example command copies all of the files from a Cloud Storage directory to the your new instance's `/home/jupyter/` directory.
    
        gcloud storage cp gs://BUCKET_NAMEPATH* /home/jupyter/

## What's next

  - Learn how to [upgrade the environment of Agent Platform Workbench instances](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/upgrade) .

  - Learn more about [using SSH access](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/ssh-access) to connect to your Agent Platform Workbench instance.
