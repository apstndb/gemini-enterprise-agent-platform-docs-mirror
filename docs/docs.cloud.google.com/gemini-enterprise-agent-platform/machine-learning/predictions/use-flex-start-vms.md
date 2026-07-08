---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/use-flex-start-vms
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/use-flex-start-vms
title: Use Flex-start VMs with inference
description: Use Flex-start VMs with Agent Platform inference.
data_source: docs.cloud.google.com
---

> **Preview**
> 
> This feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](https://docs.cloud.google.com/terms/service-terms#1) . Pre-GA features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

This guide describes the benefits and limitations of using Flex-start VMs with Gemini Enterprise Agent Platform inference. This guide also describes how to deploy a model that uses Flex-start VMs.

## Overview

You can reduce the cost of running your inference jobs by using Flex-start VMs, which are powered by [Dynamic Workload Scheduler](https://cloud.google.com/blog/products/compute/introducing-dynamic-workload-scheduler) . Flex-start VMs offer significant discounts and are well-suited for short-duration workloads.

You can specify how long you need a Flex-start VM, for any duration up to seven days. After the requested time expires, your deployed model is automatically undeployed. You can also manually undeploy the model before the time expires.

## Automatic undeployment

If you request a Flex-start VM for a specific duration, your model is automatically undeployed after that time period. For example, if you request a Flex-start VM for five hours, the model is automatically undeployed five hours after submission. You are only charged for the amount of time your workload is running.

## Limitations and requirements

Consider the following limitations and requirements when you use Flex-start VMs:

  - **Maximum duration** : Flex-start VMs have a maximum usage duration of seven days. Any deployment request for a longer duration will be rejected.
  - **TPU support** : Using Flex-start VMs with TPU Pods isn't supported.
  - **Quota** : Make sure you have sufficient Agent Platform preemptible quota before launching your job. To learn more, see [Rate quotas](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/quotas#serving) .
  - **Queued provisioning** : Using Flex-start VMs with queued provisioning isn't supported.
  - **Node recycling** : Node recycling isn't supported.

## Billing

If your workload runs for less than seven days, using Flex-start VMs can reduce your costs.

When you use Flex-start VMs, you're billed based on the duration of your job and the machine type that you select. You are only charged for the time your workload is actively running. You don't pay for the time that the job is in a queue or for any time after the requested duration has expired.

Billing is distributed across two SKUs:

  - The Compute Engine SKU, with the label `vertex-ai-online-prediction` . See [Dynamic Workload Scheduler pricing](https://cloud.google.com/products/dws/pricing) .

  - The Agent Platform management fee SKU. See [Agent Platform pricing](https://cloud.google.com/products/gemini-enterprise-agent-platform/pricing#prediction) .

## Get inferences by using Flex-start VMs

To use Flex-start VMs when you deploy a model to get inferences, you can use the REST API.

Before using any of the request data, make the following replacements:

  - LOCATION\_ID : The region where you are using Agent Platform.
  - PROJECT\_ID : Your \[project ID\](/resource-manager/docs/creating-managing-projects\#identifiers). .
  - ENDPOINT\_ID : The ID for the endpoint.
  - MODEL\_ID : The ID for the model to be deployed.
  - DEPLOYED\_MODEL\_NAME : A name for the `DeployedModel` . You can use the display name of the `Model` for the `DeployedModel` as well.
  - MACHINE\_TYPE : Optional. The machine resources used for each node of this deployment. Its default setting is `n1-standard-2` . [Learn more about machine types.](https://docs.cloud.google.com/gemini-enterprise-agent-platform/predictions/configure-compute)
  - ACCELERATOR\_TYPE : Optional. The type of accelerator to attach to the machine. [Learn more](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/configure-compute#gpus) .
  - ACCELERATOR\_COUNT : Optional. The number of accelerators for each replica to use.
  - MAX\_RUNTIME\_DURATION : The maximum duration for the flex-start deployment. The deployed model is automatically undeployed after this duration. Specify the duration in seconds, ending with an `s` . For example, `3600s` for one hour. The maximum value is `604800s` (7 days).
  - PROJECT\_NUMBER : Your project's automatically generated [project number](https://docs.cloud.google.com/resource-manager/docs/creating-managing-projects#identifiers) .

HTTP method and URL:

    POST https://LOCATION-aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/LOCATION/endpoints/ENDPOINT_ID:deployModel

Request JSON body:

    {
      "deployedModel": {
        "model": "projects/PROJECT/locations/LOCATION/models/MODEL_ID",
        "displayName": "DEPLOYED_MODEL_NAME",
        "enableContainerLogging": true,
        "dedicatedResources": {
          "machineSpec": {
            "machineType": "MACHINE_TYPE",
            "acceleratorType": "ACCELERATOR_TYPE",
            "acceleratorCount": ACCELERATOR_COUNT
          },
          "flexStart": {
            "maxRuntimeDuration": "MAX_RUNTIME_DURATION"
          },
          "minReplicaCount": 2,
          "maxReplicaCount": 2
        },
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
         "https://LOCATION-aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/LOCATION/endpoints/ENDPOINT_ID:deployModel"

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
        -Uri "https://LOCATION-aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/LOCATION/endpoints/ENDPOINT_ID:deployModel" | Select-Object -Expand Content

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

## What's next

  - [Use Spot VMs with Agent Platform inference](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/use-spot-vms) .

  - [Use reservations with Agent Platform inference](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/use-reservations) .
