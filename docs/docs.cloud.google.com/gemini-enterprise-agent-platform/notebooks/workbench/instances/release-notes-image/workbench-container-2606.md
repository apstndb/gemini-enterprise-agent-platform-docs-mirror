---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/release-notes-image/workbench-container-2606
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/release-notes-image/workbench-container-2606
title: 'Image release notes: workbench-container-2606'
description: A single development environment for the entire data science workflow.
data_source: docs.cloud.google.com
---

This page documents image releases for the `workbench-container-2606` image family (Python 3.12) of Agent Platform Workbench. Each entry lists the image version that was released and the changes it contains.

For the versioning scheme and lifecycle dates, see [Image versioning and lifecycle](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/image-versioning) . For product-level updates that aren't specific to an image, see [Agent Platform Workbench release notes](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/release-notes) .

You can see the latest product updates for all of Google Cloud on the [Google Cloud](https://docs.cloud.google.com/release-notes) page, browse and filter all release notes in the [Google Cloud console](https://console.cloud.google.com/release-notes) , or programmatically access release notes in [BigQuery](https://console.cloud.google.com/bigquery?p=bigquery-public-data&d=google_cloud_release_notes&t=release_notes&page=table) .

## August 16, 2026

Change

Updated the CUDA base image from 12.8.1 to 12.9.2 (CUDA 12.9, cuDNN 9.10). This is a minor CUDA 12 update, binary compatible with the previous image, and also addresses known vulnerabilities in a bundled NVIDIA profiler component.

Security

Updated the bundled Ruby gems rexml and net-imap to patched versions, addressing known vulnerabilities.

Deprecated

Removed the JupyterLab 3 environment from the Python 3.12 custom container; JupyterLab 4 is now the only JupyterLab environment and is always used. The Python 3.10 images are unaffected.

Change

### 20260816-2330-rc0 Release

Security

Updated aiohttp, joblib and cryptography to patched versions, addressing known vulnerabilities including CVE-2022-21797 and CVE-2025-69223.

Change

Installed latest packages from upstream dependencies.

## August 09, 2026

Change

Installed latest packages from upstream dependencies.

Change

### 20260809-2330-rc0 Release

Fixed

Fixed the Git panel's grayed out buttons which were disabled due to an issue with the Jupyter Lab's Git plugin introduced in version 0.54.0.

## August 02, 2026

Change

### 20260802-2330-rc0 Release

Fixed

Fixed issue with JupyterLab UI silently reverting file changes and interrupting kernels due to Gemini CLI's auto reload extension.

Change

The JupyterLab last-active and auto-reload extensions are now enabled only when Gemini CLI is configured, preventing them from affecting the native JupyterLab UI otherwise.

Change

Installed latest packages from upstream dependencies.

Fixed

Fixed an error that could prevent creating new `micromamba` environments at runtime due to package cache permissions.

## July 13, 2026

Feature

**Secure Boot is compatible with GPUs**

You can now enable Secure Boot on Agent Platform Workbench instances that have a GPU attached. Secure Boot with GPUs is supported on the `workbench-instances-2603` VM image and the `workbench-container-2606` custom container, which include a Secure Boot-signed NVIDIA GPU driver so the driver loads under Secure Boot. For more information, see [Create an instance](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/create) .

## June 30, 2026

Feature

**Python 3.12 base containers for Agent Platform Workbench custom containers**

You can build [custom containers](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/create-custom-container) for Agent Platform Workbench instances using Python 3.12 base containers, in addition to the default Python 3.10 base containers. The Python 3.12 standard and slim base containers are available at the following URIs:

  - `us-docker.pkg.dev/workbench-images/gcr.io/workbench-container-2606:latest`
  - `us-docker.pkg.dev/workbench-images/gcr.io/workbench-container-slim-2606:latest`
