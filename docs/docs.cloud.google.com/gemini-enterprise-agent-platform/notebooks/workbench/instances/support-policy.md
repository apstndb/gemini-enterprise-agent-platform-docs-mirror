---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/support-policy
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/support-policy
title: Support policy
description: Learn about the support commitments for Agent Platform Workbench images, including vulnerability handling, packages, support windows, and how to request changes.
data_source: docs.cloud.google.com
---

# Support policy

Gemini Enterprise Agent Platform Workbench images are tested and qualified for running data science and ML workloads on Google Cloud. Supported images are actively patched with security updates (CVEs) and bug fixes. This policy applies to both VM images and custom container base images.

To learn about image contents and versioning, see [Image versioning and lifecycle](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/image-versioning) . To learn about what changed in each release, see [Image release notes](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/release-notes-image) .

## Support duration

Each image family is supported for 2 years from the date it becomes active. During the support window:

  - The image family is actively scanned for security vulnerabilities, and security fixes are applied on a regular basis.
  - Critical bugs are patched.
  - High-priority security and bug fixes are released on demand; lower-priority fixes are released on a regular cadence.
  - Fixes are delivered in minor releases (image names) within the image family. Upgrade to the latest minor version to receive them. See [Manage image versions](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/manage-image-versions) .
  - No new breaking features are introduced.
  - All changes are recorded in the [Image release notes](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/release-notes-image) .

## Deprecation

When a newer major version is released, the previous image family is eventually deprecated. Each image family has a published release date and deprecation date. For more information, see [Image versioning and lifecycle](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/image-versioning) .

A deprecated image family no longer receives new versions or fixes, and it stops pointing to a latest image name. Existing instances keep running, and you can still create an instance from a specific deprecated image name. To keep receiving fixes, upgrade to an active image family. See [Manage image versions](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/manage-image-versions) .

What happens to an image after deprecation depends on its type:

| Image type              | After deprecation                                                                           |
| ----------------------- | ------------------------------------------------------------------------------------------- |
| VM images               | Remain available in [Compute Engine](https://docs.cloud.google.com/compute/docs/overview) . |
| Custom container images | Persist indefinitely in the registry.                                                       |

Moving to a new image family can change the OS, Python version, frameworks, and file paths. Review the [Image release notes](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/release-notes-image) and test before you upgrade across families.

## Contact us

For technical support, contact Google Cloud Support. To request a new image feature or an added or upgraded package, file a request through Google Cloud Support and include the image family and the specific capability you need.
