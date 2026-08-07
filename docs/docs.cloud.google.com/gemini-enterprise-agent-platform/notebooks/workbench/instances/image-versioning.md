---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/image-versioning
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/image-versioning
title: Image versioning and lifecycle
description: Learn how Agent Platform Workbench image versions are numbered and how images move through their lifecycle, for both VM images and custom container images.
data_source: docs.cloud.google.com
---

# Image versioning and lifecycle

This page describes how Agent Platform Workbench image versions are numbered and how images move through their lifecycle, for both VM images and custom container images.

To create an instance on a specific VM image version, see [create an instance with a specific image version](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/manage-image-versions#create-instance-with-vm-image) .

To learn about what changed in each release, see [Image release notes](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/release-notes-image) .

## Versioning

Agent Platform Workbench images use a major version and a minor version.

  - **Image Family (major version):** uses calendar versioning ( `YYMM` ); for example, `workbench-instances-2603` (2603). A new image family marks a significant change to the image, such as a new operating system, Python version, or framework baseline. A larger or potentially breaking change ships as a new image family while the previous one keeps receiving updates. This gives you time to migrate instead of causing a potential breaking change.
  - **Image Name (minor version):** uses date versioning in the form `YYYYMMDD-HHMM-rcX` , for example `20260629-1557-rc0` . An image name is a point release within an image family, such as a bug fix or security patch.

Each image family points to its latest image name. To upgrade or change versions, see [Manage image versions](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/manage-image-versions) .

### Legacy milestone versioning

Releases built upon Debian 11 and earlier use milestone versioning, for example `m144` . Releases built upon Debian 12 and later use calendar and date versioning described earlier.

### Release cadence

Google updates actively maintained image names (minor versions) regularly, approximately weekly. The exact timing of any given release can vary, and some releases contain only security or dependency updates. This cadence is approximate. To consult the actual release history, see [Image release notes](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/release-notes-image) .

If you need a known, stable image name for a deployment, pin to a specific minor version rather than tracking the family, and upgrade on your own schedule.

## Lifecycle

An Agent Platform Workbench instances image moves through the following states:

**Active** : the image family is fully supported and receives security and bug fixes. The image family points to its latest active image name.

**End of support:** the image family no longer receives new versions or fixes. You can still create instances from a specific deprecated image name, but you should upgrade to an active image family.

Each image family has two dates:

  - **Release date** : when the major version became available.
  - **Deprecation date:** the date the image family is marked as deprecated. After this date, it no longer receives new versions or fixes.

## VM images

Agent Platform Workbench VM images are Google-built boot images, published in the `cloud-notebooks-managed` image project at ` projects/cloud-notebooks-managed/global/images/family/ IMAGE_FAMILY  ` . Each image family includes several image names, one per release. To see the full release history, see [Image release notes](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/release-notes-image) . To list the most recent available image names, see [List available VM images](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/manage-image-versions#retrieve-image-list) .

### Active VM images

The following table lists active VM images:

| Image family                       | OS        | Python | Kernels                                                          | CUDA | Release date | End of support |
| ---------------------------------- | --------- | ------ | ---------------------------------------------------------------- | ---- | ------------ | -------------- |
| `workbench-instances-2603` (26.03) | Debian 12 | 3.12   | Single Kernel: Python 3.12, TensorFlow 2.21.0, PyTorch 2.12.1    | 13.0 | March 2026   | March 2028     |
| `workbench-instances` (Legacy)     | Debian 11 | 3.10   | Multiple Kernels: Python 3.10, TensorFlow 2.11.0, PyTorch 1.13.1 | 11.8 | July 2023    | March 2027     |

## Custom container images

A custom container runs on two images: the base container image which you can version and extend, and the Google-managed container host image that runs it.

### Base container image

The base container image uses the same image family (major) and image name (minor) versioning as VM images. The image family is a date suffix on the container name, for example `workbench-container-2606` . The image name version is a date-based tag, for example `workbench-container-2606:20260629-1557-rc0` .

Agent Platform Workbench provides Google-built base container images in two variants: standard and slim. Learn more about creating an [Agent Platform Workbench instance using a custom container](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/create-custom-container#base-containers) .

| Image family                    | Variant  | OS           | Python | Kernels                                                          | CUDA   | Release date | End of support |
| ------------------------------- | -------- | ------------ | ------ | ---------------------------------------------------------------- | ------ | ------------ | -------------- |
| `workbench-container-2606`      | Standard | Ubuntu 24.04 | 3.12   | Single Kernel: Python 3.12, TensorFlow 2.21.0, PyTorch 2.12.1    | 12.8.1 | June 2026    | June 2028      |
| `workbench-container-slim-2606` | Slim     | Ubuntu 24.04 | 3.12   | Single Kernel: Python 3.12, TensorFlow 2.21.0, PyTorch 2.12.1    | N/A    | June 2026    | June 2028      |
| `workbench-container`           | Standard | Ubuntu 24.04 | 3.10   | Multiple Kernels: Python 3.10, TensorFlow 2.11.0, PyTorch 1.13.1 | 12.8.1 | August 2024  | March 2027     |
| `workbench-container-slim`      | Slim     | Ubuntu 24.04 | 3.10   | Single Kernel: Python 3.10, TensorFlow 2.11.0, PyTorch 1.13.1    | N/A    | August 2024  | March 2027     |

### Container host image

The container host has a single image family that closely tracks the latest production-ready Container-Optimized OS (COS) version. It is published under the `workbench-container-host` family in the `cloud-notebooks-managed` image project, and each version uses a date version, for example, `20260701-2130-rc0` . You can't pin the host version when you create an instance. New instances use the latest host image. For host OS changes, see the [Container-Optimized OS release notes](https://docs.cloud.google.com/container-optimized-os/docs/release-notes) .

## What's next

  - [Manage image versions](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/manage-image-versions) : Create an instance on a specific version, upgrade, and roll back.
  - [Image release notes](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/release-notes-image) : See what changed in each image release.
  - [Support policy](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/support-policy) : Learn about CVE handling, packages, support windows, and deprecation notice.
