---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/images-overview
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/images-overview
title: Agent Platform Workbench images
description: 'Overview of the image types available for Agent Platform Workbench instances: VM images and custom containers, and how to choose between them.'
data_source: docs.cloud.google.com
---

# Agent Platform Workbench images

Every Gemini Enterprise Agent Platform Workbench instance runs on an image that Google builds and maintains. The image determines the operating system, the Python version, the preinstalled ML frameworks (such as TensorFlow and PyTorch), the GPU and CUDA stack, and the JupyterLab environment your instance starts with.

Agent Platform Workbench provides two types of mutually exclusive images:

  - **VM images** : Google-built boot images that install the operating system, frameworks, kernels, and JupyterLab directly on the instance host.
  - **Custom containers** : a Google-provided base container image that you can extend with your own packages, kernels, and JupyterLab configuration. Your container runs on a Google-managed host. Use custom containers for reproducible, pre-provisioned environments that you reuse across many instances.

To compare the two image types and choose one, see [Choose an image type](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/images-overview#choose-an-image-type) .

## Choose an image type

Use the following table to choose the type that fits your workflow. For details about the contents, versions, and lifecycle of each image, see [Image versioning and lifecycle](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/image-versioning) .

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Option</th>
<th>VM images</th>
<th>Custom containers</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>What it is</td>
<td>A Google-built boot image that installs the operating system, frameworks, kernels, and JupyterLab directly on the instance host.</td>
<td>A Google-provided base container that runs on a Google-managed host.</td>
</tr>
<tr class="even">
<td>Operating system</td>
<td>Debian</td>
<td>Host: Container-Optimized OS (COS), managed by Google<br />
Container: Ubuntu</td>
</tr>
<tr class="odd">
<td>How you customize</td>
<td>Add packages and micromamba environments to a running instance. The image itself is Google-managed and immutable.</td>
<td>Build a custom container image ahead of time and reuse it across many instances.</td>
</tr>
<tr class="even">
<td>Host access</td>
<td>Full access to the instance host.</td>
<td>The COS host is Google-managed and not modifiable.</td>
</tr>
<tr class="odd">
<td>Best for</td>
<td>The default experience; workloads that need host access or custom system processes.</td>
<td>Customized environments that you can deploy at scale.</td>
</tr>
<tr class="even">
<td>How to create</td>
<td><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/create-specific-version">Create an instance with a specific version</a></td>
<td><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/create-custom-container">Create an instance with a custom container</a></td>
</tr>
</tbody>
</table>

## Agent Platform Workbench VM images

Agent Platform Workbench VM images are private images, built by Google, that provision the required packages and kernels directly onto the host machine. Agent Platform Workbench supports Debian-based VM images. A VM installs directly on the instance host, so you can interact with the host machine.

To create an instance on a specific VM image version, see [create an instance with a specific image version](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/create-specific-version) .

## Agent Platform Workbench custom containers

A custom container lets you bring a customized image to Agent Platform Workbench instances using a Docker container. Use a custom container to ship custom packages, kernels, and a ready-made JupyterLab environment without building them at instance startup.

You start from a Google-provided base container image, extend it with what you need, and then provision Agent Platform Workbench instances from the container that you build. Google publishes two variants of the base container image:

  - **Standard: supports all Agent Platform Workbench features** . Includes pre-installed data science packages, CUDA libraries, Google Cloud JupyterLab integrations (BigQuery and Managed Service for Apache Spark), common system packages, and micromamba-based kernel management.
  - **Slim** : a minimal base image with JupyterLab, metadata-based JupyterLab configuration, and micromamba-based kernel management. You install any additional packages or extensions.

Your container runs on a Google-managed host, based on Container-Optimized OS (COS), that provides features such as idle shutdown, the proxy agent, and service telemetry. For more information, see [Container-Optimized OS features and benefits](https://docs.cloud.google.com/container-optimized-os/docs/concepts/features-and-benefits) .

For the base image URIs, sizes, and supported Python versions, see [Create a custom container](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/create-custom-container) . For constraints, see [Custom container limitations](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/create-custom-container#limitations) .

## What's next

  - [Image versioning and lifecycle](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/image-versioning) : See what each image contains, how versions are numbered, and when images are deprecated.
  - [Manage image versions](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/manage-image-versions) : Create an instance on a specific version, upgrade, and roll back.
  - [Image release notes](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/release-notes-image) : See what changed in each image release.
  - [Support policy](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/support-policy) : Learn about CVE handling, packages, support windows, and deprecation notice.
