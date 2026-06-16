---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/use-reservations-batch
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/use-reservations-batch
title: Use reservations with batch inference
description: Use Compute Engine reservations with Gemini Enterprise Agent Platform batch inference.
data_source: docs.cloud.google.com
---

> **Preview**
> 
> This feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](https://docs.cloud.google.com/terms/service-terms#1) . Pre-GA features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

This document explains how to use [Compute Engine reservations](https://docs.cloud.google.com/compute/docs/instances/reservations-overview) to gain a high level of assurance that your batch inference jobs have the necessary virtual machine (VM) resources to run.

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

  - To consume a `SPECIFIC_RESERVATION` reservation, grant the [Compute Viewer](https://docs.cloud.google.com/iam/docs/roles-permissions/compute#compute.viewer) IAM role to the Agent Platform service account in the project that owns the reservations ( `service-${ PROJECT_NUMBER }@gcp-sa-aiplatform.iam.gserviceaccount.com` , where PROJECT\_NUMBER is the project number of the project that consumes the reservation).

  - The following services and capabilities aren't supported when using Compute Engine reservations with Agent Platform batch inference:
    
      - Federal Risk and Authorization Management Program (FedRAMP) compliance

## Billing

When using Compute Engine reservations, you're billed for the following:

  - Compute Engine pricing for the Compute Engine resources, including any applicable committed use discounts (CUDs). See [Compute Engine pricing](https://cloud.google.com/compute/all-pricing) .
  - Agent Platform batch inference management fees in addition to your infrastructure usage. See [Prediction pricing](https://cloud.google.com/products/gemini-enterprise-agent-platform/pricing#prediction-prices) .

## Before you begin

  - Review the [requirements](https://docs.cloud.google.com/compute/docs/instances/reservations-overview#requirements) and [restrictions](https://docs.cloud.google.com/compute/docs/instances/reservations-overview#restrictions) for reservations.
  - Review the [quota requirements](https://docs.cloud.google.com/compute/docs/instances/reservations-overview#requirements-shared-reservations) and [restrictions](https://docs.cloud.google.com/compute/docs/instances/reservations-overview#restrictions-shared-reservations) for shared reservations.

## Allow a reservation to be consumed

Before consuming a reservation of CPUs, GPU VMs, or TPUs, you must set its [sharing policy](https://docs.cloud.google.com/compute/docs/instances/reservations-overview#sharing-policy) to allow Agent Platform to consume the reservation. To do so, use one of the following methods:

  - [Allow consumption while creating a reservation](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/use-reservations-batch#allow-new-reservation)
  - [Allow consumption in an existing reservation](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/use-reservations-batch#allow-existing-reservation)

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

## Get batch inferences by using a reservation

To create a batch inference request that consumes a Compute Engine reservation of GPU VMs, you can use the REST API and choose either Cloud Storage or BigQuery for the source and destination.

### Cloud Storage

Before using any of the request data, make the following replacements:

  - LOCATION\_ID : The region where the model is stored and the batch prediction job is executed. For example, `us-central1` .

  - PROJECT\_ID : The project where the reservation was created. To consume a shared reservation from another project, you must share the reservation with that project. For more information, see [Modify the consumer projects in a shared reservation](https://docs.cloud.google.com/compute/docs/instances/reservations-modify#modifying-consumer-projects-shared-reservation) .

  - BATCH\_JOB\_NAME : A display name for the batch prediction job.

  - MODEL\_ID : The ID for the model to use for making predictions.

  - INPUT\_FORMAT : The [format of your input data](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/use-reservations-batch#input_data_requirements) : `jsonl` , `csv` , `tf-record` , `tf-record-gzip` , or `file-list` .

  - INPUT\_URI : The Cloud Storage URI of your input data. May contain wildcards.

  - OUTPUT\_DIRECTORY : The Cloud Storage URI of a directory where you want Agent Platform to save output.

  - MACHINE\_TYPE : The [machine resources](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/configure-compute) to be used for this batch prediction job.

  - ACCELERATOR\_TYPE : The type of accelerator to attach to the machine. For more information about the type of GPU that each machine type supports, see [GPUs for compute workloads](https://docs.cloud.google.com/compute/docs/gpus#gpus_for_compute_workloads) .

  - ACCELERATOR\_COUNT : The number of accelerators to attach to the machine.

  - RESERVATION\_AFFINITY\_TYPE : Must be `ANY` , `SPECIFIC_RESERVATION` , or `NONE` .
    
      - `ANY` means that the VMs of your `customJob` can automatically consume any reservation with matching properties.
      - `SPECIFIC_RESERVATION` means that the VMs of your `customJob` can only consume a reservation that the VMs specifically targets by name.
      - `NONE` means that the VMs of your `customJob` can't consume any reservation. Specifying `NONE` has the same effect as omitting a reservation affinity specification.

  - BATCH\_SIZE : The number of instances to send in each prediction request; the default is 64. Increasing the batch size can lead to higher throughput, but it can also cause request timeouts.

  - STARTING\_REPLICA\_COUNT : The number of nodes for this batch prediction job.

HTTP method and URL:

    POST https://LOCATION_ID-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION_ID/batchPredictionJobs

Request JSON body:

    {
      "displayName": "BATCH_JOB_NAME",
      "model": "projects/PROJECT_ID/locations/LOCATION_ID/models/MODEL_ID",
      "inputConfig": {
        "instancesFormat": "INPUT_FORMAT",
        "gcsSource": {
          "uris": ["INPUT_URI"],
        },
      },
      "outputConfig": {
        "predictionsFormat": "jsonl",
        "gcsDestination": {
          "outputUriPrefix": "OUTPUT_DIRECTORY",
        },
      },
      "dedicatedResources" : {
        "machineSpec" : {
          "machineType": MACHINE_TYPE,
          "acceleratorType": "ACCELERATOR_TYPE",
          "acceleratorCount": ACCELERATOR_COUNT,
          "reservationAffinity": {
            "reservationAffinityType": "RESERVATION_AFFINITY_TYPE",
            "key": "compute.googleapis.com/reservation-name",
            "values": [
              "projects/PROJECT_ID/zones/ZONE/reservations/RESERVATION_NAME"
            ]
          }
        },
        "startingReplicaCount": STARTING_REPLICA_COUNT
      },
      "manualBatchTuningParameters": {
        "batch_size": BATCH_SIZE,
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
         "https://LOCATION_ID-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION_ID/batchPredictionJobs"

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
        -Uri "https://LOCATION_ID-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION_ID/batchPredictionJobs" | Select-Object -Expand Content

You should receive a JSON response similar to the following:

    {
      "name": "projects/PROJECT_NUMBER/locations/LOCATION_ID/batchPredictionJobs/BATCH_JOB_ID",
      "displayName": "BATCH_JOB_NAME 202005291958",
      "model": "projects/PROJECT_ID/locations/LOCATION_ID/models/MODEL_ID",
      "inputConfig": {
        "instancesFormat": "jsonl",
        "gcsSource": {
          "uris": [
            "INPUT_URI"
          ]
        }
      },
      "outputConfig": {
        "predictionsFormat": "jsonl",
        "gcsDestination": {
          "outputUriPrefix": "OUTPUT_DIRECTORY"
        }
      },
      "state": "JOB_STATE_PENDING",
      "createTime": "2020-05-30T02:58:44.341643Z",
      "updateTime": "2020-05-30T02:58:44.341643Z",
    }

### BigQuery

Before using any of the request data, make the following replacements:

  - LOCATION\_ID : The region where the model is stored and the batch prediction job is executed. For example, `us-central1` .

  - PROJECT\_ID : The project where the reservation was created. To consume a shared reservation from another project, you must share the reservation with that project. For more information, see [Modify the consumer projects in a shared reservation](https://docs.cloud.google.com/compute/docs/instances/reservations-modify#modifying-consumer-projects-shared-reservation) .

  - BATCH\_JOB\_NAME : A display name for the batch prediction job.

  - MODEL\_ID : The ID for the model to use for making predictions.

  - INPUT\_PROJECT\_ID : The ID of the Google Cloud project where you want to get the data from.

  - INPUT\_DATASET\_NAME : The name of the BigQuery dataset where you want to get the data from.

  - INPUT\_TABLE\_NAME : The name of the BigQuery table where you want to get the data from.

  - OUTPUT\_PROJECT\_ID : The ID of the Google Cloud project where you want to save the output.

  - OUTPUT\_DATASET\_NAME : The name of the destination BigQuery dataset where you want to save the output.

  - OUTPUT\_TABLE\_NAME : The name of the BigQuery destination table where you want to save the output.

  - MACHINE\_TYPE : The [machine resources](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/configure-compute) to be used for this batch prediction job.

  - ACCELERATOR\_TYPE : The type of accelerator to attach to the machine. For more information about the type of GPU that each machine type supports, see [GPUs for compute workloads](https://docs.cloud.google.com/compute/docs/gpus#gpus_for_compute_workloads) .

  - ACCELERATOR\_COUNT : The number of accelerators to attach to the machine.

  - RESERVATION\_AFFINITY\_TYPE : Must be `ANY` , `SPECIFIC_RESERVATION` , or `NONE` .
    
      - `ANY` means that the VMs of your `customJob` can automatically consume any reservation with matching properties.
      - `SPECIFIC_RESERVATION` means that the VMs of your `customJob` can only consume a reservation that the VMs specifically targets by name.
      - `NONE` means that the VMs of your `customJob` can't consume any reservation. Specifying `NONE` has the same effect as omitting a reservation affinity specification.

  - BATCH\_SIZE : The number of instances to send in each prediction request; the default is 64. Increasing the batch size can lead to higher throughput, but it can also cause request timeouts.

  - STARTING\_REPLICA\_COUNT : The number of nodes for this batch prediction job.

HTTP method and URL:

    POST https://LOCATION_ID-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION_ID/batchPredictionJobs

Request JSON body:

    {
      "displayName": "BATCH_JOB_NAME",
      "model": "projects/PROJECT_ID/locations/LOCATION_ID/models/MODEL_ID",
      "inputConfig": {
        "instancesFormat": "bigquery",
        "bigquerySource": {
          "inputUri": "bq://INPUT_PROJECT_ID.INPUT_DATASET_NAME.INPUT_TABLE_NAME"
        },
      },
      "outputConfig": {
        "predictionsFormat":"bigquery",
        "bigqueryDestination":{
          "outputUri": "bq://OUTPUT_PROJECT_ID.OUTPUT_DATASET_NAME.OUTPUT_TABLE_NAME"
        }
      },
      "dedicatedResources" : {
        "machineSpec" : {
          "machineType": MACHINE_TYPE,
          "acceleratorType": "ACCELERATOR_TYPE",
          "acceleratorCount": ACCELERATOR_COUNT,
          "reservationAffinity": {
            "reservationAffinityType": "RESERVATION_AFFINITY_TYPE",
            "key": "compute.googleapis.com/reservation-name",
            "values": [
              "projects/PROJECT_ID/zones/ZONE/reservations/RESERVATION_NAME"
            ]
          }
        },
        "startingReplicaCount": STARTING_REPLICA_COUNT
      },
      "manualBatchTuningParameters": {
        "batch_size": BATCH_SIZE,
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
         "https://LOCATION_ID-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION_ID/batchPredictionJobs"

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
        -Uri "https://LOCATION_ID-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION_ID/batchPredictionJobs" | Select-Object -Expand Content

You should receive a JSON response similar to the following:

    {
      "name": "projects/PROJECT_NUMBER/locations/LOCATION_ID/batchPredictionJobs/BATCH_JOB_ID",
      "displayName": "BATCH_JOB_NAME 202005291958",
      "model": "projects/PROJECT_ID/locations/LOCATION_ID/models/MODEL_ID",
      "inputConfig": {
        "instancesFormat": "jsonl",
        "bigquerySource": {
          "uris": [
            "INPUT_URI"
          ]
        }
      },
      "outputConfig": {
        "predictionsFormat": "jsonl",
        "bigqueryDestination": {
          "outputUri": "OUTPUT_URI"
        }
      },
      "state": "JOB_STATE_PENDING",
      "createTime": "2020-05-30T02:58:44.341643Z",
      "updateTime": "2020-05-30T02:58:44.341643Z",
    }

### Retrieve batch inference results

When a batch inference task is complete, the output of the inference is stored in the Cloud Storage bucket or BigQuery location that you specified in your request.

## What's next

  - Learn more about [reservations of Compute Engine zonal resources](https://docs.cloud.google.com/compute/docs/instances/reservations-overview) .
  - Learn how to [use reservations with Agent Platform online inference](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/use-reservations) .
  - Learn how to [use reservations with Agent Platform training](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/use-reservations) .
  - Learn how to [view reservations](https://docs.cloud.google.com/compute/docs/instances/reservations-view) .
  - Learn how to [monitor reservations consumption](https://docs.cloud.google.com/compute/docs/instances/reservations-monitor) .
