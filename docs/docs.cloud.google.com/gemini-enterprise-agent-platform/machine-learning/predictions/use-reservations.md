---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/use-reservations
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/use-reservations
title: Use reservations with online inference
description: Use Compute Engine reservations with Gemini Enterprise Agent Platform online inference.
data_source: docs.cloud.google.com
---

This document explains how to use [Compute Engine reservations](https://docs.cloud.google.com/compute/docs/instances/reservations-overview) to gain a high level of assurance that your online inference jobs have the necessary virtual machine (VM) resources to run.

Reservations are a Compute Engine feature. They help ensure that you have the resources available to create VMs with the same hardware (memory and vCPUs) and optional resources (CPUs, GPUs, TPUs, and Local SSD disks) whenever you need them.

When you create a reservation, Compute Engine verifies that the requested capacity is available in the specified zone. If so, then Compute Engine reserves the resources, creates the reservation, and the following happens:

  - You can immediately consume the reserved resources, and they remain available until you delete the reservation.
  - You're charged for the reserved resources at the same on-demand rate as running VMs, including any applicable discounts, until the reservation is deleted. A VM consuming a reservation doesn't incur separate charges. You're charged only for the resources outside of the reservation, such as disks or IP addresses. To learn more, see [pricing for reservations](https://docs.cloud.google.com/compute/docs/instances/reservations-overview#reservation-billing) .

## Limitations and requirements

When using Compute Engine reservations with Agent Platform, consider the following limitations and requirements:

Agent Platform can only use reservations for [CPUs](https://docs.cloud.google.com/compute/docs/cpu-platforms) , [GPU VMs](https://docs.cloud.google.com/compute/docs/gpus) , or [TPUs](https://docs.cloud.google.com/tpu/docs/intro-to-tpu) ( [Preview](https://cloud.google.com/products#product-launch-stages) ).

Agent Platform can't consume reservations of VMs that have [Local SSD disks manually attached](https://docs.cloud.google.com/compute/docs/disks/local-ssd#lssd_disk_options) .

Using Compute Engine reservations with Agent Platform is only supported for Gemini Enterprise Agent Platform serverless training, inference, and [Gemini Enterprise Agent Platform Workbench](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/instances/reservations) (Preview).

A reservation's VM properties must match exactly with your Agent Platform workload to consume the reservation. For example, if a reservation specifies an `a2-ultragpu-8g` machine type, then the Agent Platform workload can only consume the reservation if it also uses an `a2-ultragpu-8g` machine type. See [Requirements](https://docs.cloud.google.com/compute/docs/instances/reservations-overview#requirements) .

To consume a shared reservation of GPU VMs or TPUs, you must consume it using its owner project or a consumer project with which the reservation is shared. See [How shared reservations work](https://docs.cloud.google.com/compute/docs/instances/reservations-overview#how-shared-reservations-work) .

To support regular updates of your Agent Platform deployments, we recommend increasing your VM count by more than the total number of replicas as follows, according to the reservation type used by your [`DeployedModel`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.endpoints#DeployedModel) :

`SPECIFIC_RESERVATION` : Must specify at least 1 additional VM; we recommend 10% (but at least 1). Deployed models using `SPECIFIC_RESERVATION` are guaranteed to only consume VMs from the reservation. Agent Platform cannot perform updates if there is no additional VM.

`ANY` :

  - Not required to have additional VMs, because deployed models using `ANY` reservation use on-demand VMs if the reservation capacity is not enough. However, without additional VMs, your reservation might not be fully utilized after an upgrade. For example, suppose you have a reservation with 40 VMs and deploy a model with 40 replicas using that reservation. When you first deploy, all 40 VMs in the reservation are used by the `DeployedModel` . After an upgrade, only 36 VMs are from the reservation, and 4 VMs are on-demand.
  - If you want to keep the usage within the reservation, we recommend having at least 1 additional VM for each `DeployedModel` or `DeploymentResourcePool` using the reservation. If the total number of VMs of the same type in your `ANY` reservations is less than 50, we recommend 10% (but at least 1) more. If it's greater than 50, we recommend 25% more. For example:
      - If you plan to deploy models using 40 A3 VMs, you can have 1 A3 reservation with 44 VMs, or 2 A3 reservations: reservation X with 30 VMs, and reservation Y with 14 VMs (44 in total). The same applies to other numbers of reservations, as long as they are all shared with Agent Platform and the total number of VMs in those reservations is at least 44.
      - If you plan to deploy models using 100 A3 VMs, the total number of VMs in all A3 reservations shared with Agent Platform should be at least 125.
      - If you plan to deploy 2 models using 10 VMs, the total number of VMs in all A3 reservations shared with Agent Platform should be at least 12. The number of VMs is less than 50, but the number of additional VMs is 2 (1 per `DeployedModel` ).

To consume a `SPECIFIC_RESERVATION` reservation, grant the [Compute Viewer](https://docs.cloud.google.com/iam/docs/roles-permissions/compute#compute.viewer) IAM role to the Agent Platform service account in the project that owns the reservations ( `service-${ PROJECT_NUMBER }@gcp-sa-aiplatform.iam.gserviceaccount.com` , where PROJECT\_NUMBER is the project number of the project that consumes the reservation).

## Billing

When using Compute Engine reservations, you're billed for the following:

  - Compute Engine pricing for the Compute Engine resources, including any applicable committed use discounts (CUDs). See [Compute Engine pricing](https://cloud.google.com/compute/all-pricing) .
  - Agent Platform online inference management fees in addition to your infrastructure usage. See [Prediction pricing](https://cloud.google.com/products/gemini-enterprise-agent-platform/pricing#prediction-prices) .

> **Note:** When consuming from a reservation or spot capacity, billing is spread across two SKUs: the Compute Engine SKU with the label `goog-vertex-ai-product:vertex-ai-online-prediction` and the Agent Platform Management Fee SKU. This enables you to use your Committed Use Discounts (CUDs) in Agent Platform.

## Before you begin

  - Review the [requirements](https://docs.cloud.google.com/compute/docs/instances/reservations-overview#requirements) and [restrictions](https://docs.cloud.google.com/compute/docs/instances/reservations-overview#restrictions) for reservations.
  - Review the [quota requirements](https://docs.cloud.google.com/compute/docs/instances/reservations-overview#requirements-shared-reservations) and [restrictions](https://docs.cloud.google.com/compute/docs/instances/reservations-overview#restrictions-shared-reservations) for shared reservations.

## Allow a reservation to be consumed

Before consuming a reservation of CPUs, GPU VMs, or TPUs, you must set its [sharing policy](https://docs.cloud.google.com/compute/docs/instances/reservations-overview#sharing-policy) to allow Agent Platform to consume the reservation. To do so, use one of the following methods:

  - [Allow consumption while creating a reservation](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/use-reservations#allow-new-reservation)
  - [Allow consumption in an existing reservation](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/use-reservations#allow-existing-reservation)

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

### Allow consumption of multiple specific reservations

> **Preview**
> 
> This feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](https://docs.cloud.google.com/terms/service-terms#1) . Pre-GA features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

You can allow consumption of multiple specific reservations by specifying two or more reservations, in priority order, in the list of reservation names in the `values` field of the reservation affinity specification. You should list them in order of priority.

Each reservation must be shared with Vertex, and the zone of the reservation must be in the region of the endpoint. Otherwise, you can mix reservations across source projects and multiple zones.

## Verify that a reservation is consumed

To verify that the reservation is being consumed, see [Verify reservations consumption](https://docs.cloud.google.com/compute/docs/instances/reservations-consume#verify-consumption) in the Compute Engine documentation.

## Get online inferences by using a reservation

To create a model deployment that consumes a Compute Engine reservation of GPU VMs, use the REST API or Agent Platform SDK for Python.

### REST

Before using any of the request data, make the following replacements:

  - LOCATION\_ID : The region where you are using Agent Platform.
  - PROJECT\_ID : the project where the reservation was created. To consume a shared reservation from another project, you must share the reservation with that project. For more information, see [Modify the consumer projects in a shared reservation](https://docs.cloud.google.com/compute/docs/instances/reservations-modify#modifying-consumer-projects-shared-reservation) .
  - ENDPOINT\_ID : The ID for the endpoint.
  - MODEL\_ID : The ID for the model to be deployed.
  - DEPLOYED\_MODEL\_NAME : A name for the `DeployedModel` . You can use the display name of the `Model` for the `DeployedModel` as well.
  - MACHINE\_TYPE : the machine type to use for each node in this deployment. Its default setting is `n1-standard-2` . For more information about the supported machine types, see [Configure compute resources for prediction](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/configure-compute) .
  - ACCELERATOR\_TYPE : the type of accelerator to attach to the machine. For more information about the type of GPU that each machine type supports, see [GPUs for compute workloads](https://docs.cloud.google.com/compute/docs/gpus#gpus_for_compute_workloads) .
  - ACCELERATOR\_COUNT : the number of accelerators to attach to the machine.
  - RESERVATION\_AFFINITY\_TYPE : Must be `ANY` , `SPECIFIC_RESERVATION` , or `NONE` .
      - `ANY` means that the VMs of your `customJob` automatically can consume any reservation with matching properties.
      - `SPECIFIC_RESERVATION` means that the VMs of your `customJob` can consume only reservations that the VMs specifically target by name.
      - `NONE` means that the VMs of your `customJob` can't consume any reservation. Specifying `NONE` has the same effect as omitting a reservation affinity specification.
  - ZONE : the zone where the reservation was created.
  - RESERVATION\_NAME\_N : the names of your reservations, in priority order. Each must be the full resource name of the reservation or reservation block.
  - MIN\_REPLICA\_COUNT : The minimum number of nodes for this deployment. The node count can be increased or decreased as required by the inference load, up to the maximum number of nodes and never fewer than this number of nodes. This value must be greater than or equal to 1.
  - MAX\_REPLICA\_COUNT : The maximum number of nodes for this deployment. The node count can be increased or decreased as required by the inference load, up to this number of nodes and never fewer than the minimum number of nodes.
  - TRAFFIC\_SPLIT\_THIS\_MODEL : the percentage of the prediction traffic to this endpoint to be routed to the model being deployed with this operation. Defaults to 100. All traffic percentages must add up to 100. [Learn more about traffic splits](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/deployment#models-endpoint) .
  - DEPLOYED\_MODEL\_ID\_N : Optional. If other models are deployed to this endpoint, you must update their traffic split percentages so that all percentages add up to 100.
  - TRAFFIC\_SPLIT\_MODEL\_N : the traffic split percentage value for the deployed model ID key.
  - PROJECT\_NUMBER : Your project's automatically generated [project number](https://docs.cloud.google.com/resource-manager/docs/creating-managing-projects#identifiers) .

HTTP method and URL:

    POST https://LOCATION_ID-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION_ID/endpoints/ENDPOINT_ID:deployModel

Request JSON body:

    {
      "deployedModel": {
        "model": "projects/PROJECT/locations/LOCATION_ID/models/MODEL_ID",
        "displayName": "DEPLOYED_MODEL_NAME",
        "dedicatedResources": {
          "machineSpec": {
            "machineType": "MACHINE_TYPE",
            "acceleratorType": "ACCELERATOR_TYPE",
            "acceleratorCount": ACCELERATOR_COUNT,
            "reservationAffinity": {
              "reservationAffinityType": "RESERVATION_AFFINITY_TYPE",
              "key": "compute.googleapis.com/reservation-name",
              "values": [
                "projects/PROJECT_ID/zones/ZONE/reservations/RESERVATION_NAME_1",
                "projects/PROJECT_ID/zones/ZONE/reservations/RESERVATION_NAME_2"
              ]
            }
          },
          "minReplicaCount": MIN_REPLICA_COUNT,
          "maxReplicaCount": MAX_REPLICA_COUNT
        },
      },
      "trafficSplit": {
        "0": TRAFFIC_SPLIT_THIS_MODEL,
        "DEPLOYED_MODEL_ID_1": TRAFFIC_SPLIT_MODEL_1,
        "DEPLOYED_MODEL_ID_2": TRAFFIC_SPLIT_MODEL_2
      },
    }

To send your request, expand one of these options:

#### curl (Linux, macOS, or Cloud Shell)

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) , or by using [Cloud Shell](https://docs.cloud.google.com/shell/docs) , which automatically logs you into the `gcloud` CLI . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Save the request body in a file named `request.json` , and execute the following command:

    curl -X POST \
         -H "Authorization: Bearer $(gcloud auth print-access-token)" \
         -H "Content-Type: application/json; charset=utf-8" \
         -d @request.json \
         "https://LOCATION_ID-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION_ID/endpoints/ENDPOINT_ID:deployModel"

#### PowerShell (Windows)

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Save the request body in a file named `request.json` , and execute the following command:

    $cred = gcloud auth print-access-token
    $headers = @{ "Authorization" = "Bearer $cred" }
    
    Invoke-WebRequest `
        -Method POST `
        -Headers $headers `
        -ContentType: "application/json; charset=utf-8" `
        -InFile request.json `
        -Uri "https://LOCATION_ID-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION_ID/endpoints/ENDPOINT_ID:deployModel" | Select-Object -Expand Content

You should receive a JSON response similar to the following:

    {
      "name": "projects/PROJECT_ID/locations/LOCATION_ID/endpoints/ENDPOINT_ID/operations/OPERATION_ID",
      "metadata": {
        "@type": "type.googleapis.com/google.cloud.aiplatform.v1beta1.DeployModelOperationMetadata",
        "genericMetadata": {
          "createTime": "2020-10-19T17:53:16.502088Z",
          "updateTime": "2020-10-19T17:53:16.502088Z"
        }
      }
    }

### Python

To learn how to install or update the Agent Platform SDK for Python, see [Install the Agent Platform SDK for Python](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/start/install-sdk) . For more information, see the [Agent Platform SDK for Python API reference documentation](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest) .

Before running any of the following scripts, make the following replacements:

  - DEPLOYED\_NAME : a name for the deployed model.
  - TRAFFIC\_SPLIT : the traffic split percentage value for the deployed model ID key.
  - MACHINE\_TYPE : the machine used for each node of this deployment. Its default setting is `n1-standard-2` . Learn more about [machine types](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/configure-compute) .
  - ACCELERATOR\_TYPE : the type of accelerator to attach to the machine. For more information about the type of GPU that each machine type supports, see [GPUs for compute workloads](https://docs.cloud.google.com/compute/docs/gpus#gpus_for_compute_workloads) .
  - ACCELERATOR\_COUNT : the number of accelerators to attach to the machine.
  - PROJECT\_ID : the project where the reservation was created in. To consume a shared reservation from another project, you must share the reservation with that project. For more information, see [Modify the consumer projects in a shared reservation](https://docs.cloud.google.com/compute/docs/instances/reservations-modify#modifying-consumer-projects-shared-reservation) .
  - ZONE : the zone where the reservation is located.
  - RESERVATION\_NAME\_N : the names of your reservations, in priority order. Each must be the full resource name of the reservation or reservation block.
  - MIN\_REPLICA\_COUNT : The minimum number of nodes for this deployment. The node count can be increased or decreased as required by the inference load, up to the maximum number of nodes and never fewer than this number of nodes. This value must be greater than or equal to 1.
  - MAX\_REPLICA\_COUNT : The maximum number of nodes for this deployment. The node count can be increased or decreased as required by the inference load, up to this number of nodes and never fewer than the minimum number of nodes.

Depending on the type of reservation that you want to consume, do one of the following:

  - To consume one or more specific reservations:
    
        endpoint5.deploy(
            model = model,
            deployed_model_display_name=DEPLOYED_NAME,
            traffic_split=TRAFFIC_SPLIT,
            machine_type="MACHINE_TYPE",
            accelerator_type="ACCELERATOR_TYPE",
            accelerator_count=ACCELERATOR_COUNT,
            reservation_affinity_type="SPECIFIC_RESERVATION",
            reservation_affinity_key="compute.googleapis.com/reservation-name",
            reservation_affinity_values=[
                "projects/PROJECT_ID/zones/ZONE/reservations/RESERVATION_NAME_1",
                "projects/PROJECT_ID/zones/ZONE/reservations/RESERVATION_NAME_2"
                ],
            min_replica_count=MIN_REPLICA_COUNT,
            max_replica_count=MAX_REPLICA_COUNT,
            sync=True
        )

  - To consume an automatically consumed reservation:
    
        endpoint5.deploy(
            model = model,
            deployed_model_display_name=DEPLOYED_NAME,
            traffic_split=TRAFFIC_SPLIT,
            machine_type="MACHINE_TYPE",
            accelerator_type="ACCELERATOR_TYPE",
            accelerator_count=ACCELERATOR_COUNT,
            reservation_affinity_type="ANY_RESERVATION",
            min_replica_count=MIN_REPLICA_COUNT,
            max_replica_count=MAX_REPLICA_COUNT,
            sync=True
        )

## What's next

  - Learn more about [reservations of Compute Engine zonal resources](https://docs.cloud.google.com/compute/docs/instances/reservations-overview) .
  - Learn how to [use reservations with Agent Platform batch inference](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/use-reservations-batch) .
  - Learn how to [use reservations with Agent Platform training](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/use-reservations) .
  - Learn how to [view reservations](https://docs.cloud.google.com/compute/docs/instances/reservations-view) .
  - Learn how to [monitor reservations consumption](https://docs.cloud.google.com/compute/docs/instances/reservations-monitor) .
