---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/configure-compute
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/configure-compute
title: Configure compute resources for inference
description: Learn about the different compute resources that you can use for Agent Platform inference and how to configure them.
data_source: docs.cloud.google.com
---

Agent Platform allocates *nodes* to handle online and batch inferences. When you [deploy a custom-trained model or AutoML model to an `Endpoint` resource to serve online inferences](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/deploy-model-console) or when you [request batch inferences](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/batch-predictions) , you can customize the type of virtual machine that the inference service uses for these nodes. You can optionally configure inference nodes to use GPUs.

*Machine types* differ in a few ways:

  - Number of virtual CPUs (vCPUs) per node
  - Amount of memory per node
  - [Pricing](https://docs.cloud.google.com/gemini-enterprise-agent-platform/pricing)

By selecting a machine type with more computing resources, you can serve inferences with lower latency or handle more inference requests at the same time.

## Manage cost and availability

To help manage costs or ensure availability of VM resources, Agent Platform provides the following:

  - To help ensure that you pay only for the computing resources that you need, you can use Vertex AI Inference autoscaling. For more information, see [Scale inference nodes for Vertex AI Inference](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/autoscaling) .

  - To make sure that VM resources are available when your inference jobs need them, you can use Compute Engine reservations. Reservations provide a high level of assurance in obtaining capacity for Compute Engine resources. For more information, see [Use reservations with inference](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/use-reservations) .

  - To reduce the cost of running your inference jobs, you can use Spot VMs. Spot VMs are virtual machine (VM) instances that are excess Compute Engine capacity. Spot VMs have significant discounts, but Compute Engine might preemptively stop or delete Spot VMs to reclaim the capacity at any time. For more information, see [Use Spot VMs with inference](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/use-spot-vms) .

## Where to specify compute resources

### Online inference

If you want to use a custom-trained model or an AutoML tabular model to serve online inferences, you must specify a machine type when you deploy the `Model` resource as a `DeployedModel` to an `Endpoint` . For other types of AutoML models, Agent Platform configures the machine types automatically.

Specify the machine type (and, optionally, GPU configuration) in the [`dedicatedResources.machineSpec` field of your `DeployedModel`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.endpoints#deployedmodel) .

Learn how to deploy each model type:

  - [Deploy an AutoML tabular model in Google Cloud console](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/deploy-model-console)
  - [Deploy a custom-trained model in Google Cloud console](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tutorials/image-classification-custom/serving#1_create_an_endpoint)
  - [Deploy a custom-trained model using client libraries](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/deploy-model-api)

### Batch inference

If you want to get batch inferences from a custom-trained model or an AutoML tabular model, you must specify a machine type when you [create a `BatchPredictionJob` resource](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/batch-predictions) . Specify the machine type (and, optionally, GPU configuration) in the [`dedicatedResources.machineSpec` field of your `BatchPredictionJob`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.batchPredictionJobs) .

<span id="machine_type_comparison"></span>

## Machine types

The following tables compare the available machine types for serving inferences from custom-trained models and AutoML tabular models.

For information about TPU accelerator types, see [Deploy a model to Cloud TPU VMs](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/use-tpu) .

### Machine types: CPU

### E2 Series

| Name             | vCPUs | Memory (GB) |
| ---------------- | ----- | ----------- |
| `e2-standard-2`  | 2     | 8           |
| `e2-standard-4`  | 4     | 16          |
| `e2-standard-8`  | 8     | 32          |
| `e2-standard-16` | 16    | 64          |
| `e2-standard-32` | 32    | 128         |
| `e2-highmem-2`   | 2     | 16          |
| `e2-highmem-4`   | 4     | 32          |
| `e2-highmem-8`   | 8     | 64          |
| `e2-highmem-16`  | 16    | 128         |
| `e2-highcpu-2`   | 2     | 2           |
| `e2-highcpu-4`   | 4     | 4           |
| `e2-highcpu-8`   | 8     | 8           |
| `e2-highcpu-16`  | 16    | 16          |
| `e2-highcpu-32`  | 32    | 32          |

### N1 Series

| Name             | vCPUs | Memory (GB) |
| ---------------- | ----- | ----------- |
| `n1-standard-2`  | 2     | 7.5         |
| `n1-standard-4`  | 4     | 15          |
| `n1-standard-8`  | 8     | 30          |
| `n1-standard-16` | 16    | 60          |
| `n1-standard-32` | 32    | 120         |
| `n1-highmem-2`   | 2     | 13          |
| `n1-highmem-4`   | 4     | 26          |
| `n1-highmem-8`   | 8     | 52          |
| `n1-highmem-16`  | 16    | 104         |
| `n1-highmem-32`  | 32    | 208         |
| `n1-highcpu-4`   | 4     | 3.6         |
| `n1-highcpu-8`   | 8     | 7.2         |
| `n1-highcpu-16`  | 16    | 14.4        |
| `n1-highcpu-32`  | 32    | 28.8        |

### N2 Series

| Name              | vCPUs | Memory (GB) |
| ----------------- | ----- | ----------- |
| `n2-standard-2`   | 2     | 8           |
| `n2-standard-4`   | 4     | 16          |
| `n2-standard-8`   | 8     | 32          |
| `n2-standard-16`  | 16    | 64          |
| `n2-standard-32`  | 32    | 128         |
| `n2-standard-48`  | 48    | 192         |
| `n2-standard-64`  | 64    | 256         |
| `n2-standard-80`  | 80    | 320         |
| `n2-standard-96`  | 96    | 384         |
| `n2-standard-128` | 128   | 512         |
| `n2-highmem-2`    | 2     | 16          |
| `n2-highmem-4`    | 4     | 32          |
| `n2-highmem-8`    | 8     | 64          |
| `n2-highmem-16`   | 16    | 128         |
| `n2-highmem-32`   | 32    | 256         |
| `n2-highmem-48`   | 48    | 384         |
| `n2-highmem-64`   | 64    | 512         |
| `n2-highmem-80`   | 80    | 640         |
| `n2-highmem-96`   | 96    | 768         |
| `n2-highmem-128`  | 128   | 864         |
| `n2-highcpu-2`    | 2     | 2           |
| `n2-highcpu-4`    | 4     | 4           |
| `n2-highcpu-8`    | 8     | 8           |
| `n2-highcpu-16`   | 16    | 16          |
| `n2-highcpu-32`   | 32    | 32          |
| `n2-highcpu-48`   | 48    | 48          |
| `n2-highcpu-64`   | 64    | 64          |
| `n2-highcpu-80`   | 80    | 80          |
| `n2-highcpu-96`   | 96    | 96          |

### N2D Series

| Name               | vCPUs | Memory (GB) |
| ------------------ | ----- | ----------- |
| `n2d-standard-2`   | 2     | 8           |
| `n2d-standard-4`   | 4     | 16          |
| `n2d-standard-8`   | 8     | 32          |
| `n2d-standard-16`  | 16    | 64          |
| `n2d-standard-32`  | 32    | 128         |
| `n2d-standard-48`  | 48    | 192         |
| `n2d-standard-64`  | 64    | 256         |
| `n2d-standard-80`  | 80    | 320         |
| `n2d-standard-96`  | 96    | 384         |
| `n2d-standard-128` | 128   | 512         |
| `n2d-standard-224` | 224   | 896         |
| `n2d-highmem-2`    | 2     | 16          |
| `n2d-highmem-4`    | 4     | 32          |
| `n2d-highmem-8`    | 8     | 64          |
| `n2d-highmem-16`   | 16    | 128         |
| `n2d-highmem-32`   | 32    | 256         |
| `n2d-highmem-48`   | 48    | 384         |
| `n2d-highmem-64`   | 64    | 512         |
| `n2d-highmem-80`   | 80    | 640         |
| `n2d-highmem-96`   | 96    | 768         |
| `n2d-highcpu-2`    | 2     | 2           |
| `n2d-highcpu-4`    | 4     | 4           |
| `n2d-highcpu-8`    | 8     | 8           |
| `n2d-highcpu-16`   | 16    | 16          |
| `n2d-highcpu-32`   | 32    | 32          |
| `n2d-highcpu-48`   | 48    | 48          |
| `n2d-highcpu-64`   | 64    | 64          |
| `n2d-highcpu-80`   | 80    | 80          |
| `n2d-highcpu-96`   | 96    | 96          |
| `n2d-highcpu-128`  | 128   | 128         |
| `n2d-highcpu-224`  | 224   | 224         |

### C2 Series

| Name             | vCPUs | Memory (GB) |
| ---------------- | ----- | ----------- |
| `c2-standard-4`  | 4     | 16          |
| `c2-standard-8`  | 8     | 32          |
| `c2-standard-16` | 16    | 64          |
| `c2-standard-30` | 30    | 120         |
| `c2-standard-60` | 60    | 240         |

### C2D Series

| Name               | vCPUs | Memory (GB) |
| ------------------ | ----- | ----------- |
| `c2d-standard-2`   | 2     | 8           |
| `c2d-standard-4`   | 4     | 16          |
| `c2d-standard-8`   | 8     | 32          |
| `c2d-standard-16`  | 16    | 64          |
| `c2d-standard-32`  | 32    | 128         |
| `c2d-standard-56`  | 56    | 224         |
| `c2d-standard-112` | 112   | 448         |
| `c2d-highcpu-2`    | 2     | 4           |
| `c2d-highcpu-4`    | 4     | 8           |
| `c2d-highcpu-8`    | 8     | 16          |
| `c2d-highcpu-16`   | 16    | 32          |
| `c2d-highcpu-32`   | 32    | 64          |
| `c2d-highcpu-56`   | 56    | 112         |
| `c2d-highcpu-112`  | 112   | 224         |
| `c2d-highmem-2`    | 2     | 16          |
| `c2d-highmem-4`    | 4     | 32          |
| `c2d-highmem-8`    | 8     | 64          |
| `c2d-highmem-16`   | 16    | 128         |
| `c2d-highmem-32`   | 32    | 256         |
| `c2d-highmem-56`   | 56    | 448         |
| `c2d-highmem-112`  | 112   | 896         |

### C3 Series

| Name             | vCPUs | Memory (GB) |
| ---------------- | ----- | ----------- |
| `c3-highcpu-4`   | 4     | 8           |
| `c3-highcpu-8`   | 8     | 16          |
| `c3-highcpu-22`  | 22    | 44          |
| `c3-highcpu-44`  | 44    | 88          |
| `c3-highcpu-88`  | 88    | 176         |
| `c3-highcpu-176` | 176   | 352         |

### Machine types: GPU

### A2 Series

| Name             | vCPUs | Memory (GB) | GPUs ( [NVIDIA A100](https://docs.cloud.google.com/compute/docs/gpus#a100-gpus) ) |
| ---------------- | ----- | ----------- | --------------------------------------------------------------------------------- |
| `a2-highgpu-1g`  | 12    | 85          | 1 (A100 40GB)                                                                     |
| `a2-highgpu-2g`  | 24    | 170         | 2 (A100 40GB)                                                                     |
| `a2-highgpu-4g`  | 48    | 340         | 4 (A100 40GB)                                                                     |
| `a2-highgpu-8g`  | 96    | 680         | 8 (A100 40GB)                                                                     |
| `a2-megagpu-16g` | 96    | 1360        | 16 (A100 40GB)                                                                    |
| `a2-ultragpu-1g` | 12    | 170         | 1 (A100 80GB)                                                                     |
| `a2-ultragpu-2g` | 24    | 340         | 2 (A100 80GB)                                                                     |
| `a2-ultragpu-4g` | 48    | 680         | 4 (A100 80GB)                                                                     |
| `a2-ultragpu-8g` | 96    | 1360        | 8 (A100 80GB)                                                                     |

### A3 Series

| Name             | vCPUs | Memory (GB) | GPUs ( [NVIDIA H100 or H200](https://docs.cloud.google.com/compute/docs/gpus#a3-series) ) |
| ---------------- | ----- | ----------- | ----------------------------------------------------------------------------------------- |
| `a3-highgpu-1g`  | 26    | 234         | 1 (H100 80GB)                                                                             |
| `a3-highgpu-2g`  | 52    | 468         | 2 (H100 80GB)                                                                             |
| `a3-highgpu-4g`  | 104   | 936         | 4 (H100 80GB)                                                                             |
| `a3-highgpu-8g`  | 208   | 1872        | 8 (H100 80GB)                                                                             |
| `a3-edgegpu-8g`  | 208   | 1872        | 8 (H100 80GB)                                                                             |
| `a3-ultragpu-8g` | 224   | 2952        | 8 (H200 141GB)                                                                            |

### A4 Series

| Name            | vCPUs | Memory (GB) | GPUs ( [NVIDIA B200](https://docs.cloud.google.com/compute/docs/gpus#b200-gpus) ) |
| --------------- | ----- | ----------- | --------------------------------------------------------------------------------- |
| `a4-highgpu-8g` | 224   | 3,968       | 8                                                                                 |

### A4X Series

| Name             | vCPUs | Memory (GB) | GPUs ( [NVIDIA GB200](https://docs.cloud.google.com/compute/docs/gpus#gb200-gpus) ) |
| ---------------- | ----- | ----------- | ----------------------------------------------------------------------------------- |
| `a4x-highgpu-4g` | 140   | 884         | 4                                                                                   |

### G2 Series

| Name             | vCPUs | Memory (GB) | GPUs ( [NVIDIA L4](https://docs.cloud.google.com/compute/docs/gpus#l4-gpus) ) |
| ---------------- | ----- | ----------- | ----------------------------------------------------------------------------- |
| `g2-standard-4`  | 4     | 16          | 1                                                                             |
| `g2-standard-8`  | 8     | 32          | 1                                                                             |
| `g2-standard-12` | 12    | 48          | 1                                                                             |
| `g2-standard-16` | 16    | 64          | 1                                                                             |
| `g2-standard-24` | 24    | 96          | 2                                                                             |
| `g2-standard-32` | 32    | 128         | 1                                                                             |
| `g2-standard-48` | 48    | 192         | 4                                                                             |
| `g2-standard-96` | 96    | 384         | 8                                                                             |

### G4 Series

| Name              | vCPUs | Memory (GB) | GPUs ( [NVIDIA RTX PRO 6000](https://docs.cloud.google.com/compute/docs/gpus#rtx-6000-gpus) ) |
| ----------------- | ----- | ----------- | --------------------------------------------------------------------------------------------- |
| `g4-standard-48`  | 48    | 180         | 1                                                                                             |
| `g4-standard-96`  | 96    | 360         | 2                                                                                             |
| `g4-standard-192` | 192   | 720         | 4                                                                                             |
| `g4-standard-384` | 384   | 1440        | 8                                                                                             |

Learn about [pricing for each machine type](https://cloud.google.com/gemini-enterprise-agent-platform/generative-ai/pricing) . Read more about the detailed specifications of these machine types in the [Compute Engine documentation about machine types](https://docs.cloud.google.com/compute/docs/machine-resource) .

### Find the ideal machine type

#### Online inference

To find the ideal machine type for your use case, we recommend loading your model on multiple machine types and measuring characteristics such as the latency, cost, concurrency, and throughput.

One way to do this is to run [this notebook](https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/community/vertex_endpoints/find_ideal_machine_type/find_ideal_machine_type.ipynb) on multiple machine types and compare the results to find the one that works best for you.

Gemini Enterprise Agent Platform reserves approximately 1 vCPU on each replica for running system processes. This means that running the notebook on a single core machine type would be comparable to using a 2-core machine type for serving inferences.

When considering inference costs, remember that although larger machines cost more, they can lower overall cost because fewer replicas are required to serve the same workload. This is particularly evident for GPUs, which tend to cost more per hour, but can both provide lower latency and cost less overall.

#### Batch inference

For more information, see [Choose machine type and replica count](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/get-batch-predictions#choose_machine_type_and_replica_count) .

## Optional GPU accelerators

> **Caution:** The [Gemini Enterprise Agent Platform Service Level Agreement (SLA)](https://cloud.google.com/vertex-ai/sla?e=48754805) doesn't apply to the A4X machine series.

Some configurations, such as the [A2 series](https://docs.cloud.google.com/compute/docs/accelerator-optimized-machines#a2-vms) and [G2 series](https://docs.cloud.google.com/compute/docs/accelerator-optimized-machines#g2-vms) , have a fixed number of GPUs built-in.

The [A4X ( `a4x-highgpu-4g` )](https://docs.cloud.google.com/compute/docs/accelerator-optimized-machines#a4x-vms) series requires a minimum replica count of 18. This machine is purchased per rack, and has a minimum of 18 VMs.

Other configurations, such as the N1 series, let you optionally add GPUs to accelerate each inference node.

> **Note:** GPUs are **not** recommended for use with AutoML tabular models. For this type of model, GPUs don't provide a worthwhile performance benefit. Specifying GPUs during AutoML model deployment isn't supported in Google Cloud console.

To add optional GPU accelerators, you must account for several requirements:

  - You can only use GPUs when your `Model` resource is based on a [TensorFlow SavedModel](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/training/exporting-model-artifacts) , or when you [use a custom container](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/use-custom-container) that has been designed to take advantage of GPUs. You can't use GPUs for scikit-learn or XGBoost models.
  - The availability of each type of GPU varies depending on which region you use for your model. Learn [which types of GPUs are available in which regions](https://docs.cloud.google.com/vertex-ai/docs/general/locations#accelerators) .
  - You can only use one type of GPU for your `DeployedModel` resource or `BatchPredictionJob` , and there are limitations on the number of GPUs you can add depending on which machine type you are using. The following table describes these limitations.

The following table shows the optional GPUs that are available for online inference and how many of each type of GPU you can use with each Compute Engine machine type:

Valid numbers of GPUs for each machine type

Machine type

[NVIDIA Tesla P100](https://docs.cloud.google.com/compute/docs/gpus#p100-gpus)

[NVIDIA Tesla V100](https://docs.cloud.google.com/compute/docs/gpus#v100-gpus)

[NVIDIA Tesla P4](https://docs.cloud.google.com/compute/docs/gpus#p4-gpus)

[NVIDIA Tesla T4](https://docs.cloud.google.com/compute/docs/gpus#t4-gpus)

`n1-standard-2`

1, 2, 4

1, 2, 4, 8

1, 2, 4

1, 2, 4

`n1-standard-4`

1, 2, 4

1, 2, 4, 8

1, 2, 4

1, 2, 4

`n1-standard-8`

1, 2, 4

1, 2, 4, 8

1, 2, 4

1, 2, 4

`n1-standard-16`

1, 2, 4

2, 4, 8

1, 2, 4

1, 2, 4

`n1-standard-32`

2, 4

4, 8

2, 4

2, 4

`n1-highmem-2`

1, 2, 4

1, 2, 4, 8

1, 2, 4

1, 2, 4

`n1-highmem-4`

1, 2, 4

1, 2, 4, 8

1, 2, 4

1, 2, 4

`n1-highmem-8`

1, 2, 4

1, 2, 4, 8

1, 2, 4

1, 2, 4

`n1-highmem-16`

1, 2, 4

2, 4, 8

1, 2, 4

1, 2, 4

`n1-highmem-32`

2, 4

4, 8

2, 4

2, 4

`n1-highcpu-2`

1, 2, 4

1, 2, 4, 8

1, 2, 4

1, 2, 4

`n1-highcpu-4`

1, 2, 4

1, 2, 4, 8

1, 2, 4

1, 2, 4

`n1-highcpu-8`

1, 2, 4

1, 2, 4, 8

1, 2, 4

1, 2, 4

`n1-highcpu-16`

1, 2, 4

2, 4, 8

1, 2, 4

1, 2, 4

`n1-highcpu-32`

2, 4

4, 8

2, 4

2, 4

Optional GPUs incur [additional costs](https://docs.cloud.google.com/gemini-enterprise-agent-platform/pricing) .

## Coschedule multiple replicas on a single VM

To optimize the cost of your deployment, you can deploy multiple replicas of the same model onto a single VM equipped with multiple GPU hardware accelerators, such as the `a3-highgpu-8g` VM, which has eight NVIDIA H100 GPUs. Each model replica can be assigned to one or more GPUs.

For smaller workloads, you can also partition a single GPU into multiple smaller instances using [NVIDIA multi-instance GPUs (MIG)](https://docs.cloud.google.com/kubernetes-engine/docs/how-to/gpus-multi) . This lets you assign resources at a sub-GPU level, maximizing the utilization of each accelerator. For more information on multi-instance GPUs, see the [NVIDIA multi-instance GPU user guide](https://docs.nvidia.com/datacenter/tesla/mig-user-guide/index.html) .

Both of these capabilities are designed to provide more efficient resource utilization and greater cost-effectiveness for your serving workloads.

### Limitations

This feature is subject to the following limitations:

  - All of the coscheduled model replicas must be the same model version.
  - Using [deployment resource pools](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/model-co-hosting) to share resources across deployments isn't supported.

### Supported machine types

The following machine types are supported. Note that, for machine types that only have one GPU, no coscheduling is needed.

| Machine type    | Coschedule | Coschedule + MIG |
| --------------- | ---------- | ---------------- |
| a2-highgpu-1g   | N/A        | Yes              |
| a2-highgpu-2g   | Yes        | Yes              |
| a2-highgpu-4g   | Yes        | Yes              |
| a2-highgpu-8g   | Yes        | Yes              |
| a2-highgpu-16g  | Yes        | Yes              |
| a2-ultragpu-1g  | N/A        | Yes              |
| a2-ultragpu-2g  | Yes        | Yes              |
| a2-ultragpu-4g  | Yes        | Yes              |
| a2-ultragpu-8g  | Yes        | Yes              |
| a3-edgegpu-8g   | Yes        | Yes              |
| a3-highgpu-1g   | N/A        | Yes              |
| a3-highgpu-2g   | Yes        | Yes              |
| a3-highgpu-4g   | Yes        | Yes              |
| a3-highgpu-8g   | Yes        | Yes              |
| a3-megagpu-8g   | Yes        | Yes              |
| a3-ultragpu-8g  | Yes        | Yes              |
| a4-highgpu-8g   | Yes        | Yes              |
| a4x-highgpu-8g  | Yes        | Yes              |
| g4-standard-48  | N/A        | Yes              |
| g4-standard-96  | Yes        | Yes              |
| g4-standard-192 | Yes        | Yes              |
| g4-standard-384 | Yes        | Yes              |

### Prerequisites

Before using this feature, read [Deploy a model by using the gcloud CLI or Agent Platform API](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/deploy-model-api) .

### Deploying the model replicas

The following samples demonstrate how to deploy coscheduled model replicas.

> **Note:** In this preview, NVIDIA MIG is supported for Agent Platform API and REST API, but not for Google Cloud CLI.

> **Note:** When MIG is enabled, you can't use GPU sharing, because each replica is limited to consuming MIG in a single GPU instance. Therefore, the `accelerator_count` must be set to 1 when a `gpu_partition_size` is specified.

### gcloud

Use the following `gcloud` command to deploy coscheduled model replicas on a VM:

    gcloud ai endpoints deploy-model ENDPOINT_ID \
      --region=LOCATION_ID \
      --model=MODEL_ID \
      --display-name=DEPLOYED_MODEL_NAME \
      --min-replica-count=MIN_REPLICA_COUNT \
      --max-replica-count=MAX_REPLICA_COUNT \
      --machine-type=MACHINE_TYPE \
      --accelerator=type=ACC_TYPE,count=ACC_COUNT \
      --traffic-split=0=100

Replace the following:

  - ENDPOINT\_ID : The ID for the endpoint.
  - LOCATION\_ID : The region where you are using Agent Platform.
  - MODEL\_ID : The model ID for the model to be deployed.
  - DEPLOYED\_MODEL\_NAME : A name for the `DeployedModel` . You can use the display name of the `Model` for the `DeployedModel` as well.
  - MIN\_REPLICA\_COUNT : The minimum number of nodes for this deployment. The node count can be increased or decreased as required by the inference load, up to the maximum number of nodes and never fewer than this number of nodes.
  - MAX\_REPLICA\_COUNT : The maximum number of nodes for this deployment. The node count can be increased or decreased as required by the inference load, up to this number of nodes and never fewer than the minimum number of nodes. . One VM is required for every 2 replicas to be deployed.
  - MACHINE\_TYPE : The type of VM to use for this deployment. Must be from the accelerator-optimized family.
  - ACC\_TYPE : The GPU accelerator type. Should correspond to the MACHINE\_TYPE . For `a3-highgpu-8g` , use `nvidia-h100-80gb` .
  - ACC\_COUNT : The number of GPUs that each replica can use. Must be at least 1 and no more than the total number of GPUs in the machine.

### REST

Before using any of the request data, make the following replacements:

  - PROJECT\_NUMBER : The project number.
  - LOCATION\_ID : The region where you are using Agent Platform.
  - MODEL\_ID : The ID for the model to be deployed.
  - DEPLOYED\_MODEL\_NAME : A name for the `DeployedModel` . You can use the display name of the `Model` for the `DeployedModel` as well.
  - MACHINE\_TYPE : Optional. The machine resources used for each node of this deployment. Its default setting is `n1-standard-2` . [Learn more about machine types.](https://docs.cloud.google.com/vertex-ai/docs/predictions/configure-compute)
  - ACC\_TYPE : The GPU accelerator type. Should correspond to the \`GPU\_PARTITION\_SIZE\`.
  - GPU\_PARTITION\_SIZE : The GPU partition size. For example, "1g.10gb".
  - ACC\_COUNT : The number of GPUs that each replica can use. Must be at least 1 and no more than the total number of GPUs in the machine.
  - MIN\_REPLICA\_COUNT : The minimum number of nodes for this deployment. The node count can be increased or decreased as required by the inference load, up to the maximum number of nodes and never fewer than this number of nodes.
  - MAX\_REPLICA\_COUNT : The maximum number of nodes for this deployment. The node count can be increased or decreased as required by the inference load, up to this number of nodes and never fewer than the minimum number of nodes.

HTTP method and URL:

    POST https://LOCATION_ID-aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/LOCATION_ID/endpoints/ENDPOINT_ID:deployModel

Request JSON body:

    {
      "deployedModel": {
        "model": "projects/PROJECT_NUMBER/locations/LOCATION_ID/models/MODEL_ID",
        "displayName": "DEPLOYED_MODEL_NAME",
        "dedicatedResources": {
          "machineSpec": {
            "machineType": "MACHINE_TYPE",
            "acceleratorType": "ACC_TYPE",
            "gpuPartitionSize": "GPU_PARTITION_SIZE",
            "acceleratorCount": "ACC_COUNT""
          },
          "minReplicaCount": MIN_REPLICA_COUNT,
          "maxReplicaCount": MAX_REPLICA_COUNT,
          "autoscalingMetricSpecs": [
            {
              "metricName": "aiplatform.googleapis.com/prediction/online/accelerator/duty_cycle",
              "target": 70
            }
          ]
        }
      }
    }

To send your request, expand one of these options:

#### curl (Linux, macOS, or Cloud Shell)

Save the request body in a file named `request.json` , and execute the following command:

    curl -X POST \
         -H "Content-Type: application/json; charset=utf-8" \
         -d @request.json \
         "https://LOCATION_ID-aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/LOCATION_ID/endpoints/ENDPOINT_ID:deployModel"

#### PowerShell (Windows)

Save the request body in a file named `request.json` , and execute the following command:

    $headers = @{  }
    
    Invoke-WebRequest `
        -Method POST `
        -Headers $headers `
        -ContentType: "application/json; charset=utf-8" `
        -InFile request.json `
        -Uri "https://LOCATION_ID-aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/LOCATION_ID/endpoints/ENDPOINT_ID:deployModel" | Select-Object -Expand Content

You should receive a successful status code (2xx) and an empty response.

### Python

To learn how to install or update the Vertex AI SDK for Python, see [Install the Vertex AI SDK for Python](https://docs.cloud.google.com/vertex-ai/docs/start/use-vertex-ai-python-sdk) . For more information, see the [Python API reference documentation](https://docs.cloud.google.com/python/docs/reference/aiplatform/latest) .

Use the following Python command to deploy coscheduled model replicas on a VM.

    endpoint.deploy(
        model=<var>MODEL</var>,
        machine_type=MACHINE_TYPE,
        min_replica_count=MIN_REPLICA_COUNT,
        max_replica_count=MAX_REPLICA_COUNT,
        accelerator_type=ACC_TYPE,
        gpu_partition_size=GPU_PARTITION_SIZE,
        accelerator_count=ACC_COUNT
    )

Replace the following:

  - MODEL : The model object returned by the [following API call](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/deploy-model-api#aiplatform_deploy_model_custom_trained_model_sample-python_vertex_ai_sdk) :
    
        model = aiplatform.Model(model_name=model_name)

  - MACHINE\_TYPE : The type of VM to use for this deployment. Must be from the accelerator-optimized family. In the preview, only `a3-highgpu-8g` is supported.

  - MIN\_REPLICA\_COUNT : The minimum number of nodes for this deployment. The node count can be increased or decreased as required by the inference load, up to the maximum number of nodes and never fewer than this number of nodes.

  - MAX\_REPLICA\_COUNT : The maximum number of nodes for this deployment. The node count can be increased or decreased as required by the inference load, up to this number of nodes and never fewer than the minimum number of nodes.

  - ACC\_TYPE : The GPU accelerator type. Should correspond to the GPU\_PARTITION\_SIZE .

  - GPU\_PARTITION\_SIZE : The GPU partition size. For example, `"1g.10gb"` . For a comprehensive list of supported partition sizes for each GPU type, see [Multi-instance GPU partitions](https://docs.cloud.google.com/kubernetes-engine/docs/how-to/gpus-multi#multi-instance_gpu_partitions) .

  - ACC\_COUNT : The number of GPUs that each replica can use. Must be at least 1 and no more than the total number of GPUs in the machine. For `a3-highgpu-8g` , specify between 1 and 8.

### Monitor VM usage

Use the following instructions to monitor the actual machine count for your deployed replicas in the Metrics Explorer.

1.  In the Google Cloud console, go to the **Metrics Explorer** page.

2.  Select the project you want to view metrics for.

3.  From the **Metric** drop-down menu, click **Select a metric** .

4.  In the **Filter by resource or metric name** search bar, enter `Gemini Enterprise Agent Platform Endpoint` .

5.  Select the **Agent Platform Endpoint \> Prediction** metric category. Under **Active metrics** , select **Machine count** .

6.  Click **Apply** .

### Billing

Billing is based on the number of VMs that are used, not the number of GPUs. You can [monitor your VM usage by using Metrics Explorer](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/configure-compute#monitor-usage) .

### High availability

Because more than one replica is being coscheduled on the same VM, Vertex AI Inference cannot spread your deployment across multiple VMs and therefore multiple zones until your replica count exceeds the single VM node. For high availability purposes, Google recommends deploying on at least two nodes (VMs).

## What's next

  - [Deploy an AutoML tabular model in Google Cloud console](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/deploy-model-console)
  - [Deploy a custom-trained model in Google Cloud console](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/tutorials/image-recognition-custom/serving#1_create_an_endpoint)
  - [Deploy a custom-trained model using client libraries](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/deploy-model-api)
  - [Get batch inferences](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/predictions/batch-predictions)
