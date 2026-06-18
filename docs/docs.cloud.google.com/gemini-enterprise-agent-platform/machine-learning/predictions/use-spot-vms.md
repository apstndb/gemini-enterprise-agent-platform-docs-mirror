---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/use-spot-vms
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/use-spot-vms
title: Use Spot VMs with inference
description: Use Spot VMs with Agent Platform inference.
data_source: docs.cloud.google.com
---

## Overview

You can reduce the cost of running your prediction jobs by using Spot VMs. Spot VMs are virtual machine (VM) instances that are excess Compute Engine capacity. Spot VMs have significant discounts, but Compute Engine might preemptively stop or delete (preempt) Spot VMs to reclaim the capacity at any time.

To learn more, see [Spot VMs](https://docs.cloud.google.com/compute/docs/instances/spot) .

## Limitations and requirements

Consider the following limitations and requirements when using Spot VMs with Agent Platform:

  - All [Spot VMs limitations](https://docs.cloud.google.com/compute/docs/instances/spot#limitations) apply when using Spot VMs with Agent Platform.
  - Using Spot VMs with Agent Platform is supported only for serverless training and inference.
  - Using Spot VMs with TPU Pods isn't supported.
  - Submitting your job through the Google Cloud console is not supported.

## Billing

If your workloads are fault-tolerant and can withstand possible VM preemption, Spot VMs can reduce your compute costs significantly. If some of your VMs stop during processing, the job slows but does not completely stop. Spot VMs complete your batch processing tasks without placing additional load on your existing VMs and without requiring you to pay full price for additional standard VMs. See [Preemption handling](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/use-spot-vms#preemption-handling) .

When you use Spot VMs, you're billed by job duration and machine type. You don't pay for the time that the job is in a queue or preempted.

> **Note:** When consuming from a reservation or spot capacity, billing is spread across two SKUs: the Compute Engine SKU with the label `vertex-ai-online-prediction` and the Agent Platform Management Fee SKU. This enables you to use your Committed Use Discounts (CUDs) in Agent Platform.

## Preemption handling

Spot VMs can be reclaimed by Compute Engine at any time. To learn how to get the most out of your Spot VMs, see [Spot VM best practices](https://docs.cloud.google.com/compute/docs/instances/create-use-spot#best-practices) .

## Get inferences by using Spot VMs

To use Spot VMs when you deploy a model to get inferences, you can use the REST API or the Agent Platform SDK for Python.

### REST

Before using any of the request data, make the following replacements:

  - LOCATION\_ID : The region where you are using Agent Platform.
  - PROJECT\_ID : Your \[project ID\](/resource-manager/docs/creating-managing-projects\#identifiers). .
  - ENDPOINT\_ID : The ID for the endpoint.
  - MODEL\_ID : The ID for the model to be deployed.
  - DEPLOYED\_MODEL\_NAME : A name for the `DeployedModel` . You can use the display name of the `Model` for the `DeployedModel` as well.
  - MACHINE\_TYPE : Optional. The machine resources used for each node of this deployment. Its default setting is `n1-standard-2` . [Learn more about machine types.](https://docs.cloud.google.com/vertex-ai/docs/predictions/configure-compute)
  - ACCELERATOR\_TYPE : Optional. The type of accelerator to be attached to the machine. [Learn more](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/configure-compute#gpus) .
  - ACCELERATOR\_COUNT : Optional. The number of accelerators for each replica to use.
  - MIN\_REPLICA\_COUNT : The minimum number of nodes for this deployment. The node count can be increased or decreased as required by the inference load, up to the maximum number of nodes and never fewer than this number of nodes. This value must be greater than or equal to 1.
  - MAX\_REPLICA\_COUNT : The maximum number of nodes for this deployment. The node count can be increased or decreased as required by the inference load, up to this number of nodes and never fewer than the minimum number of nodes.
  - TRAFFIC\_SPLIT\_THIS\_MODEL : The percentage of the prediction traffic to this endpoint to be routed to the model being deployed with this operation. Defaults to 100. All traffic percentages must add up to 100. [Learn more about traffic splits](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/deployment#models-endpoint) .
  - DEPLOYED\_MODEL\_ID\_N : Optional. If other models are deployed to this endpoint, you must update their traffic split percentages so that all percentages add up to 100.
  - TRAFFIC\_SPLIT\_MODEL\_N : The traffic split percentage value for the deployed model id key.
  - PROJECT\_NUMBER : Your project's automatically generated [project number](https://docs.cloud.google.com/resource-manager/docs/creating-managing-projects#identifiers) .

HTTP method and URL:

    POST https://LOCATION_ID-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION_ID/endpoints/ENDPOINT_ID:deployModel

Request JSON body:

    {
    
    
    "acceleratorCount": 1}, "spot": true, "minReplicaCount": 1, "maxReplicaCount": 1}}, "trafficSplit": {"0": 100}}' \
      "https://LOCATION_ID-aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/LOCATION_ID/endpoints/ENDPOINT_ID:deployModel"
    
      "deployedModel": {
        "model": "projects/PROJECT/locations/us-central1/models/MODEL_ID",
        "displayName": "DEPLOYED_MODEL_NAME",
        "enableContainerLogging": true,
        "dedicatedResources": {
          "machineSpec": {
            "machineType": "MACHINE_TYPE",
            "acceleratorType": "ACCELERATOR_TYPE",
            "acceleratorCount": ACCELERATOR_COUNT
          },
          "spot": true,
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
      "name": "projects/PROJECT_ID/locations/LOCATION/endpoints/ENDPOINT_ID/operations/OPERATION_ID",
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

    endpoint5.deploy(
        model = model,
        deployed_model_display_name=DEPLOYED_NAME,
        traffic_split=TRAFFIC_SPLIT,
        machine_type="MACHINE_TYPE",
        accelerator_type="ACCELERATOR_TYPE",
        accelerator_count=ACCELERATOR_COUNT,
        min_replica_count=MIN_REPLICA_COUNT,
        max_replica_count=MAX_REPLICA_COUNT,
        spot=True,
        sync=True
    )

## What's next

  - Learn more about [Spot VMs](https://docs.cloud.google.com/compute/docs/instances/spot) .
  - To learn more about Compute Engine VMs in general, read the [Virtual machine instances](https://docs.cloud.google.com/compute/docs/instances) documentation.
  - To learn how to create Spot VMs, read [Create and use Spot VMs](https://docs.cloud.google.com/compute/docs/instances/create-use-spot) .
  - [Use Spot VMs with Agent Platform training](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/use-spot-vms) .
  - [Use Flex-start VMs with Agent Platform inference](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/use-flex-start-vms) .
