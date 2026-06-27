---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/manage-image-versions
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/manage-image-versions
title: Manage image versions
description: Manage image versions in a Agent Platform Workbench instance.
data_source: docs.cloud.google.com
---

# Manage image versions

This document describes how to manage image versions for Gemini Enterprise Agent Platform Workbench instances, including software stack details and instructions for creating and upgrading instances.

Reference the [Agent Platform Workbench release notes](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/release-notes) to check what is supported with each image version.

## VM images

VM images on Agent Platform Workbench instances use two separate versioning schemes: major and minor.

  - **Major versions** : Agent Platform Workbench instances use calendar versioning ( `YY.MM` ) to mark major releases which introduce significant changes to the underlying image. These can include updates to support in frameworks, OS, and Python versioning. Once a new major version is released, users can expect the following:
    
      - New features will only be developed in the latest release track.
      - Older release branches will continue to be updated at the same cadence but are expected to be phased out in the near future.
    
    The image family name reflects the release train (for example, `workbench-instances-YYMM` ).

  - **Minor versions** : The minor version is a date-based tag that indicates the specific build of the image, following the format `YYYYMMDD-HHMM-rcX` . This includes point releases such as bug fixes and security patches applied to the latest release train.

### Legacy release track

**Image family:** `workbench-instances`

  - **OS** : Debian 11
  - **Python** : 3.11
  - **Frameworks** : TensorFlow/PyTorch/Base (common ML packages)

**Minor versioning** : The **legacy release** images will continue to be updated using milestone versioning incremented numerically (for example, `m140` ) to signify minor updates.

### Retrieve image list

VM images are stored in a private repository. To retrieve a list of available VM images and their supported configurations, you can use the `gcloud workbench instances get-config` command in the Google Cloud CLI or the `GetConfig` API.

### gcloud

To retrieve the valid configurations for Agent Platform Workbench instances in a specific location, use the `gcloud workbench instances get-config` command.

    gcloud workbench instances get-config --location=LOCATION

Replace the following:

  - `  LOCATION  ` : the Google Cloud region (for example, `us-central1` ).

### cURL

To retrieve the configurations using the API, make a GET request to the `getConfig` endpoint.

    curl -X GET -H "Authorization: Bearer $(gcloud auth print-access-token)" \
      "https://notebooks.googleapis.com/v2/projects/PROJECT_ID/locations/LOCATION/instances:getConfig"

Replace the following:

  - `  PROJECT_ID  ` : your Google Cloud project ID.
  - `  LOCATION  ` : the region where you want to retrieve configurations.

### Create instance with specific VM image

To create a Agent Platform Workbench instance with a specific VM image version, you can use the gcloud CLI or Terraform:

### gcloud

Specify the selected image family or image name using the `--vm-image-family` or `--vm-image-name` flag in `gcloud workbench instances create` .

    # Using an image family
    gcloud workbench instances create INSTANCE_NAME \
      --vm-image-project=cloud-notebooks-managed \
      --vm-image-family=workbench-instances-2603 \
      --location=LOCATION
    
    # Using a specific image name
    gcloud workbench instances create INSTANCE_NAME \
      --vm-image-project=cloud-notebooks-managed \
      --vm-image-name=workbench-instances-2603-20240315-1800-rc0 \
      --location=LOCATION

Replace the following:

  - `  INSTANCE_NAME  ` : the name of your instance.
  - `  LOCATION  ` : the region where you want to create the instance.

For more information on creating an instance with a specific version, see [Create a specific version](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/create-specific-version#create_a_specific_version) .

### Terraform

In the Terraform configuration, set the `vm_image` block within the `google_workbench_instance` resource.

    resource "google_workbench_instance" "vm_instance" {
      # ... other configurations
      gce_setup {
        vm_image {
          project      = "cloud-notebooks-managed"
          family       = "workbench-instances-2603" # Or use name = "workbench-instances-2603-20240315-1800-rc0"
        }
      }
      # ...
    }

### Upgrade a VM image

Agent Platform Workbench instances support upgrading to the latest version of an image family. By default, an instance is upgraded to the latest image in its current image family. To upgrade across image families (for example, between major versions), see [Upgrade across image families](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/manage-image-versions#upgrade-across-image-families) . To use an older image, a new instance must be created.

To upgrade a VM image to the latest version within its image family, you can use the gcloud CLI or Terraform:

### gcloud

    gcloud workbench instances upgrade INSTANCE_NAME --location=LOCATION

Replace the following:

  - `  INSTANCE_NAME  ` : the name of your instance.
  - `  LOCATION  ` : the region where your instance is located.

### Terraform

To upgrade an instance using Terraform, update the `family` or `name` in the `vm_image` block to the selected version and apply the configuration.

    resource "google_workbench_instance" "vm_instance" {
      # ... other configurations
      gce_setup {
        vm_image {
          project      = "deeplearning-platform-release"
          family       = "workbench-instances-2603" # Update to the latest family
        }
      }
    }

For more information on upgrading, see [Upgrade an instance's environment](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/upgrade) .

#### Upgrade across image families

To upgrade an instance to the latest image in a *different* image family (for example, to move from the legacy `workbench-instances` release track to the newer `workbench-instances-2603` release track), specify the target image family during the upgrade. This is the supported path for moving between major versions without recreating the instance.

### gcloud

Use the `--image-family` flag with `gcloud workbench instances upgrade` to specify the target image family. The instance is upgraded to the latest image in the specified family.

    gcloud workbench instances upgrade INSTANCE_NAME \
      --location=LOCATION \
      --image-family=projects/IMAGE_PROJECT/global/images/family/IMAGE_FAMILY

Replace the following:

  - `  INSTANCE_NAME  ` : the name of your instance.
  - `  LOCATION  ` : the region where your instance is located.
  - `  IMAGE_PROJECT  ` : the project that hosts the image family (for example, `deeplearning-platform-release` ).
  - `  IMAGE_FAMILY  ` : the name of the target image family (for example, `workbench-instances-2603` ).

For example, to upgrade an instance to the latest image in the `workbench-instances-2603` family:

    gcloud workbench instances upgrade example-instance \
      --location=us-central1 \
      --image-family=projects/deeplearning-platform-release/global/images/family/workbench-instances-2603

If the `--image-family` flag is omitted, the instance is upgraded to the latest image in its current image family.

> > **Note:** Upgrading across image families with Terraform isn't supported. Use the gcloud CLI for cross-family upgrades.

## Custom container image

Custom containers on Agent Platform Workbench instances follow a strictly sequential release model without any image branching or parallel maintenance. A date versioning tag is used, which is shared with all the images used to manage custom containers on Agent Platform Workbench instances for any given release. The versioning tag follows the format `YYYYMMDD-HHMM-rcX` .

[Create a custom container-based instance](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/create-custom-container) describes how to build and utilize custom containers on Agent Platform Workbench instances.

### Host image

**Image family:** `workbench-container-host`

The container host uses Google's Container Optimized OS (COS). The version cannot be specified when creating a new Agent Platform Workbench custom container instance. Instead, new instances use the latest COS image as the container host. The underlying image follows the latest stable OS version from COS. See the [Container-Optimized OS release notes](https://docs.cloud.google.com/container-optimized-os/docs/release-notes) .

### Custom container base images

Custom containers are built on top of the following Google-provided base containers when using Agent Platform Workbench instances:

  - Base Container: `us-docker.pkg.dev/deeplearning-platform-release/gcr.io/workbench-container:latest`
  - Slim Container: `us-docker.pkg.dev/deeplearning-platform-release/gcr.io/workbench-container-slim:latest`

The containers are tagged with their corresponding release tag, which can be observed in the Artifact Registry page.

### Create instance with container images

To create a Agent Platform Workbench instance using a custom container, the following methods can be used:

### gcloud

    gcloud workbench instances create INSTANCE_NAME \
      --project=PROJECT_ID \
      --location=ZONE \
      --container-repository=REGION-docker.pkg.dev/PROJECT_ID/REPOSITORY_NAME/IMAGE_NAME \
      --container-tag=latest

Replace the following:

  - `  INSTANCE_NAME  ` : the name of your instance.
  - `  PROJECT_ID  ` : your Google Cloud project ID.
  - `  ZONE  ` : the zone where you want to create the instance (for example, `us-central1-a` ).
  - `  REGION  ` : the region for the Artifact Registry repository (for example, `us` ).
  - `  REPOSITORY_NAME  ` : the name of your Artifact Registry repository.
  - `  IMAGE_NAME  ` : the name of your container image.

### Terraform

Set the `container_image` block within the `google_workbench_instance` resource.

    resource "google_workbench_instance" "container_instance" {
      # ... other configurations
      gce_setup {
        container_image {
          repository = "us-docker.pkg.dev/deeplearning-platform-release/gcr.io/workbench-container"
          tag  = "latest"
        }
      }
      # ...
    }

### Upgrading custom containers

To upgrade the container host image, see [Upgrade a VM image](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/manage-image-versions#upgrade-vm-image) for examples using `gcloud` or Terraform.

To upgrade the custom container image, a mutable tag (such as `:latest` ) can be used. When the custom container instance is restarted, the image is repulled if changes have been made to that tag in the registry. Alternatively, the instance can be updated to use a different image tag.
