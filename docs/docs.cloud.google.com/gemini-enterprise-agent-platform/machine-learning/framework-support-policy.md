---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/framework-support-policy
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/framework-support-policy
title: Gemini Enterprise Agent Platform framework support policy
description: Learn about the framework support policy for Gemini Enterprise Agent Platform services.
data_source: docs.cloud.google.com
---

Gemini Enterprise Agent Platform publishes containers and virtual machine images to simplify the configuration of your machine learning (ML) workloads. These images contain the operating system, the ML frameworks, drivers, and other libraries. We publish new versions of images regularly to include new patches, security updates, and features. Each image provided by Gemini Enterprise Agent Platform provides support for a specific minor version of an ML framework.

This allows you time to update and test your code when moving from one framework version to another. You should always test your jobs and models thoroughly when switching to a new framework version, regardless of whether it's a major or minor update.

For all services, subscribe to the [Gemini Enterprise Agent Platform release notes](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/release-notes) page for announcements about new version releases for your containers, images, and frameworks.

For the list of supported framework versions, see the [Supported frameworks list](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/supported-frameworks) .

## Shared responsibility

Securing your workloads on Gemini Enterprise Agent Platform is a shared responsibility. While Gemini Enterprise Agent Platform regularly publishes new versions of images to address security vulnerabilities, you are responsible for tasks such as the following:

  - Manually upgrading to the latest version.

  - Ensuring that you properly configured your services to use the latest version.

For more information, see [Shared responsibility](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/shared-responsibility) .

## Support policy for framework versions

During the supported period for an ML framework version, we publish new image versions regularly. The updates might include the following:

  - Patch updates for supported frameworks. For example, if we support TensorFlow 2.7, and TensorFlow releases 2.7.1 to address bugs, then we release a new image version.

  - Security updates for supported frameworks.

  - Non-breaking updates to other packages and software installed on the image.

  - Updates to dependencies that have reached end-of-support. For example, if an image has Python 3.7 installed and it reaches the end-of-support date, we release a new image version. If the change in dependency might be a breaking change, we update the [Supported frameworks list](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/supported-frameworks) to indicate the change in the dependency.

Once published, an image version is immutable and doesn't change. You should always use the latest image version, as earlier versions might have security vulnerabilities or other critical bugs.

### Support policy schedule

Support periods for each framework version follows this schedule:

  - **End-of-patch and support date:** After this date, Gemini Enterprise Agent Platform no longer publishes new image versions for that framework version. Existing resources that have been deployed to Gemini Enterprise Agent Platform continue to function. After this date, we recommend you plan to switch to a more recent framework version.
    
    To receive troubleshooting support from Gemini Enterprise Agent Platform, you might be asked to upgrade to a framework version that is within the supported time period.
    
      - For online predictions using prebuilt containers, in the event of security vulnerabilities, Gemini Enterprise Agent Platform might delete existing endpoints using out-of-support framework versions.

  - **End-of-availability date:** After this date, you can no longer use images for this framework version. Services might block the creation of new resources using these images, and the images are no longer available for download.
    
      - For online predictions using prebuilt containers, you can no longer create new endpoints using this version after this date, and Gemini Enterprise Agent Platform might delete existing endpoints that use this version.
    
      - End-of-availability dates don't exist for pipeline frameworks that are open source pypi.org Python libraries, such as the Kubeflow Pipelines SDK and TensorFlow Extended SDK.

## Services covered by the framework support policy

If you use the following services, you should be aware of new version releases that might require you to update your container images or frameworks:

  - [Prebuilt containers for custom training](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/pre-built-containers)

  - [Prebuilt containers for predictions and explanations](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/pre-built-containers)

  - [Prebuilt containers for Ray on Agent Platform](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/supported-frameworks#ray)

  - [Gemini Enterprise Agent Platform Pipelines](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/pipelines/build-pipeline#version-pipeline)
    
      - For the version support schedule for pipeline SDKs, see [Supported frameworks for pipelines](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/supported-frameworks#pipelines) in "Supported frameworks list."

For all services, subscribe to the [Gemini Enterprise Agent Platform release notes](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/release-notes) page for announcements about new version releases for your containers, images, and frameworks.

## What's next

  - Review the [list of supported framework versions](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/supported-frameworks) .
