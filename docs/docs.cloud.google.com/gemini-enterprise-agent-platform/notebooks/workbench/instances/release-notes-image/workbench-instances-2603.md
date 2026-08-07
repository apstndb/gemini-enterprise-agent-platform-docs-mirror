---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/release-notes-image/workbench-instances-2603
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/release-notes-image/workbench-instances-2603
title: 'Image release notes: workbench-instances-2603'
description: A single development environment for the entire data science workflow.
data_source: docs.cloud.google.com
---

This page documents image releases for the `workbench-instances-2603` image family (Debian 12) of Agent Platform Workbench. Each entry lists the image version that was released and the changes it contains.

For the versioning scheme and lifecycle dates, see [Image versioning and lifecycle](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/image-versioning) . For product-level updates that aren't specific to an image, see [Agent Platform Workbench release notes](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/release-notes) .

You can see the latest product updates for all of Google Cloud on the [Google Cloud](https://docs.cloud.google.com/release-notes) page, browse and filter all release notes in the [Google Cloud console](https://console.cloud.google.com/release-notes) , or programmatically access release notes in [BigQuery](https://console.cloud.google.com/bigquery?p=bigquery-public-data&d=google_cloud_release_notes&t=release_notes&page=table) .

## July 13, 2026

Change

### 20260712-2130-rc0 Release

Change

Installed latest packages from upstream dependencies.

Fixed

Fixed broken cupy installation.

Feature

**Secure Boot is compatible with GPUs**

You can now enable Secure Boot on Agent Platform Workbench instances that have a GPU attached. Secure Boot with GPUs is supported on the `workbench-instances-2603` VM image and the `workbench-container-2606` custom container, which include a Secure Boot-signed NVIDIA GPU driver so the driver loads under Secure Boot. For more information, see [Create an instance](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/create) .

## July 06, 2026

Change

### 20260701-2130-rc0 Release

Change

Installed latest packages from upstream dependencies.

Fixed

Fixed a race condition that could cause JupyterLab to be unreachable (HTTP 524) on GPU instances.

Fixed

Fixed an issue where long-running requests (for example, streaming or long-poll connections) could be terminated after about 60 seconds.

## June 29, 2026

Change

### 20260628-2130-rc0 Release

Change

Installed latest packages from upstream dependencies.

Feature

Installed TensorFlow and PyTorch packages to the default kernel.

## June 24, 2026

Change

### 20260624-1604-rc0 Release

Change

Installed latest packages from upstream dependencies.

Fixed

Fixed an issue where notebook kernels could become unavailable if the Dataproc plugin failed to load.

## June 23, 2026

Change

### 20260622-2130-rc0 Release

Change

Installed latest packages from upstream dependencies.

Fixed

Fixed a duplicate "Python 3 (ipykernel)" kernel appearing in the launcher.

## June 01, 2026

Change

### 20260531-2130-rc0 Release

Change

Installed latest packages from upstream dependencies.

## May 25, 2026

Change

### 20260524-2130-rc0 Release

Change

Installed latest packages from upstream dependencies.

Fixed

Fixed a Python 3.12 compatibility issue in the JupyterLab server configuration.

Change

Hardened JupyterLab authentication configuration.

## May 11, 2026

Change

### 20260510-2130-rc0 Release

Change

Installed latest packages from upstream dependencies.

## May 04, 2026

Change

### 20260503-2130-rc0 Release

Change

Installed latest packages from upstream dependencies.

Change

Improved metadata server resolution reliability on Debian 12 by using the recommended metadata.google.internal name.

## April 27, 2026

Change

### 20260426-2130-rc0 Release

Change

Installed latest packages from upstream dependencies.

## April 20, 2026

Change

### 20260419-2130-rc0 Release

Change

Installed latest packages from upstream dependencies.

Fixed

Fixed intermittent connectivity failures caused by proxy TLS certificate rotation.

Change

The post-startup script now re-runs after an instance auto-upgrade.
