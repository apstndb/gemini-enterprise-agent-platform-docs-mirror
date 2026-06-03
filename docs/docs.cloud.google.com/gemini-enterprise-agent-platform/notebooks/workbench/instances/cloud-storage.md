---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/cloud-storage
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/cloud-storage
title: Access Cloud Storage buckets and files in JupyterLab in a Agent Platform Workbench instance.
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

This page shows you how to mount a Cloud Storage bucket to the JupyterLab interface of your Gemini Enterprise Agent Platform Workbench instance so that you can browse files that are stored in Cloud Storage. You can also open and edit files that are compatible with JupyterLab, such as text files and notebook (IPYNB) files.

## Overview

Agent Platform Workbench instances include a Cloud Storage integration that lets you mount a Cloud Storage bucket. This means you can browse the contents of the bucket and work with compatible files from within the JupyterLab interface.

You can access any of the Cloud Storage buckets and files that your instance has access to within the same project as your Agent Platform Workbench instance.

> **Note:** Your Agent Platform Workbench instance's access to Cloud Storage is determined by the single user or service account that you used to grant access to your instance. For example, if you granted a specific service account access to your instance, you must also grant that service account access to the Cloud Storage buckets that you want to use in JupyterLab.

## Before you begin

### Required roles

To get the permissions that you need to mount a Cloud Storage bucket to a Agent Platform Workbench instance, ask your administrator to grant you the following IAM roles:

  - [Notebooks Runner](https://docs.cloud.google.com/iam/docs/roles-permissions/notebooks#notebooks.runner) ( `roles/notebooks.runner` ) on the project
  - [Storage Object User](https://docs.cloud.google.com/iam/docs/roles-permissions/storage#storage.objectUser) ( `roles/storage.objectUser` ) on the Agent Platform Workbench instance's service account

For more information about granting roles, see [Manage access to projects, folders, and organizations](https://docs.cloud.google.com/iam/docs/granting-changing-revoking-access) .

You might also be able to get the required permissions through [custom roles](https://docs.cloud.google.com/iam/docs/creating-custom-roles) or other [predefined roles](https://docs.cloud.google.com/iam/docs/roles-overview#predefined) .

### Required permission for enabling shared storage mounting

To enable shared storage mounting in your Agent Platform Workbench instance, ask your administrator to grant your Agent Platform Workbench instance's service account the `storage.buckets.list` permission on the project.

The `storage.buckets.list` permission is required for the **Mount shared storage** button to appear in the JupyterLab interface of your Agent Platform Workbench instance.

## Create a bucket and a Agent Platform Workbench instance

You must have access to at least one Cloud Storage bucket in the same project as your Agent Platform Workbench instance.

1.  If you need to create a Cloud Storage bucket, see [Create a bucket](https://docs.cloud.google.com/storage/docs/creating-buckets) .
2.  If you haven't already, [create a Agent Platform Workbench instance](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/create) in the same project as your Cloud Storage bucket.

## Open JupyterLab

1.  In the Google Cloud console, go to the **Instances** page.

2.  Next to your Agent Platform Workbench instance's name, click **Open JupyterLab** .
    
    Your Agent Platform Workbench instance opens JupyterLab.

## Mount the Cloud Storage bucket

To mount and then access a Cloud Storage bucket, do the following:

1.  In JupyterLab, make sure the folder **File Browser** tab is selected.

2.  In the left sidebar, click the ![Mount shared storage button](https://docs.cloud.google.com/static/gemini-enterprise-agent-platform/notebooks/workbench/images/icon-mount-shared-storage.png) **Mount shared storage** button. If you don't see the button, drag the right side of the sidebar to expand the sidebar until you see the button.
    
    ![The Mount shared storage button in the top right corner of the left sidebar](https://docs.cloud.google.com/static/gemini-enterprise-agent-platform/notebooks/workbench/instances/images/mount-shared-storage-button.png)

3.  In the **Bucket name** field, enter the Cloud Storage bucket name that you want to mount.

4.  Click **Mount** .

5.  Your Cloud Storage bucket appears as a folder in the **File browser** tab of the left sidebar. Double-click the folder to open it and browse the contents.

## Troubleshoot

To find methods for diagnosing and resolving issues with mounting a Cloud Storage bucket to your instance, see [Troubleshooting Agent Platform Workbench](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/troubleshooting-workbench#instances) .

## What's next

  - Learn more about [Cloud Storage](https://docs.cloud.google.com/storage/docs/introduction) .

  - Learn how to [query data in BigQuery from within JupyterLab](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/bigquery) .
