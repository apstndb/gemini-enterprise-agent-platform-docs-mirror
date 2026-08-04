---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/release-notes-image/workbench-container-2606
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/release-notes-image/workbench-container-2606
title: 'Image release notes: workbench-container-2606'
description: A single development environment for the entire data science workflow.
data_source: docs.cloud.google.com
---

This page documents image releases for the `workbench-container-2606` image family (Python 3.12) of Agent Platform Workbench. Each entry lists the image version that was released and the changes it contains.

For product-level updates that aren't specific to an image, see [Agent Platform Workbench release notes](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/release-notes) .

You can see the latest product updates for all of Google Cloud on the [Google Cloud](https://docs.cloud.google.com/release-notes) page, browse and filter all release notes in the [Google Cloud console](https://console.cloud.google.com/release-notes) , or programmatically access release notes in [BigQuery](https://console.cloud.google.com/bigquery?p=bigquery-public-data&d=google_cloud_release_notes&t=release_notes&page=table) .

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
