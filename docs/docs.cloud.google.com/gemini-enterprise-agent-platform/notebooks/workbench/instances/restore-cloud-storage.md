---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/restore-cloud-storage
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/restore-cloud-storage
title: Back up and restore files by using Cloud Storage
description: Back up and restore files on a Agent Platform Workbench instance by using Cloud Storage.
data_source: docs.cloud.google.com
---

# Back up and restore files by using Cloud Storage

This page describes how to use Cloud Storage to back up and restore files on your Gemini Enterprise Agent Platform Workbench instance.

## Overview

This guide describes two ways to use Cloud Storage to help you back up and restore files on your Agent Platform Workbench instance:

  - [Mount a Cloud Storage bucket](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/restore-cloud-storage#mount-bucket) to your Agent Platform Workbench instance.

  - [Export your files to Cloud Storage](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/restore-cloud-storage#export-to-storage) and then restore them.

## Before you begin

### Required roles

To get the permissions that you need to mount a Cloud Storage bucket to a Agent Platform Workbench instance, ask your administrator to grant you the following IAM roles:

  - [Notebooks Runner](https://docs.cloud.google.com/iam/docs/roles-permissions/notebooks#notebooks.runner) ( `roles/notebooks.runner` ) on the project
  - [Storage Object User](https://docs.cloud.google.com/iam/docs/roles-permissions/storage#storage.objectUser) ( `roles/storage.objectUser` ) on the Agent Platform Workbench instance's service account

For more information about granting roles, see [Manage access to projects, folders, and organizations](https://docs.cloud.google.com/iam/docs/granting-changing-revoking-access) .

You might also be able to get the required permissions through [custom roles](https://docs.cloud.google.com/iam/docs/creating-custom-roles) or other [predefined roles](https://docs.cloud.google.com/iam/docs/roles-overview#predefined) .

## Mount a Cloud Storage bucket

Agent Platform Workbench instances include a Cloud Storage integration that lets you mount a Cloud Storage bucket. This means you can browse the contents of the bucket and work with compatible files from within the JupyterLab interface.

You can access any of the Cloud Storage buckets and files that your instance has access to within the same project as your Agent Platform Workbench instance.

> **Note:** Your Agent Platform Workbench instance's access to Cloud Storage is determined by the single user or service account that you used to grant access to your instance. For example, if you granted a specific service account access to your instance, you must also grant that service account access to the Cloud Storage buckets that you want to use in JupyterLab.

### Required permission for enabling shared storage mounting

To enable shared storage mounting in your Agent Platform Workbench instance, ask your administrator to grant your Agent Platform Workbench instance's service account the `storage.buckets.list` permission on the project.

The `storage.buckets.list` permission is required for the **Mount shared storage** button to appear in the JupyterLab interface of your Agent Platform Workbench instance.

### Create a bucket and a Agent Platform Workbench instance

You must have access to at least one Cloud Storage bucket in the same project as your Agent Platform Workbench instance.

1.  If you need to create a Cloud Storage bucket, see [Create a bucket](https://docs.cloud.google.com/storage/docs/creating-buckets) .
2.  If you haven't already, [create a Agent Platform Workbench instance](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/create) in the same project as your Cloud Storage bucket.

### Open JupyterLab

1.  In the Google Cloud console, go to the **Instances** page.

2.  Next to your Agent Platform Workbench instance's name, click **Open JupyterLab** .
    
    Your Agent Platform Workbench instance opens JupyterLab.

### Mount the Cloud Storage bucket

To mount and then access a Cloud Storage bucket, do the following:

1.  In JupyterLab, make sure the folder **File Browser** tab is selected.

2.  In the left sidebar, click the ![Mount shared storage button](https://docs.cloud.google.com/static/gemini-enterprise-agent-platform/notebooks/workbench/images/icon-mount-shared-storage.png) **Mount shared storage** button. If you don't see the button, drag the right side of the sidebar to expand the sidebar until you see the button.
    
    ![The Mount shared storage button in the top right corner of the left sidebar](https://docs.cloud.google.com/static/gemini-enterprise-agent-platform/notebooks/workbench/instances/images/mount-shared-storage-button.png)

3.  In the **Bucket name** field, enter the Cloud Storage bucket name that you want to mount.

4.  Click **Mount** .

5.  Your Cloud Storage bucket appears as a folder in the **File browser** tab of the left sidebar. Double-click the folder to open it and browse the contents.

## Export to and restore files from Cloud Storage

This section describes how to export files to Cloud Storage and restore files located in a Cloud Storage bucket.

### Export to Cloud Storage

1.  In the Google Cloud console, go to the **Instances** page.

2.  Next to your Agent Platform Workbench instance's name, click **Open JupyterLab** .
    
    Your Agent Platform Workbench instance opens JupyterLab.

3.  In JupyterLab, make sure the folder **File Browser** tab is selected.

4.  In the left sidebar, click the ![Export to GCS button](https://docs.cloud.google.com/static/gemini-enterprise-agent-platform/notebooks/workbench/images/icon-export-to-gcs.png) **Export to GCS** button. If you don't see the button, drag the right side of the sidebar to expand the sidebar until you see the button.

5.  In the **Provide export location** dialog, enter a Cloud Storage bucket name that you want to export files to. If you need to create a Cloud Storage bucket, see [Create a bucket](https://docs.cloud.google.com/storage/docs/creating-buckets) .
    
    Agent Platform Workbench opens a new notebook that includes code for exporting your instance's files to Cloud Storage.

6.  Run the code in this cell.

### Restore files from Cloud Storage

To restore a file to your Agent Platform Workbench instance, you can use [gcloud storage cp](https://docs.cloud.google.com/sdk/gcloud/reference/storage/cp) to copy the file.

Run the following code in a cell of one of your instance's notebooks:

    !gcloud storage cp URI /home/jupyter/FILE_NAME

Replace the following:

  - `  URI  ` : the gsutil URI of the file that you want to copy, for example: gs:// BUCKET\_NAME / ZONE / INSTANCE\_ID / FILE\_NAME
  - `  FILE_NAME  ` : the name of the file to copy

For more information, see [Download the object from your bucket](https://docs.cloud.google.com/storage/docs/discover-object-storage-gcloud) .

## What's next

  - [Use a snapshot to back up and restore data](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/restore-snapshot)

  - [Save a notebook to GitHub](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/save-to-github)
