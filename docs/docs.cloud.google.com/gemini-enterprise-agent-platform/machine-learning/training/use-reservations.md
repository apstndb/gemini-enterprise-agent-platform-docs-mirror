---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/use-reservations
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/use-reservations
title: Use reservations with training
description: Use Compute Engine reservations with Gemini Enterprise Agent Platform serverless training.
data_source: docs.cloud.google.com
---

This document explains how to use [Compute Engine reservations](https://docs.cloud.google.com/compute/docs/instances/reservations-overview) to gain a high level of assurance that your serverless training jobs have the necessary virtual machine (VM) resources to run.

Reservations are a Compute Engine feature. They help ensure that you have the resources available to create VMs with the same hardware (memory and vCPUs) and optional resources (CPUs, GPUs, TPUs, and Local SSD disks) whenever you need them.

When you create a reservation, Compute Engine verifies that the requested capacity is available in the specified zone. If so, then Compute Engine reserves the resources, creates the reservation, and the following happens:

  - You can immediately consume the reserved resources, and they remain available until you delete the reservation.
  - You're charged for the reserved resources at the same on-demand rate as running VMs, including any applicable discounts, until the reservation is deleted. A VM consuming a reservation doesn't incur separate charges. You're charged only for the resources outside of the reservation, such as disks or IP addresses. To learn more, see [pricing for reservations](https://docs.cloud.google.com/compute/docs/instances/reservations-overview#reservation-billing) .

## Limitations and requirements

When using Compute Engine reservations with Agent Platform, consider the following limitations and requirements:

  - Agent Platform can only use reservations for [CPUs](https://docs.cloud.google.com/compute/docs/cpu-platforms) , [GPU VMs](https://docs.cloud.google.com/compute/docs/gpus) , or [TPUs](https://docs.cloud.google.com/tpu/docs/intro-to-tpu) ( [Preview](https://cloud.google.com/products#product-launch-stages) ).

  - Agent Platform can't consume reservations of VMs that have [Local SSD disks manually attached](https://docs.cloud.google.com/compute/docs/disks/local-ssd#lssd_disk_options) .

  - Using Compute Engine reservations with Agent Platform is only supported for Gemini Enterprise Agent Platform serverless training, inference, and [Gemini Enterprise Agent Platform Workbench](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/reservations) (Preview).

  - A reservation's VM properties must match exactly with your Agent Platform workload to consume the reservation. For example, if a reservation specifies an `a2-ultragpu-8g` machine type, then the Agent Platform workload can only consume the reservation if it also uses an `a2-ultragpu-8g` machine type. See [Requirements](https://docs.cloud.google.com/compute/docs/instances/reservations-overview#requirements) .

  - To consume a shared reservation of GPU VMs or TPUs, you must consume it using its owner project or a consumer project with which the reservation is shared. See [How shared reservations work](https://docs.cloud.google.com/compute/docs/instances/reservations-overview#how-shared-reservations-work) .

  - To support regular updates of your Agent Platform deployments, we recommend increasing your VM count by at least 1 additional VM for each concurrent deployment.

  - Flex Start for Dynamic Workload Scheduler and [running training jobs on a persistent resource](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/persistent-resource-train) are both supported except when using Compute Engine reservations with Agent Platform training.

## Billing

When using Compute Engine reservations, you're billed for the following:

  - Compute Engine pricing for the Compute Engine resources, including any applicable committed use discounts (CUDs). See [Compute Engine pricing](https://cloud.google.com/compute/all-pricing) .
  - Agent Platform serverless training management fees in addition to your infrastructure usage. See [Custom-trained models pricing](https://cloud.google.com/products/gemini-enterprise-agent-platform/pricing#custom-trained_models) .

## Before you begin

  - Review the [requirements](https://docs.cloud.google.com/compute/docs/instances/reservations-overview#requirements) and [restrictions](https://docs.cloud.google.com/compute/docs/instances/reservations-overview#restrictions) for reservations.
  - Review the [quota requirements](https://docs.cloud.google.com/compute/docs/instances/reservations-overview#requirements-shared-reservations) and [restrictions](https://docs.cloud.google.com/compute/docs/instances/reservations-overview#restrictions-shared-reservations) for shared reservations.

## Allow a reservation to be consumed

Before consuming a reservation of CPUs, GPU VMs, or TPUs, you must set its [sharing policy](https://docs.cloud.google.com/compute/docs/instances/reservations-overview#sharing-policy) to allow Agent Platform to consume the reservation. To do so, use one of the following methods:

  - [Allow consumption while creating a reservation](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/use-reservations#allow-new-reservation)
  - [Allow consumption in an existing reservation](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/use-reservations#allow-existing-reservation)

### Allow consumption while creating a reservation

When creating a [single-project](https://docs.cloud.google.com/compute/docs/instances/reservations-single-project) or [shared reservation](https://docs.cloud.google.com/compute/docs/instances/reservations-shared) of GPU VMs, you can allow Agent Platform to consume the reservation as follows:

  - If you're using the Google Cloud console, then, in the **Google Cloud services** section, select **Share reservation** .
  - If you're using the Google Cloud CLI, then include the `--reservation-sharing-policy` flag set to `ALLOW_ALL` .
  - If you're using the REST API, then, in the request body, include the `serviceShareType` field set to `ALLOW_ALL` .

### Allow consumption of an existing reservation

You can modify an auto-created reservation of GPU VMs or TPUs for a future reservation only after the reservation's start time.

To allow Agent Platform to consume an existing reservation, use one of the following methods:

  - [Modify a reservation of GPU VMs](https://docs.cloud.google.com/compute/docs/instances/reservations-modify#modify-sharing-policy)
  - [Modify a reservation of TPUs](https://docs.cloud.google.com/tpu/docs/share-reservation#share-with-vertex)

## Verify that a reservation is consumed

To verify that the reservation is being consumed, see [Verify reservations consumption](https://docs.cloud.google.com/compute/docs/instances/reservations-consume#verify-consumption) in the Compute Engine documentation.

## Create a serverless training job with a reservation

Use the REST API to create a Gemini Enterprise Agent Platform serverless training job that consumes a Compute Engine reservation of GPU VMs.

### REST

Before using any of the request data, make the following replacements:

  - LOCATION : The region where the container or Python package will be run.
  - PROJECT\_ID : the project where the reservation was created in. To consume a shared reservation from another project, you must share the reservation with that project. For more information, see [Modify the consumer projects in a shared reservation](https://docs.cloud.google.com/compute/docs/instances/reservations-modify#modifying-consumer-projects-shared-reservation) .
  - JOB\_NAME : Required. A display name for the `CustomJob` .
  - MACHINE\_TYPE : the machine type to use for the job. Its default setting is `n1-standard-2` . For more information about the supported machine types, see [Configure compute resources for custom training](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/configure-compute) .
  - ACCELERATOR\_TYPE : the type of accelerator to attach to the machine. For more information about the type of GPU that each machine type supports, see [GPUs for compute workloads](https://docs.cloud.google.com/compute/docs/gpus#gpus_for_compute_workloads) .
  - ACCELERATOR\_COUNT : the number of accelerators to attach to the machine.
  - Define the custom training job:
      - RESERVATION\_AFFINITY\_TYPE : Must be `ANY_RESERVATION` , `SPECIFIC_RESERVATION` , or `NO_RESERVATION` .
        
          - `ANY_RESERVATION` means that the VMs of your `customJob` can automatically consume any reservation with matching properties.
          - `SPECIFIC_RESERVATION` means that the VMs of your `customJob` can consume only a reservation that the VMs specifically target by name.
          - `NO_RESERVATION` means that the VMs of your `customJob` can't consume any reservation. Specifying `NO_RESERVATION` has the same effect as omitting a reservation affinity specification.
    
      - ZONE : the zone where the reservation was created.
    
      - RESERVATION\_NAME : the name of your reservation.
    
      - DISK\_TYPE : Optional. The type of the boot disk to use for the job, either `pd-standard` (default) or `pd-ssd` . [Learn more about disk types.](https://docs.cloud.google.com/compute/docs/disks#disk-types)
    
      - DISK\_SIZE : Optional. The size in GB of the boot disk to use for the job. The default value is 100.
    
      - REPLICA\_COUNT : the number of worker replicas to use. In most cases, set this to `1` for your [first worker pool](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/create-custom-job#configure_distributed_training) .
    
      - If your training application runs in a custom container, specify the following:
        
          - CUSTOM\_CONTAINER\_IMAGE\_URI : The URI of a container image in Artifact Registry or Docker Hub that is to be run on each worker replica.
          - CUSTOM\_CONTAINER\_COMMAND : Optional. The command to be invoked when the container is started. This command overrides the container's default entrypoint.
          - CUSTOM\_CONTAINER\_ARGS : Optional. The arguments to be passed when starting the container.
    
      - If your training application is a Python package that runs in a prebuilt container, specify the following:
        
          - EXECUTOR\_IMAGE\_URI : The URI of the container image that runs the provided code. Refer to the [available prebuilt containers for training](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/pre-built-containers) .
          - PYTHON\_PACKAGE\_URIS : Comma-separated list of Cloud Storage URIs specifying the Python package files which are the training program and its dependent packages. The maximum number of package URIs is 100.
          - PYTHON\_MODULE : The Python module name to run after installing the packages.
          - PYTHON\_PACKAGE\_ARGS : Optional. Command-line arguments to be passed to the Python module.
    
      - TIMEOUT : Optional. The maximum running time for the job.
  - Specify the LABEL\_NAME and LABEL\_VALUE for any labels that you want to apply to this custom job.

HTTP method and URL:

    POST https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/customJobs

Request JSON body:

    {
      "displayName": "JOB_NAME",
      "jobSpec": {
        "workerPoolSpecs": [
          {
            "machineSpec": {
              "machineType": "MACHINE_TYPE",
              "acceleratorType": "ACCELERATOR_TYPE",
              "acceleratorCount": ACCELERATOR_COUNT,
              "reservationAffinity": {
                "reservationAffinityType": "RESERVATION_AFFINITY_TYPE",
                // Use the following key and values only if
                // the reservationAffinityType is SPECIFIC_RESERVATION.
                "key": "compute.googleapis.com/reservation-name",
                "values": [
                  "projects/PROJECT_ID/zones/ZONE/reservations/RESERVATION_NAME"
                ]
              },
            },
            "replicaCount": REPLICA_COUNT,
            "diskSpec": {
              "bootDiskType": DISK_TYPE,
              "bootDiskSizeGb": DISK_SIZE
            },
    
            // Union field task can be only one of the following:
            "containerSpec": {
              "imageUri": CUSTOM_CONTAINER_IMAGE_URI,
              "command": [
                CUSTOM_CONTAINER_COMMAND
              ],
              "args": [
                CUSTOM_CONTAINER_ARGS
              ]
            },
            "pythonPackageSpec": {
              "executorImageUri": EXECUTOR_IMAGE_URI,
              "packageUris": [
                PYTHON_PACKAGE_URIS
              ],
              "pythonModule": PYTHON_MODULE,
              "args": [
                PYTHON_PACKAGE_ARGS
              ]
            }
            // End of list of possible types for union field task.
          }
          // Specify one workerPoolSpec for single replica training, or multiple workerPoolSpecs
          // for distributed training.
        ],
        "scheduling": {
          "timeout": TIMEOUT
        }
      },
      "labels": {
        LABEL_NAME_1": LABEL_VALUE_1,
        LABEL_NAME_2": LABEL_VALUE_2
      }
    }

To send your request, choose one of these options:

#### curl

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) , or by using [Cloud Shell](https://docs.cloud.google.com/shell/docs) , which automatically logs you into the `gcloud` CLI . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Save the request body in a file named `request.json` , and execute the following command:

    curl -X POST \
         -H "Authorization: Bearer $(gcloud auth print-access-token)" \
         -H "Content-Type: application/json; charset=utf-8" \
         -d @request.json \
         "https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/customJobs"

#### PowerShell

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Save the request body in a file named `request.json` , and execute the following command:

    $cred = gcloud auth print-access-token
    $headers = @{ "Authorization" = "Bearer $cred" }
    
    Invoke-WebRequest `
        -Method POST `
        -Headers $headers `
        -ContentType: "application/json; charset=utf-8" `
        -InFile request.json `
        -Uri "https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/customJobs" | Select-Object -Expand Content

The response contains information about specifications as well as the TRAININGPIPELINE\_ID .

#### Response

    {
      "name": "projects/PROJECT_ID/locations/LOCATION/customJobs/JOB_ID",
      "displayName": "JOB_NAME",
      "trainingTaskInputs": {
        "workerPoolSpecs": [
          {
            "machineSpec": {
              "machineType": "MACHINE_TYPE",
              "acceleratorType": "ACCELERATOR_TYPE",
              "acceleratorCount": ACCELERATOR_COUNT
            },
            "replicaCount": "1",
            "pythonPackageSpec": {
              "executorImageUri": "us-docker.pkg.dev/vertex-ai/training/training-tf-cpu.2-1:latest",
              "packageUris": [
                "gs://BUCKET_NAME/training/hello-custom-training-1.0.tar.gz"
              ],
              "pythonModule": "trainer.task",
              "args": [
                "--model-dir=gs://BUCKET_NAME/output/"
              ]
            }
          }
        ]
      },
      "state": "JOB_STATE_PENDING",
      "createTime": "2020-09-15T19:09:54.342080Z",
      "startTime": "2020-09-15T19:13:42.991045Z",
    }

## What's next

  - Learn more about [reservations of Compute Engine zonal resources](https://docs.cloud.google.com/compute/docs/instances/reservations-overview) .
  - Learn how to [use reservations with Agent Platform online inference](https://docs.cloud.google.com/vertex-ai/docs/predictions/use-reservations) .
  - Learn how to [use reservations with Agent Platform batch inference](https://docs.cloud.google.com/vertex-ai/docs/predictions/use-reservations-batch) .
  - Learn how to [view reservations](https://docs.cloud.google.com/compute/docs/instances/reservations-view) .
  - Learn how to [monitor reservations consumption](https://docs.cloud.google.com/compute/docs/instances/reservations-monitor) .
