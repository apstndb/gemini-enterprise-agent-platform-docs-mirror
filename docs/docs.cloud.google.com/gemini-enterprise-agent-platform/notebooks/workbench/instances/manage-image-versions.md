---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/manage-image-versions
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/manage-image-versions
title: Manage image versions
description: Manage image versions in a Agent Platform Workbench instance.
data_source: docs.cloud.google.com
---

# Manage image versions

This page describes how to manage image versions for Gemini Enterprise Agent Platform Workbench instances, including how to do the following:

  - List the available image names
  - Create an instance on a specific image name
  - Upgrade or move an instance between image families

To learn about the versioning scheme, image contents, and lifecycle, see [Image versioning and lifecycle](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/image-versioning) .

To learn about what changed in each release, see [Image release notes](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/release-notes-image) .

## VM images

This section describes how to list available VM images, create an instance on a specific VM image, and upgrade an instance's VM image.

### List available VM images

VM images are stored in a private repository. To list available VM images and their supported configurations, use `gcloud workbench instances get-config` or the `GetConfig` API.

### gcloud

    gcloud workbench instances get-config --location=LOCATION

Replace `  LOCATION  ` with the Google Cloud region, for example, `us-central1` .

### cURL

    curl -X GET -H "Authorization: Bearer $(gcloud auth print-access-token)" \
      "https://notebooks.googleapis.com/v2/projects/PROJECT_ID/locations/LOCATION/instances:getConfig"

Replace the following:

  - `  PROJECT_ID  ` : your Google Cloud project ID.
  - `  LOCATION  ` : the region where you want to retrieve configurations.

### Create an instance with a specific VM image

To create an instance on a specific VM image, use gcloud CLI or Terraform. You can specify an image family to get its latest image name, or specify an image name to get the exact version.

### gcloud

    # Using an image family
    gcloud workbench instances create INSTANCE_NAME \
      --vm-image-project=cloud-notebooks-managed \
      --vm-image-family=IMAGE_FAMILY \
      --location=LOCATION
    
    # Using a specific image name
    gcloud workbench instances create INSTANCE_NAME \
      --vm-image-project=cloud-notebooks-managed \
      --vm-image-name=IMAGE_NAME \
      --location=LOCATION

Replace the following:

  - `  INSTANCE_NAME  ` : the name of your instance.

  - `  IMAGE_FAMILY  ` : the VM image family from the [Image versioning and lifecycle](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/image-versioning) page.

  - `  LOCATION  ` : the region where you want to create the instance.

  - `  IMAGE_NAME  ` : a specific image name. To find available image names, see [Image release notes](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/release-notes-image) or run `gcloud workbench instances get-config` . For more information, see [List available VM images](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/manage-image-versions#retrieve-image-list) .

### Terraform

    resource "google_workbench_instance" "vm_instance" {
      # ... other configurations
      gce_setup {
        vm_image {
          project = "cloud-notebooks-managed"
          family  = "IMAGE_FAMILY" # Or specify image name to get an exact version
        }
      }
      # ...
    }

### Upgrade a VM image

By default, an instance upgrades to the latest image name in its current image family. To use an older image name, create a new instance from a specific image name.

### gcloud

    gcloud workbench instances upgrade INSTANCE_NAME --location=LOCATION

Replace the following:

  - `  INSTANCE_NAME  ` : the name of your instance.
  - `  LOCATION  ` : the region where your instance is located.

### Terraform

In the Terraform configuration, set the `vm_image` block within the `google_workbench_instance` resource.

    resource "google_workbench_instance" "vm_instance" {
      # ... other configurations
      gce_setup {
        vm_image {
          project = "cloud-notebooks-managed"
          family  = "workbench-instances-2603" # Or use name = "workbench-instances-2603-20240315-1800-rc0"
        }
      }
      # ...
    }

For more information about creating an instance with a specific version, see [Create a specific version](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/create-specific-version#create_a_specific_version) .

### Upgrade across image families

To change an instance to the latest image name in a different image family (for example, from `workbench-instances` to the newer `workbench-instances-2603` ), specify the target image family during the upgrade. This is the supported path for changing between major versions without recreating the instance.

### gcloud

Use the `--image-family` flag with `gcloud workbench instances upgrade` to specify the target image family. The instance is upgraded to the latest image in the specified family.

    gcloud workbench instances upgrade INSTANCE_NAME \
      --location=LOCATION \
      --image-family=projects/IMAGE_PROJECT/global/images/family/IMAGE_FAMILY

Replace the following:

  - `  INSTANCE_NAME  ` : the name of your instance.
  - `  LOCATION  ` : the region where your instance is located.
  - `  IMAGE_PROJECT  ` : the project that hosts the image family (for example, `cloud-notebooks-managed` ).
  - `  IMAGE_FAMILY  ` : the name of the target image family (for example, `workbench-instances-2603` ).

For example, to upgrade an instance to the latest image in the `workbench-instances-2603` family:

    gcloud workbench instances upgrade example-instance \
      --location=us-central1 \
      --image-family=projects/cloud-notebooks-managed/global/images/family/workbench-instances-2603

If the `--image-family` flag is omitted, the instance is upgraded to the latest image in its current image family.

> > **Note:** Upgrading across image families with Terraform isn't supported. Use the gcloud CLI for cross-family upgrades.

## Custom container image

Custom containers on Agent Platform Workbench instances follow a strictly sequential release model without any image branching or parallel maintenance. A date versioning tag is used, which is shared with all the images used to manage custom containers on Agent Platform Workbench instances for any given release. The versioning tag follows the format `YYYYMMDD-HHMM-rcX` .

[Create a custom container-based instance](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/create-custom-container) describes how to build and utilize custom containers on Agent Platform Workbench instances.

### Host image

**Image family:** `workbench-container-host`

The container host uses Google's Container Optimized OS (COS). The version cannot be specified when creating a new Agent Platform Workbench custom container instance. Instead, new instances use the latest COS image as the container host. The underlying image follows the latest stable OS version from COS. See the [Container-Optimized OS release notes](https://docs.cloud.google.com/container-optimized-os/docs/release-notes) .

## Custom container instances

This section covers creating and upgrading instances that use custom containers. To build a custom container, see [create an instance using a custom container](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/create-custom-container) . For the base container images and their specifications, see [Image versioning and lifecycle](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/image-versioning) .

### Create an instance with a custom container

To create an Agent Platform Workbench instance using a custom container, use gcloud CLI or Terraform.

### gcloud

    gcloud workbench instances create INSTANCE_NAME \
      --project=PROJECT_ID \
      --location=ZONE \
      --container-repository=REGION-docker.pkg.dev/PROJECT_ID/REPOSITORY_NAME/IMAGE_NAME \
      --container-tag=TAG

Replace the following:

  - `  INSTANCE_NAME  ` : the name of your instance.

  - `  PROJECT_ID  ` : the Google Cloud project where you want to create the instance.

  - `  ZONE  ` : the zone where you want to create the instance (for example, `us-central1-a` ).

  - `  REGION  ` : the region for the Artifact Registry repository (for example, `us` ).

  - `  REPOSITORY_NAME  ` : the name of your Artifact Registry repository.

  - `  IMAGE_NAME  ` : a specific image name. To find available image names, see [Image release notes](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/release-notes-image) or run `gcloud workbench instances get-config` . For more information, see [List available VM images](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/manage-image-versions#retrieve-image-list) .

  - `  TAG  ` : the image tag, for example `latest` .

### Terraform

    resource "google_workbench_instance" "container_instance" {
      # ... other configurations
      gce_setup {
        container_image {
          repository = "REGION-docker.pkg.dev/PROJECT_ID/REPOSITORY_NAME/IMAGE_NAME"
          tag        = "TAG"
        }
      }
      # ...
    }

### Upgrade a custom container

A custom container instance runs on two images, which upgrade differently:

  - **Container host image:** managed by Google. It follows the [VM upgrade path](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/manage-image-versions#upgrade-vm-image) .
  - **Base Container image:** the image you build and select. To upgrade it, either reference a mutable tag such as `:latest` (the instance picks up the changes to that tag on restart) or update the instance to a different tag.

## What's next

  - [Image versioning and lifecycle](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/image-versioning) : See what each image contains, how versions are numbered, and when images are deprecated.
  - [Image release notes](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/release-notes-image) : See what changed in each image release.
  - [Support policy](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/support-policy) : Learn about CVE handling, packages, support windows, and deprecation notice.
