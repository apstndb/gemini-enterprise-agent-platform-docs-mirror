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

## September 18, 2026

Change

### 20260918-2230-rc0 Release

Change

Installed latest packages from upstream dependencies.

Feature

JupyterLab now forwards client-side logs (console errors, uncaught exceptions, unhandled promise rejections, and failed network requests) to the instance backend, where they surface in Cloud Logging for easier debugging.

## September 13, 2026

Change

### 20260913-2230-rc0 Release

Change

Installed latest packages from upstream dependencies.

Fixed

Fixed an issue where the `notebook-disable-nbconvert` metadata flag was ignored in custom containers.

Change

The obsolete `google-cloud-sdk` transitional package is no longer installed. The Google Cloud CLI itself is unchanged; it was already provided by the `google-cloud-cli` package.

Fixed

Fixed the %%bigquery notebook cell magic, which returned an error instead of query results in JupyterLab 4.

## August 30, 2026

Change

### 20260830-2230-rc0 Release

Change

Installed latest packages from upstream dependencies.

Fixed

Cloud Storage buckets that you mount through the file browser are now automatically re-mounted after the instance is restarted or is stopped and started. Previously the mounted folder could be left behind as an empty, unusable directory that had to be manually removed and re-mounted.

Fixed

The terminal and file browser are now more responsive when working in a Cloud Storage bucket that is mounted through the file browser. Frequent background checks for non-existent files are now cached instead of repeatedly querying Cloud Storage, which previously could make actions such as listing files or running terminal commands take several seconds.

## August 23, 2026

Change

### 20260823-2230-rc0 Release

Change

Installed latest packages from upstream dependencies.

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
