---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/release-notes
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/release-notes
title: Agent Platform Workbench release notes
description: A single development environment for the entire data science workflow.
data_source: docs.cloud.google.com
---

This page documents production updates to Agent Platform Workbench. Check this page for announcements about new or updated features, bug fixes, known issues, and deprecated functionality. Agent Platform Workbench is a component of Gemini Enterprise Agent Platform. For information on all Agent Platform releases, see the [Agent Platform release notes](https://docs.cloud.google.com/gemini-enterprise-agent-platform/release-notes) .

You can see the latest product updates for all of Google Cloud on the [Google Cloud](https://docs.cloud.google.com/release-notes) page, browse and filter all release notes in the [Google Cloud console](https://console.cloud.google.com/release-notes) , or programmatically access release notes in [BigQuery](https://console.cloud.google.com/bigquery?p=bigquery-public-data&d=google_cloud_release_notes&t=release_notes&page=table) .

To get the latest product updates delivered to you, add the URL of this page to your [feed reader](https://wikipedia.org/wiki/Comparison_of_feed_aggregators) , or add the [feed URL](https://docs.cloud.google.com/feeds/aiplatformnotebooks-release-notes.xml) directly.

## July 13, 2026

v2

Feature

**Agent Platform Workbench image release**

The following Agent Platform Workbench instances image releases are available:

  - **20260712-2130-rc0 ( `workbench-instances-2603` - Debian 12)**
      - Installed latest packages from upstream dependencies.
      - Fixed broken cupy installation.
  - **M144 ( `workbench-instances` - Debian 11)**
      - Installed latest packages from upstream dependencies.
      - Fixed a race condition that could cause JupyterLab to be unreachable (HTTP 524) on GPU instances.

## July 06, 2026

v2

Feature

**Agent Platform Workbench image release**

The following Agent Platform Workbench instances image release is available:

  - **20260701-2130-rc0 ( `workbench-instances-2603` - Debian 12)**
      - Installed latest packages from upstream dependencies.
      - Fixed a race condition that could cause JupyterLab to be unreachable (HTTP 524) on GPU instances.
      - Fixed an issue where long-running requests (for example, streaming or long-poll connections) could be terminated after about 60 seconds.

## June 30, 2026

v2

Feature

**Python 3.12 base containers for Agent Platform Workbench custom containers**

You can build [custom containers](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/create-custom-container) for Agent Platform Workbench instances using Python 3.12 base containers, in addition to the default Python 3.10 base containers. The Python 3.12 standard and slim base containers are available at the following URIs:

  - `us-docker.pkg.dev/workbench-images/gcr.io/workbench-container-2606:latest`
  - `us-docker.pkg.dev/workbench-images/gcr.io/workbench-container-slim-2606:latest`

## June 29, 2026

v2

Feature

**Agent Platform Workbench image release**

The following Agent Platform Workbench instances image release is available:

  - **20260628-2130-rc0 ( `workbench-instances-2603` - Debian 12)**
      - Installed latest packages from upstream dependencies.
      - Installed TensorFlow and PyTorch packages to the default kernel.

## June 24, 2026

v2

Feature

**Agent Platform Workbench image release**

The following Agent Platform Workbench instances image release is available:

  - **20260624-1604-rc0 ( `workbench-instances-2603` - Debian 12)**
      - Installed latest packages from upstream dependencies.
      - Fixed an issue where notebook kernels could become unavailable if the Dataproc plugin failed to load.

## June 23, 2026

v2

Feature

**Agent Platform Workbench image release**

The following Agent Platform Workbench instances image releases are available:

  - **20260622-2130-rc0 ( `workbench-instances-2603` - Debian 12)**
      - Installed latest packages from upstream dependencies.
      - Fixed a duplicate "Python 3 (ipykernel)" kernel appearing in the launcher.
  - **M143 ( `workbench-instances` - Debian 11)**
      - Installed latest packages from upstream dependencies.

## June 01, 2026

v2

Feature

**Agent Platform Workbench image release**

The following Agent Platform Workbench instances image release is available:

  - **20260531-2130-rc0 ( `workbench-instances-2603` - Debian 12)**
      - Installed latest packages from upstream dependencies.

## May 28, 2026

v2

Feature

**Agent Platform Workbench image release**

The following Agent Platform Workbench instances image release is available:

  - **M142 ( `workbench-instances` - Debian 11)**
      - Installed latest packages from upstream dependencies.
      - Fixed pip availability in the base environment.
      - Hardened JupyterLab authentication configuration.

## May 25, 2026

v2

Feature

**Agent Platform Workbench image release**

The following Agent Platform Workbench instances image release is available:

  - **20260524-2130-rc0 ( `workbench-instances-2603` - Debian 12)**
      - Installed latest packages from upstream dependencies.
      - Fixed a Python 3.12 compatibility issue in the JupyterLab server configuration.
      - Hardened JupyterLab authentication configuration.

## May 11, 2026

v2

Feature

**Agent Platform Workbench image release**

The following Agent Platform Workbench instances image release is available:

  - **20260510-2130-rc0 ( `workbench-instances-2603` - Debian 12)**
      - Installed latest packages from upstream dependencies.

## May 04, 2026

v2

Feature

**Agent Platform Workbench image release**

The following Agent Platform Workbench instances image release is available:

  - **20260503-2130-rc0 ( `workbench-instances-2603` - Debian 12)**
      - Installed latest packages from upstream dependencies.
      - Improved metadata server resolution reliability on Debian 12 by using the recommended metadata.google.internal name.

## April 27, 2026

v2

Feature

**Agent Platform Workbench image release**

The following Agent Platform Workbench instances image release is available:

  - **20260426-2130-rc0 ( `workbench-instances-2603` - Debian 12)**
      - Installed latest packages from upstream dependencies.

## April 20, 2026

v2

Feature

**Agent Platform Workbench image release**

The following Agent Platform Workbench instances image releases are available:

  - **20260419-2130-rc0 ( `workbench-instances-2603` - Debian 12)**
      - Installed latest packages from upstream dependencies.
      - Fixed intermittent connectivity failures caused by proxy TLS certificate rotation.
      - The post-startup script now re-runs after an instance auto-upgrade.
  - **M141 ( `workbench-instances` - Debian 11)**
      - Installed latest packages from upstream dependencies.
      - Fixed intermittent connectivity failures caused by proxy TLS certificate rotation.
      - The post-startup script now re-runs after an instance auto-upgrade.

## March 30, 2026

v2

Feature

**M140 release**

The M140 release of Vertex AI Workbench instances includes the following:

  - **Gemini CLI Update** : Minor updates to Gemini CLI's dependencies.

v2

Feature

**Workbench Image Release 26.03**

Released the new 26.03 image version under the following image family `workbench-instances-2603` . This major update introduces:

  - **OS Upgrade** : Migration to Debian 12 (Bookworm) for improved security and performance.
  - **Python Upgrade** : Python 3.12 as the default version.
  - **New Versioning Scheme** : Transitioned to a date-based versioning format (e.g., v26.03) to provide better historical context for image updates. For more information on new versioning schema see the [latest documentation](https://cloud.google.com/vertex-ai/docs/workbench/instances/manage-image-versions)
  - **Micromamba CLI** : Installed by default
  - **JupyterLab Environments** : Supports only JupyterLab 4.

## February 20, 2026

v2

Fixed

Fixed a vulnerability in Vertex AI Workbench for users utilizing managed credentials.

## January 29, 2026

v2

Feature

**M139 release**

The M139 release of Vertex AI Workbench instances includes the following:

  - Removed a startup script dependency on `gs://dl-platform-public-configs` .

## January 16, 2026

v2

Feature

[Preview](https://cloud.google.com/products#product-launch-stages) : The Gemini CLI is available in Vertex AI Workbench instances. The Gemini CLI is an open source AI agent that provides access to Gemini directly in a terminal. You can use the Gemini CLI to do tasks like the following:

  - Create a new notebook.
  - Run notebook cells.
  - Write and edit a notebook's code and text cells.
  - Explain code and technical concepts.
  - Interact with a Vertex AI Workbench instance's local file system, including performing complex file operations that span multiple files based on a single, high-level instruction.
  - Run basic shell commands.
  - Run commands to interact with other Google Cloud services, such as Vertex AI and BigQuery.

To get started, see [Use the Gemini CLI](https://docs.cloud.google.com/vertex-ai/docs/workbench/instances/gemini-cli) .

## January 14, 2026

v2

Feature

**M138 release**

The M138 release of Vertex AI Workbench instances includes the following:

  - Fixed an issue where daemon processes launched by post-startup scripts, such as gcsfuse mounts, did not persist after the script finished executing.

## December 12, 2025

v2

Feature

  - The following features are now [generally available (GA)](https://cloud.google.com/products#product-launch-stages) :
    
      - [Create new Vertex AI Workbench instances](https://docs.cloud.google.com/vertex-ai/docs/workbench/instances/create#create) with JupyterLab 4+.
    
      - [Create an instance with managed user credential access.](https://docs.cloud.google.com/vertex-ai/docs/workbench/instances/create-euc-instance)

  - Using post-startup scripts for new instances with user credential access is now available in private GA. For information about access to this release, see the [access request page](https://docs.google.com/forms/d/e/1FAIpQLSdzNZUFsRRbB0KaMCObGUYzIo6lK3X2tO7JZOm_DZrUhBYw5Q/viewform) . For more information, see [Create instances with post-startup scripts](https://docs.cloud.google.com/vertex-ai/docs/workbench/instances/create-euc-instance#post-startup-scripts) .

## December 10, 2025

v2

Feature

**M137 release**

The M137 release of Vertex AI Workbench instances includes the following:

  - Patched an issue where `sudo` prompts for a password when a custom Jupyter user name is specified.

## December 09, 2025

v2

Feature

[Generally available (GA)](https://cloud.google.com/products#product-launch-stages) : Encrypt your data-in-use by using [Confidential Computing](https://docs.cloud.google.com/confidential-computing/docs/confidential-computing-overview) . You can enable the Confidential VM service when you create a Vertex AI Workbench instance. To get started, see [Create an instance with Confidential Computing](https://docs.cloud.google.com/vertex-ai/docs/workbench/instances/create-confidential-computing) .

## November 21, 2025

v2

Feature

**M136 release**

The M136 release of Vertex AI Workbench instances includes the following:

  - Patched an issue where image outputs aren't displayed properly.

## November 17, 2025

v2

Feature

**M135 release**

The M135 release of Vertex AI Workbench instances includes the following:

  - Patched an issue where user-triggered OS shutdowns aren't reported to the Notebooks API.

## October 09, 2025

v2

Feature

**M134 release**

The M134 release of Vertex AI Workbench instances includes the following:

  - Patched a regression with custom notebook metrics reporting (for example, `jupyterlab_kernels` and `docker_status metrics` ).
  - Updated the Dataproc JupyterLab plugin ( `dataproc-jupyter-plugin` ) to version 0.1.92.
  - When using Google Cloud CLI commands, the `project` and `region` properties are preset.

## October 01, 2025

v2

Feature

[Generally available (GA)](https://cloud.google.com/products/#product-launch-stages) : You can use [Workforce Identity Federation](https://docs.cloud.google.com/iam/docs/workforce-identity-federation) with Vertex AI Workbench instances. Workforce Identity Federation lets you create and manage Vertex AI Workbench instances with credentials provided by an external identity provider (IdP). For more information, see [Create an instance with third party credentials](https://docs.cloud.google.com/vertex-ai/docs/workbench/instances/create-third-party-instance) .

## September 17, 2025

v2

Feature

**M133 release**

The M133 release of Vertex AI Workbench instances includes the following:

  - Patched an incompatibility with the Dataproc JupyterLab plugin ( `dataproc-jupyter-plugin` ) and instances with end-user credentials enabled.

## August 29, 2025

v2

Feature

**M132 release**

The M132 release of Vertex AI Workbench instances includes the following:

  - The new scheduler Jupyter plugin ( `scheduler-jupyter-plugin` ) is now preinstalled in the Jupyterlab 4 environment, with support for both the Cloud Composer and Vertex AI notebook schedulers.

  - Updated the Dataproc JupyterLab plugin ( `dataproc-jupyter-plugin` ) to version 0.1.90.

  - Patched bugs related to the managed end user credentials feature (Preview), resolving an incompatibility with listing Dataproc remote kernels.

  - Patched a bug that caused instances with disabled proxy access to get stuck in provisioning.

  - Removed the archived Debian 11 backports repository, resolving an issue with running `apt update` within the instance.

## August 05, 2025

v2

Feature

[Generally available](https://cloud.google.com/products#product-launch-stages) : You can consume reservations with Vertex AI Workbench instances. Reservations of Compute Engine zonal resources help you gain a high level of assurance that your jobs have the necessary resources to run. For more information, see [Use reservations with Vertex AI Workbench instances](https://docs.cloud.google.com/vertex-ai/docs/workbench/instances/reservations) .

## July 10, 2025

v2

Feature

**M131 release**

The M131 release of Vertex AI Workbench instances includes the following:

  - Updated the Dataproc JupyterLab plugin to version 0.1.89.

## June 26, 2025

v2

Feature

**M130 release**

The M130 release of Vertex AI Workbench instances includes the following:

  - Updated the Dataproc JupyterLab plugin to version 0.1.87.
  - Added the BigQuery JupyterLab plugin, version 0.0.1.
  - The `GOOGLE_CLOUD_REGION` environment variable is now set by default.

## June 10, 2025

v2

Feature

Available in [Preview](https://cloud.google.com/products#product-launch-stages) : You can consume reservations with Vertex AI Workbench instances. Reservations of Compute Engine zonal resources help you gain a high level of assurance that your jobs have the necessary resources to run. For more information, see [Use reservations with Vertex AI Workbench instances](https://docs.cloud.google.com/vertex-ai/docs/workbench/instances/reservations) .

## April 16, 2025

v2

Feature

**M129 release**

The M129 release of Vertex AI Workbench instances includes the following:

  - Updated the Dataproc JupyterLab plugin to version 0.1.85.

## March 26, 2025

v2

Feature

The ability to back up and restore data on a Vertex AI Workbench instance is now [generally available](https://cloud.google.com/products#product-launch-stages) . For more information, see [Back up and restore data on an instance](https://docs.cloud.google.com/vertex-ai/docs/workbench/instances/restore) .

## March 20, 2025

v2

Feature

Encrypt your data-in-use by using [Confidential Computing](https://docs.cloud.google.com/confidential-computing/docs/confidential-computing-overview) . This feature is now available in [Preview](https://cloud.google.com/products#product-launch-stages) . You can enable the Confidential VM service when you create a Vertex AI Workbench instance. To get started, see [Create an instance with Confidential Computing](https://docs.cloud.google.com/vertex-ai/docs/workbench/instances/create-confidential-computing) .

## March 12, 2025

v1

Feature

**M128 release**

The M128 release of Vertex AI Workbench user-managed notebooks includes the following:

  - Miscellaneous package updates.

v1

Feature

The M128 release of Vertex AI Workbench managed notebooks includes the following:

  - Miscellaneous package updates.

v2

Feature

**M128 release**

The M128 release of Vertex AI Workbench instances includes the following:

  - Miscellaneous package updates.

## January 16, 2025

v1

Feature

**M127 release**

The M127 release of Vertex AI Workbench user-managed notebooks includes the following:

  - Fixed an issue related to ownership of the home directory when using authorized ssh keys.

v2

Feature

**M127 release**

The M127 release of Vertex AI Workbench instances includes the following:

  - Fixed an issue related to ownership of the home directory when using authorized ssh keys.

v1

Feature

The M127 release of Vertex AI Workbench managed notebooks includes the following:

  - Fixed an issue related to ownership of the home directory when using authorized ssh keys.

## November 20, 2024

v2

Feature

**M126 release**

The M126 release of Vertex AI Workbench instances includes the following:

  - [Preview](https://cloud.google.com/products#product-launch-stages) : JupyterLab 4+ is available on new Vertex AI Workbench instances. To try it, select JupyterLab 4 when you [create your instance](https://docs.cloud.google.com/vertex-ai/docs/workbench/instances/create#create) .
  - Upgraded JupyterLab to 3.6.8.

v1

Feature

The M126 release of Vertex AI Workbench managed notebooks includes the following:

  - Upgraded JupyterLab to 3.6.8.

v1

Feature

**M126 release**

The M126 release of Vertex AI Workbench user-managed notebooks includes the following:

  - Upgraded JupyterLab to 3.6.8.
  - One or more framework versions have reached their end of patch and support dates. To view end of patch and support dates, see [Supported framework versions](https://docs.cloud.google.com/vertex-ai/docs/workbench/user-managed/images#supported-frameworks) .

## September 26, 2024

v2

Feature

**M125 release**

The M125 release of Vertex AI Workbench instances includes the following:

  - `bigframes` 1.9.0 is now available in all environments except TensorFlow.
  - Fixed a regression introduced in M124 where Conda was getting downgraded to an older version.
  - Patched a vulnerability with `adm` and `docker` permissions when the instance's root access isn't enabled.

v1

Feature

**M125 release**

The M125 release of Vertex AI Workbench user-managed notebooks includes the following:

  - Patched a vulnerability with `adm` and `docker` permissions when the instance's root access isn't enabled.

v1

Feature

The M125 release of Vertex AI Workbench managed notebooks includes the following:

  - Patched a vulnerability with `adm` and `docker` permissions when the instance's root access isn't enabled.

## September 10, 2024

v2

Feature

The ability to back up and restore data on a Vertex AI Workbench instance is now available in [Preview](https://cloud.google.com/products#product-launch-stages) . For more information, see [Back up and restore an instance](https://docs.cloud.google.com/vertex-ai/docs/workbench/instances/restore) .

## August 20, 2024

v1

Feature

**M124 release**

The M124 release of Vertex AI Workbench user-managed notebooks includes the following:

  - Pytorch 2.3.0 with CUDA 12.1 and Python 3.10 user-managed notebooks instances are now available.
  - Fixed a bug that prevented kernels from appearing when the Cloud Resource Manager API is turned off and Dataproc is enabled.

## August 19, 2024

v2

Announcement

The ability to create a Vertex AI Workbench instance based on a custom container is now [generally available](https://cloud.google.com/products#product-launch-stages) . Only custom containers derived from the Google-provided base container are supported. For more information, see [Create an instance using a custom container](https://docs.cloud.google.com/vertex-ai/docs/workbench/instances/create-custom-container) .

## August 08, 2024

v2

Feature

**M124 release**

The M124 release of Vertex AI Workbench instances includes the following:

  - Fixed a bug that prevented kernels from appearing when the Cloud Resource Manager API is turned off and Dataproc is enabled.
  - Spark notebooks on Dataproc: The Serverless Spark runtime template creation screen now has an easy-to-use UI for configuring resource allocation, autoscaling, and GPU settings.

v1

Feature

**M124 release**

The M124 release of Vertex AI Workbench managed notebooks includes the following:

  - Fixed a bug that prevented kernels from appearing when the Cloud Resource Manager API is turned off and Dataproc is enabled.

## July 24, 2024

v1

Feature

**M123 release**

The M123 release of Vertex AI Workbench managed notebooks includes the following:

  - Fixed a bug that caused conflicting permissions with the Jupyter user and google-sudoers.
  - Updated Nvidia drivers to version 550.90.07 to fix vulnerabilities.

## July 16, 2024

v1

Feature

**M123 release**

The M123 release of Vertex AI Workbench user-managed notebooks includes the following:

  - Fixed a bug that caused conflicting permissions with the Jupyter user and google-sudoers.
  - Fixed a bug for custom container instances using a disabled root.

v2

Feature

**M123 release**

The M123 release of Vertex AI Workbench instances includes the following:

  - Fixed a bug that caused conflicting permissions with the Jupyter user and google-sudoers.

## June 21, 2024

v2

Feature

**M122 release**

The M122 release of Vertex AI Workbench instances includes the following:

  - Updated Nvidia drivers to version 550.90.07 to fix vulnerabilities.

v1

Feature

**M122 release**

The M122 release of Vertex AI Workbench user-managed notebooks includes the following:

  - Updated Nvidia drivers to version 550.90.07 to fix vulnerabilities.

## June 07, 2024

v2

Feature

You can now create a Vertex AI Workbench instance based on a custom container. This feature is available in [Preview](https://cloud.google.com/products#product-launch-stages) . Only custom containers derived from the Google-provided base container are supported. For more information, see [Create an instance using a custom container](https://docs.cloud.google.com/vertex-ai/docs/workbench/instances/create-custom-container) .

## June 03, 2024

v2

Feature

You can now use [Workforce Identity Federation](https://docs.cloud.google.com/iam/docs/workforce-identity-federation) with Vertex AI Workbench instances in [Preview](https://cloud.google.com/products/#product-launch-stages) . Workforce Identity Federation lets you create and manage Vertex AI Workbench instances with credentials provided by an external identity provider (IdP). For more information, see [Create an instance with third party credentials](https://docs.cloud.google.com/vertex-ai/docs/workbench/instances/create-third-party-instance) .

## May 17, 2024

v1

Feature

**M121 release**

The M121 release of Vertex AI Workbench user-managed notebooks includes the following:

  - Updated Nvidia drivers to 550.54.15 to fix an issue where Nvidia drivers failed to install on startup after Debian 11 images upgraded kernel to `linux-image-5.10.0-29-cloud-amd64` .
  - The `linux-headers-cloud-amd64` metapackage is now installed for faster driver recompiling on kernel upgrades.
  - TensorFlow 2.6 CPU and GPU images are deprecated. There will be no further updates to these images in future releases.

v2

Feature

**M121 release**

The M121 release of Vertex AI Workbench instances includes the following:

  - Updated Nvidia drivers to 550.54.15 to fix an issue where Nvidia drivers failed to install on startup after Debian 11 images upgraded kernel to `linux-image-5.10.0-29-cloud-amd64` .
  - The `linux-headers-cloud-amd64` metapackage is now installed for faster driver recompiling on kernel upgrades.

v1

Feature

The M121 release of Vertex AI Workbench managed notebooks includes the following:

  - Updated the R CPU kernel from R 4.3 to R 4.4.

## April 29, 2024

v1

Feature

**M120 release**

The M120 release of Vertex AI Workbench managed notebooks includes the following:

  - Minor bug fixes for the `libcurl` package.

## April 25, 2024

v2

Feature

**M120 release**

The M120 release of Vertex AI Workbench instances includes the following:

  - Minor bug fixes for the `libcurl` package.

v1

Feature

**M120 release**

The M120 release of Vertex AI Workbench user-managed notebooks includes the following:

  - Upgraded TensorFlow 2.15 user-managed notebooks to TensorFlow 2.15.1.
  - Minor bug fixes for the `libcurl` package.

## March 29, 2024

v1

Fixed

**M119 release**

The M119 release of Vertex AI Workbench user-managed notebooks includes the following:

  - Fixed an issue wherein Dataproc extensions caused JupyterLab to crash when remote kernels weren't available.

## March 18, 2024

v2

Feature

**M118 release**

The M118 release of Vertex AI Workbench instances includes the following:

  - Updated Nvidia drivers to R535.

v1

Feature

**M118 release**

The M118 release of Vertex AI Workbench user-managed notebooks includes the following:

  - PyTorch 2.1.0 with CUDA 12.1 and Python 3.10 user-managed notebooks instances are now available.
  - PyTorch 2.2.0 with CUDA 12.1 and Python 3.10 user-managed notebooks instances are now available.
  - Updated Nvidia drivers of older user-managed notebooks images to R535.

v1

Feature

The M118 release of Vertex AI Workbench managed notebooks includes the following:

  - Updated Nvidia drivers to R535, which fixed a bug where the latest PyTorch 2.0 kernel didn't work due to outdated drivers.

## February 28, 2024

v2

Feature

**M117 release**

The M117 release of Vertex AI Workbench instances includes the following:

  - Removed the Cloud Storage browser in the left side pane in favor of the existing **Mount shared storage** button.

## February 08, 2024

v1

Feature

**M116 release**

The M116 release of Vertex AI Workbench user-managed notebooks includes the following:

  - Updated custom container user-managed notebooks to use NVIDIA driver version 535.104.05.
  - Fixed bugs in custom container user-managed notebooks where GPUs either wouldn't attach to the container properly, or detached after some time.

v1

Feature

The M116 release of Vertex AI Workbench managed notebooks includes the following:

  - Fixed a bug (present in versions M113 through M115) that prevented new local kernels from being usable.

## January 19, 2024

v2

Feature

**M115 release**

The M115 release of Vertex AI Workbench instances includes the following:

  - Added support for `venv` kernels.

v1

Feature

The M115 release of Vertex AI Workbench managed notebooks includes the following:

  - Fixed the BigQuery connector within PySpark containers.

v1

Feature

**M115 release**

The M115 release of Vertex AI Workbench user-managed notebooks includes the following:

  - Added support for TensorFlow 2.15 with Python 3.10 on Debian 11.
  - Added support for TensorFlow 2.14 with Python 3.10 on Debian 11.

## January 16, 2024

v1

Deprecated

Vertex AI Workbench user-managed notebooks is [deprecated](https://docs.cloud.google.com/vertex-ai/docs/deprecations) . On January 30, 2025, support for user-managed notebooks will end and the ability to create user-managed notebooks instances will be removed. Existing instances will continue to function but patches, updates, and upgrades won't be available. To continue using Vertex AI Workbench, you can [migrate your user-managed notebooks instances to Vertex AI Workbench instances](https://docs.cloud.google.com/vertex-ai/docs/workbench/user-managed/migrate-to-instances) .

v1

Deprecated

Vertex AI Workbench managed notebooks is [deprecated](https://docs.cloud.google.com/vertex-ai/docs/deprecations) . On January 30, 2025, support for managed notebooks will end and the ability to create managed notebooks instances will be removed. Existing instances will continue to function but patches, updates, and upgrades won't be available. To continue using Vertex AI Workbench, you can [migrate your managed notebooks instances to Vertex AI Workbench instances](https://docs.cloud.google.com/vertex-ai/docs/workbench/managed/migrate-to-instances) .

## December 14, 2023

v1

Feature

**M114 release**

The M114 release of Vertex AI Workbench user-managed notebooks includes the following:

  - Starting with this release, Python 3.7 is no longer available.
  - Upgraded R to 4.3 on Debian 11 Python 3.10 instances.
  - Upgraded JupyterLab to 3.6.6.

v1

Feature

The M114 release of Vertex AI Workbench managed notebooks includes the following:

  - Starting with this release, Python 3.7 is no longer available.
  - Added new Dataproc extension for remote kernels.
  - Upgraded JupyterLab to 3.6.6.
  - Fixed an issue that sometimes prevented users from running or scheduling notebooks using a default kernel.

## November 16, 2023

v2

Feature

**M113 release**

The M113 release of Vertex AI Workbench instances includes the following:

  - Added the Dataproc JupyterLab plugin to Vertex AI Workbench instances. To get started, see [Create a Dataproc-enabled instance](https://docs.cloud.google.com/vertex-ai/docs/workbench/instances/create-dataproc-enabled) .
  - When using an instance's Google Cloud CLI, `gcloud config` is preset with the following defaults:
      - `project` is set to your instance's project.
      - Your compute region is set to your instance's region.
      - Your Dataproc region is set to your instance's region.
  - Fixed an issue that prevented Dataproc kernels from working.
  - Fixed a CORS (cross-origin resource sharing) error.

v1

Feature

**M113 release**

The M113 release of Vertex AI Workbench user-managed notebooks includes the following:

  - Miscellaneous bug fixes and improvements in Python 3.10 notebooks.

## October 10, 2023

v1

Feature

**M112 release**

The M112 release of Vertex AI Workbench user-managed notebooks includes the following:

  - Miscellaneous bug fixes and improvements.

## September 25, 2023

v2

Feature

Vertex AI Workbench instances are now generally available ( [GA](https://cloud.google.com/products/#product-launch-stages) ). Vertex AI Workbench instances combine features from managed notebooks and user-managed notebooks to provide a robust data science solution. Supported features include:

  - Idle timeout
  - BigQuery and Cloud Storage integrations
  - End-user and service account authentication
  - VPC Service Controls
  - Customer managed encryption keys (CMEK) and Cloud External Key Manager (Cloud EKM)
  - Health status monitoring
  - Scheduled notebook runs
  - Dataproc integration

To get started, see [Introduction to Vertex AI Workbench instances](https://docs.cloud.google.com/vertex-ai/docs/workbench/instances/introduction) .

## September 18, 2023

v1

Deprecated

Debian 10 and Python 3.7 images have reached their end of patch and support life for Vertex AI Workbench managed notebooks and user-managed notebooks. Debian 11 and Python 3.10 images are available.

## September 14, 2023

v1 & v2

Feature

**M111 release**

The M111 release of Vertex AI Workbench instances includes the following:

  - Miscellaneous software updates.

v1 & v2

Feature

The M111 release of Vertex AI Workbench user-managed notebooks includes the following:

  - PyTorch 2.0 user-managed notebooks instances now include PyTorch XLA 2.0.
  - Miscellaneous software updates.

v1 & v2

Feature

The M111 release of Vertex AI Workbench managed notebooks includes the following:

  - Miscellaneous software updates.

## August 10, 2023

v1 & v2

Feature

**M110 release**

The M110 release of Vertex AI Workbench user-managed notebooks includes the following:

  - Added support for TensorFlow 2.13 with Python 3.10 on Debian 11.
  - Added support for TensorFlow 2.8 with Python 3.10 on Debian 11.
  - Miscellaneous software updates.

v1 & v2

Deprecated

TensorFlow 2.9 user-managed instances are deprecated.

v1 & v2

Feature

The M110 release of Vertex AI Workbench managed notebooks includes the following:

  - Increased shared memory size to available memory capacity.
  - Added support for Python 3.10 on Debian 11.
      - Added support for PyTorch 2.0 with Python 3.10.

> **Note:** Python 3.7 on Debian 10 images are still available.

## July 19, 2023

v2

Feature

Vertex AI Workbench instances are now available in [Preview](https://cloud.google.com/products/#product-launch-stages) . Vertex AI Workbench instances combine features from managed notebooks and user-managed notebooks to provide a robust data science solution. Supported features include:

  - Idle timeout
  - BigQuery and Cloud Storage integrations
  - End-user and service account authentication
  - VPC Service Controls
  - Customer managed encryption keys (CMEK)
  - Health status monitoring
  - Run notebooks on a schedule
  - Dataproc integration

To get started, see [Introduction to Vertex AI Workbench instances](https://docs.cloud.google.com/vertex-ai/docs/workbench/instances/introduction) .

## June 26, 2023

v1

Feature

**M109 release**

The M109 release of Vertex AI Workbench user-managed notebooks includes the following:

  - PyTorch 2.0 with Python 3.10 and CUDA 11.8 user-managed notebooks instances are now available.
  - Miscellaneous software updates.

v1

Feature

The M109 release of Vertex AI Workbench managed notebooks includes the following:

  - Fixed a bug that caused high cpu utilization due to excessive internal diagnostic tool processes.
  - Fixed a bug that was showing incorrect kernel image icons in the Jupyterlab launcher.

## May 04, 2023

v1

Feature

**M108 release**

The M108 release of Vertex AI Workbench user-managed notebooks includes the following:

  - Miscellaneous software updates.

## April 13, 2023

v1

Feature

**M107 release**

The M107 release of Vertex AI Workbench user-managed notebooks includes the following:

  - Fixed a bug that displayed the wrong version of the JupyterLab user interface.
  - Fixed a bug where a cron job for the diagnostic tool was added at every restart.
  - Miscellaneous software updates.

## April 06, 2023

v1

Feature

**M106 release**

The M106 release of Vertex AI Workbench user-managed notebooks includes the following:

  - Rolled back a previous change in which Jupyter dependencies were located in a separate Conda environment.
  - Fixed a bug in which kernels used by notebooks did not contain the specified machine learning frameworks.
  - Miscellaneous software updates.

## March 31, 2023

v1

Feature

**M105 release**

The M105 release of Vertex AI Workbench user-managed notebooks includes the following:

  - The following user-managed notebooks images are now available with Python 3.10 on Debian 11:
    
      - TensorFlow 2.11 CPU ( `tf-2-11-cpu-debian-11-py310` )
      - TensorFlow 2.11 GPU with Cuda 11.3 ( `tf-2-11-cu113-notebooks-debian-11-py310` )
      - PyTorch 1.13 with Cuda 11.3 ( `pytorch-1-13-cu113-notebooks-debian-11-py310` )
      - Base CPU ( `common-cpu-notebooks-debian-11-py310` )
      - Base GPU with Cuda 11.3 ( `common-cu113-notebooks-debian11-py310` )

  - The following user-managed notebooks images are now available with Python 3.9 on Debian 11:
    
      - TensorFlow 2.6 CPU ( `tf-2-6-cpu-notebooks-debian-11-py39` )
      - TensorFlow 2.6 GPU with Cuda 11.3 ( `tf-2-6-cu113-notebooks-debian-11-py39` )

  - Jupyter-related libraries have been moved to a different Conda environment, separate from the one containing machine learning frameworks and base software libraries.

## March 27, 2023

v1

Feature

**M105 release**

The M105 release of Vertex AI Workbench managed notebooks includes the following:

  - Fixed an issue wherein a runtime with idle shutdown enabled doesn't detect activity and shuts down.
  - Fixed an issue wherein the runtime data disk runs out of space and prevents access.
  - Fixed an issue wherein end user credentials are not preserved after shutdown.
  - Changed Health Agent logging levels from `DEBUG` to `INFO` .

## March 16, 2023

v1

Feature

**M104 release**

The M104 release of Vertex AI Workbench user-managed notebooks includes the following:

  - Fixed a regression in which `jupyter-user` metadata was ignored.
  - Enabled access to the Jupyter Gateway Client configuration by using the `notebook-enable-gateway-client` and `gateway-client-url` metadata tags.
  - Added the following packages:
      - google-cloud-artifact-registry
      - google-cloud-bigquery-storage
      - google-cloud-language
      - keyring
      - keyrings.google-artifactregistry-auth
  - Fixed a bug in which curl could not find the right SSL certificate path by default.

v1

Change

TensorFlow Enterprise 2.1 has reached the end of its support period. See [Version details](https://docs.cloud.google.com/tensorflow-enterprise/docs/overview#version_details) .

## February 21, 2023

v1

Feature

**M104 update**

This update of the M104 release of Vertex AI Workbench managed notebooks includes the following:

  - Fixed a bug where local and remote kernels are not displayed. This happens when remote kernels are not accessible.
  - Minor bug fixes and improvements.

## February 09, 2023

v1

Feature

**M104 release**

The M104 release of Vertex AI Workbench managed notebooks includes the following:

  - Added a fix for a security vulnerability in single-user managed notebooks instances.
  - Made enhancements to the network selection user experience in the managed notebooks executor.
  - Minor bug fixes and improvements.

## January 30, 2023

v1

Feature

**M103 release**

The M103 release of Vertex AI Workbench user-managed notebooks includes the following:

  - Fixed a bug in which a warning tells the user to run `jupyter lab build` when creating a new instance.
  - Upgraded PyTorch to 1.13.1.
  - Minor bug fixes and improvements.

## December 15, 2022

v1

Feature

**M102 release**

The M102 release of Vertex AI Workbench user-managed notebooks includes the following:

  - TensorFlow 2.11 is now available.
  - PyTorch 1.13 is now available.
  - Regular security patches and package upgrades.

## December 09, 2022

v1

Feature

**M101 release**

The M101 release of Vertex AI Workbench includes the following:

  - TensorFlow patch version upgrades:
      - From 2.8.3 to 2.8.4.
      - From 2.9.2 to 2.9.3.
      - From 2.10.0 to 2.10.1.
  - TensorFlow 1.15 on Vertex AI Workbench is now deprecated.
  - Added `*.notebooks.cloud.google.com` as part of the domains required for users to access Notebooks API. Removed `*.datalab.cloud.google.com` .
  - Regular security patches and package upgrades.

## November 08, 2022

v1

Feature

**M100 release**

The M100 release of Vertex AI Workbench includes the following:

  - Fixed a bug that prevented an instance with a GPU from starting.
  - Regular package updates.
  - Miscellaneous bug and display fixes.

v1

Fixed

Fixed a server-side request forgery (SSRF) vulnerability. Previous versions of managed notebooks and user-managed notebooks instances still contain the vulnerability. It is recommended that you [migrate your data](https://docs.cloud.google.com/vertex-ai/docs/workbench/managed/migrate) to a new instance.

## October 25, 2022

v1beta1

Breaking

The `v1beta1` version of the Notebooks API is scheduled for removal no earlier than January 16, 2023. After this date, you must use Notebooks API `v1` to manage Vertex AI Workbench resources.

## October 18, 2022

v1

Feature

**M98 release**

The M98 release of Vertex AI Workbench managed notebooks includes the following:

  - Upgraded Go from 1.16.5 to 1.19.2.
  - Upgraded R from 4.1 to 4.2.
  - Upgraded JupyterLab from 3.2 to 3.4.
  - Miscellaneous bug and display fixes.
  - Added a fix for the BigQuery SQL editor to run queries correctly in non-US locations.
  - Regular package updates.

[Learn more about managed notebooks versions](https://docs.cloud.google.com/vertex-ai/docs/workbench/managed/versions) .

## September 20, 2022

v1

Feature

**M96 release**

The M96 release of Vertex AI Workbench managed notebooks includes the following:

  - Fixed a problem where users were not able to save large Notebooks.
  - Fixed a display issue when using JupyterLab's simple interface.
  - Improved timeout behavior switch hardware operations.
  - Improved error messaging when a service account cannot access the Runtime.
  - Security fixes.
  - Regular package refreshment and bug fixes.

[Learn more about managed notebooks versions](https://docs.cloud.google.com/vertex-ai/docs/workbench/managed/versions) .

v1

Fixed

Fixed a server-side request forgery (SSRF) vulnerability. Previous versions of managed notebooks and user-managed notebooks instances still contain the vulnerability. It is recommended that you [migrate your data](https://docs.cloud.google.com/vertex-ai/docs/workbench/managed/migrate) to a new instance.

## August 17, 2022

v1 & v1beta1

Feature

**M95 release**

The M95 release of Vertex AI Workbench managed notebooks includes the following:

  - Fixed a bug where users were regularly getting a 502 error when trying to access JupyterLab.
  - Fixed a bug where opening an instance in Single User mode slowed the start of an instance.
  - Fixed a bug where a managed notebooks instance was not starting after adding a GPU.
  - Fixed bugs on the Serverless Spark form input.
  - Improved the ActivityLog refresh after Serverless Spark creation.
  - Fixed a bug related to the display of materialized views in BigQuery.
  - Refreshed the JupyterLab interface with an improved Google-specific theme.
  - Fixed a bug related to viewing Cloud Storage buckets and folders with large numbers of objects.
  - Regular package refreshment and bug fixes.

[Learn more about managed notebooks versions](https://docs.cloud.google.com/vertex-ai/docs/workbench/managed/versions) .

## May 27, 2022

v1 & v1beta1

Feature

**M93 release**

The M93 release of Vertex AI Workbench managed notebooks includes the following:

v1 & v1beta1

Fixed

  - Fixed a bug that prevented kernels from shutting down properly in Vertex AI Workbench managed notebooks.

[Learn more about managed notebooks versions](https://docs.cloud.google.com/vertex-ai/docs/workbench/managed/versions) .

## May 12, 2022

v1 & v1beta1

Feature

**M91 release**

The M91 release of Vertex AI Workbench managed notebooks includes the following:

  - Log streaming to the consumer project via Logs Viewer is now supported.
  - Added the `net-tools` package.
  - Regular package refreshments and bug fixes.

v1 & v1beta1

Fixed

  - Fixed an issue that caused Spark server networking errors when using Dataproc Serverless Spark and VPC Peering.

[Learn more about managed notebooks versions](https://docs.cloud.google.com/vertex-ai/docs/workbench/managed/versions) .

## April 06, 2022

v1 & v1beta1

Feature

[Vertex AI Workbench](https://docs.cloud.google.com/vertex-ai/docs/workbench) is generally available ( [GA](https://cloud.google.com/products#product-launch-stages) ). Vertex AI Workbench is a single notebook surface for all your data science needs that lets you access BigQuery data and Cloud Storage from within JupyterLab, execute notebook code in Vertex AI custom training and Spark, use custom containers, manage costs with idle timeout, and secure your instances with VPC Service Controls and customer managed encryption keys (CMEK).

Features supported include:

  - Google-managed instances and the latest GPU support
  - [Idle shutdown](https://docs.cloud.google.com/vertex-ai/docs/workbench/managed/idle-shutdown) for managed notebooks instances
  - [Custom containers](https://docs.cloud.google.com/vertex-ai/docs/workbench/managed/custom-container)
  - End-user and service account authentication
  - Native plug-ins for [BigQuery](https://docs.cloud.google.com/vertex-ai/docs/workbench/managed/bigquery) and [Cloud Storage](https://docs.cloud.google.com/vertex-ai/docs/workbench/managed/cloud-storage)
  - In-notebook Spark connect to Dataproc clusters
  - Jobs support via the [managed notebooks executor](https://docs.cloud.google.com/vertex-ai/docs/workbench/managed/executor) on Vertex AI custom training and Spark
  - One-click deploy for NGC containers
  - VPC Service Controls
  - [Customer managed encryption keys (CMEK)](https://docs.cloud.google.com/vertex-ai/docs/workbench/managed/cmek)

v1 & v1beta1

Feature

The Vertex AI Workbench managed notebooks [executor](https://docs.cloud.google.com/vertex-ai/docs/workbench/managed/executor) is generally available ( [GA](https://cloud.google.com/products#product-launch-stages) ). Use the executor to run notebook files on a schedule or as a one-time execution. You can use parameters in your execution to make specific changes to each run. For example, you might specify a different dataset to use, change the learning rate on your model, or change the version of the model. For more information, see [Run notebook files with the executor](https://docs.cloud.google.com/vertex-ai/docs/workbench/managed/executor) .

## October 11, 2021

v1 & v1beta1

Feature

[Vertex AI Workbench](https://docs.cloud.google.com/vertex-ai/docs/workbench) is now available in [Preview](https://cloud.google.com/products#product-launch-stages) . Vertex AI Workbench is a notebook-based development environment for the entire data science workflow.

v1 & v1beta1

Announcement

The Notebooks product and all existing Notebooks instances are now part of Vertex AI Workbench as [user-managed notebooks](https://docs.cloud.google.com/vertex-ai/docs/workbench/user-managed/introduction) .

## September 10, 2021

v1 & v1beta1

Change

Due to a recent change, the `iam.serviceAccounts.actAs` permission on the specified service account for the notebook instance is required for users to continue to have access to their notebook instances. The Google internal Inverting Proxy server that provides access to notebook instances now verifies that this permission is present before allowing users access to the JupyterLab URL. The JupyterLab URL this update covers is: `*.notebooks.googleusercontent.com` This update only applies to notebook instances in **Single User** mode and verifies that the assigned single user is authorized to execute code inside the notebook instance. Notebook instances running in Service Account or Project Editor mode already perform this verification via the Inverting Proxy server.

## July 26, 2021

v1 & v1beta1

Change

If using proxy single-user mode, Notebooks API now verifies if the specified user ( `proxy-user-mail` ) has Service Account permissions on the Service Account. This check is performed during instance creation and registration.

## June 18, 2021

v1

Feature

Support for Compute Reservations. Notebooks API allows the use of Compute Reservations during instance creation.

## March 26, 2021

v1

Feature

Cross Project Service Account is supported for user-managed notebooks.

## March 04, 2021

v1

Change

New Notebooks instances add labels for VM image ( `goog-caip-notebook` ) and volume ( `goog-caip-notebook-volume` ).

## February 01, 2021

v1

Feature

Notebooks [Terraform Module](https://registry.terraform.io/providers/hashicorp/google/latest/docs/resources/notebooks_instance) supports Notebooks API v1

## January 23, 2021

v1

Feature

Notebooks API supports [Shielded VM configuration](https://cloud.google.com/security/products/shielded-vm) .

v1

Announcement

VPC-SC for Notebooks (now known as user-managed notebooks) is now [Generally Available](https://cloud.google.com/products#product-launch-stages) .

## September 21, 2020

v1

Feature

AI Platform Notebooks (now known as user-managed notebooks) API is now [Generally Available](https://cloud.google.com/products#product-launch-stages) . The API now includes an [isUpgradable](https://docs.cloud.google.com/ai-platform/notebooks/docs/reference/rest/v1/projects.locations.instances/isUpgradeable) endpoint and adds manual and auto-upgrade functionality to notebooks instances created using the API.

v1

Feature

[Cloud Audit Logging for AI Platform Notebooks](https://docs.cloud.google.com/vertex-ai/docs/workbench/user-managed/audit-logging) (now known as user-managed notebooks) is now [Generally Available](https://cloud.google.com/products#product-launch-stages) .

[Granular IAM permissions for AI Platform Notebooks](https://docs.cloud.google.com/vertex-ai/docs/workbench/user-managed/iam) (now known as user-managed notebooks) is now [Generally Available](https://cloud.google.com/products#product-launch-stages) .

AI Platform Notebooks now supports [E2 machine types](https://docs.cloud.google.com/compute/docs/machine-types#e2_machine_types) .

The following new regions have been added:

  - `europe-west2` (London, UK)
  - `europe-west3` (Frankfurt, Germany)
  - `europe-west6` (Zürich, Switzerland)

## March 31, 2020

v1beta1

Feature

AI Platform Notebooks (now known as user-managed notebooks) is now [Generally Available](https://cloud.google.com/products#product-launch-stages) . Some integrations with and specific features of AI Platform Notebooks are still in beta, such as [Virtual Private Cloud Service Controls](https://docs.cloud.google.com/ai-platform/notebooks/docs/service-perimeter) , [Identity and Access Management (IAM)](https://docs.cloud.google.com/ai-platform/notebooks/docs/iam) roles, and [AI Platform Notebooks API](https://docs.cloud.google.com/ai-platform/notebooks/docs/reference/rest) .

## February 04, 2020

v1beta1

Feature

[VPC Service Controls](https://docs.cloud.google.com/vpc-service-controls/docs/overview) now supports AI Platform Notebooks. Learn [how to use a notebook instance within a service perimeter](https://docs.cloud.google.com/ai-platform/notebooks/docs/service-perimeter) . This functionality is in [beta](https://cloud.google.com/products/#product-launch-stages) .

## February 03, 2020

v1beta1

Feature

AI Platform Notebooks now supports Access Transparency. Access Transparency provides you with logs of actions that Google staff have taken when accessing your data. To learn more about Access Transparency, see the [Overview of Access Transparency](https://docs.cloud.google.com/assured-workloads/access-transparency/docs/overview) .

## September 12, 2019

v1

Feature

You can now use customer-managed encryption keys (CMEK) to protect data on the boot disks of your AI Platform Notebooks (now known as user-managed notebooks) VM instances. CMEK in AI Platform Notebooks is generally available. For more information, see [Using customer-managed encryption keys (CMEK)](https://docs.cloud.google.com/vertex-ai/docs/workbench/user-managed/cmek) .

## September 09, 2019

v1beta1

Feature

AI Platform Notebooks now provides more ways for you to customize your network settings, encrypt your notebook content, and grant access to your notebook instance. These options are available when you [create a notebook](https://docs.cloud.google.com/ai-platform/notebooks/docs/create-new#create-with-options) .

v1beta1

Feature

Now you can implement AI Platform Notebooks using custom containers. Use a [Deep Learning Containers image](https://docs.cloud.google.com/ai-platform/deep-learning-containers/docs/choosing-container#choose_a_container_image_type) or [create a derivative container](https://docs.cloud.google.com/ai-platform/deep-learning-containers/docs/derivative-container) of your own, then [create a new notebook instance using your custom container](https://docs.cloud.google.com/ai-platform/notebooks/docs/custom-container) .

## July 12, 2019

v1beta1

Change

R upgraded to version 3.6.

R Notebooks are no longer dependent on a Conda environment.

## June 03, 2019

v1beta1

Feature

You can now create AI Platform Notebooks instances with R and core R packages installed. Learn [how to install R dependencies](https://docs.cloud.google.com/ai-platform/notebooks/docs/dependencies) , and read guides for [using R with BigQuery in AI Platform Notebooks](https://docs.cloud.google.com/ai-platform/notebooks/docs/use-r-bigquery) and [using R and Python in the same notebook](https://docs.cloud.google.com/ai-platform/notebooks/docs/r-python-same-notebook) .

## March 01, 2019

v1beta1

Feature

[AI Platform Notebooks](https://docs.cloud.google.com/ai-platform/notebooks/docs/overview) is now available in beta. AI Platform Notebooks enables you to create and manage virtual machine (VM) instances that are pre-packaged with [JupyterLab](https://jupyterlab.readthedocs.io/en/stable/getting_started/overview.html) and a suite of deep learning software.

Visit the [AI Platform Notebooks overview](https://docs.cloud.google.com/ai-platform/notebooks/docs/overview) and the [guide to creating a new notebook instance](https://docs.cloud.google.com/ai-platform/notebooks/docs/create-new) to learn more.
