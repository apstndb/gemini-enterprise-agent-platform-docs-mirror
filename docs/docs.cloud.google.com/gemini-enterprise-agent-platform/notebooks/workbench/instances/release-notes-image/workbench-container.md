---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/release-notes-image/workbench-container
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/release-notes-image/workbench-container
title: 'Image release notes: workbench-container'
description: A single development environment for the entire data science workflow.
data_source: docs.cloud.google.com
---

This page documents image releases for the `workbench-container` image family (Python 3.10) of Agent Platform Workbench. Each entry lists the image version that was released and the changes it contains.

For the versioning scheme and lifecycle dates, see [Image versioning and lifecycle](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/image-versioning) . For product-level updates that aren't specific to an image, see [Agent Platform Workbench release notes](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/release-notes) .

You can see the latest product updates for all of Google Cloud on the [Google Cloud](https://docs.cloud.google.com/release-notes) page, browse and filter all release notes in the [Google Cloud console](https://console.cloud.google.com/release-notes) , or programmatically access release notes in [BigQuery](https://console.cloud.google.com/bigquery?p=bigquery-public-data&d=google_cloud_release_notes&t=release_notes&page=table) .

## August 16, 2026

Change

### 20260816-2230-rc0 Release

Change

Installed latest packages from upstream dependencies.

## August 09, 2026

Change

### 20260809-2230-rc0 Release

Change

Installed latest packages from upstream dependencies.

Fixed

Fixed the Git panel's grayed out buttons which were disabled due to an issue with the Jupyter Lab's Git plugin introduced in version 0.54.0.

## August 02, 2026

Change

### 20260802-2230-rc0 Release

Fixed

Fixed issue with JupyterLab UI silently reverting file changes and interrupting kernels due to Gemini CLI's auto reload extension.

Change

The JupyterLab last-active and auto-reload extensions are now enabled only when Gemini CLI is configured, preventing them from affecting the native JupyterLab UI otherwise.

Change

Installed latest packages from upstream dependencies.
