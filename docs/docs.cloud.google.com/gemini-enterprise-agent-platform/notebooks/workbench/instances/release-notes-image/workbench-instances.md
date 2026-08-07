---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/release-notes-image/workbench-instances
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/release-notes-image/workbench-instances
title: 'Image release notes: workbench-instances'
description: A single development environment for the entire data science workflow.
data_source: docs.cloud.google.com
---

This page documents image releases for the `workbench-instances` image family (Debian 11) of Agent Platform Workbench. Each entry lists the image version that was released and the changes it contains.

For the versioning scheme and lifecycle dates, see [Image versioning and lifecycle](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/image-versioning) . For product-level updates that aren't specific to an image, see [Agent Platform Workbench release notes](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/release-notes) .

You can see the latest product updates for all of Google Cloud on the [Google Cloud](https://docs.cloud.google.com/release-notes) page, browse and filter all release notes in the [Google Cloud console](https://console.cloud.google.com/release-notes) , or programmatically access release notes in [BigQuery](https://console.cloud.google.com/bigquery?p=bigquery-public-data&d=google_cloud_release_notes&t=release_notes&page=table) .

## July 13, 2026

Change

### M144 Release

Change

Installed latest packages from upstream dependencies.

Fixed

Fixed a race condition that could cause JupyterLab to be unreachable (HTTP 524) on GPU instances.

## June 23, 2026

Change

### M143 Release

Change

Installed latest packages from upstream dependencies.

## May 28, 2026

Change

### M142 Release

Change

Installed latest packages from upstream dependencies.

Fixed

Fixed pip availability in the base environment.

Change

Hardened JupyterLab authentication configuration.

## April 20, 2026

Change

### M141 Release

Change

Installed latest packages from upstream dependencies.

Fixed

Fixed intermittent connectivity failures caused by proxy TLS certificate rotation.

Change

The post-startup script now re-runs after an instance auto-upgrade.

## March 30, 2026

Change

### M140 Release

Change

**Gemini CLI Update** : Minor updates to Gemini CLI's dependencies.

## January 29, 2026

Change

### M139 Release

Change

Removed a startup script dependency on `gs://dl-platform-public-configs` .

## January 14, 2026

Change

### M138 Release

Fixed

Fixed an issue where daemon processes launched by post-startup scripts, such as gcsfuse mounts, did not persist after the script finished executing.

## December 10, 2025

Change

### M137 Release

Fixed

Patched an issue where `sudo` prompts for a password when a custom Jupyter user name is specified.

## November 21, 2025

Change

### M136 Release

Fixed

Patched an issue where image outputs aren't displayed properly.

## November 17, 2025

Change

### M135 Release

Fixed

Patched an issue where user-triggered OS shutdowns aren't reported to the Notebooks API.

## October 09, 2025

Change

### M134 Release

Fixed

Patched a regression with custom notebook metrics reporting (for example, `jupyterlab_kernels` and `docker_status metrics` ).

Change

Updated the Dataproc JupyterLab plugin ( `dataproc-jupyter-plugin` ) to version 0.1.92.

Change

When using Google Cloud CLI commands, the `project` and `region` properties are preset.

## September 17, 2025

Change

### M133 Release

Fixed

Patched an incompatibility with the Dataproc JupyterLab plugin ( `dataproc-jupyter-plugin` ) and instances with end-user credentials enabled.

## August 29, 2025

Change

### M132 Release

Change

The new scheduler Jupyter plugin ( `scheduler-jupyter-plugin` ) is now preinstalled in the Jupyterlab 4 environment, with support for both the Cloud Composer and Vertex AI notebook schedulers.

Change

Updated the Dataproc JupyterLab plugin ( `dataproc-jupyter-plugin` ) to version 0.1.90.

Fixed

Patched bugs related to the managed end user credentials feature (Preview), resolving an incompatibility with listing Dataproc remote kernels.

Fixed

Patched a bug that caused instances with disabled proxy access to get stuck in provisioning.

Change

Removed the archived Debian 11 backports repository, resolving an issue with running `apt update` within the instance.

## July 10, 2025

Change

### M131 Release

Change

Updated the Dataproc JupyterLab plugin to version 0.1.89.

## June 26, 2025

Change

### M130 Release

Change

Updated the Dataproc JupyterLab plugin to version 0.1.87.

Feature

Added the BigQuery JupyterLab plugin, version 0.0.1.

Change

The `GOOGLE_CLOUD_REGION` environment variable is now set by default.

## April 16, 2025

Change

### M129 Release

Change

Updated the Dataproc JupyterLab plugin to version 0.1.85.

## March 12, 2025

Change

### M128 Release

Change

Miscellaneous package updates.

## January 16, 2025

Change

### M127 Release

Fixed

Fixed an issue related to ownership of the home directory when using authorized ssh keys.

## November 20, 2024

Change

### M126 Release

Feature

[Preview](https://cloud.google.com/products#product-launch-stages) : JupyterLab 4+ is available on new Vertex AI Workbench instances. To try it, select JupyterLab 4 when you [create your instance](https://docs.cloud.google.com/vertex-ai/docs/workbench/instances/create#create) .

Change

Upgraded JupyterLab to 3.6.8.

## September 26, 2024

Change

### M125 Release

Feature

`bigframes` 1.9.0 is now available in all environments except TensorFlow.

Fixed

Fixed a regression introduced in M124 where Conda was getting downgraded to an older version.

Fixed

Patched a vulnerability with `adm` and `docker` permissions when the instance's root access isn't enabled.

## August 08, 2024

Change

### M124 Release

Fixed

Fixed a bug that prevented kernels from appearing when the Cloud Resource Manager API is turned off and Dataproc is enabled.

Change

Spark notebooks on Dataproc: The Serverless Spark runtime template creation screen now has an easy-to-use UI for configuring resource allocation, autoscaling, and GPU settings.

## July 16, 2024

Change

### M123 Release

Fixed

Fixed a bug that caused conflicting permissions with the Jupyter user and google-sudoers.

## June 21, 2024

Change

### M122 Release

Change

Updated Nvidia drivers to version 550.90.07 to fix vulnerabilities.

## May 17, 2024

Change

### M121 Release

Change

Updated Nvidia drivers to 550.54.15 to fix an issue where Nvidia drivers failed to install on startup after Debian 11 images upgraded kernel to `linux-image-5.10.0-29-cloud-amd64` .

Change

The `linux-headers-cloud-amd64` metapackage is now installed for faster driver recompiling on kernel upgrades.

## April 25, 2024

Change

### M120 Release

Fixed

Minor bug fixes for the `libcurl` package.

## March 18, 2024

Change

### M118 Release

Change

Updated Nvidia drivers to R535.

## February 28, 2024

Change

### M117 Release

Change

Removed the Cloud Storage browser in the left side pane in favor of the existing **Mount shared storage** button.

## January 19, 2024

Change

### M115 Release

Feature

Added support for `venv` kernels.

## November 16, 2023

Change

### M113 Release

Feature

Added the Dataproc JupyterLab plugin to Vertex AI Workbench instances. To get started, see [Create a Dataproc-enabled instance](https://docs.cloud.google.com/vertex-ai/docs/workbench/instances/create-dataproc-enabled) .

Change

When using an instance's Google Cloud CLI, `gcloud config` is preset with the following defaults: \* `project` is set to your instance's project. \* Your compute region is set to your instance's region. \* Your Dataproc region is set to your instance's region.

Fixed

Fixed an issue that prevented Dataproc kernels from working.

Fixed

Fixed a CORS (cross-origin resource sharing) error.

## September 14, 2023

Change

### M111 Release

Change

Miscellaneous software updates.
